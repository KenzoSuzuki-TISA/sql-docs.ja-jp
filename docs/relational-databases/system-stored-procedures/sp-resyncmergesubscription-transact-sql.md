---
title: sp_resyncmergesubscription (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_resyncmergesubscription_TSQL
- sp_resyncmergesubscription
helpviewer_keywords:
- sp_resyncmergesubscription
ms.assetid: e04d464a-60ab-4b39-a710-c066025708e6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 087bb377be29db42f4e58ede6cfb0a823459501b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52747554"
---
# <a name="spresyncmergesubscription-transact-sql"></a>sp_resyncmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  マージ サブスクリプションを、指定の有効な状態に再同期します。 これによって、サブスクリプション データベースを、正常終了した前回の検証時や指定の日時など、特定の時点に強制的に集約または同期できます。 この方法でサブスクリプションを再同期する場合、スナップショットは再適用されません。 このストアド プロシージャは、スナップショット レプリケーション サブスクリプションまたはトランザクション レプリケーション サブスクリプションでは使用しません。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されるか、サブスクライバー側でサブスクリプション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_resyncmergesubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
        , [ @publication = ] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @resync_type = ] resync_type ]  
    [ , [ @resync_date_str = ] resync_date_string ]  
```  
  
## <a name="arguments"></a>引数  
 [ **@publisher** =] **'***パブリッシャー***'**  
 パブリッシャーの名前です。 *パブリッシャー*は**sysname**、既定値は NULL です。 ストアド プロシージャをパブリッシャー側で実行する場合は、NULL の値が有効です。 ストアド プロシージャをサブスクライバー側で実行する場合は、パブリッシャーを指定する必要があります。  
  
 [ **@publisher_db** =] **'***publisher_db***'**  
 パブリケーション データベースの名前です。 *publisher_db*は**sysname**、既定値は NULL です。 ストアド プロシージャをパブリケーション データベースのパブリッシャー側で実行する場合は、NULL の値が有効です。 ストアド プロシージャをサブスクライバー側で実行する場合は、パブリッシャーを指定する必要があります。  
  
 [ **@publication** =] **'***パブリケーション***'**  
 パブリケーションの名前です。 *パブリケーション*は**sysname**、既定値はありません。  
  
 [ **@subscriber** =] **'***サブスクライバー***'**  
 サブスクライバーの名前です。 *サブスクライバー*は**sysname**、既定値は NULL です。 ストアド プロシージャをサブスクライバー側で実行する場合は、NULL の値が有効です。 ストアド プロシージャをパブリッシャー側で実行する場合は、サブスクライバーを指定する必要があります。  
  
 [ **@subscriber_db** =] **'***@subscriber_db***'**  
 サブスクリプション データベースの名前です。 *subscription_db*は**sysname**、既定値は NULL です。 ストアド プロシージャをサブスクリプション データベースのサブスクライバー側で実行する場合は、NULL の値が有効です。 ストアド プロシージャをパブリッシャー側で実行する場合は、サブスクライバーを指定する必要があります。  
  
 [ **@resync_type** =] *resync_type*  
 再同期の開始時期を定義します。 *resync_type*は**int**値は次のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**0**|初期スナップショットの後から同期を開始。 このオプションでは、初期スナップショット以降のすべての変更がサブスクライバーに再適用されるので、最もリソースが使用されます。|  
|**1**|正常終了した前回の検証以降の同期を開始。 正常終了した前回の検証以降の、すべての新しい生成結果または完了していない生成結果がサブスクライバーに再適用されます。|  
|**2**|指定した日付から同期を開始*resync_date_str*します。 指定の日付以降の、すべての新しい生成結果または完了していない生成結果がサブスクライバーに再適用されます。|  
  
 [ **@resync_date_str=**] *resync_date_string*  
 再同期を開始する日付を定義します。 *resync_date_string*は**nvarchar (30)**、既定値は NULL です。 このパラメーターが使用されるときに、 *resync_type*の値は、 **2**します。 指定した日付は、それと同等に変換されます**datetime**値。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_resyncmergesubscription**はマージ レプリケーションで使用します。  
  
 値**0**の*resync_type*リソースを消費可能性がある多くよりも小さい、全体を再初期化を初期スナップショット以降のすべての変更を再適用、パラメーターとして使用することがあります。 たとえば、初期スナップショットが 1 か月前に配信された場合は、過去 1 か月分のデータが再適用されます。 初期スナップショットに 1 GB のデータが含まれていた場合、過去 1 か月のデータ変更量が 2 MB であれば、1 GB のスナップショット全体を再適用するよりは変更データを再適用する方が効率的です。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_resyncmergesubscription**します。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
