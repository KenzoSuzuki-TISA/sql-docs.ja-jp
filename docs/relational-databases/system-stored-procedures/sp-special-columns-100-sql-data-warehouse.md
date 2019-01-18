---
title: sp_special_columns_100 (SQL データ ウェアハウス) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.subservice: design
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5774fadc-77cc-46f8-8f9f-a0f9efe95e21
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: fdebe91359fbe9d7c9ef7aaadc38ba096427f651
ms.sourcegitcommit: 0a64d26f865a21f4bd967b2b72680fd8638770b8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2019
ms.locfileid: "54395391"
---
# <a name="spspecialcolumns100-sql-data-warehouse"></a>sp_special_columns_100 (SQL データ ウェアハウス)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  テーブル内の行を一意に識別する列の最適集合を返します。 トランザクションが行の任意の値を更新した場合に自動的に更新される列も返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_special_columns_100 [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @qualifier = ] 'qualifier' ]   
     [ , [ @col_type = ] 'col_type' ]   
     [ , [ @scope = ] 'scope' ]  
     [ , [ @nullable = ] 'nullable' ]   
     [ , [ @ODBCVer = ] 'ODBCVer' ]   
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 [ @table_name=] '*table_name*'  
 カタログ情報を返すために使用するテーブルの名前です。 *名前*は**sysname**、既定値はありません。 ワイルドカードによるパターン照合はサポートされていません。  
  
 [ @table_owner=] '*table_owner*'  
 カタログ情報を返すために使用するテーブルのテーブル所有者です。 *所有者*は**sysname**、既定値は NULL です。 ワイルドカードによるパターン照合はサポートされていません。 場合*所有者*が指定されていない、基になる DBMS の既定のテーブル可視性規則が適用されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、指定された名前のテーブルを現在のユーザーが所有している場合、そのテーブルの列が返されます。 場合*所有者*が指定されていない、現在のユーザーが、指定のテーブルを所有していない*名前*、この手順は、指定のテーブルを探します*名前*データベースによって所有されています。所有者。 テーブルが存在する場合は、その列が返されます。  
  
 [ @qualifier=] '*修飾子*'  
 テーブル識別子の名前です。 *修飾子*は**sysname**、既定値は NULL です。 さまざまな DBMS 製品は、3 つの部分がテーブルの名前付けをサポート (*qualifier.owner.name*)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、この列はデータベース名を表します。 製品によっては、テーブルのデータベース環境のサーバー名を表す場合があります。  
  
 [ @col_type=] '*col_type*'  
 列の種類です。 *col_type*は**char (** 1 **)**、既定値は r です種類 R 最適な列または列のセットを返します、または複数の列から値を取得することによって、指定した任意の行では、。一意に識別するテーブル。 列は、この目的のために特別に設計された疑似列、または、テーブルでインデックスが一意な 1 つ以上の列になります。 種類 V は、指定したテーブルに自動更新される列が 1 つ以上存在する場合、該当する列または列のセットを返します。この列は、トランザクションによって行の値が更新されると、データ ソースによって自動的に更新される列です。  
  
 [ @scope=] '*scope*'  
 ROWID の最低限必要な範囲を指定します。 *スコープ*は**char (** 1 **)**、既定値は t です。 範囲 C には、、ROWID がその行に配置されている場合にのみ有効であることを指定します。 範囲 T は、ROWID がトランザクションに対して有効であることを指定します。  
  
 [ @nullable=] '*null 許容*'  
 特別列に NULL 値を認めるかどうかを示します。 *null 許容*は**char (** 1 **)**、既定値は u です。 O には、null 値を許容しない特別列を指定します。 U は部分的に NULL を許容する列を指定します。  
  
 [ @ODBCVer=] '*ODBCVer*'  
 使用する ODBC のバージョンを指定します。 *ODBCVer*は**int (** 4 **)**、既定値は 2 です。 既定値は ODBC Version 2.0 を示します。 ODBC version 2.0 と ODBC version 3.0 の違いの詳細については、ODBC version 3.0 の ODBC SQLSpecialColumns 仕様を参照してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|SCOPE|**smallint**|行 ID の実際の範囲。 0、1、または 2 になる場合があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 常に 0 を返します。 このフィールドは常に値を返します。<br /><br /> 0 = SQL_SCOPE_CURROW。 行 ID は、その行に位置している間のみ有効であることが保証されます。 その行が別のトランザクションによって更新または削除された場合は、後でその行 ID を使って再度選択しても行は返されません。<br /><br /> 1 = SQL_SCOPE_TRANSACTION。 行 ID は現在のトランザクションの間は、有効であることが保証されます。<br /><br /> 2 = SQL_SCOPE_SESSION。 行 ID は、セッションの間は (複数のトランザクションにまたがって) 有効であることが保証されます。|  
|COLUMN_NAME|**sysname**|各列の列名、*テーブル*が返されます。 このフィールドは常に値を返します。|  
|DATA_TYPE|**smallint**|ODBC SQL データ型。|  
|TYPE_NAME|**sysname**|データ ソースに依存するデータ型名です。たとえば、 **char**、 **varchar**、 **money**、または**テキスト**します。|  
|PRECISION|**Int**|データ ソース上の列の有効桁数。 このフィールドは常に値を返します。|  
|LENGTH|**Int**|データ ソース内のバイナリ形式でのデータ型の長さ (バイト単位) の必須の 10 **char (** 10 **)**、4 の**整数**、および 2 の**smallint**.|  
|SCALE|**smallint**|データ ソース上の列の小数点以下桁数。 NULL は、小数点以下桁数を適用できないデータ型に対して返されます。|  
|PSEUDO_COLUMN|**smallint**|その列が疑似列であるかどうかを示します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は常に 1 を返します。<br /><br /> 0 = SQL_PC_UNKNOWN<br /><br /> 1 = SQL_PC_NOT_PSEUDO<br /><br /> 2 = SQL_PC_PSEUDO|  
  
## <a name="remarks"></a>コメント  
 sp_special_columns は、odbc SQLSpecialColumns と同じです。 返される結果は、SCOPE の順序に従って並べ替えられます。  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 次の例では、`FactFinance` テーブルの行を一意に識別する列に関する情報が返されます。  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_special_columns_100 @table_name = 'FactFinance';  
```  
  
## <a name="see-also"></a>参照  
 [SQL Data Warehouse のストアド プロシージャ](../../relational-databases/system-stored-procedures/sql-data-warehouse-stored-procedures.md)  
  
  

