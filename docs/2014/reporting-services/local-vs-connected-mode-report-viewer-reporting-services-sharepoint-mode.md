---
title: レポート ビューアーでのローカル モードと接続モードのレポート ビューアー (Reporting Services の SharePoint モード) レポート |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: a230a9bb-6046-401f-b5e5-53ff6edf2264
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: b51ca3d0cc9e8716f090677f3e61d1177df746f6
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/13/2018
ms.locfileid: "53372294"
---
# <a name="local-mode-vs-connected-mode-reports-in-the-report-viewer-reporting-services-in-sharepoint-mode"></a>レポート ビューアーでのローカル モードと接続モードのレポート (Reporting Services の SharePoint モード)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポートは、 *レポート サーバーを使用する、* ローカル モード *または*接続モード [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のいずれかで実行するように構成できます。 代わりに、データ拡張機能でローカル モード レポートがサポートされている場合は、レポート ビューアーを使用して SharePoint から直接レポートを表示できます。 この方法は、 *ローカル モード*と呼ばれます。 以前のバージョンの [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]では、レポート ビューアー コントロールでレポートを表示できるように、SharePoint モードで構成されている [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバーに SharePoint ファームが接続されている必要がありました。 この方法は、 *リモート モード* または *接続モード*と呼ばれます。  
  
 *ローカル モード* では、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバーはありません。 SharePoint 製品用に [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインをインストールする必要がありますが、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバーは必須ではありません。 ローカル モードでは、ユーザーはレポートを表示できますが、サブスクリプションやデータ警告などのサーバー側機能にはアクセスできません。  
  
||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint モード:|  
  
 **このトピックの内容:**  
  
-   [ローカル モードと接続モードおよびサポートされる拡張機能](#bkmk_local_vs_connected)  
  
-   [SharePoint 2013 でのローカル モードと Access Services の構成](#bkmk_local_mode_sharepoint2013)  
  
-   [SharePoint 2010 でのローカル モード レポートの作成](#bkmk_local_mode_sharepoint2010)  
  
##  <a name="bkmk_local_vs_connected"></a> ローカル モードと接続モードおよびサポートされる拡張機能  
 **ローカル モード:** ローカル モードをサポートしているデータ拡張機能を使用している場合は、レポート ビューアーによって SharePoint から直接レポートが表示されます。 *ローカル モード* では、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバーはありません。 SharePoint 製品用に [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインをインストールする必要がありますが、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバーは必須ではありません。 ローカル モードでは、ユーザーはレポートを表示できますが、サブスクリプションやデータ警告などのサーバー側機能には **アクセスできません** 。  
  
 **接続モード**( *リモート モード* とも呼ばれる) では、レポート ビューアー コントロールでレポートを表示できるように、SharePoint モードの [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバーが SharePoint ファームに接続されている必要があります。  
  
 ローカル モード レポートをサポートしているデータ処理拡張機能の一覧を次に示します。  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Access 2010 レポート拡張機能。 Access Services の詳細については、次を参照してください[Access Services と SQL Reporting Services:。インストールの SQL Server 2008 R2 Reporting Services アドイン (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=192686)します。  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint リスト データ拡張機能。 SharePoint リスト データ拡張機能の詳細については、「 [Reporting Services でサポートされるデータ ソース &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
 カスタム データ処理拡張機能を開発して、ローカル モードをサポートすることもできます。 詳細については、「 [Implementing a Data Processing Extension](extensions/data-processing/implementing-a-data-processing-extension.md)」を参照してください。  
  
 ローカル モードでは、データ ソースが埋め込まれているレポート、または .rsds ファイルの共有データ ソースが含まれているレポートを表示できます。 ただし、レポートまたはその関連データ ソースを管理することはできません。 データ ソースを編集しようとすると、データ ソースの編集はローカル モードではサポートされないというエラーが表示されます。 SharePoint サイトのデータ ソース管理は、接続モードでのみサポートされます。  
  
> [!NOTE]  
>  以前のバージョンと同様に、.rsds ファイルにユーザー名とパスワードを埋め込むことはできません。  
  
##  <a name="bkmk_local_mode_sharepoint2013"></a> SharePoint 2013 でのローカル モードと Access Services の構成  
 既存の Access 2010 Web データベースと [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ローカル モードをサポートするように SharePoint 2013 ファームを構成できます。 詳細については、「 [SharePoint Server 2013 での Web データベース用の Access Services 2010 のセットアップと構成](https://technet.microsoft.com/library/ee748653\(office.15\).aspx)」を参照してください。  
  
 SharePoint 2013 用の新しい Access Web データベースを作成することはできません。 Access 2013 では、新しい種類のデータベース (Access で構築される *Access Web App* ) が使用されるので、Web ブラウザーで SharePoint アプリケーションとして使用し、他のユーザーと共有します。  
  
 詳細については、次を参照してください。  
  
-   [Access 2013 の新機能](http://office.microsoft.com/access-help/what-s-new-in-access-2013-HA102809500.aspx) (http://office.microsoft.com/access-help/what-s-new-in-access-2013-HA102809500.aspx)。  
  
-   [Access アプリの基本的なタスク](http://office.microsoft.com/access-help/basic-tasks-for-an-access-app-HA102840210.aspx?CTT=5&origin=HA102809500) (http://office.microsoft.com/access-help/basic-tasks-for-an-access-app-HA102840210.aspx?CTT=5&origin=HA102809500)。  
  
##  <a name="bkmk_local_mode_sharepoint2010"></a> SharePoint 2010 でのローカル モード レポートの作成  
 ローカル モードには ASP.NET セッション状態が必要です。 Access サービスをインストールすると、ASP.NET セッション状態が有効になります。 PowerShell を使用して有効にすることもできます。  
  
1.  SharePoint 2010 管理シェルを開きます。  
  
2.  次のコマンドを入力します。  
  
    ```  
    - Enable-SPSessionStateService  
    ```  
  
3.  プロンプトが表示されたら、データベースの名前を入力します。  
  
4.  IIS リセットを実行します。  
  
 詳細については、次を参照してください[Access Services と SQL Reporting Services:。インストールの SQL Server 2008 R2 Reporting Services アドイン (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=192686)と[Enable-spsessionstateservice](https://technet.microsoft.com/library/ff607857\(v=office.15\).aspx)します。  
  
## <a name="connected-mode"></a>または  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 接続モードでの ADS 拡張機能の使用に関する最新情報については、「[Access Services Report in SharePoint Site shows error in data extension 'ADS'](https://social.technet.microsoft.com/wiki/contents/articles/25298.access-services-report-in-sharepoint-site-shows-error-in-data-extension-ads.aspx)」 (SharePoint サイトの Access Services レポートでデータ拡張機能 'ADS' のエラーが表示される) を参照してください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services でサポートされるデータ ソース (SSRS)](create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
