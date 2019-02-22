---
Description: A USB function driver supports runtime idle detection by implementing USB selective suspend.
title: USB drivers (WDF) でのセレクティブ サスペンドします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be1759f7aee84db8120eb104e491fd3e3fbcd1d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532732"
---
# <a name="selective-suspend-in-usb-drivers-wdf"></a>USB drivers (WDF) でのセレクティブ サスペンドします。


USB 関数ドライバー サポート ランタイム アイドル検出 USB のセレクティブを実装することによって中断します。 ここでは、Windows® Driver Foundation (WDF) に基づいている USB ドライバーの選択的に実装する方法についてドライバー開発者向けの中断のコンテンツします。

## <a name="about-selective-suspend"></a>選択的について次のように中断します。


セレクティブ サスペンドの電源を切るとがアタッチされているコンピューターの動作状態 (S0) のまま、アイドル状態の USB デバイスを後で再開する機能です。 エネルギー効率の高い操作: モバイル Pc で特に-すべての USB デバイスとドライバーを選択的にサポートする必要がありますを中断します。 S0 状態のままのシステムがアイドル状態のとき、デバイスの電源と、次の重要な利点があります。

-   セレクティブ サスペンド、電源を保存します。
-   セレクティブ サスペンド熱の読み込みやノイズなどの環境要因を軽減できます。

アイドル状態になっているデバイスのハードウェアの電源、ドライバーはこの機能をサポートする必要があります。 セレクティブ サスペンドのサポート、USB Windows® Driver Foundation (WDF) に基づいているドライバーで最も基本的なプラグ アンド プレイのサポートに必要なもの以外、いくつかの余分なコールバックが必要です。

USB デバイスのすべての関数ドライバーでは、システムの実行中にアイドル状態のデバイスを中断する積極的な電源管理を実装する必要があります。 このトピックでは、選択的に実装する方法を説明します。 WDF ベースのドライバーで中断します。 WDF に慣れていない場合は、Windows Driver Kit (WDK) と、Windows Driver Foundation でのドライバーの開発を参照してください。

USB デバイス サポート ランタイム アイドル状態の検出を選択的に USB で中断します。 セレクティブ サスペンドにより、同じハブに接続されているその他のデバイスに影響を与えずに、一時停止状態に挿入するアイドル状態のデバイスまたは — 多機能デバイスの場合-デバイスで他の関数には影響しません。 すべてのデバイスと機能が中断されたときに、hub 全体または多機能デバイス電源を切断できます。

選択的なハードウェアの観点から中断は USB ポート経由での物理的な状態です。 ポートに関連付けられているすべての関数がアイドル状態で、ポートを選択的に入力できる場合に中断します。

USB 仕様に準拠しているは、すべての USB デバイスを選択的にサポートする必要がありますを中断します。 USB バスがアイドル状態のとき、デバイスが電源を切断できる場合があります。 選択的な Microsoft 提供の USB ハブのドライバー実装は、ハードウェア レベルで中断します。

USB には、バス ドライバーと通信し、管理デバイス I/O 制御要求を中断して、デバイスの機能を再開するには、WDF を通じてその個々 のデバイス機能の選択的実装を中断するドライバーが機能します。 WDF 両方のカーネルのモードを有効にし、選択的にサポートするためにユーザー モード ドライバーが中断します。

選択的関数ドライバーの USB の詳細については、コードを中断、ドライバーがユーザー モードまたはカーネル モードで実行するかどうかによって異なります。 次のガイドラインを考慮してください。

-   ユーザー モード ドライバー フレームワーク (UMDF) を使用すると、可能であれば、USB ドライバーを実装します。 ユーザー モード ドライバーでは、システムのデータが破損する可能性が低いと、カーネル モード ドライバーよりもデバッグが簡単です。
-   ドライバーがアイソクロナス エンドポイントを使用してデータをストリームまたはその他の機能またはカーネル モードでのみ使用可能なリソースが必要だ場合にのみ、カーネル モード ドライバー フレームワーク (KMDF) を使用します。

## <a name="power-policy-ownership-io-queues-and-selective-suspend"></a>電源ポリシーの所有権、I/O キュー、および選択的中断


デバイス スタックの電源ポリシー所有者 (PPO) は、どの電源状態が、デバイスは、特定の時点である必要がありますを決定するドライバーです。 各デバイス スタックの 1 つだけのドライバーは、PPO を指定できます。 関数のドライバーには、そのデバイスに対して PPO 通常です。

USB ドライバー サポート オプションを選択では、中断し、そのデバイス スタックで PPO 上に重ねられる、ドライバーは電源管理対象のキューを使用する必要があります。 これは、両方の UMDF および KMDF ドライバーの場合は true。 要求が電源管理対象のキューに到着するは、デバイスが中断されている間、デバイス全体のスタックが停止することができます。

図 1 は、その I/O キューを USB ドライバーへの I/O 要求のフローを示しています。

![wdf の usb ドライバーへの要求のフロー](images/flowrequestswdfusbdriver.png)

図では、USB ドライバーの要求が到着します。 フレームワークでは、適切なキューに要求を追加します。

キューが電源管理の対象でない場合、フレームワークは (シーケンシャル、パラレル、または手動) キューのドライバーが構成されているディスパッチ種類に応じてドライバーに要求を表示します。 ドライバーは、要求を処理します。

キューが電源管理の対象デバイスが中断されていない場合は、フレームワークは、構成済みのディスパッチの種類に応じてドライバーに要求を表示します。

ただし、デバイスが中断されている場合、フレームワークのアクションは、かどうか、ドライバーは、デバイス スタックの PPO に依存します。 ドライバーが、PPO の場合は、フレームワークは、デバイスの電源を USB 親ドライバーと通信します。 デバイスが再開されると、フレームワークは、ドライバーに要求を表示します。

ドライバーでない場合、PPO フレームワークをとりませんそれ以上の操作 PPO のみデバイスを再開することができますので。 要求はキューに残ります。 デバイス スタックは失速、PPO がデバイスを再開することをすべての要求を受信しない場合です。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="selective-suspend-in-umdf-drivers.md" data-raw-source="[Selective suspend in UMDF drivers](selective-suspend-in-umdf-drivers.md)">UMDF ドライバーでのセレクティブ サスペンドします。</a></p></td>
<td><p>このトピックでは、UMDF 関数のドライバー サポート USB のセレクティブを中断する方法について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="selective-suspend-in-a-kmdf-function-driver.md" data-raw-source="[Selective suspend in USB KMDF function drivers](selective-suspend-in-a-kmdf-function-driver.md)">KMDF の USB 機能ドライバーでのセレクティブ サスペンドします。</a></p></td>
<td><p>このトピックでは、KMDF 関数ドライバー サポート USB のセレクティブを中断する方法について説明します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[Windows Driver Frameworks (WDF)](https://go.microsoft.com/fwlink/p/?linkid=53698)  
[プラグ アンド プレイ - アーキテクチャとドライバー サポート](https://go.microsoft.com/fwlink/p/?linkid=320985)  
[KMDF ドライバーでの PnP と電源管理](https://go.microsoft.com/fwlink/p/?linkid=320986)  
[WDF のドライバーが電源管理対象の I/O キューを使用する場合](https://go.microsoft.com/fwlink/p/?linkid=320987)  
[WDF の USB ドライバーの記述](https://go.microsoft.com/fwlink/p/?linkid=320988)  
[USB クライアント ドライバーでの電源管理の実装](https://go.microsoft.com/fwlink/p/?linkid=320989)  


