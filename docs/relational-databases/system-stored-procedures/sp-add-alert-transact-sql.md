---
title: sp_add_alert (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_alert
- sp_add_alert_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_alert
ms.assetid: d9b41853-e22d-4813-a79f-57efb4511f09
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4193e073f4ad4c52d6b2c7f6b82c6246107e85a1
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2019
ms.locfileid: "54127072"
---
# <a name="spaddalert-transact-sql"></a>sp_add_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  警告を作成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_add_alert [ @name = ] 'name'   
     [ , [ @message_id = ] message_id ]   
     [ , [ @severity = ] severity ]   
     [ , [ @enabled = ] enabled ]  
     [ , [ @delay_between_responses = ] delay_between_responses ]   
     [ , [ @notification_message = ] 'notification_message' ]   
     [ , [ @include_event_description_in = ] include_event_description_in ]   
     [ , [ @database_name = ] 'database' ]   
     [ , [ @event_description_keyword = ] 'event_description_keyword_pattern' ]   
     [ , { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ]   
     [ , [ @raise_snmp_trap = ] raise_snmp_trap ]   
     [ , [ @performance_condition = ] 'performance_condition' ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @wmi_namespace = ] 'wmi_namespace' ]  
     [ , [ @wmi_query = ] 'wmi_query' ]  
```  
  
## <a name="arguments"></a>引数  
 [  **@name =** ] **'**_名前_**'**  
 警告の名前を指定します。 この名前は、警告に対する応答として送信される電子メールまたはポケットベルのメッセージに表示されます。 一意であり、割合を含めることができます (**%**) 文字。 *名前*は**sysname**、既定値はありません。  
  
 [ **@message_id =** ] *message_id*  
 警告を定義するメッセージ エラー番号を指定します。 (通常、エラー番号に対応して、 **sysmessages**テーブルです)。*message_id*は**int**、既定値は**0**します。 場合*重大度*、警告を定義するために使用*message_id*あります**0**または NULL。  
  
> [!NOTE]  
>  のみ**sysmessages** Microsoft Windows アプリケーション ログに書き込まれたエラーが原因で、アラートを送信します。  
  
 [ **@severity =** ] *severity*  
 重大度レベル (から**1**を通じて**25**)、アラートを定義します。 すべて[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にメッセージが格納されている、 **sysmessages**テーブルに送信される、[!INCLUDE[msCoName](../../includes/msconame-md.md)]指定された重大度を持つ Windows アプリケーション ログと警告を送信します。 *重大度*は**int**、既定値は 0。 場合*message_id* 、警告を定義するために使用*重大度*あります**0**します。  
  
 [ **@enabled =** ] *enabled*  
 警告の現在の状態を示します。 *有効になっている*は**tinyint**、既定値は 1 (有効)。 場合**0**アラートが有効でないとは発生しません。  
  
 [ **@delay_between_responses =** ] *delay_between_responses*  
 警告に対する応答から次の応答までの待機時間を秒単位で指定します。 *delay_between_responses*は**int**、既定値は**0**、つまりが発生するたび、アラートの応答) 間の待機中ではありません。 応答は、次のいずれかまたは両方の方法で行うことができます。  
  
-   1 つ以上の通知を電子メールまたはポケットベルで送信する。  
  
-   ジョブを実行する。  
  
 この値を設定すると、たとえば短時間に繰り返し警告が発生したとき、不要な電子メール メッセージの送信を防止できます。  
  
 [  **@notification_message =** ] **'**_このパラメーター_**'**  
 電子メールの一部としてオペレーターに送信される追加の省略可能なメッセージ**net send**、またはポケットベル通知します。 *このパラメーター*は**nvarchar (512)**、既定値は NULL です。 指定する*このパラメーター*は書き加えるなど特別な注意を追加するために便利です。  
  
 [  **@include_event_description_in =** ] *include_event_description_in*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラーに関する説明を通知メッセージに含めるかどうかを指定します。 *include_event_description_in*は**tinyint**、既定値は**5** (電子メールと**net send**)、およびは 1 つまたはと共にこれらの値の詳細は、**または**論理演算子です。  
  
> [!IMPORTANT]
>  今後のバージョンの **では、** エージェントからポケットベル オプションと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] net send [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オプションが削除される予定です。 新しい開発作業では、これらの機能の使用を避け、現在これらの機能を使用しているアプリケーションは修正するようにしてください。  
  
|値|説明|  
|-----------|-----------------|  
|**0**|なし|  
|**1**|[電子メール]|  
|**2**|[ポケットベル]|  
|**4**|**net send**|  
  
 [  **@database_name =** ] **'**_データベース_**'**  
 どのデータベースでエラーが発生したときに警告を起動するかを指定します。 場合*データベース*が指定されていない、エラーの発生場所に関係なく警告が発生します。 *データベース*は**sysname**します。 角かっこ ([ ]) で囲まれた名前は使用できません。 既定値は NULL になります。  
  
 [  **@event_description_keyword =** ] **'**_event_description_keyword_pattern_**'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラーの説明に、どのような文字のシーケンスが含まれている必要があるかを指定します。 [!INCLUDE[tsql](../../includes/tsql-md.md)] LIKE 式のパターン検索文字を使用できます。 *event_description_keyword_pattern*は**nvarchar (100)**、既定値は NULL です。 このパラメーターはオブジェクト名をフィルター処理するために役立ちます (たとえば、 **%customer_table%**)。  
  
 [ **@job_id =** ] *job_id*  
 対象となる警告に対する応答として実行するジョブのジョブ ID 番号を指定します。 *job_id*は**uniqueidentifier**、既定値は NULL です。  
  
 [  **@job_name =** ] **'**_job_name_**'**  
 この警告への応答として実行するジョブの名前を指定します。 *job_name*は**sysname**、既定値は NULL です。  
  
> [!NOTE]  
>  いずれか*job_id*または*job_name*指定する必要がありますが、両方を指定することはできません。  
  
 [ **@raise_snmp_trap =** ] *raise_snmp_trap*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version 7.0 では実装されていません。 *raise_snmp_trap*は**tinyint**、既定値は 0。  
  
 [  **@performance_condition =** ] **'**_performance_condition_**'**  
 形式で表される値は、'*itemcomparatorvalue*'。 *performance_condition*は**nvarchar (512)** 既定値は null の場合、これらの要素で構成されています。  
  
|形式の要素|説明|  
|--------------------|-----------------|  
|*アイテム*|パフォーマンス オブジェクト、パフォーマンス カウンター、またはカウンターの名前付きインスタンス。|  
|*比較演算子*|演算子 >、<、または = のいずれか。|  
|*[値]*|カウンターの数値。|  
  
 [  **@category_name =** ] **'**_カテゴリ_**'**  
 警告カテゴリの名前を指定します。 *カテゴリ*は**sysname**、既定値は NULL です。  
  
 [ **@wmi_namespace**=] **'**_wmi_namespace_**'**  
 イベントのクエリに対する WMI 名前空間を指定します。 *wmi_namespace*は**sysname**、既定値は NULL です。 サポートされるのはローカル サーバーの名前空間だけです。  
  
 [ **@wmi_query**=] **'**_wmi_query_**'**  
 警告に対する WMI イベントを指定するクエリを指定します。 *wmi_query*は**nvarchar (512)**、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 **sp_add_alert**から実行する必要があります、 **msdb**データベース。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアプリケーションで生成されたエラーやメッセージが Windows のアプリケーション ログに送られます。したがって、警告を起動できるのは次の場合です。  
  
-   重大度が 19 以上**sys.messages**エラー  
  
-   WITH LOG 構文で RAISERROR ステートメントが呼び出された場合。  
  
-   すべて**sys.messages**エラーは、変更またはを使用して作成**sp_altermessage**  
  
-   すべてのイベントを使用してログに記録**xp_logevent**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、警告システム全体を簡単に管理できるグラフィカルなツールです。警告の基本構成を設定するには、SQL Server Management Studio を使用することをお勧めします。  
  
 警告が正常に動作しないときは、次のことを確認してください。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのサービスが実行されていること。  
  
-   Windows アプリケーション ログにイベントが表示されること。  
  
-   警告が有効になっていること。  
  
-   **xp_logevent** で生成されたイベントは master データベースで発生します。 このため、 **xp_logevent** では、警告の **@database_name** が **'master'** または NULL になっていないと、警告が起動されません。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sp_add_alert** を実行できるのは、 **sysadmin**固定サーバー ロールのメンバーだけです。  
  
## <a name="examples"></a>使用例  
 次の例では、警告発生時にジョブ `Back up the AdventureWorks2012 Database` を実行する Test Alert という警告を追加します。  
  
> [!NOTE]  
>  この例では、メッセージ 55001 と、ジョブ `Back up the AdventureWorks2012 Database` が既に存在することを前提としています。 この例は、説明の目的でのみが表示されます。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_alert  
    @name = N'Test Alert',  
    @message_id = 55001,   
   @severity = 0,   
   @notification_message = N'Error 55001 has occurred. The database will be backed up...',   
   @job_name = N'Back up the AdventureWorks2012 Database' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_notification &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_altermessage &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_delete_alert &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-alert-transact-sql.md)   
 [sp_help_alert &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [sp_update_alert &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
