---
description: Определение поддерживаемых возможностей
title: Определение поддерживаемых возможностей | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], Supports method
- Supports method [ADO]
ms.assetid: 65090cba-6d46-4775-8d61-f6838e7752a6
author: rothja
ms.author: jroth
ms.openlocfilehash: c2caaf9e708b9a9fccd728472c7b13857978fdbe
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991385"
---
# <a name="determining-what-is-supported"></a>Определение поддерживаемых возможностей
Метод **поддерживает** , чтобы определить, поддерживает ли указанный объект **Recordset** определенный тип функциональности. Он имеет следующий синтаксис:  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>Remarks  
 Метод **поддерживает** возвращает логическое значение, указывающее, поддерживает ли поставщик все функции, определяемые аргументом курсороптионс. Чтобы определить, какие типы функций поддерживает объект **Recordset** , можно использовать метод **поддерживает** . Если объект **набора записей** поддерживает функции, соответствующие константы которых находятся в *Курсороптионс*, метод **поддерживает** возврат значения **true**. В противном случае возвращается **значение false**.  
  
 Используя метод **поддержки** , можно проверить возможность добавления новых записей объектом **Recordset** , использовать закладки, использовать метод **Find** , использовать прокрутку, использовать свойство **index** и для выполнения пакетных обновлений. Полный список констант и их значений см. в разделе [курсороптионенум](../../reference/ado-api/cursoroptionenum.md).  
  
 Несмотря на то, что метод **поддерживает** возврат значения **true** для заданной функциональности, он не гарантирует, что поставщик может сделать эту функцию доступной во всех обстоятельствах. Метод Supports просто **возвращает значение,** указывающее, может ли поставщик поддерживать указанные функциональные возможности при условии, что выполняются определенные условия. Например, метод **поддержки** может указывать на то, что объект **набора записей** поддерживает обновления, даже если курсор основан на множественном соединении таблицы — некоторые столбцы, которые не обновляются.