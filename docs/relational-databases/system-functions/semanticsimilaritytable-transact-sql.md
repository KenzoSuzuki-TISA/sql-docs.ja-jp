---
title: semanticsimilaritytable (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- semanticsimilaritytable
- semanticsimilaritytable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semanticsimilaritytable function
ms.assetid: b49d40ab-7552-438b-ad67-6237dcccb75b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bca3fe143308bb7bf3d8a8e7754c018c749786cc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47791180"
---
# <a name="semanticsimilaritytable-transact-sql"></a>semanticsimilaritytable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  指定されたドキュメントに意味が似ている指定された列のコンテンツを持つドキュメントに対し、0 行、1 行、または複数の行から成るテーブルを返します。  
  
 この行セット関数は、標準のテーブル名のように、SELECT ステートメントの FROM 句で参照できます。  

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
SEMANTICSIMILARITYTABLE  
    (  
    table,  
    { column | (column_list) | * },  
    source_key  
    )  
```  
  
##  <a name="Arguments"></a> 引数  
 **テーブル**  
 フルテキスト インデックスとセマンティック インデックスが有効になっているテーブルの名前を指定します。  
  
 この名前は、1 部から 4 部の構成の名前にできますが、リモート サーバー名は許可されません。  
  
 **column**  
 結果を返すインデックス付きの列の名前です。 列でセマンティック インデックス作成が有効になっている必要があります。  
  
 **column_list**  
 複数の列を指定します。その際、各列をコンマで区切り、かっこで囲みます。 すべての列でセマンティック インデックス作成が有効になっている必要があります。  
  
 **\***  
 セマンティック インデックスが有効になっているすべての列が含まれていることを示します。  
  
 **source_key**  
 特定の行の結果を要求する、行の一意のキーです。  
  
 このキーは、可能であれば常に、ソース テーブル内の一意なフルテキスト キーの型に暗黙的に変換されます。 キーは定数または変数として指定できますが、式や、スカラー サブクエリの結果にすることはできません。  
  
## <a name="table-returned"></a>返されるテーブル  
 次の表に、この行セット関数から返される、類似したドキュメントまたは関連ドキュメントに関する情報を示します。  
  
 結果が複数の列から要求される場合は、列ごとに一致したドキュメントが返されます。  
  
|Column_name|型|説明|  
|------------------|----------|-----------------|  
|**source_column_id**|**int**|ソース ドキュメントを使用して類似したドキュメントを検出したときの、検出元の列の ID。<br /><br /> 列 ID から列名 (または列名から列 ID) を取得する方法の詳細については、COL_NAME 関数と COLUMNPROPERTY 関数のセクションを参照してください。|  
|**matched_column_id**|**int**|類似したドキュメントの検出元の列の ID。<br /><br /> 列 ID から列名 (または列名から列 ID) を取得する方法の詳細については、COL_NAME 関数と COLUMNPROPERTY 関数のセクションを参照してください。|  
|**matched_document_key**|**\***<br /><br /> このキーは、ソース テーブル内の一意キーの型と一致します。|クエリで指定したドキュメントに類似していることが判明したドキュメントまたは行の、フルテキストおよびセマンティックな抽出の一意のキー値。|  
|**score**|**REAL**|類似した他のすべてのドキュメントとの関係における、このドキュメントの類似性の相対値。<br /><br /> 値の範囲内の小数値は、[0.0, 1.0] より高いスコアより近い一致を表す、1.0 は完全なスコアです。|  
  
## <a name="general-remarks"></a>全般的な解説  
 詳細については、次を参照してください。[類似および関連ドキュメント セマンティック検索による](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)します。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 複数の列にわたって類似したドキュメントに対するクエリを実行することはできません。 **SEMANTICSIMILARITYTABLE**関数により識別されるソース列と同じ列から類似したドキュメントのみを取得、 **source_key**引数。  
  
## <a name="metadata"></a>メタデータ  
 セマンティックな類似性の抽出および作成の詳細と状態については、次の動的管理ビューに対してクエリを実行してください。  
  
-   [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 フルテキストおよびセマンティック インデックスが作成されたベース テーブルに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、AdventureWorks2012 サンプル データベースの HumanResources.JobCandidate テーブルから、指定した候補に類似する上位 10 件の候補を取得します。  
  
```scr  
SELECT TOP(10) KEY_TBL.matched_document_key AS Candidate_ID  
FROMSEMANTICSIMILARITYTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume,  
    @CandidateID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
  
```  
  
  
