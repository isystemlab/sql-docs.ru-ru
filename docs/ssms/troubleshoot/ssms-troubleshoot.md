---
title: Устранение неполадок, при которых SQL Server Management Studio (SSMS) перестает отвечать на запросы или аварийно завершает работу
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: dnethi
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
manager: jroth
ms.custom: ''
ms.date: 07/01/2019
ms.openlocfilehash: 424b0863da9d0d2cfb56676bed5c368efc4d9349
ms.sourcegitcommit: 0b0f5aba602732834c8439c192d95921149ab4c3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2019
ms.locfileid: "67501191"
---
# <a name="get-diagnostic-data-after-a-sql-server-management-studio-ssms-crash"></a>Получение диагностических данных после аварийного завершения работы SQL Server Management Studio (SSMS)

[Добавить [Применяется к](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)

## <a name="get-full-memory-dump-of-sql-server-management-studio-ssms-when-it-hangs-or-crashes"></a>Создание полного дампа памяти для устранения неполадок с SQL Server Management Studio (SSMS), при которых программа перестает отвечать на запросы или аварийно завершает работу

Чтобы получить диагностические сведения для устранения неполадок, при которых SSMS перестает отвечать на запросы или аварийно завершает работу, выполните следующие действия:

1. Скачайте [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Распакуйте файл в папку.

3. Откройте окно командной строки и выполните следующую команду.

    (командная строка) <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    If it prompts you to accept a license agreement, select *Agree*.

4. Start SSMS, if it hasn't started already.

5. Reproduce the issue.

6. The text should appear in the cmd prompt about writing the dump file, wait for that to finish.

7. Create a new folder and copy the *.dmp file that is written out to that folder.

8. Copy the following files into the same folder.

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"
    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"
    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. Zip up the folder

## Get full memory dump of SSMS when it throws an OutOfMemoryException

You can get a full memory dump with any managed exception.

To capture diagnostic information to troubleshoot an OutOfMemoryException from SSMS, follow the steps below.

1. Download [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Unzip the download into a folder.

3. Open Command Prompt and run the following command.

    ```command prompt
    <PathToProcDumpFolder>\procdump.exe -e 1 -f System.OutOfMemoryException -ma -w ssms.exe
    ```

    При появлении запроса на предоставление согласия с условиями лицензионного соглашения выберите *Принимаю*.

4. Запустите SQL Server Management Studio, если программа еще не запущена.

5. Воспроизведите проблему.

6. В окне командной строки отобразится текст о записи файла дампа. Дождитесь завершения процедуры.

7. Создайте папку и скопируйте в нее созданный DMP-файл.

8. Скопируйте в эту же папку следующие файлы:

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. Запакуйте папку в ZIP-архив.