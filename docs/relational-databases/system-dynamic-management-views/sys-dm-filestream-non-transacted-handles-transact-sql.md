---
title: sys.dm_filestream_non_transacted_handles (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_filestream_non_transacted_handles_TSQL
- dm_filestream_non_transacted_handles
- dm_filestream_non_transacted_handles_TSQL
- sys.dm_filestream_non_transacted_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_filestream_non_transacted_handles dynamic management view
ms.assetid: 507ec125-67dc-450a-9081-94cde5444a92
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2b25594feb96fe10f0a04ad0ab542fd582089759
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/27/2018
ms.locfileid: "52411629"
---
# <a name="sysdmfilestreamnontransactedhandles-transact-sql"></a>sys.dm_filestream_non_transacted_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  FileTable データに関連付けられており、現在開いている非トランザクション ファイル ハンドルを表示します。  
  
 このビューには、開かれているファイル ハンドルごとに 1 つの行が含まれています。 このビューのデータはサーバーの現在の内部状態に対応しているので、ハンドルが開かれたり閉じられたりするたびに、データが変化します。 このビューでは、履歴情報は含まれません。  
  
 詳細については、「 [FileTable の管理](../../relational-databases/blob/manage-filetables.md)」を参照してください。  
  
|**列**|**型**|**[説明]**|  
|----------------|--------------|---------------------|  
|database_id|ssNoversion|ハンドルが関連付けられているデータベースの ID。|  
|object_id|ssNoversion|ハンドルが関連付けられている FileTable のオブジェクト ID。|  
|handle_id|ssNoversion|一意のハンドル コンテキスト ID。 使用される、 [sp_kill_filestream_non_transacted_handles &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)ストアド プロシージャを特定のハンドルを強制終了します。|  
|file_object_type|ssNoversion|ハンドルの種類。 ハンドルを開くときの対象だった階層のレベル (つまりデータベースまたはアイテム) を示します。|  
|file_object_type_desc|nvarchar(120)|「未定義」<br />"SERVER_ROOT"<br />"DATABASE_ROOT"<br />"TABLE_ROOT"、<br />"TABLE_ITEM"|  
|correlation_process_id|varbinary(8)|要求を生成したプロセスの一意な識別子を格納します。|  
|correlation_thread_id|varbinary(8)|要求を生成したスレッドの一意な識別子を格納します。|  
|file_context|varbinary(8)|このハンドルで使用されるファイル オブジェクトへのポインター。|  
|state|ssNoversion|ハンドルの現在の状態。 通常は、アクティブ、閉じられた、強制終了された、のいずれかです。|  
|state_desc|nvarchar(120)|"ACTIVE"、<br />"CLOSED"、<br />「終了」|  
|current_workitem_type|ssNoversion|このハンドルが現在処理されている状態。|  
|current_workitem_type_desc|nvarchar(120)|"NoSetWorkItemType"<br />"FFtPreCreateWorkitem"<br />"FFtGetPhysicalFileNameWorkitem"<br />"FFtPostCreateWorkitem"<br />"FFtPreCleanupWorkitem"<br />"FFtPostCleanupWorkitem"<br />"FFtPreCloseWorkitem"<br />"FFtQueryDirectoryWorkItem"<br />"FFtQueryInfoWorkItem"<br />"FFtQueryVolumeInfoWorkItem"<br />"FFtSetInfoWorkitem"<br />"FFtWriteCompletionWorkitem"|  
|fcb_id|BIGINT|FileTable のファイル制御ブロック ID。|  
|item_id|varbinary(892)|ファイルまたはディレクトリのアイテム ID。 通常、サーバーのルートのハンドルは NULL です。|  
|is_directory|bit|ディレクトリであることを示します。|  
|item_name|nvarchar (512)|項目の名前。|  
|opened_file_name|nvarchar (512)|最初に開くことを要求されたパス。|  
|database_directory_name|nvarchar (512)|opened_file_name の一部で、データベースのディレクトリ名を表す部分。|  
|table_directory_name|nvarchar (512)|opened_file_name の一部で、テーブルのディレクトリ名を表す部分。|  
|remaining_file_name|nvarchar (512)|opened_file_name の一部で、残りのディレクトリ名を表す部分。|  
|open_time|DATETIME|ハンドルが開かれた時刻。|  
|flags|ssNoversion|ShareFlagsUpdatedToFcb = 0x1、<br />DeleteOnClose = 0x2、<br />NewFile = 0x4、<br />PostCreateDoneForNewFile = 0x8、<br />StreamFileOverwritten = 0x10、<br />RequestCancelled = 0x20、<br />NewFileCreationRolledBack = 0x40|  
|login_id|ssNoversion|ハンドルを開いたプリンシパルの ID。|  
|login_name|nvarchar (512)|ハンドルを開いたプリンシパルの名前。|  
|login_sid|varbinary (85)|ハンドルを開いたプリンシパルの SID。|  
|read_access|bit|読み取りアクセス用に開かれました。|  
|write_access|bit|書き込みアクセス用に開かれました。|  
|delete_access|bit|削除アクセス用に開かれました。|  
|share_read|bit|share_read を許可して開かれました。|  
|share_write|bit|share_write を許可して開かれました。|  
|share_delete|bit|share_delete を許可して開かれました。|  
  
## <a name="see-also"></a>参照  
 [FileTable の管理](../../relational-databases/blob/manage-filetables.md)  
  
  
