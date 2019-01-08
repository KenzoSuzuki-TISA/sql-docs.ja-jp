---
title: sp_helpsubscription_properties (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscription_properties
- sp_helpsubscription_properties_TSQL
helpviewer_keywords:
- sp_helpsubscription_properties
ms.assetid: 7a76a645-97eb-47ac-b3ea-e2d75012cbed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c81f2878c5573174b7f50f15f2ef2adf9329021a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52808284"
---
# <a name="sphelpsubscriptionproperties-transact-sql"></a>sp_helpsubscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  セキュリティ情報を取得、 [MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)テーブル。 このストアド プロシージャはサブスクライバー側で実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpsubscription_properties [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db =] 'publisher_db' ]   
    [ , [ @publication =] 'publication' ]  
    [ , [ @publication_type = ] publication_type ]   
```  
  
## <a name="arguments"></a>引数  
 [ **@publisher=**] **'***publisher***'**  
 パブリッシャーの名前です。 *パブリッシャー*は**sysname**、既定値は**%**、すべてのパブリッシャーに関する情報を返します。  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 パブリッシャー データベースの名前です。 *publisher_db*は**sysname**、既定値は**%**、すべてのパブリッシャー データベースに関する情報を返します。  
  
 [ **@publication=**] **'***publication***'**  
 パブリケーションの名前です。 *パブリケーション*は**sysname**、既定値は**%**、すべてのパブリケーションに関する情報を返します。  
  
 [  **@publication_type=**] *publication_type*  
 パブリケーションの種類です。*publication_type*は**int**、既定値は NULL です。 指定した場合、 *publication_type*値は次のいずれかを指定する必要があります。  
  
|値|説明|  
|-----------|-----------------|  
|**0**|トランザクション パブリケーション|  
|**1**|スナップショット パブリケーション|  
|**2**|マージ パブリケーション|  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**パブリッシャー**|**sysname**|パブリッシャーの名前。|  
|**publisher_db**|**sysname**|パブリッシャー データベースの名前です。|  
|**パブリケーション**|**sysname**|パブリケーションの名前。|  
|**publication_type**|**int**|パブリケーションの種類です。<br /><br /> **0** = トランザクション<br /><br /> **1** = スナップショット<br /><br /> **2**マージを =|  
|**publisher_login**|**sysname**|パブリッシャーで使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証用のログイン ID。|  
|**publisher_password**|**nvarchar (524)**|パブリッシャーで使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証用の (暗号化されている) パスワードです。|  
|**publisher_security_mode**|**int**|パブリッシャーで使用されているセキュリティ モードです。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証<br /><br /> **1** = Windows 認証|  
|**ディストリビューター**|**sysname**|ディストリビューターの名前。|  
|**distributor_login**|**sysname**|ディストリビューター ログイン。|  
|**distributor_password**|**nvarchar (524)**|暗号化されたディストリビューター パスワードです。|  
|**distributor_security_mode**|**int**|ディストリビューターで使用されているセキュリティ モードです。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証<br /><br /> **1** = Windows 認証|  
|**ftp_address**|**sysname**|これは旧バージョンとの互換性のためにだけ用意されています。 ディストリビューター用ファイル転送プロトコル (FTP) サービスのネットワーク アドレス。|  
|**ftp_port**|**int**|これは旧バージョンとの互換性のためにだけ用意されています。 ディストリビューター用 FTP サービスのポート番号。|  
|**ftp_login**|**sysname**|これは旧バージョンとの互換性のためにだけ用意されています。 FTP サービスへの接続に使用されるユーザー名です。|  
|**ftp_password**|**nvarchar (524)**|これは旧バージョンとの互換性のためにだけ用意されています。 FTP サービスへの接続に使用されるユーザー パスワードです。|  
|**alt_snapshot_folder**|**nvarchar (255)**|スナップショットの代替フォルダーの場所を指定します。|  
|**working_directory**|**nvarchar (255)**|データ ファイルとスキーマ ファイルを保存するために使用する作業ディレクトリ名です。|  
|**@use_ftp**|**bit**|標準のプロトコルの代わりに FTP を使用してスナップショットを取得します。 場合**1**FTP を使用します。|  
|**dts_package_name**|**sysame**|データ変換サービス (DTS) パッケージの名前。|  
|**dts_package_password**|**nvarchar (524)**|パッケージのパスワード (ある場合) を指定します。|  
|**dts_package_location**|**int**|DTS パッケージが格納されている場所です。<br /><br /> **0**パッケージの場所は、ディストリビューター側では。<br /><br /> **1**パッケージの場所はサブスクライバーです。|  
|**offload_agent**|**bit**|エージェントをリモートから起動できるかどうかを指定します。 場合**0**エージェントをリモートでアクティブにできません。|  
|**offload_server**|**sysname**|リモートからのアクティブ化に使用するサーバーのネットワーク名。|  
|**dynamic_snapshot_location**|**nvarchar (255)**|スナップショット ファイルが保存されるフォルダーへのパス。|  
|**@use_web_sync**|**bit**|HTTPS 経由でサブスクリプションを同期することができるかどうかの値が指定**1**この機能が有効になっていることを意味します。|  
|**internet_url**|**nvarchar(260)**|Web 同期中にレプリケーション リスナーの位置を表す URL です。|  
|**internet_login**|**nvarchar(128)**|基本認証を使用して Web 同期をホストしている Web サーバーに接続するときにマージ エージェントが使用するログインです。|  
|**internet_password**|**nvarchar (524)**|基本認証を使用して Web 同期をホストしている Web サーバーに接続するときにマージ エージェントが使用するログインのパスワードです。|  
|**internet_security_mode**|**int**|値が、Web 同期をホストしている Web サーバーに接続するときに使用する認証モード**1** 、Windows 認証を示し、値の**0**基本認証を意味します。|  
|**internet_timeout**|**int**|Web 同期要求が期限切れとなるまでの時間 (秒単位)。|  
|**ホスト名**|**nvarchar(128)**|この関数が WHERE 句のパラメーター化された行フィルターで使用される場合の HOST_NAME() の値を指定します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helpsubscription_properties**はスナップショット レプリケーション、トランザクション レプリケーション、およびマージ レプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_helpsubscription_properties**します。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
