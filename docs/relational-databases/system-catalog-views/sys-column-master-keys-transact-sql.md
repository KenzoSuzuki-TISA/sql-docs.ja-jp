---
title: sys.column_master_keys (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- column_master_key_definitions_TSQL
- column_master_key_definitions
- sys.column_master_key_definitions_TSQL
- sys.column_master_key_definitions
- column_master_keys_TSQL
- column_master_keys
- sys.column_master_keys_TSQL
- sys.column_master_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_master_key_definitions catalog view
- sys.column_master_keys catalog view
ms.assetid: fbec2efa-5fe9-4121-9b34-60497b0b2aca
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1cb1740bdb0ae26d91e2a9ad9e2becb69d3b2810
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52518715"
---
# <a name="syscolumnmasterkeys-transact-sql"></a>sys.column_master_keys (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  各データベースのマスター _ キーを使用して、追加の行を返します、 [CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)ステートメント。 各行では、1 つの列のマスター_キー (CMK) を表します。  
    
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|CMK の名前。|  
|**column_master_key_id**|**int**|列のマスター_キーの ID です。|  
|**create_date**|**datetime**|列のマスター_キーが作成された日付。|  
|**modify_date**|**datetime**|列のマスター_キーが前回変更された日付。|  
|**key_store_provider_name**|**sysname**|CMK を格納している列のマスター_キーのストアのプロバイダーの名前。 使用できる値は、以下のとおりです。<br /><br /> MSSQL_CERTIFICATE_STORE - 列マスター キー ストアが証明書ストアである場合。<br /><br /> ユーザー定義値をカスタム型の列マスター キー ストアがある場合。|  
|**key_path**|**nvarchar (4000)**|キーの列マスター_キー ストア固有のパス。 パスの形式は、列のマスター_キーのストアの種類によって異なります。 例:<br /><br /> `'CurrentUser/Personal/'<thumbprint>`<br /><br /> 開発者は、責任を定義するためのカスタム列マスター_キー ストアでは、カスタムの列のマスター_キーのストアの場合、どのようなキーのパスをします。|  
|**allow_enclave_computations**|**bit**|かどうか、列マスター_キーがエンクレーブ対応、(場合、このマスター _ キーで暗号化された列暗号化キーは、サーバー側のセキュリティで保護された enclaves 内の計算に使用できます) を示します。 詳細については、「[セキュア エンクレーブを使用する Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)」を参照してください。|  
|**signature**|**varbinary(max)**|デジタル署名**key_path**と**allow_enclave_computations**、列マスター_キーを使用して生成された、によって参照される**key_path**します。|


  
## <a name="permissions"></a>アクセス許可  
 必要があります、 **VIEW ANY COLUMN MASTER KEY**権限。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Always Encrypted &#40;データベース エンジン&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
  
  
