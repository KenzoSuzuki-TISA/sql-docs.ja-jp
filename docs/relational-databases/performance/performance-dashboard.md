---
title: パフォーマンス ダッシュボード | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- performance dashboard [SQL Server]
- performance dashboard reports
- perf dashboard
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753e
author: pelopes
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 99ff37b3c974f6ba63515b3b51e87719a1912521
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2019
ms.locfileid: "54242399"
---
# <a name="performance-dashboard"></a>パフォーマンス ダッシュボード
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] バージョン 17.2 以降には、パフォーマンス ダッシュボードが含まれています。 このダッシュボードは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 以降) のパフォーマンスの状態に対する分析情報を迅速かつ視覚的に提供できるように設計されています。 

パフォーマンス ダッシュボードは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にパフォーマンスのボトルネックが存在するかどうかを迅速に特定するのに役立ちます。 ボトルネックが見つかった場合は、問題を解決するのに必要な追加の診断データを容易に取り込むことができます。 パフォーマンス ダッシュボードで容易に識別できる一般的なパフォーマンスの問題には次のようなものがあります。
-  CPU のボトルネック (および、CPU を最も消費しているクエリ)
-  I/O ボトルネック (および、IO を最も実行しているクエリ)
-  クエリ オプティマイザーによって生成された推奨インデックス (不足しているインデックス)
-  ブロッキング
-  リソースの競合 (ラッチの競合を含む)

パフォーマンス ダッシュボードはまた、前に実行されたコストの高いクエリを識別するためにも役立ちます。高コストを定義するには、次のようないくつかのメトリックを利用できます: CPU、論理書き込み数、論理読み取り数、期間、物理読み取り数、および CLR 時間。

パフォーマンス ダッシュボードは、次のセクションおよびサブレポートに分かれています。
-  システムの CPU 使用率
-  現在待機中の要求
-  現在の利用状況
   -  ユーザー要求
   -  ユーザー セッション
   -  Cache Hit Ratio
-  履歴情報
   -  の待機
   -  ラッチ
   -  I/O 統計
   -  コストの高いクエリ
- その他の情報
  -  アクティブなトレース
  -  アクティブな xEvent セッション
  -  データベース
  -  欠落したインデックス

> [!NOTE] 
> パフォーマンス ダッシュボードでは、内部的に、[実行](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)、[インデックス](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)、および [I/O](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md) 関連の動的管理ビュー (DMV) および関数 (DMF) が使用されます。

## <a name="to-view-the-performance-dashboard"></a>パフォーマンス ダッシュボードを表示するには 
  
パフォーマンス ダッシュボードを表示するには、オブジェクト エクスプローラー内で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス名を右クリックし、**[レポート]**、**[標準レポート]** の順に選択し、**[パフォーマンス ダッシュボード]** をクリックします。  
  
![メニュー内の [パフォーマンス ダッシュボード]](../../relational-databases/performance/media/perf_dashboard_ssms.png "メニュー内の [パフォーマンス ダッシュボード]")  
  
パフォーマンス ダッシュ ボードは、新しいタブとして表示されます。CPU のボトルネックが明らかに存在する例を次に示します。  
  
![パフォーマンス ダッシュ ボードのメイン画面](../../relational-databases/performance/media/perf_dashboard.png "パフォーマンス ダッシュ ボードのメイン画面")  
  
## <a name="remarks"></a>Remarks
**[欠落したインデックス]** レポートでは、クエリのコンパイル中にクエリ オプティマイザーによって識別された、欠落の可能性があるインデックスが表示されます。 ただし、これらの推奨事項は額面どおりに受け取るべきではありません。 インデックスを作成する場合は、スコアが 100,000 を超えていれば、ユーザー クエリを最大限に向上させると想定されるため、Microsoft ではこのようなインデックスを評価対象にすることをお勧めします。 

> [!TIP]
> 新しいインデックスの提案が同じテーブル内の既存のインデックスに匹敵するかどうかを常に確認します。テーブルでは、新しいインデックスを作成するのではなく、既存のインデックスを変更するだけで実際に同じ結果が得られることがあります。 たとえば、列 C1、C2、C3 に新しく提案されたインデックスが指定されると、最初に列 C1 と C2 に既存のインデックスが存在するかどうかが確認されます。 存在する場合は、単に列 C3 を既存のインデックスに (既存の列の順序を保持したまま) 追加すると、新しいインデックスを作成せずに済みます。
> 詳細については、[インデックス アーキテクチャとデザイン ガイド](../../relational-databases/sql-server-index-design-guide.md)に関するページを参照してください。

**[待機]** レポートでは、アイドル待機とスリープ待機のすべてが除外されます。 待機の詳細については、「[sys.dm_os_wait_stats &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)」および[待機とキューを使用した SQL Server 2005 のパフォーマンス チューニング](http://download.microsoft.com/download/4/7/a/47a548b9-249e-484c-abd7-29f31282b04d/performance_tuning_waits_queues.doc)に関する記事を参照してください。

基になる DMV 内のデータがクリアされたために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が再起動すると、**[コストの高いクエリ]** レポートはリセットされます。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降、コストの高いクエリに関する詳細情報はクエリ ストアで見つけることができます。 

> [!NOTE]
> パフォーマンス ダッシュボードは最初に、[SQL Server 2005](http://www.microsoft.com/download/details.aspx?id=22602) 向けのスタンドアロン ダウンロードとしてリリースされ、その後、[SQL Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=29063) 向けに更新されました。

## <a name="permissions"></a>アクセス許可  
`VIEW SERVER STATE` および `ALTER TRACE` アクセス許可が必要です。 

## <a name="see-also"></a>参照  
 [パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [パフォーマンス監視およびチューニング ツール](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [利用状況モニターを開く方法 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)     
 [利用状況モニター](../../relational-databases/performance-monitor/activity-monitor.md)     
 [クエリのストアを使用した、パフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
