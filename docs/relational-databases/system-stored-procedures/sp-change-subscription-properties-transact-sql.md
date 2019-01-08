---
title: sp_change_subscription_properties (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_change_subscription_properties_TSQL
- sp_change_subscription_properties
helpviewer_keywords:
- sp_change_subscription_properties
ms.assetid: cf8137f9-f346-4aa1-ae35-91a2d3c16f17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 45aadf2eab3cad31bfc376de59e8cce25126533f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52785734"
---
# <a name="spchangesubscriptionproperties-transact-sql"></a>sp_change_subscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  プル サブスクリプションの情報を更新します。 このストアド プロシージャは、サブスクライバー側でサブスクリプション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_change_subscription_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @property = ] 'property'  
        , [ @value = ] 'value'  
    [ , [ @publication_type = ] publication_type ]  
```  
  
## <a name="arguments"></a>引数  
 [ **@publisher=**] **'***publisher***'**  
 パブリッシャーの名前です。 *パブリッシャー*は**sysname**、既定値はありません。  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 パブリッシャー データベースの名前です。 *publisher_db*は**sysname**、既定値はありません。  
  
 [ **@publication=**] **'***publication***'**  
 パブリケーションの名前です。 *パブリケーション*は**sysname**、既定値はありません。  
  
 [  **@property=**] **'***プロパティ***'**  
 変更するプロパティを指定します。 *プロパティ*は**sysname**します。  
  
 [  **@value=**] **'***値***'**  
 プロパティの新しい値を指定します。 *値*は**nvarchar (1000)**、既定値はありません。  
  
 [  **@publication_type =** ] *publication_type*  
 パブリケーションのレプリケーションの種類を指定します。 *publication_type*は**int**、これらの値のいずれかを指定できます。  
  
|値|パブリケーションの種類|  
|-----------|----------------------|  
|**0**|トランザクション|  
|**1**|スナップショット|  
|**2**|Merge|  
|NULL (既定値)|この場合、レプリケーションによってパブリケーションの種類が決まります。 このストアド プロシージャでは複数のテーブルを検索する必要があるため、このオプションを指定すると、パブリケーションの種類を直接指定したときに比べて動作が遅くなります。|  
  
 次の表に、アーティクルのプロパティと、それぞれの値を示します。  
  
|プロパティ|値|説明|  
|--------------|-----------|-----------------|  
|**alt_snapshot_folder**||スナップショットの代替フォルダーの場所を指定します。 NULL に設定すると、スナップショット ファイルはパブリッシャーで指定された既定の場所から取得されます。|  
|**distrib_job_login**||エージェントを実行する [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントのログイン。|  
|**distrib_job_password**||エージェントを実行する Windows アカウントのパスワード。|  
|**distributor_login**||ディストリビューター ログイン。|  
|**distributor_password**||ディストリビューター パスワード。|  
|**distributor_security_mode**|**1**|ディストリビューターに接続するときに Windows 認証を使用。|  
||**0**|ディストリビューターに接続するときに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用。|  
|**dts_package_name**||SQL Server 2000 データ変換サービス (DTS) パッケージの名前。 トランザクション パブリケーションまたはスナップショット パブリケーションの場合のみ、この値を指定できます。|  
|**dts_package_password**||パッケージのパスワードを指定します。 *dts_package_password*は**sysname**既定値は null の場合、変更せずに残すパスワード プロパティが指定します。<br /><br /> 注:DTS パッケージにはパスワードが必要です。<br /><br /> トランザクション パブリケーションまたはスナップショット パブリケーションの場合のみ、この値を指定できます。|  
|**dts_package_location**||DTS パッケージが格納されている場所です。 トランザクション パブリケーションまたはスナップショット パブリケーションの場合のみ、この値を指定できます。|  
|**dynamic_snapshot_location**||スナップショット ファイルが保存されるフォルダーへのパス。 マージ パブリケーションの場合のみ、この値を指定できます。|  
|**ftp_address**||これは旧バージョンとの互換性のためにだけ用意されています。|  
|**ftp_login**||これは旧バージョンとの互換性のためにだけ用意されています。|  
|**ftp_password**||これは旧バージョンとの互換性のためにだけ用意されています。|  
|**ftp_port**||これは旧バージョンとの互換性のためにだけ用意されています。|  
|**ホスト名**||パブリッシャーに接続するときに使用されるホスト名。|  
|**internet_login**||基本認証を使用して Web 同期をホストしている Web サーバーに接続するときにマージ エージェントが使用するログインです。|  
|**internet_password**||基本認証を使用して Web 同期をホストしている Web サーバーに、マージ エージェントが接続するときのパスワード。|  
|**internet_security_mode**|**1**|Web 同期に Windows 統合認証を使用。 基本認証を Web 認証と共に使用することをお勧めします。 詳しくは、「 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)」をご覧ください。|  
||**0**|Web 同期に基本認証を使用。<br /><br /> 注:Web 同期には、Web サーバーへの SSL 接続が必要です。|  
|**internet_timeout**||Web 同期要求が期限切れとなるまでの時間 (秒単位)。|  
|**internet_url**||Web 同期中にレプリケーション リスナーの位置を表す URL です。|  
|**merge_job_login**||エージェントを実行する Windows アカウントのログイン。|  
|**merge_job_password**||エージェントを実行する Windows アカウントのパスワード。|  
|**publisher_login**||パブリッシャーのログイン。 変更する*publisher_login*はマージ パブリケーションに対するサブスクリプションの場合のみ使用します。|  
|**publisher_password**||パブリッシャーのパスワード。 変更する*publisher_password*はマージ パブリケーションに対するサブスクリプションの場合のみ使用します。|  
|**publisher_security_mode**|**1**|パブリッシャーに接続するときに Windows 認証を使用。 変更する*publisher_security_mode*はマージ パブリケーションに対するサブスクリプションの場合のみ使用します。|  
||**0**|パブリッシャーに接続するときに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用。|  
|**@use_ftp**|**true**|標準のプロトコルの代わりに FTP を使用してスナップショットを取得。|  
||**false**|標準のプロトコルを使用してスナップショットを取得。|  
|**@use_web_sync**|**true**|Web 同期を有効にする。|  
||**false**|Web 同期を無効にする。|  
|**working_directory**||スナップショットのファイル転送でファイル転送プロトコル (FTP) を使用する場合、パブリケーションのデータとスキーマ ファイルを一時的に保存するために使用する作業ディレクトリの名前。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_change_subscription_properties**はあらゆる種類のレプリケーションで使用します。  
  
 **sp_change_subscription_properties**プル サブスクリプションのために使用します。  
  
 Oracle パブリッシャーの場合の値の*publisher_db*は、Oracle では、サーバーのインスタンスごとに 1 つのデータベースのみが許可されるために無視されます。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_change_subscription_properties**します。  
  
## <a name="see-also"></a>参照  
 [プル サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [sp_addmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_addmergepullsubscription_agent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_addpullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_addpullsubscription_agent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
