---
title: sp_cursor (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_TSQL
- sp_cursor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor
ms.assetid: 41ade0ca-5f11-469d-bd4d-c8302ccd93b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e3277e64e4c4e04e270298d3532ebc0c2b1f93c5
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210521"
---
# <a name="spcursor-transact-sql"></a>sp_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  位置指定更新を要求します。 このプロシージャは、カーソルのフェッチ バッファー内にある 1 つ以上の行に対して操作を実行します。 sp_cursor は、ID を指定して呼び出される、表形式データ ストリーム (TDS) パケットでは 1 を = です。  
  
||  
|-|  
|**適用対象**:SQL Server ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]を通じて[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_cursor  cursor, optype, rownum, table  
    [ , value[...n]]]  
```  
  
## <a name="arguments"></a>引数  
 *カーソル (cursor)*  
 カーソル ハンドルです。 *カーソル*が必要なパラメーターです、 **int**値を入力します。 *カーソル*は、*処理*値は SQL Server によって生成され、sp_cursoropen プロシージャから返されます。  
  
 *optype*  
 カーソルが実行する操作を指定する必須のパラメーターです。 *optype* 、次のいずれかが必要です**int**値を入力します。  
  
|値|名前|説明|  
|-----------|----------|-----------------|  
|0X0001|UPDATE|フェッチ バッファー内の 1 つ以上の行を更新する場合に使用します。  指定されている行*rownum*は、再アクセス、更新します。|  
|0x0002|Del|フェッチ バッファー内の 1 つ以上の行を削除する場合に使用します。 指定されている行*rownum*再アクセス、削除されます。|  
|0X0004|INSERT|SQL をビルドせずにデータを挿入**挿入**ステートメント。|  
|0X0008|REFRESH|基になるテーブルのデータをバッファーに再読み込みする場合に使用します。オプティミスティック コンカレンシーのために更新や削除が失敗した場合や UPDATE の後に、行を更新するために使用できます。|  
|0X10|LOCK|SQL Server U ロックを指定された行が含まれるページに獲得されるが発生します。 このロックは、S ロックとは互換性がありますが、X ロックや他の U ロックとは互換性がありません。 短期間のロックを実装する場合に使用できます。|  
|0X20|SETPOSITION|DELETE または UPDATE ステートメントを配置してプログラムを後続の SQL server を実行するときにのみ使用されます。|  
|0X40|ABSOLUTE|UPDATE または DELETE との組み合わせでのみ使用できます。  ABSOLUTE は KEYSET カーソルでのみ使用されます (DYNAMIC カーソルでは無視されます。STATIC カーソルは更新できません)。<br /><br /> 注:まだフェッチされていないキーセット内の行に対して ABSOLUTE を指定すると、操作でコンカレンシー チェックが失敗する可能性があるため、返される結果が保証されません。|  
  
 *rownum*  
 カーソルによる操作、更新、または削除の対象となるフェッチ バッファー内の行を指定します。  
  
> [!NOTE]  
>  RELATIVE、NEXT、または PREVIOUS のフェッチ操作の開始位置や、sp_cursor を使用して実行される更新や削除には影響しません。  
  
 *rownum*が必要なパラメーターです、 **int**値を入力します。  
  
 1  
 フェッチ バッファー内の最初の行を示します。  
  
 2  
 フェッチ バッファー内の 2 番目の行を示します。  
  
 3, 4, 5  
 3 番目、4 番目、5 番目の行を示します。  
  
 n  
 フェッチ バッファー内の n 番目の行を示します。  
  
 0  
 フェッチ バッファー内のすべての行を示します。  
  
> [!NOTE]  
>  更新、削除、更新、またはロックで使用するために有効なのみ*optype*値。  
  
 *テーブル*  
 テーブルを識別するテーブル名を*optype*カーソル定義は、結合を含むまたはあいまいな列名がによって返されるときに適用される、*値*パラメーター。 特定のテーブルを指定しない場合、既定値は FROM 句の最初のテーブルになります。 *テーブル*文字列入力値を必要とする省略可能なパラメーターです。 文字列は、任意の文字または UNICODE データ型として指定できます。 *テーブル*マルチパートのテーブル名を指定できます。  
  
 *value*  
 値を挿入または更新する場合に使用します。 *値*文字列パラメーターは、UPDATE および INSERT でのみ使用*optype*値。 文字列は、任意の文字または UNICODE データ型として指定できます。  
  
> [!NOTE]  
>  パラメーター名*値*ユーザーが割り当てることができます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 バッファー番号 0 の位置指定の DELETE または UPDATE 操作が含む DONE メッセージを返す、RPC を使用する場合、 *rowcount* 0 (失敗) またはフェッチ バッファー内の行ごとに 1 (成功)。  
  
## <a name="remarks"></a>コメント  
  
## <a name="optype-parameter"></a>optype パラメーター  
 SETPOSITION と更新、削除、更新、またはロックの組み合わせを除く絶対と UPDATE または DELETE、または、 *optype*値は相互に排他的です。  
  
 更新の値の SET 句がから構築された、*値*パラメーター。  
  
 INSERT を使用する利点の 1 つ*optype*値が非文字データ挿入のための文字形式に変換するを回避することができます。 値の指定方法は UPDATE と同じです。 必須の列が含まれていない場合、INSERT は失敗します。  
  
-   SETPOSITION の値は、RELATIVE、NEXT、または PREVIOUS のフェッチ操作の開始位置や、sp_cursor インターフェイスを使用して実行される更新や削除には影響しません。 値がフェッチ バッファー内の行を指定していない場合は、位置が 1 に設定され、エラーは返されません。 SETPOSITION を実行すると、位置を次の sp_cursorfetch 操作、T-SQL まで有効になります**フェッチ**操作、または sp_cursor SETPOSITION の操作、同じカーソルを使用します。 次の操作が sp_cursorfetch 操作の場合は、カーソルの位置が新しいフェッチ バッファーの最初の行に設定されますが、その他のカーソル呼び出しは位置の値に影響しません。 SETPOSITION と REFRESH、UPDATE、DELETE、または LOCK を OR 句で結合すると、位置の値を最後に変更された行に設定することができます。  
  
 を介してフェッチ バッファー内の行が指定されていない場合、 *rownum*パラメーター位置は、返されるエラーの 1 に設定されます。 設定された位置は、同じカーソルを使用して次の sp_cursorfetch 操作、T-SQL FETCH 操作、または sp_cursor SETPOSITION 操作が行われるまで有効なままになります。  
  
 SETPOSITION と REFRESH、UPDATE、DELETE、または LOCK を OR 句で結合すると、カーソル位置を最後に変更された行に設定することができます。  
  
## <a name="rownum-parameter"></a>rownum パラメーター  
 指定した場合、 *rownum*パラメーターは、フェッチ バッファー内の行番号ではなくキーセット内の行番号として解釈できます。 コンカレンシー制御はユーザーが管理する必要があります。 したがって、SCROLL_LOCKS カーソルの場合はその行のロックを独自に保持し (トランザクションを使用できます)、 OPTIMISTIC カーソルの場合は、この操作を実行する前にその行をフェッチしておく必要があります。  
  
## <a name="table-parameter"></a>table パラメーター  
 場合、 *optype*値が UPDATE または INSERT、および完全更新または挿入ステートメントとして送信された、*値*パラメーターで指定された値*テーブル*は無視されます。  
  
> [!NOTE]  
>  ビューに関しては、変更できるのはビューに参加している 1 つのテーブルだけです。 *値*パラメーターの列名は、ビュー内の列名を反映する必要がありますが、テーブル名には、(この場合 sp_cursor はの代わりにビュー名)、基になるベース テーブルの指定できます。  
  
## <a name="value-parameter"></a>value パラメーター  
 規則を使用するために 2 つの代替案がない*値*「引数」セクションで述べた。  
  
1.  名前を使用することができます '\@' という名前のいずれかの選択リスト内の列の名前を付けた*値*パラメーター。 この方法には、データ変換が不要になる可能性があるという利点があります。  
  
2.  完全な UPDATE または INSERT ステートメントを送信するか、複数のパラメーターを使用して、完全なステートメントに SQL Server を作成し、UPDATE または INSERT ステートメントの一部を送信するには、パラメーターを使用します。 例については、この後の「例」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="alternative-value-parameter-uses"></a>value パラメーターの複数の使用方法  
 UPDATE の場合:  
  
 1 つのパラメーターを使用する場合は、次の構文を使用して UPDATE ステートメントを送信できます。  
  
 `[ [ UPDATE <table name> ] SET ] {<column name> = expression} [,...n]`  
  
> [!NOTE]  
>  場合更新\<テーブル名 > を指定すると、任意の値がの指定、*テーブル*パラメーターは無視されます。  
  
 複数のパラメーターを使用する場合は、最初のパラメーターに次の形式の文字列を指定する必要があります。  
  
 `[ SET ] <column name> = expression  [,...n]`  
  
 後続のパラメーターは次の形式で指定します。  
  
 `<column name> = expression  [,...n]`  
  
 ここで、\<テーブル名 > で作成される update ステートメントが指定した値または既定値に 1 つ、*テーブル*パラメーター。  
  
 INSERT の場合:  
  
 1 つのパラメーターを使用する場合は、次の構文を使用して INSERT ステートメントを送信できます。  
  
 `[ [ INSERT [INTO] <table name> ] VALUES ] ( <expression> [,...n] )`  
  
> [!NOTE]  
>  場合挿入*\<テーブル名 >* を指定すると、任意の値がの指定、*テーブル*パラメーターは無視されます。  
  
 複数のパラメーターを使用する場合は、最初のパラメーターに次の形式の文字列を指定する必要があります。  
  
 `[ VALUES ( ] <expression>  [,...n]`  
  
 後続のパラメーターは次の形式で指定します。  
  
 `expression [,...n]`  
  
 ただし、VALUES を指定した場合は例外として、最後の式の末尾に ")" を付ける必要があります。 ここで、 *\<テーブル名 >* で作成される UPDATE ステートメントが指定した値または既定値に 1 つ、*テーブル*パラメーター。  
  
> [!NOTE]  
>  1 つのパラメーターを名前付きパラメーターとして送信することもできます ("`@VALUES`" など)。 その場合、他の名前付きパラメーターは使用できません。  
  
## <a name="see-also"></a>参照  
 [sp_cursoropen &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorfetch &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
