---
title: タイプ Id |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- type identifiers [ODBC]
- identifiers [ODBC], type
- type identifiers [ODBC], about type identifiers
ms.assetid: 1d9fdfa2-e378-44fe-ac66-9743d9bbdd5a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cbefab0f02f3229d8b4c0a62a568634ec222290b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47825170"
---
# <a name="type-identifiers"></a>型識別子
ODBC SQL と C# のデータ型を記述するには 2 つのセットを定義します*タイプ id*します。 型識別子には、SQL 列または C バッファーの種類について説明します。 **#Define**値しは一般に関数の引数として渡されるまたはメタデータに返されます。  
  
 たとえば、次の呼び出し**SQLBindParameter** SQL_DATE_STRUCT 型の変数を SQL ステートメントで日付のパラメーターにバインドします。 C 型識別子 SQL_C_TYPE_DATE の種類を指定する、*日付*変数、および SQL の型識別子 SQL_TYPE_DATE は動的パラメーターの型を指定します。  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER  DateInd = 0;  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &Date, 0, &DateInd);  
```
