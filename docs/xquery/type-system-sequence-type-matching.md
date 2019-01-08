---
title: シーケンス型の照合 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence type matching [XQuery]
- XQuery, sequence type matching
ms.assetid: 8c56fb69-ca04-4aba-b55a-64ae216c492d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3df2ef3f14cb8ca4fd7e7bcf5799b6966c16dc10
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52511452"
---
# <a name="type-system---sequence-type-matching"></a>型システム - シーケンス型の照合
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 式の値は必ず 0 個以上のアイテムのシーケンスになります。 アイテムはアトミック値またはノードのいずれかです。 シーケンス型とは、クエリ式から返されたシーケンス型を特定の型と照合する機能のことです。 以下に例を示します。  
  
-   式の値がアトミックの場合、その値が整数型、小数型、または文字列型であるかどうかを確認できます。  
  
-   式の値が XML ノードの場合、その値がコメント ノード、処理命令ノード、またはテキスト ノードであるかどうかを確認できます。  
  
-   式から特定の名前や型の XML 要素または属性ノードが返されるかどうかを確認できます。  
  
 シーケンス型の照合では、`instance of` ブール演算子を使用できます。 詳細については、`instance of`式を参照してください[SequenceType 式&#40;XQuery&#41;](../xquery/sequencetype-expressions-xquery.md)します。  
  
## <a name="comparing-the-atomic-value-type-returned-by-an-expression"></a>式から返されるアトミック値の型の比較  
 式からアトミック値のシーケンスが返される場合、シーケンス内の値の型を確認することが必要な場合があります。 次の例は、シーケンス型の構文を使用して式から返されるアトミック値の型を評価する方法を示しています。  
  
### <a name="example-determining-whether-a-sequence-is-empty"></a>例:シーケンスが空かどうかを判断します。  
 **Empty()** シーケンスの種類は、指定された式で返されるシーケンスが空のシーケンスであるかどうかを確認するシーケンス型の式で使用できます。  
  
 次の例の XML スキーマでは、<`root`> 要素を NULL にできます。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="https://www.w3.org/2001/XMLSchema">  
      <element name="root" nillable="true" type="byte"/>  
</schema>'  
GO  
```  
  
 この場合、型指定された XML インスタンスで <`root`> 要素に値を指定すると、`instance of empty()` から False が返されます。  
  
```  
DECLARE @var XML(SC1)  
SET @var = '<root>1</root>'  
-- The following returns False  
SELECT @var.query('data(/root[1]) instance of  empty() ')  
GO  
```  
  
 インスタンスの <`root`> 要素を NULL にすると、要素の値は空のシーケンスになり、`instance of empty()` から True が返されます。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" />'  
SELECT @var.query('data(/root[1]) instance of  empty() ')  
GO  
```  
  
### <a name="example-determining-the-type-of-an-attribute-value"></a>例:属性値の型を決定します。  
 場合によっては、式から返されるシーケンス型を処理前に評価することが必要なことがあります。 たとえば、ノードが union 型として定義されている XML スキーマを使用している場合です。 次の例では、コレクションの XML スキーマで、値を小数型または文字列型にすることができる union 型として属性 `a` を定義しています。  
  
```  
-- Drop schema collection if it exists.  
-- DROP XML SCHEMA COLLECTION SC.  
-- GO  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="https://www.w3.org/2001/XMLSchema">  
  <element name="root">  
    <complexType>  
       <sequence/>  
         <attribute name="a">  
            <simpleType>  
               <union memberTypes="decimal string"/>  
            </simpleType>  
         </attribute>  
     </complexType>  
  </element>  
</schema>'  
GO  
```  
  
 型指定された XML インスタンスを処理する前に、属性 `a` の値の型を確認できます。 次の例では、属性 `a` の値は小数型です。 そのため、`, instance of xs:decimal` から True が返されます。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root a="2.5"/>'  
SELECT @var.query('data((/root/@a)[1]) instance of xs:decimal')  
GO  
```  
  
 ここで、属性 `a` の値を文字列型に変更します。 この場合でも、`instance of xs:string` から True が返されます。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root a="Hello"/>'  
SELECT @var.query('data((/root/@a)[1]) instance of xs:string')  
GO  
```  
  
### <a name="example-cardinality-in-sequence-expressions"></a>例:シーケンス式のカーディナリティ  
 この例は、シーケンス式のカーディナリティの効果を示しています。 次の XML スキーマでは、バイト型で NULL にできる <`root`> 要素を定義しています。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="https://www.w3.org/2001/XMLSchema">  
      <element name="root" nillable="true" type="byte"/>  
</schema>'  
GO  
```  
  
 次のクエリでは、式により単一のバイト型が返されるので、`instance of` から True が返されます。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root>111</root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte ')   
GO  
```  
  
 <`root`> 要素を NULL にすると、その要素の値は空のシーケンスになります。 つまり、式 `/root[1]` から空のシーケンスが返されます。 したがって、`instance of xs:byte` では False が返されます。 この場合の既定のカーディナリティは 1 であることに注意してください。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"></root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte ')   
GO  
-- result = false  
```  
  
 出現インジケーター (`?`) を追加してカーディナリティを指定すると、シーケンス式から True が返されます。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"></root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte? ')   
GO  
-- result = true  
```  
  
 シーケンス型の式のテストは、次の 2 段階で完了することに注意してください。  
  
1.  最初に、式の型が指定された型と一致するかどうかがテストで判断されます。  
  
2.  次に、型が一致した場合は、式から返されたアイテム数が指定された出現インジケーターと一致するかどうかが判断されます。  
  
 どちらにも該当する場合、`instance of` 式から True が返されます。  
  
### <a name="example-querying-against-an-xml-type-column"></a>例:Xml 型の列に対するクエリを実行します。  
 次の例では、クエリがの Instructions 列に対して指定されて**xml**で入力、[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]データベース。 Instructions 列にはスキーマが関連付けられているので、この列は型指定された XML 列です。 XML スキーマで整数型の `LocationID` 属性が定義されます。 そのため、シーケンス式で、 `instance of xs:integer?` True を返します。  
  
```  
SELECT Instructions.query('   
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
data(/AWMI:root[1]/AWMI:Location[1]/@LocationID) instance of xs:integer?') as Result   
FROM Production.ProductModel   
WHERE ProductModelID = 7  
```  
  
## <a name="comparing-the-node-type-returned-by-an-expression"></a>式から返されるノードの型の比較  
 式からノードのシーケンスが返される場合、シーケンス内のノードの型を確認することが必要な場合があります。 次の例は、シーケンス型の構文を使用して、式から返されるノードの型を評価する方法を示しています。 次のシーケンス型を使用できます。  
  
-   **item()** -シーケンス内の任意の項目に一致します。  
  
-   **node()** -シーケンスがノードであるかどうかを決定します。  
  
-   **processing-instruction()** -式が処理命令を返すかどうかを決定します。  
  
-   **comment()** -式がコメントを返すかどうかを決定します。  
  
-   **document-node()** -式がドキュメント ノードを返すかどうかを決定します。  
  
 次の例は、これらのシーケンス型を示しています。  
  
### <a name="example-using-sequence-types"></a>例:シーケンス型の使用  
 この例では、型指定されていない XML 変数に対して複数のクエリを実行しています。 これらのクエリは、シーケンス型の使用方法を示しています。  
  
```  
DECLARE @var XML  
SET @var = '<?xml-stylesheet href="someValue" type="text/xsl" ?>  
<root>text node  
  <!-- comment 1 -->   
  <a>Data a</a>  
  <!-- comment  2 -->  
</root>'  
```  
  
 最初のクエリでは、式から要素 <`a`> の型指定された値が返されます。 2 つ目のクエリでは、式から要素 <`a`> が返されます。 これらはどちらもアイテムです。 したがって、両方のクエリから True が返されます。  
  
```  
SELECT @var.query('data(/root[1]/a[1]) instance of item()')  
SELECT @var.query('/root[1]/a[1] instance of item()')  
```  
  
 次の 3 つのクエリのすべての XQuery 式では、<`root`> 要素の要素ノードの子が返されます。 そのため、シーケンス型の式 `instance of node()` から True が返され、他の 2 つの式 `instance of text()` と `instance of document-node()` からは False が返されます。  
  
```  
SELECT @var.query('(/root/*)[1] instance of node()')  
SELECT @var.query('(/root/*)[1] instance of text()')  
SELECT @var.query('(/root/*)[1] instance of document-node()')   
```  
  
 次のクエリでは、<`root`> 要素の親はドキュメント ノードなので、`instance of document-node()` 式から True が返されます。  
  
```  
SELECT @var.query('(/root/..)[1] instance of document-node()') -- true  
```  
  
 次のクエリでは、式から XML インスタンスの最初のノードを取得します。 このノードは処理命令ノードなので、`instance of processing-instruction()` 式により True が返されます。  
  
```  
SELECT @var.query('(/node())[1] instance of processing-instruction()')  
```  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 特定の制限事項を次に示します。  
  
-   **document-node()** コンテンツ タイプの構文はサポートされません。  
  
-   **processing-instruction (name)** 構文がサポートされていません。  
  
## <a name="element-tests"></a>要素のテスト  
 要素のテストは、式から返された要素ノードと特定の名前や型を持つ要素ノードを照合する場合に使用します。 次のような要素のテストを使用できます。  
  
```  
element ()  
element(ElementName)  
element(ElementName, ElementType?)   
element(*, ElementType?)  
```  
  
## <a name="attribute-tests"></a>属性のテスト  
 属性のテストでは、式から返された属性が属性ノードであるかどうかが判断されます。 次のような属性のテストを使用できます。  
  
 `attribute()`  
  
 `attribute(AttributeName)`  
  
 `attribute(AttributeName, AttributeType)`  
  
## <a name="test-examples"></a>テストの例  
 次の例は、要素のテストおよび属性のテストが役立つシナリオを示しています。  
  
### <a name="example-a"></a>例 A  
 次の XML スキーマでは、<`firstName`> 要素と <`lastName`> 要素を省略できる、`CustomerType` 複合型を定義しています。 指定した XML インスタンスでは、特定の顧客の名前が存在するかどうかを判断する必要があるとします。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="https://www.w3.org/2001/XMLSchema"  
targetNamespace="myNS" xmlns:ns="myNS">  
  <complexType name="CustomerType">  
     <sequence>  
        <element name="firstName" type="string" minOccurs="0"   
                  nillable="true" />  
        <element name="lastName" type="string" minOccurs="0"/>  
     </sequence>  
  </complexType>  
  <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
DECLARE @var XML(SC)  
SET @var = '<x:customer xmlns:x="myNS">  
<firstName>SomeFirstName</firstName>  
<lastName>SomeLastName</lastName>  
</x:customer>'  
```  
  
 次のクエリでは、`instance of element (firstName)` 式を使用して、<`customer`> の最初の子要素が <`firstName`> という名前の要素であるかどうかを判断しています。 この場合、True が返されます。  
  
```  
SELECT @var.query('declare namespace x="myNS";   
     (/x:customer/*)[1] instance of element (firstName)')  
GO  
```  
  
 インスタンスから <`firstName`> 要素を削除すると、クエリにより False が返されます。  
  
 また、次の構文も使用できます。  
  
-   次のクエリで示すような `element(ElementName, ElementType?)` シーケンス型の構文。 この構文では、名前が `firstName` で型が `xs:string` の NULL 要素ノードまたは NULL 以外の要素ノードが照合されます。  
  
    ```  
    SELECT @var.query('declare namespace x="myNS";   
    (/x:customer/*)[1] instance of element (firstName, xs:string?)')  
    ```  
  
-   次のクエリで示すような `element(*, type?)` シーケンス型の構文。 この構文では、名前に関係なく、要素ノードの型が `xs:string` の場合にその要素ノードが照合されます。  
  
    ```  
    SELECT @var.query('declare namespace x="myNS"; (/x:customer/*)[1] instance of element (*, xs:string?)')  
    GO  
    ```  
  
### <a name="example-b"></a>例 B  
 次の例は、式から返されたノードが特定の名前の要素ノードかどうかを判断する方法を示しています。 使用して、 **element()** をテストします。  
  
 次の例では、クエリ対象の XML インスタンス内にある 2 つの <`Customer`> 要素の型は、それぞれ `CustomerType` と `SpecialCustomerType` という異なる型です。 式から返される <`Customer`> 要素の型を確認するとします。 次の XML スキーマ コレクションでは、`CustomerType` 型と `SpecialCustomerType` 型を定義しています。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="https://www.w3.org/2001/XMLSchema"  
          targetNamespace="myNS"  xmlns:ns="myNS">  
  <complexType name="CustomerType">  
    <sequence>  
      <element name="firstName" type="string"/>  
      <element name="lastName" type="string"/>  
    </sequence>  
  </complexType>  
  <complexType name="SpecialCustomerType">  
     <complexContent>  
       <extension base="ns:CustomerType">  
        <sequence>  
            <element name="Age" type="int"/>  
        </sequence>  
       </extension>  
     </complexContent>  
    </complexType>  
   <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
```  
  
 この XML スキーマ コレクションの作成に使用する型指定された**xml**変数。 この変数に割り当てられた XML インスタンスには、型が異なる 2 つの <`customer`> 要素があります。 最初の要素は `CustomerType` 型で、2 つ目の要素は `SpecialCustomerType` 型です。  
  
```  
DECLARE @var XML(SC)  
SET @var = '  
<x:customer xmlns:x="myNS">  
   <firstName>FirstName1</firstName>  
   <lastName>LastName1</lastName>  
</x:customer>  
<x:customer xsi:type="x:SpecialCustomerType" xmlns:x="myNS" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance">  
   <firstName> FirstName2</firstName>  
   <lastName> LastName2</lastName>  
   <Age>21</Age>  
</x:customer>'  
```  
  
 次のクエリで、`instance of element (*, x:SpecialCustomerType ?)` 式は False を返します。この式で返されている最初の customer 要素が、`SpecialCustomerType` 型ではないためです。  
  
```  
SELECT @var.query('declare namespace x="myNS";   
    (/x:customer)[1] instance of element (*, x:SpecialCustomerType ?)')  
```  
  
 上記のクエリの式を変更し、2 つ目の <`customer`> 要素 (`/x:customer)[2]`) を取得すると、`instance of` から True が返されます。  
  
### <a name="example-c"></a>例 C  
 この例では、属性のテストを使用します。 次の XML スキーマでは、CustomerID 属性と Age 属性を含む CustomerType 複合型を定義しています。 Age 属性は省略できます。 特定の XML インスタンスでは、<`customer`> 要素内に Age 属性が指定されているかどうかを判断できます。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="https://www.w3.org/2001/XMLSchema"  
       targetNamespace="myNS" xmlns:ns="myNS">  
<complexType name="CustomerType">  
  <sequence>  
     <element name="firstName" type="string" minOccurs="0"   
               nillable="true" />  
     <element name="lastName" type="string" minOccurs="0"/>  
  </sequence>  
  <attribute name="CustomerID" type="integer" use="required" />  
  <attribute name="Age" type="integer" use="optional" />  
 </complexType>  
 <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
```  
  
 次のクエリでは、クエリ対象の XML インスタンスに `Age` という名前の属性ノードが存在するので、True が返されます。 この式では、`attribute(Age)` 属性のテストを使用しています。 属性の順序が決まっていないので、クエリでは FLWOR 式を使用してすべての属性を取得し、`instance of` 式を使用して各属性をテストします。 例では、最初に、型指定された XML スキーマ コレクションを作成**xml**変数。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<x:customer xmlns:x="myNS" CustomerID="1" Age="22" >  
<firstName>SomeFName</firstName>  
<lastName>SomeLName</lastName>  
</x:customer>'  
SELECT @var.query('declare namespace x="myNS";   
FOR $i in /x:customer/@*  
RETURN  
    IF ($i instance of attribute (Age)) THEN  
        "true"  
        ELSE  
        ()')     
GO  
  
```  
  
 省略可能な `Age` 属性をインスタンスから削除すると、上記のクエリにより False が返されます。  
  
 属性のテストで、属性の名前と型 (`attribute(name,type)`) を指定できます。  
  
```  
SELECT @var.query('declare namespace x="myNS";   
FOR $i in /x:customer/@*  
RETURN  
    IF ($i instance of attribute (Age, xs:integer)) THEN  
        "true"  
        ELSE  
        ()')  
```  
  
 または、指定することができます、`attribute(*, type)`シーケンス型の構文。 この構文を指定すると、名前は一致しなくても属性の型と指定した型が一致する場合に属性のノードが照合されます。  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 特定の制限事項を次に示します。  
  
-   要素のテストには、出現インジケーターで、型名を続けて (**?**)。  
  
-   **element (ElementName, TypeName)** はサポートされていません。  
  
-   **要素 (\*、TypeName)** はサポートされていません。  
  
-   **schema-element()** はサポートされていません。  
  
-   **schema-attribute (attributename)** はサポートされていません。  
  
-   明示的に照会する**xsi:type**または**xsi:nil**はサポートされていません。  
  
## <a name="see-also"></a>参照  
 [システム入力&#40;XQuery&#41;](../xquery/type-system-xquery.md)  
  
  
