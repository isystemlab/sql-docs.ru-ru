---
description: RightsEnum
title: Ригхтсенум | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RightsEnum
helpviewer_keywords:
- RightsEnum enumeration [ADOX]
ms.assetid: 55ee67c7-a583-42aa-849a-78264b4cb614
author: rothja
ms.author: jroth
ms.openlocfilehash: be2bd513cf41247fd6ce5c8f1172353557287144
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983415"
---
# <a name="rightsenum"></a>RightsEnum
Задает права или разрешения для группы или пользователя на объекте.  
  
|Константа|Значение|Описание|  
|--------------|-----------|-----------------|  
|**adRightCreate**|16384 (&H4000)|У пользователя или группы есть разрешение на создание новых объектов этого типа.|  
|**adRightDelete**|65536 (&H10000)|Пользователь или группа имеет разрешение на удаление данных из объекта. Для таких объектов, как **таблицы**, пользователь имеет разрешение на удаление значений данных из записей.|  
|**адригхтдроп**|256 (&H100)|У пользователя или группы есть разрешение на удаление объектов из каталога. Например, **таблицы** можно удалить с помощью команды SQL DROP TABLE.|  
|**адригхтексклусиве**|512 (&H200)|У пользователя или группы есть разрешение на доступ к объекту в монопольном режиме.|  
|**adRightExecute**|536870912 (&H20000000)|У пользователя или группы есть разрешение на выполнение этого объекта.|  
|**adRightFull**|268435456 (&H10000000)|У пользователя или группы есть все разрешения на объект.|  
|**adRightInsert**|32768 (&H8000)|Пользователь или группа имеет разрешение на вставку объекта. Для таких объектов, как **таблицы**, пользователь имеет разрешение на вставку данных в таблицу.|  
|**адригхтмаксимумалловед**|33554432 (&H2000000)|У пользователя или группы максимальное число разрешений, разрешенных поставщиком. Определенные разрешения зависят от поставщика.|  
|**адригхтноне**|0|У пользователя или группы нет разрешений для объекта.|  
|**адригхтреад**|-2147483648 (&H80000000)|У пользователя или группы есть разрешение на чтение объекта. Для таких объектов, как [таблицы](./table-object-adox.md), пользователь имеет разрешение на чтение данных в таблице.|  
|**адригхтреаддесигн**|1024 (&H400)|Пользователь или группа имеет разрешение на чтение макета для объекта.|  
|**адригхтреадпермиссионс**|131072 (&H20000)|Пользователь или группа могут просматривать, но не изменять определенные разрешения для объекта в каталоге.|  
|**адригхтреференце**|8192 (&H2000)|У пользователя или группы есть разрешение на ссылку на объект.|  
|**адригхтупдате**|1073741824 (&H40000000)|У пользователя или группы есть разрешение на обновление объекта. Для таких объектов, как **таблицы**, пользователь имеет разрешение на обновление данных в таблице.|  
|**адригхтвисгрант**|4096 (&H1000)|У пользователя или группы есть разрешение на предоставление разрешений на объект.|  
|**adRightWriteDesign**|2048 (&H800)|Пользователь или группа имеет разрешение на изменение структуры объекта.|  
|**адригхтвритеовнер**|524288 (&H80000)|Пользователь или группа имеет разрешение на изменение владельца объекта.|  
|**адригхтвритепермиссионс**|262144 (&H40000)|Пользователь или группа может изменять определенные разрешения для объекта в каталоге.|  
  
## <a name="applies-to"></a>Применение  

:::row:::
    :::column:::
        [Метод GetPermissions (ADOX)](./getpermissions-method-adox.md)  
    :::column-end:::
    :::column:::
        [Метод SetPermissions (ADOX)](./setpermissions-method-adox.md)  
    :::column-end:::
:::row-end:::