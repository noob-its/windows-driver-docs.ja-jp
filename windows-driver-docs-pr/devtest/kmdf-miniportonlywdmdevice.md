---
title: MiniportOnlyWdmDevice ルール (kmdf)
description: MiniportOnlyWdmDevice ルールでは、WDF のドライバーがベア WDM デバイス オブジェクトを作成する IoCreateDevice および IoCreateDeviceSecure 関数を使用する必要があることを指定します。
ms.assetid: 23B9431E-3932-42F3-B797-0820D9A43295
ms.date: 05/21/2018
keywords:
- MiniportOnlyWdmDevice ルール (kmdf)
topic_type:
- apiref
api_name:
- MiniportOnlyWdmDevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 781caecf55b598226c46e4817ec2aba5b5a6105d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579570"
---
# <a name="miniportonlywdmdevice-rule-kmdf"></a>MiniportOnlyWdmDevice ルール (kmdf)


**MiniportOnlyWdmDevice**ルールでは、WDF のドライバーを使用する必要がありますいないことを指定します[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)と[ **IoCreateDeviceSecure** ](https://msdn.microsoft.com/library/windows/hardware/ff548407)ベア WDM デバイス オブジェクトを作成する関数。 これにより、クラッシュを IRP を WDM デバイスに送信するコンピューター。 デバイスの IRP ディスパッチ エントリは、WDF に固有のエントリに設定されますが、フレームワークは、WDF デバイスを作成していないためにです。 ただし、それらのドライバーのディスパッチのエントリ ポイントが設定されていないため、ミニポート ドライバーでは、Ddi を使用できます。

|              |      |
|--------------|------|
| ドライバー モデル | KMDF |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>MiniportOnlyWdmDevice</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>対象
----------

[**WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)
[**IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397)
[**IoCreateDeviceSecure**](https://msdn.microsoft.com/library/windows/hardware/ff548407)
 

 




