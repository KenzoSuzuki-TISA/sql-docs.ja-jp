---
title: sp_addmessage (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addmessage
- sp_addmessage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addmessage
ms.assetid: 54746d30-f944-40e5-a707-f2d9be0fb9eb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4b5ba2a19505d0d7a1493b997eda7d12f3a588f7
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52524106"
---
# <a name="spaddmessage-transact-sql"></a>sp_addmessage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスの新しいユーザー定義エラー メッセージを保存します。 使用して格納されているメッセージ**sp_addmessage**を使用して表示できます、 **sys.messages**カタログ ビューです。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addmessage [ @msgnum= ] msg_id , [ @severity= ] severity , [ @msgtext= ] 'msg'   
     [ , [ @lang= ] 'language' ]   
     [ , [ @with_log= ] { 'TRUE' | 'FALSE' } ]   
     [ , [ @replace= ] 'replace' ]   
```  
  
## <a name="arguments"></a>引数  
 [ **@msgnum****=** ] *msg_id*  
 メッセージの ID を指定します。 *msg_id*は**int**既定値は NULL です。 *msg_id*ユーザー定義エラー メッセージが 50,001 から 2,147, 483,647 までの整数を指定できます。 組み合わせた*msg_id*と*言語*一意である必要があります指定した言語の ID が既に存在する場合、エラーが返されます。  
  
 [ **@severity =** ]*severity*  
 エラーの重大度レベルを指定します。 *重大度*は**smallint**既定値は NULL です。 有効なレベルは 1 ～ 25 です。 重大度レベルの詳細については、「 [データベース エンジン エラーの重大度](../../relational-databases/errors-events/database-engine-error-severities.md)」を参照してください。  
  
 [  **@msgtext =** ] **'**_msg_**'**  
 エラー メッセージのテキストを指定します。 *msg*は**nvarchar (255)** 既定値は NULL です。  
  
 [  **@lang =** ] **'**_言語_**'**  
 このメッセージの言語を指定します。 *言語*は**sysname**既定値は NULL です。 複数の言語を同じサーバーにインストールできる*言語*各メッセージを記述する言語を指定します。 ときに*言語*は省略すると、言語が既定の言語のセッション。  
  
 [  **@with_log =** ] { **'** TRUE **'** | **'FALSE'** }  
 メッセージを、発生時に Windows のアプリケーション ログに書き込むかどうかを指定します。 **@with_log** **varchar (5)** 既定値は FALSE。 TRUE の場合は、エラーは常に Windows のアプリケーション ログに書き込まれます。 FALSE の場合、常に Windows のアプリケーション ログに書き込まれるわけではありませんが、エラーの発生状況によっては書き込まれることもあります。 メンバーのみ、 **sysadmin**サーバーの役割は、このオプションを使用できます。  
  
> [!NOTE]  
>  Windows のアプリケーション ログにメッセージを書き込む場合は、[!INCLUDE[ssDE](../../includes/ssde-md.md)]のエラー ログ ファイルにも同じ内容が書き込まれます。  
  
 [ **@replace** *=* ] **'**_置換_**'**  
 文字列として指定されている場合*置換*、既存のエラー メッセージが新しいメッセージ テキストと重大度レベルで上書きされます。 *置換*は**varchar (7)** 既定値は NULL です。 場合、このオプションを指定する必要があります*msg_id*既に存在します。 英語版のすべてのメッセージが同じであるその他のすべての言語の英語版のメッセージ重大度レベルが置き換えられます*msg_id*します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 英語以外のバージョンの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、米国 の英語以外のバージョンで、別の言語を使用してメッセージを追加するには、あらかじめ英語版のメッセージが存在している必要があります。 2 つのバージョンのメッセージの重大度は同じであることが必要です。  
  
 パラメーターが含まれたメッセージをローカライズする場合は、元のメッセージのパラメーターに相当するパラメーター番号を使用します。 各パラメーター番号の後に感嘆符 (!) を挿入します。  
  
|元のメッセージ|ローカライズされたメッセージ|  
|----------------------|-----------------------|  
|'元のメッセージ param 1: %s, <br /><br /> param 2: %d'|'ローカライズされたメッセージ param 1: %1!, <br /><br /> param 2: %2!'|  
  
 言語の構文に相違があるため、ローカライズされたメッセージのパラメーター番号は、元のメッセージと同じ順に出現しないことがあります。  
  
## <a name="permissions"></a>アクセス許可  
メンバーシップが必要です、 **sysadmin**または**serveradmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-defining-a-custom-message"></a>A. カスタム メッセージを定義する  
 次の例では、カスタム メッセージを**sys.messages**します。  
  
```  
USE master;  
GO  
EXEC sp_addmessage 50001, 16,   
   N'Percentage expects a value between 20 and 100.   
   Please reexecute with a more appropriate value.';  
GO  
```  
  
### <a name="b-adding-a-message-in-two-languages"></a>B. 2 種類の言語のメッセージを追加する  
 次の例では、まず英語のメッセージを追加し、英語し、フランス語で、同じメッセージを追加`.`  
  
```  
USE master;  
GO  
EXEC sp_addmessage @msgnum = 60000, @severity = 16,   
   @msgtext = N'The item named %s already exists in %s.',   
   @lang = 'us_english';  
  
EXEC sp_addmessage @msgnum = 60000, @severity = 16,   
   @msgtext = N'L''élément nommé %1! existe déjà dans %2!',   
   @lang = 'French';  
GO  
```  
  
### <a name="c-changing-the-order-of-parameters"></a>C. パラメーターの順序を変更する  
 次の例では、まず英語のメッセージを追加し、次にパラメーターの順序を変えてローカライズされたメッセージを追加します。  
  
```  
USE master;  
GO  
  
EXEC sp_addmessage   
    @msgnum = 60000,   
    @severity = 16,  
    @msgtext =   
        N'This is a test message with one numeric  
        parameter (%d), one string parameter (%s),   
        and another string parameter (%s).',  
    @lang = 'us_english';  
  
EXEC sp_addmessage   
    @msgnum = 60000,   
    @severity = 16,  
    @msgtext =   
        -- In the localized version of the message,  
        -- the parameter order has changed. The   
        -- string parameters are first and second  
        -- place in the message, and the numeric   
        -- parameter is third place.  
        N'Dies ist eine Testmeldung mit einem   
        Zeichenfolgenparameter (%3!),  
        einem weiteren Zeichenfolgenparameter (%2!),   
        und einem numerischen Parameter (%1!).',  
    @lang = 'German';  
GO    
  
-- Changing the session language to use the U.S. English  
-- version of the error message.  
SET LANGUAGE us_english;  
GO  
  
RAISERROR(60000,1,1,15,'param1','param2') -- error, severity, state,  
GO                                       -- parameters.  
  
-- Changing the session language to use the German  
-- version of the error message.  
SET LANGUAGE German;  
GO  
  
RAISERROR(60000,1,1,15,'param1','param2'); -- error, severity, state,   
GO                                       -- parameters.  
```  
  
## <a name="see-also"></a>参照  
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [sp_altermessage &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
