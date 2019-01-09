---
title: sp_replmonitorhelpsubscription (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelpsubscription_TSQL
- sp_replmonitorhelpsubscription
helpviewer_keywords:
- sp_replmonitorhelpsubscription
ms.assetid: a681b2db-c82d-4624-a10c-396afb0ac42f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9ac45c3b25e1a13366ae273b8d21d7e41e768251
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52748310"
---
# <a name="spreplmonitorhelpsubscription-transact-sql"></a>sp_replmonitorhelpsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  パブリッシャー側の 1 つ以上のパブリケーションに属するサブスクリプションの現在の状態情報を返します。サブスクリプションごとに 1 行のデータが返されます。 このストアド プロシージャはレプリケーションの監視に使用し、ディストリビューター側でディストリビューション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_replmonitorhelpsubscription [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @mode = ] mode ]  
    [ , [ @topnum = ] topnum ]   
    [ , [ @exclude_anonymous = ] exclude_anonymous ]   
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>引数  
 [ **@publisher** =] **'***パブリッシャー***'**  
 状態を監視しているパブリッシャーの名前を指定します。 *パブリッシャー*は**sysname**既定値は NULL です。 場合**null**ディストリビューターを使用するすべてのパブリッシャーの情報が返されます。  
  
 [ **@publisher_db** =] **'***publisher_db***'**  
 パブリッシャー データベースの名前を指定します。 *publisher_db*は**sysname**既定値は NULL です。 NULL の場合、パブリッシャー側のパブリッシュされたすべてのデータベースに関する情報が返されます。  
  
 [ **@publication** =] **'***パブリケーション***'**  
 監視されているパブリケーションの名前を指定します。 *パブリケーション*は**sysname**既定値は NULL です。  
  
 [ **@publication_type** =] *publication_type*  
 パブリケーションの種類を指定します。 *publication_type*は**int**、これらの値のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**0**|トランザクション パブリケーションです。|  
|**1**|スナップショット パブリケーションです。|  
|**2**|マージ パブリケーションです。|  
|NULL (既定値)|レプリケーションでは、パブリケーションの種類の判別が試行されます。|  
  
 [ **@mode** =]*モード*  
 サブスクリプションの監視情報を返すときに使用するフィルター選択モードを指定します。 *モード*は**int**、これらの値のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**0** (既定値)|すべてのサブスクリプションを返します。|  
|**1**|エラーがあるサブスクリプションだけを返します。|  
|**2**|しきい値超過の警告を生成したサブスクリプションだけを返します。|  
|**3**|エラーがあった、またはしきい値超過の警告を生成したサブスクリプションだけを返します。|  
|**4**|最上位 25 のパフォーマンスの低いサブスクリプションを返します。|  
|**5**|パフォーマンスが低い下位 50 個のサブスクリプションを返します。|  
|**6**|現在同期しているサブスクリプションだけを返します。|  
|**7**|現在同期していないサブスクリプションだけを返します。|  
  
 [ **@topnum** =] *topnum*  
 返されたデータのうち、先頭から指定した数のサブスクリプションだけを結果セットに含めます。 *topnum*は**int**、既定値はありません。  
  
 [ **@exclude_anonymous** =] *exclude_anonymous*  
 匿名プル サブスクリプションを結果セットから除外するかどうかを指定します。 *exclude_anonymous*は**ビット**、既定値は**0**です値の**1**匿名サブスクリプションを除外することを意味し、値**0。** 含まれていることを意味します。  
  
 [  **@refreshpolicy=** ] *refreshpolicy*  
 内部使用のみです。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**status**|**int**|パブリケーションに関連付けられたすべてのレプリケーション エージェントの状態を調査し、次の順序に従って、見つかった最も高いステータスを返します。<br /><br /> **6** = に失敗しました<br /><br /> **5** = 再試行<br /><br /> **2** = 停止<br /><br /> **4** = アイドル状態<br /><br /> **3** = 実行中<br /><br /> **1** = 開始|  
|**警告**|**int**|パブリケーションに属しているサブスクリプションによって生成されるしきい値警告の最大値です。次の 1 つ以上の値の論理和になります。<br /><br /> **1** = 有効期限の保有期間のしきい値内で、トランザクション パブリケーションに対するサブスクリプションが同期されていません。<br /><br /> **2** = 待機時間、トランザクション パブリッシャーからサブスクライバーへのデータのレプリケートにかかった時間 (秒)、しきい値を超えています。<br /><br /> **4** = mergeexpiration 保有期間のしきい値内でマージ パブリケーションに対するサブスクリプションが同期されていません。<br /><br /> **8** = mergefastrunduration - マージ サブスクリプションの同期の完了にかかった時間、高速ネットワーク接続経由で秒単位で、しきい値を超えています。<br /><br /> **16** = mergeslowrunduration - マージ サブスクリプションの同期の完了にかかった時間、低速またはダイヤルアップ ネットワーク接続経由で秒単位で、しきい値を超えています。<br /><br /> **32** = mergefastrunspeed - 配信率マージ サブスクリプションの同期中の行が高速ネットワーク接続経由でのしきい値の割合で、1 秒あたりの行を維持するために失敗しました。<br /><br /> **64** mergeslowrunspeed - 配信率 = マージ サブスクリプションの同期中の行が低速またはダイヤルアップ ネットワーク接続経由でのしきい値の割合で、1 秒あたりの行を維持するために失敗しました。|  
|**サブスクライバー**|**sysname**|サブスクライバーの名前です。|  
|**@subscriber_db**|**sysname**|サブスクリプションで使用されるデータベースの名前です。|  
|**publisher_db**|**sysname**|パブリケーション データベースの名前です。|  
|**パブリケーション**|**sysname**|パブリケーションの名前です。|  
|**publication_type**|**int**|パブリケーションで、これらの値のいずれかの種類を示します。<br /><br /> **0** = トランザクション パブリケーション<br /><br /> **1** = スナップショット パブリケーション<br /><br /> **2** = マージ パブリケーション|  
|**サブタイプ**|**int**|サブスクリプションの種類です。次のいずれかの値をとります。<br /><br /> **0**プッシュを =<br /><br /> **1** = プル<br /><br /> **2** = 匿名|  
|**latency**|**int**|データ変更が、トランザクション パブリケーションのログ リーダー エージェントとディストリビューション エージェントで伝達されるまでの最大待機時間 (秒単位) です。|  
|**latencythreshold**|**int**|トランザクション パブリケーションの最大待機時間です。この値を超過すると警告が生成されます。|  
|**agentnotrunning**|**int**|エージェントが実行されていない期間 (時間単位) です。|  
|**agentnotrunningthreshold**|**int**|エージェントが実行されていない期間 (時間単位) です。この値を超過すると警告が生成されます。|  
|**timetoexpiration**|**int**|同期されていないサブスクリプションが失効するまでの期間 (時間単位) です。|  
|**expirationthreshold**|**int**|サブスクリプションが失効するまでの期間 (時間単位) です。この値を超過した場合は警告が生成されます。|  
|**last_distsync**|**datetime**|ディストリビューション エージェントが前回実行された日時。|  
|**distribution_agentname**|**sysname**|トランザクション パブリケーションに対するサブスクリプションに関するディストリビューション エージェント ジョブの名前です。|  
|**mergeagentname**|**sysname**|マージ パブリケーションへのサブスクリプションに関するマージ エージェント ジョブの名前です。|  
|**mergesubscriptionfriendlyname**|**sysname**|サブスクリプションに付けられた表示名です。|  
|**mergeagentlocation**|**sysname**|マージ エージェントが実行されるサーバーの名前です。|  
|**mergeconnectiontype**|**int**|マージ パブリケーションに対するサブスクリプションの同期時に使用される接続です。次のいずれかの値をとります。<br /><br /> **1** = ローカル エリア ネットワーク (LAN)<br /><br /> **2** = ダイヤルアップ ネットワーク接続<br /><br /> **3** = web 同期します。|  
|**mergePerformance**|**int**|サブスクリプションに対するすべての同期と比較した前回の同期のパフォーマンスです。前回の同期の配信速度を前回までのすべての配信速度の平均で割った値に基づいて算出されます。|  
|**mergerunspeed**|**float**|前回のサブスクリプションの同期の配信率です。|  
|**mergerunduration**|**int**|前回のサブスクリプションの同期の完了にかかった時間です。|  
|**monitorranking**|**int**|結果セットのサブスクリプションの並べ替えに使用される順位値。次のいずれかの値をとります。<br /><br /> トランザクション パブリケーションの場合 :<br /><br /> **60** = エラー<br /><br /> **56** = 警告: パフォーマンス クリティカル<br /><br /> **52** = 警告: まもなく期限切れまたは期限切れ<br /><br /> **50** = 警告: 初期化されていないサブスクリプション<br /><br /> **40** = コマンドの再試行に失敗しました<br /><br /> **30** = (成功) を実行していません。<br /><br /> **20** = 実行中 (開始、実行中、またはアイドル状態)<br /><br /> マージ パブリケーションの場合<br /><br /> **60** = エラー<br /><br /> **56** = 警告: パフォーマンス クリティカル<br /><br /> **54** = 警告: 長期マージ<br /><br /> **52** = 警告: 間もなく期限切れになりません。<br /><br /> **50** = 警告: 初期化されていないサブスクリプション<br /><br /> **40** = コマンドの再試行に失敗しました<br /><br /> **30** = 実行中 (開始、実行中、またはアイドル状態)<br /><br /> **20** = (成功) を実行していません。|  
|**distributionagentjobid**|**binary(16)**|トランザクション パブリケーションへのサブスクリプションに関するディストリビューション エージェント ジョブの ID です。|  
|**mergeagentjobid**|**binary(16)**|マージ パブリケーションへのサブスクリプションに関するマージ エージェント ジョブの ID です。|  
|**distributionagentid**|**int**|サブスクリプションに関するディストリビューション エージェント ジョブの ID です。|  
|**distributionagentprofileid**|**int**|ディストリビューション エージェントで使用されるエージェント プロファイルの ID です。|  
|**mergeagentid**|**int**|サブスクリプションに関するマージ エージェント ジョブの ID です。|  
|**mergeagentprofileid**|**int**|マージ エージェントで使用されるエージェント プロファイルの ID です。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_replmonitorhelpsubscription**はあらゆる種類のレプリケーションで使用します。  
  
 **sp_replmonitorhelpsubscription**の値によって決定されると、サブスクリプションの状態の重大度に基づく結果セットを並べ替えます*monitorranking*します。 たとえば、エラー状態のすべてのサブスクリプションの列は、警告状態のサブスクリプションの列よりも上に並べられます。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **db_owner**または**replmonitor** 、ディストリビューション データベースの固定データベース ロールが実行できる**sp_replmonitorhelpsubscription**します。  
  
## <a name="see-also"></a>参照  
 [Programmatically Monitor Replication (プログラムによるレプリケーションの監視)](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
