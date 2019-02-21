---
title: KSPROPERTY\_VIDEODECODER\_標準
description: KSPROPERTY\_VIDEODECODER\_標準プロパティは、現在のアナログ ビデオ標準を制御します。 このプロパティを実装する必要があります。
ms.assetid: 955c267a-703e-4d18-a4e9-710f316cfb48
keywords:
- KSPROPERTY_VIDEODECODER_STANDARD ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEODECODER_STANDARD
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a42192f1712071e370215612e78e27eea3c1718
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531743"
---
# <a name="kspropertyvideodecoderstandard"></a>KSPROPERTY\_VIDEODECODER\_標準


KSPROPERTY\_VIDEODECODER\_標準プロパティは、現在のアナログ ビデオ標準を制御します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_videodecoder_standard_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_STANDARD_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566052" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566052)"><strong>KSPROPERTY_VIDEODECODER_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、現在のアナログ ビデオ標準を指定する ULONG です。

<a name="remarks"></a>注釈
-------

**値**、KSPROPERTY のメンバー\_VIDEODECODER\_S 構造体が現在のアナログ ビデオ標準を指定します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEODECODER\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566052)

 

 





