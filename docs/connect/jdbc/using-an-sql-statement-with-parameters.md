---
title: SQL ステートメント パラメーターの使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3202b88f-ce13-44dd-982c-c6a3b0260378
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66a0215721b906ed81e9daa06cb3dbc07804229d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47629470"
---
# <a name="using-an-sql-statement-with-parameters"></a>パラメータがある SQL ステートメントの使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

IN パラメーターを含む SQL ステートメントを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのデータを処理する場合は、[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) クラスの [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) メソッドを使用して、要求されたデータを含む [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) を取得することができます。 この場合、最初に [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) クラスの [prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) メソッドを使用して、SQLServerPreparedStatement オブジェクトを作成する必要があります。

SQL ステートメントを作成する場合、IN パラメータは ?  (疑問符) 文字で指定します。これはパラメータ値のプレースホルダになり、後で SQL ステートメントに渡されます。 パラメーターの値を指定するには、SQLServerPreparedStatement クラスの setter メソッドのいずれかを使用できます。 使用する setter メソッドは、SQL ステートメントに渡す値のデータ型によって決定されます。

setter メソッドに値を渡す場合は、SQL ステートメントで使用する実際の値だけでなく、SQL ステートメント内のパラメータの順序も指定する必要があります。 たとえば、SQL ステートメントに 1 つのパラメーターが含まれている場合、その序数値は、1 をなります。 ステートメントに 2 つのパラメーターが含まれている場合、1 つ目の序数値は 1 に、2 つ目の序数値は 2 になります。

次の例は、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] サンプル データベースに対して開いている接続を関数に渡し、準備された SQL ステートメントを作成して 1 つの String のパラメーター値を指定して実行し、その結果を結果セットから読み取ります。

[!code[JDBC#UsingSQLWithParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_1_1.java)]

## <a name="see-also"></a>参照

[SQL でのステートメントの使用](../../connect/jdbc/using-statements-with-sql.md)
