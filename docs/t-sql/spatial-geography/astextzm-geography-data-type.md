---
title: AsTextZM (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AsTextZM (geography Data Type)
- AsTextZM_TSQL
- AsTextZM
- AsTextZM_(geography_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsTextZM method
ms.assetid: e9dc27f6-e945-4457-8498-7644db34008e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f8a147ff48d0436c51519532af3485e0bde11ed2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713020"
---
# <a name="astextzm-geography-data-type"></a>AsTextZM (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  インスタンスに格納されている **Z** (標高) 値および **M** (メジャー) 値で補完された **geography** インスタンスについて、Open Geospatial Consortium (OGC) Well-Known Text (WKT) 表現を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.AsTextZM ()  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **nvarchar(max)**  
  
 CLR の戻り値の型: **SqlChars**  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>使用例  
 **Z** (標高) 値および **M** (メジャー) 値を含む `Point` インスタンスを作成する例を次に示します。 `STAsText()` は WKT 値 (-122.34900 47.65100) を選択します。`AsTextZM()` は同じ WKT 値を選択し、**Z** および **M** の値も返すため、(-122.34900 47.65100 10.3 12) が出力されます。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.STAsText();  
SELECT @g.AsTextZM();  
```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40;geography データ型&#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [Z &#40;geography データ型&#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
