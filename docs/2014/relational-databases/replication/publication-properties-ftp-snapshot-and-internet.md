---
title: '[パブリケーションのプロパティ]、[FTP スナップショットとインターネット] | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.internetsynchronization.f1
ms.assetid: 8e0198c3-5e4e-418c-9920-78ccbbfc1323
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 72d53ea0cf2d1abff25b7b97a1fe66cc9d9646b7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52784844"
---
# <a name="publication-properties-ftp-snapshot-and-internet"></a>[パブリケーションのプロパティ]、[FTP スナップショットとインターネット]
  このページで以下の操作を実行できます。  
  
-   ファイル転送プロトコル (FTP) を通じてスナップショットを配信するためのプロパティを設定する。 詳細については、次を参照してください。 [FTP によるスナップショットの転送](transfer-snapshots-through-ftp.md)詳細については、Windows ドキュメント。  
  
    > [!NOTE]  
    >  FTP 設定を変更するには、新しいスナップショットを生成する必要があります。  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンでのマージ レプリケーションに対して、Web 同期のプロパティを設定して、サブスクリプションを HTTPS (安全なハイパーテキスト転送プロトコル) 経由で同期できるようにする。 Web 同期を使用するには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] インターネット インフォメーション サービス (IIS) サーバーを構成する必要があります。 詳細については、「 [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[FTP 経由でスナップショットにアクセス]**  
 **[ファイル転送プロトコル (FTP) を使用したスナップショット ファイルのダウンロードをサブスクライバーに許可する]** を選択し、 **[FTP サーバー名]**、 **[ポート番号]**、 **[FTP ルート フォルダーからのパス]**、 **[ログイン]**、および **[パスワード]** を指定し、サブスクライバーがスナップショットの配信に FTP を使用できるようにします。  
  
 このオプションを選択すると、サブスクライバーは FTP を使用してスナップショット ファイルを取得できますが、この設定は必須ではありません。 このオプションを選択した場合、サブスクリプションの新規作成ウィザードでは、サブスクライバーがスナップショット ファイルを FTP 経由で取得する設定が既定で有効になります。 設定を変更するには、 **[サブスクリプションのプロパティ]** ダイアログ ボックスを使用します。 サブスクライバーが FTP 経由でスナップショットにアクセスするように設定する場合は、 **[パブリケーションのプロパティ]** ダイアログ ボックスの **[スナップショット]** ページで、スナップショット ファイルの場所として FTP フォルダーを指定します。 これにより、スナップショット エージェントは、新しいスナップショットが生成されたときに FTP フォルダー内のファイルを自動的に更新します。 場所を FTP フォルダーに設定していない場合は、新しいスナップショットが生成されたときにファイルを手動で更新する必要があります。 詳細については、「[FTP でのスナップショットの配信](publish/deliver-a-snapshot-through-ftp.md)」を参照してください。  
  
 **[Web 同期]**  
 マージ レプリケーションのみです。 **[Web サーバーへの接続による同期をサブスクライバーに許可する]** を選択し、マージ サブスクライバーが Web 同期を使用できるように Web サーバー アドレスを指定します。 Web サーバーは、SSL (Secure Sockets Layer) を使用する必要があります。また、Web アドレスは https://server.domain.com/synchronize のように完全修飾である必要があります。 詳しくは、「 [Configure Web Synchronization](configure-web-synchronization.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [Create a Publication](publish/create-a-publication.md)   
 [パブリケーション プロパティの表示および変更](publish/view-and-modify-publication-properties.md)   
 [プル サブスクリプションのプロパティの表示または変更](view-and-modify-pull-subscription-properties.md)   
 [プッシュ サブスクリプションのプロパティの表示または変更](view-and-modify-push-subscription-properties.md)   
 [初期スナップショットの作成および適用](create-and-apply-the-initial-snapshot.md)   
 [データとデータベース オブジェクトのパブリッシュ](publish/publish-data-and-database-objects.md)  
  
  
