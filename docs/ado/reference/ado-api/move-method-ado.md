---
description: Метод Move (ADO)
title: Метод Move (ADO) | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Move
- Recordset15::raw_Move
helpviewer_keywords:
- Move method [ADO]
ms.assetid: 13fe9381-d00b-4f4a-9162-83c3f21b3837
author: rothja
ms.author: jroth
ms.openlocfilehash: 6b394d64a9d1b1f403137e9875db83fdd82c2ac1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990595"
---
# <a name="move-method-ado"></a>Метод Move (ADO)
Перемещает текущую запись в объекте [набора записей](./recordset-object-ado.md) .  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>Параметры  
 *нумрекордс*  
 Выражение типа **Long** со знаком, указывающее количество записей, перемещаемых текущей позицией записи.  
  
 *Начало*  
 Необязательный элемент. **Строковое** значение или **вариант** , результатом которого является закладка. Можно также использовать значение [букмаркенум](./bookmarkenum.md) .  
  
## <a name="remarks"></a>Remarks  
 Метод **Move** поддерживается для всех объектов **Recordset** .  
  
 Если аргумент *нумрекордс* больше нуля, текущее расположение записи перемещается вперед (к концу **набора записей**). Если значение *нумрекордс* меньше нуля, текущее расположение записи перемещается назад (в направлении начала **набора записей**).  
  
 Если при вызове **Move** положение текущей записи перемещается в точку до первой записи, ADO устанавливает текущую запись в позицию перед первой записью в наборе записей ([BOF](./bof-eof-properties-ado.md) имеет **значение true**). Попытка перемещения назад, если свойство **BOF** уже имеет **значение true** , приводит к ошибке.  
  
 Если при вызове **Move** положение текущей записи перемещается в точку после последней записи, ADO устанавливает текущую запись в позицию после последней записи в наборе записей (значение[EOF](./bof-eof-properties-ado.md) равно **true**). Попытка перемещения вперед, если свойство **EOF** уже имеет **значение true** , приводит к ошибке.  
  
 Вызов метода **Move** из пустого объекта **Recordset** приводит к ошибке.  
  
 Если передать аргумент *Start* , то перемещение будет относиться к записи с этой закладкой, предполагая, что объект **набора записей** поддерживает закладки. Если значение не указано, то перемещение отсчитывается относительно текущей записи.  
  
 Если свойство [CacheSize](./cachesize-property-ado.md) используется для локального кэширования записей от поставщика, передача аргумента *нумрекордс* , который перемещает текущую запись за пределы текущей группы кэшированных записей, заставляет ADO получить новую группу записей, начиная с целевой записи. Свойство **CacheSize** определяет размер вновь полученной группы, а конечную запись — первую извлеченную запись.  
  
 Если объект **Recordset** является только прямым, пользователь по-прежнему может передать аргумент *нумрекордс* меньше нуля, если назначение находится в текущем наборе кэшированных записей. Если при вызове **Move** положение текущей записи перемещается в запись до первой кэшированной записи, возникнет ошибка. Таким же, можно использовать кэш записей, поддерживающий полную прокрутку для поставщика, поддерживающего только прямую прокрутку. Поскольку кэшированные записи загружаются в память, следует избегать кэширования большего количества записей, чем необходимо. Даже если объект **набора записей** с прямым переходом поддерживает обратные перемещения таким образом, вызов метода [MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) для любого объекта **набора записей** с прямыми последовательностью будет по-прежнему вызывать ошибку.  
  
> [!NOTE]
>  Поддержка перемещения в обратном направлении в **наборе записей** только для последовательного доступа не является прогнозируемой в зависимости от поставщика. Если текущая запись была размещена после последней записи в **наборе записей**, **Перемещение** в обратном направлении может привести к неправильному текущему положению.  
  
## <a name="applies-to"></a>Применение  
 [Объект Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>См. также  
 [Пример метода Move (Visual Basic)](./move-method-example-vb.md)   
 [Пример метода Move (VBScript)](./move-method-example-vbscript.md)   
 [Пример метода Move (Visual c++)](./move-method-example-vc.md)   
 [Методы MoveFirst, MoveLast, MoveNext и MovePrevious (ADO)](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Методы MoveFirst, MoveLast, MoveNext и MovePrevious (RDS)](../rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [Метод MoveRecord (ADO)](./moverecord-method-ado.md)