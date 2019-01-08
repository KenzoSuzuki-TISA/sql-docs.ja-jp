---
title: MSpeer_conflictdetectionconfigresponse (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_conflictdetectionconfigresponse
- MSpeer_conflictdetectionconfigresponse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigureresponse
ms.assetid: 2685fb66-731d-40f7-af4b-596b9222c5d4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e0b4ffd576c9be5f219a1f7d792aa04f00ed1b6c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52757874"
---
# <a name="mspeerconflictdetectionconfigresponse-transact-sql"></a>MSpeer_conflictdetectionconfigresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  トポロジ全体の構成要求に対する各ノードの応答を保存するために、ピア ツー ピア レプリケーションで使用されます。 このテーブルは、パブリケーション データベース内に保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|request_id|**int**|競合構成要求エントリを識別、 [MSpeer_conflictdetectionconfigrequest](../../relational-databases/system-tables/mspeer-conflictdetectionconfigrequest-transact-sql.md)テーブル。|  
|peer_node|**sysname**|応答を生成したサーバー インスタンスの名前です。|  
|peer_db|**sysname**|応答を生成したピア側のサブスクリプション データベースです。|  
|peer_version|**sysname**|パブリッシャーのバージョン番号を識別します。|  
|peer_db_version|**sysname**|ピア データベースのバージョン番号を識別します。|  
|is_peer|**bit**|ノードが読み取り専用サブスクライバーかどうかを示します。 値**0**読み取り専用サブスクライバーが示されます。|  
|conflict_detection_enabled|**bit**|トポロジで競合検出を有効にするかどうかを指定します。|  
|originator_id|**varbinary(16)**|競合検出のためにトポロジの各ノードを識別します。 詳細については、「 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)」を参照してください。|  
|peer_conflict_retention|**int**|メタデータが競合テーブルに保存される期間 (日数) です。|  
|peer_subscriptions|**XML**|要求に応答したノードに関する情報です。|  
|progress_phase|**nvarchar(32)**|処理の現在のフェーズを識別します。有効値は次のとおりです。<br /><br /> Started<br /><br /> 収集されたピア バージョン<br /><br /> 収集された状態|  
|modified_date|**datetime**|フェーズが完了した日時です。|  
  
## <a name="see-also"></a>参照  
 [レプリケーション テーブル &#40; です。TRANSACT-SQL と &#41; です。](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
