---
title: Установка компонентов SSMA на SQL Server (MySQLToSql) | Документация Майкрософт
description: Установите компоненты на сервер, на котором выполняется SQL Server для поддержки преобразования базы данных MySQL с помощью SSMA, включая пакет расширений SSMA и поставщиков MySQL.
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- SSMA extension pack, Installation
ms.assetid: 6772d0c5-258f-4d7b-afb0-b5f810e71af1
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: a38808c64209edb094c986e63305707a0a834edb
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823675"
---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>Установка компонентов SSMA на SQL Server (MySQLToSql)

Помимо установки SSMA, необходимо также установить компоненты на компьютере, на котором выполняется [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . К этим компонентам относится пакет расширений SSMA, который поддерживает миграцию данных, и поставщики MySQL для обеспечения подключения между серверами.

## <a name="ssma-for-mysql-extension-pack"></a>Пакет расширений SSMA для MySQL

Пакет расширений SSMA добавляет базу данных **сисдб**к указанному экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Эта база данных содержит таблицы и хранимые процедуры, необходимые для переноса данных.

Кроме того, при переносе данных в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA создает [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] задания агента, когда для переноса данных используется модуль миграции данных на стороне сервера.

### <a name="prerequisites"></a>Предварительные условия

Перед установкой SSMA для серверных компонентов MySQL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Убедитесь, что компьютер соответствует следующим требованиям.

- Установщик [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows версии 3.1 или более поздняя версия.
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] Версия 4.7.2 или более поздняя. Его можно получить в [центре разработчиков .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).
- Поставщик клиента MySQL и подключение к базе данных MySQL, которую необходимо перенести. Вы можете установить поставщики с носителя продукта MySQL или с веб-сайта MySQL.
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Служба браузера должна быть запущена во время установки. Используется для заполнения списка экземпляров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в мастере установки. Службу браузера можно отключить [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] после установки.  

  > [!NOTE]
  > Если [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Служба браузера запущена, но список экземпляров в программе установки по-прежнему не отображается, необходимо разблокировать UDP-порт 1434. Вы можете использовать брандмауэр Windows, чтобы временно разблокировать порт, или временно отключить брандмауэр Windows. Также может потребоваться временное отключение антивирусного по. После установки обязательно включите брандмауэры и антивирусное по.

### <a name="installing-the-extension-pack"></a>Установка пакета расширений

Пакет расширений можно установить в любое время перед переносом данных в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

> [!IMPORTANT]
> Чтобы установить пакет расширений, необходимо быть членом роли сервера **sysadmin** на экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

Чтобы установить пакет расширений, выполните следующие действия.

1. Скопируйте SSMA для **SSMAforMySQLExtensionPack_*n*. msi**, где *n* — номер сборки, на компьютер, на котором работает [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
2. Дважды щелкните **SSMAforMySQLExtensionPack_*n*. msi**.
3. В диалоговом окне **Добро пожаловать** нажмите кнопку **Далее**.
4. В диалоговом окне Лицензионное **соглашение** ознакомьтесь с лицензионным соглашением. Если вы согласны, выберите параметр **я принимаю условия соглашения** , а затем нажмите кнопку **Далее**.
5. В диалоговом окне **Выбор типа установки** выберите вариант **Обычная**.
6. В диалоговом окне **все готово для установки** нажмите кнопку **установить**.
7. В диалоговом окне « **Завершение первого шага установки** » нажмите кнопку **Далее**.

   Появится новое диалоговое окно, в котором будет выбран экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для установки пакета расширений.
  
8. Выберите экземпляр, на [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] котором будут перенесены схемы MySQL, и нажмите кнопку **Далее**.
  
   Имя экземпляра по умолчанию совпадает с именем компьютера. За именованными экземплярами будет следовать обратная косая черта и имя экземпляра.

9. На странице Подключение выберите метод проверки подлинности и нажмите кнопку **Далее**.
  
    При проверке подлинности Windows будут использоваться учетные данные Windows для входа на экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . При выборе проверки подлинности сервера необходимо ввести [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] имя входа и пароль.

10. На следующем шаге необходимо задать пароль для главного ключа, который будет использоваться для шифрования любых конфиденциальных данных, хранящихся в базе данных пакета расширений при переносе данных на стороне сервера. Укажите надежный пароль и нажмите кнопку **Далее**.

11. В следующем диалоговом окне выберите **установить служебные программы база данных *n* и установите библиотеки пакетов расширений**, где *n* — номер версии, а затем нажмите кнопку **Далее**.

    База данных **сисдб** создается с таблицами и хранимыми процедурами, необходимыми для переноса данных (используя модуль миграции данных на стороне сервера) в этой базе данных.

12. Чтобы установить служебные программы на другой экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , выберите **Да**, а затем нажмите кнопку **Далее**. Чтобы выйти из мастера, нажмите кнопку **нет**.

## <a name="see-also"></a>См. также

- [Установка клиента SSMA для MySQL](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)
- [Перенос баз данных MySQL в базу данных SQL Azure SQL Server](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)
