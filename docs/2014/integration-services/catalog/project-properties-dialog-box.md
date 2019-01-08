---
title: '[プロジェクトのプロパティ] ダイアログ ボックス | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.isprojectprop.general.f1
- sql12.ssis.ssms.isprojectprop.permissions.f1
ms.assetid: d5cf52f5-1fe2-438a-98a3-fe117360acf8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 48e299e72343987d0738c739404284314f23dcf5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52759044"
---
# <a name="project-properties-dialog-box"></a>[プロジェクトのプロパティ] ダイアログ ボックス
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトは、配置の 1 単位です。 各プロジェクトには、パッケージ、パラメーター、および環境の参照を含めることができます。 プロジェクトはセキュリティ保護可能なオブジェクトであり、データベース プリンシパルの権限を定義できます。 プロジェクトを再配置するときに、以前のバージョンのプロジェクトを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログに保存できます。  
  
 プロジェクト パラメーターとパッケージ パラメーターを使用して、実行時にパッケージ内のプロパティに値を割り当てることができます。 パッケージを実行する前に値が必要なパラメーターもあります。 環境変数を参照するパラメーター値がある場合は、実行する前に、プロジェクトに対応する環境の参照を含めておく必要があります。  
  
 **目的に合ったトピックをクリックしてください**  
  
-   [[プロジェクトのプロパティ] ダイアログ ボックスを開く](#open_dialog)  
  
-   [[全般] ページのオプションの設定](#general)  
  
-   [[権限] ページのオプションの設定](#permissions)  
  
##  <a name="open_dialog"></a> [プロジェクトのプロパティ] ダイアログ ボックスを開く  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]から [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに接続します。  
  
     SSISDB データベースをホストする [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続されます。  
  
2.  オブジェクト エクスプローラーで、ツリーを展開して、 **[Integration Services カタログ]** ノードを表示します。  
  
3.  **[SSISDB]** ノードを展開します。  
  
4.  プロパティを設定するプロジェクトが格納されているフォルダーを展開します。  
  
5.  プロジェクトを右クリックし、 **[プロパティ]** をクリックします。  
  
##  <a name="general"></a> [全般] ページのオプションの設定  
 プロジェクトのプロパティを表示するには、[全般] ページを使用します。  
  
 **名前**  
 プロジェクト名を一覧表示します。  
  
 **[Identifier]**  
 プロジェクト ID を一覧表示します。  
  
 **[説明]**  
 プロジェクトの説明を表示します (省略可)。  
  
 **プロジェクトのバージョン**  
 プロジェクトのバージョンを一覧表示します。  
  
 **配置日**  
 プロジェクトを配置または再配置した日付と時刻を一覧表示します。  
  
##  <a name="permissions"></a> [権限] ページのオプションの設定  
 プロジェクトの明示的な権限を表示および設定するには、 **[権限]** ページを使用します。  
  
 参照  
 **[参照]** をクリックすると、 **[すべてのプリンシパルを参照]** ダイアログ ボックスを使用して、権限を設定するユーザーおよびロールを選択できます。  
  
 **名前**  
 ユーザーまたはロールの名前を一覧表示します。  
  
 **型**  
 ユーザーまたはロールの種類を一覧表示します。  
  
 **権限**  
 権限を一覧表示します。  
  
 **Grantor**  
 権限を付与するユーザーまたはロールを一覧表示します。  
  
 **Grant**  
 **[許可]** を選択すると、選択したユーザーまたはロールに対して権限が付与されます。  
  
 **Deny**  
 **[拒否]** を選択すると、選択したユーザーまたはロールに対する権限が拒否されます。  
  
  
