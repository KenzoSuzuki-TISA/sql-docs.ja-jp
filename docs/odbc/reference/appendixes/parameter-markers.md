---
title: パラメーター マーカー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 833e2740e54f07701fb66a894bb5e4798c4a42e2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516400"
---
# <a name="parameter-markers"></a>パラメーター マーカー
SQL 92 の仕様に従って、アプリケーションは、次の場所にパラメーター マーカーを配置できません。 詳細な一覧は、SQL 92 仕様を参照してください。  
  
-   **選択**一覧  
  
-   両方と*式*で、*比較述語*  
  
-   二項演算子の両方のオペランドとして  
  
-   最初と 2 番目のオペランドとして、 **BETWEEN**操作  
  
-   最初と 3 番目の両方のオペランドとして、 **BETWEEN**操作  
  
-   式との最初の値の両方として、 **IN**操作  
  
-   単項演算子のオペランドとして + または - 操作  
  
-   引数として、*セットの参照関数*  
  
 パラメーター マーカーの詳細については、SQL 92 仕様を参照してください。 パラメーターの詳細については、次を参照してください。[ステートメント パラメーター](../../../odbc/reference/develop-app/statement-parameters.md)します。
