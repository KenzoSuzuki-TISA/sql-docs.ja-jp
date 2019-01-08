---
title: sys.column_store_row_groups (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.column_store_row_groups_TSQL
- column_store_row_groups
- sys.column_store_row_groups
- column_store_row_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_row_groups catalog view
ms.assetid: 76e7fef2-d1a4-4272-a2bb-5f5dcd84aedc
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: fff57d41e522ae2e002809982bfeb084c28bbbba
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52531661"
---
# <a name="syscolumnstorerowgroups-transact-sql"></a>sys.column_store_row_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  セグメント単位でクラスター化列ストア インデックス情報を提供して、システム管理に関する管理者の決定を支援します。 **sys.column_store_row_groups** (削除済みとしてマークされているを含む) に物理的に格納されている行の合計数の列と列の削除済みとしてマークされている行の数。 使用**sys.column_store_row_groups**行を判断するグループが削除された行の割合が高いと、再構築する必要があります。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|このインデックスが定義されているテーブルの ID。|  
|**index_id**|**int**|この列ストア インデックスがあるテーブルのインデックスの ID。|  
|**partition_number**|**int**|行グループ row_group_id を保持するテーブル パーティションの ID。 この DMV を sys.partitions に結合するには、partition_number を使用できます。|  
|**row_group_id**|**int**|この行グループに関連付けられている行グループ番号。 この番号はパーティション内で一意です。<br /><br /> -1 = メモリ内のテーブルの末尾。|  
|**delta_store_hobt_id**|**bigint**|デルタ ストアで OPEN の行グループの hobt_id でします。<br /><br /> 行グループがデルタ ストア内にない場合は NULL です。<br /><br /> メモリ内のテーブルの末尾の場合は NULL です。|  
|**state**|**tinyint**|state_description に関連付けられている ID 番号。<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN <br /><br /> 2 = CLOSED <br /><br /> 3 = COMPRESSED <br /><br /> 4 = 廃棄 (TOMBSTONE)|  
|**state_description**|**nvarchar(60)**|行グループの永続的な状態の説明:<br /><br /> 非表示 - 非圧縮セグメント デルタ ストア内のデータからの構築プロセスでします。 非表示の圧縮されたセグメントが完了するまで、読み取りアクションでデルタ ストアが使用されます。 その後、新しいセグメントが表示されると、ソース デルタ ストアは削除されます。<br /><br /> 開く - 新しいレコードを受け入れる読み取り/書き込み行グループ。 OPEN の行グループは、行ストア形式のままであり、列ストア形式に圧縮されていません。<br /><br /> 終了 - いっぱいされましたが、組ムーバー プロセスによってまだ圧縮行グループ。<br /><br /> 圧縮 - いっぱいになり、圧縮行グループ。|  
|**total_rows**|**bigint**|行グループに物理的に格納されている行の合計。 削除された行がまだ格納されていることがあります。 1 つの行グループの最大行数は 1,048,576 (16 進数では FFFFF) です。|  
|**deleted_rows**|**bigint**|削除済みとしてマークされている行グループ内の行の合計。 これはデルタ行グループの場合は常に 0 です。|  
|**size_in_bytes**|**bigint**|この行グループ内にあるすべてのデータ (メタデータと共有辞書は除く) のサイズ (バイト単位)。デルタ行グループと列ストア行グループの両方が対象です。|  
  
## <a name="remarks"></a>コメント  
 クラスター化または非クラスター化列ストア インデックスがある各テーブルの列ストア行グループごとに 1 つの行を返します。  
  
 使用**sys.column_store_row_groups**行グループおよび行グループのサイズに含まれる行の数を決定します。  
  
 行グループ内の削除済みの行の数が合計行数に対して占める割合が高くなると、テーブルの効率が低下します。 テーブルのサイズが小さくなるよう列ストア インデックスを再構築して、テーブルを読み取るために必要なディスク I/O を削減します。 使用して列ストア インデックスを再構築する、**リビルド**のオプション、 **ALTER INDEX**ステートメント。  
  
 更新可能な列ストアが最初に新しいデータを挿入、**オープン**行グループは行ストア形式であり、デルタ テーブルと呼ばれるをこともできます。  Open の行グループがいっぱいの状態に変わります**CLOSED**します。 Closed 行グループが、組ムーバーによって列ストア形式に圧縮され、状態が**圧縮**します。  組ムーバーは、定期的に起動され、列ストア行グループに圧縮する準備ができている CLOSED 状態の行グループがあるかどうかを確認するバックグラウンド プロセスです。  また、組ムーバーは、すべての行が削除された行グループの割り当てを解除します。 行グループの割り当て解除のマーク**廃棄 (tombstone)** します。 組ムーバーを直ちに実行するを使用して、 **REORGANIZE**のオプション、 **ALTER INDEX**ステートメント。  
  
 列ストア行グループは、いっぱいになると圧縮され、新しい行の受け入れを停止します。 圧縮されたグループから行が削除されると、削除された行は、保持されますが、削除済みとしてマークされます。 圧縮されたグループに対する更新は、圧縮されたグループからの削除、および OPEN 状態のグループへの挿入として実装されます。  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーがある場合、テーブルの情報を返します**VIEW DEFINITION**テーブルに対する権限。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例の結合、 **sys.column_store_row_groups**特定のテーブルに関する情報を返すには、その他のシステム テーブル。 計算済みの `PercentFull` 列は、行グループの効率の推定値を示します。 コメントのハイフンの前後に 1 つのテーブルの削除に関する情報、**場所**句とテーブル名を指定します。  
  
```  
SELECT i.object_id, object_name(i.object_id) AS TableName,   
i.name AS IndexName, i.index_id, i.type_desc,   
CSRowGroups.*,   
100*(total_rows - ISNULL(deleted_rows,0))/total_rows AS PercentFull    
FROM sys.indexes AS i  
JOIN sys.column_store_row_groups AS CSRowGroups  
    ON i.object_id = CSRowGroups.object_id  
AND i.index_id = CSRowGroups.index_id   
--WHERE object_name(i.object_id) = '<table_name>'   
ORDER BY object_name(i.object_id), i.name, row_group_id;  
```  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server のシステム カタログよく寄せられる質問のクエリを実行します。](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [列ストア インデックス ガイド](~/relational-databases/indexes/columnstore-indexes-overview.md)     
 [sys.column_store_dictionaries &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
  

