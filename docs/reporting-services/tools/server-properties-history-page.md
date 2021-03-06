---
title: Свойства сервера (страница "Журнал") | Документация Майкрософт
description: Узнайте, как использовать страницу журнала Reporting Services в SQL Server Management Studio с целью задания значения по умолчанию для количества сохраняемых копий журнала отчета.
ms.date: 06/10/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.serverproperties.history.f1
ms.assetid: be9d8018-a46f-4625-9ae1-138ebe6b38ba
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 47238e11a5c4d1b455914fca948dacc680286a14
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913910"
---
# <a name="server-properties-history-page"></a>Свойства сервера (страница «Журнал»)
  Используйте эту страницу [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] в [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] для задания значения по умолчанию для количества сохраняемых копий журнала отчета. Значение по умолчанию предоставляет начальный параметр, который задает пределы объема журнала отчета для всех отчетов. Эти настройки можно изменить для отдельных отчетов.  
  
 Журнал отчета представляет собой коллекцию моментальных снимков отчета, включающих данные отчета и макет на момент создания моментального снимка. Журнал отчета можно использовать для сохранения копии отчета в том виде, какой он имел на конкретную дату и время. Можно создавать и управлять журналом отчета для отдельных отчетов, выполняемых на сервере отчетов, работающем в собственном режиме, или на сервере отчетов, работающем в режиме интеграции с SharePoint.  
  
 Моментальные снимки журнала отчета хранятся в базе данных сервера отчетов. Если количество хранимых моментальных снимков не ограничено, то следует периодически проверять размер базы данных, чтобы убедиться в том, что она не увеличивается слишком быстро и не занимает чрезмерно большой объем дискового пространства.  
  
 Чтобы открыть эту страницу:
 1) Запустите среду [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 2) Подключитесь к экземпляру сервера отчетов.
 3) Щелкните правой кнопкой мыши имя сервера отчетов и выберите пункт **Свойства**.
 4) Нажмите кнопку **Журнал** , чтобы открыть эту страницу.  
  
## <a name="options"></a>Параметры  
 **Хранить в журнале отчета неограниченное количество моментальных снимков**  
 Сохранение всех моментальных снимков журнала отчета. Для уменьшения размера журнала отчетов моментальные снимки нужно удалять вручную.  
  
 **Ограничить количество копий журнала отчета**  
 Сохранение заданного количества моментальных снимков журнала отчета. По достижении предела старые копии будут удаляться из журнала отчетов, чтобы освободить место для новых.  
  
 Если объем журнала отчета будет ограничен позже, при превышении указанного предела объема существующего журнала отчета сервер отчетов сокращает объем журнала до нового предела. Первыми удаляются наиболее старые моментальные снимки отчетов. Если журнал отчетов отсутствует или его объем меньше заданного предела, добавляются новые моментальные снимки отчетов. По достижении предела при добавлении новых моментальных снимков отчетов удаляются наиболее старые моментальные снимки.  
  
## <a name="see-also"></a>См. также:  
 [Установка свойств сервера отчетов (среда Management Studio)](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Подключение к серверу отчетов в среде Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Справка F1 по использованию сервера отчетов среде Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  
