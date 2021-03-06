---
title: Развертывание на OpenShift
titleSuffix: SQL Server Big Data Cluster
description: Сведения об обновлении кластеров больших данных SQL Server на OpenShift.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aa838fc8920469921063ebdface6680e3bc5a3bf
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892494"
---
# <a name="deploy-big-data-clusters-2019-on-openshift-on-premises-and-azure-red-hat-openshift"></a>Развертывание [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] в локальной среде OpenShift и Azure Red Hat OpenShift

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Эта статья поясняет, как развернуть кластер больших данных SQL Server в средах OpenShift, локально или в Azure Red Hat OpenShift (АТО).

> [!TIP]
> Чтобы осуществить начальную загрузку образца среды с помощью ARO и затем развернуть кластер больших данных на этой платформе, можно использовать скрипт Python, доступный [здесь](quickstart-big-data-cluster-deploy-aro.md).


Накопительный пакет обновления 5 для SQL Server 2019 предоставляет поддержку кластеров больших данных SQL Server на OpenShift. Кластеры больших данных можно развернуть в локальной среде OpenShift или в Azure Red Hat OpenShift (ARO). Для развертывания требуется версия кластера OpenShift не ниже 4.3. Хотя рабочий процесс развертывания аналогичен развертыванию в других платформах на основе Kubernetes ([kubeadm](deploy-with-kubeadm.md) и [AKS](deploy-on-aks.md)), имеются некоторые различия. Разница в основном связана с запуском приложений в качестве непривилегированного пользователя и контекстом безопасности, используемым для пространства имен, в котором развертывается кластер больших данных.

Сведения о развертывании кластера OpenShift в локальной среде см. в [документации по Red Hat OpenShift](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-installation-and-upgrade). Для развертываний ARO см. [Azure Red Hat OpenShift](/azure/openshift/intro-openshift).

В этой статье описаны шаги развертывания, характерные для платформы OpenShift, указаны варианты доступа к целевой среде и пространство имен, которое используется для развертывания кластера больших данных.

## <a name="pre-requisites"></a>Предварительные требования

> [!IMPORTANT]
> Указанные ниже предварительные требования должны быть выполнены администратором кластера OpenShift (роль кластера "Администратор кластера") с достаточными разрешениями для создания этих объектов на уровне кластера. Дополнительные сведения о ролях кластера в OpenShift см. в разделе [Использование RBAC для определения и применения разрешений](https://docs.openshift.com/container-platform/4.4/authentication/using-rbac.html).

1. Измените параметр `pidsLimit` в OpenShift в соответствии с рабочими нагрузками SQL Server. Значение по умолчанию в OpenShift слишком мало для нагрузок, характерных для рабочей среды. Рекомендуется указать по меньшей мере `4096`, но оптимальное значение будет зависеть от параметра `max worker threads` в SQL Server и количества процессоров ЦП на узле OpenShift. 
    - Чтобы узнать, как изменить `pidsLimit` для кластера OpenShift, используйте [эти инструкции]( https://github.com/openshift/machine-config-operator/blob/master/docs/ContainerRuntimeConfigDesign.md). Обратите внимание, что версии OpenShift до `4.3.5` имели дефект, препятствовавший применению измененного значения. Обновите OpenShift до последней версии. 
    - Чтобы упростить расчет оптимального значения с учетом среды и запланированных рабочих нагрузок SQL Server, можно использовать оценку и примеры ниже:

    |Количество процессоров|Максимальное число рабочих потоков по умолчанию|Число рабочих процессов на процессор по умолчанию|Минимальное значение pidsLimit|
    |--------------------|--------------------------|-----------------------------|-----------------------|
    |          64        |           512            |             16              | 512 + (64 *16) = 1536 |
    |         128        |           512            |             32              | 512 + (128*32) = 4608 |

    > [!NOTE]
    > Другие процессы (например, резервное копирование, CLR, Fulltext, SQLAgent) также добавляют некоторые дополнительные служебные данные, поэтому добавляйте к предполагаемому значению некоторый запас.

2. Создайте настраиваемое ограничение контекста безопасности (SCC) с помощью присоединенного [`bdc-scc.yaml`](#bdc-sccyaml-file).

    ```console
    oc apply -f bdc-scc.yaml
    ```

    > [!NOTE]
    > Настраиваемое ограничение контекста безопасности для кластера больших данных основано на встроенном `nonroot` ограничении контекста безопасности в OpenShift с дополнительными разрешениями. Дополнительные сведения об ограничениях контекста безопасности в OpenShift см. в разделе [Управление ограничениями контекста безопасности](https://docs.openshift.com/container-platform/4.3/authentication/managing-security-context-constraints.html). Подробные материалы о том, какие дополнительные разрешения требуются для кластеров больших данных поверх `nonroot` ограничения контекста безопасности, можно скачать [здесь](https://aka.ms/sql-bdc-openshift-security).

3. Создайте пространство имен или проект:

   ```console
   oc new-project <namespaceName>
   ```

4. Назначьте настраиваемое ограничение контекста безопасности учетным записям службы для пользователей в пространстве имен, где развернут кластер больших данных:

   ```console
   oc adm policy add-scc-to-group bdc-scc system:serviceaccounts:<namespaceName>
   ```

5. Назначьте соответствующее разрешение для пользователя, развертывающего кластер больших данных. Выполните одно из следующих действий. 

   - Если пользователь, развертывающий кластер больших данных, имеет роль администратора кластера, перейдите к [развертыванию кластера больших данных](#deploy-big-data-cluster).

   - Если пользователь, развертывающий кластер больших данных, является администратором пространства имен, назначьте ему локальную роль администратора кластера для созданного пространства имен. Это предпочтительный вариант, когда пользователь, развертывающий кластер больших данных и управляющий им, должен иметь разрешения администратора на уровне пространства имен.

   ```console
   oc adm policy add-role-to-user cluster-admin <deployingUser> -n <namespaceName>
   ```

   После этого пользователь, развертывающий кластер больших данных, должен войти в консоль OpenShift:

   ```console
   oc login -u <deployingUser> -p <password>
   ```

## <a name="deploy-big-data-cluster"></a>Развертывание кластера больших данных

1. Установите последний [azdata](../azdata/install/deploy-install-azdata.md).

1. Клонируйте один из встроенных файлов конфигурации для OpenShift в зависимости от целевой среды (локальная среда OpenShift или АТО) и сценария развертывания. Параметры для OpenShift во встроенных файлах конфигурации описаны в подразделе *Параметры для OpenShift в файлах конфигурации развертывания* ниже. Дополнительные сведения о доступных файлах конфигурации см. в [руководстве по развертыванию](deployment-guidance.md).

   Выведите список всех доступных встроенных файлов конфигурации.

   ```console
   azdata bdc config list
   ```

   Чтобы клонировать один из встроенных файлов конфигурации, выполните приведенную ниже команду (при необходимости можно заменить профиль с учетом целевой платформы или сценария):

   ```console
   azdata bdc config init --source openshift-dev-test --target custom-openshift
   ```

   Для развертывания в ARO рекомендуется начать с одного из профилей `aro-` , включающих значения по умолчанию для `serviceType` и `storageClass`, подходящие для этой среды. Пример:

   ```console
   azdata bdc config init --source aro-dev-test --target custom-openshift
   ```

1. Настройте файлы конфигурации control.json и bdc.json. Ниже приведены некоторые дополнительные ресурсы, которые помогут вам выполнить настройку для поддержки различных вариантов использования.

   - [Память](concept-data-persistence.md)
   - [Сопутствующие параметры AD](active-directory-deploy.md)
   - [Другие настройки](deployment-custom-configuration.md)

   > [!NOTE]
   > Интеграция с Azure Active Directory для кластера больших данных не поддерживается, поэтому вы не можете использовать этот метод проверки подлинности при развертывании в ARO.

1. Задайте [переменные среды](deployment-guidance.md#env).

1. Разверните кластер больших данных.

   ```console
   azdata bdc create --config custom-openshift --accept-eula yes
   ```

1. После успешного развертывания можно войти в систему и вывести список конечных точек внешнего кластера:

```console
   azdata login -n mssql-cluster
   azdata bdc endpoint list
```

## <a name="openshift-specific-settings-in-the-deployment-configuration-files"></a>Параметры для OpenShift в файлах конфигурации развертывания

Накопительный пакет обновления 5 для SQL Server 2019 представляет два параметра для управления сбором метрик объектов pod и узлов. Для этих параметров по умолчанию во встроенных профилях для OpenShift задано значение `false`, так как контейнерам мониторинга требуется [привилегированный контекст безопасности](https://www.openshift.com/blog/managing-sccs-in-openshift), что ослабляет некоторые ограничения безопасности для пространства имен, в котором развернут кластер больших данных.

```json
    "security": {
      "allowNodeMetricsCollection": false,
      "allowPodMetricsCollection": false
}
```

Именем класса хранения по умолчанию в ARO является managed-premium (в отличие от AKS, где класс хранения по умолчанию называется default). Это можно найти в `control.json`, соответствующем `aro-dev-test` и `aro-dev-test-ha`:

```json
    },
    "storage": {
      "data": {
        "className": "managed-premium",
        "accessMode": "ReadWriteOnce",
        "size": "15Gi"
      },
      "logs": {
        "className": "managed-premium",
        "accessMode": "ReadWriteOnce",
        "size": "10Gi"
      }
```

## <a name="bdc-sccyaml-file"></a>Файл `bdc-scc.yaml`

```yaml
apiVersion: security.openshift.io/v1
kind: SecurityContextConstraints
metadata:
  annotations:
    kubernetes.io/description: SQL Server BDC custom scc is based on 'nonroot' scc plus additional capabilities.
  generation: 2
  name: bdc-scc
allowHostDirVolumePlugin: false
allowHostIPC: false
allowHostNetwork: false
allowHostPID: false
allowHostPorts: false
allowPrivilegeEscalation: true
allowPrivilegedContainer: false
allowedCapabilities:
  - SETUID
  - SETGID
  - CHOWN
  - SYS_PTRACE
defaultAddCapabilities: null
fsGroup:
  type: RunAsAny
readOnlyRootFilesystem: false
requiredDropCapabilities:
  - KILL
  - MKNOD
runAsUser:
  type: MustRunAsNonRoot
seLinuxContext:
  type: MustRunAs
supplementalGroups:
  type: RunAsAny
volumes:
  - configMap
  - downwardAPI
  - emptyDir
  - persistentVolumeClaim
  - projected
  - secret
```

## <a name="next-steps"></a>Дальнейшие действия

[Руководство. Загрузка примера данных в кластер больших данных SQL Server](tutorial-load-sample-data.md)