---
title: ユーザーとワークスペースの設定
titleSuffix: Azure Data Studio
description: ユーザーとワークスペースの設定を変更することによって Azure Data Studio をカスタマイズする方法。
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 6bf09159c8b7384a835a06bfafe744ea2f90f0c2
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030506"
---
# <a name="modify-user-and-workspace-settings"></a>ユーザーとワークスペースの設定を変更します。

[!INCLUDE[name-sos](../includes/name-sos-short.md)] の設定を好みに応じて構成するのは簡単です。 [!INCLUDE[name-sos](../includes/name-sos-short.md)]のエディター、ユーザー インターフェイス、および機能の振る舞い、ほぼすべての部分について任意に変更できます。

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 2 つのさまざまなスコープの設定を提供します。

* **ユーザー設定** は開いている[!INCLUDE[name-sos](../includes/name-sos-short.md)]のすべてのインスタンスに対してグローバルに適用されます。
* **ワークスペース**ワークスペースの設定は、コンピューター上のフォルダーに固有の設定とは、フォルダーはエクスプ ローラーのサイドバーで開いている場合にのみ使用できます。 このスコープで定義された設定は、ユーザー スコープをオーバーライドします。

## <a name="creating-user-and-workspace-settings"></a>ユーザーとワークスペースの設定の作成

メニュー コマンド**ファイル** > **設定** > **設定**(**コード** >  **設定** > **設定**Mac で) ユーザーとワークスペースの設定を構成するエントリ ポイントを提供します。 既定の設定の一覧が表示されます。 適切な変更に必要な任意の設定をコピー`settings.json`ファイル。 右側のタブを使用して、ユーザーとワークスペースの設定ファイルをすばやく切り替えることができます。

ユーザーとワークスペースの設定を開くことも、**コマンド パレット**(**Ctrl + Shift + P**) と**設定。ユーザー設定を開く**と**設定。ワークスペースの設定を開く**キーボード ショートカットを使用して、または (**Ctrl +,**)。

次の例では、エディター内の行番号を無効にし、行のコードを自動的にインデントを設定するを構成します。

![設定の例](media/settings/sample-settings.png)

設定の変更がによって再読み込み[!INCLUDE[name-sos](../includes/name-sos-short.md)]、変更された後`settings.json`ファイルを保存します。

>**注:** ワークスペースの設定は、チーム プロジェクトに固有の設定を共有するために役立ちます。

## <a name="settings-file-locations"></a>設定ファイルの場所

プラットフォームに応じて、ユーザー設定ファイルは。

* **Windows** `%APPDATA%\sqlops\User\settings.json`
* **Mac** `$HOME/Library/Application Support/sqlops/User/settings.json`
* **Linux** `$HOME/.config/sqlops/User/settings.json`

ワークスペースの設定ファイルが下にある、`.[!INCLUDE[name-sos](../includes/name-sos-short.md)]`プロジェクトのフォルダー。

## <a name="hot-exit"></a>ホットの終了

Azure Data Studio では、既定で終了すると、ファイルに未保存の変更が記録されています。 これは、Visual Studio Code でホット終了機能と同じです。

既定では、ホットな終了は off です。 編集することによってホットの終了を有効にする、`files.hotExit`設定します。 詳細については、次を参照してください。 [(Visual Studio Code のドキュメント) でホット終了](https://code.visualstudio.com/docs/editor/codebasics#_hot-exit)します。


## <a name="tab-color"></a>タブの色

を使用しているどのような接続を識別するを簡略化する、エディターで開いているタブにその色が、接続が所属するサーバー グループの色を一致するように設定することができます。 既定では、タブの色は既定で無効にします。 編集して、タブの色を有効にする、`sql.tabColorMode`設定します。

## <a name="additional-resources"></a>その他のリソース

[!INCLUDE[name-sos](../includes/name-sos-short.md)]機能から Visual Studio Code の設定の詳細については、ユーザーとワークスペースの設定を継承、 [for Visual Studio Code の設定](https://code.visualstudio.com/docs/getstarted/settings)記事。
