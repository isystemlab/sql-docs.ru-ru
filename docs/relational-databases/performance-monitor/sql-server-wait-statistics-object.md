---
title: Объект статистики ожидания (SQL Server) | Документация Майкрософт
description: Сведения об объекте производительности SQLServer:Wait Statistics, который содержит счетчики производительности, сообщающие сведения о состоянии ожидания.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Wait Statistics object
- SQLServer:Wait Statistics
ms.assetid: cb7f917d-4291-4115-9b78-ee7692ebbb2d
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 64a21ac3072869f74c71997be5160b55758fc917
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457410"
---
# <a name="sql-server-wait-statistics-object"></a>SQL Server, объект Wait Statistics
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Объект производительности **SQLServer:Wait Statistics** содержит счетчики производительности, сообщающие сведения о состоянии ожидания.  
  
 В таблице ниже перечислены счетчики, содержащиеся в объекте статистики ожидания.  
  
|SQL Server, счетчики статистики ожидания|Описание|  
|-----------------------------------------|-----------------|  
|**Ожиданий блокировок**|Статистика процессов, ожидающих в состоянии блокировки.|  
|**Ожиданий буфера журнала**|Статистика процессов, ожидающих освобождения буфера журнала.|  
|**Ожиданий записи в журнал**|Статистика процессов, ожидающих записи в буфер журнала.|  
|**Ожиданий в очереди на выделение памяти**|Статистика процессов, ожидающих предоставления памяти.|  
|**Ожиданий сетевых операций ввода-вывода**|Статистика, относящаяся к сетевому вводу-выводу.|  
|**Ожиданий кратковременной блокировки объектов, отличных от страниц**|Статистика, относящаяся к не страничным кратковременным блокировкам.|  
|**Число ожиданий кратковременной блокировки операций ввода-вывода страниц**|Статистика, относящаяся к кратковременным блокировкам страничного ввода-вывода.|  
|**Ожиданий кратковременной блокировки страниц**|Статистика, относящаяся к страничным кратковременным блокировкам, исключая кратковременные блокировки ввода-вывода.|  
|**Ожиданий поточно-ориентированных объектов памяти**|Статистика процессов, ожидающих поточно-ориентированного выделения памяти.|  
|**Ожиданий владения транзакцией**|Статистика, относящаяся к процессам, синхронизирующим доступ к транзакции.|  
|**Ожиданий исполнителя**|Статистика, относящаяся к процессам, ожидающим освобождения рабочего потока.|  
|**Ожиданий синхронизации рабочего пространства**|Статистика, относящаяся к процессам, синхронизирующим доступ к рабочему пространству.|  
  
 Каждый из счетчиков объекта содержит следующие экземпляры.  
  
|Элемент|Описание|  
|----------|-----------------|  
|**Среднее время ожидания блокировки (мс)**|Среднее время для выбранного типа ожидания.|  
|**Совокупное время ожидания (мс) в секунду**|Общее время ожидания в секунду для выбранного типа ожидания.|  
|**Выполняющиеся сеансы ожидания**|Количество ожидающих в данный момент процессов для определенного типа ожидания.|  
|**Начатые сеансы ожидания (в секунду)**|Число ожиданий, запущенных за одну секунду, для выбранного типа ожидания.|  
  
## <a name="see-also"></a>См. также:  
 [Наблюдение за использованием ресурсов (системный монитор)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
