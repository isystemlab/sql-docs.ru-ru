---
title: Справочник по отладки bdc mssqlctl
titleSuffix: SQL Server big data clusters
description: Справочная статья по команды отладки mssqlctl bdc.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 20257039a40594cd592bcc4d4f6050027d8858ea
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728577"
---
# <a name="mssqlctl-bdc-debug"></a>mssqlctl bdc отладки

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

В следующей статье приведены ссылки для **отладки bdc** команды в **mssqlctl** средство. Дополнительные сведения о других **mssqlctl** команды, см. в разделе [mssqlctl ссылку](reference-mssqlctl.md).

## <a name="commands"></a>Команды
|     |     |
| --- | --- |
[Копировать журналы mssqlctl отладки bdc](#mssqlctl-bdc-debug-copy-logs) | Копировать журналы.
[файлы дампа отладки mssqlctl bdc](#mssqlctl-bdc-debug-dump) | Триггер дампа ведения журнала.
## <a name="mssqlctl-bdc-debug-copy-logs"></a>Копировать журналы mssqlctl отладки bdc
Копировать журналы отладки из больших данных кластера — конфигурации kube необходим в вашей системе.
```bash
mssqlctl bdc debug copy-logs --namespace -n 
                             [--container -c]  
                             [--target-folder -d]  
                             [--pod -p]  
                             [--timeout -t]
```
### <a name="required-parameters"></a>Обязательные параметры
#### `--namespace -n`
Имя каталога бизнес-данных, используемое для пространства имен kubernetes.
### <a name="optional-parameters"></a>Необязательные параметры
#### `--container -c`
Скопировать журналы для контейнеров с похожим именем, необязательно, по умолчанию копирует журналы для всех контейнеров. Нельзя указывать несколько раз. Если указано несколько раз, последний может быть использован один
#### `--target-folder -d`
Целевой путь к папке для копирования журналов. Необязательно, по умолчанию создает результат в локальной папке.  Нельзя указывать несколько раз. Если указано несколько раз, последний может быть использован один
#### `--pod -p`
Скопируйте журналы для модулей POD с похожим именем. Необязательно, по умолчанию копий журналы для всех модулей. Нельзя указывать несколько раз. Если указано несколько раз, последний может быть использован один
#### `--timeout -t`
Число секунд ожидания завершения выполнения команды. Значение по умолчанию — 0, который не ограничен
### <a name="global-arguments"></a>Глобальные аргументы
#### `--debug`
Увеличьте уровень подробного ведения журнала для отображения всех журналов отладки.
#### `--help -h`
Отображение этого справочного сообщения и выход.
#### `--output -o`
Формат выходных данных.  Допустимые значения: json, jsonc, table, tsv.  По умолчанию: json.
#### `--query -q`
Строка запроса JMESPath. См. в разделе [ http://jmespath.org/ ](http://jmespath.org/]) Дополнительные сведения и примеры.
#### `--verbose`
Увеличьте уровень подробного ведения журнала. Используйте параметр--debug, чтобы получить полные журналы отладки.
## <a name="mssqlctl-bdc-debug-dump"></a>файлы дампа отладки mssqlctl bdc
Активировать ведение журнала дампа и скопируйте его из контейнера - kube config необходим в вашей системе.
```bash
mssqlctl bdc debug dump --namespace -n 
                        --container -c  
                        [--target-folder -d]
```
### <a name="required-parameters"></a>Обязательные параметры
#### `--namespace -n`
Имя каталога бизнес-данных, используемое для пространства имен kubernetes.
#### `--container -c`
Скопировать журналы для контейнеров с похожим именем, необязательно, по умолчанию копирует журналы для всех контейнеров. Нельзя указывать несколько раз. Если указано несколько раз, последний может быть использован один
### <a name="optional-parameters"></a>Необязательные параметры
#### `--target-folder -d`
Целевой путь к папке для копирования журналов. Необязательно, по умолчанию создает результат в локальной папке.  Нельзя указывать несколько раз. Если указано несколько раз, последний может быть использован один `./output/dump`
### <a name="global-arguments"></a>Глобальные аргументы
#### `--debug`
Увеличьте уровень подробного ведения журнала для отображения всех журналов отладки.
#### `--help -h`
Отображение этого справочного сообщения и выход.
#### `--output -o`
Формат выходных данных.  Допустимые значения: json, jsonc, table, tsv.  По умолчанию: json.
#### `--query -q`
Строка запроса JMESPath. См. в разделе [ http://jmespath.org/ ](http://jmespath.org/]) Дополнительные сведения и примеры.
#### `--verbose`
Увеличьте уровень подробного ведения журнала. Используйте параметр--debug, чтобы получить полные журналы отладки.

## <a name="next-steps"></a>Следующие шаги

Дополнительные сведения о других **mssqlctl** команды, см. в разделе [mssqlctl ссылку](reference-mssqlctl.md). Дополнительные сведения об установке **mssqlctl** инструмент, см. в разделе [установить mssqlctl для управления кластерами больших данных SQL Server 2019](deploy-install-mssqlctl.md).