---
description: Коллекция Indexes (ADOX)
title: Коллекция indexes (ADOX) | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Indexes
- Indexes
helpviewer_keywords:
- Indexes collection [ADOX]
ms.assetid: 184cf536-455c-42be-bf1c-a5c25bade961
author: rothja
ms.author: jroth
ms.openlocfilehash: daea070c8bd39d6208404f119578773382078634
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984195"
---
# <a name="indexes-collection-adox"></a>Коллекция Indexes (ADOX)
Содержит все объекты [индекса](./index-object-adox.md) таблицы.  
  
## <a name="remarks"></a>Remarks  
 Метод [append](./append-method-adox-indexes.md) для коллекции **индексов** уникален для ADOX. Вы можете:  
  
-   Добавьте новый индекс в коллекцию с помощью метода **append** .  
  
 Остальные свойства и методы являются стандартными для коллекций ADO. Вы можете:  
  
-   Доступ к индексу в коллекции со свойством [Item](../ado-api/item-property-ado.md) .  
  
-   Возвращает количество индексов, содержащихся в коллекции, со свойством [Count](../ado-api/count-property-ado.md) .  
  
-   Удалите индекс из коллекции с помощью метода [Delete](./delete-method-adox-collections.md) .  
  
-   Обновите объекты в коллекции, чтобы отразить текущую схему базы данных методом [Refresh](../ado-api/refresh-method-ado.md) .  
  
 Этот раздел содержит следующий раздел.  
  
-   [Свойства, методы и события коллекции Indexes](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>См. также  
 [Пример метода Append для индексов (Visual Basic)](./indexes-append-method-example-vb.md)   
 [Объект Index (ADOX)](./index-object-adox.md)