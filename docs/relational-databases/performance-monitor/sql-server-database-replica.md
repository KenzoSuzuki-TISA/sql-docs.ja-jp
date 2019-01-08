---
title: SQL Server、Database Replica | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- SQLServer:Database Replica
- performance counters [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], performance counters
ms.assetid: a5f6bdce-2b13-4924-aaeb-b50b57d624d8
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 8b06de03e5fba1b351d304c97c6bd4262e7fd313
ms.sourcegitcommit: 0c1d552b3256e1bd995e3c49e0561589c52c21bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53380453"
---
# <a name="sql-server-database-replica"></a>SQL Server、データベース レプリカ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **SQLServer:Database Replica** パフォーマンス オブジェクトには、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の AlwaysOn 可用性グループのセカンダリ データベースに関する情報を報告するパフォーマンス カウンターが含まれています。 このオブジェクトは、セカンダリ レプリカをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスでのみ有効です。  
  
|カウンター名|[説明]|表示|  
|------------------|-----------------|--------------|  
|**受信ファイル バイト数/秒**|セカンダリ データベースのセカンダリ レプリカが最近 1 秒間に受信した FILESTREAM データの量。|セカンダリ レプリカ|  
|**ログ適用保留キュー**|データベース レプリカへの適用を待機しているログ ブロックの数。|セカンダリ レプリカ|
|**ログ適用準備完了キュー**|待機中でデータベース レプリカに適用可能なログ ブロックの数。|セカンダリ レプリカ| 
|**受信ログ バイト数/秒**|データベースのセカンダリ レプリカが最近 1 秒間に受信したログ レコードの量。|セカンダリ レプリカ|  
|**Log remaining for undo**|元に戻すフェーズを完了するためのログの残量 (KB 単位)。|セカンダリ レプリカ|  
|**Log Send Queue**|まだセカンダリ レプリカに送信されていない、プライマリ データベースのログ ファイル内のログ レコードの量 (KB 単位)。 この値は、プライマリ レプリカからセカンダリ レプリカに送信されます。 セカンダリに送信される FILESTREAM ファイルはキューのサイズに含まれません。|セカンダリ レプリカ|  
|**Mirrored Write Transaction/sec**|最後の 1 秒間に、プライマリ データベースに書き込まれたトランザクションのうち、ログがセカンダリ データベースに送信されるまでコミットを待機したトランザクションの数。|プライマリ レプリカ|  
|**Recovery Queue**|まだ再実行されていないセカンダリ レプリカのログ ファイル内のログ レコードの量。|セカンダリ レプリカ|  
|**Redo blocked/sec**|再実行スレッドがデータベースのリーダーで保持されているロックでブロックされる回数。|セカンダリ レプリカ|  
|**Redo Bytes Remaining**|元に戻すフェーズを完了するために再実行されるログの残量 (KB 単位)。|セカンダリ レプリカ|  
|**再適用バイト数/秒**|セカンダリ データベースで最近 1 秒間に再実行されたログ レコードの量。|セカンダリ レプリカ|  
|**Total Log requiring undo**|元に戻す必要のあるログの合計 KB 数。|セカンダリ レプリカ|  
|**Transaction Delay**|終了していないコミットの確認を待機中に生じた遅延 (ミリ秒単位)。|プライマリ レプリカ|  
  
## <a name="see-also"></a>参照  
 [リソースの利用状況の監視 &#40;システム モニター&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server、Availability Replica](../../relational-databases/performance-monitor/sql-server-availability-replica.md)   
 [SQL Server、Databases オブジェクト](../../relational-databases/performance-monitor/sql-server-databases-object.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
