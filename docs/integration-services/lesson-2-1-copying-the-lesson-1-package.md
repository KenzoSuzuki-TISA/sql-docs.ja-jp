---
title: 手順 1:レッスン 1 のパッケージをコピーする | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 7f1616c2-2b4e-4010-be50-27d7b897403a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 31979c1515fa54a059bddf562ddb42e4ff6131f4
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143182"
---
# <a name="lesson-2-1-copy-the-lesson-1-package"></a>レッスン 2-1:レッスン 1 のパッケージをコピーする

ここでは、**Lesson 1.dtsx** パッケージのコピーを作成します。 レッスン 1 を終了していない場合は、このチュートリアルに含まれる、完了しているレッスン 1 のパッケージを使用することもできます。 レッスン 2 の残りの実習では、このパッケージの新しいコピーを使用します。  
  
## <a name="create-the-lesson-2-package"></a>レッスン 2 のパッケージの作成  

完了したレッスン 1 をコピーする場合、この手順を使用します。  レッスン 1 のサンプルをコピーするには、次のセクションを参照してください。
  
1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools がまだ開いていない場合は、**[開始]** > **[すべてのプログラム]** > **[Microsoft SQL Server 2017]** の順に選択し、次に **[SQL Server Data Tools]** を選択します。  
  
2.  **[ファイル]** メニューで、**[開く]** > **[プロジェクト/ソリューション]** の順に選択し、**[SSIS Tutorial]** フォルダーを選択し、**[開く]** を選択してから、**[SSIS Tutorial.sln]** をダブルクリックします。  
  
3.  **ソリューション エクスプローラー**で、**[Lesson 1.dtsx]** を右クリックし、**[コピー]** を選択します。  
  
4.  **ソリューション エクスプローラー**で、**[SSIS パッケージ]** を右クリックし、**[貼り付け]** を選択します。  
  
    コピーしたパッケージの既定の名前は、**Lesson 2.dtsx** です。  
  
5.  **ソリューション エクスプローラー**で **[Lesson 2.dtsx]** をダブルクリックし、パッケージを開きます。  
  
6.  **[制御フロー]** デザイン画面の背景上で任意の場所を右クリックし、**[プロパティ]** を選択します。  
  
7.  **[プロパティ]** ウィンドウで、**[Name]** プロパティを「**Lesson 2**」に変更します。  
  
8.  **ID** プロパティのボックスを選択し、ドロップダウン矢印を選択し、[**\<新しい ID の生成>**] を選択します。  
  
## <a name="use-the-sample-lesson-1-package"></a>レッスン 1 のサンプル パッケージの使用  
  
1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools を開き、SSIS Tutorial プロジェクトを開きます。  
  
2.  **ソリューション エクスプローラー**で **[SSIS パッケージ]** を右クリックし、**[既存のパッケージを追加]** を選択します。  
  
3.  **[既存のパッケージのコピーを追加]** ダイアログの **[パッケージの場所]** で、**[ファイル システム]** を選択します。  
  
4.  参照ボタン **[...]** をクリックし、コンピューター上の **Lesson 1.dtsx** に移動して、**[開く]** を選択します。  
  
5.  前のセクションの手順 3 から 8 の説明に従って、レッスン 1 パッケージをコピーして貼り付けます。  
  
## <a name="go-to-next-task"></a>次の実習に進む

[手順 2:Foreach ループ コンテナーの追加および構成](../integration-services/lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
