---
title: sp_addsubscriber (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsubscriber
- sp_addsubscriber_TSQL
helpviewer_keywords:
- sp_addsubscriber
ms.assetid: b8a584ea-2a26-4936-965b-b84f026e39c0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ad13c4904270d3162dac8791b7724533e8da6656
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211751"
---
# <a name="spaddsubscriber-transact-sql"></a>sp_addsubscriber (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  パブリッシャーに新しいサブスクライバーを追加し、サブスクライバーがパブリケーションを受け取れるようにします。 このストアド プロシージャは、スナップショット パブリケーションとトランザクション パブリケーションの場合はパブリッシャー側でパブリケーション データベースについて実行され、リモート ディストリビューターを使用するマージ パブリケーションの場合はディストリビューター側で実行されます。  
  
> [!IMPORTANT]  
>  このストアド プロシージャの使用は非推奨とされます。 パブリッシャー側でサブスクライバーを明示的に登録する必要はなくなりました。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addsubscriber [ @subscriber = ] 'subscriber'  
    [ , [ @type = ] type ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @commit_batch_size = ] commit_batch_size ]  
    [ , [ @status_batch_size = ] status_batch_size ]  
    [ , [ @flush_frequency = ] flush_frequency ]  
    [ , [ @frequency_type = ] frequency_type ]  
    [ , [ @frequency_interval = ] frequency_interval ]  
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday = ] frequency_subday ]  
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]  
    [ , [ @active_start_date = ] active_start_date ]  
    [ , [ @active_end_date = ] active_end_date ]  
    [ , [ @description = ] 'description' ]  
    [ , [ @security_mode = ] security_mode ]  
    [ , [ @encrypted_password = ] encrypted_password ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
 [  **@subscriber=**] **'***サブスクライバー***'**  
 有効なサブスクライバーとして、このサーバーのパブリケーションに追加するサーバーの名前を指定します。 *サブスクライバー*は**sysname**、既定値はありません。  
  
 [  **@type=**]*型*  
 サブスクライバーの種類を指定します。 *型*は**tinyint**、これらの値のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**0** (既定値)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバー|  
|**1**|ODBC データ ソース サーバー|  
|**2**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet データベース|  
|**3**|OLE DB プロバイダー|  
  
 [  **@login=**] **'***ログイン***'**  
 ログイン id[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。 *login* のデータ型は **sysname** で、既定値は NULL です。  
  
> [!NOTE]  
>  このパラメーターは、スクリプトの下位互換性を確保するために用意されているものであり、非推奨とされます。 実行するときに、サブスクリプションごとにプロパティが指定ようになりました[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)します。 値を指定した場合、その値はサブスクライバーでのサブスクリプションの作成時に既定値として使用され、警告メッセージが返されます。  
  
 [  **@password=**] **'***パスワード***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のパスワードを指定します。 *パスワード*は**nvarchar (524)**、既定値は NULL です。  
  
> [!IMPORTANT]  
>  空白のパスワードは使用しないでください。 強力なパスワードを使用してください。  
  
> [!NOTE]  
>  このパラメーターは、スクリプトの下位互換性を確保するために用意されているものであり、非推奨とされます。 実行するときに、サブスクリプションごとにプロパティが指定ようになりました[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)します。 値を指定した場合、その値はサブスクライバーでのサブスクリプションの作成時に既定値として使用され、警告メッセージが返されます。  
  
 [  **@commit_batch_size=**] *commit_batch_size*  
 このパラメーターは、スクリプトの下位互換性を確保するために用意されているものであり、非推奨とされます。  
  
> [!NOTE]  
>  値を指定した場合、その値はサブスクライバーでのサブスクリプションの作成時に既定値として使用され、警告メッセージが返されます。  
  
 [  **@status_batch_size=**] *status_batch_size*  
 このパラメーターは、スクリプトの下位互換性を確保するために用意されているものであり、非推奨とされます。  
  
> [!NOTE]  
>  値を指定した場合、その値はサブスクライバーでのサブスクリプションの作成時に既定値として使用され、警告メッセージが返されます。  
  
 [  **@flush_frequency=**] *flush_frequency*  
 このパラメーターは、スクリプトの下位互換性を確保するために用意されているものであり、非推奨とされます。  
  
> [!NOTE]  
>  値を指定した場合、その値はサブスクライバーでのサブスクリプションの作成時に既定値として使用され、警告メッセージが返されます。  
  
 [  **@frequency_type=**] *frequency_type*  
 レプリケーション エージェントをスケジュールに組み込む頻度を指定します。 *frequency_type*は**int**、これらの値のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|指定日時|  
|**2**|[要求時]|  
|**4**|毎日。|  
|**8**|毎週。|  
|**16**|毎月。|  
|**32**|月単位|  
|**64** (既定値)|自動的に起動|  
|**128**|定期的|  
  
> [!NOTE]  
>  このパラメーターは、スクリプトの下位互換性を確保するために用意されているものであり、非推奨とされます。 実行するときに、サブスクリプションごとにプロパティが指定ようになりました[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)します。 値を指定した場合、その値はサブスクライバーでのサブスクリプションの作成時に既定値として使用され、警告メッセージが返されます。  
  
 [**@frequency_interval=** ] *frequency_interval*  
 設定した頻度に適用される値は、 *frequency_type*します。 *frequency_interval*は**int**、既定値は 1 です。  
  
> [!NOTE]  
>  このパラメーターは、スクリプトの下位互換性を確保するために用意されているものであり、非推奨とされます。 実行するときに、サブスクリプションごとにプロパティが指定ようになりました[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)します。 値を指定した場合、その値はサブスクライバーでのサブスクリプションの作成時に既定値として使用され、警告メッセージが返されます。  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 レプリケーション エージェントを実行する日付を指定します。 このパラメーターが使用されるときに*frequency_type*に設定されている**32** (月単位)。 *frequency_relative_interval*は**int**、これらの値のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**1** (既定値)|First|  
|**2**|第 2 週|  
|**4**|第 3 週|  
|**8**|第 4 週|  
|**16**|Last|  
  
> [!NOTE]  
>  このパラメーターは、スクリプトの下位互換性を確保するために用意されているものであり、非推奨とされます。 実行するときに、サブスクリプションごとにプロパティが指定ようになりました[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)します。 値を指定した場合、その値はサブスクライバーでのサブスクリプションの作成時に既定値として使用され、警告メッセージが返されます。  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 使用される定期実行係数*frequency_type*します。 *frequency_recurrence_factor*は**int**、既定値は**0**します。  
  
> [!NOTE]  
>  このパラメーターは、スクリプトの下位互換性を確保するために用意されているものであり、非推奨とされます。 実行するときに、サブスクリプションごとにプロパティが指定ようになりました[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)します。 値を指定した場合、その値はサブスクライバーでのサブスクリプションの作成時に既定値として使用され、警告メッセージが返されます。  
  
 [  **@frequency_subday=**] *frequency_subday*  
 定義した期間にスケジュールを組み直す頻度を指定します。 *frequency_subday*は**int**、これらの値のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|1 回。|  
|**2**|第 2 週|  
|**4** (既定値)|Minute|  
|**8**|Hour|  
  
> [!NOTE]  
>  このパラメーターは、スクリプトの下位互換性を確保するために用意されているものであり、非推奨とされます。 実行するときに、サブスクリプションごとにプロパティが指定ようになりました[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)します。 値を指定した場合、その値はサブスクライバーでのサブスクリプションの作成時に既定値として使用され、警告メッセージが返されます。  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 間隔は、 *frequency_subday*します。 *frequency_subday_interval*は**int**、既定値は**5**します。  
  
> [!NOTE]  
>  このパラメーターは、スクリプトの下位互換性を確保するために用意されているものであり、非推奨とされます。 実行するときに、サブスクリプションごとにプロパティが指定ようになりました[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)します。 値を指定した場合、その値はサブスクライバーでのサブスクリプションの作成時に既定値として使用され、警告メッセージが返されます。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 レプリケーション エージェントを最初にスケジュール設定する時刻を HHMMSS 形式で指定します。 *active_start_time_of_day*は**int**、既定値は**0**します。  
  
> [!NOTE]  
>  このパラメーターは、スクリプトの下位互換性を確保するために用意されているものであり、非推奨とされます。 実行するときに、サブスクリプションごとにプロパティが指定ようになりました[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)します。 値を指定した場合、その値はサブスクライバーでのサブスクリプションの作成時に既定値として使用され、警告メッセージが返されます。  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 レプリケーション エージェントのスケジュール設定を停止する時刻を HHMMSS 形式で指定します。 *active_end_time_of_day*は**int**既定値は 235959、午後 11時 59分: 59 を意味 24 時間制です。  
  
> [!NOTE]  
>  このパラメーターは、スクリプトの下位互換性を確保するために用意されているものであり、非推奨とされます。 実行するときに、サブスクリプションごとにプロパティが指定ようになりました[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)します。 値を指定した場合、その値はサブスクライバーでのサブスクリプションの作成時に既定値として使用され、警告メッセージが返されます。  
  
 [  **@active_start_date=**] *active_start_date*  
 レプリケーション エージェントを最初にスケジュール設定する日付を YYYYMMDD 形式で指定します。 *active_start_date*は**int**、既定値は 0。  
  
> [!NOTE]  
>  このパラメーターは、スクリプトの下位互換性を確保するために用意されているものであり、非推奨とされます。 実行するときに、サブスクリプションごとにプロパティが指定ようになりました[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)します。 値を指定した場合、その値はサブスクライバーでのサブスクリプションの作成時に既定値として使用され、警告メッセージが返されます。  
  
 [  **@active_end_date=**] *active_end_date*  
 レプリケーション エージェントのスケジュール設定を停止する日付を YYYYMMDD 形式で指定します。 *active_end_date*は**int**、既定値は 99991231、9999 年 12 月 31 日。  
  
> [!NOTE]  
>  このパラメーターは、スクリプトの下位互換性を確保するために用意されているものであり、非推奨とされます。 実行するときに、サブスクリプションごとにプロパティが指定ようになりました[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)します。 値を指定した場合、その値はサブスクライバーでのサブスクリプションの作成時に既定値として使用され、警告メッセージが返されます。  
  
 [  **@description=**] **'***説明***'**  
 サブスクライバーのテキスト形式の説明を指定します。 *説明*は**nvarchar (255)**、既定値は NULL です。  
  
 [  **@security_mode=**] *security_mode*  
 実装されているセキュリティ モードを指定します。 *security_mode*は**int**、既定値は 1 です。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。 **1** Windows 認証を指定します。  
  
> [!NOTE]  
>  このパラメーターは、スクリプトの下位互換性を確保するために用意されているものであり、非推奨とされます。 実行するときに、サブスクリプションごとにプロパティが指定ようになりました[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)します。 値を指定した場合、その値はサブスクライバーでのサブスクリプションの作成時に既定値として使用され、警告メッセージが返されます。  
  
 [  **@encrypted_password=**] *encrypted_password*  
 このパラメーターは非推奨し、設定のみに、旧バージョンとの互換性のため提供*encrypted_password*任意の値が**0**エラーが発生します。  
  
 [ **@publisher**=] **'***パブリッシャー***'**  
 以外を指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーです。 *パブリッシャー*は**sysname**、既定値は NULL です。  
  
> [!NOTE]  
>  *パブリッシャー*から発行するときに使用されません、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーです。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_addsubscriber**はスナップショット レプリケーション、トランザクション レプリケーション、およびマージ レプリケーションで使用します。  
  
 **sp_addsubscriber**サブスクライバーのみマージ パブリケーションへの匿名サブスクリプションを持つ場合は必要ありません。  
  
 **sp_addsubscriber**書き込む、 [MSsubscriber_info](../../relational-databases/system-tables/mssubscriber-info-transact-sql.md)テーブルに、**配布**データベース。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールが実行できる**sp_addsubscriber**します。  
  
## <a name="see-also"></a>参照  
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [sp_changesubscriber &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)  
  
  
