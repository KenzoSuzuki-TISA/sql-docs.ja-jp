---
title: 手順 3:フラット ファイル接続マネージャーの変換 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 459e3995-2116-4f15-aaa2-32f26113869c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1de57ab14dc4dcfc07f838494ca48f8b12da6660
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143562"
---
# <a name="lesson-2-3-modify-the-flat-file-connection-manager"></a>レッスン 2-3:フラット ファイル接続マネージャーの変更

この実習では、レッスン 1 で作成したフラット ファイル接続マネージャーを変更します。 そのフラット ファイル接続マネージャーはファイルを 1 つ静的に読み込むように構成されています。 フラット ファイル接続マネージャーで繰り返しファイルを読み込むには、ユーザー定義変数 `User::varFileName` を使用するように接続マネージャーの ConnectionString プロパティを変更します。この変数に、実行時に読み込むファイルのパスを定義します。  
  
ユーザー定義変数の値を使用するように接続マネージャーの ConnectionString プロパティを変更することで、接続マネージャーはさまざまなフラット ファイルに接続します。 実行時、Foreach ループ コンテナーが繰り返されるたびに `User::varFileName` 変数がこう損されます。 変数が更新されると、接続マネージャーが複数のフラット ファイルに接続され、異なるデータセットを処理するデータ フローのタスクが発生します。  
  
## <a name="configure-the-flat-file-connection-manager-to-use-a-variable"></a>変数を使用するようにフラット ファイル接続マネージャーを構成する  
  
1.  **接続マネージャー** ペインで、 **[Sample Flat File Source Data]** を右クリックして **[プロパティ]** をクリックします。  
  
2.  **[プロパティ]** ウィンドウの **[式]** で、空のセルを選択し、参照ボタン **[...]** を選択します。  
  
3.  **[プロパティ式エディター]** ダイアログの **[プロパティ]** 列で **ConnectionString** を選択します。  
  
4.  **[式]** 列の参照ボタン **[...]** を選択し、**[式ビルダー]** ダイアログ ボックスを開きます。  
  
5.  **[式ビルダー]** ダイアログで **[変数]** ノードを展開します。  
  
6.  **User::varFileName** 変数を **[式]** ボックスにドラッグします。  
  
7.  **[OK]** を選択し、**[式ビルダー]** ダイアログを閉じます。  
  
8.  再度 **[OK]** を選択し、**[プロパティ式エディター]** ダイアログを閉じます。  
  
## <a name="go-to-next-task"></a>次の実習に進む  
[手順 4:レッスン 2 で作成したチュートリアル パッケージのテスト](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
  
  
