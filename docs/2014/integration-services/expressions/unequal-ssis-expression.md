---
title: '!= (等しくない) (SSIS 式) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- unequal operator (!=)
- '!= (not equal to)'
ms.assetid: fad20e85-c0e6-42bf-af70-2bc80ee09be5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b7df4340e2dc54a2c30b1c5693efeda26ecc9b3b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52785524"
---
# <a name="-unequal-ssis-expression"></a>!= (等しくない) (SSIS 式)
  互換性のあるデータ型の 2 つの式が等しくないかどうかを判別するための比較を実行します。 式エバリュエーターは、比較の実行前にさまざまなデータ型を自動的に変換します。  
  
 ただし、一部のデータ型では、式を正常に評価する前に明示的なキャストを含む必要がある場合があります。 データ型間の有効なキャストについて詳しくは、「[Cast &#40;SSIS 式&#41;](cast-ssis-expression.md)」をご覧ください。  
  
## <a name="syntax"></a>構文  
  
```  
  
expression1 != expression2  
  
```  
  
## <a name="arguments"></a>引数  
 *expression1、expression2*  
 有効な式を指定します。  
  
## <a name="result-types"></a>戻り値の型  
 DT_BOOL  
  
## <a name="remarks"></a>コメント  
 比較する式のいずれかが NULL の場合、比較結果は NULL になります。 両方の式が NULL の場合も、結果は NULL になります。  
  
 設定する式の *expression1* と *expression2*は、次のいずれかのルールに従う必要があります。  
  
-   **数値** *expression1* と *expression2* の両方が数値データ型である必要があります。 データ型の積集合は、式エバリュエーターが実行する暗黙的な数値変換に関する規則で指定されているように、数値データ型である必要があります。 2 つの数値データ型の積集合を NULL にすることはできません。 詳しくは、「 [式における Integration Services データ型](integration-services-data-types-in-expressions.md)」をご覧ください。  
  
-   **文字** *expression1* と *expression2* は、どちらも DT_STR または DT_WSTR データ型に評価される必要があります。 2 つの式が評価される文字列データ型は、異なっていてもかまいません。  
  
    > [!NOTE]  
    >  文字列の比較では、大文字と小文字、アクセント、かな、および文字幅が区別されます。  
  
-   **日付、時刻、または日付/時刻**両方*expression1*と*expression2*次のデータ型のいずれかを評価する必要があります。DT_DBDATE、DT_DATE、DT_DBTIME、DT_DBTIME2、DT_DBTIMESTAMP、DT_DBTIMESTAMP2、DT_DBTIMESTAPMOFFSET、または DT_FILETIME。  
  
    > [!NOTE]  
    >  時刻データ型に評価される式と、日付データ型または日付/時刻データ型に評価される式との間の比較はサポートされていません。 システムによってエラーが生成されます。  
  
     式の比較の際は、次の変換規則が記載順に適用されます。  
  
    -   2 つの式が同じデータ型に評価される場合、そのデータ型の比較が実行されます。  
  
    -   一方の式が DT_DBTIMESTAMPOFFSET データ型の場合、もう一方の式が暗黙的に DT_DBTIMESTAMPOFFSET に変換され、DT_DBTIMESTAMPOFFSET の比較が実行されます。 詳しくは、「 [式における Integration Services データ型](integration-services-data-types-in-expressions.md)」をご覧ください。  
  
    -   一方の式が DT_DBTIMESTAMP2 データ型の場合、もう一方の式が暗黙的に DT_DBTIMESTAMP2 に変換され、DT_DBTIMESTAMP2 の比較が実行されます。  
  
    -   一方の式が DT_DBTIME2 データ型の場合、もう一方の式が暗黙的に DT_DBTIME2 に変換され、DT_DBTIME2 の比較が実行されます。  
  
    -   一方の式が DT_DBTIMESTAMPOFFSET、DT_DBTIMESTAMP2、DT_DBTIME2 のいずれの型でもない場合、両方の式が DT_DBTIMESTAMP データ型に変換されてから比較が実行されます。  
  
     式の比較は、次の前提に基づいて実行されます。  
  
    -   それぞれの式のデータ型に秒の小数部が含まれている場合、秒の小数部の桁数が最も少ないデータ型の残りの桁の値は 0 と見なされます。  
  
    -   それぞれの式が日付データ型であり、一方のみにタイム ゾーン オフセットがある場合、タイム ゾーン オフセットがない日付データ型は協定世界時 (UTC) と見なされます。  
  
-   **論理** *expression1* と *expression2* は、どちらもブール型に評価される必要があります。  
  
-   **GUID** *expression1* と *expression2* は、どちらも DT_GUID データ型に評価される必要があります。  
  
-   **バイナリ** *expression1* と *expression2* は、どちらも DT_BYTES データ型に評価される必要があります。  
  
-   **BLOB**両方*expression1*と*expression2*同じバイナリ ラージ オブジェクト ブロック (BLOB) データ型に評価される必要があります。DT_TEXT、DT_NTEXT、または DT_IMAGE です。  
  
 データ型について詳しくは、「 [Integration Services のデータ型](../data-flow/integration-services-data-types.md)」をご覧ください。  
  
## <a name="expression-examples"></a>式の例  
 現在の日付が 2003 年 7 月 4 日ではない場合にのみ、この例の結果は TRUE に評価されます。 詳しくは、「[GETDATE &#40;SSIS 式&#41;](getdate-ssis-expression.md)」をご覧ください。  
  
```  
"7/4/2003" != GETDATE()  
```  
  
 **ListPrice** 列の値が 500 でない場合、この例の結果は TRUE に評価されます。  
  
```  
ListPrice != 500  
```  
  
 この例では、変数 **LPrice**を使用しています。 **LPrice** の値が 500 でない場合、この例の結果は TRUE に評価されます。 式を解析するためには、この変数のデータ型は数値である必要があります。  
  
```  
@LPrice != 500  
```  
  
## <a name="see-also"></a>参照  
 [== &#40;等しい&#41; &#40;SSIS 式&#41;](equal-ssis-expression.md)   
 [演算子の優先順位と結合規則](operator-precedence-and-associativity.md)   
 [演算子 &#40;SSIS 式&#41;](operators-ssis-expression.md)  
  
  
