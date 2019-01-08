---
title: マージ アーティクルの競合追跡と競合解決のレベルの指定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], levels
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 81e9ecb6-1d31-4a78-b32a-96f7f4d67077
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3ff61c601be83ac27c4febb7f31598bdb8fce037
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52810274"
---
# <a name="specify-the-conflict-tracking-and-resolution-level-for-merge-articles"></a>マージ アーティクルの競合追跡と競合解決のレベルの指定
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、マージ アーティクルの競合追跡と回避のレベルを指定する方法について説明します。  
  
 マージ パブリケーションへのサブスクリプションを同期する際、パブリッシャーとサブスクライバーの同じデータに加えられた変更によって、競合が発生していないかどうかがレプリケーション時に確認されます。 競合を行レベルで検出するか (行に加えられたすべての変更が競合と見なされます)、列レベルで検出するか (同じ行と列に対する変更のみが競合と見なされます) を指定できます。 アーティクルの競合解決は行レベルで実行されます。 論理レコードが使用される場合の競合の検出と解決の詳細については、「 [Detecting and Resolving Conflicts in Logical Records](../merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)」を参照してください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
-   **マージ アーティクルに対して競合の追跡と競合解決のレベルを指定するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   サブスクリプションを初期化した後で追跡レベルを変更した場合は、サブスクリプションを再初期化する必要があります。 プロパティ変更の影響の詳細については、「[パブリケーションおよびアーティクルのプロパティの変更](change-publication-and-article-properties.md)」を参照してください。  
  
-   行レベルおよび列レベルの追跡では、行レベルでの競合回避は常に実行されます。優先されなかった行が優先された行で上書きされます。 マージ レプリケーションでは、論理レコード レベルでの競合の追跡と回避も指定できますが、このオプションは [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]にはありません。 レプリケーション ストアド プロシージャからこのオプションを設定する方法については、「 [マージ テーブル アーティクル間に論理レコード リレーションシップを定義する](define-a-logical-record-relationship-between-merge-table-articles.md)」を参照してください。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **[アーティクルのプロパティ]** ダイアログ ボックスの **[プロパティ]** タブで、マージ アーティクルに対する行レベルまたは列レベルの追跡を指定します。このダイアログ ボックスは、パブリケーションの新規作成ウィザードおよび **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで使用できます。 ウィザードの使用およびダイアログ ボックスへのアクセスの詳細については、「[パブリケーションの作成](create-a-publication.md)」および「[View and Modify Publication Properties](view-and-modify-publication-properties.md)」 (パブリケーション プロパティの表示および変更) を参照してください。  
  
#### <a name="to-specify-row--or-column-level-tracking"></a>行レベルまたは列レベルの追跡を指定するには  
  
1.  パブリケーションの新規作成ウィザードの **[アーティクル]** ページまたは **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで、テーブルを選択します。  
  
2.  **[アーティクルのプロパティ]** をクリックし、次に **[反転表示されたテーブル アーティクルのプロパティを設定]** または **[すべてのテーブル アーティクルのプロパティを設定]** をクリックします。  
  
3.  **プロパティ**のタブ、**アーティクルのプロパティ\<資料 >** ダイアログ ボックスで、次のいずれかの値を選択、**追跡レベル**プロパティ。**行レベルの追跡**または**列レベルの追跡**します。  
  
4.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスが表示されている場合は、**[OK]** をクリックして保存し、ダイアログ ボックスを閉じます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-specify-conflict-tracking-options-for-a-new-merge-article"></a>新しいマージ アーティクルの競合追跡オプションを指定するには  
  
1.  パブリッシャーのパブリケーション データベースに対して、 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) を実行し、次のいずれかの値を **@column_tracking**に指定します。  
  
    -   **true** - アーティクルに対して列レベルの追跡を使用します。  
  
    -   **false** - 既定の行レベルの追跡を使用します。  
  
#### <a name="to-change-conflict-tracking-options-for-a-merge-article"></a>マージ アーティクルの競合追跡オプションを変更するには  
  
1.  マージ アーティクルの競合追跡オプションを定義するには、 [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)を実行します。 アーティクルの結果セットの **column_tracking** オプションの値を調べます。 値 **1** は、列レベルの追跡が使用されていることを示します。値 **0** は、行レベルの追跡が使用されていることを示します。  
  
2.  パブリッシャー側のパブリケーション データベースに対して、 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)を実行します。 **@property** に **column_tracking** の値を指定し、**@value** に次のいずれかの値を指定します。  
  
    -   **true** - アーティクルに対して列レベルの追跡を使用します。  
  
    -   **false** - 既定の行レベルの追跡を使用します。  
  
     **@force_invalidate_snapshot** と **@force_reinit_subscription** の両方に **1** の値を指定します。  
  
## <a name="see-also"></a>参照  
 [Advanced Merge Replication Conflict Detection and Resolution](../merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Detecting and Resolving Conflicts in Logical Records](../merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [Define a Logical Record Relationship Between Merge Table Articles](define-a-logical-record-relationship-between-merge-table-articles.md)   
 [マージ レプリケーションの競合の検出と解決](../merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)  
  
  
