---
title: MySQL (MySQLToSQL) への接続 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7289b3d5b287c1619a08921eba5cc30ff741e3b1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/27/2018
ms.locfileid: "52399905"
---
# <a name="connect-to-mysql-mysqltosql"></a>MySQL への接続 (MySQLToSQL)
使用して、 **MySQL への接続**を移行する MySQL データベースに接続するためのダイアログ ボックス。  
  
このダイアログ ボックスにアクセスする、**ファイル**メニューの  **MySQL への接続**します。 以前接続した場合、コマンドは**MySQL への再接続**します。  
  
## <a name="options"></a>および  
**Provider**  
  
使用可能な MySQL プロバイダーは、MySQL ODBC 5.1 のドライバー (信頼されている) です。  
  
**モード**  
  
既定のモードは、標準的なモードです。 標準モードでは、入力または、MySQL、サーバー名、サーバーのポート、ユーザー名、およびパスワードの値を選択します。  
  
**サーバー名**  
  
MySQL サーバー名を入力します。 これは、標準モードのオプションです。  
  
**[サーバー ポート]**  
  
サーバーのポートを入力します。 既定のサーバーのポートは、3306 です。 これは、標準モードのオプションです。  
  
**ユーザー名**  
  
SSMA が MySQL データベースへの接続に使用するユーザー名を入力します。  
  
**Password**  
  
ユーザー名に対応するパスワードを入力します。  
  
**SSL**  
  
MySQL に安全に接続する場合は、チェックの Secure Socket Layer (SSL) を使用すること、 **SSL**チェック ボックスをオンします。  
  
**構成**  
  
Secure Socket Layer (SSL) 経由の MySQL への接続を構成するオプションを提供します。  
  
> [!NOTE]  
> 有効にする**構成**に SSL を設定する必要があります**True**します。  
  
[構成] ボタンをクリックすると、ダイアログ ボックスが表示されます。 MySQL データベースを次の 3 つの証明書ファイル ダイアログ ボックス内に存在するパスに接続する必要があります中に暗号化を使用するには、[プライバシー強化メール証明書 (PEM)] に定義されています。  
  
-   **SSL 証明機関:** 信頼の SSL Ca の一覧で、ファイルへのパスを指定します。  
  
-   **SSL 証明書:** セキュリティで保護された接続を確立するために使用する SSL 証明書ファイルの名前を指定します。  
  
-   **SSL キー:** セキュリティで保護された接続を確立するために使用する SSL のキー ファイルの名前を指定します。  
  
> [!NOTE]  
> -   **OK**必要な情報が提供されているときにボタンが有効になります。 ファイル パスのいずれかの情報が有効でない場合は、"OK"ボタンが無効になります。  
> -   **キャンセル**ボタンがダイアログ ボックスを閉じ、**をオフに**メイン接続フォームからは、SSL オプション。  
  
