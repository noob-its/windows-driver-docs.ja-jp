---
title: MS\_SM\_HbaApiVersion WMI クラス
description: MS\_SM\_HbaApiVersion WMI クラス
ms.assetid: 3d0591e5-ed95-4509-bd27-e122ac9186d2
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2d3b3fa51a7a9477a68c61ef32bd7f233c16b552
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529065"
---
# <a name="mssmhbaapiversion-wmi-class"></a>MS\_SM\_HbaApiVersion WMI クラス


記憶域管理 API をサポートする HBA ミニポート ドライバーは、MS を使用して\_SM\_HbaApiVersion クラスは、現在の HBA の API バージョン。

MS\_SM\_HbaApiVersion クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MS_SM_HbaApiVersion
{
    uint32 WmiHbaApiVersion;  
    uint32 HbaApiVersion;  
    string Description;
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SM\_HbaApiVersion**](https://msdn.microsoft.com/library/windows/hardware/ff563211)

この WMI クラスに関連付けられているメソッドはありません。

 

 




