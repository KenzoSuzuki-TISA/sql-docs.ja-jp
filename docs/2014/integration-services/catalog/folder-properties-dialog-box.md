---
title: '[フォルダーのプロパティ] ダイアログ ボックス | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.iscreatefolder.f1
- sql12.ssis.ssms.isfolderprop.general.f1
- sql12.ssis.ssms.isfolderprop.permissions.f1
ms.assetid: d9a2bfae-fcc8-46be-b588-4a9db03f7e45
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6cbca0592074b34250d5d07003494800942affaa
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804564"
---
# <a name="folder-properties-dialog-box"></a>[フォルダーのプロパティ] ダイアログ ボックス
  フォルダーには、`SSISDB` カタログ内のプロジェクトおよび環境が含まれます。 フォルダーごとに、フォルダーの内容に適用される権限を定義します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の権限の詳細については、「[catalog.grant_permission &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database)」をご覧ください。  
  
## <a name="to-set-folder-description-and-permissions"></a>フォルダーの説明と権限を設定するには  
  
1.  フォルダーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[全般]** ページで、 **[全般]** の下にある **[説明]** を選択して説明を入力します (省略可)。  
  
3.  **[権限]** ページで、 **[参照]** をクリックし、1 つ以上のデータベース プリンシパルを選択して **[OK]** をクリックします。  
  
4.  **[ログインまたはロール]** で名前を選択し、 **[権限]** で適切な権限を指定します。  
  
5.  **[OK]** をクリックして変更を受け入れ、 **[フォルダーのプロパティ]** ダイアログ ボックスを閉じます。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; サーバー](integration-services-ssis-server-and-catalog.md)   
 [catalog.grant_permission &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database)  
  
  
