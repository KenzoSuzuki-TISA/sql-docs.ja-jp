---
title: MSsnapshot_history (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsnapshot_history
- MSsnapshot_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshot_history system table
ms.assetid: 56bf4128-1689-4963-9343-432dd0898d31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ca24fdce036c4f63e49e7d0eb12054d2d67aa6aa
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52800724"
---
# <a name="mssnapshothistory-transact-sql"></a>MSsnapshot_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsnapshot_history**テーブルは、ローカル ディストリビューターに関連付けられているスナップショット エージェントの履歴行を保持します。 このテーブルは、ディストリビューション データベースに保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|スナップショット エージェントの ID。|  
|**runstatus**|**int**|実行ステータスです。<br /><br /> **1** = 開始します。<br /><br /> **2** = 成功します。<br /><br /> **3** = 実行中です。<br /><br /> **4** = アイドル状態です。<br /><br /> **5** = 再試行します。<br /><br /> **6** = 失敗します。|  
|**start_time**|**datetime**|ジョブの実行開始時刻です。|  
|**time**|**datetime**|メッセージが記録された時刻です。|  
|**duration**|**int**|メッセージ セッションの実行時間 (秒) です。|  
|**comments**|**nvarchar (255)**|メッセージ テキストです。|  
|**delivered_transactions**|**int**|セッション中に配信されたトランザクションの総数です。|  
|**delivered_commands**|**int**|1 秒あたりの配信コマンド数です。|  
|**delivery_rate**|**float(53)**|1 秒あたりの平均配信コマンド数です。|  
|**error_id**|**int**|内のエラーの ID、 [MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md)システム テーブル。|  
|**timestamp**|**timestamp**|このテーブルのタイムスタンプ列です。|  
  
## <a name="see-also"></a>参照  
 [レプリケーション テーブル &#40; です。TRANSACT-SQL と &#41; です。](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
