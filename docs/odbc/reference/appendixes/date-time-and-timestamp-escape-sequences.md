---
title: 日付、時刻、およびタイムスタンプ エスケープ シーケンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC]
- escape sequences [ODBC], about escape sequences
- ODBC escape sequences [ODBC], about escape sequences
- ODBC escape sequences [ODBC]
ms.assetid: 67b7dee0-e5b1-4469-a626-0c7767852b80
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6bd73a1bd7a9f41b20300e4abf47688a6c78794
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2018
ms.locfileid: "53200931"
---
# <a name="date-time-and-timestamp-escape-sequences"></a>日付、時刻、およびタイムスタンプ エスケープ シーケンス
ODBC では、日付、時刻、およびタイムスタンプのリテラルのエスケープ シーケンスを定義します。 これらのエスケープ シーケンスの構文は次のとおりです。  
  
```  
  
{d 'value'}  
{t 'value'}  
{ts 'value'}  
```  
  
 BNF 表記では、構文がとおりです。  
  
```  
  
      ODBC-date-time-escape ::=  
     ODBC-date-escape  
     | ODBC-time-escape  
     | ODBC-timestamp-escapeODBC-date-escape ::=  
     ODBC-esc-initiator d 'date-value' ODBC-esc-terminatorODBC-time-escape ::=  
     ODBC-esc-initiator t 'time-value' ODBC-esc-terminatorODBC-timestamp-escape ::=  
     ODBC-esc-initiator ts 'timestamp-value' ODBC-esc-terminatorODBC-esc-initiator ::= {  
ODBC-esc-terminator ::= }  
date-value ::=   
     years-value date-separator months-value date-separator days-valuetime-value ::=   
     hours-value time-separator minutes-value time-separatorseconds-valuetimestamp-value ::= date-value timestamp-separator time-valuedate-separator ::= -  
time-separator ::= :  
timestamp-separator ::=  
     (The blank character)years-value ::= digit digit digit digitmonths-value ::= digit digitdays-value ::= digit digithours-value ::= digit digitminutes-value ::= digit digitseconds-value ::= digit digit[.digit...]  
```  
  
## <a name="remarks"></a>コメント  
 日付、時刻、およびタイムスタンプのリテラルのエスケープ シーケンスは、日付、時刻、タイムスタンプ データ型が、データ ソースでサポートされている場合にサポートされます。 アプリケーションを呼び出す必要があります**SQLGetTypeInfo**をこれらのデータ型がサポートされているかどうかを判断します。
