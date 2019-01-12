---
title: sp_dbfixedrolepermission (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbfixedrolepermission
- sp_dbfixedrolepermission_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbfixedrolepermission
ms.assetid: b8c30191-f532-49cd-83f3-c271f63ce572
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7e7305e73d1f2f35d5cb4666e68114c9ee8f58e7
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2019
ms.locfileid: "54126212"
---
# <a name="spdbfixedrolepermission-transact-sql"></a>sp_dbfixedrolepermission (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  固定データベース ロールの権限を表示します。 **sp_dbfixedrolepermission**正しい情報が返されます[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]します。 ただし、この出力には、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] で実装された権限階層への変更は反映されません。 詳細については、次を参照してください。[権限&#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dbfixedrolepermission [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>引数  
 [  **@rolename =** ] **'**_ロール_**'**  
 有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定データベール ロールの名前を指定します。 *ロール*は**sysname**、既定値は NULL です。 場合*ロール*が指定されていない、すべての固定データベース ロールのアクセス許可が表示されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**DbFixedRole**|**sysname**|固定データベース ロールの名前。|  
|**権限**|**nvarchar (70)**|アクセス許可に関連付けられている**DbFixedRole**|  
  
## <a name="remarks"></a>コメント  
 固定データベース ロールの一覧を表示するには、実行**sp_helpdbfixedrole**します。 次の表は、固定データベース ロールを示しています。  
  
|固定データベース ロール|説明|  
|-------------------------|-----------------|  
|**db_owner**|データベース所有者|  
|**db_accessadmin**|データベース アクセス管理者|  
|**db_securityadmin**|データベース セキュリティ管理者|  
|**db_ddladmin**|データベース データ定義言語 (DDL) 管理者|  
|**db_backupoperator**|データベース バックアップ オペレーター|  
|**db_datareader**|データベース データ リーダー|  
|**db_datawriter**|データベース データ ライター|  
|**db_denydatareader**|データベース否定データ リーダー|  
|**db_denydatawriter**|データベース否定データ ライター|  
  
 メンバー、 **db_owner**固定データベース ロールには、その他のすべての固定データベース ロールの権限します。 固定サーバー ロールのアクセス許可を表示するには、実行**sp_srvrolepermission**します。  
  
 結果セットには、データベース ロールのメンバーが実行できる、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントとその他の特別な操作が含まれます。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次のクエリでは、固定データベース ロールを指定せず、すべての固定データベース ロールに対する権限を返します。  
  
```  
EXEC sp_dbfixedrolepermission;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprolemember の各&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helpdbfixedrole &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql.md)   
 [sp_srvrolepermission &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
