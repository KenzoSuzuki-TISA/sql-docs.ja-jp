---
title: シーケンスと Qname (XQuery) |Microsoft Docs
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
- sequence [XQuery]
- XQuery, sequence
- QName [XQuery]
- predefined namespaces [XML in SQL Server]
ms.assetid: 3593ac26-dd78-4bf0-bb87-64fbcac5f026
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0e7c73e33a1f19acb2158ced848c220b2b7af447
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2019
ms.locfileid: "54254157"
---
# <a name="sequence-and-qnames-xquery"></a>シーケンスと QName (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  このトピックでは、次の XQuery の基本概念について説明します。  
  
-   Sequence  
  
-   QName と事前に定義された名前空間  
  
## <a name="sequence"></a>Sequence  
 XQuery では、式の結果は、XML ノードおよび XSD アトミック型のインスタンスの一覧で構成されるシーケンスです。 シーケンス内の個々のエントリはアイテムと呼ばれます。 シーケンス内のアイテムは、次のいずれかになります。  
  
-   要素、属性、テキスト、処理命令、コメント、またはドキュメントなどのノード  
  
-   XSD 単純型のインスタンスなどのアトミック値  
  
 たとえば、次のクエリでは、2 つの要素ノードのアイテムのシーケンスが作成されます。  
  
```  
SELECT Instructions.query('  
     <step1> Step 1 description goes here</step1>,  
     <step2> Step 2 description goes here </step2>  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
  
```  
  
 これは、結果です。  
  
```  
<step1> Step 1 description goes here </step1>  
<step2> Step 2 description goes here </step2>   
```  
  
 上記のクエリでは、`,` 構成要素の最後にあるコンマ (`<step1>`) はシーケンス コンストラクターであり、必要な表記です。 結果に含まれる空白文字は説明の便宜上追加したもので、このドキュメント内のすべての例の結果にも同じ理由で空白文字を使用しています。  
  
 次に、シーケンスに関して理解する必要のある追加の情報を示します。  
  
-   クエリの結果が他のシーケンスを含むシーケンスになる場合、含まれているシーケンスは外側のシーケンスにフラット化されます。 たとえば、シーケンス ((1,2, (3,4,5)),6) はデータ モデル内で (1, 2, 3, 4, 5, 6) にフラット化されます。  
  
    ```  
    DECLARE @x xml;  
    SET @x = '';  
    SELECT @x.query('(1,2, (3,4,5)),6');  
    ```  
  
-   空のシーケンスとは、アイテムが含まれていないシーケンスです。 これは "()" で表されます。  
  
-   アイテムを 1 つしか持たないシーケンスは、アトミック値として扱うことができます。また、アトミック値は、1 つだけのアイテムを持つシーケンスとして扱うこともできます。 つまり (1) = 1 という式が成り立ちます。  
  
 この実装では、シーケンスは同種である必要があります。 つまり、アトミック値のシーケンスまたはノードのシーケンスのいずれかになります。 たとえば、有効なシーケンスは次のとおりです。  
  
```  
DECLARE @x xml;  
SET @x = '';  
-- Expression returns a sequence of 1 text node (singleton).  
SELECT @x.query('1');  
-- Expression returns a sequence of 2 text nodes  
SELECT @x.query('"abc", "xyz"');  
-- Expression returns a sequence of one atomic value. data() returns  
-- typed value of the node.  
SELECT @x.query('data(1)');  
-- Expression returns a sequence of one element node.   
-- In the expression XML construction is used to construct an element.  
SELECT @x.query('<x> {1+2} </x>');  
```  
  
 異種シーケンスはサポートされていないため、次のクエリはエラーを返します。  
  
```  
SELECT @x.query('<x>11</x>, 22');  
```  
  
## <a name="qname"></a>QName  
 XQuery の識別子は QName です。 QName は、名前空間プレフィックスとローカル名で構成されます。 この実装では、XQuery の変数名は QName であり、プレフィックスは付きません。  
  
 クエリが指定されている次の例を検討してください、型指定されていないに対して**xml**変数。  
  
```  
DECLARE @x xml;  
SET @x = '<Root><a>111</a></Root>';  
SELECT @x.query('/Root/a');  
```  
  
 式 (`/Root/a`) では、`Root` と `a` が QName です。  
  
 次の例では、クエリを指定する、型指定されたに対して**xml**列。 クエリは、すべてを反復処理\<手順 > 最初のワーク センターからの場所にある要素。  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $Step in /AWMI:root/AWMI:Location[1]/AWMI:step  
      return  
           string($Step)   
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 クエリ式では、次の点に注意してください。  
  
-   `AWMI root`、`AWMI:Location`、`AWMI:step`、`$Step` は、すべて QName です。 `AWMI` はプレフィックスであり、`root`、`Location`、および `Step` はすべてローカル名です。  
  
-   `$step` 変数は QName であり、プレフィックスを持っていません。  
  
 次の名前空間は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の XQuery サポートで使用するために、事前に定義されています。  
  
|Prefix|[URI]|  
|------------|---------|  
|xs|http://www.w3.org/2001/XMLSchema|  
|xsi|http://www.w3.org/2001/XMLSchema-instance|  
|xdt|http://www.w3.org/2004/07/xpath-datatypes|  
|fn|http://www.w3.org/2004/07/xpath-functions|  
|(プレフィックスなし)|`urn:schemas-microsoft-com:xml-sql`|  
|sqltypes|https://schemas.microsoft.com/sqlserver/2004/sqltypes|  
|xml|`http://www.w3.org/XML/1998/namespace`|  
|(プレフィックスなし)|`https://schemas.microsoft.com/sqlserver/2004/SOAP`|  
  
 各データベースを作成するには、 **sys** XML スキーマ コレクションです。 各データベースにはこれらのスキーマが保持されるため、ユーザーが作成した XML スキーマ コレクションからアクセスすることができます。  
  
> [!NOTE]  
>  この実装がサポートしていません、`local`の XQuery 仕様に記載されているプレフィックス http://www.w3.org/2004/07/xquery-local-functions します。  
  
## <a name="see-also"></a>参照  
 [XQuery の基礎](../xquery/xquery-basics.md)  
  
  
