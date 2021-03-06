---
description: Универсальные приложения
title: Универсальные приложения | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], generic applications
- interoperability [ODBC], levels
- generic applications [ODBC]
ms.assetid: dda2a3c4-76ef-40a6-b3a1-9e95bed61618
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9980edcaf34182b4c7f43aa8e935d095f2345138
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476686"
---
# <a name="generic-applications"></a>Универсальные приложения
Универсальные приложения иногда выполняют жестко запрограммированную задачу, например электронную таблицу, которая получает данные из базы данных. Они также могут выполнять разнообразные определяемые пользователем задачи, такие как универсальное приложение запросов, позволяющее пользователю вводить и выполнять инструкцию SQL. Общие универсальные приложения — это то, что они должны работать с различными СУБД и что разработчик не знает заранее, какие именно эти СУБД будут использоваться.  
  
 Поэтому универсальные приложения должны быть строго совместимыми. Разработчик должен предоставить множество вариантов, вычислить возможности взаимодействия для функций и написать код, который ожидает, что драйверы поддерживают широкий спектр функций. Хотя универсальные приложения могут быть настроены для работы с популярными СУБД, они редко содержат код, зависящий от драйвера или СУБД.
