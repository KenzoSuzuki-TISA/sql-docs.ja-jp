---
title: サブスクリプション、[同期の履歴] (マージ サブスクリプション、SQL Server 2000) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.subscription.downlevelsynchhistory.f1
ms.assetid: 0a0deab2-1c08-4371-9681-d9403e0236cc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 435b24f8f6d7c9255db3c7d72f78ffe474a85c6e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52821986"
---
# <a name="subscription-synchronization-history-merge-subscription-sql-server-2000"></a>サブスクリプション、[同期の履歴] (マージ サブスクリプション、SQL Server 2000)
  **[同期の履歴]** タブには、マージ エージェントの状態、履歴、情報メッセージ、エラー メッセージなどの詳細情報が表示されます。  
  
## <a name="options"></a>および  
 表示するマージ エージェント セッションを **[表示]** メニューで選択した後、 **[マージ エージェントのセッション]** という名前のグリッドで特定のセッションを選択します。 このセッションの詳細情報は、 **[選択されたセッションのアクション]** というラベルのグリッドに表示されます。 選択したセッションがエラーで終了した場合は、 **[選択されたセッションのエラーの詳細またはメッセージ]** というラベルのテキスト領域も表示されます。  
  
 **[表示]**  
 表示するマージ エージェント セッションを選択します。 一般的に、マージ エージェントは継続的に実行されるため、表示されるセッションが 1 つのみである場合もあります。  
  
 **ステータス**  
 マージ エージェントの状態です。 表示される状態の種類を、次に示します。  
  
-   [エラー]  
  
-   [完了]  
  
-   [再試行中]  
  
-   実行中  
  
 **Start Time**  
 セッションの開始時刻です。  
  
 **[終了時刻]**  
 セッションの終了時刻です。 エージェントが停止していない場合は、このフィールドは空になっています。  
  
 **Duration**  
 このセッションでマージ エージェントが実行された時間の合計です。 エージェントが現在実行中の場合、経過時間を表します。エージェントが終了している場合、セッションの合計時間を表します。  
  
 **エラー メッセージ**  
 セッションがエラーで終了した場合、このフィールドにはマージ エージェントによってログに記録された最後のエラー メッセージが表示されます。 セッションがエラーで終了しなかった場合は、このフィールドは空白です。  
  
 **[動作メッセージ]**  
 選択したセッション中にマージ エージェントによって記録された、すべての情報メッセージとエラー メッセージです。  
  
 **[動作時間]**  
 **[動作メッセージ]** 列で説明されたアクションが実行された時間です。  
  
 **[選択されたセッションのエラーの詳細またはメッセージ]**  
 選択したセッションの **[状態]** 列に **[エラー]** の値が表示されている場合にのみ表示されます。 このテキスト領域では、エラーの詳細情報とエラーの発生時に試行されたコマンドが表示されます。 エラーに関連する追加コンテンツへのリンクも含まれます。  
  
## <a name="see-also"></a>参照  
 [レプリケーション モニターの開始](monitor/start-the-replication-monitor.md)   
 [サブスクリプションに関連付けられているエージェントの情報を表示し、タスクを実行する &#40;レプリケーション モニター&#41;](monitor/view-information-and-perform-tasks-for-subscription-agents.md)   
 [レプリケーションの監視](monitoring-replication.md)   
 [レプリケーション エージェントの概要](agents/replication-agents-overview.md)  
  
  
