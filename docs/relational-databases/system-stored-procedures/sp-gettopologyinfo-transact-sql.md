---
title: sp_gettopologyinfo (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_gettopologyinfo_TSQL
- sp_gettopologyinfo
helpviewer_keywords:
- sp_gettopologyinfo
ms.assetid: 8bbe8a06-a4aa-4219-8402-12db6a4682c6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4b5532a5c9dfba03a0e2b9b2fe649912cd0535cc
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52764554"
---
# <a name="spgettopologyinfo-transact-sql"></a>sp_gettopologyinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ピア ツー ピア トランザクション レプリケーション トポロジに関する情報を返します。 実行[sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md)この手順を実行する前に情報を収集します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_gettopologyinfo [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>引数  
 [ @request_id=] *request_id*  
 トポロジ状態要求の ID を指定します。 *request_id*は**int**、既定値は NULL です。 ID を取得するには、@request_id出力パラメーターを [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md)またはクエリ 、 [MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md)システム テーブル。  
  
## <a name="result-sets"></a>結果セット  
 sp_gettopologyinfo では、単一の XML 列で構成される結果セットが返されます。 XML 列にデータが内のデータと同じ、 [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md)システム テーブル。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 sp_gettopologyinfo は、ピア ツー ピア トランザクション レプリケーションで使用します。 実行[sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) sp_gettopologyinfo を実行する前にします。 プロシージャはピア ツー ピア トポロジ構成ウィザードから使用されますが、トポロジ情報が必要な場合は XML 形式で直接使用することもできます。 表形式の結果を使用する場合は、クエリ、 [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md)システム テーブル。  
  
## <a name="permissions"></a>アクセス許可  
 固定サーバー ロール sysadmin または固定データベース ロール db_owner のメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
