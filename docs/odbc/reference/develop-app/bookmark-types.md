---
description: Типы закладок
title: Типы закладок | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- variable-length bookmarks [ODBC]
- bookmarks [ODBC]
- fixed-length bookmarks [ODBC]
ms.assetid: cb2e7443-0260-4d1a-930f-0154db447979
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e85d50a5fe3c21707a78ac2572d8a96166745319
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476816"
---
# <a name="bookmark-types"></a>Типы закладок
Все закладки в ODBC *3. x* — это закладки с переменной длиной. Это позволяет использовать в качестве закладки первичный ключ или уникальный индекс, связанный с таблицей. Закладка также может быть 32-битным значением, как использовалось в ODBC *2. x*. Чтобы указать, что закладка используется с курсором, приложение ODBC *3. x* задает для атрибута SQL_ATTR_USE_BOOKMARK инструкции значение SQL_UB_VARIABLE. Закладка переменной длины используется автоматически.  
  
 Приложение может вызвать **SQLColAttribute** с аргументом *фиелдидентифиер* , для которого задано значение SQL_DESC_OCTET_LENGTH, чтобы получить длину закладки. Поскольку закладка с переменной длиной может иметь значение типа Long, приложение не должно выполнять привязку к столбцу 0, если только он не будет использовать закладку для многих строк в наборе строк.  
  
 Закладки фиксированной длины поддерживаются только в целях обратной совместимости. Если приложение ODBC *2. x* , работающее с драйвером ODBC *3. x* , вызывает **SQLSetStmtOption** для установки SQL_USE_BOOKMARKS SQL_UB_ON, оно сопоставляется в диспетчере драйверов для SQL_UB_VARIABLE. Используется закладка переменной длины, даже если заполнено только 32 разрядов. Если драйвер поддерживает закладки с фиксированной длиной, он будет поддерживать закладки с переменной длиной. Если приложение ODBC *3. x* , работающее с драйвером ODBC *2. x* , вызывает **SQLSetStmtAttr** для установки SQL_ATTR_USE_BOOKMARKS в SQL_UB_VARIABLE, оно сопоставляется в диспетчере драйверов для SQL_UB_ON и используется 32-разрядная закладка фиксированной длины. После этого атрибут инструкции SQL_ATTR_FETCH_BOOKMARK_PTR должен указывать на 32-разрядную закладку. Если используемые закладки длиннее 32 бит, например, если в качестве закладок используются первичные ключи, курсор должен сопоставлять фактические значения с 32-битным значением. Например, можно создать хэш-таблицу. Когда приложение ODBC *3. x* , работающее с драйвером ODBC *2. x* , привязывает закладку, длина буфера должна быть равна 4.
