---
title: Экспорт в файл изображения (построитель отчетов) | Документация Майкрософт
description: В построителе отчетов модуль подготовки отчетов для изображений преобразует отчет с разбиением на страницы в битовую карту или метафайл. По умолчанию используется TIFF-файл, отображаемый на нескольких страницах.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 020d8ea2-de07-4212-a2bb-2ed0df2c8db8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d5a3bd0cd2dfdba8b34ff6dc97f56fb3eaf53306
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/29/2020
ms.locfileid: "80342843"
---
# <a name="exporting-to-an-image-file-report-builder-and-ssrs"></a>Экспорт в файл изображения (построитель отчетов и службы SSRS)
  Модуль подготовки отчетов изображений преобразует отчет с разбиением на страницы в битовую карту или метафайл. По умолчанию модуль подготовки изображения создает отчет в файле TIFF, который можно просматривать на нескольких страницах. Полученное изображение клиент может просмотреть в программе просмотра изображений и распечатать. В этом разделе содержатся сведения о модуле подготовки изображений и описаны исключения из правил подготовки к просмотру.  
  
 Модуль подготовки изображений создает файлы в форматах, поддерживаемых [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]: BMP, EMF, EMFPlus, GIF, JPEG, PNG и TIFF. Если используется формат TIFF, то файлу для главного потока будет присвоено имя *имя_отчета*.tif. Для других форматов, которые формируются по принципу "одна страница в одном файле", файлу будет присвоено имя *имя_отчета_страница.ext* , где *ext* — расширение файла в зависимости от выбранного формата. Чтобы создать файл в другом поддерживаемом формате изображений, укажите в параметре **OutputFormatDeviceInfo** любую из перечисленных выше строк.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="supported-image-formats"></a><a name="SupportedImageFormats"></a> Поддерживаемые форматы изображения  
 В следующей таблице приведены расширения имени файла и тип MIME для каждого формата модуля подготовки изображений.  
  
|**Тип**|**Расширение**|**MIMEType**|  
|--------------|-------------------|------------------|  
|BMP|BMP|image/bmp|  
|GIF|GIF|image/gif|  
|JPEG|JPEG|image/jpeg|  
|PNG|png|image/png|  
|TIFF|tif|image/tiff|  
|EMF|EMF|image/emf|  
|EMFPlus|EMF|image/emf|  
  
  
##  <a name="rendering-multiple-pages"></a><a name="RenderingMultiplePages"></a> Подготовка к просмотру нескольких страниц  
 TIFF — это единственный формат, который позволяет представлять многостраничные документы в едином файле. Другие форматы, такие как JPG или PNG, выводят по одной странице одновременно и требуют отдельного вызова модуля подготовки отчетов для подготовки к просмотру каждой страницы.  
  
  
##  <a name="interactivity"></a><a name="Interactivity"></a> Интерактивность  
 Интерактивные возможности не поддерживаются ни одним из форматов изображения, формируемых этим модулем подготовки отчетов. Не обрабатываются следующие интерактивные элементы.  
  
-   Гиперссылки  
  
-   Показать или скрыть  
  
-   Схема документа  
  
-   Ссылки с детализацией или дополнительной информацией  
  
-   Сортировка конечным пользователем  
  
-   Фиксированные заголовки  
  
-   Закладки  
  
  
##  <a name="device-information-settings"></a><a name="DeviceInfo"></a> Настройки сведений об устройстве  
 Некоторые параметры по умолчанию для этого модуля подготовки отчетов можно изменить через настройку сведений об устройстве. Дополнительные сведения см. в разделе [Image Device Information Settings](../../reporting-services/image-device-information-settings.md).  
  
  
## <a name="see-also"></a>См. также:  
 [Разбиение на страницы в службах Reporting Services (построитель отчетов и службы SSRS)](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Поведение при подготовке к просмотру (построитель отчетов и службы SSRS)](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Интерактивные возможности различных модулей подготовки отчетов к просмотру (построитель отчетов и службы SSRS)](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Подготовка к просмотру элементов отчета (построитель отчетов и службы SSRS)](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Таблицы, матрицы и списки (построитель отчетов и службы SSRS)](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
