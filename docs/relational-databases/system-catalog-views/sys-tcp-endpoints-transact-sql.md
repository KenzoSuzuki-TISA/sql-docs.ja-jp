---
title: sys.tcp_endpoints (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.tcp_endpoints
- sys.tcp_endpoints_TSQL
- tcp_endpoints
- tcp_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.tcp_endpoints catalog view
ms.assetid: 43cc3afa-cced-4463-8e97-fbfdaf2e4fa8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ad6a7f9e9c727f88015b9b815a37a5825e3b2f47
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47805510"
---
# <a name="systcpendpoints-transact-sql"></a>sys.tcp_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  システム内の各 TCP エンドポイントごとに 1 行のデータを保持します。 によって記述されるエンドポイント**sys.tcp_endpoints**許可し、接続権限を取り消すオブジェクトを提供します。 ポートおよび IP アドレスに関して表示される情報は、プロトコルの構成に使用されるものではなく、実際のプロトコルの構成と一致しない場合もあります。 表示し、プロトコルの構成を使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager。  
  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**< 継承された列 >**||列を継承[sys.endpoints](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)します。|  
|**port**|ssNoversion|エンドポイントがリッスンするポート番号です。 NULL 値は許可されません。|  
|**is_dynamic_port**|bit|1 = ポート番号が動的に割り当てられました。<br /><br /> NULL 値は許可されません。|  
|**ip_address**|**nvarchar(45)**|LISTENER_IP 句で指定されたリスナーの IP アドレスです。 NULL 値が許可されます。|  
  
## <a name="remarks"></a>コメント  
 次のクエリを実行して、エンドポイントおよび接続に関する情報を収集します。 現在の接続または TCP 接続を使用しないエンドポイントは、NULL 値と共に表示されます。 追加、**場所**句`WHERE des.session_id = @@SPID`現在の接続に関する情報を返します。  
  
```  
SELECT des.login_name, des.host_name, program_name,  dec.net_transport, des.login_time,   
e.name AS endpoint_name, e.protocol_desc, e.state_desc, e.is_admin_endpoint,   
t.port, t.is_dynamic_port, dec.local_net_address, dec.local_tcp_port   
FROM sys.endpoints AS e  
LEFT JOIN sys.tcp_endpoints AS t  
   ON e.endpoint_id = t.endpoint_id  
LEFT JOIN sys.dm_exec_sessions AS des  
   ON e.endpoint_id = des.endpoint_id  
LEFT JOIN sys.dm_exec_connections AS dec  
   ON des.session_id = dec.session_id;  
```  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [エンドポイントのカタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)  
  
  
