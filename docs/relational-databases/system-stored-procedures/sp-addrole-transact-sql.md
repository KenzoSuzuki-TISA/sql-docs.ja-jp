---
title: sp_addrole (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addrole
- sp_addrole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addrole
ms.assetid: e8a21642-8440-419a-8585-93d3d9d44f00
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: f51d462e46a86a3c824a7e37aeb1f30ba28d987b
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2018
ms.locfileid: "53212921"
---
# <a name="spaddrole-transact-sql"></a>sp_addrole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のデータベースに新しいデータベース ロールを作成します。  
  
> [!IMPORTANT]
>  **sp_addrole**が以前のバージョンの互換性のために含まれる[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将来のリリースではサポートされない可能性があります。 使用[CREATE ROLE](../../t-sql/statements/create-role-transact-sql.md)代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addrole [ @rolename = ] 'role' [ , [ @ownername = ] 'owner' ]   
```  
  
## <a name="arguments"></a>引数  
 [  **@rolename =** ] **'***ロール***'**  
 新しいデータベース ロールの名前を指定します。 *ロール*は、 **sysname**、既定値はありません。 *ロール*有効な識別子 (ID) である必要があり、現在のデータベースに既に存在する必要があります。  
  
 [  **@ownername =**] **'***所有者***'**  
 新しいデータベース ロールの所有者を指定します。 *所有者*は、 **sysname**、現在実行しているユーザーの既定値。 *所有者*データベース ユーザーまたはデータベース ロール、現在のデータベースである必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ロールは 1 ～ 128 文字で指定でき、英数字と記号を含めることができます。 データベース ロールの名前のことはできません。 円記号を含める (\\)、null 値、または空の文字列 (**''**)。  
  
 データベース ロールに追加した後を使用して、 [sp_addrolemember &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) 、ロールにプリンシパルを追加します。 GRANT、DENY、または REVOKE ステートメントを使用して権限をデータベース ロールに適用すると、そのデータベース ロールのメンバーには、それぞれのアカウントに直接適用した場合と同様に、権限が継承されます。  
  
> [!NOTE]  
>  新しいサーバー ロールを作成することはできません。 ロールは、データベース レベルでのみ作成できます。  
  
 **sp_addrole**ユーザー定義のトランザクション内で使用することはできません。  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する CREATE ROLE 権限が必要です。 スキーマを作成する場合は、データベースに対する CREATE SCHEMA 権限が必要です。 場合*所有者*ユーザーまたはグループとして指定すると、そのユーザーまたはグループに対する impersonate 権限が必要です。 場合*所有者*ロールとして指定すると、そのロールまたはそのロールのメンバーに対する ALTER 権限が必要です。 所有者をアプリケーション ロールとして指定する場合は、そのアプリケーション ロールに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、`Managers` という新しいロールを現在のデータベースに追加します。  
  
```  
EXEC sp_addrole 'Managers';  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)  
  
  
