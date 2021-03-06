---
description: SQLExecDirect (драйвер ODBC для Visual FoxPro)
title: SQLExecDirect (драйвер ODBC для Visual FoxPro) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExecDirect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5004060f-8510-4018-87a4-d41789e69d3e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d12218097caf6d4a2c4a0375f1a8e9542b2ccf59
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449186"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (драйвер ODBC для Visual FoxPro)
> [!NOTE]  
>  В этом разделе содержатся сведения, относящиеся к драйверу ODBC для Visual FoxPro. Общие сведения об этой функции см. в соответствующем разделе [справочника по API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Поддержка: полная  
  
 Соответствие API ODBC: уровень ядра  
  
 Выполняет новую [инструкцию SQL доступный](../../odbc/microsoft/visual-foxpro-terminology.md). Драйвер ODBC для Visual FoxPro использует текущие значения переменных маркера параметра, если в инструкции существуют какие либо параметры.  
  
 Чтобы создать пакетную команду для отправки более одной инструкции SQL за раз, используйте точку с запятой (;) для разделения каждой инструкции SQL в пакете.  
  
 Если имена таблицы, представления или поля содержат пробелы, заключите их в кавычки. Например, если база данных содержит таблицу с именем Моя таблица и поле My, заключите каждый элемент идентификатора следующим образом:  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 Дополнительные сведения см. в разделе [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) в *справочнике программиста по ODBC*.
