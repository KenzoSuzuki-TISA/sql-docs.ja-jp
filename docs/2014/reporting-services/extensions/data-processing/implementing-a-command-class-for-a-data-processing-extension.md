---
title: データ処理拡張機能の Command クラスの実装 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], commands
- Command class
- commands [Reporting Services]
ms.assetid: 465ef8d1-c503-407c-8afd-58d620e344ee
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ed2080a83ff83b6a6b5a5f6739d9c8bf409cdcde
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/13/2018
ms.locfileid: "53361064"
---
# <a name="implementing-a-command-class-for-a-data-processing-extension"></a>データ処理拡張機能の Command クラスの実装
  **Command** オブジェクトを使用して、要求を作成し、それをデータ ソースに渡します。 コマンド テキストは、テキスト、XML など多くのさまざまな構文形式を使用できます。 結果が返されると、**Command** オブジェクトは、**DataReader** オブジェクトとして結果を返します。  
  
 **Command** クラスを作成するには、<xref:Microsoft.ReportingServices.DataProcessing.IDbCommand> を実装します。 **DataReader** オブジェクトとして結果セットを返すには、<xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> メソッドを実装します。 **Command** クラスの <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> メソッドには、引数として <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior> 列挙を取得する実装を含める必要があります。 データ処理拡張機能をレポート デザイナーに配置するには、<xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior.SchemaOnly> メソッドで <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> の場合を処理する実装を含める必要があります。 スキーマだけの実装は、レポート デザイナーにフィールド一覧を提供するために使用します。 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> メソッドによって返される **DataReader** オブジェクトは、フィールド、つまり、列の型および名前の情報を結果セットに含める必要があります。  
  
 必要に応じて、**Command** クラスは <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> を実装できます。 このインターフェイスにより、実装クラスでクエリを分析して、クエリのパラメーターの一覧を返すことができます。 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> インターフェイスの機能を使用できるのはレポート デザイナーだけです。 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> を実装すると、レポート デザイナーのユーザーがプレビュー モードでレポートを実行するたびに、ユーザーにパラメーターを入力するように要求できます。 さらに、**[データセット]** ダイアログの **[パラメーター]** タブでパラメーターを表示できます。  
  
> [!NOTE]  
>  カスタム データ処理拡張機能でパラメーターをサポートしない場合は、<xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> を実装する必要はありません。  
  
 **Command** クラス実装の例については、「[SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)」 (SQL Server Reporting Services 製品サンプル) を参照してください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services の拡張機能](../reporting-services-extensions.md)   
 [データ処理拡張機能の実装](implementing-a-data-processing-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../reporting-services-extension-library.md)  
  
  
