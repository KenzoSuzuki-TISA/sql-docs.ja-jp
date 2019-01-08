---
title: sp_helpdynamicsnapshot_job (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdynamicsnapshot_TSQL
- sp_helpdynamicsnapshot_job_TSQL
- job_TSQL
- helpdynamicsnapshot
- job
- sp_helpdynamicsnapshot
- sp_helpdynamicsnapshot_job
- helpdynamicsnapshot_TSQL
helpviewer_keywords:
- sp_helpdynamicsnapshot_job
ms.assetid: d6dfdf26-f874-495f-a8a6-8780699646d7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6e31562dcec495013b96dd772db2ae85c7702796
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52783284"
---
# <a name="sphelpdynamicsnapshotjob-transact-sql"></a>sp_helpdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  フィルター処理されたデータ スナップショットを生成するエージェント ジョブに関する情報を返します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpdynamicsnapshot_job [ [ @publication = ] 'publication' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
```  
  
## <a name="arguments"></a>引数  
 [ **@publication =** ] **'***publication***'**  
 パブリケーションの名前です。 *パブリケーション*は**sysname**、既定値は**%**、指定された一致するすべてのフィルター選択されたデータ スナップショット ジョブに関する情報を返します*dynamic_snapshot_jobid*と*dynamic_snapshot_jobname*すべてのパブリケーション。  
  
 [ **@dynamic_snapshot_jobname =** ] **'***dynamic_snapshot_jobname***'**  
 フィルター選択されたデータ スナップショット ジョブの名前を指定します。 *dynamic_snapshot_jobname*は**sysname**、既定値は**%**'、パブリケーションの指定したすべての動的ジョブが返されます*dynamic_snapshot_jobid*します。 ジョブの作成時にジョブ名が明示的に指定されなかった場合、ジョブ名は次の形式になります。  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
 [ **@dynamic_snapshot_jobid =** ] **'***dynamic_snapshot_jobid***'**  
 フィルター選択されたデータ スナップショット ジョブの識別子を指定します。 *dynamic_snapshot_jobid*は**uniqueidentifier**、既定値は NULL を指定された一致するすべてのスナップショット ジョブが返されます*dynamic_snapshot_jobname*します。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|フィルター処理されたデータ スナップショット ジョブの識別子。|  
|**job_name**|**sysname**|フィルター処理されたスナップショット ジョブの名前。|  
|**job_id**|**uniqueidentifier**|識別、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ディストリビューターでエージェント ジョブ。|  
|**dynamic_filter_login**|**sysname**|評価するために使用される値、 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)でパラメーター化された行フィルターがパブリケーションに対して定義されている関数。|  
|**dynamic_filter_hostname**|**sysname**|評価するために使用される値、 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)でパラメーター化された行フィルターがパブリケーションに対して定義されている関数。|  
|**dynamic_snapshot_location**|**nvarchar (255)**|パラメーター化された行フィルターを使用する場合、スナップショット ファイルの読み取り元フォルダーへのパス。|  
|**frequency_type**|**int**|スケジュールに組み込まれているエージェントの実行の頻度。次のいずれかの値になります。<br /><br /> **1** = 1 回<br /><br /> **2** = 要求時<br /><br /> **4** = 毎日<br /><br /> **8** = 毎週<br /><br /> **16**毎月を =<br /><br /> **32** = 月単位<br /><br /> **64** = 自動開始<br /><br /> **128** = 定期的|  
|**frequency_interval**|**int**|エージェントの実行日。次のいずれかの値になります。<br /><br /> **1**日曜日を =<br /><br /> **2** = 月曜日<br /><br /> **3** = 火曜日<br /><br /> **4** = 水曜日<br /><br /> **5** = 木曜日<br /><br /> **6** = 金曜日<br /><br /> **7** = 土曜日<br /><br /> **8** = 日<br /><br /> **9** = 平日<br /><br /> **10**週末の曜日を =|  
|**frequency_subday_type**|**int**|エージェントを実行ときにどのくらいの頻度を定義する型*frequency_type*は**4** (毎日)、これらの値のいずれかを指定できます。<br /><br /> **1** = 指定した時刻<br /><br /> **2**秒を =<br /><br /> **4**分を =<br /><br /> **8**時間を =|  
|**frequency_subday_interval**|**int**|間隔数*frequency_subday_type*エージェントのスケジュールされた実行の間で発生します。|  
|**frequency_relative_interval**|**int**|指定された月にエージェントを実行する週と*frequency_type*は**32** (月単位)、これらの値のいずれかを指定できます。<br /><br /> **1**最初を =<br /><br /> **2**秒を =<br /><br /> **4** = サード<br /><br /> **8**第 4 を =<br /><br /> **16**最後を =|  
|**frequency_recurrence_factor**|**int**|週または月を単位とした、エージェントの予定実行間隔。|  
|**active_start_date**|**int**|エージェントの最初の実行予定日。日付の形式は YYYYMMDD です。|  
|**active_end_date**|**int**|エージェントの最後の実行予定日。日付の形式は YYYYMMDD です。|  
|**active_start_time**|**int**|エージェントの最初の実行予定時刻。時刻の形式は HHMMSS です。|  
|**active_end_time**|**int**|エージェントの最後の実行予定時刻。時刻の形式は HHMMSS です。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helpdynamicsnapshot_job**はマージ レプリケーションで使用します。  
  
 すべて既定のパラメーター値を使用する場合は、パブリケーション データベース全体が対象となり、すべてのパーティション データ スナップショット ジョブに関する情報が返されます。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロール、 **db_owner** 、パブリケーションが実行できるは、データベース ロール、およびパブリケーション アクセス リストを固定**sp_helpdynamicsnapshot_job**.  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
