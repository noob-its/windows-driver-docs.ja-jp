---
title: バグ チェック 0xCE DRIVER_UNLOADED_WITHOUT_CANCELLING_PENDING_OPERATIONS
description: DRIVER_UNLOADED_WITHOUT_CANCELLING_PENDING_OPERATIONS のバグ チェックでは、0x000000CE の値を持ちます。 これは、ドライバーをアンロードする前に保留中の操作をキャンセルするが失敗したことを示します。
ms.assetid: ade0d20d-25f0-45ad-a099-31f3521b91cd
keywords:
- バグ チェック 0xCE DRIVER_UNLOADED_WITHOUT_CANCELLING_PENDING_OPERATIONS
- DRIVER_UNLOADED_WITHOUT_CANCELLING_PENDING_OPERATIONS
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_UNLOADED_WITHOUT_CANCELLING_PENDING_OPERATIONS
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 740ceeb0b1a6a677d5ec7f80b82b75ff7ea260ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536871"
---
# <a name="bug-check-0xce-driverunloadedwithoutcancellingpendingoperations"></a>バグ チェック 0xCE の。ドライバー\_UNLOADED\_せず\_CANCELLING\_PENDING\_操作


ドライバー\_UNLOADED\_せず\_CANCELLING\_PENDING\_操作のバグ チェックが 0x000000CE の値を持ちます。 これは、ドライバーをアンロードする前に保留中の操作をキャンセルするが失敗したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="driverunloadedwithoutcancellingpendingoperations-parameters"></a>ドライバー\_UNLOADED\_せず\_CANCELLING\_PENDING\_操作パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>参照されているメモリ アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>書き込み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>メモリ (わかる場合) を参照されているアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

その名前がブルー スクリーンに印刷され、場所のメモリに格納されているドライバーのエラーの原因が識別できる場合 (PUNICODE\_文字列) **KiBugCheckDriver**します。

<a name="cause"></a>原因
-----

このドライバーは、ルック アサイド リスト、Dpc、ワーカー スレッド、またはアンロードする前にこのようなその他の項目をキャンセルできませんでした。

 

 



