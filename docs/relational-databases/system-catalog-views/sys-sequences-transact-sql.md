---
title: sys.sequences (TRANSACT-SQL) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sequences_TSQL
- sys.sequences
- sequences
- sequences_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sequence number object, sys. sequences catalog view
- sys.sequences catalog view
ms.assetid: 0e1b0e32-1cce-40f7-83c8-860ec660138a
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e33dfa78117b68d1cb67baed2aea6bd7f5487e5b
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/27/2018
ms.locfileid: "52398125"
---
# <a name="syssequences-transact-sql"></a>sys.sequences (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  データベース内のシーケンス オブジェクトごとに 1 行のデータを格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|\<列を継承 >||すべての列を継承[sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)します。|  
|**start_value**|**sql_variant NOT NULL**|シーケンス オブジェクトの開始値。 ALTER SEQUENCE を使用してシーケンス オブジェクトを再開するときに、この値から再開されます。 ときに、シーケンス オブジェクトによりに進みます、 **minimum_value**または**maximum_value**ではなく、 **start_value**します。|  
|**increment**|**sql_variant NOT NULL**|各生成値の後にシーケンス オブジェクトを増分するために使用される値。|  
|**minimum_value**|**sql_variant 型の NULL**|シーケンス オブジェクトによって生成できる最小値。 この値に達した後、シーケンス オブジェクトは、より多くの値を生成しようとしてエラーを返すか、または CYCLE オプションが指定されている場合は再開します。 MINVALUE が指定されていない場合、この列は、シーケンス ジェネレーターのデータ型でサポートされる最小値を返します。|  
|**maximum_value**|**sql_variant 型の NULL**|シーケンス オブジェクトによって生成できる最大値。 シーケンス オブジェクトがこの値に達した後にいずれかが開始されます CYCLE オプションが指定されている場合、複数の値または再起動を生成しようとするときはエラーを返します。 MAXVALUE が指定されていない場合、この列は、シーケンス ジェネレーターのデータ型によってサポートされる最大値を返します。|  
|**is_cycling**|**bit NOT NULL**|シーケンス オブジェクトに対して NO CYCLE が指定されている場合は 0 を返し、CYCLE が指定されている場合は 1 を返します。|  
|**is_cached**|**bit NOT NULL**|シーケンス オブジェクトに対して NO CACHE が指定されている場合は 0 を返し、CACHE が指定されている場合は 1 を返します。|  
|**cache_size**|**int NULL**|シーケンス オブジェクトの指定されたキャッシュ サイズを返します。 シーケンスが NO CACHE オプションを使用して作成されている場合、またはキャッシュ サイズを指定せずに CACHE が指定されている場合、この列には NULL が格納されます。 キャッシュ サイズとして指定された値がシーケンス オブジェクトで返すことができる値の最大数より大きい場合、取得不可能なキャッシュ サイズがそのまま表示されます。|  
|**system_type_id**|**tinyint NOT NULL**|シーケンス オブジェクトのデータ型のシステム型の ID。|  
|**user_type_id**|**int NOT NULL**|ユーザーによって定義されたシーケンス オブジェクトのデータ型の ID。|  
|**有効桁数 (precision)**|**tinyint NOT NULL**|データ型の最大有効桁数。|  
|**scale**|**tinyint NOT NULL**|型の小数点以下の最大桁数。 小数点以下桁数は有効桁数と共に返され、完全なメタデータが提供されます。 シーケンス オブジェクトの場合、整数型のみが許可されているため、小数点以下桁数は常に 0 です。|  
|**current_value**|**sql_variant NOT NULL**|必須の最後の値。 NEXT VALUE FOR 関数の実行を最後の値の最後に実行から返される値、 **sp_sequence_get_range**プロシージャ。 シーケンスがまったく使用されていない場合は、START WITH 値を返します。|  
|**is_exhausted**|**bit NOT NULL**|0 は、より多くの値をシーケンスから生成できることを示します。 1 は、シーケンス オブジェクトが MAXVALUE パラメーターに達し、さらにシーケンス サイクルが CYCLE に設定されていないことを示します。 ALTER SEQUENCE を使用してシーケンスが再開されるまで、NEXT VALUE FOR 関数はエラーを返します。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンでは、カタログ ビューでのメタデータの表示が、ユーザーが所有しているかそのユーザーが権限を許可されている、セキュリティ保護可能なメタデータに制限されます。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [シーケンス番号](../../relational-databases/sequence-numbers/sequence-numbers.md)   
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [sp_sequence_get_range &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md)  
  
  
