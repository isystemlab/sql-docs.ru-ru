---
description: sp_addsrvrolemember (Transact-SQL)
title: sp_addsrvrolemember (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addsrvrolemember
- sp_addsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addsrvrolemember
ms.assetid: 777f0e09-8ee5-4cb2-a3ac-939d02c3cd22
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ec0b94d4423574729d4c92d869a73d04673edac8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536750"
---
# <a name="sp_addsrvrolemember-transact-sql"></a>sp_addsrvrolemember (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Добавляет имя входа в качестве члена предопределенной роли сервера.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Вместо этого используйте [инструкцию ALTER Server Role](../../t-sql/statements/alter-server-role-transact-sql.md) .  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_addsrvrolemember [ @loginame= ] 'login'   
    , [ @rolename = ] 'role'  
```  
  
## <a name="arguments"></a>Аргументы  
 [ @loginame **=** ] **"**_Login_**"**  
 Имя входа, добавляемое к предопределенной роли сервера. Аргумент *Login* имеет тип **sysname**и не имеет значения по умолчанию. *имя входа* может быть именем входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или именем входа Windows. Если имени входа Windows еще не был предоставлен доступ к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], он предоставляется автоматически.  
  
 [ @rolename **=** ] **"**_роль_**"**  
 Имя предопределенной роли сервера, к которой добавляется имя входа. Аргумент *Role* имеет тип **sysname**, значение по умолчанию NULL и должен иметь одно из следующих значений:  
  
-   sysadmin  
  
-   securityadmin  
  
-   serveradmin  
  
-   setupadmin  
  
-   processadmin  
  
-   diskadmin  
  
-   dbcreator  
  
-   bulkadmin  

## <a name="return-code-values"></a>Значения кода возврата  
 0 (успешное завершение) или 1 (неуспешное завершение)  
  
## <a name="remarks"></a>Примечания  
 При добавлении имени входа к предопределенной роли сервера, оно получает разрешения, связанные с этой ролью.  
  
 Нельзя изменить членство в роли имени входа sa и public.  
  
 Для добавления члена к фиксированной или пользовательской роли базы данных используется хранимая процедура sp_addrolemember.  
  
 Процедуру sp_addsrvrolemember нельзя выполнять в пользовательской транзакции.  
  
## <a name="permissions"></a>Разрешения  
 Требует членства в роли, к которой добавляется новый элемент.  
  
## <a name="examples"></a>Примеры  
 В следующем примере имя входа Windows добавляется `Corporate\HelenS` к `sysadmin` предопределенной роли сервера.  
  
```  
EXEC sp_addsrvrolemember 'Corporate\HelenS', 'sysadmin';  
GO  
```  
  
## <a name="see-also"></a>См. также  
 [Хранимые процедуры безопасности (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Хранимая процедура sp_addrolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Функции безопасности (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md)   
 [CREATE SERVER ROLE (Transact-SQL)](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE (Transact-SQL)](../../t-sql/statements/drop-server-role-transact-sql.md)  
  
  
