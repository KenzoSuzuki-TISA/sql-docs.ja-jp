---
title: TOKENCOUNT (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1c0efed1-c2b3-4f20-a3a1-ad91283b7c0a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d449e6245b779fd281fc9c8f047a9eb352d56846
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52822766"
---
# <a name="tokencount-ssis-expression"></a>TOKENCOUNT (SSIS 式)
  指定された区切り記号で区切られたトークンを含んでいる文字列内のトークン数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
TOKENCOUNT(character_expression, delimiter_string)  
```  
  
## <a name="arguments"></a>引数  
 *character_expression*  
 区切り記号で区切られたトークンを含む文字列です。  
  
 *delimiter_string*  
 区切り記号を含む文字列です。 たとえば、"; ," には 3 つの区切り記号 (セミコロン、空白、コンマ) が含まれています。  
  
## <a name="result-types"></a>戻り値の型  
 DT_I4  
  
## <a name="remarks"></a>コメント  
 TOKEN 関数には次の解説が適用されます。  
  
-   区切り記号には 1 つ以上の区切り文字を含めることができます。  
  
-   先頭の区切り記号はスキップされます。  
  
-   TOKENCOUNT は、DT_WSTR データ型でのみ機能します。 *character_expression* 引数が DT_STR データ型の文字列リテラルまたはデータ列である場合は、TOKEN による演算の実行前に、暗黙的に DT_WSTR データ型にキャストされます。 その他のデータ型は、明示的に DT_WSTR データ型にキャストされる必要があります。  
  
-   character_expression が NULL の場合、TOKENCOUNT は 0 (ゼロ) を返します。  
  
-   この式の引数として、変数と列を使用できます。  
  
## <a name="expression-examples"></a>式の例  
 次の例では、TOKENCOUNT 関数は、文字列には、3 つのトークンが含まれているために 3 を返します。「01」、「12」、「2011」。  
  
```  
TOKENCOUNT("01/12/2011", "/")  
```  
  
 次の例では、TOKENCOUNT 関数は 4 を返します。これは、文字列に 4 つのトークン ("a"、"little"、"white"、および "dog") が含まれているためです。  
  
```  
TOKENCOUNT("a little white dog"," ")  
```  
  
 次の例では、TOKENCOUNT 関数は 1 を返します。 関数は区切り記号に対応する入力文字列を解析しますが、文字列には区切り記号が含まれていないため、文字列全体を最初のトークンとして加算します。  
  
```  
TOKENCOUNT("a little white dog","|")  
```  
  
 次の例では、TOKENCOUNT 関数は 4 を返します。 この例では、5 つの区切り記号が指定されています。 入力文字列には 4 つのトークン ("a"、"little"、"white"、および "dog") が含まれています。  
  
```  
TOKENCOUNT("a:little|white dog","| ,.:")  
```  
  
 次の例では、TOKENCOUNT 関数は 4 を返します。 先頭の空白文字はすべて無視されます。  
  
```  
TOKENCOUNT("        a little white dog", " ")  
```  
  
## <a name="see-also"></a>参照  
 [関数 (SSIS 式)](functions-ssis-expression.md)  
  
  
