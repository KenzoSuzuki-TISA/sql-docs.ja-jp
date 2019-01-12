---
title: sp_addsrvrolemember (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 80de1581116ddc477ee1d5b8197532a853ee3da7
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2019
ms.locfileid: "54130522"
---
# <a name="spaddsrvrolemember-transact-sql"></a>sp_addsrvrolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ログインを固定サーバー ロールのメンバーとして追加します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md)代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addsrvrolemember [ @loginame= ] 'login'   
    , [ @rolename = ] 'role'  
```  
  
## <a name="arguments"></a>引数  
 [ @loginame **=** ] **'**_ログイン_**'**  
 固定サーバー ロールに追加するログインの名前を指定します。 *ログイン*は**sysname**、既定値はありません。 *ログイン*できます、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインまたは Windows ログインします。 Windows ログインに対して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] へのアクセスが許可されていない場合は、アクセスが自動的に許可されます。  
  
 [ @rolename **=** ] **'**_ロール_**'**  
 ログインを追加する固定サーバー ロールの名前を指定します。 *ロール*は**sysname**、既定値は null の場合、値は次のいずれかを指定する必要があります。  
  
-   sysadmin  
  
-   securityadmin  
  
-   serveradmin  
  
-   setupadmin  
  
-   processadmin  
  
-   diskadmin  
  
-   dbcreator  
  
-   bulkadmin  

## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 ログインを固定サーバー ロールに追加すると、そのロールに関係付けられている権限がログインに与えられます。  
  
 Sa ログインのあること、およびパブリックのロールのメンバーシップを変更することはできません。  
  
 Sp_addrolemember を使用して、メンバー、固定データベース ロールまたはユーザー定義ロールを追加します。  
  
 ログインは、ユーザー定義のトランザクション内で実行できません。  
  
## <a name="permissions"></a>アクセス許可  
 新しいメンバーを追加するロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、Windows ログイン `Corporate\HelenS` を固定サーバー ロール `sysadmin` に追加します。  
  
```  
EXEC sp_addsrvrolemember 'Corporate\HelenS', 'sysadmin';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [セキュリティ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)  
  
  
