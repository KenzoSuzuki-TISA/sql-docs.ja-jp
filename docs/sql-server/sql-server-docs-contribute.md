---
title: SQL Server のドキュメントに投稿する方法 | Microsoft Docs
ms.date: 08/13/2018
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.topic: conceptual
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: c9855f798a7867dfd67a52a1c8452340cdf2a69a
ms.sourcegitcommit: 60739bcb48ccce17bca4e11a85df443e93ca23e3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52439904"
---
# <a name="how-to-contribute-to-sql-server-documentation"></a>SQL Server のドキュメントに投稿する方法

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

誰でも SQL Server のドキュメントに投稿できます。 投稿には、入力ミスの修正、もっとよい説明の提案、技術的正確さの改善などがあります。 この記事では、コンテンツへの投稿の概要とプロセスについて説明します。

2 つの主要なワークフローを使って投稿することができます。

|||
|---|---|
| [ブラウザーで編集する](#githubui) | 任意の記事のちょっとした編集を簡単に行うのに適しています。 |
| [ツールを使ってローカルに編集する](#tools) | 複雑な編集、複数の記事が関係する編集、および docs.microsoft.com への頻繁な投稿に適しています。 |

公開されるすべての投稿は、SQL コンテンツ チームによって技術的正確さと一貫性が検証されます。 

## <a id="githubui"></a> ブラウザーで編集する

お使いのブラウザーで SQL Server のコンテンツに簡単な編集を加え、Microsoft に送信することができます。 完全なプロセスは、[Microsoft Docs 共同作成者ガイド概要](https://docs.microsoft.com/contribute/#quick-edits-to-existing-documents)の記事に記載されています。 次のビデオは、お使いのブラウザーで変更を送信するためのエンド ツー エンド プロセスを示しています。

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE23pxh]

> [!TIP]
> **[編集]** ボタンの場所はビデオで示す内容と若干異なりますが、プロセスは同じです。
>
> ![[編集] ボタン](./media/sql-server-docs-contribute/edit-sql-server-docs.png)

## <a id="tools"></a> ツールを使ってローカルに編集する

もう 1 つの編集オプションは、**sql-docs** または **azure-docs** リポジトリをフォークして、お使いのコンピューターにローカルに複製します。 その後、Markdown エディターと git クライアントを使って、変更を送信することができます。 このワークフローは、複雑で複数のファイルが関係する編集に適しています。 また、docs.microsoft.com に頻繁に投稿する場合にも適しています。

この方法で投稿する場合は、次の記事を参照してください。

- [GitHub アカウントを作成する](https://docs.microsoft.com/contribute/get-started-setup-github)
- [コンテンツ オーサリング ツールをインストールする](https://docs.microsoft.com/contribute/get-started-setup-tools)
- [Git リポジトリをローカルに設定する](https://docs.microsoft.com/contribute/get-started-setup-local)
- [ツールを使って投稿する](https://docs.microsoft.com/contribute/how-to-write-workflows-major)

ドキュメントを大幅に変更するプル要求を送信する場合は、オンライン**貢献者使用許諾契約書 (CLA)** の提出を求める GitHub のコメントを受け取ります。 オンライン フォームを提出してからでないと、プル要求は受け付けられません。

## <a name="recognition"></a>認識

変更が受け付けられると、記事の上部で共同作成者として認識されます。

![コンテンツへの投稿の認識](./media/sql-server-docs-contribute/contribution-recognition.png)

## <a name="sql-docs-overview"></a>sql-docs の概要

このセクションでは、**sql-docs** リポジトリでの作業に関するその他のガイダンスを提供します。

> [!IMPORTANT]
> このセクションの情報は、**sql-docs** に固有のものです。Azure のドキュメントに含まれる SQL の記事を編集する場合は、[GitHub で azure-docs リポジトリの Readme](https://github.com/MicrosoftDocs/azure-docs/blob/master/README.md) を参照してください。

[sql-docs](https://github.com/MicrosoftDocs/sql-docs) リポジトリでは、複数の標準フォルダーを使ってコンテンツが整理されています。

| フォルダー | [説明] |
|---|---|
| [docs](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs) | 公開されたすべての SQL Server コンテンツが格納されています。 サブフォルダーには、異なる分野のコンテンツが論理的にまとめられています。 |
| [docs/includes](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs/includes) | インクルード ファイルが格納されています。 これらのファイルは、他のトピックに含めることのできるコンテンツのブロックです。 |
| **./media** | 各フォルダーには、記事の画像用に 1 つの **media** サブフォルダーが含まれる場合があります。 **media** フォルダーには、画像が表示されるトピックと同じ名前のサブフォルダーがあります。 画像は .png ファイルで、すべて小文字のスペースを含まない名前になっている必要があります。 |
| **TOC.MD** | 目次のファイルです。 各サブフォルダーでは、1 つの TOC.MD ファイルを使うことができます。 |

#### <a name="applies-to-includes"></a>applies-to インクルード

SQL Server の各記事には、タイトルの後に **applies-to** インクルード ファイルが含まれています。 これは、その記事が適用される SQL Server の領域またはバージョンを示します。

**appliesto-ss-asdb-asdw-pdw-md.md** インクルード ファイルの Markdown の例を次に示します。

```Markdown
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
```

このインクルード ファイルにより、記事の上部に次のテキストが追加されます。

![適用対象のテキスト](./media/sql-server-docs-contribute/applies-to.png)

記事の適切な applies-to インクルード ファイルを探すには、次のヒントを参考にしてください。

- 一般的に使用されるインクルードの一覧は、[SQL Server のバージョンと applies-to インクルード ファイル](applies-to-includes.md)に関するページを参照してください。
- 同じ機能または関連タスクをカバーしている他の記事を探します。 その記事を編集する場合は、applies-to インクルード リンクの Markdown をコピーできます (送信しないで編集をキャンセルできます)。
- [docs/includes](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs/includes) ディレクトリで、"applies-to" というテキストを含むファイルを探します。 GitHub の **[Find]** ボタンを使ってすばやくフィルター処理できます。 ファイルをクリックして、どのようにレンダリングされるかを確認します。
- 名前付けの規則に注意してください。 名前に "x" が含まれる場合は、通常、サービスのサポートがないことを示すプレースホルダーです。 たとえば、**appliesto-xx-xxxx-asdw-xxx-md.md** は、**asdw** だけが明示され、他のフィールドは "x" になっているので、Azure SQL Data Warehouse のみのサポートであることを示します。
- **tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md** のようにバージョン番号が指定されていることもあります。 SQL Server の特定のバージョンで機能が導入されたことがわかっている場合は、そのインクルードだけを使ってください。

## <a name="contributor-resources"></a>共同作成者のリソース

- [docs.microsoft.com の共同作成者ガイド](https://docs.microsoft.com/contribute/)
- [Microsoft スタイル ガイド](https://docs.microsoft.com/teamblog/style-guide)
- [Markdown の基礎](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)

> [!TIP]
> ドキュメントに関するフィードバックではなく製品のフィードバックの場合は、[こちらで SQL Server 製品に関するフィードバックを提供](https://feedback.azure.com/forums/908035-sql-server)してください。

## <a name="next-steps"></a>次の手順

GitHub で [sql-docs リポジトリ](https://github.com/MicrosoftDocs/sql-docs)を調べます。

記事を探し、変更内容を送信して、SQL Server コミュニティに投稿します。 

ありがとうございます。
