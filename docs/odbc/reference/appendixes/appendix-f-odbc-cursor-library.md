---
title: '付録 f: ODBC カーソル ライブラリ |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- cursor library [ODBC]
ms.assetid: a03084df-4e48-48ef-917d-4a3fae48a605
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c27845976651b0d68b91b6269a21d1cae3518df8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649590"
---
# <a name="appendix-f-odbc-cursor-library"></a>付録 F: ODBC カーソル ライブラリ
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 ODBC カーソル ライブラリ (Odbccr32.dll) は、レベル 1 API への準拠のレベルに準拠している任意のドライバーのスクロール可能なカーソルのブロックをサポートし、自社のアプリケーションやドライバーで開発者が再配布できます。 カーソル ライブラリもサポートしている位置指定更新と delete ステートメントによって生成される結果セットの**選択**ステートメント。 ただし、サポート対象は静的カーソルと順方向専用カーソル、カーソル ライブラリは多くのアプリケーションのニーズを満たします。 さらに、特に小規模または中規模の結果セット、および適切なカーソルのサポートがないアプリケーションの優れたパフォーマンスを提供できます。  
  
 カーソル ライブラリは、ドライバー マネージャーとドライバーの間に存在するダイナミック リンク ライブラリ (DLL) です。 アプリケーションは、関数を呼び出すときに、ドライバー マネージャーは、関数を実行するか、指定のドライバーで関数を呼び出したカーソル ライブラリで関数を呼び出します。 特定の接続には、アプリケーションは、カーソル ライブラリが常に使用になっていること、ドライバーは、スクロール可能なカーソルをサポートしていない場合に使用または使用されていませんかどうかを指定します。  
  
 カーソル ライブラリは、ドライバーをドライバー マネージャーとして表示されます。 場合は、カーソル ライブラリは、ドライバー マネージャーと ODBC 2 の間存在します。*x*ドライバー、カーソル ライブラリは、ODBC 2 として表示されます *。x*ドライバー。 ドライバー マネージャーと、ODBC 3 の間、カーソル ライブラリが存在するかどうかは *.x*ドライバー、カーソル ライブラリは、ODBC 3 として表示 *.x*ドライバー。 カーソル ライブラリによって発生した現象は、ODBC 2 の両方でサポートされているバインディングのオフセットを除く操作をしているドライバーのバージョンによって異なります。*x*および ODBC 3 *。x*ドライバー。  
  
 ブロック カーソルを実装する**SQLFetch**と**SQLFetchScroll**、カーソル ライブラリを繰り返し呼び出す**SQLFetch**ドライバー。 スクロールを実装するには、メモリとディスクのファイルが取得したデータをキャッシュします。 アプリケーションでは、新しい行セットを要求、カーソル ライブラリをドライバーまたはキャッシュから、必要に応じて取得します。  
  
 位置指定更新プログラムの実装を delete ステートメントは、カーソル ライブラリを構築します、**更新**または**削除**ステートメントを**場所**キャッシュされたを指定する句行にバインドされた各列の値。 位置指定の update ステートメントを実行するとき、カーソル ライブラリは、行セットのバッファー内の値からそのキャッシュを更新します。  
  
 ODBC カーソル ライブラリの詳細については、この付録の次のセクションを参照してください。  
  
-   [ODBC カーソル ライブラリの使用](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [位置指定更新と Delete ステートメントの実行](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [カーソル ライブラリのコード例](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [実装に関するメモ](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [ODBC カーソル ライブラリのエラー コード](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
