---
title: ポートを列挙します。
description: ポートを列挙します。
ms.assetid: b38c5556-5124-45ea-af2f-4a4cd9313cc7
keywords:
- WDK NDIS をポート NDIS を列挙します。
- WDK の NDIS OID 要求をポートします。
- NDIS ポート WDK、OID 要求
- OID 要求 WDK NDIS ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9858b55d37f59c16dd4a49f5756aadef42be2ee6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538317"
---
# <a name="enumerating-ports"></a>ポートを列挙します。





NDIS プロトコルおよびフィルター ドライバーを使用できる、 [OID\_GEN\_ENUMERATE\_ポート](https://msdn.microsoft.com/library/windows/hardware/ff569583)OID のクエリ要求に関連付けられているアクティブな NDIS ポートの特性を決定する、基になるミニポート アダプター。 NDIS が、この OID を処理し、ミニポート ドライバーには、この OID クエリは受け取りません。

NDIS でクエリの結果は、クエリが成功すると、 [ **NDIS\_ポート\_配列**](https://msdn.microsoft.com/library/windows/hardware/ff566786)構造体。 **NumberOfPorts**の NDIS メンバー\_ポート\_ミニポート アダプターに関連付けられているアクティブなポートの数が配列に含まれています。 **ポート**の NDIS メンバー\_ポート\_配列へのポインターのリストに含まれる[ **NDIS\_ポート\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566791)構造体。 各 NDIS\_ポート\_の特性構造が 1 つのポートの特性を定義します。

 

 




