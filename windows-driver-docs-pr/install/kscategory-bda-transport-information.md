---
title: KSCATEGORY_BDA_TRANSPORT_INFORMATION
description: KSCATEGORY_BDA_TRANSPORT_INFORMATION
ms.assetid: 0af3159c-8c44-4c42-8141-944bb734623c
keywords:
- KSCATEGORY_BDA_TRANSPORT_INFORMATION デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_BDA_TRANSPORT_INFORMATION
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 46edb7fd52062034beb21670285e2020ff5528a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535496"
---
# <a name="kscategorybdatransportinformation"></a>KSCATEGORY_BDA_TRANSPORT_INFORMATION


KSCATEGORY_BDA_TRANSPORT_INFORMATION[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) でトランスポートについてフィルター (TIF) の機能のカテゴリ、 [ドライバーのアーキテクチャをブロードキャスト](https://msdn.microsoft.com/library/windows/hardware/ff556573)(性 BDA)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>識別子</p></td>
<td align="left"><p>KSCATEGORY_BDA_TRANSPORT_INFORMATION</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{A2E3074F-6C3D-11d3-B653-00C04F79498E}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

BDA デバイス用のドライバーでは、オペレーティング システムに、デバイスが BDA トランスポートについてフィルターをサポートすることを示す KSCATEGORY_BDA_TRANSPORT_INFORMATION のインスタンスを登録します。

BDA トランスポート情報のフィルターの KS 機能のカテゴリの詳細については、次を参照してください。 [BDA フィルター カテゴリ Guid](https://msdn.microsoft.com/library/windows/hardware/ff556521)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows XP、DirectX 9.0 a がインストールされている、Windows 2000 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 




