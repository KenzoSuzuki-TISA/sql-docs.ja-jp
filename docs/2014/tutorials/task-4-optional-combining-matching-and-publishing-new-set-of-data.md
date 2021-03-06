---
title: タスク 4 (省略可能)。結合、照合、および新しいデータ セットの発行 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 13a13f03-b307-4555-8e33-6d98c459d994
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 05c8785427b905138e513ab7134d56def7cdcf4d
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/13/2018
ms.locfileid: "53353072"
---
# <a name="task-4-optional-combining-matching-and-publishing-new-set-of-data"></a>タスク 4 (省略可能)。新しいデータ セットを結合、照合、およびパブリッシュする
  後で、MDS リポジトリにさらにデータを追加する場合があります。 データを追加する前に、重複や不正確なデータを追加しないことを確認して、MDS で既に管理されているデータを新しいデータを比較に役立ちます。 Excel 用マスター データ サービス アドインを使用すると、データを MDS にパブリッシュする前に、2 つのワークシートのデータを結合し、データを比較することで重複を識別して削除できます。 MDS Excel アドインの照合機能は、データの一致を識別するための DQS 照合機能を使用します。 ここでは、MDS にパブリッシュする前に、2 つのワークシートのデータを 1 つに結合し、重複を識別して削除するための照合作業を行います。 参照してください[Excel 用 MDS アドインでのデータ品質照合](https://msdn.microsoft.com/library/hh548681.aspx)と[データの結合](https://msdn.microsoft.com/library/hh548680.aspx)詳細についてはトピック。  
  
1.  新しいインスタンスを起動**Excel**します。 をクリックして**開始**、 をポイント**実行**、型**Excel**、 をクリック**OK**します。  
  
2.  切り替えて、**マスター データ** タブをクリックして**マスター データ**メニュー バーでします。  
  
3.  をクリックして**Connect**リボンで、**接続と読み込み**グループへの接続に、 **MDS サーバー**。 この接続は、このレッスンの前の手順で構成しました。  
  
     ![Excel - エクスプ ローラー ボタンを表示するマスター データ ボタンで](../../2014/tutorials/media/et-combinematchandpublishnewsod-01.jpg "Excel - [マスター データ] ボタン エクスプ ローラーボタンを表示します。")  
  
4.  表示する必要があります、**マスター データ エクスプ ローラー**右側のウィンドウ。 マスター データ エクスプ ローラーが表示されない場合はクリックして**エクスプ ローラーの**リボンのボタンをクリックします。  
  
5.  **マスター データ エクスプ ローラー**ウィンドウで、 **Suppliers**のドロップダウン リストで、**モデル**します。 モデルに 1 個のエンティティ **サプライヤー**します。  
  
     ![Excel - マスター データ エクスプ ローラー ウィンドウ](../../2014/tutorials/media/et-combinematchandpublishnewsod-02.jpg "Excel - [マスター データ エクスプ ローラー] ウィンドウ")  
  
6.  ダブルクリック**業者**にエンティティ メンバーを Excel ワークシートに読み込むエンティティの一覧でします。  
  
7.  クリックして**Sheet2**下部に切り替えるには、 **Sheet2**タブ。表示されない場合**Sheet2**、新しいワークシートを追加します。  
  
8.  開いている**Suppliers.xls**ファイル (元の入力ファイルは、チュートリアル ファイルに含まれている) と (3) すべての行をコピー、 **CombineAndCleanse**ワークシート**Sheet2**します。  
  
9. 戻り、 **Supplier**シートに、**書籍 1 - Microsoft Excel** (いない、 **Cleansed and Matched Supplier List** Excel) に接続されている**MDS**.  
  
10. クリックして**マスター データ**メニュー バーでします。  
  
11. クリックして**データの結合**リボン上。 表示されます、**データの結合** ダイアログ ボックス。  
  
12. **データの結合** ダイアログ ボックスで、次に、ボタンをクリックして**MDS データと結合する範囲**テキスト ボックスの次の図のようにします。  
  
     ![Excel - データ ダイアログ ボックスの結合](../../2014/tutorials/media/et-combinematchandpublishnewsod-03.jpg "Excel - 結合データ ダイアログ ボックス")  
  
13. これで、ダイアログ ボックスは圧縮表示されます。 をクリックして**Sheet2**に切り替える、 **Sheet2**を 4 つの行 (1 つのヘッダー行を含む) を含む新しい仕入先データを持つタブ。  
  
14. **Sheet2**を選択します**ヘッダー行を含むすべての行**(既に選択されているような) 場合も同様です。 表示する必要があります、 **MDS データと結合する範囲**が自動的に更新します。  
  
     ![Excel - 結合データ ダイアログ ボックス - 最小](../../2014/tutorials/media/et-combinematchandpublishnewsod-04.jpg "Excel - 結合データ ダイアログ ボックス - 最小化")  
  
15. 戻り、 **Suppliers**閉じず タブ、**データの結合** ダイアログ ボックス。  
  
16. をクリックして、**ボタン**横に、**テキスト ボックス**します。 これで、ダイアログ ボックスは展開表示されます。 列の間のすべてのマッピングを表示する必要があります、 **Supplier** MDS**エンティティ**に**Excel**列が自動的に設定されます。  
  
     ![Excel - データが格納されたデータ ダイアログ ボックスの結合](../../2014/tutorials/media/et-combinematchandpublishnewsod-05.jpg "Excel - 結合データが格納されたデータ ダイアログ ボックス")  
  
17. いることを確認**コード**エンティティの列にマップされます、 **SupplierID**ワークシート内の列と**郵便番号/zip Code**エンティティの列にマップされます、 **の郵便番号/zipCode**ワークシート内の列。  
  
18. **データの結合**ダイアログ ボックスで、をクリックして**結合**します。  
  
19. 3 つのデータ行がワークシートの下部に追加され、色分けされていることを確認してください。  
  
     ![Excel - 結合後の新しい要素](../../2014/tutorials/media/et-combinematchandpublishnewsod-06.jpg "Excel - 結合後の新しい要素")  
  
20. をクリックして**数学データ**重複を識別するために、リボン上。 この機能は、DQS の照合機能を使用します。  
  
21. **データの照合**ダイアログ ボックスで、 **Suppliers**の**DQS ナレッジ ベース**します。  
  
     ![Excel - [データ] ダイアログ ボックスの一致](../../2014/tutorials/media/et-combinematchandpublishnewsod-07.jpg "Excel - [データ] ダイアログ ボックスの一致")  
  
22. 次の表のようにワークシートの列をドメインにマップします。  
  
    |ワークシートの列|[ドメイン]|  
    |----------------------|------------|  
    |Code (MDS の Supplier エンティティ用にコードとしてアップロードした仕入先の ID)|Supplier ID|  
    |Name (Supplier エンティティの名前として MDS にアップロードした仕入先の名前)|Supplier Name|  
    |ContactEmailAddress|ContactEmail|  
  
23. 選択**前提条件となる**の**コード**列のマッピング。  
  
24. 入力**70%** として、**重み**の**Supplier Name**と**30%** として、**重み**の**Contact Email**図のようにします。  
  
25. **[OK]** をクリックします。  
  
26. この照合プロセスでは、**Code:S1**します。  
  
     ![Excel - 照合結果](../../2014/tutorials/media/et-combinematchandpublishnewsod-08.jpg "Excel - 照合結果")  
  
27. 選択、**重複する行 (オレンジ)**、右クリックしをクリックします**削除**行を削除します。  
  
28. 削除、 **CLUSTER_ID**列ため、もはや必要はありません。  
  
29. クリックして**発行**レコードを公開する、他の 2 つ新規に**Codes S66**と**S57**を MDS にします。  
  
30. **パブリッシュと注釈設定** ダイアログ ボックスで、追加、**注釈**、 をクリック**発行**します。  
  
31. 切り替えて、**マスター データ マネージャー Web アプリケーション**します。  
  
32. ホーム ページで、確認**Suppliers**が選択されている、**モデル**、 をクリック**エクスプ ローラー**します。 既にある場合、**エクスプ ローラー**を開き、インターネット ブラウザーを更新します。  
  
33. **並べ替え**によって一覧**コード**でレコードを検索および**S57**と**S66**コードとして。 使用することも、**フィルター**ツールバーの一覧で特定のレコードを検索します。  
  
34. これで、閉じる**Book1 - Microsoft Excel**ファイルを保存せずにウィンドウ。  
  
## <a name="next-step"></a>次の手順  
 [タスク 5:Excel からドメイン ベースの属性を作成します。](../../2014/tutorials/task-5-creating-a-domain-based-attribute-from-excel.md)  
  
  
