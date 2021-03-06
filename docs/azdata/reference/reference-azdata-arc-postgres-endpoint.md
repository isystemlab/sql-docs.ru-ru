---
title: Справочник по azdata arc postgres endpoint
titleSuffix: SQL Server big data clusters
description: Справочная статья по командам azdata arc postgres endpoint.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 097bfb40f8636f66f142fc785c4699dce2084440
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358762"
---
# <a name="azdata-arc-postgres-endpoint"></a>azdata arc postgres endpoint

Применяется к [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

В следующей статье приводятся справочные сведения по командам **sql** в средстве **azdata**. Дополнительные сведения о других командах **azdata** см. в [справочнике по azdata](reference-azdata.md).

## <a name="commands"></a>Команды

|Команда|Описание|
| --- | --- |
[azdata arc postgres endpoint list](#azdata-arc-postgres-endpoint-list) | Выводит список конечных точек группы серверов PostgreSQL.
## <a name="azdata-arc-postgres-endpoint-list"></a>azdata arc postgres endpoint list
Выводит список конечных точек группы серверов PostgreSQL.
```bash
azdata arc postgres endpoint list --name -n 
                                  [--engine-version -ev]
```
### <a name="examples"></a>Примеры
Вывод списка конечных точек группы серверов PostgreSQL.
```bash
azdata arc postgres endpoint list -n postgres01
```
### <a name="required-parameters"></a>Обязательные параметры
#### `--name -n`
Имя группы серверов PostgreSQL.
### <a name="optional-parameters"></a>Необязательные параметры
#### `--engine-version -ev`
--engine-version можно использовать вместе с параметром --name для идентификации группы серверов гипермасштабирования PostgreSQL, если две группы серверов с разными версиями подсистемы имеют одинаковое имя. --engine-version — необязательный параметр, который должен иметь значение 11 или 12, когда он используется для идентификации группы серверов.
### <a name="global-arguments"></a>Глобальные аргументы
#### `--debug`
Повышение уровня детализации журнала для включения всех журналов отладки.
#### `--help -h`
Отображение этого справочного сообщения и выход.
#### `--output -o`
Формат вывода.  Допустимые значения: json, jsonc, table, tsv.  Значение по умолчанию: json.
#### `--query -q`
Строка запроса JMESPath. Дополнительные сведения и примеры см. в разделе [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Повышение уровня детализации журнала. Чтобы включить полные журналы отладки, используйте параметр --debug.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о других командах **azdata** см. в [справочнике по azdata](reference-azdata.md). 

Дополнительные сведения об установке средства **azdata** см. в разделе [Установка azdata](..\install\deploy-install-azdata.md).

