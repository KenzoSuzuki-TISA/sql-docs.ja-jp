---
title: 手順 4:データ フロー タスクをパッケージに追加します |。Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 96af3073-8f11-4444-b934-fe8613a2d084
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 06c80bc188937ef66f72fef003a5f8c27830ad10
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52793944"
---
# <a name="step-4-adding-a-data-flow-task-to-the-package"></a>手順 4:データ フロー タスクをパッケージに追加します。
  前の実習では、データ ソースおよび変換先データに接続するための接続マネージャーを作成しました。次の実習では、パッケージにデータ フロー タスクを追加します。 データ フロー タスクには、変換元と変換先の間でデータを移動させるデータ フロー エンジンがカプセル化されており、データを移動する際に、変換、クリーン、修正を行うことができます。 抽出、変換、読み込み (ETL) プロセスのほとんどが、このデータ フロー タスクで実行されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、データ フローと制御フローが切り離されています。  
  
### <a name="to-add-a-data-flow-task"></a>データ フロー タスクを追加するには  
  
1.  **[制御フロー]** タブをクリックします。  
  
2.  **[SSIS ツールボックス]** で **[お気に入り]** を展開し、 **[データ フロー タスク]** を **[制御フロー]** タブのデザイン画面上にドラッグします。  
  
    > [!NOTE]  
    >  SSIS ツールボックスが表示されていない場合は、メイン メニューの [SSIS]、[SSIS ツールボックス] の順に選択し、SSIS ツールボックスを表示します。  
  
3.  **制御フロー**デザイン画面で、新しく追加したを右クリックして**Data Flow Task**、 をクリックして**の名前を変更**、名を変更して、`Extract Sample Currency Data`します。  
  
     デザイン画面に追加するすべてのコンポーネントに一意な名前を付けるようにしましょう。 使いやすさと管理しやすさを考慮し、各コンポーネントの機能がわかるような名前を付けます。 このような方法で名前を付けておけば、自己文書化された [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを作成できます。 パッケージを文書化するには、注釈を使用する方法もあります。 注釈の詳細については、「 [パッケージで注釈を使用する](use-annotations-in-packages.md)」を参照してください。  
  
4.  データ フロー タスクを右クリックし、をクリックして**プロパティ**、[プロパティ] ウィンドウであることを確認し、`LocaleID`プロパティに設定されて**英語 (米国)** します。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [手順 5:追加して、フラット ファイル ソースを構成します。](lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
## <a name="see-also"></a>参照  
 [[データ フロー タスク]](control-flow/data-flow-task.md)  
  
  
