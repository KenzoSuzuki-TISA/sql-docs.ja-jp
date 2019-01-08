---
title: SQL Server 照合順序名 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], SQL collations
- SQL collations
- names [SQL Server], collations
ms.assetid: 56483d24-add7-483d-9b96-c6fda460ddbc
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 765f825a690af65ec4740975cc21c5364d133bb5
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211401"
---
# <a name="sql-server-collation-name-transact-sql"></a>SQL Server 照合順序名 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序の照合順序名を指定する単一の文字列です。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は Windows 照合順序をサポートします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が Windows 照合順序をサポートする前に開発された、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序と呼ばれる、限られた数 (<80) の照合順序をサポートしています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序は旧バージョンとの互換性を維持するためにサポートされていますが、新規の開発作業に使用しないでください。 Windows 照合順序について詳しくは、「[Windows 照合順序名 &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)」をご覧ください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
<SQL_collation_name> :: =   
SQL_SortRules[_Pref]_CPCodepage_<ComparisonStyle>  
  
<ComparisonStyle> ::=  
_CaseSensitivity_AccentSensitivity | _BIN  
```  
  
## <a name="arguments"></a>引数  
 *SortRules*  
 辞書順での並べ替えを指定した場合に適用される、並べ替え規則を持つアルファベットまたは言語を示す文字列です。 たとえば、Latin1_General や Polish を指定します。  
  
 **Pref**  
 大文字優先を指定します。 場合でも、大文字と小文字の比較は、その他の区別がない場合に小文字のバージョンでは、前に、文字の大文字バージョンを並べ替えます。  
  
 *Codepage*  
 照合順序で使用されるコード ページを識別する 1 ～ 4 桁の番号を指定します。 **CP1** はコード ページ 1252 を示します。他のすべてのコード ページの場合は、完全なコード ページ番号を指定します。 たとえば、**CP1251** はコード ページ 1251 を示し、**CP850** はコード ページ 850 を示します。  
  
 *CaseSensitivity*  
 **CI** を指定すると大文字小文字は区別されず、**CS** を指定すると大文字小文字が区別されます。  
  
 *AccentSensitivity*  
 **AI** を指定するとアクセントは区別されず、**AS** を指定するとアクセントが区別されます。  
  
 **BIN**  
 使用するバイナリ並べ替え順を指定します。  
  
## <a name="remarks"></a>Remarks  
 現在のサーバーでサポートされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序の一覧を表示するには、次のクエリを実行します。  
  
```  
SELECT * FROM sys.fn_helpcollations()   
WHERE name LIKE 'SQL%';  
```  

> [!NOTE]
>  並べ替え順 ID 80 では、コード ページ 1250 およびバイナリ順の任意の Window 照合順序を使用します。 例 :Albanian_BIN、Croatian_BIN、Czech_BIN、Romanian_BIN、Slovak_BIN、Slovenian_BIN。  
  
## <a name="see-also"></a>参照  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [定数 &#40;Transact-SQL&#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqlserver)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [テーブル &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)  
  
  
