---
title: タスク 3:Excel ファイルからドメイン値のインポート |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 242e8309-1195-495b-9cd5-aa127748c185
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 16356826909edbde5218ad509af6864817a856c1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/27/2018
ms.locfileid: "52399205"
---
# <a name="task-3-importing-domain-values-from-an-excel-file"></a>タスク 3:Excel ファイルからドメイン値をインポートする
  ここでは、Excel ファイルのワークシートから **State** ドメインの値をインポートします。  
  
1.  **[ドメイン リスト]** から **State**ドメインをクリックします。  
  
2.  右側のペインで、 **[ドメイン値]** タブがアクティブになっていることを確認します。  
  
3.  右側のペインのツール バーで、 **[値をインポートします]** の横にある **下矢印** をクリックし、 **[Excel から有効な値をインポートします]** をクリックします。  
  
     ![Excel のメニューから有効な値をインポート](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-01.jpg "Excel のメニューからの有効な値のインポート")  
  
4.  **[参照]** をクリックし、 **Suppliers.xls**を選択して、 **[開く]** をクリックします。  
  
5.  **[ワークシート]** に **StatesToImport$** を選択します。  
  
     ![ドメインのインポート ダイアログ ボックスの値](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-02.jpg "ドメインのインポート ダイアログ ボックスの値")  
  
6.  **[OK]** をクリックして **[ドメイン値のインポート]** ダイアログ ボックスを閉じます。 インポートしたすべての州の名前が一覧に表示されます。 インポート後は、 **[新規のみ表示]** オプションが自動的に選択されます。 値をインポートすると、リスト内の古い値が表示されない、このオプションは自動的にインポートした後有効になっているためにです。 すべての値を表示するには、このチェック ボックスをオフにします。 同じ値のセットをもう一度インポートすると、これらはドメインに既に存在するので、値はインポートされません。  
  
     ![ドメインの値にのみ新しいチェック ボックスを表示する](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-03.jpg "ドメインの値にのみ新しいチェック ボックスを表示します。")  
  
## <a name="next-step"></a>次の手順  
 [タスク 4:ドメイン ルールを設定](../../2014/tutorials/task-4-setting-domain-rules.md)  
  
  
