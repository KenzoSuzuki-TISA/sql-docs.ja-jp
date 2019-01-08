---
title: syspublications (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- syspublications
- syspublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspublications system table
ms.assetid: a86eb4f5-1f7b-493e-af55-3d15cf878228
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ed5e46a5bfb9b4c4081eb2df7d4f93b7dd12b29f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52822936"
---
# <a name="syspublications-transact-sql"></a>syspublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベースに定義されているパブリケーションごとに 1 行のデータを格納します。 このテーブルは、パブリケーション データベース内に保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**description**|**nvarchar (255)**|パブリケーションの説明エントリします。|  
|**name**|**sysname**|パブリケーションに関連付けられた一意な名前。|  
|**pubid**|**int**|パブリケーションの一意な ID を示す ID 列。|  
|**repl_freq**|**tinyint**|レプリケーションの頻度。<br /><br /> **0** = トランザクション ベースします。<br /><br /> **1** = テーブルの定期更新します。|  
|**status**|**tinyint**|状態。<br /><br /> **0** = 非アクティブです。<br /><br /> **1** = アクティブ。|  
|**sync_method**|**tinyint**|同期方法。<br /><br /> **0** = ネイティブ モードの一括コピー プログラム ユーティリティ (**BCP**)。<br /><br /> **1** = キャラクター モード BCP。<br /><br /> **3** = 同時実行は、ネイティブ モード BCP が使用されますが、スナップショット時にテーブルがロックされていないことを意味します。<br /><br /> **4** = Concurrent_c で、キャラクター モード BCP が使用されますが、スナップショット時にテーブルがロックされていないことを意味します。|  
|**snapshot_jobid**|**binary(16)**|スケジュールされたタスク id。|  
|**independent_agent**|**bit**|このパブリケーションに対して、スタンドアロンのディストリビューション エージェントがあるかどうかを示します。<br /><br /> **0** = パブリケーションは共有ディストリビューション エージェントを使用して、パブリッシャー データベース/サブスクライバー データベースの各ペアが 1 つの共有エージェント。<br /><br /> **1** = このパブリケーション用のスタンドアロン ディストリビューション エージェントが存在します。|  
|**immediate_sync**|**bit**|同期ファイルが作成またはスナップショット エージェントを実行するたびに再作成するかどうかを示します、 **1**エージェントを実行するたびに、それらが作成されることを意味します。|  
|**enabled_for_internet**|**bit**|パブリケーションの同期ファイルが他のサービスとファイル転送プロトコル (FTP) 経由でインターネットに公開されるかどうかを示します、 **1**インターネットからアクセスできることを意味します。|  
|**allow_push**|**bit**|パブリケーションに対してプッシュ サブスクリプションを許可するかどうかを示す、 **1**が許可されていることを意味します。|  
|**allow_pull**|**bit**|パブリケーションに対してプル サブスクリプションを許可するかどうかを示す、 **1**が許可されていることを意味します。|  
|**allow_anonymous**|**bit**|パブリケーションに対して匿名サブスクリプションを許可するかどうかを示す、 **1**が許可されていることを意味します。|  
|**immediate_sync_ready**|**bit**|スナップショットがスナップショット エージェントによって生成されたかどうか、および新しいサブスクリプションで使用できるかどうかを示します。 即時更新パブリケーションでのみ意味を持ちます。 **1**スナップショット準備ができていることを示します。|  
|**allow_sync_tran**|**bit**|パブリケーションでサブスクリプションの即時更新を許可するかどうかを示します。 **1**即時更新サブスクリプションを許可することを意味します。|  
|**autogen_sync_procs**|**bit**|即時更新サブスクリプションの同期ストアド プロシージャがパブリッシャーで生成されるかどうかを示します。 **1**パブリッシャー側で生成されることを意味します。|  
|**保有期間**|**int**|指定されたパブリケーションに関する変更を保存する時間。|  
|**allowed_queued_tran**|**bit**|変更をパブリッシャーで適用できるようになるまで、サブスクライバーで変更をキューに保持するかどうかを示します。 場合**1**、サブスクライバーの変更はキューに登録します。|  
|**snapshot_in_defaultfolder**|**bit**|既定のフォルダーに、スナップショット ファイルが格納されているかどうかを指定します。<br /><br /> **0** = スナップショット ファイルがで指定された代替位置に格納されている*alternate_snapshot_folder*します。<br /><br /> **1** = スナップショット ファイルは既定のフォルダーにあります。|  
|**alt_snapshot_folder**|**nvarchar (255)**|スナップショットの代替フォルダーの場所を指定します。|  
|**pre_snapshot_script**|**nvarchar (255)**|ポインターを指定します、 **.sql**ファイルの場所。 ディストリビューション エージェントは、サブスクライバー側でスナップショットを適用するとき、レプリケートされたオブジェクト スクリプトより前に、プリスナップショット スクリプトを実行します。|  
|**post_snapshot_script**|**nvarchar (255)**|ポインターを指定します、 **.sql**ファイルの場所。 ディストリビューション エージェントは、最初の同期中、他のすべてのレプリケートされたオブジェクト スクリプトとデータが適用された後に、ポストスナップショット スクリプトを実行します。|  
|**compress_snapshot**|**bit**|指定に書き込まれたスナップショット、 *alt_snapshot_folder*の場所を圧縮するには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 形式です **。1**スナップショットが圧縮されることを意味します。|  
|**ftp_address**|**sysname**|ディストリビューター用 FTP サービスのネットワーク アドレス。 ディストリビューション エージェントが受け取るパブリケーション スナップショット ファイルの場所を示します。|  
|**ftp_port**|**int**|ディストリビューター用 FTP サービスのポート番号。 パブリケーションのスナップショット ファイルが取得するため、ディストリビューション エージェントの存在を指定します。|  
|**ftp_subdirectory**|**nvarchar (255)**|パブリケーションで、FTP を利用したスナップショット配布がサポートされている場合に、ディストリビューション エージェントがパブリケーション スナップショット ファイルを取得する場所。|  
|**ftp_login**|**sysname**|FTP サービスへの接続に使用されるユーザー名。|  
|**ftp_password**|**nvarchar (524)**|FTP サービスへの接続に使用されるユーザー パスワード。|  
|**allow_dts**|**bit**|パブリケーションがデータ変換を許可するかどうかを示します。 **1** DTS 変換が許可されることを指定します。|  
|**allow_subscription_copy**|**bit**|パブリケーションにサブスクライブするサブスクリプション データベースをコピーする機能が有効かどうかを示します。 **1**コピーが許可されていることを意味します。|  
|**centralized_conflicts**|**bit**|競合レコードがパブリッシャーに格納されるかどうかを示します。<br /><br /> **0** = 競合レコードはパブリッシャー側の両方と、競合の原因となったサブスクライバーで格納されます。<br /><br /> **1** = 競合レコードはパブリッシャーに格納されます。|  
|**conflict_retention**|**int**|競合の保有期間の日数を指定します。|  
|**conflict_policy**|**int**|キュー更新サブスクライバー オプションを使用するときの競合の解決方法。 これらの値のいずれかを指定できます。<br /><br /> **1** = パブリッシャー優先します。<br /><br /> **2** = サブスクライバー優先します。<br /><br /> **3** = サブスクリプションを再初期化します。|  
|**queue_type**|**int**|使用されるキューの種類。 これらの値のいずれかを指定できます。<br /><br /> **1** 、msmq を =[!INCLUDE[msCoName](../../includes/msconame-md.md)]メッセージ キューがトランザクションを格納します。<br /><br /> **2** = を使用して、sql[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]トランザクションを格納します。<br /><br /> 注:[!INCLUDE[msCoName](../../includes/msconame-md.md)] メッセージ キューイングは非推奨とされており、現在は利用できません。|  
|**ad_guidname**|**sysname**|パブリケーションが [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory にパブリッシュされるかどうかを示します。 有効なグローバル一意識別子 (GUID) は、Active Directory でパブリケーションがパブリッシュされることと、GUID は、対応する Active Directory パブリケーション オブジェクトを指定します。 **objectGUID**します。 NULL の場合、パブリケーションは Active Directory にパブリッシュされません。|  
|**backward_comp_level**|**int**|データベースの互換性レベル。次のいずれかの値になります。<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].<br /><br /> **110** = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].<br /><br /> **120** = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].|  
|**allow_initialize_from_backup**|**bit**|サブスクライバーが初期スナップショットではなくバックアップから、このパブリケーションに対するサブスクリプションを初期化できるかどうかを示します。 **1** 、バックアップからサブスクリプションを初期化できることを意味し、 **0**できないことを意味します。 詳細については、「 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)を使用して、サブスクリプションを手動で初期化する方法について説明します。|  
|**min_autonosync_lsn**|**[バイナリ]**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**int**|パブリケーションに対してスキーマ レプリケーションがサポートされているかどうかを示します。 **1** 、パブリッシャーで実行されるデータ定義言語 (DDL) ステートメントがレプリケートされることを示しますと**0** DDL ステートメントがレプリケートされないことを示します。 詳細については、「[パブリケーション データベースでのスキーマの変更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)」を参照してください。|  
|**options**|**int**|追加のパブリッシング オプションを指定するビットマップ。ビットごとのオプション値は次のようになります。<br /><br /> **0x1** - ピア ツー ピア レプリケーションに対して有効です。<br /><br /> **0x2** -ピア ツー ピア レプリケーションに対してローカル変更のみをパブリッシュします。<br /><br /> **0x4** - に対して有効でない[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サブスクライバー。<br /><br /> **0x8** - ピア ツー ピア競合検出に対して有効です。|  
|**originator_id**|**smallint**|競合検出のためにピア ツー ピア レプリケーション トポロジの各ノードを識別します。 詳細については、「 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)」を参照してください。|  
  
## <a name="see-also"></a>参照  
 [レプリケーション テーブル &#40; です。TRANSACT-SQL と &#41; です。](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addpublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)  
  
  
