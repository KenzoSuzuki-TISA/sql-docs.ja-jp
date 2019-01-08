---
title: MSmerge_contents (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_contents
- MSmerge_contents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_contents system table
ms.assetid: 8d68a61a-683f-4b20-92f9-c0a8d9ba0ad1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e5aa95edeb1a947aea517de30efcbbbc3c6c799c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52750384"
---
# <a name="msmergecontents-transact-sql"></a>MSmerge_contents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_contents**テーブルには、発行された後に、現在のデータベースで変更された行ごとに 1 行が含まれています。 このテーブルは、マージ プロセスが、変更された行を判断するために使用します。 このテーブルは、パブリケーション データベースとサブスクリプション データベースに保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|パブリッシュされたテーブルのニックネーム。|  
|**rowguid**|**uniqueidentifier**|指定した行の行識別子 (ROWID)。|  
|**生成**|**bigint**|識別される行の生成、 **tablenick**と**rowguid**します。|  
|**partchangegen**|**bigint**|最新のデータ変更に関連する generation 値です。フィルター選択されたパブリケーションに行が含まれているかどうかを変更します。|  
|**系列**|**varbinary(501)**|この行に加えられた変更の履歴を管理するために使用するサブスクライバーのニックネームとバージョン番号のペアです。|  
|**colvl**|**varbinary(7489)**|列バージョン情報です。|  
|**マーカー**|**uniqueidentifier**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**logical_record_parent_rowguid**|**uniqueidentifier**|最上位レベル親行を識別**MSmerge_contents** (によって**rowguid**) 論理レコードの対応する子行はごとです。|  
|**logical_record_lineage**|**varbinary(501)**|論理レコードの最上位レベルの親行に加えられた変更の履歴を管理するために使用するサブスクライバーのニックネームとバージョン番号のペアです。 論理レコードのすべての子行に対しては、この値は NULL です。|  
|**logical_relation_change_gen**|**bigint**|変更によって論理レコードの再配置が生じ、既存の行が論理レコード内外に移動した場合、その前回の変更に関連付けられた generation 値です。|  
  
## <a name="see-also"></a>参照  
 [レプリケーション テーブル &#40; です。TRANSACT-SQL と &#41; です。](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
