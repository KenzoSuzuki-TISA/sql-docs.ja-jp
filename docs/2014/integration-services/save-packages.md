---
title: パッケージを保存する | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 17c1de2c-637f-45c2-a148-79294bae0af4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 618e34d05c2958d51116f77f07b1235995c03719
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52761254"
---
# <a name="save-packages"></a>パッケージを保存する
  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] では、 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーを使用してパッケージを構築し、XML ファイル (.dtsx ファイル) としてファイル システムに保存します。 パッケージ XML ファイルのコピーは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の msdb データベースまたはパッケージ ストアに保存することもできます。 パッケージ ストアとは、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスが管理するファイル システムの場所にあるフォルダーのことです。  
  
 ファイル システムに保存したパッケージは、後で [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスを使用して、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] またはパッケージ ストアにインポートできます。 詳細については、「[パッケージをインポートおよびエクスポートする (SSIS サービス)](../../2014/integration-services/import-and-export-packages-ssis-service.md)」を参照してください。  
  
 また、コマンド プロンプト ユーティリティの **dtutil** を使用して、ファイル システムと msdb 間でパッケージをコピーできます。 詳細については、「 [dtutil ユーティリティ](dtutil-utility.md)」を参照してください。  
  
### <a name="to-save-a-package"></a>パッケージを保存するには  
  
-   [ファイル システムにパッケージを保存する](../../2014/integration-services/save-a-package-to-the-file-system.md)  
  
-   [パッケージのコピーを保存する](../../2014/integration-services/save-a-copy-of-a-package.md)  
  
  
