---
title: テキスト ボックス内のテキストの書式設定 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: df0794b5-96b0-4034-bd17-1be7f31e29db
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 7816944c854f7c7482902d4f681d54e295b05fff
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540004"
---
# <a name="format-text-in-a-text-box-report-builder-and-ssrs"></a>テキスト ボックス内のテキストの書式設定 (レポート ビルダーおよび SSRS)
  テキスト ボックス内のテキストは、どの部分も個別に書式設定できます。また、1 つのテキスト ボックスに、プレースホルダー テキストと静的テキストを混在させることができます。 複数の書式を混在させ、プレースホルダー テキストを追加できるこの機能により、文書の差し込みを行ったり、レポート内のテキストに使用するテンプレートを作成したりできます。 プレースホルダーを使用することによって、あらゆる式を定義できるほか、それぞれの式に対して、個別に書式を適用することもできます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-combine-multiple-formats-in-a-text-box"></a>テキスト ボックスで複数の書式を混在させるには  
  
1.  **[挿入]** タブの **[テキスト ボックス]** をクリックします。 デザイン画面をクリックし、次にマウスをドラッグして、必要なサイズのボックスを作成します。  
  
2.  テキスト ボックス内で、書式設定の対象となるテキストを選択します。  
  
3.  選択したテキストを右クリックして、 **[テキストのプロパティ]** をクリックします。  
  
4.  書式設定オプションを設定します。 たとえば、 **[全般]** タブには次のオプションがあります。  
  
    -   **[ツールヒント]** : テキスト、または結果がツールヒントになる式を入力します。 ツールヒントは、ユーザーがレポートのアイテムの上にポインターを置いたときに表示されます。  
  
    -   **[マークアップの種類]** : 選択したテキストの表示方法を指定するオプションを選択します。  
  
         **[テキスト形式]** : 選択したテキストを単純なテキストとして表示します。 HTML はリテラル テキストとして処理されます。  
  
         **[HTML]**  : 選択したテキストを HTML として表示します。 プレースホルダーの式の値が有効な HTML タグを含んでいる場合、これらのタグは HTML として表示されます。 詳細については、[「レポートへの HTML のインポート &#40;レポート ビルダーおよび SSRS&#41;](importing-html-into-a-report-report-builder-and-ssrs.md)」を参照してください。  
  
5.  **[OK]** をクリックします。  
  
6.  書式設定の対象となるその他のテキストについても、手順 2. ～ 5. を繰り返します。  
  
### <a name="to-format-text-and-placeholders-differently-in-the-same-text-box"></a>同じテキスト ボックス内のテキストとプレースホルダーの書式を個別に設定するには  
  
1.  **[挿入]** タブの **[一覧]** をクリックします。 デザイン画面をクリックし、次にマウスをドラッグして、必要なサイズのボックスを作成します。 **[データセットのプロパティ]** ダイアログ ボックスが表示されます。 共有データセットまたはレポートに埋め込まれたデータセットを使用できます。 詳細については、「[[クエリ] ([データセットのプロパティ] ダイアログ ボックス) &#40;レポート ビルダー&#41;](../report-data/dataset-properties-dialog-box-query-report-builder.md)」または「[[クエリ] ([データセットのプロパティ] ダイアログ ボックス)](../dataset-properties-dialog-box-query.md)」を参照してください。  
  
2.  **[挿入]** タブの **[テキスト ボックス]** をクリックします。 一覧内をクリックし、次にマウスをドラッグして、必要なサイズのボックスを作成します。  
  
3.  テキスト ボックスのラベルを入力します。たとえば、「**My Field**」と入力します。  
  
4.  データセットからテキスト ボックスにフィールドをドラッグします。 フィールドに対してプレースホルダーが作成されます。  
  
5.  基本的な書式設定の場合は、プレースホルダー テキストを選択し、 **[ホーム]** タブの **[フォント]** グループにある書式設定オプションのいずれかをクリックします。たとえば、**[太字]** ボタンをクリックします。  
  
     詳細な書式設定オプションの場合は、プレースホルダー テキストを右クリックし、 **[プレースホルダー プロパティ]** をクリックします。  
  
6.  **[OK]** をクリックします。 レポート デザイン ビューで、テキスト ボックスに "**My Field**: [*FieldName*]" と表示されます ( *FieldName* はフィールド名)。  
  
7.  **[実行]** をクリックします。  
  
 一覧はフィールド内の値ごとに 1 回繰り返され、プレースホルダー *FieldName* がデータセット内のそのフィールドの値に置き換わります。  
  
## <a name="see-also"></a>参照  
 [テキスト ボックス &#40;レポート ビルダーおよび SSRS&#41;](text-boxes-report-builder-and-ssrs.md)   
 [テキストとプレースホルダーの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [レポートでの式の使用 &#40;レポート ビルダーおよび SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](expression-examples-report-builder-and-ssrs.md)   
 [レポートへの HTML の追加 &#40;レポート ビルダーおよび SSRS&#41;](add-html-into-a-report-report-builder-and-ssrs.md)   
 [一覧 &#40;レポート ビルダーおよび SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [数値と日付の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [[全般] ([プレースホルダーのプロパティ] ダイアログ ボックス) &#40;レポート ビルダーおよび SSRS&#41;](../placeholder-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
