---
title: Приостановка базы данных доступности для группы доступности
description: Определение возможных причин, по которым база данных доступности группы доступности Always On может приостановить работу.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: end-user-help
f1_keywords:
- sql13.swb.agdashboard.drp1notsuspended.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 6baee70f-848c-4e86-b20d-78875c0f82cb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8f5b246accb66b13cf13466d17b5d8318d5d8ec0
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/23/2020
ms.locfileid: "91114656"
---
# <a name="availability-database-is-suspended-for-an-availability-group"></a>Приостановка базы данных доступности для группы доступности
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
    
## <a name="introduction"></a>Введение  
  
|||  
|-|-|  
|**Имя политики**|Состояние приостановки базы данных доступности|  
|**Проблема**|База данных доступности приостановлена.|  
|**Категория**|**Предупреждение**|  
|**Аспект**|База данных доступности|  
  
## <a name="description"></a>Description  
 Эта политика проверяет состояние перемещения данных базы данных-получателя (которая также называется «реплика базы данных-получателя»). Эта политика находится в нерабочем состоянии, если перемещение данных приостановлено. В остальном политика находится в рабочем состоянии.  
  
> [!NOTE]  
>  Для этого выпуска [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]сведения о возможных причинах проблем и решениях доступны в разделе [База данных доступности приостановлена](https://go.microsoft.com/fwlink/p/?LinkId=220860) в TechNet Wiki.  
  
## <a name="possible-causes"></a>Возможные причины  
 Возможны следующие причины приостановки синхронизации данных в этой базе данных доступности:  
  
-   Из-за ошибки система могла приостановить синхронизацию данных.  
  
-   Администратор базы данных мог приостановить синхронизацию данных для выполнения задач технического обслуживания.  
  
## <a name="possible-solution"></a>Возможное решение  
 Восстановите синхронизацию данных. При повторном возникновении проблемы проверьте группу доступности в журнале событий, а затем с помощью диагностики определите причину приостановки перемещения данных системой.  
  
## <a name="see-also"></a>См. также:  
 [Обзор групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Использование панели мониторинга AlwaysOn (среда SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
