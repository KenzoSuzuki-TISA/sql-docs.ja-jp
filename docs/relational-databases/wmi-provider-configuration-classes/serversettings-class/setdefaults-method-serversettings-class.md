---
title: SetDefaults メソッド (ServerSettings クラス) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (ServerSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: 76e4cfab-4b15-4da4-bb2f-8aac6f927f79
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 5e7a9dfd6d68f25b98469a79850444fc4726d785
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/15/2018
ms.locfileid: "51668081"
---
# <a name="setdefaults-method-serversettings-class"></a>SetDefaults メソッド (ServerSettings クラス)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  インスタンスのすべての既定値を設定[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]既存のデータを上書きするオプションを使用します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>要素  
 *object*  
 A [ServerSettings クラス](../../../relational-databases/wmi-provider-configuration-classes/serversettings-class/serversettings-class.md)を表すオブジェクトを[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]クライアント インスタンス。  
  
#### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|---------------|-----------------|  
|*OverwriteAll*|インスタンス上の既存の値を上書きするかどうかを指定するブール値[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: **true**既存のデータを上書きするか、 **false**既存のデータを上書きしない場合。|  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 u**int32** 値。サービスが正常に変更された場合は 0、要求がサポートされない場合は 1 になります。それ以外の数値はエラーを示します。  
  
## <a name="remarks"></a>コメント  
  
## <a name="see-also"></a>参照  
 [サーバー ネットワーク プロトコルとネットワーク ライブラリの構成](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
