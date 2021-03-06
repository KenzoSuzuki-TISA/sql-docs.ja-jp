---
title: ローカルの CDC Service を管理する方法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7f9be649-cd93-40c1-bc48-0480106f207c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fe88db4809b69abf292ae0888786bc4606785c3d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52773044"
---
# <a name="how-to-manage-a-local-cdc-service"></a>ローカルの CDC Service を管理する方法
  この手順では、CDC Service 構成コンソールを使用して特定の CDC サービスを管理する方法について説明します。  
  
### <a name="to-manage-a-specific-cdc-service"></a>特定の CDC Service を管理するには  
  
1.  **[スタート]** メニューの **[CDC Service Configuration for Oracle]** をクリックします。  
  
2.  CDC Service 構成コンソールの左ペインで **[ローカルの CDC Service]** を展開します。  
  
3.  操作する CDC サービスを選択します。  
  
     操作する CDC サービスを右クリックして、目的のアクションをクリックすることもできます。  
  
     **または**  
  
     CDC Service 構成コンソールの左ペインで **[ローカルの CDC Service]** をクリックし、作業するサービスを CDC Service 構成コンソールの中央のセクションで選択します。  
  
     操作する CDC サービスを右クリックして、目的のアクションをクリックすることもできます。  
  
4.  CDC サービスの操作時には、以下のタスクを実行できます。  
  
    -   **サービスの削除**  
  
         サービスを削除するには、CDC Service 構成コンソールの右側にある **[アクション]** ペインで **[削除]** をクリックします。  
  
         または、削除する CDC サービスを右クリックして **[削除]** を選択します。  
  
         **注**:サービスを削除するときに、サービスが実行されている場合は、削除する前に、サービスが停止しました。  
  
         Oracle CDC Windows Service の定義を削除するには、プログラムに、関連付けられている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内の MSXDBCDC データベースに対する更新アクセスが必要です。 **[OK]** をクリックしてサービスを削除すると、MSXDBCDC データベース内にある Oracle CDC Service 登録の削除が試みられます。 権限がないために削除できない場合、MSXDBCDC データベースに対する更新アクセスを持つ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを入力するためのダイアログ ボックスが表示されます。  
  
         [SQL Server への接続] ダイアログ ボックスに入力するデータについては、「 [Manage an Oracle CDC Service](manage-an-oracle-cdc-service.md) 」および「 [Connection to SQL Server for Delete](connection-to-sql-server-for-delete.md)」を参照してください。  
  
    -   **CDC Service のプロパティの編集**  
  
         CDC Service 構成コンソールの右側にある **[アクション]** ペインで **[プロパティ]** をクリックします。  
  
         または、プロパティを編集する CDC サービスを右クリックして **[プロパティ]** を選択します。  
  
## <a name="see-also"></a>参照  
 [Manage an Oracle CDC Service](manage-an-oracle-cdc-service.md)  
  
  
