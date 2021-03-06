---
description: Миграция данных Sybase ASE в SQL Server — база данных SQL Azure (SybaseToSQL)
title: Перенос данных Sybase ASE в SQL Server в базе данных SQL Azure | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migrating data,Client Side Data Migration
- Migrating data,Server Side Data Migration
ms.assetid: 54a39f5e-9250-4387-a3ae-eae47c799811
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 2268615b8a8ed25883d7d9dce92d8e775f228a4b
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034990"
---
# <a name="migrating-sybase-ase-data-into-sql-server---azure-sql-database--sybasetosql"></a>Миграция данных Sybase ASE в SQL Server — база данных SQL Azure (SybaseToSQL)
После успешной загрузки объектов базы данных адаптивного сервера предприятия (ASE) в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или базе данных SQL Azure можно перенести данные из ASE в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или базу данных SQL Azure.  
  
> [!IMPORTANT]  
> Если используемое ядро является модулем миграции данных на стороне сервера, то перед переносом необходимо установить пакет расширения SSMA для Sybase ASE и поставщики Sybase ASE на компьютере, на котором работает SSMA. Также должна быть запущена служба агент SQL Server. Дополнительные сведения об установке пакета расширений см. в разделе Install [SSMA Components on SQL Server (SybaseToSQL)](./installing-ssma-components-on-sql-server-sybasetosql.md) .  
  
## <a name="setting-migration-options"></a>Настройка параметров миграции  
Перед переносом данных в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или базу данных SQL Azure проверьте параметры миграции проекта в диалоговом окне " **Параметры проекта** ".  
  
-   С помощью этого диалогового окна можно задать такие параметры, как размер пакета миграции, блокировка таблицы, проверка ограничений, обработка значений NULL и обработка значений идентификаторов. Дополнительные сведения о параметрах миграции проекта см. в разделе [Project Settings (Migration) (Sybase)](./project-settings-migration-sybasetosql.md).  
  
    Дополнительные сведения о **параметрах переноса расширенных данных**см. в разделе [Параметры переноса данных](data-migration-settings-sybasetosql.md) .  
  
-   **Модуль миграции** в диалоговом окне **Параметры проекта** позволяет пользователю выполнить процесс миграции с использованием двух типов модулей миграции данных, визуализациям.:  
  
    1.  Модуль миграции данных на стороне клиента  
  
    2.  Модуль миграции данных на стороне сервера  
  
**Перенос данных на стороне клиента:**  
  
-   Чтобы запустить миграцию данных на стороне клиента, выберите в диалоговом окне **Параметры проекта** параметр **модуль миграции данных на стороне клиента** .  
  
-   В **параметрах проекта**параметр **модуля миграции данных на стороне клиента** установлен по умолчанию.  
  
    > [!NOTE]  
    > Модуль переноса данных Client-Side находится внутри приложения SSMA и, следовательно, не зависит от доступности пакета расширений.  
  
**Перенос данных на стороне сервера:**  
  
-   Во время переноса данных на стороне сервера ядро находится в целевой базе данных. Он устанавливается с помощью пакета расширений. Дополнительные сведения об установке пакета расширений см. в разделе Install [SSMA Components on SQL Server (SybaseToSQL)](./installing-ssma-components-on-sql-server-sybasetosql.md) .  
  
-   Чтобы начать миграцию на стороне сервера, выберите параметр **модуль миграции данных на стороне сервера** в диалоговом окне **Параметры проекта** .  
  
> [!NOTE]  
> Если база данных SQL Azure используется в качестве целевой базы данных, то допускается только **Перенос данных на стороне клиента** , а перенос данных на стороне сервера не поддерживается.  
  
## <a name="migrating-data-to-sql-server-or-azure-sql-database"></a>Перенос данных в SQL Server или базу данных SQL Azure  
Миграция данных — это операция групповой загрузки, которая перемещает строки данных из ASE таблиц в SQL Serverные таблицы в транзакциях. Число строк, загруженных в SQL Server или базу данных SQL Azure в каждой транзакции, настраивается в параметрах проекта.  
  
Чтобы просмотреть сообщения о миграции, убедитесь, что панель вывода видна. В противном случае выберите **выходные данные** в меню **вид** .  
  
**Перенос данных**  
  
1.  Проверьте выполнение следующих условий.  
  
    -   Поставщики ASE установлены на компьютере, на котором выполняется SSMA.  
  
    -   Вы выполнили синхронизацию преобразованных объектов с целевой базой данных (SQL Server или базой данных SQL Azure).  
  
2.  В обозревателе метаданных Sybase выберите объекты, содержащие данные, которые необходимо перенести.  
  
    -   Чтобы перенести данные для всех схем, установите флажок рядом с пунктом **схемы**.  
  
    -   Чтобы перенести данные или пропустить отдельные таблицы, сначала разверните схему, разверните узел **таблицы**, а затем установите или снимите флажок рядом с таблицей.  
  
3.  Для миграции данных возникают два варианта:  
  
    **Перенос данных на стороне клиента:**  
  
    Для выполнения **переноса данных на стороне клиента**выберите параметр **модуль миграции данных на стороне клиента** в диалоговом окне " **Параметры проекта** ".  
  
    **Перенос данных на стороне сервера:**  
  
    -   Прежде чем выполнять перенос данных на стороне сервера, убедитесь, что:  
  
        1.  Пакет расширений SSMA для Sybase устанавливается на экземпляре SQL Server.  
  
        2.  Служба агент SQL Server запущена на экземпляре SQL Server  
  
    -   Для выполнения **переноса данных на стороне сервера**выберите параметр **модуль миграции данных на стороне сервера** в диалоговом окне " **Параметры проекта** ".  
  
4.  Щелкните правой кнопкой мыши **схемы** в обозревателе метаданных Sybase и выберите пункт **перенести данные**. Можно также перенести данные для отдельных объектов или категорий объектов: щелкните правой кнопкой мыши объект или его родительскую папку и выберите пункт **перенести данные** .  
  
    > [!NOTE]  
    > Если пакет расширений SSMA для Sybase не установлен на экземпляре SQL Server и выбран **модуль миграции данных на стороне сервера** , то при переносе данных в целевую базу данных возникает следующая ошибка: "SSMA Data Migration Components не найдено в SQL Server, миграция данных на стороне сервера не будет возможна. Убедитесь, что пакет расширений установлен правильно. Нажмите кнопку **Отмена** , чтобы завершить перенос данных.  
  
5.  В диалоговом окне **Подключение к SYBASE ASE** введите учетные данные подключения и нажмите кнопку **подключить**. Дополнительные сведения о подключении к Sybase ASE см. в статье [Подключение к sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)  
  
    Если целевая база данных SQL Server, введите учетные данные подключения в диалоговом окне **Подключение к SQL Server** и нажмите кнопку **подключить**. Дополнительные сведения о подключении к SQL Server см. в разделе [Подключение к SQL Server (SybaseToSQL)](./connecting-to-sql-server-sybasetosql.md) .  
  
    Если целевая база данных является базой данных SQL Azure, введите учетные данные подключения в диалоговом окне **Подключение к базе данных SQL Azure** и нажмите кнопку **подключить**. Дополнительные сведения о подключении к базе данных SQL Azure см. в статье [Подключение к базе данных SQL azure &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
    Сообщения будут отображаться в области **вывода** . По завершении миграции появится **отчет о переносе данных** . Если какие бы то ни было данные не были перенесены, щелкните строку, содержащую ошибки, а затем нажмите кнопку **сведения**. Завершив работу с отчетом, нажмите кнопку **Закрыть**. Дополнительные сведения об отчете о переносе данных см. в разделе [отчет о переносе данных (SSMA Common)](./data-migration-report-sybasetosql.md) .  
  
> [!NOTE]  
> Если в качестве целевой базы данных используется SQL Express Edition, то разрешена только миграция данных на стороне клиента, а миграция данных на стороне сервера не поддерживается.  
  
## <a name="see-also"></a>См. также:  
[Миграция баз данных Sybase ASE в SQL Server — база данных SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
