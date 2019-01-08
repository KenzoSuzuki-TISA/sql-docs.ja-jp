---
title: REFERENTIAL_CONSTRAINTS (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- REFERENTIAL_CONSTRAINTS
- REFERENTIAL_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.REFERENTIAL_CONSTRAINTS view
- REFERENTIAL_CONSTRAINTS view
ms.assetid: 5d358f18-0a85-4b55-af4b-98d5f4cd1020
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 149bcdddd5388c9c68a9d2d96c5474903104757d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52508023"
---
# <a name="referentialconstraints-transact-sql"></a>REFERENTIAL_CONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在のデータベース内の FOREIGN KEY 制約ごとに 1 行のデータを返します。 この情報スキーマ ビューは、現在のユーザーが権限を所有しているオブジェクトについての情報を返します。  
  
 これらのビューから情報を取得するには、完全修飾名を指定**INFORMATION_SCHEMA** 。_view_name_します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar(** 128 **)**|制約修飾子|  
|**CONSTRAINT_SCHEMA**|**nvarchar(** 128 **)**|制約を含むスキーマの名前です。<br /><br /> **\*\* 重要な\* \*** オブジェクトのスキーマを決定 INFORMATION_SCHEMA ビューを使用しないでください。 オブジェクトのスキーマを調べる唯一の信頼性のある方法は、sys.objects カタログ ビューに対するクエリを実行する方法です。|  
|**CONSTRAINT_NAME**|**sysname**|制約名。|  
|**UNIQUE_CONSTRAINT_CATALOG**|**nvarchar(** 128 **)**|UNIQUE 制約修飾子です。|  
|**UNIQUE_CONSTRAINT_SCHEMA**|**nvarchar(** 128 **)**|UNIQUE 制約を含むスキーマの名前です。<br /><br /> **\*\* 重要な\* \*** オブジェクトのスキーマを決定 INFORMATION_SCHEMA ビューを使用しないでください。 オブジェクトのスキーマを調べる唯一の信頼性のある方法は、sys.objects カタログ ビューに対するクエリを実行する方法です。|  
|**UNIQUE_CONSTRAINT_NAME**|**sysname**|UNIQUE 制約。|  
|**MATCH_OPTION**|**varchar (** 7 **)**|参照に関する制約の一致条件です。 常に SIMPLE を返します。 これは、一致条件が定義されていないことを表します。 次のいずれかに当てはまる場合には、条件は一致したと見なされます。<br /><br /> 外部キー列内の少なくとも 1 つの値が NULL である。<br /><br /> 外部キー列のすべての値が NULL でなく、主キー テーブルに同じキーの行がある。|  
|**UPDATE_RULE**|**varchar (** 11 **)**|ときに実行されるアクションを[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントにこの制約によって定義されている参照の整合性に違反しています。 次のいずれかを返します。 <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> この制約の ON UPDATE で NO ACTION が指定されている場合、制約内で参照されている主キーの更新が外部キーに反映されません。 少なくとも 1 つの外部キーに同じ値が含まれるために、このような主キーの更新が参照整合性違反を引き起こす場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] による親テーブルと参照元テーブルへの変更は実行されません。 また [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってエラーが発生します。<br /><br /> この制約の ON UPDATE で CASCADE が指定されている場合は、主キーの値の変更が外部キーの値に自動的に反映されます。|  
|**DELETE_RULE**|**varchar (** 11 **)**|この制約によって定義される参照整合性に [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが違反したときに実行されるアクションです。 次のいずれかを返します。 <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> この制約の ON DELETE で NO ACTION が指定されている場合、制約内で参照されている主キーの削除が外部キーに反映されません。 少なくとも 1 つの外部キーに同じ値が含まれるために、このような主キーの削除が参照整合性違反を引き起こす場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] による親テーブルと参照元テーブルへの変更は実行されません。 また [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってエラーが発生します。<br /><br /> この制約の ON DELETE で CASCADE が指定されている場合、主キーの値の変更が外部キーの値に自動的に反映されます。|  
  
## <a name="see-also"></a>参照  
 [システム ビュー &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [情報スキーマ ビュー &#40;TRANSACT-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.foreign_keys &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)  
  
  
