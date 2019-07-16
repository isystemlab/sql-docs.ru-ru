---
title: Назначение "Гибкая работа с файлами" | Документы Майкрософт
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpextfiledest.f1
- sql14.dts.designer.afpextfiledest.f1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2a0ffa4b881fe550aba6c547fcea690932eef110
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66462612"
---
# <a name="flexible-file-destination"></a>Назначение "Гибкая работа с файлами"

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Назначение **Гибкая работа с файлами** позволяет пакету служб SSIS записывать данные в различных поддерживаемых службах хранилища.

Сейчас поддерживаются службы хранилища

- [Хранилище BLOB-объектов Azure](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage 2-го поколения](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)
   
Перетащите назначение **Гибкая работа с файлами** в конструктор потока данных и дважды щелкните его, чтобы открыть редактор.
  
Назначение **Гибкая работа с файлами** входит в состав [пакета дополнительных компонентов SQL Server Integration Services (SSIS) для Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  

Доступны следующие свойства **редактора назначения "Гибкая работа с файлами"** .

- **Тип диспетчера соединений с файлами**. Определяет тип диспетчера подключений к источникам. Затем выберите один из указанных типов или создайте новый.
- **Путь к папке**. Указывает путь к папке назначения.
- **Имя файла.** Указывает имя файла назначения.
- **Формат файла**. Указывает формат файла назначения. Поддерживаемые форматы: **текст**, **Avro**, **ORC**, **Parquet**.
- **Знак-разделитель столбцов**. Указывает символ, используемый в качестве разделителя столбцов (многосимвольные разделители не поддерживаются).
- **Использовать первую строку в качестве имен столбцов**. Указывает, следует ли записывать в первую строку имена столбцов.
- **Сжать файл**. Указывает, сжимать ли файл.
- **Тип сжатия**. Указывает используемый формат сжатия. Поддерживаемые форматы: **GZIP**, **DEFLATE**, **BZIP2**.
- **Уровень сжатия**. Указывает используемый уровень сжатия.

Доступны следующие свойства **расширенного редактора**.

- **rowDelimiter:** символ, используемый для разделения строк в файле. Допускается только один знак. Значение по умолчанию — **\r\n**.
- **escapeChar:** Специальный символ, используемый для экранирования разделителя столбцов в содержимом входного файла. Не следует указывать escapeChar и quoteChar для таблицы одновременно. Допускается только один знак. Нет значения по умолчанию.
- **quoteChar:** Символ, используемый для заключения строкового значения в кавычки. Разделители столбцов и строк внутри знаков кавычек будут рассматриваться как часть строкового значения. Это свойство применяется к входному и выходному наборам данных. Не следует указывать escapeChar и quoteChar для таблицы одновременно. Допускается только один знак. Нет значения по умолчанию.
- **nullValue:** один или несколько символов, используемых для представления значения NULL. Значением **по умолчанию** является \N.
- **encodingName:** задает имя кодировки. См. раздел [Encoding.EncodingName](https://docs.microsoft.com/en-us/dotnet/api/system.text.encoding?redirectedfrom=MSDN&view=netframework-4.8).
- **skipLineCount:**  указывает количество непустых строк, которые нужно пропустить при чтении данных из входных файлов. Если указаны skipLineCount и firstRowAsHeader, то сначала пропускаются строки, а затем считываются данные заголовка из входного файла.
- **treatEmptyAsNull:** Указывает, следует ли интерпретировать NULL или пустую строку как значение NULL при считывании данных из входного файла. Значение **по умолчанию** — true.

После указания сведений о соединении переключитесь на страницу **Столбцы** , чтобы сопоставить столбцы источника со столбцами назначения для потока данных служб SSIS.

**Необходимое условие для использования формата файлов ORC или Parquet**.

Для использования формата файла ORC и Parquet требуется Java.
Архитектура сборки Java (32- или 64-разрядная) должна соответствовать архитектуре используемой среды выполнения SSIS.
Были протестированы следующие сборки Java:

- [Zulu OpenJDK 8u192](https://www.azul.com/downloads/zulu/zulu-windows/)
- [Среда выполнения Oracle Java SE 8u192](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)

**Настройка Zulu's OpenJDK**

1. Скачайте и извлеките ZIP-пакет установки.
2. Запустите `sysdm.cpl` из командной строки.
3. На вкладке **Дополнительно** выберите **Переменные среды**.
4. В разделе **Системные переменные** выберите **Создать**.
5. Введите `JAVA_HOME` в поле **Имя переменной**.
6. Выберите **Обзор каталога**, перейдите к извлеченной папке и выберите вложенную папку `jre`.
   Затем нажмите кнопку **ОК**. **Значение переменной** заполняется автоматически.
7. Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Создание системной переменной**.
8. Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Переменные среды**.
9. Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Свойства системы**.

**Настройка среды выполнения Oracle Java SE**

1. Скачайте и запустите EXE-установщик.
2. Следуйте указаниям установщика, чтобы завершить настройку.