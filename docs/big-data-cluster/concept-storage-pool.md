---
title: 記憶域プールとは何ですか。
titleSuffix: SQL Server 2019 big data clusters
description: この記事では、SQL Server 2019 のビッグ データ クラスターで記憶域プールについて説明します。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: c89ddc5d155af4542b5101e9a6e394effc5d9fd3
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241523"
---
# <a name="what-is-the-storage-pool-sql-server-2019-big-data-clusters"></a>記憶域プール (SQL Server 2019 ビッグ データ クラスター) とは何ですか。

この記事では、の役割を説明します、 *SQL Server の記憶域プール*で SQL Server 2019 ビッグ データ クラスター (プレビュー)。 次のセクションでは、アーキテクチャと SQL の記憶域プールの機能について説明します。

## <a name="storage-pool-architecture"></a>記憶域プールのアーキテクチャ

記憶域プールは、記憶域ノードから成る Linux、Spark、および HDFS 上の SQL Server で構成されます。 SQL のビッグ データ クラスター内のすべての記憶域ノードは、HDFS クラスターのメンバーです。

![記憶域プールのアーキテクチャ](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>責任

記憶域ノードは責任を負います。

- Spark からデータの取り込み。
- HDFS (Parquet 形式) でデータ ストレージ。 HDFS では、HDFS のデータが SQL のビッグ データ クラスター内のすべての記憶域ノードに分散され、データの永続性も提供します。
- HDFS と SQL Server エンドポイント経由のデータ アクセス。

## <a name="next-steps"></a>次の手順

SQL Server のビッグ データ クラスターに関する詳細については、次の概要を参照してください。

- [SQL Server 2019 ビッグ データ クラスターとは](big-data-cluster-overview.md)
