---
title: '[パブリケーションのプロパティ]、[スナップショット] | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.snapshotformat.f1
ms.assetid: 8e9133b1-fc37-4a85-8a7c-d5eaf172fbef
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d7d94874d03c05fffbc62743b5337649a3e228a2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804404"
---
# <a name="publication-properties-snapshot"></a>[パブリケーションのプロパティ]、[スナップショット]
  **[パブリケーションのプロパティ]** ダイアログ ボックスの **[スナップショット]** ページを使用すると、スナップショット形式、スナップショット フォルダーの場所、およびスナップショットのアプリケーションの前後に実行するスクリプトを設定できます。 スナップショット フォルダーは、共有として指定する必要があり、エージェントがフォルダーでファイルを読み書きするための十分な権限を持っている必要があります。 フォルダーの適切なセキュリティ保護の詳細については、「[スナップショット フォルダーのセキュリティ保護](security/secure-the-snapshot-folder.md)」を参照してください。  
  
> [!NOTE]  
>  変更する場合は、パブリケーションの新しいスナップショットが必要です。 詳細については、「[Change Publication and Article Properties](publish/change-publication-and-article-properties.md)」 (パブリケーションおよびアーティクルのプロパティの変更) を参照してください。  
  
## <a name="options"></a>および  
 **[スナップショットの形式]**  
 スナップショットの形式にネイティブ モードまたはキャラクター モードを選択します。  
  
-   すべてのサブスクライバーが [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外の [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] のインスタンスである場合は、**[ネイティブ SQL Server - サブスクライバーはすべて SQL Server を実行しているサーバーである必要があります]** を選択します。 ネイティブ スナップショットの形式によってパフォーマンスが最適化されます。  
  
-   いずれかのサブスクライバーが **を実行している場合、または** 以外のバージョンのサブスクライバーである場合は、 [!INCLUDE[ssEW](../../includes/ssew-md.md)] [文字 - パブリッシャーまたはサブスクライバーで SQL Server が実行されていない場合は必須][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を選択します。  
  
 **[スナップショット ファイルの場所]**  
 スナップショット ファイルを格納する場所を選択します。 既定の場所に格納するか、既定の場所ではなく代替位置に格納したり、既定の場所と代替位置の両方に格納したりできます。 代替位置に格納されたファイルは圧縮できます。  
  
-   パブリッシャーに既定のスナップショット フォルダーを使用する場合は、 **[ファイルを既定のフォルダーに保存する]** を選択します。 このダイアログ ボックスでは、スナップショット フォルダーの場所は読み取り専用です。パブリッシャーのスナップショット フォルダーの場所の変更は、 **[ディストリビューターのプロパティ]** ダイアログ ボックスのみで行うことができます。 詳細については、「[既定のスナップショットの場所の指定 &#40;SQL Server Management Studio&#41;](specify-the-default-snapshot-location-sql-server-management-studio.md)」を参照してください。  
  
-   既定の場所の代わり、または既定の場所に加えて代替位置を指定する場合は、 **[ファイルを次のフォルダーに保存する]** を選択します。 テキスト ボックスにパスを入力するか、 **[参照]** をクリックしてその場所に移動します。 スナップショットの代替場所のファイルを圧縮する場合は、 **[スナップショット ファイルをこのフォルダーに圧縮]** を選択します。 他のサーバー、ネットワーク ドライブ、または CD-ROM やリムーバブル ディスクなどのリムーバブル メディアに代替位置を設定できます。 詳細については、「 [Alternate Snapshot Folder Locations](alternate-snapshot-folder-locations.md) 」および「 [Compressed Snapshots](compressed-snapshots.md)」を参照してください。  
  
 **[追加スクリプトの実行]**  
 サブスクライバーでスナップショットが適用される前後で実行するスクリプトを指定します。 **[スナップショットの形式]** が **[文字]** である場合は、スクリプトを指定できません。  
  
 スクリプトはオプションです。スクリプトを使用すると、サブスクライバーでのコマンドの実行や管理上の変更の適用を容易に行うことができます。 スクリプトの実行の詳細については、「[スナップショットが適用される前および後のスクリプトの実行](execute-scripts-before-and-after-the-snapshot-is-applied.md)」を参照してください。  
  
-   **[スクリプトをスナップショットの適用前に以下のスクリプトを実行]** テキスト ボックスにパスを入力するか、 **[参照]** をクリックしてスクリプトの場所を指定します。  
  
-   **[スナップショットの適用後に以下のスクリプトを実行]** テキスト ボックスにパスを入力するか、 **[参照]** をクリックしてスクリプトの場所を指定します。  
  
## <a name="see-also"></a>参照  
 [Create a Publication](publish/create-a-publication.md)   
 [パブリケーション プロパティの表示および変更](publish/view-and-modify-publication-properties.md)   
 [初期スナップショットの作成および適用](create-and-apply-the-initial-snapshot.md)   
 [スナップショットを使用したサブスクリプションの初期化](initialize-a-subscription-with-a-snapshot.md)   
 [データとデータベース オブジェクトのパブリッシュ](publish/publish-data-and-database-objects.md)  
  
  
