---
title: sp_expired_subscription_cleanup (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_expired_subscription_cleanup
- SP_EXPIRED_SUBSCRIPTION_CLEANUP_TSQL
helpviewer_keywords:
- sp_expired_subscription_cleanup
ms.assetid: 6abc29fe-d77a-4673-9d99-ae31c688012c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 24aa8a9018a2de742a8ed4715b87e56126326021
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2019
ms.locfileid: "54130892"
---
# <a name="spexpiredsubscriptioncleanup-transact-sql"></a>sp_expired_subscription_cleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  各パブリケーションのすべてのサブスクリプションの状態を確認して、期限切れになったものを削除します。 任意のデータベース、パブリッシャーまたはディストリビューターの以外のディストリビューション データベースでこのストアド プロシージャが実行される[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーです。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_expired_subscription_cleanup [ [ @publisher = ] 'publisher' ]   
```  
  
## <a name="arguments"></a>引数  
 [  **@publisher=** ] **'**_パブリッシャー_**'**  
 以外の名前を指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーです。 *パブリケーション*は**sysname**既定値は NULL です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パブリッシャーの場合はこのパラメーターを指定しないでください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_expired_subscription_cleanup**はあらゆる種類のレプリケーションで使用します。  
  
 **sp_expired_subscription_cleanup**を検出し、パブリケーション データベースから 24 時間ごとに有効期限が切れたサブスクリプションが削除、有効期限切れサブスクリプション クリーンアップのジョブによって実行されます。 保有期間内にパブリッシャーと同期されなかった古いサブスクリプションが含まれている場合、パブリケーションは期限切れとして宣言され、サブスクリプションのトレースがパブリッシャーでクリーンアップされます。 詳細については、「 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_expired_subscription_cleanup**します。  
  
## <a name="see-also"></a>参照  
 [sp_mergesubscription_cleanup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md)   
 [sp_subscription_cleanup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
