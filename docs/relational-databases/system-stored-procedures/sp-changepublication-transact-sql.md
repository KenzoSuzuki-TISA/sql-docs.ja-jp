---
title: sp_changepublication (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changepublication
- sp_changepublication_TSQL
helpviewer_keywords:
- sp_changepublication
ms.assetid: c36e5865-25d5-42b7-b045-dc5036225081
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7b247e6869d3eea05325fd9020ee6a073540deb4
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2018
ms.locfileid: "53209131"
---
# <a name="spchangepublication-transact-sql"></a>sp_changepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  パブリケーションのプロパティを変更します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_changepublication [ [ @publication = ] 'publication' ]  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
 [ **@publication =** ] **'***publication***'**  
 パブリケーションの名前です。 *パブリケーション*は**sysname**、既定値は NULL です。  
  
 [  **@property =** ] **'***プロパティ***'**  
 変更するパブリケーションのプロパティを指定します。 *プロパティ*は**nvarchar (255)** します。  
  
 [  **@value =** ] **'***値***'**  
 新しいプロパティ値を指定します。 *値*は**nvarchar (255)**、既定値は NULL です。  
  
 次の表に、変更可能なパブリケーションのプロパティと、プロパティの値に関する制限を示します。  
  
|プロパティ|値|説明|  
|--------------|-----------|-----------------|  
|**allow_anonymous**|**true**|指定したパブリケーションに対して匿名サブスクリプションを作成できると*immediate_sync*必要もあります**true**します。 ピア ツー ピア パブリケーションの場合は変更できません。|  
||**false**|指定したパブリケーションに対して匿名サブスクリプションを作成できません。 ピア ツー ピア パブリケーションの場合は変更できません。|  
|**allow_initialize_from_backup**|**true**|サブスクライバーでは、初期スナップショットではなくバックアップから、このパブリケーションへのサブスクリプションを初期化できます。 このプロパティを変更することはできません以外[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリケーション。|  
||**false**|サブスクライバーでは初期スナップショットを使用する必要があります。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
|**allow_partition_switch**|**true**|ALTER TABLE…パブリッシュされたデータベースに対して SWITCH ステートメントを実行できます。 詳細については、「[パーティション テーブルとパーティション インデックスのレプリケート](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)」を参照してください。|  
||**false**|ALTER TABLE…パブリッシュされたデータベースに対して SWITCH ステートメントを実行することはできません。|  
|**allow_pull**|**true**|指定したパブリケーションに対してプル サブスクリプションを許可します。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
||**false**|指定したパブリケーションに対してプル サブスクリプションを許可しません。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
|**allow_push**|**true**|指定したパブリケーションに対してプッシュ サブスクリプションを許可します。|  
||**false**|指定したパブリケーションに対してプッシュ サブスクリプションを許可しません。|  
|**allow_subscription_copy**|**true**|このパブリケーションにサブスクライブするデータベースをコピーできるようにします。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
||**false**|このパブリケーションにサブスクライブするデータベースをコピーできないようにします。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
|**alt_snapshot_folder**||スナップショットの代替フォルダーの場所。|  
|**centralized_conflicts**|**true**|競合レコードはパブリッシャーに保存されます。 アクティブなサブスクリプションがない場合にのみ変更できます。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
||**false**|競合レコードは、競合の原因となったパブリッシャーとサブスクライバーの両方に保存されます。 アクティブなサブスクリプションがない場合にのみ変更できます。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
|**compress_snapshot**|**true**|代替スナップショット フォルダーにあるスナップショットは .cab ファイル形式に圧縮されます。 既定のスナップショット フォルダー内のスナップショットは圧縮できません。|  
||**false**|スナップショットは圧縮されません。これはレプリケーションの既定の動作です。|  
|**conflict_policy**|**pub wins**|パブリッシャーが競合で優先される場合に、サブスクライバーの更新で競合を解決する方法です。 このプロパティを変更できるのは、アクティブなサブスクリプションがない場合に限られます。 Oracle パブリッシャーに対してはサポートされていません。|  
||**sub reinit**|サブスクライバーの更新で、競合が発生した場合はサブスクリプションを再初期化する必要があります。 このプロパティを変更できるのは、アクティブなサブスクリプションがない場合に限られます。 Oracle パブリッシャーに対してはサポートされていません。|  
||**sub wins**|サブスクライバーが競合で優先される場合に、サブスクライバーの更新で競合を解決する方法です。 このプロパティを変更できるのは、アクティブなサブスクリプションがない場合に限られます。 Oracle パブリッシャーに対してはサポートされていません。|  
|**conflict_retention**||**int**競合の保有期間を日数で指定します。 既定の保有期間は 14 日です。 **0**競合のクリーンアップが必要ないことを意味します。 Oracle パブリッシャーに対してはサポートされていません。|  
|**description**||パブリケーションを記述するエントリです。省略可能です。|  
|**enabled_for_het_sub**|**true**|パブリケーションで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーのサポートを有効にします。 **enabled_for_het_sub**パブリケーションに対するサブスクリプションがある場合は変更できません。 実行する必要があります[レプリケーションのストアド プロシージャ (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)設定する前に、次の要件に準拠する**enabled_for_het_sub**を true にします。<br /> - **allow_queued_tran**あります**false**します。<br /> - **allow_sync_tran**あります**false**します。<br /> 変更する**enabled_for_het_sub**に**true**既存のパブリケーション設定を変更することがあります。 詳細については、「 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)」を参照してください。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
||**false**|パブリケーションで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーはサポートされません。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
|**enabled_for_internet**|**true**|パブリケーションはインターネットに対応しており、サブスクライバーへのスナップショット ファイルの転送にファイル転送プロトコル (FTP) を使用できます。 パブリケーションの同期ファイルは、次のディレクトリに配置されます。C:\Program files \microsoft SQL server \mssql\repldata\ftp します。 *ftp_address* NULL にすることはできません。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
||**false**|パブリケーションはインターネットに対応していません。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
|**enabled_for_p2p**|**true**|パブリケーションでピア ツー ピア レプリケーションがサポートされます。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。<br /> 設定する**enabled_for_p2p**に**true**、次の制限が適用されます。<br /> - **allow_anonymous**あります**false**<br /> - **allow_dts を含む**あります**false**します。<br /> - **allow_initialize_from_backup**あります**は true。**<br /> - **allow_queued_tran**あります**false**します。<br /> - **allow_sync_tran**あります**false**します。<br /> - **enabled_for_het_sub**あります**false**します。<br /> - **independent_agent**あります**true**します。<br /> - **repl_freq**あります**連続**します。<br /> - **replicate_ddl**あります**1**します。|  
||**false**|パブリケーションでピア ツー ピア レプリケーションがサポートされません。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
|**ftp_address**||パブリケーション スナップショット ファイルに FTP でアクセスできる場所です。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
|**ftp_login**||FTP サービスへの接続に使用するユーザー名です。値 ANONYMOUS は許可されます。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
|**ftp_password**||FTP サービスに接続するときに使用するユーザー名に対応するパスワード。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
|**ftp_port**||ディストリビューター用 FTP サービスのポート番号。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
|**ftp_subdirectory**||スナップショット ファイルを作成する場所を指定します、パブリケーションが FTP を使用してスナップショットの配布をサポートしている場合。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
|**immediate_sync**|**true**|スナップショット エージェントを実行するたびに、パブリケーションの同期ファイルが作成または再作成されます。 サブスクリプションの前にスナップショット エージェントが完了していれば、サブスクライバーではサブスクリプションの直後に同期ファイルを取得できます。 新しいサブスクリプションは、最近実行されたスナップショット エージェントによって生成された最新の同期ファイルを取得します。 *independent_agent*必要もあります**true**します。 に関する追加情報の下の「解説」を参照してください**immediate_sync**します。|  
||**false**|新しいサブスクリプションがある場合にのみ、同期ファイルが作成されます。 サブスクリプションの後、スナップショット エージェントが起動して完了するまで、サブスクライバーは同期ファイルを取得できません。|  
|**independent_agent**|**true**|パブリケーションに専用のディストリビューション エージェントがあります。|  
||**false**|パブリケーションでは共有ディストリビューション エージェントが使用されます。パブリケーションおよびサブスクリプション データベースの各ペアには 1 つの共有エージェントがあります。|  
|**このとき p2p_continue_onconflict**|**true**|ディストリビューション エージェントは、競合の検出時に変更の処理を続行します。<br /> **注意が必要です。** 既定値の `FALSE` を使用することをお勧めします。 このオプションを設定すると`TRUE`、ディストリビューション エージェントが、最高の発信元 ID を持つノードから競合する行を適用してトポロジ内のデータを収束しようとしています。 この方法では収束が保証されません。 競合が検出された後に、トポロジに一貫性があることを確認する必要があります。 詳細については、「 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)」の「競合の処理」を参照してください。|  
||**false**|ディストリビューション エージェントは、競合の検出時に変更の処理を停止します。|  
|**post_snapshot_script**||ディストリビューション エージェントで実行される [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト ファイルの場所を指定します。このスクリプトの実行は、初期同期で、レプリケートされたすべてのオブジェクト スクリプトとデータが適用された後で行われます。|  
|**pre_snapshot_script**||ディストリビューション エージェントで実行される [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト ファイルの場所を指定します。このスクリプトの実行は、初期同期で、レプリケートされたすべてのオブジェクト スクリプトとデータが適用される前に行われます。|  
|**publish_to_ActiveDirectory**|**true**|このパラメーターは、旧バージョンのスクリプトとの互換性を保つために用意されており、非推奨とされます。 現在、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory にはパブリケーション情報を追加できません。|  
||**false**|Active Directory からパブリケーション情報を削除します。|  
|**queue_type**|**sql**|トランザクションの保存に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用。 このプロパティを変更できるのは、アクティブなサブスクリプションがない場合に限られます。<br /><br /> 注:[!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing (MSMQ) の使用は現在サポートされていません。 値を指定する**msmq**の*値*エラーが発生します。|  
|**repl_freq**|**継続的です**|ログ ベースのすべてのトランザクションの出力をパブリッシュします。|  
||**スナップショット**|スケジュールされた同期イベントのみをパブリッシュします。|  
|**replicate_ddl**|**1**|データ定義言語 (DDL) ステートメントがパブリッシャーで実行がレプリケートされます。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。|  
||**0**|DDL ステートメントはレプリケートされません。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリケーションの場合は変更できません。 スキーマ変更のレプリケーションは、ピア ツー ピア レプリケーションを使用する場合は無効にできません。|  
|**replicate_partition_switch**|**true**|ALTER TABLE…パブリッシュされたデータベースに対して実行される SWITCH ステートメントをサブスクライバーにレプリケートする必要があります。 このオプションは有効な場合にのみ*allow_partition_switch*が TRUE に設定します。 詳細については、「[パーティション テーブルとパーティション インデックスのレプリケート](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)」を参照してください。|  
||**false**|ALTER TABLE…SWITCH ステートメントをサブスクライバーにレプリケートしないようにします。|  
|**保有期間**||**int**保有期間を時間、サブスクリプションの利用状況を表します。 保有期間内にサブスクリプションがアクティブ状態でなくなると削除されます。|  
|**snapshot_in_defaultfolder**|**true**|スナップショット ファイルは既定のスナップショット フォルダーに格納されます。 場合*alt_snapshot_folder*も指定、スナップショット ファイルは既定値と別の場所の両方に格納します。|  
||**false**|指定された別の場所にスナップショット ファイルが格納されている*alt_snapshot_folder*します。|  
|**status**|**アクティブ**|パブリケーション データはパブリケーションが作成された直後にサブスクライバーで使用できます。 Oracle パブリッシャーに対してはサポートされていません。|  
||**非アクティブ**|パブリケーション データはパブリケーションが作成されてもサブスクライバーで使用できません。 Oracle パブリッシャーに対してはサポートされていません。|  
|**sync_method**|**native**|サブスクリプションの同期時に、すべてのテーブルのネイティブ モード一括コピー出力を使用します。|  
||**character**|サブスクリプションの同期時に、すべてのテーブルについてキャラクター モード一括コピー出力を使用します。|  
||**同時実行**|すべてのテーブルについてネイティブ モード BCP 出力を使用しますが、スナップショット生成処理中にテーブルをロックしません。 スナップショット レプリケーションには無効です。|  
||**concurrent_c**|すべてのテーブルについてキャラクター モード BCP 出力を使用しますが、スナップショット生成処理中にテーブルをロックしません。 スナップショット レプリケーションには無効です。|  
|**taskid**||このプロパティは現在サポートされておらず、非推奨とされます。|  
|**allow_drop**|**true**|により、`DROP TABLE`トランザクション レプリケーションの一部であるアーティクルの DLL をサポートします。 サポートされる最小バージョン。[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Service Pack 2 以降および[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]Service Pack 1 以降。 その他の参照。[KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactional-replication-in-sql-server-2014-or-in-sql-server-2016-sp1)|
||**false**|無効にします`DROP TABLE`トランザクション レプリケーションの一部であるアーティクルの DLL をサポートします。 これは、**既定**このプロパティの値。|
|**NULL** (既定値)||サポートされている値の一覧を返します*プロパティ*します。|  
  
[ **@force_invalidate_snapshot =** ]*更によって*  
 このストアド プロシージャが実行する操作によって既存のスナップショットが無効になることを許可します。 *更によって*は、**ビット**、既定値は**0**します。  
  - **0**スナップショットが無効であることをアーティクルへの変更が発生しないことを指定します。 ストアド プロシージャで、変更に新しいスナップショットが必要であることが検出されると、エラーが発生し、変更は加えられません。  
  - **1**アーティクルへの変更は、無効になるスナップショットで発生する可能性がありますを指定します。 新しいスナップショットが必要となる既存のサブスクリプションがある場合、この値は、既存のスナップショットに設定して、新しいスナップショットを生成のアクセス許可を示します。   
変更によって新しいスナップショットの生成が必要になるプロパティについては、「解説」を参照してください。  
  
[ **@force_reinit_subscription =** ]*更によって*  
 このストアド プロシージャが実行する操作によって、既存のサブスクリプションの再初期化が必要になることを許可します。 *更によって*は、**ビット**、既定値は**0**します。  
  - **0**アーティクルへの変更では、サブスクリプションを再初期化するのには発生しないことを指定します。 変更に既存のサブスクリプションの再初期化が必要であることをストアド プロシージャが検出すると、エラーが発生し、変更は加えられません。  
  - **1**アーティクルへの変更が発生する、既存のサブスクリプションを再初期化されることを指定します。 サブスクリプションの再初期化を許可します。  
  
[ **@publisher** =] **'***パブリッシャー***'**  
 以外を指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーです。 *パブリッシャー*は**sysname**、既定値は NULL です。  
  
  > [!NOTE]  
  >  *パブリッシャー*でアーティクルのプロパティを変更する場合、使用されませんが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーです。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_changepublication**スナップショット レプリケーションおよびトランザクション レプリケーションで使用されます。  
  
 次のプロパティを変更した後に、新しいスナップショットを生成する必要がありの値を指定する必要があります**1**の*更によって*パラメーター。  
-   **alt_snapshot_folder**  
-   **compress_snapshot**  
-   **enabled_for_het_sub**  
-   **ftp_address**  
-   **ftp_login**  
-   **ftp_password**  
-   **ftp_port**  
-   **ftp_subdirectory**  
-   **post_snapshot_script**  
-   **pre_snapshot_script**  
-   **snapshot_in_defaultfolder**  
-   **sync_mode**  
  
使用して、Active Directory パブリケーション オブジェクトの一覧、 **publish_to_active_directory**パラメーター、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクトは、Active Directory で既に作成する必要があります。  
  
## <a name="impact-of-immediate-sync"></a>即時同期の影響  
 即時同期では、サブスクリプションがない場合でも、初期スナップショットが生成された直後に、ログ内のすべての変更が追跡されます。 ログに記録された変更は、顧客が新しいピア ノードを追加するバックアップを使用する際に使用されます。 バックアップが復元された後、ピアは、バックアップが作成された後に発生しているその他の変更と同期されました。 コマンドがディストリビューション データベースで追跡されるため、同期ロジックは最後の LSN のバックアップを確認し、このコマンドは、最大保有期間内で、バックアップが作成された場合に使用できることを知ること、開始点として使用できます。 (既定値は 0 時間、最大保有期間を最小保有期間は 24 時間です)。  
  
 即時同期がオフの場合は、変更は少なくとも最小保有期間に保持され、すぐに複製されているすべてのトランザクションのクリーンアップします。 即時同期が無効で、既定の保有期間で構成される場合、バックアップの作成後に必要な変更がクリーンアップされたため、新しいピア ノードが正しく初期化されない可能性があります。 残された唯一のオプションがトポロジの停止です。 即時同期を有効に設定すると、柔軟性が向上するため、これは P2P アプリケーションにお勧めの設定です。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_changepublication](../../relational-databases/replication/codesnippet/tsql/sp-changepublication-tra_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_changepublication**します。  
  
## <a name="see-also"></a>参照  
 [パブリケーション プロパティの表示および変更](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [パブリケーションとアーティクルのプロパティの変更](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addpublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_droppublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
