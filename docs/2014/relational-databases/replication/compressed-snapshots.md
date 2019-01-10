---
title: 圧縮スナップショット | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], compressed
- snapshot replication [SQL Server], compressed snapshots
- compressed snapshots [SQL Server replication]
ms.assetid: 979ffa7c-3a88-4e70-8cf2-b8d452fd7a7f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c45dc872cd75640f244c55863cdbace607812a38
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52815344"
---
# <a name="compressed-snapshots"></a>圧縮スナップショット
  低速なネットワークでスナップショットを転送する場合や、スナップショットをリムーバブル メディアに保存する際にそのままではメディアに収まらない場合は、スナップショット ファイルを圧縮することができます。 スナップショット ファイルを圧縮すると、このような場合に役に立つ反面、スナップショットの生成および適用に要する時間が増大します。  
  
 圧縮スナップショット ファイルは [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB ファイル形式で書き込まれます。このファイル形式では 2 GB 以下のファイルを圧縮できます (スナップショット ファイルのサイズが 2 GB を超える場合は圧縮できません)。 ファイルを圧縮するには、代替スナップショット フォルダーにファイルを書き込む必要があります (既定のスナップショット フォルダーに書き込まれるファイルは圧縮できません)。 代替スナップショット フォルダーの詳細については、「[Alternate Snapshot Folder Locations (スナップショット フォルダーの代替位置)](alternate-snapshot-folder-locations.md)」を参照してください。  
  
 ファイルは、ディストリビューション エージェントまたはマージ エージェントが実行されている場所で圧縮解除されます。一般にプル サブスクリプションで圧縮スナップショットを使用する場合、サブスクライバーでファイルの圧縮が解除されるようにします。 サブスクライバーが圧縮ファイルを受信すると、そのファイルは最初は一時的な場所に書き込まれます。 圧縮ファイルがサブスクライバーにコピーされた後、圧縮ファイル内のスナップショット ファイルは CAB ユーティリティによって 1 ファイルずつ順番に圧縮解除されます。 サブスクライバーで必要な空き容量は、圧縮ファイルと圧縮されていない最大のファイルを合計したサイズと同じです。  
  
> [!NOTE]  
>  圧縮スナップショットを使用すると、ネットワーク経由でスナップショット ファイルを移動する際のパフォーマンスが向上する場合があります。 ただし、スナップショットを圧縮すると、スナップショット ファイル生成時のスナップショット エージェント、およびスナップショット ファイル適用時のディストリビューション エージェントまたはマージ エージェントで、追加の処理が必要になります。 これにより、スナップショット生成が遅くなり、スナップショットを適用するための時間が延びることもあります。 また、ネットワークに障害が発生した場合、圧縮スナップショットを復旧することはできません。したがって、信頼性の低いネットワークには向いていません。 ネットワーク経由で圧縮スナップショットを使用するときは、これらのトレードオフを慎重に検討してください。  
  
 **スナップショット ファイルを圧縮および配信するには**  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:[スナップショット ファイルの圧縮 (SQL Server Management Studio)](publish/compress-snapshot-files-sql-server-management-studio.md)  
  
-   レプリケーション[!INCLUDE[tsql](../../includes/tsql-md.md)]プログラミングします。[スナップショットのプロパティの構成 (レプリケーション Transact-SQL プログラミング)](publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>参照  
 [Initialize a Subscription with a Snapshot (スナップショットを使用したサブスクリプションの初期化)](initialize-a-subscription-with-a-snapshot.md)   
 [スナップショット オプション](snapshot-options.md)  
  
  
