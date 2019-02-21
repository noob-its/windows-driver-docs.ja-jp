---
title: Iasphelp get\_ComputerName メソッド
description: ComputerName プロパティは、プリント サーバーの名前を取得する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_fd5c59b9-c223-4762-898d-693e9960619c.xml
- print.iasphelp\_computername
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 20fbd286-5b09-4c30-ae6c-4245854bc7b3
keywords:
- 印刷デバイスの get_ComputerName メソッド
- get_ComputerName メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_ComputerName メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_ComputerName
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8f62d992c2123c5e3cbcb6df40c559ceba78a20
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535662"
---
# <a name="iasphelpgetcomputername-method"></a>Iasphelp::get\_ComputerName メソッド

**ComputerName**プロパティは、プリント サーバーの名前を取得する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_ComputerName(
  [out] BSTR *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
コンピューター名の文字列へのポインターを受信する場所への呼び出し元が指定のポインター。

<a name="return-value"></a>戻り値
------------

このメソッドは、これらの値のいずれかを返すことができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>リターン コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>S_OK を返します</strong></td>
<td><p>操作に成功しました。</p></td>
</tr>
<tr class="even">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>メモリ不足です。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

```vb
Dim objPrinter, CompName
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
CompName = objPrinter.ComputerName
```

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>対象プラットフォーム</p></td>
<td>Desktop</td>
</tr>
</tbody>
</table>