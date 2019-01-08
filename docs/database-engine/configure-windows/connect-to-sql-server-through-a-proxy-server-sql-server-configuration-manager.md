---
title: プロキシ サーバーで SQL Server に接続する - SQL Server 構成マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 12/15/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Remote WinSock
- RWS
- LATs
- proxy servers [SQL Server]
- connections [SQL Server], proxy server
- Microsoft Proxy Server [SQL Server]
- local address tables [SQL Server]
ms.assetid: 39714de0-2a1f-4179-9091-5c3fa4612545
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5a1abe3ff72d0782b3c0393ca9599c8b57879cc2
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204601"
---
# <a name="connect-to-sql-server-through-a-proxy-server-sql-server-configuration-manager"></a>プロキシ サーバーを介して SQL Server に接続する方法 (SQL Server 構成マネージャー)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックでは、SQL Server 構成マネージャーを使用して、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] でプロキシ サーバーを介して SQL Server に接続する方法について説明します。 リモート WinSock (RWS) 経由でリモートで受信待ちするには、受信待ちするノード アドレスがローカル アドレス テーブル (LAT) のエントリの範囲外になるように、プロキシ サーバーに対して LAT を定義します。  
  
##  <a name="SSMSProcedure"></a> SQL Server 構成マネージャーの使用  
  
#### <a name="to-enable-connections-to-sql-server-through-microsoft-proxy-server"></a>Microsoft Proxy Server を介して SQL Server に接続できるようにするには  
  
1.  「[特定の TCP ポートで受信待ちするようにサーバーを構成する方法 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)」の手順に従い、[!INCLUDE[ssDE](../../includes/ssde-md.md)] で使用される TCP/IP ポートを判断するか、任意のポートを使用するように [!INCLUDE[ssDE](../../includes/ssde-md.md)] を構成します。  
  
2.  プロキシ サーバーで、プロキシ サーバー用のローカル アドレス テーブル (LAT) を定義し、受信待ちするノード アドレスが LAT エントリの範囲外になるようにします。 詳細については、プロキシ サーバーのマニュアルを参照してください。  
  
> [!NOTE]
>  このトピックの対象は、オンプレミスの [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]です。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]に関連する接続問題については、 [「Troubleshoot connection issues to Azure SQL Database」](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-common-connection-issues)(Azure SQL Database の接続問題のトラブルシューティング) を参照してください。  


