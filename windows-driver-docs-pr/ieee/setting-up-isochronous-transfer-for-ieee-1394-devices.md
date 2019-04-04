---
title: IEEE 1394 デバイスの等時性転送の設定
description: IEEE 1394 デバイスの等時性転送の設定
ms.assetid: 5161da54-0f20-496c-bf64-dc756b987de2
keywords:
- アイソクロナス I/O WDK の IEEE 1394 バスを設定します。
- バスは、WDK の IEEE 1394 をサイクルします。
- WDK の IEEE 1394 のアイソクロナス チャネル バス
- リソースは、WDK の IEEE 1394 を処理します。
- WDK の IEEE 1394 をバッファー処理します。
- WDK の IEEE 1394 バス速度
- 帯域幅の割り当てください。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2785ccf8456c3d43a48237eed60a292efc0f90a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581410"
---
# <a name="setting-up-isochronous-transfer-for-ieee-1394-devices"></a>IEEE 1394 デバイスの等時性転送の設定


自分のデバイス ドライバーを開始する前に、次の手順に従う必要があります。

### <a href="" id="step-1---choose-the-transfer-speed-"></a>手順 1 です。 転送速度を選択します。

IEEE 1394 バスは、ハードウェアの使用によって制限されている、いくつかの異なる速度をサポートできます。 特定のデバイスでは、ある程度の速度をサポートする場合でも、のみ低速度をサポートする別のデバイスに接続する可能性があります。 ドライバーは、デバイスとコンピューター間の転送速度を実行時に決定する必要があります。 バス ドライバーにクエリを実行、 [**要求\_取得\_速度\_BETWEEN\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff537645)最大速度を判断する要求バスの 2 つのデバイスまたはデバイスとホスト コンピューター間。

### <a href="" id="step-2---allocate-bandwidth-"></a>手順 2 です。 帯域幅を割り当てます。

Isochronous データ転送はすべてを配置する前に、ドライバーは、バスの帯域幅を予約する必要があります。 バスは、固定量に達するまでに割り当てられた帯域幅の量を追跡します (送信できる最大帯域幅が 1 つの 80% を IEEEE 1394 1995 の仕様に従って*バスのサイクル*、これは、125 ナノ秒); そうはないです。現在割り当てられている帯域幅の一部が解放されるまでに、帯域幅を取得するには、他のデバイスを許可します。 ドライバーの送信、 [**要求\_アイソクロナス\_ALLOCATE\_帯域幅**](https://msdn.microsoft.com/library/windows/hardware/ff537647)帯域幅を予約するバス ドライバーに要求します。

要求が成功すると、バス ドライバーは、帯域幅ハンドルを返します。 ドライバーは、バス ドライバー帯域幅に関連するそれ以降の要求でこのハンドルを使用します。 たとえば、ドライバーを使用できます[**要求\_アイソクロナス\_設定\_チャネル\_帯域幅**](https://msdn.microsoft.com/library/windows/hardware/ff537658)帯域幅の量を調整するハンドル割り当てられます。 これを使用する必要があります、ドライバーが割り当てられた帯域幅が完了したら、 [**要求\_アイソクロナス\_FREE\_帯域幅**](https://msdn.microsoft.com/library/windows/hardware/ff537652)を使用できるように、帯域幅を解放するにはバス上の他のデバイスで

要求が失敗した場合、ドライバーにはすべてのデータ転送する必要がありますしません。 帯域幅の割り当てに失敗したドライバーは、該当する場合に帯域幅が後で割り当てを試行する状態自体にする必要がありますので、後続の試行で割り当てできる可能性があります。 システムはすべて以前に割り当てられた帯域幅とチャネルを自動的に解放すると、バスのリセット後にあるために、バスのリセットは、成功する可能性が後に、帯域幅を割り当てようとします。

帯域幅の割り当てに成功するドライバーはする必要があります先ほど説明した上の理由から、バスのリセット後、帯域幅とチャネル再割り当ています。 さらに、リセット後、帯域幅のハンドルが古くなるし、を呼び出して解放する必要があります[**要求\_アイソクロナス\_FREE\_帯域幅**](https://msdn.microsoft.com/library/windows/hardware/ff537652)帯域幅がない限り、IRB で割り当てられた\_フラグ\_許可\_リモート\_無料フラグを設定します。

### <a href="" id="step-3---allocate-a-channel-"></a>手順 3 です。 チャネルを割り当てます。

帯域幅の割り当て後に要求が成功すると、ドライバーの要求、*アイソクロナス チャネル*でデータを書き込みます。 複数のデバイスが 1 つのアイソクロナス チャネル上のパケットを読み取ることができますが、デバイスの 1 つだけがチャネルに書き込むことができます。 アイソクロナス パケットを受信するデバイスでは、受信確認パケットを代わりに送信しないでください。

ドライバーでは、チャネルを要求を送信して、 [**要求\_アイソクロナス\_ALLOCATE\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff537648)バス ドライバーに要求します。 ドライバーを特定のチャネルまたはアイソクロナス要求\_ANY\_無料のチャネルを割り当てることのチャネル。 成功した場合は、バス ドライバーは、割り当てられているチャネルを返します。 バス ドライバーでは、エラー コードを返します、ドライバーはすべてのデータ転送を試行する必要があり、手順 2. で割り当てられる帯域幅の割り当てを解除する必要があります。

ドライバーは、チャネルが現在使用できないため、決してされる使用可能なを想定しないでください。 チャネルは可能性がありますドライバーを適切な場合、チャネルが後で割り当てを試行する状態のままに自体に、いつでもでも無料なります。

### <a href="" id="step-4---allocate-a-resource-handle-"></a>手順 4 です。 リソース ハンドルを割り当てます。

ドライバーにチャネルがによって割り当てられると、そのチャネルのリソース ハンドルを割り当てます。 すべての後続ステップで、ドライバーは、リソース ハンドルを使用して、チャネルを指定します。

ドライバーは、送信することで、チャネルのリソース ハンドルを割り当てる、 [**要求\_アイソクロナス\_ALLOCATE\_リソース**](https://msdn.microsoft.com/library/windows/hardware/ff537649)バス ドライバーに要求します。

ドライバーは、リソース ハンドルを割り当てます、ときにも、ハンドルにアタッチされているバッファーの使用方法を示すフラグを指定します。

-   ドライバーが、チャネルを使用して、デバイスからデータを読み取るかどうか (、 [**要求\_アイソクロナス\_リッスン**](https://msdn.microsoft.com/library/windows/hardware/ff537655)操作)、リソースを設定\_使用\_IN\_リッスン中のフラグ。 ドライバーが、チャネルを使用して、デバイスにデータを書き込むかどうか (、 [**要求\_アイソクロナス\_説明**](https://msdn.microsoft.com/library/windows/hardware/ff537660)操作)、リソースを設定\_使用\_IN\_説明フラグ。

-   ドライバーでは、ハンドルを使用して、トランザクションのデータ バッファーを提供します。 (詳細については、この手順 5 を参照してください)。バス ドライバーではを実行し、デバイス ドライバーは、多くのバッファーがアタッチされるまでに、操作を一時停止するまでに、順序で、バッファーを使用します。 参照してください[アイソクロナス DMA 転送の IEEE 1394 デバイスのバッファリング](https://msdn.microsoft.com/library/windows/hardware/ff537014)詳細についてはします。

-   ドライバーは、アイソクロナス サイクル クロックの特定の値に、操作を同期することを指定できます。 参照してください[アイソクロナス同期オプションの IEEE 1394 デバイス](https://msdn.microsoft.com/library/windows/hardware/ff537379)詳細についてはします。

-   ドライバーは、アイソクロナス リッスンするためのオプションを設定できます。 ドライバーでは、データ パケットから isochronous パケット ヘッダーを削除するかどうかを指定できます。 ドライバーは、各バッファーは、データが格納される必要がありますまたはバッファー、あたり待機中のデータ バッファー 1 つパケットに到着したデータがコピーされるかどうかも指定できます。 参照してください[アイソクロナス IEEE 1394 デバイス用のオプションのリッスン](https://msdn.microsoft.com/library/windows/hardware/ff537377)詳細についてはします。

この要求が失敗した場合、ドライバーの前の手順で、割り当てられたすべてのアイソクロナス リソース割り当てを解除する必要があります。

### <a href="" id="step-5---attach-buffers-to-the-resource-handle-"></a>手順 5 です。 バッファーをリソース ハンドルにアタッチします。

ドライバーは、リソース ハンドルを割り当てます後、は、ハンドルにバッファーをアタッチします。 ホスト DMA コント ローラーはからデータを読み取るか、接続されているバッファーにデータを書き込みます。

各バッファーで、ドライバーに渡します、 [**アイソクロナス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537401)構造体のバッファーの使用方法を説明します。 バッファーのアイソクロナスで\_記述子構造体、ドライバーは、次の情報を指定できます。

-   フレームごとのバイト数の最大数。 データを送信するときに、ホスト コント ローラーは、このサイズのパケットにデータ バッファーを分割します。

-   省略可能なコールバック ルーチンの場合。 処理が完了したら、バス ドライバーがこのルーチンを呼び出す

-   同期オプション。 参照してください[アイソクロナス同期オプションの IEEE 1394 デバイス](https://msdn.microsoft.com/library/windows/hardware/ff537379)の同期オプションの説明。

-   アイソクロナス トークの操作に、ドライバーは、次のいくつかのデータ パケットを先頭に追加するヘッダーの一覧としてこのバッファーを指定できます。 参照してください[アイソクロナス IEEE 1394 デバイス用のオプションの説明](https://msdn.microsoft.com/library/windows/hardware/ff537380)詳細についてはします。

操作が開始されると、ドライバーが不要なバッファーをデタッチすることができ、追加のバッファーを関連付けることができます。 識別されるコールバック ルーチンを使用できます[**アイソクロナス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537401)自体をバス ドライバーに接続されている最後のバッファー処理が完了したときに通知します。 参照してください[アイソクロナス DMA 転送の IEEE 1394 デバイスのバッファリング](https://msdn.microsoft.com/library/windows/hardware/ff537014)DMA が IEEE 1394 のデバイスでのバッファー処理の説明についてはします。

### <a href="" id="step-6---begin-the-data-transfer"></a>手順 6 です。 データ転送を開始します。

ドライバーの問題、デバイスからの読み取り、 [**要求\_アイソクロナス\_リッスン**](https://msdn.microsoft.com/library/windows/hardware/ff537655)要求。 デバイス ドライバーの問題に書き込む、 [**要求\_アイソクロナス\_説明**](https://msdn.microsoft.com/library/windows/hardware/ff537660)要求。 ドライバーの読み取りまたは書き込みを適切なデバイスに固有の方法でデバイスをアクティブ化できます。

 

 



