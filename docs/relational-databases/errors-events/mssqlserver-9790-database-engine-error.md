---
title: MSSQLSERVER_9790 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9790 (Database Engine error)
ms.assetid: 83fd379f-5deb-4f97-8cb4-282e3d3fed94
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dd965940d43fdcc1e2420e8c5a43e512b45298e2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840400"
---
# <a name="mssqlserver9790"></a>MSSQLSERVER_9790
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|9790|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SB3_XMIT_ERROR_ENTRANCE_BROKER_SINGLE_USER|  
|メッセージ テキスト|着信メッセージをルーティングできません。 ルーティング情報を保持するシステム データベース MSDB がシングル ユーザー モードです。|  
  
## <a name="explanation"></a>説明  
MSDB データベースがシングル ユーザー モードであったため、外部から受信したメッセージを分類しようとしたときにエラーが発生しました。  
  
## <a name="user-action"></a>ユーザーの操作  
ALTER DATABASE コマンドを使用して、MSDB をマルチ ユーザー モードに変更します。  
  
