---
title: sp_procoption (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_procoption
- sp_procoption_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_procoption
ms.assetid: 6f0221bd-70b4-4b04-b15d-722235aceb3c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fcde4fd9439862dd88bdb1ff8c9eb40ff85ce0d4
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/18/2018
ms.locfileid: "53590426"
---
# <a name="spprocoption-transact-sql"></a>sp_procoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ストアド プロシージャの自動実行を設定または解除します。 ストアド プロシージャに設定されている自動実行の実行時間のすべてのインスタンスを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が開始します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_procoption [ @ProcName = ] 'procedure'   
    , [ @OptionName = ] 'option'   
    , [ @OptionValue = ] 'value'   
```  
  
## <a name="arguments"></a>引数  
 [  **@ProcName =** ] **'**_プロシージャ_**'**  
 オプションを設定する対象のプロシージャの名前です。 *プロシージャ*は**nvarchar (776)**、既定値はありません。  
  
 [  **@OptionName =** ] **'**_オプション_**'**  
 設定するオプションの名前です。 値だけ*オプション*は**スタートアップ**します。  
  
 [  **@OptionValue =** ] **'**_値_**'**  
 オプションを設定するかどうか (**true**または**で**) かオフ (**false**または**オフ**)。 *値*は**varchar (12)**、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 成功した場合は 0 を、失敗した場合はエラー番号をそれぞれ返します。  
  
## <a name="remarks"></a>コメント  
 スタートアップ プロシージャがである必要があります、**マスター**データベースし、入力または出力パラメーターを含めることはできません。 ストアド プロシージャの実行は、すべてのデータベースが復旧され、スタートアップ時に "復元が完了しました" というメッセージがログに記録されると開始されます。  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例は、プロシージャの自動実行を設定します。  
  
```  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionName = ] 'startup'   
    , @OptionValue = 'on';   
```  
  
 次の例は、プロシージャの自動実行を停止します。  
  
```  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionValue = 'off';   
```  
  
## <a name="see-also"></a>参照  
 [ストアド プロシージャの実行](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)  
  
  
