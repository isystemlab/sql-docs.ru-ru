---
title: Руководство. Создание и использование индексов в столбцах с поддержкой анклава с помощью случайного шифрования | Документация Майкрософт
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 0c22fb10e6264420c95149bb77c2318fdf89a715
ms.sourcegitcommit: 3a64cac1e1fc353e5a30dd7742e6d6046e2728d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67556971"
---
# <a name="tutorial-creating-and-using-indexes-on-enclave-enabled-columns-using-randomized-encryption"></a>Руководство. Создание и использование индексов в столбцах с поддержкой анклава с помощью случайного шифрования
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Из этого руководства вы узнаете, как создавать и использовать индексы в столбцах с поддержкой анклава с помощью случайного шифрования, поддерживаемого в функции [Always Encrypted с безопасными анклавами](encryption/always-encrypted-enclaves.md). Буду рассмотрены следующие темы.

- создание индекса, если у вас есть доступ к ключам (главный ключ столбца и ключ шифрования столбца), которые обеспечивают защиту столбца.
- создание индекса, если у вас нет доступа к ключам, которые обеспечивают защиту столбца.

## <a name="prerequisites"></a>предварительные требования

Это руководство представляет собой продолжение статьи [Руководство. Начало работы с Always Encrypted с безопасными анклавами с использованием SSMS](./tutorial-getting-started-with-always-encrypted-enclaves.md). Убедитесь, что вы полностью изучили его, прежде чем выполнять действия ниже.

## <a name="step-1-enable-accelerated-database-recovery-adr-in-your-database"></a>Шаг 1. Ускорение восстановления базы данных (ADR)

Мы настоятельно рекомендуем вам включить ADR для базы данных, прежде чем создавать первый индекс в столбце с поддержкой анклава с помощью случайного шифрования. Подробные сведения см. в разделе [Восстановление базы данных](./encryption/always-encrypted-enclaves.md##database-recovery) статьи [Always Encrypted с безопасными анклавами](./encryption/always-encrypted-enclaves.md).

1. Закройте все экземпляры SSMS, которые вы использовали при работе с предыдущим руководством. Это приведет к закрытию подключений базы данных, что обязательно для включения ADR.
1. От имени системного администратора откройте новый экземпляр SSMS и подключитесь к своему экземпляру SQL Server **без** включенной функции Always Encrypted для подключения к базе данных.
    1. Запустите SSMS.
    1. В диалоговом окне **Соединение с сервером** укажите имя сервера, выберите метод аутентификации и введите учетные данные.
    1. Нажмите кнопку **Параметры >>** и выберите вкладку **Always Encrypted**.
    1. Убедитесь, что флажок **Включить Always Encrypted (шифрование столбцов)** **не** установлен.
    1. Выберите **Подключиться**.
1. Откройте новое окно запроса и выполните инструкцию ниже, чтобы включить ADR.

   ```sql
   ALTER DATABASE ContosoHR SET ACCELERATED_DATABASE_RECOVERY = ON;
   ```

## <a name="step-2-create-and-test-an-index-without-role-separation"></a>Шаг 2. Создание и тестирование индекса без разделения ролей

На этом шаге вы создадите и протестируете индекс в зашифрованном столбце. Вы будете выступать в качестве отдельного пользователя, который выполняет роли администратора базы данных и владельца данных с доступом к ключам, обеспечивающим защиту данных.

1. Откройте новый экземпляр SSMS и подключитесь к экземпляру SQL Server **с** включенной функцией Always Encrypted для подключения к базе данных.
   1. Создайте новый экземпляр SSMS.
   1. В диалоговом окне **Соединение с сервером** укажите имя сервера, выберите метод аутентификации и введите учетные данные.
   1. Нажмите кнопку **Параметры >>** и выберите вкладку **Always Encrypted**.
   1. Установите флажок **Включить Always Encrypted (шифрование столбцов)** и укажите URL-адрес аттестации анклава (например, ht<span>tp://<span>hgs.bastion.local/Attestation).
   1. Выберите **Подключиться**.
   1. Если отобразится запрос на включение параметризации для запросов Always Encrypted, нажмите кнопку **Включить**.
1. Если отобразится запрос на включение параметризации для Always Encrypted, обязательно включите ее.
   1. Выберите пункт **Инструменты** в главном меню SSMS.
   2. Выберите **Параметры**.
   3. Выберите **Выполнение запроса** > **SQL Server** > **Дополнительно**.
   4. Убедитесь, что установлен флажок **Включить параметризацию для Always Encrypted**.
   5. Нажмите кнопку **ОК**.
1. Откройте окно запроса и выполните инструкции ниже, чтобы зашифровать столбец **LastName** в таблице **Employees**. Вы создадите и будете использовать индекс в таком столбце на следующих шагах.

   ```sql
   USE [ContosoHR];
   GO   
   ALTER TABLE [dbo].[Employees]
   ALTER COLUMN [LastName] [nvarchar](50) COLLATE Latin1_General_BIN2 
   ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized    ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
   GO   
   ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
   GO
   ```

1. Создайте индекс в столбце **LastName**. Так как вы подключены к базе данных с включенной функцией Always Encrypted, драйвер клиента в SSMS прозрачно предоставит **CEK1** (ключ шифрования столбца, обеспечивающий защиту столбца **LastName**) анклаву, что необходимо для создания индекса.

   ```sql
   USE [ContosoHR];
   GO

   CREATE INDEX IX_LastName ON [Employees] ([LastName])
   INCLUDE ([EmployeeID], [FirstName], [SSN], [Salary]);
   GO
   ```

1. Выполните полнофункциональный запрос к столбцу **LastName** и убедитесь, что SQL Server использует индекс при выполнении запроса.
   1. В том же или в новом окне запроса убедитесь, что кнопка **Включить динамическую статистику запросов** на панели инструментов активирована.
   1. Выполните приведенный ниже запрос.

       ```sql
       USE [ContosoHR];
       GO

       DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
       SELECT * FROM [dbo].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
       GO
      ```

   1. На вкладке **Статистика динамических запросов** (в нижней части окна запроса) убедитесь, что запрос использует индекс.

## <a name="step-3-create-an-index-with-role-separation"></a>Шаг 3. Создание индекса с разделением ролей

На этом шаге вы создадите индекс в зашифрованном столбце от имени двух разных пользователей. Один пользователь — это администратор баз данных, который требуется для создания индекса, но который не имеет доступа к ключам. Другой пользователь — это владелец данных с доступом к ключам.

1. Используя экземпляр SSMS **без** включенной функции Always Encrypted, выполните инструкцию ниже, чтобы очистить индекс в столбце **LastName**.

   ```sql
   USE [ContosoHR];
   GO

   DROP INDEX IX_LastName ON [Employees]; 
   GO
   ```

1. От имени владельца данных (или приложения с доступом к ключам) поместите **CEK1** в кэш в анклаве.

   > [!NOTE]
   > Если вы не перезапустили экземпляр SQL Server после **шага 2 (создание и тестирование индекса без разделения ролей)** , этот шаг выполнять не нужно, так как **CEK1** уже присутствует в кэше. Мы добавили его, чтобы продемонстрировать, как владелец данных может передать ключ в анклав, если он еще не присутствует в нем.

   1. В экземпляре SSMS **с** включенной функцией Always Encrypted выполните в окне запроса приведенные ниже инструкции. Эта инструкция отправит все ключи шифрования столбцов с поддержкой анклава в анклав. Подробные сведения см. в статье [sp_enclave_send_keys (Transact-SQL)](../system-stored-procedures/sp-enclave-send-keys-sql.md).

        ```sql
        USE [ContosoHR];
        GO

        EXEC sp_enclave_send_keys;
        GO
        ```

   1. В качестве альтернативы для вызова указанной выше хранимой процедуры вы можете выполнить запрос DML, который применяет анклав к столбцу **LastName**. Таким образом в анклав будет введен только **CEK1**.

        ```sql
        USE [ContosoHR];
        GO

        DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
        SELECT * FROM [dbo].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
        GO
        ```

1. Создайте индекс от имени администратора баз данных.
    1. В экземпляре SSMS **без** включенной функции Always Encrypted выполните в окне запроса приведенные ниже инструкции.

        ```sql
        USE [ContosoHR];
        GO

        CREATE INDEX IX_LastName ON [Employees] ([LastName])
        INCLUDE ([EmployeeID], [FirstName], [SSN], [Salary]);
        GO
        ```

1. От имени владельца данных выполните полнофункциональный запрос к столбцу **LastName** и убедитесь, что SQL Server использует индекс при выполнении запроса.
   1. В экземпляре SSMS **с** включенной функцией Always Encrypted выберите существующее окно запроса или откройте новое и убедитесь, что кнопка **Включить динамическую статистику запросов** на панели инструментов активирована.
   1. Выполните приведенный ниже запрос. 

        ```sql
        USE [ContosoHR];
        GO

        DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
        SELECT * FROM [dbo].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
        GO
        ```

   1. На вкладке **Статистика динамических запросов** (в нижней части окна запроса) убедитесь, что запрос использует индекс.

## <a name="next-steps"></a>Следующие шаги

- Подробные сведения о других сценариях использования для Always Encrypted с безопасными анклавами см. в статье [Настройка Always Encrypted с безопасными анклавами](encryption/configure-always-encrypted-enclaves.md).