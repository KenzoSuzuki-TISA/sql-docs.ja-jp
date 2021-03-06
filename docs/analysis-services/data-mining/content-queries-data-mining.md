---
title: コンテンツ クエリ (データ マイニング) |Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 20d730ed2fd975d800b27882ecc218f7ce1868b3
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52529048"
---
# <a name="content-queries-data-mining"></a>コンテンツ クエリ (データ マイニング)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  コンテンツ クエリは、マイニング モデルの内部の統計および構造に関する情報を抽出するための手段です。 コンテンツ クエリを使用すると、ビューアーでは簡単に得られない詳細な情報がわかる場合があります。 また、コンテンツ クエリの結果を利用して、他の用途のためにプログラムで情報を抽出できます。  
  
 ここでは、コンテンツ クエリを使用して取得できる情報の種類に関する一般的な情報と、コンテンツ クエリの一般的な DMX 構文を紹介します。  
  
 [基本的なコンテンツ クエリ](#bkmk_ContentQuery)  
  
-   [構造およびケース データに対するクエリ](#bkmk_Structure)  
  
-   [モデル パターンに対するクエリ](#bkmk_Patterns)  
  
 [使用例](#bkmk_Examples)  
  
-   [アソシエーション モデルに対するコンテンツ クエリ](#bkmk_Assoc)  
  
-   [デシジョン ツリー モデルに対するコンテンツ クエリ](#bkmk_DecTree)  
  
 [クエリ結果の操作](#bkmk_Results)  
  
##  <a name="bkmk_ContentQuery"></a> 基本的なコンテンツ クエリ  
 コンテンツ クエリは、予測クエリ ビルダーを使用しても作成できます。SQL Server Management Studio で提供される DMX コンテンツ クエリ テンプレートを使用するか、DMX に直接クエリを書き込みます。 コンテンツ クエリは、予測クエリと異なり、外部データを結合する必要がないため、簡単に書き込むことができます。  
  
 ここでは、作成できるコンテンツ クエリの種類の概要について説明します。  
  
-   マイニング構造またはケース データに対するクエリでは、トレーニングに使用された詳細なデータを表示できます。  
  
-   モデルに対するクエリでは、パターン、属性一覧、数式などが返されます。  
  
###  <a name="bkmk_Structure"></a> 構造およびケース データに対するクエリ  
 DMX では、マイニング構造およびモデルの構築に使用されるキャッシュ データに対するクエリをサポートしています。 既定では、このキャッシュは、マイニング構造が定義されると作成され、構造またはモデルが処理されると値が設定されます。  
  
> [!WARNING]  
>  データをトレーニング セットとテスト セットに分割する必要がある場合は、このキャッシュを消去または削除できません。 キャッシュを消去すると、ケース データに対するクエリを実行できなくなります。  
  
 次の例は、ケース データに対するクエリ、またはマイニング構造のデータに対するクエリを作成するときに共通するパターンを示しています。  
  
 **モデルのすべてのケースを取得する**  
 `SELECT FROM <model>.CASES`  
  
 このステートメントを使用すると、モデルの構築に使用されたケース データから指定した列を所得できます。 このクエリを実行するには、モデルのドリルスルー権限を持っている必要があります。  
  
 **構造に含まれているすべてのデータを表示する**  
 `SELECT FROM <structure>.CASES`  
  
 このステートメントを使用すると、特定のマイニング モデルには含まれていない列も含め、構造に含まれているデータをすべて表示できます。 マイニング構造からデータを取得するには、モデルと構造の両方に対するドリルスルー権限を持っている必要があります。  
  
 **値の範囲を取得する**  
 `SELECT DISTINCT RangeMin(<column>), RangeMax(<column>) FROM <model>`  
  
 このステートメントを使用すると、連続列または DISCRETIZED 列のバケットの最小値、最大値、および平均を取得できます。  
  
 **個別の値を取得する**  
 `SELECT DISTINCT <column>FROM <model>`  
  
 このステートメントを使用すると、DISCRETE 列のすべての値を取得できます。  DISCRETIZED 列に対してはこのステートメントを使用せずに、 **RangeMin** 関数および **RangeMax** 関数を使用してください。  
  
 **モデルまたは構造のトレーニングに使用されたケースを取得する**  
 `SELECT  FROM <mining structure.CASES WHERE IsTrainingCase()`  
  
 このステートメントを使用すると、モデルのトレーニングに使用されたデータの完全なセットを取得できます。  
  
 **モデルまたは構造のテストに使用されたケースを取得する**  
 `SELECT  FROM <mining structure.CASES WHERE IsTestingCase()`  
  
 このステートメントを使用すると、特定の構造に関連するマイニング モデルのテスト用に確保されているデータを取得できます。  
  
 **特定のモデル パターンから基になるケース データにドリルスルーする**  
 `SELECT FROM <model>.CASESWHERE IsTrainingCase() AND IsInNode(<node>)`  
  
 このステートメントを使用すると、トレーニング済みのモデルから詳細なケース データを取得できます。 特定のノードを指定する必要があります。たとえば、クラスターのノード ID、デシジョン ツリーの特定の分岐などを認識している必要があります。また、このクエリを実行するには、モデルのドリルスルー権限を持っている必要があります。  
  
###  <a name="bkmk_Patterns"></a> モデル パターン、統計、および属性に対するクエリ  
 データ マイニング モデルのコンテンツは、多くの目的で役に立ちます。 モデル コンテンツのクエリを使用すると、以下の操作を実行できます。  
  
-   独自の計算を行うために式または確率を抽出します。  
  
-   アソシエーション モデルでは、予測の生成に使用される規則を取得します。  
  
-   特定のルールをカスタム アプリケーションで使用できるようにそのルールの説明を取得します。  
  
-   時系列モデルで検出された移動平均を表示します。  
  
-   傾向線のセグメントの回帰式を取得します。  
  
-   特定のクラスターの一部として識別された顧客に関する実用的な情報を取得します。  
  
 次の例は、モデル コンテンツに対するクエリの作成に共通するパターンを示しています。  
  
 **モデルからパターンを取得する**  
 `SELECT FROM <model>.CONTENT`  
  
 このステートメントを使用すると、モデル内の特定のノードに関する詳細情報を取得できます。 ノードには、アルゴリズムの種類に応じて、ルールと式、サポート、分散の統計情報などが含まれています。  
  
 **トレーニング済みのモデルで使用された属性を取得する**  
 `CALL System.GetModelAttributes(<model>)`  
  
 このストアド プロシージャを使用すると、モデルによって使用された属性の一覧を取得できます。 たとえば、この情報は、機能を選択したために除外された属性を特定するのに役立ちます。  
  
 **データ マイニング ディメンションに格納されているコンテンツを取得する**  
 `SELECT FROM <model>.DIMENSIONCONTENT`  
  
 このステートメントを使用すると、データ マイニング ディメンションからデータを取得できます。  
  
 この種類のクエリは主に、内部で使用するためのものです。 ただし、この機能はすべてのアルゴリズムでサポートされているわけではありません。 サポートされているかどうかは、MINING_SERVICES スキーマ行セット内のフラグで示されます。  
  
 独自のプラグイン アルゴリズムを開発する場合は、このステートメントを使用してテスト用のモデルのコンテンツを確認できます。  
  
 **モデルの PMML 表現を取得する**  
 `SELECT * FROM <model>.PMML`  
  
 PMML 形式でモデルを表す XML ドキュメントを取得します。 すべてのモデルの種類がサポートされているわけではありません。  
  
##  <a name="bkmk_Examples"></a> 使用例  
 すべてのアルゴリズムに対して標準であるようなモデル コンテンツもありますが、一部のコンテンツは、そのモデルの構築に使用したアルゴリズムによってかなり異なります。 したがって、コンテンツ クエリを作成する際には、特定のモデルに関してどのような情報が最も有用であるかを把握しておく必要があります。  
  
 ここでは、アルゴリズムの選択がモデルに保存されている情報の種類にどのように影響するかを、例を使用して説明します。 マイニング モデル コンテンツ、および各種のモデルに特有のコンテンツの詳細については、「[マイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)」を参照してください。  
  
###  <a name="bkmk_Assoc"></a> 例 1:アソシエーション モデルに対するコンテンツ クエリ  
 `SELECT FROM <model>.CONTENT`ステートメントは、クエリの対象となるモデルの種類に応じてさまざまな種類の情報を返します。 アソシエーション モデルの場合、重要な情報は *ノード型*です。 ノードは、モデル コンテンツの情報のコンテナーのようなものです。 アソシエーション モデルでは、ルールを表すノードは NODE_TYPE の値が 8 で、アイテムセットを表すノードは NODE_TYPE の値が 7 です。  
  
 したがって、次のクエリでは、サポートで順位付けされた (既定の順序) 上位 10 個のアイテムセットが返されます。  
  
```  
SELECT TOP 10 NODE_DESCRIPTION, NODE_PROBABILITY, SUPPORT  
FROM <model>.CONTENT WHERE NODE_TYPE = 7  
```  
  
 次のクエリはこの情報に対して構築されます。 クエリは 3 つの列を返します: ノード、完全なルール、およびアイテム セットの右側にある製品の ID のアイテム セットの一部として他の製品に関連する予測された製品は、します。  
  
```  
SELECT FLATTENED NODE_UNIQUE_NAME, NODE_DESCRIPTION,  
     (SELECT RIGHT(ATTRIBUTE_NAME, (LEN(ATTRIBUTE_NAME)-LEN('Association model name')))   
FROM NODE_DISTRIBUTION  
WHERE LEN(ATTRIBUTE_NAME)>2  
)   
AS RightSideProduct  
FROM [<Association model name>].CONTENT  
WHERE NODE_TYPE = 8   
ORDER BY NODE_SUPPORT DESC  
```  
  
 FLATTENED キーワードは、入れ子になった行セットをフラット テーブルに変換することを示します。 ルールの右辺の製品を表す属性は、NODE_DISTRIBUTION テーブルに含まれています。したがって、長さが 2 より大きいという要件を追加して、属性名を含む行のみを取得しています。  
  
 また、単純な文字列関数を使用して、3 番目の列からモデルの名前を削除しています (通常、モデル名は入れ子になった列の値の先頭に含まれています)。  
  
 WHERE 句で NODE_TYPE の値を 8 として指定して、ルールのみを取得しています。  
  
 例については、「 [結合モデルのクエリ例](../../analysis-services/data-mining/association-model-query-examples.md)」を参照してください。  
  
###  <a name="bkmk_DecTree"></a> 例 2:デシジョン ツリー モデルに対するコンテンツ クエリ  
 デシジョン ツリー モデルは、予測や分類のために使用できます。  この例では、結果を予測するためにモデルを使用していますが、結果の分類に使用できる要因またはルールを見つけることもできます。  
  
 デシジョン ツリー モデルでは、ノードはツリーとリーフ ノードの両方を表すために使用されます。 各ノードのキャプションに結果へのパスの説明が含まれています。 したがって、特定の結果のパスをトレースするには、そのパスを含むノードを識別して、そのノードの詳細を取得する必要があります。  
  
 予測クエリでは、次の例のように、予測関数 [PredictNodeId &#40;DMX&#41;](../../dmx/predictnodeid-dmx.md) を追加して関連するノードの ID を取得できます。  
  
```  
SELECT  Predict([Bike Buyer]), PredictNodeID([Bike Buyer])   
FROM [<decision tree model name>]  
PREDICTION JOIN   
<input rowset>   
```  
  
 結果を含むノードの ID がわかれば、次のように NODE_CAPTION を含むコンテンツ クエリを作成して、その予測を説明するルール (パス) を取得できます。  
  
```  
SELECT NODE_CAPTION  
FROM [<decision tree model name>]   
WHERE NODE_UNIQUE_NAME= '<node id>'  
```  
  
 例については、「 [デシジョン ツリー モデルのクエリ例](../../analysis-services/data-mining/decision-trees-model-query-examples.md)」を参照してください。  
  
##  <a name="bkmk_Results"></a> クエリ結果の操作  
 例が示すように、多くの場合、コンテンツ クエリは表形式の行セットを返しますが、入れ子になった列からの情報も含まれます。 返された行セットはフラット化できますが、結果の操作が複雑になります。 特に、NODE_DISTRIBUTION ノードのコンテンツはネスト化されていますが、モデルに関して非常に興味深い情報を含みます。  
  
 階層的な行セットの操作方法の詳細については、MSDN で OLEDB の仕様を参照してください。  
  
## <a name="see-also"></a>参照  
 [DMX 選択ステートメントについて](../../dmx/understanding-the-dmx-select-statement.md)   
 [データ マイニング クエリ](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
