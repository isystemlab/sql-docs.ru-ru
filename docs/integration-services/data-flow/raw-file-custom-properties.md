---
description: Пользовательские свойства необработанного файла
title: Пользовательские свойства необработанного файла | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7e81f7e1-fac0-4b57-b145-8f1b9e4720bf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5b1b7f0e1416b20ce641848abe47d3497f7c7b7f
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196412"
---
# <a name="raw-file-custom-properties"></a>Пользовательские свойства необработанного файла

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **Пользовательские свойства источника**  
  
 Источник «Необработанный файл» обладает как пользовательскими свойствами, так и свойствами, общими для всех компонентов потока данных.  
  
 В следующей таблице описаны пользовательские свойства источника «Необработанный файл». Все свойства доступны для чтения и записи.  
  
|Имя свойства|Тип данных|Описание|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (перечисление)|Режим, используемый для доступа к необработанным данным. Допустимые значения: **File name** (0) и **File name from variable** (1). Значение по умолчанию — **File name** (0).|  
|FileName|Строка|Полный путь и имя исходного файла.|  
  
 Вывод и выходные столбцы источника «Необработанный файл» не имеют пользовательских свойств.  
  
 Дополнительные сведения см. в статье [Raw File Source](../../integration-services/data-flow/raw-file-source.md).  
  
 **Пользовательские свойства назначений**  
  
 Назначение «Необработанный файл» обладает как пользовательскими свойствами, так и свойствами, общими для всех компонентов потока данных.  
  
 В следующей таблице описаны пользовательские свойства назначения «Необработанный файл». Все свойства доступны для чтения и записи.  
  
|Имя свойства|Тип данных|Описание|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (перечисление)|Значение, указывающее, содержит ли свойство FileName имя файла, или указывающее переменную, которая содержит имя файла. Возможные варианты: **File name** (0) и **File name from variable** (1).|  
|FileName|Строка|Имя файла, в который назначение «Необработанный файл» осуществляет запись.|  
|WriteOption|Integer (перечисление)|Значение, указывающее, следует ли назначению «Необработанный файл» удалять существующий файл с таким же именем. Возможные варианты: **Create Always** (0), **Create Once** (1), **Truncate and Append** (3) и **Append** (2). По умолчанию для этого свойства используется значение **Create Always** (0).|  
  
> [!NOTE]  
>  Операция добавления в файл требует, чтобы метаданные добавляемых данных совпадали с метаданными данных, уже содержащихся в файле.  
  
 У ввода и входных столбцов назначения «Необработанный файл» нет пользовательских свойств.  
  
 Дополнительные сведения см. в статье [Raw File Destination](../../integration-services/data-flow/raw-file-destination.md).  
  
## <a name="see-also"></a>См. также  
 [Общие свойства](./set-the-properties-of-a-data-flow-component.md)  
  
