---
title: sys.dm_db_xtp_memory_consumers (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_memory_consumers
- dm_db_xtp_memory_consumers
- dm_db_xtp_memory_consumers_TSQL
- sys.dm_db_xtp_memory_consumers_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_memory_consumers dynamic management view
ms.assetid: f7ab2eaf-e627-464d-91fe-0e170b3f37bc
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 768fb39cdf26b01d55ffaf175ec07e181d265b52
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52522749"
---
# <a name="sysdmdbxtpmemoryconsumers-transact-sql"></a>sys.dm_db_xtp_memory_consumers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[hek_2](../../includes/hek-2-md.md)] データベース エンジンのデータベース レベルのメモリ コンシューマーを報告します。 ビューは、データベース エンジンで使用する各メモリ コンシューマーの行を返します。 この DMV を使用して、別の内部オブジェクトにメモリを分散する方法を参照してください。  
  
 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|memory_consumer_id|**bigint**|メモリ コンシューマーの ID (内部)。|  
|memory_consumer_type|**int**|メモリ コンシューマーの種類。<br /><br /> 0=集計  (複数のコンシューマーのメモリ使用量を集計します。 表示することはできません)<br /><br /> 2=VARHEAP (可変長ヒープのメモリ使用量を追跡します)<br /><br /> 3=HASH (インデックスのメモリ使用量を追跡します)<br /><br /> 5=DB ページ プール (実行時の操作に使用するデータベース ページ プールのメモリ使用量を追跡します。 たとえば、テーブル変数および一部のシリアル化可能なスキャンが対象になります。 この種類のメモリ コンシューマーは 1 つのデータベースに 1 つだけ存在します)|  
|memory_consumer_type_desc|**nvarchar(64)**|メモリ コンシューマーの種類:VARHEAP、HASH、または PGPOOL。<br /><br /> 0 - (これは表示されません)。<br /><br /> 2 - VARHEAP<br /><br /> 3 - HASH<br /><br /> 5 - PGPOOL|  
|memory_consumer_desc|**nvarchar(64)**|メモリ コンシューマー インスタンスの説明。<br /><br /> VARHEAP: <br />データベース ヒープ。 データベース (行) のユーザー データを割り当てるために使用します。<br />データベース システム ヒープ。 メモリ ダンプに含められ、ユーザー データを含まないデータベース データを割り当てるために使用します。<br />範囲インデックス ヒープ。 BW ページを割り当てるために範囲インデックスによって使用されるプライベート ヒープ。<br /><br /> ハッシュ:object_id はテーブルを示し、index_id はハッシュ インデックスそのものを示すため、説明はありません。<br /><br /> PGPOOL。データベース用のページ プールは Database 64K ページ プールのみです。|  
|object_id|**bigint**|割り当てられたメモリに関連するオブジェクト ID。 システム オブジェクトに対しては負の値になります。|  
|xtp_object_id|**bigint**|メモリ最適化テーブルのオブジェクトの ID。|  
|index_id|**int**|コンシューマーのインデックス ID (存在する場合)。 ベース テーブルに対しては NULL になります。|  
|allocated_bytes|**bigint**|このコンシューマーのために予約されたバイト数。|  
|used_bytes|**bigint**|このコンシューマーが使用したバイト数。 VARHEAP のみに適用されます。|  
|allocation_count|**int**|割り当ての数。|  
|partition_count|**int**|内部使用のみです。|  
|sizeclass_count|**int**|内部使用のみです。|  
|min_sizeclass|**int**|内部使用のみです。|  
|max_sizeclass|**int**|内部使用のみです。|  
|memory_consumer_address|**varbinary**|コンシューマーの内部アドレス。 内部使用のみです。|  
|xtp_object_id|**bigint**|メモリ最適化テーブルに対応する、インメモリ OLTP オブジェクトの ID。|  
  
## <a name="remarks"></a>コメント  
 出力では、データベース レベルのアロケーターは、ユーザー テーブル、インデックス、およびシステム テーブルを参照します。 object_id = NULL の VARHEAP は、可変長列を含むテーブルに割り当てられたメモリを参照します。  
  
## <a name="permissions"></a>アクセス許可  
 現在のデータベースに対して VIEW DATABASE STATE 権限を持っている場合は、すべての行が返されます。 この権限を持っていない場合は、空の行セットが返されます。  
  
 VIEW DATABASE 権限がない場合は、SELECT 権限を持っているテーブル内の行に対するすべての列が返されます。  
  
 システム テーブルは、VIEW DATABASE STATE 権限を持つユーザーにのみ返されます。  
  
## <a name="general-remarks"></a>全般的な解説  
 メモリ最適化テーブルに列ストア インデックスが設定されているとき、システムは、列ストア インデックスのデータを追跡するためにいくつかのメモリを消費するには、いくつかの内部テーブルを使用します。 これらの内部テーブルとそのメモリ消費量を示すサンプル クエリについての詳細を参照してください[sys.memory_optimized_tables_internal_attributes (TRANSACT-SQL)](../../relational-databases/system-catalog-views/sys-memory-optimized-tables-internal-attributes-transact-sql.md)します。
 
  
## <a name="examples"></a>使用例  
  
```  
-- memory consumers (database level)  
SELECT OBJECT_NAME(object_id), *   
FROM sys.dm_db_xtp_memory_consumers;  
```  
  
## <a name="user-scenario"></a>ユーザー シナリオ  
  
```  
-- memory consumers (database level)  
  
select  convert(char(10), object_name(object_id)) as Name,   
convert(char(10),memory_consumer_type_desc ) as memory_consumer_type_desc, object_id,index_id, allocated_bytes,  used_bytes   
from sys.dm_db_xtp_memory_consumers  
```  
  
 列の一部の出力例を次に示します。 データベース レベルのアロケーターは、ユーザー テーブル、インデックス、およびシステム テーブルを参照します。 object_id = NULL の VARHEAP (最終行) は、テーブルのデータ行に割り当てられたメモリ (この例では t1) を参照します。 割り当てられたバイト数は、MB 換算で 1340 MB です。  
  
```  
Name       memory_consumer_type_desc object_id   index_id    allocated_bytes      used_bytes  
---------- ------------------------- ----------- ----------- -------------------- --------------------  
t3         HASH                      629577281   2           8388608              8388608  
t2         HASH                      597577167   2           8388608              8388608  
t1         HASH                      565577053   2           1048576              1048576  
NULL       HASH                      -6          1           2048                 2048  
NULL       VARHEAP                   -6          NULL        0                    0  
NULL       HASH                      -5          3           8192                 8192  
NULL       HASH                      -5          2           8192                 8192  
NULL       HASH                      -5          1           8192                 8192  
NULL       HASH                      -4          1           2048                 2048  
NULL       VARHEAP                   -4          NULL        0                    0  
NULL       HASH                      -3          1           2048                 2048  
NULL       HASH                      -2          2           8192                 8192  
NULL       HASH                      -2          1           8192                 8192  
NULL       VARHEAP                   -2          NULL        196608               26496  
NULL       HASH                      0           1           2048                 2048  
NULL       PGPOOL                    0           NULL        0                    0  
NULL       VARHEAP                   NULL        NULL        1405943808           1231220560  
  
(17 row(s) affected)  
```  
  
 割り当てられているし、この DMV から使用されるメモリの合計がオブジェクト レベルと同じ[sys.dm_db_xtp_table_memory_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql.md)します。  
  
```  
select  sum(allocated_bytes)/(1024*1024) as total_allocated_MB,   
        sum(used_bytes)/(1024*1024) as total_used_MB  
from sys.dm_db_xtp_memory_consumers  
  
total_allocated_MB   total_used_MB  
-------------------- --------------------  
1358                 1191  
```  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルの動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
