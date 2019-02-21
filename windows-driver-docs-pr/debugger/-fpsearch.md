---
title: fpsearch
description: Fpsearch 拡張機能は、指定されたアドレスの解放された特別なプールを検索します。
ms.assetid: 70375723-7156-47ec-b6e1-b3c51b5caaf9
keywords:
- 特別なプール
- Windows デバッグ fpsearch
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- fpsearch
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7a8e116eef4a8758a7824482a4ef37ba4ec5deb7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549233"
---
#  <a name="fpsearch"></a>! fpsearch


**! Fpsearch**拡張機能は、指定したアドレスの解放された特別なプールを検索します。

```dbgcmd
!fpsearch [Address] [Flag]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
仮想アドレスを指定します。

<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span> *フラグ*   
場合設定、デバッガーでは、解放された特別なプールを検索すると、フリー リストに各ページの生コンテンツが表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

アドレスの表示には、割り当て解除の時点での仮想アドレス、ページのフレーム数 (PFN)、プール タグ、サイズ、アドレスにデータがページング可能かどうか、スレッド ID、および呼び出し履歴が含まれます。

場合*アドレス*設定は、デバッガーが解放された特別なプール全体を表示するのには、-1。

デバッガーが解放された特別なプールに指定されたアドレスを見つけられない場合は、何も表示されません。この拡張機能からの出力の例を次に示します。

```dbgcmd
kd> !fpsearch -1 1
Searching the free page list (8 entries) for all freed special pool

1EC4000  04000200 e56b6f54 000001f4 0000059c ....Tok.........
1EC4000  00000800 00000000 00000000 00000000 ................
1EC4000  bad0b0b0 82100000 00000000 00000000 ................
1EC4000  72657355 20203233 0000bac5 00000000 User32  ........
1EC4000  00028b94 00000000 0000bac9 00000000 ................
1EC4000  00000000 00000000 ffffffff 7fffffff ................
1EC4000  8153b1b8 00028aff 00000000 00000000 ..S.............
1EC4000  0000001b 00000000 00000012 00000514 ................

26A2000  000a0008 00adecb0 000e000c 00adecba ................
26A2000  000a0008 00adecc8 000e000c 00adecd2 ................
26A2000  000e000c 00adece0 000e000c 00adecee ................
26A2000  00120010 00adecfc 000e000c 00aded0e ................
26A2000  000e000c 00aded1c 000e000c 00aded2a ............*...
26A2000  000e000c 00aded38 000e000c 00aded46 ....8.......F...
26A2000  000a0008 00aded54 000e000c 00aded5e ....T.......^...
26A2000  00120010 00aded6c 000e000c 00aded7e ....l.......~...

2161000  000a0008 00adeccc 000e000c 00adecd6 ................
2161000  000a0008 00adece4 000e000c 00adecee ................
2161000  000e000c 00adecfc 000e000c 00aded0a ................
2161000  00120010 00aded18 000e000c 00aded2a ............*...
2161000  000e000c 00aded38 000e000c 00aded46 ....8.......F...
2161000  000e000c 00aded54 000e000c 00aded62 ....T.......b...
2161000  000a0008 00aded70 000e000c 00aded7a ....p.......z...
2161000  00120010 00aded88 000e000c 00aded9a ................

...

CEC8000  0311ffa4 03120000 0311c000 00000000 ................
CEC8000  00001e00 00000000 7ff88000 00000000 ................
CEC8000  00000328 00000704 00000000 00000000 (...............
CEC8000  7ffdf000 00000000 00000000 00000000 ................
CEC8000  e18ba8c0 00000000 00000000 00000000 ................
CEC8000  00000000 00000000 00000000 00000000 ................
CEC8000  00000000 00000000 00000000 00000000 ................
CEC8000  00000000 00000000 00000000 00000000 ................

CEAD000  00000000 00000000 00000000 00000000 ................
CEAD000  00000000 00000000 00000000 00000000 ................
CEAD000  00000000 00000000 00000000 00000000 ................
CEAD000  00000000 00000000 00000000 00000000 ................
CEAD000  00000000 00000000 00000000 00000000 ................
CEAD000  00000000 00000000 00000000 00000000 ................
CEAD000  00000000 00000000 00000000 00000000 ................
CEAD000  00000000 00000000 00000000 00000000 ................
```

任意の時点での実行を停止するには、CTRL + BREAK (WinDbg) で、または (KD) では、CTRL + C キーを押します。

 

 




