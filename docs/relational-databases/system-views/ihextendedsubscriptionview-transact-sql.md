---
title: IHextendedSubscriptionView (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHextendedSubscriptionView_TSQL
- IHextendedSubscriptionView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedSubscriptionView view
ms.assetid: 124756a4-463a-4a81-bf5b-de7e8ffc7a62
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30ba4a0947f98ab34ed8c11ef0e8f3a25c3e453b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756984"
---
# <a name="ihextendedsubscriptionview-transact-sql"></a>IHextendedSubscriptionView (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHextendedSubscriptionView**ビューは、SQL Server 以外のパブリケーションに対するサブスクリプションに関する情報を公開します。 このビューは、**配布**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|アーティクルの一意識別子。|  
|**dest_db**|**sysname**|転送先データベースの名前。|  
|**srvid**|**smallint**|サブスクライバーの一意識別子。|  
|**login_name**|**sysname**|サブスクライバーに接続するときに使用するログイン名。|  
|**distribution_jobid**|**[バイナリ]**|ディストリビューション エージェント ジョブを識別します。|  
|**publisher_database_id**|**int**|パブリケーション データベースの識別子。|  
|**subscription_type**|**int**|サブスクリプションの種類です。<br /><br /> **0** = プッシュ、ディストリビューション エージェントがサブスクライバーで実行されます。<br /><br /> **1** = プル、ディストリビューション エージェントがディストリビューターで実行されます。|  
|**sync_type**|**tinyint**|初期同期の種類。<br /><br /> **1** = 自動<br /><br /> **2** = なし|  
|**status**|**tinyint**|サブスクリプションの状態:<br /><br /> **0** = 非アクティブ<br /><br /> **1** = サブスクライブ<br /><br /> **2** = アクティブ|  
|**snapshot_seqno_flag**|**bit**|スナップショット シーケンス番号が使用されているかどうかを示します。|  
|**independent_agent**|**bit**|このパブリケーションに対して、スタンドアロンのディストリビューション エージェントがあるかどうかを示します。<br /><br /> **0** = パブリケーションは共有ディストリビューション エージェントを使用して、パブリッシャー データベース/サブスクライバー データベースの各ペアが 1 つの共有エージェント。<br /><br /> **1** = このパブリケーション用のスタンドアロン ディストリビューション エージェントが存在します。|  
|**subscription_time**|**datetime**|内部使用のみです。|  
|**loopback_detection**|**bit**|双方向トランザクション レプリケーション トポロジの一部であるサブスクリプションに適用されます。 ディストリビューション エージェントが、サブスクライバーで発生したトランザクションをサブスクライバーに戻すかどうかを示します。<br /><br /> **1** = は送信しません。<br /><br /> **0** = 戻す。|  
|**agent_id**|**int**|ディストリビューション エージェントの一意識別子。|  
|**update_mode**|**tinyint**|更新モードの種類を示します。次のいずれかの値になります。<br /><br /> **0** = 読み取り専用です。<br /><br /> **1** = 即時更新します。<br /><br /> **2** = メッセージ キューを使用するキュー更新。<br /><br /> **3**イミディ エイト = メッセージ キューを使用してフェールオーバーとしてキュー更新で更新します。<br /><br /> **4** = SQL Server キューを使用するキュー更新。<br /><br /> **5** = SQL Server キューを使用して、キュー更新フェールオーバーを行う即時更新します。|  
|**publisher_seqno**|**varbinary(16)**|このサブスクリプションに対するパブリッシャー側のトランザクションのシーケンス番号。|  
|**ss_cplt_seqno**|**varbinary(16)**|同時実行スナップショット処理の完了を示すために使用するシーケンス番号。|  
  
## <a name="see-also"></a>参照  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーション テーブル &#40; です。TRANSACT-SQL と &#41; です。](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
