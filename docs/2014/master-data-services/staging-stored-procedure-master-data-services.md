---
title: ステージング ストアド プロシージャ (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 6a613106-9f87-4caf-a23a-a726fc6561c5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 6e66748610d648ec8e427315d2a317d26e699d06
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52758814"
---
# <a name="staging-stored-procedure-master-data-services"></a>ステージング ストアド プロシージャ (マスター データ サービス)
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]からステージング処理を開始する場合、次の 3 つのストアド プロシージャのいずれかを使用します。  
  
-   stg.udp_name_Leaf  
  
-   stg.udp_name_Consolidated  
  
-   stg.udp_name_Relationship  
  
 name は、エンティティの作成時に指定されたステージング テーブルの名前です。  
  
## <a name="staging-process-stored-procedure-parameters"></a>ステージング処理ストアド プロシージャのパラメーター  
 次の表では、これらのストアド プロシージャのパラメーターの一覧を示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|**VersionName**<br /><br /> 必須|バージョンの名前。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コレクションの設定に応じて、このパラメーターは大文字と小文字が区別される場合とされない場合があります。|  
|**LogFlag**<br /><br /> 必須|ステージング処理中にトランザクションをログに記録するかどうかを決定します。 有効な値は次のとおりです。<br /><br /> **0**:トランザクションを記録しません。<br />**1**:トランザクション ログを記録します。<br /><br /> <br /><br /> 詳細については、「[トランザクション (マスター データ サービス)](transactions-master-data-services.md)」を参照してください。|  
|**BatchTag**<br /><br /> Web サービス以外は必須|ステージング テーブルに指定した **BatchTag** の値。|  
|**Batch_ID**<br /><br /> Web サービスでのみ必須|ステージング テーブルに指定した **Batch_ID** の値。|  
  
### <a name="staging-process-stored-procedure-example"></a>ステージング処理ストアド プロシージャの例  
 次の例は、ステージング ストアド プロシージャを使用してステージング処理を開始する方法を示します。  
  
```  
USE [DATABASE_NAME]  
GO  
  
EXEC[stg].[udp_name_Leaf]  
      @VersionName = N'VERSION_1',  
@LogFlag = 1,  
@BatchTag = N'batch1'  
  
GO  
  
```  
  
## <a name="see-also"></a>参照  
 [検証ストアド プロシージャ (マスター データ サービス)](../../2014/master-data-services/validation-stored-procedure-master-data-services.md)   
 [読み込むか、ステージング処理を使用してマスター データ サービス内のメンバーを更新します。](/sql/2014/master-data-services/add-update-and-delete-data-master-data-services)   
 [ステージング処理中に発生するエラーを表示する&#40;マスター データ サービス&#41;](view-errors-that-occur-during-staging-master-data-services.md)  
  
  
