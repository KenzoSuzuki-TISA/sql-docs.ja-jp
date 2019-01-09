---
title: sys.dm_exec_query_profiles (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_profiles_TSQL
- sys.dm_exec_query_profiles_TSQL
- dm_exec_query_profiles
- sys.dm_exec_query_profiles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_profiles dynamic management view
ms.assetid: 54efc6cb-eea8-4f6d-a4d0-aa05eeb54081
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1fb79f056e533f4aabacdab5e3467bedce22b696
ms.sourcegitcommit: e0178cb14954c45575a0bab73dcc7547014d03b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2018
ms.locfileid: "52860095"
---
# <a name="sysdmexecqueryprofiles-transact-sql"></a>sys.dm_exec_query_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  クエリの実行中にリアルタイムでクエリの進行状況を監視します。 たとえば、この DMV を使用して、クエリで実行が遅い部分を判別します。 この DMV をシステムの他の DMV と結合するには、説明フィールドで特定されている列を使用します。 または、この DMV を他のパフォーマンス カウンター (パフォーマンス モニター、xperf など) と結合するには、タイムスタンプ列を使用します。  
  
## <a name="table-returned"></a>返されるテーブル  
 返されるカウンターは、演算子別、スレッド別です。 結果は動的であり、クエリの終了時にのみ出力を作成する SET STATISTICS XML ON などの既存のオプションの結果とは一致しません。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|このクエリが実行されるセッションを識別します。 dm_exec_sessions.session_id を参照します。|  
|request_id|**int**|対象の要求を識別します。 dm_exec_sessions.request_id を参照します。|  
|sql_handle|**varbinary(64)**|対象のクエリを識別します。 dm_exec_query_stats.sql_handle を参照します。|  
|plan_handle|**varbinary(64)**|対象のクエリを識別します。dm_exec_query_stats.plan_handle を参照します。|  
|physical_operator_name|**nvarchar (256)**|物理演算子の名前。|  
|node_id|**int**|クエリ ツリー内の演算子ノードを識別します。|  
|thread_id|**int**|同じクエリ演算子ノードに属するスレッド (並列クエリ用) を区別します。|  
|task_address|**varbinary(8)**|このスレッドが使用している SQLOS タスクを識別します。 dm_os_tasks.task_address を参照します。|  
|row_count|**bigint**|これまでに演算子によって返された行の数。|  
|rewind_count|**bigint**|これまでの巻き戻しの数。|  
|rebind_count|**bigint**|これまでの再バインドの数。|  
|end_of_scan_count|**bigint**|これまでのスキャンの終了の数。|  
|estimate_row_count|**bigint**|推定される行の数。 estimated_row_count を実際の row_count と比較することが役立つ場合があります。|  
|first_active_time|**bigint**|演算子が初めて呼び出された時刻 (ミリ秒単位)。|  
|last_active_time|**bigint**|演算子が最後に呼び出された時刻 (ミリ秒単位)。|  
|open_time|**bigint**|開いたときのタイムスタンプ (ミリ秒単位)。|  
|first_row_time|**bigint**|最初の行を開いたときのタイムスタンプ (ミリ秒単位)。|  
|last_row_time|**bigint**|最後の行を開いたときのタイムスタンプ (ミリ秒単位)。|  
|close_time|**bigint**|閉じたときのタイムスタンプ (ミリ秒単位)。|  
|elapsed_time_ms|**bigint**|経過時間の合計 (ミリ秒) をターゲット ノードの操作によってこれまでに使用します。|  
|cpu_time_ms|**bigint**|これまでにターゲット ノードの操作によって CPU 使用率 (ミリ秒単位) の時間の合計数します。|  
|database_id|**smallint**|読み取りおよび書き込みが実行されたオブジェクトを含むデータベースの ID。|  
|object_id|**int**|読み取りおよび書き込みが実行されたオブジェクトの識別子。 sys.objects.object_id を参照します。|  
|index_id|**int**|行セットが開かれている対象のインデックス (ある場合)。|  
|scan_count|**bigint**|これまでのテーブル/インデックス スキャンの数。|  
|logical_read_count|**bigint**|これまでの論理読み取りの数。|  
|physical_read_count|**bigint**|これまでの物理読み取りの数。|  
|read_ahead_count|**bigint**|これまでの先行読み取りの数。|  
|write_page_count|**bigint**|これまでのスピルによるページ書き込みの数。|  
|lob_logical_read_count|**bigint**|これまでの LOB 論理読み取りの数。|  
|lob_physical_read_count|**bigint**|これまでの LOB 物理読み取りの数。|  
|lob_read_ahead_count|**bigint**|これまでの LOB 先行読み取りの数。|  
|segment_read_count|**int**|これまでのセグメント先行読み取りの数。|  
|segment_skip_count|**int**|これまでのセグメント スキップの数。| 
|actual_read_row_count|**bigint**|残余述語が適用される前に、演算子によって読み取られた行の数。| 
|estimated_read_row_count|**bigint**|**適用対象:** 以降で[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]SP1。 <br/>残余述語が適用される前に、演算子によって読み取られる行の数が推定されます。|  
  
## <a name="general-remarks"></a>全般的な解説  
 クエリ プラン ノードで IO がない場合、IO 関連のすべてのカウンターは NULL に設定されます。  
  
 この DMV でレポートされる IO 関連のカウンターは、次の 2 つの点で、SET STATISTICS IO でレポートされるものよりも詳細です。  
  
-   SET STATISTICS IO では、特定のテーブルに対するすべての IO のカウンターはグループ化されます。 この DMV では、テーブルに対する IO を実行するクエリ プランのそれぞれのノードについて、個別のカウンターを取得します。  
  
-   並列スキャンがある場合、この DMV では、スキャンで使用される並列スレッドごとにカウンターがレポートされます。
 
以降で[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 では、標準的なクエリの実行統計プロファイリング インフラストラクチャでは、軽量なクエリの実行統計プロファイリング インフラストラクチャのサイド バイ サイドでが存在します。 新しいクエリ実行統計プロファイリング インフラストラクチャは、行の実際の数などの演算子ごとのクエリ実行統計を収集する場合のパフォーマンスのオーバーヘッドを大幅に削減します。 グローバルを使用してこの機能を有効にすることができますスタートアップ[トレース フラグ 7412](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)が自動的にオン query_thread_profile 拡張イベントを使用する場合またはします。

>[!NOTE]
> CPU と経過時間は、パフォーマンスに与える影響を軽減する軽量なクエリの実行統計プロファイリング インフラストラクチャでサポートされていません。

XML ON および SET STATISTICS PROFILE ON の従来のクエリの実行統計プロファイリング インフラストラクチャを使用して、常に統計情報を設定します。

有効にするには、sys.dm_exec_query_profiles の出力は次の操作を行います。

[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 および後で調査中のクエリと共に SET STATISTICS PROFILE ON または SET STATISTICS XML ON を使用します。 これは、プロファイリング インフラストラクチャを使用し、SET コマンドが実行されたセッションの DMV の結果を生成します。 アプリケーションから実行されているクエリを調査するいるし、してオプションの設定を有効にすることはできません、プロファイリングのインフラストラクチャが有効になります、query_post_execution_showplan イベントを使用して拡張イベントを作成できます。 

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 かオンにする[トレース フラグ 7412](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)または query_thread_profile 拡張イベントを使用します。

>[!NOTE]
> 調査中のクエリは、プロファイリング インフラストラクチャを有効になっている後に起動するがあります。 クエリが既に実行されている場合、拡張イベント セッションの開始と sys.dm_exec_query_profiles で結果が生成されません。


## <a name="permissions"></a>アクセス許可  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]が必要です、`VIEW DATABASE STATE`データベースの権限。   
   
## <a name="examples"></a>使用例  
 手順 1:sys.dm_exec_query_profiles を使用して分析するクエリを実行するセッションにログインします。 構成するには、プロファイルのクエリで SET STATISTICS PROFILE を使用します。 この同じセッションでクエリを実行します。  
  
```  
--Configure query for profiling with sys.dm_exec_query_profiles  
SET STATISTICS PROFILE ON;  
GO  

--Or enable query profiling globally under SQL Server 2016 SP1 or above  
DBCC TRACEON (7412, -1);  
GO 
  
--Next, run your query in this session, or in any other session if query profiling has been enabled globally 
```  
  
 手順 2:クエリが実行されているセッションとは異なる 2 番目のセッションにログインします。  
  
 次のステートメントでは、セッション 54 で現在実行されているクエリの進行状況が要約されます。 これを実行するために、各ノードのすべてのスレッドからの出力行の総数が計算され、そのノードの出力行の予測数と比較されます。  
  
```  
--Run this in a different session than the session in which your query is running. 
--Note that you may need to change session id 54 below with the session id you want to monitor.
SELECT node_id,physical_operator_name, SUM(row_count) row_count, 
  SUM(estimate_row_count) AS estimate_row_count, 
  CAST(SUM(row_count)*100 AS float)/SUM(estimate_row_count)  
FROM sys.dm_exec_query_profiles   
WHERE session_id=54
GROUP BY node_id,physical_operator_name  
ORDER BY node_id;  
```  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [実行関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

