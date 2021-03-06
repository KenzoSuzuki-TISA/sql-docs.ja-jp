---
title: 子 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 03c96a1c90f7ca0a18bd49c371a2ec90582b38f1
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52533414"
---
# <a name="children-mdx"></a>Children (MDX)


  指定されたメンバーの子のセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Member_Expression.Children  
```  
  
## <a name="arguments"></a>引数  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 **子**関数は、指定したメンバーの子を含む自然順序のセットを返します。 指定されているメンバーに子メンバーがない場合、この関数は空のセットを返します。  
  
## <a name="example"></a>例  
 次の例では、Geography ディメンション内の Geography 階層の United States メンバーの子が返されます。  
  
```  
SELECT [Geography].[Geography].[Country].&[United States].Children ON 0  
FROM [Adventure Works]  
```  
  
 次の例は、すべてのメンバーを返します、**メジャー**ディメンション列軸で、すべての計算されるメンバーとのすべての子のセットを含みます、`[Product].[Model Name]`行軸上の階層の属性、を**Adventure Works**キューブ。  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
  
```  
  
|リリース|履歴|  
|-------------|-------------|  
|[!INCLUDE[ssBOL2005_R03](../includes/ssbol2005-r03-md.md)]|**変更内容:**<br /> -わかりやすくするための向上に構文および引数を更新します。<br /><br /> -更新された例を追加しました。|  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
