---
title: 非推奨のシステム ストアド プロシージャへの参照の削除 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- undocumented system stored procedures [SQL Server]
- system stored procedures [SQL Server]
ms.assetid: 487d24fc-41d5-495e-843c-0ac974ec472f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bc0dbcc5296ad9ef0e8df6e94b1978fe10792c4e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183359"
---
# <a name="remove-references-to-deprecated-system-stored-procedures"></a>非推奨ｎおシステム ストアド プロシージャの参照の削除
  アップグレード アドバイザーによって、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用できなくなった、ドキュメントに記載されていないシステム ストアド プロシージャおよび拡張ストアド プロシージャを参照するステートメントが検出されました。 これらのオブジェクトを参照するステートメントは失敗します。 今後のリリースで予告なしに機能が変更または削除される可能性があるので、ドキュメントに記載されていないシステム オブジェクトまたは API を使用しないでください。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>説明  
  
### <a name="documented-system-stored-procedures"></a>ドキュメントに記載されているシステム ストアド プロシージャ  
 ドキュメントに記載されている以下のシステム ストアド プロシージャは削除されています。  
  
-   sp_addalias  
  
-   sp_addgroup  
  
-   sp_changegroup  
  
-   sp_dropgroup  
  
-   sp_helpgroup  
  
### <a name="undocumented-system-stored-procedures"></a>ドキュメントに記載されていないシステム ストアド プロシージャ  
 ドキュメントに記載されていない以下のシステム ストアド プロシージャおよび拡張ストアド プロシージャは削除されています。  
  
-   sp_articlesynctranprocs  
  
-   sp_diskdefault  
  
-   sp_EventLog  
  
-   sp_GetMBCSCharLen  
  
-   sp_helplog  
  
-   sp_helpsql  
  
-   sp_IsMBCSLeadByte  
  
-   sp_lock2  
  
-   sp_MSget_current_activity  
  
-   sp_MSset_current_activity  
  
-   sp_MSobjessearch  
  
-   xp_enum_ActiveScriptEngines  
  
-   xp_eventlog  
  
-   xp_GetAdminGroupName  
  
-   xp_GetFileDetails  
  
-   xp_GetLocalSystemAccountName  
  
-   xp_IsNTAdmin  
  
-   xp_MSLocalSystem  
  
-   xp_MSnt2000  
  
-   xp_MSplatform  
  
-   xp_SetSecurity  
  
-   xp_varbintohexstr  
  
## <a name="corrective-action"></a>修正措置  
  
### <a name="documented-system-stored-procedures"></a>ドキュメントに記載されているシステム ストアド プロシージャ  
 次の表に従ってアプリケーションを修正してください。  
  
|以前のシステム ストアド プロシージャ|方法|  
|----------------|-------------|  
|sp_addalias|別名をユーザー アカウントとデータベース ロールの組み合わせで置き換えてください。 詳細については、SQL Server オンライン ブックの「CREATE USER (Transact-SQL)」および「CREATE ROLE (Transact-SQL)」を参照してください。 アップグレードされたデータベースで別名を削除するには、sp_dropalias を使用します。|  
|sp_addgroupsp_changegroup<br /><br /> sp_dropgroup<br /><br /> sp_helpgroup|ロールを使用します。 詳細については、SQL Server オンライン ブックの「サーバー レベルのロール」および「データベース レベルのロール」を参照してください。|  
  
### <a name="undocmented-system-stored-procedures"></a>Undocmented システム ストアド プロシージャ  
 ドキュメントに記載されていないシステム ストアド プロシージャの代わりに、同じ機能を持つ CLR ストアド プロシージャを作成できます。 詳細については、SQL Server オンライン ブックの「CLR ストアド プロシージャ」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データベース エンジンのアップグレードに関する問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 アップグレード アドバイザー&#91;新規&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
