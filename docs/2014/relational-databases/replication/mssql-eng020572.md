---
title: MSSQL_ENG020572 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020572 error
ms.assetid: 636566db-ffcf-4109-8c11-15b8c7cb9cd9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 243b9b1658e2a0b34626e973799127b19ddc0e11
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52806744"
---
# <a name="mssqleng020572"></a>MSSQL_ENG020572
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|20572|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|パブリケーション '%s' のアーティクル '%s' に対するサブスクライバー '%s' のサブスクリプションが、検証エラーの発生後、再初期化されました。|  
  
## <a name="explanation"></a>説明  
 サブスクライバーのデータがパブリッシャーのデータに対して検証され、データが一致しなかったため検証に失敗しました。 検証を実行するように指定したときに、検証が失敗した場合にサブスクリプションを再初期化するオプションを選択しました。 サブスクリプションを再初期化するには、サブスクライバーで新しいスナップショットを適用する必要があります。 検証の詳細については、「 [Validate Replicated Data](validate-replicated-data.md)」を参照してください。  
  
## <a name="user-action"></a>ユーザーの操作  
 サブスクライバーで新しいスナップショットを適用すると、パブリッシャーのデータとサブスクライバーのデータが一致します。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](errors-and-events-reference-replication.md)  
  
  
