---
title: sp_delete_jobsteplog (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobsteplog
- sp_delete_jobsteplog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobsteplog
ms.assetid: e9ef4c99-abde-4038-b6a3-a25dcbaf0958
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 719038f8ce72bdb05ad9dbf3c3585c377abb3a75
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52526236"
---
# <a name="spdeletejobsteplog-transact-sql"></a>sp_delete_jobsteplog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  引数で指定したすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ ステップ ログを削除します。 このストアド プロシージャを使用して、維持するために、 **sysjobstepslogs**テーブルに、 **msdb**データベース。  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_delete_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
       [ , [ @step_id = ] step_id | [ @step_name = ] 'step_name' ]  
       [ , [ @older_than = ] 'date' ]  
       [ , [ @larger_than = ] 'size_in_bytes' ]  
```  
  
## <a name="arguments"></a>引数  
 [  **@job_id =**] **'**_job_id_**'**  
 削除するジョブ ステップ ログを含むジョブのジョブ識別番号を指定します。 *job_id*は**int**、既定値は NULL です。  
  
 [  **@job_name =**] **'**_job_name_**'**  
 ジョブの名前を指定します。 *job_name*は**sysname**、既定値は NULL です。  
  
> **注:** いずれか*job_id*または*job_name*指定する必要がありますが、両方を指定することはできません。  
  
 [ **@step_id =**] *step_id*  
 ジョブ ステップ ログを削除するジョブ ステップの識別番号を指定します。 ジョブ内のすべてのジョブ ステップ ログを削除する場合を除き、含まれない場合、 **@older_than**または**@larger_than**が指定されています。 *step_id*は**int**、既定値は NULL です。  
  
 [  **@step_name =**] **'**_step_name_**'**  
 ジョブ ステップ ログを削除するジョブ ステップの名前を指定します。 *step_name*は**sysname**、既定値は NULL です。  
  
> **注:** いずれか*step_id*または*step_name*指定できますが、両方を指定することはできません。  
  
 [  **@older_than =**] **'**_日付_**'**  
 保持しておく一番古いジョブ ステップ ログの日時を指定します。 この日時より前のジョブ ステップ ログはすべて削除されます。 *日付*は**datetime**、既定値は NULL です。 両方**@older_than**と**@larger_than**を指定できます。  
  
 [  **@larger_than =**] **'**_size_in_bytes_**'**  
 保持するジョブ ステップ ログの最大サイズをバイト単位で指定します。 このサイズより大きいすべてのジョブ ステップ ログは、削除されます。 両方**@larger_than**と**@older_than**を指定できます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 **sp_delete_jobsteplog**では、 **msdb**データベース。  
  
 場合を除く引数を持たない**@job_id**または**@job_name**は指定すると、指定したジョブのすべてのジョブ ステップ ログが削除されます。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、このストアド プロシージャを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 メンバーだけ**sysadmin**別のユーザーが所有するジョブ ステップ ログを削除することができます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-removing-all-job-step-logs-from-a-job"></a>A. ジョブからすべてのジョブ ステップ ログを削除する  
 次の例では、ジョブ `Weekly Sales Data Backup` のすべてのジョブ ステップ ログを削除します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup';  
GO  
```  
  
### <a name="b-removing-the-job-step-log-for-a-particular-job-step"></a>B. 特定のジョブ ステップに対するジョブ ステップ ログを削除する  
 次の例では、ジョブ `Weekly Sales Data Backup` のステップ 2 に対するジョブ ステップ ログを削除します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 2;  
GO  
```  
  
### <a name="c-removing-all-job-step-logs-based-on-age-and-size"></a>C. 有効期間とサイズに基づいてすべてのジョブ ステップ ログを削除する  
 次の例では、ジョブ `Weekly Sales Data Backup` から、2005 年 10 月 25 日の昼より前の、100 MB より大きいすべてのジョブ ステップ ログを削除します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @older_than = '10/25/2005 12:00:00',  
    @larger_than = 104857600;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_help_jobsteplog &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [SQL Server エージェント ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
