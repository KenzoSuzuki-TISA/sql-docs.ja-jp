---
title: 量化式 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- universal quantifiers
- effective Boolean value [XQuery]
- quantified expressions [XQuery]
- XQuery, quantified expressions
- every expression [XQuery]
- existential quantifiers [XQuery]
- some expression [XQuery]
- EBV
- expressions [XQuery], quantifiers
ms.assetid: a3a75a6c-8f67-4923-8406-1ada546c817f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 413a9519cbfcb036c5e7242889c4eaf4ec89d413
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52515393"
---
# <a name="quantified-expressions-xquery"></a>量化式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  存在量化子と全称量化子により、2 つのシーケンスに適用されるブール演算子に異なるセマンティクスが指定されます。 次に、各用語について説明します。  
  
 *存在量化子*  
 2 つのシーケンスがあるときに、最初のシーケンスの中に、使用される比較演算子に基づいて 2 番目のシーケンスと一致するアイテムがある場合、True が返されます。  
  
 *ユニバーサル量指定子*  
 2 つのシーケンスがあるときに、最初のシーケンスのすべてのアイテムが 2 番目のシーケンスと一致する場合、True が返されます。  
  
 XQuery では、次の形式の量化式がサポートされます。  
  
```  
( some | every ) <variable> in <Expression> (,...) satisfies <Expression>  
```  
  
 これらの式をクエリで使用して、存在量化または全称量化を明示的に式の 1 つ以上のシーケンスに適用できます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、`satisfies` 句の式の結果が、ノード シーケンス、空のシーケンス、ブール値のいずれかになる必要があります。 この式の結果の有効なブール値が、量化に使用されます。 使用する存在量化**一部**真の結果を式では、量化子によりバインドされた値の少なくとも 1 つの場合は True を返します。 使用する全称**すべて**量化子によりバインドされたすべての値の True である必要があります。  
  
 たとえば、次のクエリのチェックすべて\<場所 > 要素に LocationID 属性があるかどうかを参照してください。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        if (every $WC in //AWMI:root/AWMI:Location   
            satisfies $WC/@LocationID)  
        then  
             <Result>All work centers have workcenterLocation ID</Result>  
         else  
             <Result>Not all work centers have workcenterLocation ID</Result>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 LocationID はの必須の属性があるため、\<場所 > 要素、期待される結果が表示されます。  
  
```  
<Result>All work centers have Location ID</Result>   
```  
  
 使用する代わりに、 [query() メソッド](../t-sql/xml/query-method-xml-data-type.md)、使用することができます、 [value() メソッド](../t-sql/xml/value-method-xml-data-type.md)にリレーショナルの世界では、次のクエリで示すように結果を返します。 このクエリでは、すべてのワーク センターの場所に LocationID 属性が含まれている場合に True が返されます。 それ以外の場合は False が返されます。  
  
```  
SELECT Instructions.value('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        every $WC in  //AWMI:root/AWMI:Location   
            satisfies $WC/@LocationID',   
  'nvarchar(10)') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 次のクエリでは、製品の写真の中に小さいサイズの写真があるかどうかを確認します。 製品カタログ XML には、さまざまな角度で撮影されたサイズの異なる製品の写真が格納されています。 各製品カタログ XML にサイズの小さい写真が少なくとも 1 枚含まれているようにすることができます。 これを行うには、次のクエリを実行します。  
  
```  
SELECT ProductModelID, CatalogDescription.value('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     some $F in /PD:ProductDescription/PD:Picture  
        satisfies $F/PD:Size="small"', 'nvarchar(20)') as SmallPicturesStored  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 これは、結果の一部です。  
  
```  
ProductModelID SmallPicturesStored   
-------------- --------------------  
19             true        
```  
  
## <a name="implementation-limitations"></a>実装の制限事項  
 制限事項を次に示します。  
  
-   量化式の変数をバインドする操作の一部として、型のアサーションはサポートされません。  
  
## <a name="see-also"></a>参照  
 [XQuery 式](../xquery/xquery-expressions.md)  
  
  
