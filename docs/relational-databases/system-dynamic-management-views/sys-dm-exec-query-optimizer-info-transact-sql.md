---
description: sys.dm_exec_query_optimizer_info (Transact-SQL)
title: sys. dm_exec_query_optimizer_info (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_optimizer_info_TSQL
- dm_exec_query_optimizer_info
- sys.dm_exec_query_optimizer_info_TSQL
- sys.dm_exec_query_optimizer_info
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_optimizer_info dynamic management view
ms.assetid: 1d72cef1-22d8-4ae0-91db-6694fe918c9e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9678d237863801b4ecad49167d1930a694859bae
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546653"
---
# <a name="sysdm_exec_query_optimizer_info-transact-sql"></a>sys.dm_exec_query_optimizer_info (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Возвращает подробные статистики по операциям оптимизатора запросов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Это представление можно использовать для настройки рабочей нагрузки при обнаружении проблем, связанных с оптимизацией запросов, или для улучшения производительности обработки запросов. Например, можно использовать общее число оптимизаций, значение затрачиваемого времени и значение конечной стоимости для сравнения с оптимизацией запросов текущей рабочей нагрузки и любыми изменениями во время процесса настройки. Некоторые счетчики предоставляют данные, которые могут быть использованы только для внутренней диагностики [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Эти счетчики помечены атрибутом «Только для внутреннего использования.».  
  
> [!NOTE]  
>  Чтобы вызвать эту функцию из [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] или [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , используйте имя **sys. dm_pdw_nodes_exec_query_optimizer_info**.  
  
|Имя|Тип данных|Описание|  
|----------|---------------|-----------------|  
|**подписан**|**nvarchar(4000)**|Имя события статистики оптимизатора.|  
|**occurrence**|**bigint**|Количество вхождений события оптимизации для этого счетчика.|  
|**value**|**float**|Среднее значение свойства для вхождения события.|  
|**pdw_node_id**|**int**|**Применимо к**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Идентификатор узла, на котором находится данное распределение.|  
  
## <a name="permissions"></a>Разрешения  

В [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] необходимо `VIEW SERVER STATE` разрешение.   
На [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] уровнях Premium требуется `VIEW DATABASE STATE` разрешение в базе данных. На [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] уровнях Standard и Basic требуется  **Администратор сервера** или учетная запись **администратора Azure Active Directory** .   
    
## <a name="remarks"></a>Примечания  
 **sys. dm_exec_query_optimizer_info** содержит следующие свойства (счетчики). Все значения частотности рассматриваются совокупно и при перезапуске системы устанавливаются в 0. Все значения полей значений при перезапуске системы устанавливаются в NULL. Все значения значимых столбцов, по которым определяется среднее, используют значение частотности из той же строки, что и знаменатель в вычислении среднего. Все оптимизации запросов измеряются, когда [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] определяет изменения в **dm_exec_query_optimizer_info**, включая запросы, создаваемые пользователями и системой. Выполнение уже кэшированного плана не изменяет значения в **dm_exec_query_optimizer_info**, учитываются только оптимизации.  
  
|Счетчик|Наличие|Значение|  
|-------------|----------------|-----------|  
|оптимизации|Общее число операций оптимизации.|Не применяются|  
|затраченное время|Общее число операций оптимизации.|Среднее время, затраченное на оптимизацию отдельной инструкции (запроса), в секундах.|  
|окончательные затраты|Общее число операций оптимизации.|Средняя оценка затрат для оптимизированного плана во внутренних единицах затрат.|  
|обычный план|Только для внутреннего использования.|Только для внутреннего использования.|  
|задачи|Только для внутреннего использования.|Только для внутреннего использования.|  
|без плана|Только для внутреннего использования.|Только для внутреннего использования.|  
|search 0|Только для внутреннего использования.|Только для внутреннего использования.|  
|search 0 time|Только для внутреннего использования.|Только для внутреннего использования.|  
|search 0 tasks|Только для внутреннего использования.|Только для внутреннего использования.|  
|search 1|Только для внутреннего использования.|Только для внутреннего использования.|  
|search 1 time|Только для внутреннего использования.|Только для внутреннего использования.|  
|search 1 tasks|Только для внутреннего использования.|Только для внутреннего использования.|  
|поиск 2|Только для внутреннего использования.|Только для внутреннего использования.|  
|время поиска 2|Только для внутреннего использования.|Только для внутреннего использования.|  
|задачи поиска 2|Только для внутреннего использования.|Только для внутреннего использования.|  
|gain stage 0 to stage 1|Только для внутреннего использования.|Только для внутреннего использования.|  
|выигрыш при переходе от стадии 1 к стадии 2|Только для внутреннего использования.|Только для внутреннего использования.|  
|timeout|Только для внутреннего использования.|Только для внутреннего использования.|  
|превышение предела памяти|Только для внутреннего использования.|Только для внутреннего использования.|  
|инструкции insert|Количество операций оптимизации для инструкций INSERT.|Не применяются|  
|инструкции delete|Количество операций оптимизации для инструкций DELETE.|Не применяются|  
|инструкции update|Количество операций оптимизации для инструкций UPDATE.|Не применяются|  
|содержащие вложенный запрос|Количество операций оптимизации для запросов, содержащих как минимум один вложенный запрос.|Не применяются|  
|сбой устранения вложенности|Только для внутреннего использования.|Только для внутреннего использования.|  
|В таблицах|Общее число операций оптимизации.|Среднее число таблиц, на которые ссылается оптимизированный запрос.|  
|указания|Количество раз, когда было задано указание. Подсчитанные подсказки включают в себя указания запросов соединения, ГРУППИРОВАНия, объединения и ПРИНУДИТЕЛЬного УПОРЯДОЧЕНия, параметр ПРИНУДИТЕЛЬного задания плана и указания соединения.|Не применяются|  
|указание упорядочивания|Количество раз, когда было задано указание принудительного упорядочивания.|Не применяются|  
|указание соединения|Количество раз, когда по указанию соединения принудительно вызывался алгоритм соединения.|Не применяются|  
|обращение к представлению|Количество раз, когда производилось обращение к представлению в запросе.|Не применяются|  
|удаленный запрос|Количество операций оптимизации, при которых запрос обращался как минимум к одному удаленному источнику данных, например к таблице с четырехкомпонентным именем или результату инструкции OPENROWSET.|Не применяются|  
|максимальное DOP|Общее число операций оптимизации.|Среднее эффективное значение MAXDOP для оптимизированного плана. По умолчанию действующее значение MAXDOP определяется параметром конфигурации сервера **max degree of parallelism** и может быть переопределено для конкретного запроса по значению подсказки запроса MAXDOP.|  
|максимальный уровень рекурсии|Количество операций оптимизации, в которых был задан уровень MAXRECURSION больше 0 в рамках указания запроса.|Средний уровень MAXRECURSION в операциях оптимизации, для которых был задан максимальный уровень рекурсии в рамках указания запроса.|  
|загруженные индексированные представления|Только для внутреннего использования.|Только для внутреннего использования.|  
|сопоставленные индексированные представления|Количество операций оптимизации, в которых было сопоставлено одно или несколько индексированных представлений.|Среднее количество сопоставленных представлений.|  
|использованные индексированные представления|Количество операций оптимизации, для которых в выходном плане было использовано одно или несколько индексированных представлений после согласования.|Среднее количество использованных представлений.|  
|обновленные индексированные представления|Количество операций оптимизации DML-инструкции, выдающих план, обслуживающий одно или несколько индексированных представлений.|Среднее количество обслуженных представлений.|  
|запрос динамического курсора|Количество операций оптимизации, для которых был указан запрос динамического курсора.|Не применяются|  
|запрос быстрого перемещения курсора вперед|Количество операций оптимизации, для которых был указан запрос однопроходного курсора.|Не применяются|  
|merge stmt|Количество операций оптимизации для инструкций MERGE.|Не применяются|  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-viewing-statistics-on-optimizer-execution"></a>A. Просмотр статистики выполнения оптимизатора  
 Каковы текущие статистики выполнения оптимизатора для данного экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]?  
  
```  
SELECT * FROM sys.dm_exec_query_optimizer_info;  
```  
  
### <a name="b-viewing-the-total-number-of-optimizations"></a>Б. Просмотр общего количества операций оптимизации  
 Количество выполняемых операций оптимизации.  
  
```  
SELECT occurrence AS Optimizations FROM sys.dm_exec_query_optimizer_info  
WHERE counter = 'optimizations';  
```  
  
### <a name="c-average-elapsed-time-per-optimization"></a>В. Среднее время, затраченное на операцию оптимизации  
 Каково среднее время, затраченное на операцию оптимизации?  
  
```  
SELECT ISNULL(value,0.0) AS ElapsedTimePerOptimization  
FROM sys.dm_exec_query_optimizer_info WHERE counter = 'elapsed time';  
```  
  
### <a name="d-fraction-of-optimizations-that-involve-subqueries"></a>Г. Доля операций оптимизации, в которых задействованы вложенные запросы  
 Доля оптимизированных запросов, содержащих вложенные запросы.  
  
```  
SELECT (SELECT CAST (occurrence AS float) FROM sys.dm_exec_query_optimizer_info WHERE counter = 'contains subquery') /  
       (SELECT CAST (occurrence AS float)   
        FROM sys.dm_exec_query_optimizer_info WHERE counter = 'optimizations')  
        AS ContainsSubqueryFraction;  
```  
  
## <a name="see-also"></a>См. также:  
 [Динамические административные представления и функции (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Динамические административные представления и функции, связанные с выполнением (Transact-SQL)](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


