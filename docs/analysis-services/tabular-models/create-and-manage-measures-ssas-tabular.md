---
title: 作成し、Analysis Services 表形式モデルでメジャーの管理 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1c3794d9ed2927cf86b9aada08588f71b3a55b8a
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072609"
---
# <a name="create-and-manage-measures"></a>作成し、メジャーの管理 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  メジャーとは、レポートまたは Excel ピボットテーブル (またはピボットグラフ) で使用するために作成される数式のことです。 COUNT や SUM などの標準の集計関数に基づいてメジャーを作成することも、DAX を使用して独自の数式を定義することもできます。 このトピックの実習では、作成し、テーブルのメジャー グリッドを使用してメジャーを管理する方法について説明します。  
  
## <a name="tasks"></a>処理手順  
 作成し、メジャーの管理は、テーブルのメジャー グリッドを使用します。 テーブルのメジャー グリッドは、モデル デザイナーのデータ ビューのみで表示することができます。 ダイアグラム ビューでは、メジャーの作成もメジャー グリッドの表示もできません。ただし、既存のメジャーであれば、ダイアグラム ビューで表示できます。 あるテーブルのメジャー グリッドを表示するには、 **[テーブル]** メニューをクリックしてから **[メジャー グリッドの表示]** をクリックします。  
  
###  <a name="bkmk_create_stand"></a> 標準の集計式を使用してメジャーを作成するには  
  
-   メジャーを作成する列をクリックし、 **[列]** メニューをクリックしてから **[オート SUM]** をポイントし、集計の種類をクリックします。  
  
     既定名を持つメジャー、そしてその後に数式が列の直下にあるメジャー グリッドの最初のセルに自動的に作成されます。  
  
###  <a name="bkmk_create_custom"></a> カスタム式を使用してメジャーを作成するには  
  
-   メジャー グリッド内のメジャーを作成する列の下で、任意のセルをクリックしてから、数式バーに名前、コロン (:)、等号 (=)、および数式を続けて入力します。 Enter キーを押して数式を確定します。  
  
###  <a name="bkmk_edit"></a> メジャー プロパティを編集するには  
  
-   メジャー グリッド内で、メジャーをクリックしてから **[プロパティ]** ウィンドウで別のプロパティ値を入力するか選択します。  
  
###  <a name="bkmk_rename"></a> メジャー名を変更するには  
  
-   メジャー グリッド内で、メジャーをクリックしてから **[プロパティ]** ウィンドウの **[メジャー名]** ボックスに新しい名前を入力し、Enter キーを押します。  
  
     数式バー内でメジャーの名前を変更することもできます。 メジャー名の後に数式を付け、その後にコロンを付けます。  
  
###  <a name="bkmk_delete"></a> メジャーを削除するには  
  
-   メジャー グリッドで、メジャーを右クリックしてから **[削除]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [メジャー](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [Kpi](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [計算列](../../analysis-services/tabular-models/ssas-calculated-columns.md)  
  
  
