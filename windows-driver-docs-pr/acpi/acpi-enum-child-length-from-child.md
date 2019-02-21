---
title: ACPI_ENUM_CHILD_LENGTH_FROM_CHILD マクロ
description: ACPI_ENUM_CHILD_LENGTH_FROM_CHILD マクロは、可変長 ACPI_ENUM_CHILD 構造体のバイト単位のサイズを計算します。
ms.assetid: 62be7cb5-4b71-4b8e-bad5-807623cd812a
keywords:
- ACPI_ENUM_CHILD_LENGTH_FROM_CHILD マクロ ACPI デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb682142fe13b46dc324d52379360ac4422c29e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538100"
---
# <a name="acpienumchildlengthfromchild-macro"></a>ACPI\_ENUM\_子\_長さ\_FROM\_子マクロ


ACPI\_ENUM\_子\_長さ\_FROM\_子マクロには、可変長のバイト単位で、サイズが計算されます[ **ACPI\_ENUM\_。子**](https://msdn.microsoft.com/library/windows/hardware/ff536109)構造体。

<a name="syntax"></a>構文
------

```cpp
void ACPI_ENUM_CHILD_LENGTH_FROM_CHILD(
    Child
);
```

<a name="parameters"></a>パラメーター
----------

*子*   
ACPI の種類の構造体へのポインター\_ENUM\_構造体のバイト単位のサイズを計算する対象の子。

<a name="return-value"></a>戻り値
------------

ACPI のバイト単位のサイズを\_ENUM\_子構造体*子*を指します。

<a name="remarks"></a>注釈
-------

ドライバーは、このマクロを使用して ACPI のバイト単位のサイズを計算する\_ENUM\_内の子構造体、 [ **ACPI\_ENUM\_子\_出力\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff536112)構造体。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr>
<td><p>対象プラットフォーム</p></td>
<td>Desktop</td>
</tr>
<tr>
<td><p>Header</p></td>
<td>Acpiioct.h (Acpiioct.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ACPI\_ENUM\_子**](https://msdn.microsoft.com/library/windows/hardware/ff536109)

[**ACPI\_ENUM\_子\_出力\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff536112)

 

 



