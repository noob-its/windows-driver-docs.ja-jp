---
title: RemoveLockMnRemove ルール (wdm)
description: IRP の処理時に IoAcquireRemoveLock および IoReleaseRemoveLockAndWait への呼び出しが正しく使用 RemoveLockMnRemove ルールを確認します\_MJ\_MinorFunction IRP の PNP\_MN\_削除\_デバイス。
ms.assetid: 3BB367F0-AAF7-4A9E-B642-BA839DDCAA4E
ms.date: 05/21/2018
keywords:
- RemoveLockMnRemove ルール (wdm)
topic_type:
- apiref
api_name:
- RemoveLockMnRemove
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1692656e1383fa1a9746d68243d02dea405a985f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551035"
---
# <a name="removelockmnremove-rule-wdm"></a>RemoveLockMnRemove ルール (wdm)


**RemoveLockMnRemove**への呼び出し規則を確認します[ **IoAcquireRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548204)と[ **IoReleaseRemoveLockAndWait**](https://msdn.microsoft.com/library/windows/hardware/ff549567)が IRP の処理時に正しく使用\_MJ\_MinorFunction IRP の PNP\_MN\_削除\_デバイス。

このルールは、FDO および FIDO ドライバーのみに適用されます。

たとえば、フィルター ドライバーの FDO と PDO で構成される PnP ドライバー スタックがあるとします。

PnP マネージャーでは、クエリの削除がスタックを送信します。 アイドル状態のシステムの実行中に、FDO になっています。 FDO 決定電源ダウン削除クエリの状態で d0 IRP を要求します。 D0 IRP が到着すると、前に、PnP マネージャーは、PnP IRP を削除して、フィルター ドライバーが IRP が処理されたことを送信します。 フィルター ドライバーでは、スタックからデタッチされ、その状態をクリーンアップします。 スタックの上部にある、d0 が到着しますが、フィルター ドライバーは送信しません下位のスタックが存在しないコンテキストまたはデータがもはや送信先を判断します。 FDO は d0 IRP IRP がないことが到着するを待つハング状態にします。

**このエラーを回避する**

1.  デバイスは、デバイス スタックからデタッチされる前に[ **IoAcquireRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548204) IRP の次の種類のスタックを IRP が転送される前に、成功する必要があります。

    -   IRP\_MN\_クエリ\_削除
    -   IRP\_MN\_SUPRISE\_REMOVAL
    -   IRP\_MN\_削除\_デバイス

2.  [**IoReleaseRemoveLockAndWait** ](https://msdn.microsoft.com/library/windows/hardware/ff549567)呼び出す前に呼び出す必要がある[ **IoDetachDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549087)または[ **IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083). (これにより、デバイス ドライバーのすべての削除ロックが解放される)。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>RemoveLockMnRemove</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)
[**IoReleaseRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff549560)
[**IoReleaseRemoveLockAndWait**](https://msdn.microsoft.com/library/windows/hardware/ff549567) 
 [ **RemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff561032)
 

 




