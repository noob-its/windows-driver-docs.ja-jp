---
title: DirectMusic ストリームのデータ形式
description: DirectMusic ストリームのデータ形式
ms.assetid: f3aae6c0-6b9d-43fa-9ef1-d6702017f55d
keywords:
- DirectMusic WDK のオーディオ ストリームのデータを形式します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98b91ae32aa25d6a95d78afd2cf03544de85fd6b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573195"
---
# <a name="directmusic-stream-data-format"></a>DirectMusic ストリームのデータ形式


## <span id="directmusic_stream_data_format"></span><span id="DIRECTMUSIC_STREAM_DATA_FORMAT"></span>


この例では、 [ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656) DirectMusic ストリームのデータ形式を記述する構造体。

```cpp
  DataFormat.FormatSize  = sizeof(KSDATAFORMAT);
  DataFormat.Flags       = 0;
  DataFormat.SampleSize  = 0;
 DataFormat.Reserved    = 0;
  DataFormat.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_MUSIC);
  DataFormat.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_DIRECTMUSIC);
  DataFormat.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_NONE);
```

 

 



