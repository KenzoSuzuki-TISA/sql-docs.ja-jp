---
title: sys.dm_xe_session_object_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xe_session_object_columns_TSQL
- sys.dm_xe_session_object_columns_TSQL
- dm_xe_session_object_columns
- sys.dm_xe_session_object_columns
dev_langs:
- TSQL
helpviewer_keywords:
- xe
- sys.dm_xe_session_object_columns dynamic management view
ms.assetid: e97f3307-2da6-4c54-b818-a474faec752e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e87e0d981d2ee6f18368394329cf524da7e49a22
ms.sourcegitcommit: f46fd79fd32a894c8174a5cb246d9d34db75e5df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/26/2018
ms.locfileid: "53785843"
---
# <a name="sysdmxesessionobjectcolumns-transact-sql"></a>sys.dm_xe_session_object_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  セッションにバインドされたオブジェクトの構成値を示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|イベント セッションのメモリ アドレス。 sys.dm_xe_sessions.address との多対一のリレーションシップがあります。 NULL 値は許可されません。|  
|column_name|**nvarchar (256)**|構成値の名前。 NULL 値は許可されません。|  
|column_id|**int**|列の ID。 オブジェクト内で一意です。 NULL 値は許可されません。|  
|column_value|**nvarchar(3072)**|列の構成値。 NULL 値が許可されます。|  
|object_type|**nvarchar(60)**|オブジェクトの古い型。 NULL 値は許可されません。 object_type はの 1 つです。<br /><br /> イベント<br /><br /> ターゲット (target)|  
|object_name|**nvarchar (256)**|この列が所属するオブジェクトの名前。 NULL 値は許可されません。|  
|object_package_guid|**uniqueidentifier**|オブジェクトを含むパッケージの GUID。 NULL 値は許可されません。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
### <a name="relationship-cardinalities"></a>リレーションシップの基数  
  
|From|変換先|リレーションシップ|  
|----------|--------|------------------|  
|dm_xe_session_object_columns.object_name、<br /><br /> dm_xe_session_object_columns.object_package_guid|、sys.dm_xe_objects.package_guid<br /><br /> sys.dm_xe_objects.name|多対一|  
|dm_xe_session_object_columns.column_name、<br /><br /> dm_xe_session_object_columns.column_id|sys.dm_xe_object_columns.name、<br /><br /> sys.dm_xe_object_columns.column_id|多対一|  
  
## <a name="see-also"></a>参照  
 [動的管理ビューおよび関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

