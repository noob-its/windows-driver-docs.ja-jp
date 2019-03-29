---
title: KSPROPERTY\_ジャック\_シンク\_情報
description: KSPROPERTY\_ジャック\_シンク\_INFO プロパティは、フィルターのハンドルを使用してアクセスされる pin-wise プロパティとして実装されます。
ms.assetid: a51c03fa-91e4-49f2-ad76-35133c3b09ba
keywords:
- KSPROPERTY_JACK_SINK_INFO オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_JACK_SINK_INFO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fa80e12dec5c1ae1bcaec7da1928e0eecc90ce0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572919"
---
# <a name="kspropertyjacksinkinfo"></a>KSPROPERTY\_ジャック\_シンク\_情報


KSPROPERTY\_ジャック\_シンク\_INFO プロパティは、フィルターのハンドルを使用してアクセスされる pin-wise プロパティとして実装されます。

Windows 7 および以降のオペレーティング システムでは、このプロパティは 1 つまたは複数の物理ジャックに関連付けられているブリッジ暗証番号 (pin) をサポートできます。 KSPROPERTY\_ジャック\_シンク\_説明を取得する情報が使用され、ジャックの機能は、表示関連のデジタル オーディオ デバイス、HDMI デバイスまたはディスプレイ ポートなどのシンクします。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">取得</th>
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>(フィルターのハンドル) を使用してファクトリをピン留めします。</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537140" data-raw-source="[&lt;strong&gt;KSJACK_SINK_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537140)"><strong>KSJACK_SINK_INFORMATION</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (インスタンス データ) は、KSJACK\_シンク\_情報構造体。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_ジャック\_シンク\_INFO プロパティ要求情報が返されます、 **KSJACK\_シンク\_情報**構造体。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2008</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSJACK\_シンク\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff537140)

 

 





