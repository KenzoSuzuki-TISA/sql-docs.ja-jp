---
title: MSSQL_ENG014005 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014005 error
ms.assetid: f168f0d6-cb11-45d4-9781-c374d7f388ee
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8344306dba453df66b1964b04a7df446b8f7530e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47603792"
---
# <a name="mssqleng014005"></a>MSSQL_ENG014005
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|14005|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|パブリケーションを削除できませんでした。 サブスクリプションが存在します。|  
  
## <a name="explanation"></a>説明  
 1 つ以上のサブスクリプションが関連付けられているパブリケーションを削除しようとしました。 パブリケーションは、サブスクリプションが関連付けられていない場合にのみ削除できます。  
  
## <a name="user-action"></a>ユーザーの操作  
 パブリケーションを削除する前にサブスクリプションを削除します。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してパブリケーションを削除する場合は、パブリケーションを削除する前に関連するすべてのサブスクリプションを自動的に削除するオプションを使用できます。 ストアド プロシージャを使用する場合は、最初にサブスクリプションを明示的に削除する必要があります。 詳細については、「 [Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md) 」および「 [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md)」を参照してください。  
  
 パブリケーションに存在するサブスクリプションが表示されない場合や、パブリケーションの作成時にこのエラーが表示される場合は、前のサブスクリプションを削除したときに完全にクリーンアップされていない可能性があります。 レプリケーションに関連するすべてのオブジェクトと設定を削除するには、データベースで [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) を実行します。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
