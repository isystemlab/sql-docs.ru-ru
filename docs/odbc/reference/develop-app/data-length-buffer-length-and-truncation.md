---
description: Длина данных, длина буфера и усечение
title: Длина данных, длина буфера и усечение | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- data length [ODBC]
- truncating data [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 2825c6e7-b9ff-42fe-84fc-7fb39728ac5d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c9a9651f39c1ff4d2c6dc9b691453fb5354c9e1a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465836"
---
# <a name="data-length-buffer-length-and-truncation"></a>Длина данных, длина буфера и усечение
*Длина данных* — это длина в байтах данных, которая будет храниться в буфере данных приложения, а не в том виде, в котором они хранятся в источнике данных. Это различие важно, поскольку данные часто хранятся в разных типах буфера данных, чем в источнике данных. Таким образом, для передачи данных в источник данных это длина байта данных перед преобразованием в тип источника данных. Для данных, извлекаемых из источника данных, это длина байта данных после преобразования в тип буфера данных и до выполнения каких-либо усечений.  
  
 Для данных фиксированной длины, таких как целое число или структура даты, длина данных в байтах всегда равна размеру типа данных. Как правило, приложения распределяют буфер данных, который является размером типа данных. Если приложение выделяет буфер меньшего размера, последствия не определены, так как драйвер предполагает, что буфер данных имеет размер типа данных и не усекает данные для размещения в буфере меньшего размера. Если приложение выделяет буфер большего размера, дополнительное пространство никогда не используется.  
  
 Для данных переменной длины, таких как символьные или двоичные данные, важно понимать, что байтовая длина данных отделена от и часто отличается от длины в байтах буфера. Отношение этих двух значений длины описывается в разделе [буферы](../../../odbc/reference/develop-app/buffers.md) . Если длина данных в байтах превышает длину в байтах буфера, драйвер усекает выборку данных до длины в байтах буфера и возвращает SQL_SUCCESS_WITH_INFO с кодом SQLSTATE 01004 (усечение данных). Однако возвращенная длина в байтах — это длина неусеченных данных.  
  
 Например, предположим, что приложение выделяет 50 байт для двоичного буфера данных. Если драйвер содержит 10 байт двоичных данных для возврата, он возвращает 10 байт в буфере. Длина данных в байтах равна 10, а длина байта буфера равна 50. Если драйвер содержит 60 байт двоичных данных для возврата, то он усекает данные до 50 байт, возвращает эти байты в буфер и возвращает SQL_SUCCESS_WITH_INFO. Длина данных в байтах равна 60 (Длина до усечения), а длина байта буфера по-прежнему равна 50.  
  
 Для каждого столбца, который усекается, создается диагностическая запись. Поскольку для создания этих записей и обработки в приложении требуется время, усечение может привести к снижению производительности. Как правило, приложение может избежать этой проблемы, выделяя большие буферы, хотя это может оказаться невозможным при работе с длинными данными. Когда происходит усечение данных, приложение иногда может выделить буфер большего размера и повторно получить данные. в любом случае это не так. Если усечение происходит при получении данных с вызовами **SQLGetData**, приложению не требуется вызывать **SQLGetData** для данных, которые уже были возвращены. Дополнительные сведения см. в разделе [Получение длинных данных](../../../odbc/reference/develop-app/getting-long-data.md).
