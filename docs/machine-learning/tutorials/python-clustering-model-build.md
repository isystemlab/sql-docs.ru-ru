---
title: Учебник по Python. Создание кластерной модели
titleSuffix: SQL machine learning
description: В третьей части этого цикла учебников из четырех частей вы создадите модель k-средних для кластеризации в Python с использованием машинного обучения SQL.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 05/21/2020
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 144463853d677ee61e2d860caf975275dcd0a607
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/13/2020
ms.locfileid: "88173449"
---
# <a name="python-tutorial-build-a-model-to-categorize-customers-with-sql-machine-learning"></a>Учебник по Python. Создание модели для классификации клиентов с использованием машинного обучения SQL
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
В третьей части этого учебника из четырех частей вы создадите модель K-средних для кластеризации в Python. В следующей части данного цикла вы развернете эту модель в базе данных с использованием Служб машинного обучения SQL Server.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
В третьей части этого учебника из четырех частей вы создадите модель K-средних для кластеризации в Python. В следующей части данного цикла вы развернете эту модель в базе данных с использованием Служб машинного обучения SQL Server.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
В третьей части этого учебника из четырех частей вы создадите модель K-средних для кластеризации в Python. В следующей части из этой серии описывается, как развернуть эту модель в базе данных с помощью Служб машинного обучения в управляемом экземпляре SQL Azure.
::: moniker-end

В этой статье вы узнаете, как выполнять следующие задачи.

> [!div class="checklist"]
> * Определение числа кластеров для алгоритма K-средних
> * Выполнение кластеризации
> * Анализ результатов

В [первой части](python-clustering-model.md) были установлены необходимые компоненты и восстановлена демонстрационная база данных.

Во [второй части](python-clustering-model-prepare-data.md) вы узнали, как подготовить данные из базы данных для выполнения кластеризации.

В [четвертой части](python-clustering-model-deploy.md) вы узнаете, как создать в базе данных хранимую процедуру, которая может выполнять кластеризацию в Python на основе новых данных.

## <a name="prerequisites"></a>Предварительные требования

* В третьей части этого учебника предполагается, что вы уже выполнили предварительные требования [**первой части**](python-clustering-model.md), а также действия, указанные во [**второй части**](python-clustering-model-prepare-data.md).

## <a name="define-the-number-of-clusters"></a>Определение числа кластеров

Для кластеризации данных клиентов будет использоваться алгоритм **K-средних**, который является одним из простейших и популярных способов группирования данных.
Дополнительные сведения о нем см. в статье [Полное руководство по алгоритму кластеризации на основе K-средних](https://www.kdnuggets.com/2019/05/guide-k-means-clustering-algorithm.html).

Этот алгоритм принимает два входных значения: Сами данные и предварительно определенное число *k*, представляющее число создаваемых кластеров.
На выходе получается *k* кластеров, по которым разделяются входные данные.

Алгоритм K-средних группирует элементы в заданное количество кластеров (k) таким образом, чтобы элементы в одном кластере были максимально схожи друг с другом и максимально отличались от элементов других кластеров.

Чтобы определить число кластеров для алгоритма, используется график значений сумм квадратов внутри групп по числу извлеченных кластеров. Необходимое число кластеров будет находиться на изгибе графика.

```python
################################################################################################
## Determine number of clusters using the Elbow method
################################################################################################

cdata = customer_data
K = range(1, 20)
KM = (sk_cluster.KMeans(n_clusters=k).fit(cdata) for k in K)
centroids = (k.cluster_centers_ for k in KM)

D_k = (sci_distance.cdist(cdata, cent, 'euclidean') for cent in centroids)
dist = (np.min(D, axis=1) for D in D_k)
avgWithinSS = [sum(d) / cdata.shape[0] for d in dist]
plt.plot(K, avgWithinSS, 'b*-')
plt.grid(True)
plt.xlabel('Number of clusters')
plt.ylabel('Average within-cluster sum of squares')
plt.title('Elbow for KMeans clustering')
plt.show()
```

![Изгиб графика](./media/python-tutorial-elbow-graph.png)

На этом графике оптимальным является значение *k = 4*. При таком значении *k* клиенты будут группироваться по четырем кластерам.

## <a name="perform-clustering"></a>Выполнение кластеризации

В следующем скрипте Python вы будете использовать функцию KMeans из пакета sklearn.

```python
################################################################################################
## Perform clustering using Kmeans
################################################################################################

# It looks like k=4 is a good number to use based on the elbow graph.
n_clusters = 4

means_cluster = sk_cluster.KMeans(n_clusters=n_clusters, random_state=111)
columns = ["orderRatio", "itemsRatio", "monetaryRatio", "frequency"]
est = means_cluster.fit(customer_data[columns])
clusters = est.labels_
customer_data['cluster'] = clusters

# Print some data about the clusters:

# For each cluster, count the members.
for c in range(n_clusters):
    cluster_members=customer_data[customer_data['cluster'] == c][:]
    print('Cluster{}(n={}):'.format(c, len(cluster_members)))
    print('-'* 17)
print(customer_data.groupby(['cluster']).mean())
```

## <a name="analyze-the-results"></a>Анализ результатов

После выполнения кластеризации по методу K-средних можно провести анализ результатов и определить наличие практически полезной информации.

Изучите средние значения кластеризации и размеры кластеров, выводимые предыдущим скриптом.

```results
Cluster0(n=31675):
-------------------
Cluster1(n=4989):
-------------------
Cluster2(n=1):
-------------------
Cluster3(n=671):
-------------------

         customer  orderRatio  itemsRatio  monetaryRatio  frequency
cluster
0        50854.809882    0.000000    0.000000       0.000000   0.000000
1        51332.535779    0.721604    0.453365       0.307721   1.097815
2        57044.000000    1.000000    2.000000     108.719154   1.000000
3        48516.023845    0.136277    0.078346       0.044497   4.271237
```

Значения кластеров задаются с помощью переменных, определенных в [первой части](python-clustering-model-prepare-data.md#separate-customers):

* *orderRatio* = коэффициент возвратов заказов (отношение числа частично или полностью возвращенных заказов к общему числу заказов)
* *itemsRatio* = коэффициент возврата единицы товара (отношение возвращенных единиц товара к общему числу проданных единиц товара)
* *monetaryRatio* = коэффициент возврата в денежном выражении (отношение общего объема возвратов к общему объему покупок в денежном выражении)
* *frequency* = частота возвратов

Для интеллектуального анализа данных по методу K-средних часто требуется проведение дополнительного анализа результатов, а также выполнение других действий для лучшего понимания каждого кластера. Тем не менее, такой метод может дать полезные начальные результаты.
Интерпретировать результаты можно несколькими способами:

* Кластер 0 скорее всего определяет группу неактивных клиентов (все значения равны нулю).
* Кластер 3 определяет группу с отличным от других поведением.

Кластер 0 объединяет клиентов, которые не демонстрируют активность. Возможно, вам стоит сосредоточить маркетинговую деятельность именно на этой группе, чтобы стимулировать интерес ее участников к покупке. На следующем шаге вы запрашиваете из базы данных адреса электронной почты клиентов, включенных в кластер 0, чтобы отправить им маркетинговые материалы.

## <a name="clean-up-resources"></a>Очистка ресурсов

Если вы не собираетесь продолжать работу с этим учебником, удалите базу данных tpcxbb_1gb.

## <a name="next-steps"></a>Дальнейшие действия

В третьей части этого учебника вы выполнили следующие действия:

* Определение числа кластеров для алгоритма K-средних
* Выполнение кластеризации
* Анализ результатов

Чтобы развернуть созданную модель машинного обучения, перейдите к четвертой части этого учебника:

> [!div class="nextstepaction"]
> [Учебник по Python. Развертывание модели кластеризации](python-clustering-model-deploy.md)