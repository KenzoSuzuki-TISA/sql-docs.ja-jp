---
title: 共有データ ソース アイテムをセキュリティで保護する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
- security [Reporting Services], data sources
ms.assetid: 7299e498-0a1a-4821-a22a-5199bb773ce0
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d888ef0f3019e38e043ebe00c68e03f82e924f13
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2018
ms.locfileid: "48067248"
---
# <a name="secure-shared-data-source-items"></a>共有データ ソース アイテムをセキュリティで保護する
  共有データ ソース アイテムにセキュリティを設定して、そのアイテムへのアクセスを有効または無効にすることができます。  
  
 共有データ ソースにアクセスするための最低限の権限 (たとえば、 **閲覧者** ロールにより与えられる権限) を持っているユーザーは、レポート自体の表示を承認されていれば、アイテムを使用するレポートの一覧を表示できます。  
  
 それ以上の権限 (たとえば、 **コンテンツ マネージャー** ロールにより与えられる権限) を持つユーザーは、共有データ ソースのプロパティを表示および設定できます。  
  
 セキュリティを設定するには、共有データ ソースへのアクセス権を与えられたユーザー アカウントまたはグループ アカウントを指定するロールの割り当てを作成します。 共有データ ソース アイテムへのアクセス権を持つユーザーは、名前、説明、接続文字列、および資格情報を変更できます。  
  
## <a name="tasks-and-access-to-items"></a>タスクおよびアイテムへのアクセス  
 ロールの割り当てを作成するときに、以下のタスクを持つロールを使用して、ユーザーとグループに適切な権限を割り当てます。  
  
|使用するタスク|ユーザーに権限を与える操作|  
|----------------------|---------------------------------|  
|データ ソースの表示|フォルダー階層内の共有データ ソース アイテムを表示します。 このタスクがないと、アイテムがユーザーに表示されず、利用可能なデータ ソースをユーザーが認識できなくなる可能性があります。|  
|データ ソースの管理|名前、説明、および接続情報を表すプロパティを表示します。 このタスクは、フォルダー階層内の共有データ ソース アイテムの表示にも使用します。 このタスクを選択した場合は、"データ ソースの表示" タスクを省略できます。|  
|アイテムへのセキュリティの設定|共有データ ソースへのアクセスを制御するロールの割り当てを作成および変更します。 このタスクは、"データ ソースの表示" タスク、または "データ ソースの管理" タスクのいずれかと併用する必要があります。 それ以外の場合、ユーザーはアイテムを選択できないので効果がありません。|  
  
## <a name="see-also"></a>参照  
 [レポート データ ソースを管理します。](../report-data/manage-report-data-sources.md)   
 [フォルダーをセキュリティで保護する](secure-folders.md)   
 [レポートとリソースを保護します。](secure-reports-and-resources.md)   
 [ネイティブ モードのレポート サーバーに対する権限の許可](granting-permissions-on-a-native-mode-report-server.md)   
 [Reporting Services データ ソースに資格情報を保存する](../report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
  
