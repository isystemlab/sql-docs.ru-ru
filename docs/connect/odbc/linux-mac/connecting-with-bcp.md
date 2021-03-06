---
title: Соединение с помощью bcp
description: Узнайте, как использовать служебную программу bcp с Microsoft ODBC Driver for SQL Server в Linux и macOS.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bcp
ms.assetid: 3eca5717-e50f-40db-be16-a1cebbdfee70
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b66ebab16bc26beec9ef9cd8699f53e75d36d478
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727446"
---
# <a name="connecting-with-bcp"></a>Соединение с помощью bcp
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Служебная программа [bcp](../../../tools/bcp-utility.md) доступна с [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] на платформах Linux и macOS. На этой странице описаны отличия от версии `bcp` для Windows.
  
- Признаком конца поля является символ табуляции ("\t").  
  
- Признаком конца строки является символ новой строки ("\n").  
  
- Текстовый режим является предпочтительным форматом для файлов формата `bcp` и файлов данных, которые не содержат символы национального алфавита.  
  
> [!NOTE]  
> Обратная косая черта "\\" в аргументе командной строки должна быть заключена в кавычки или экранирована. Например, чтобы указать символ новой строки в качестве пользовательского признака конца строки, необходимо использовать один из следующих способов:  
>   
> -   -r\\\n  
> -   -r"\n"  
> -   -r'\n'  
  
Ниже приведен пример вызова команды `bcp` для копирования строк таблицы в текстовый файл:  
  
```  
bcp AdventureWorks2008R2.Person.Address out test.dat -Usa -Pxxxx -Sxxx.xxx.xxx.xxx  
```  
  
## <a name="available-options"></a>Доступные параметры
В текущем выпуске доступны следующие параметры и элементы синтаксиса:  

[_database_ **.** ]_schema_ **.** _table_ **in** _data\_file_ | **out** _data\_file_

- -a *packet_size*  
Указывает число байтов в каждом сетевом пакете, отправляемом от сервера и к серверу.  
  
- -b *batch_size*  
Указывает количество строк в каждом пакете импортированных данных.  
  
- -c  
Использует символьный тип данных.  
  
- -d *database_name*  
Указывает базу данных, с которой надо соединиться.  
  
- -d  
Значение, передаваемое в параметр `bcp` -S, интерпретируется как имя источника данных (DSN). Дополнительные сведения см. в разделе "Поддержка имени DSN в sqlcmd и bcp" статьи [Соединение с помощью sqlcmd](connecting-with-sqlcmd.md).  
  
- -e *error_file* Указывает полный путь к файлу ошибок, используемому для хранения строк, которые программа `bcp` не может передать из файла в базу данных.  
  
- -E  
Использует значение или значения идентификаторов в файле импортированных данных для столбца идентификаторов.  
  
- -f *format_file*  
Указывает полный путь к файлу форматирования.  
  
- -F *first_row*  
Указывает номер первой строки для экспорта из таблицы или импорта из файла данных.  
  
- -k  
Указывает, что пустые столбцы во время данной операции должны сохранить значение NULL вместо любых вставляемых значений столбцов по умолчанию.  
  
- -l  
Указывает время ожидания входа. Параметр -l задает время ожидания (в секундах) для входа в [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] при попытке соединения с сервером. Значение времени ожидания по умолчанию — 15 секунд. Время ожидания входа должно быть числом в диапазоне от 0 до 65 534. Если указанное значение не является числом или выходит за пределы указанного диапазона, программа `bcp` выдает сообщение об ошибке. Значение 0 обозначает бесконечное время ожидания.
  
- -L *last_row*  
Указывает номер последней строки для экспорта из таблицы или импорта из файла данных.  
  
- -m *max_errors*  
Указывает максимальное количество синтаксических ошибок, которые могут произойти до отмены операции программы `bcp`.  
  
- -n  
Использует собственные типы данных (базы данных) для выполнения операции массового копирования.  
  
- -P *password*  
Указывает пароль для идентификатора имени входа.  
  
- -Q  
Выполняет инструкцию SET QUOTED_IDENTIFIERS ON в соединении между программой `bcp` и экземпляром [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
- -r *row_terminator*  
Указывает признак конца строки.  
  
- -R  
Указывает, что массовое копирование в [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] данных в денежном формате, в формате даты и времени выполняется с помощью регионального формата, определенного настройками локали клиентского компьютера.  
  
- -S *server*  
Задает имя экземпляра [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], к которому требуется подключиться, или имя DSN при использовании с параметром -D.  
  
- -t *field_terminator*  
Указывает признак конца поля.  
  
- -T  
Указывает, что служебная программа `bcp` устанавливает доверительное соединение с [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (встроенная безопасность).  
  
- -U *login_id*  
Указывает идентификатор входа, используемый для соединения с [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
- -v  
Выводит номер версии и сведения об авторских правах для программы `bcp`.  
  
- -w  
Использует символы Юникода для выполнения операции массового копирования.  
  
В этом выпуске поддерживаются символы Latin-1 и UTF-16.  
  
## <a name="unavailable-options"></a>Недоступные параметры
В текущем выпуске недоступны следующие параметры и элементы синтаксиса:  

- -c  
Указывает кодовую страницу данных в файле данных.  
  
- -h *hint*  
Указывает одну или несколько подсказок, используемых во время выполнения массового импорта данных в таблицу или представление.  
  
- -i *input_file*  
Указывает имя файла ответов.  
  
- -N  
Использует собственные типы данных (базы данных) для несимвольных данных и символы Юникода для символьных данных.  
  
- -o *output_file*  
Указывает имя файла, который принимает перенаправленные из командной строки выходные данные.  
  
- -V (80 | 90 | 100)  
Использует типы данных из более ранней версии [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
- -X  
При использовании вместе с параметрами format и -f format_file приводит к созданию файла форматирования на основе XML. По умолчанию создается файл форматирования в формате, отличном от XML.  
  
## <a name="see-also"></a>См. также:

[Соединение с помощью **sqlcmd**](connecting-with-sqlcmd.md)  
[Заметки о выпуске](release-notes-tools.md)