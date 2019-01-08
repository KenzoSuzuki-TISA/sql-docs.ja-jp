---
title: sp_repldone (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repldone
- sp_repldone_TSQL
helpviewer_keywords:
- sp_repldone
ms.assetid: 045d3cd1-712b-44b7-a56a-c9438d4077b9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aaeebd1aa2d6fe4ea443c7ed18ac157135ae4d64
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52747751"
---
# <a name="sprepldone-transact-sql"></a>sp_repldone (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  サーバーで最後にディストリビュートされたトランザクションを識別するレコードを更新します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
> [!CAUTION]  
>  実行する場合**sp_repldone**順序や配信されたトランザクションの一貫性を無効にできる、手動でします。 **sp_repldone**サポート プロフェッショナルの経験豊富なレプリケーションのレプリケーションのトラブルシューティングにのみ使用する必要があります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_repldone [ @xactid= ] xactid   
        , [ @xact_seqno= ] xact_seqno   
    [ , [ @numtrans= ] numtrans ]   
    [ , [ @time= ] time   
    [ , [ @reset= ] reset ]  
```  
  
## <a name="arguments"></a>引数  
 [  **@xactid=**] *xactid*  
 最後に、サーバーの分散トランザクションの最初のレコードのログ シーケンス番号 (LSN) は、します。 *xactid*は**binary (10)**、既定値はありません。  
  
 [  **@xact_seqno=**] *xact_seqno*  
 最後に、サーバーの分散トランザクションの最後のレコードの LSN です。 *xact_seqno*は**binary (10)**、既定値はありません。  
  
 [  **@numtrans=**] *numtrans*  
 分散トランザクションの数です。 *numtrans*は**int**、既定値はありません。  
  
 [  **@time=**]*時間*  
 最後のトランザクション バッチをディストリビュートするのに必要な時間をミリ秒単位の数で指定できます。 *時間*は**int**、既定値はありません。  
  
 [  **@reset=**]*リセット*  
 リセットの状態を指定します。 *リセット*は**int**、既定値はありません。 場合**1**、レプリケートされたすべてのログ内のトランザクションがマークされているディストリビュート済み。 場合**0**、トランザクション ログは、最初のレプリケートされたトランザクションにリセットし、レプリケートされたトランザクションがマークされていないと分散します。 *リセット*場合のみ有効ですが両方*xactid*と*xact_seqno*は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_repldone**はトランザクション レプリケーションで使用します。  
  
 **sp_repldone**ログ読み取りプロセスで配布されたトランザクションを追跡するために使用します。  
  
 **Sp_repldone**、手動でわかりますサーバー (ディストリビューターに送られます)、トランザクションがレプリケートされることです。 また、レプリケーション待ちの次のトランザクションであることを示すマークが付いたトランザクションを変更できます。 レプリケートされたトランザクションの一覧内では、前後に移動できます。 このトランザクションおよびそれ以前のトランザクションはすべてディストリビュートされたことを示すマークが付きます。  
  
 必要なパラメーター *xactid*と*xact_seqno*を使用して取得できる**sp_repltrans**または**sp_replcmds**します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバー、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_repldone**します。  
  
## <a name="examples"></a>使用例  
 ときに*xactid*が null の場合、 *xact_seqno*が null の場合、および*リセット*は**1**、レプリケートされたすべて、ログ内のトランザクションがマークされているディストリビュート済み。 たとえば次のように、トランザクション ログ内のレプリケートされたトランザクションで無効になったものがあり、ログを切り詰めたい場合に便利です。  
  
```  
EXEC sp_repldone @xactid = NULL, @xact_segno = NULL, @numtrans = 0,     @time = 0, @reset = 1  
```  
  
> [!CAUTION]  
>  このプロシージャは、レプリケーションが保留されているトランザクションがあるときにトランザクション ログの切り詰めを可能にする必要がある場合など、緊急時に使用できます。  
  
## <a name="see-also"></a>参照  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replflush &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
