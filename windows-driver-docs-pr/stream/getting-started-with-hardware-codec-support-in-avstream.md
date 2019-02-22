---
title: AVStream でハードウェアのコーデック サポートの概要
description: AVStream でハードウェアのコーデック サポートの概要
ms.assetid: f8335285-e74f-4600-aee9-7e2881cb0764
keywords:
- ハードウェアのコーデック サポート WDK AVStream を使用して
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e21751d64eac49db8337e789474709134f08782
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532136"
---
# <a name="getting-started-with-hardware-codec-support-in-avstream"></a>AVStream でハードウェアのコーデック サポートの概要


以降、Windows 7 で[Windows メディア ファンデーション](https://go.microsoft.com/fwlink/p/?linkid=155069)ユーザー モード Media Foundation 変換 (仕様) として AVStream ベースのメディア コンポーネントを表します。

この機能を使用すると、ベンダーがハードウェア ベースのデコーダー、エンコーダー、およびビデオのプロセッサをさらに、アプリケーション レベルで操作できる仕様として表示できます。

AVStream モデルでは、Windows 7 で変更されずにこの機能を有効にするミニドライバーをいくつかの追加のみが必要です。

トポロジのトランス コードは、次の図に示しています。

![図に示すトランスコーディング トポロジ](images/hw-transcoding.png)

最適なパフォーマンスを図の一番下の行に表示されているメディアの処理は、専用のハードウェアで発生する必要があります。 このシナリオでは、専用のトランス コードのハードウェアをセキュリティで保護されたハードウェア エンコーダー デコーダー (解明) としてと呼びます。 マザーボードのプラグイン モジュール、またはディスプレイ アダプターの統合機能として、解明をパッケージ化することができます。

Windows 7 には、ソフトウェア ベースのコード変換もサポートしています。 ただし、システムは、CPU ではなく、専用ハードウェア上のコード変換作業を実行するため、解明ベースのソリューションには、ソフトウェア ベースのソリューションと比較して大幅にユーザー エクスペリエンスが向上します。

前の図に示すようにユーザー モードのクライアントにユーザー モードの変換は、各 MFT で公開されている IMFTransform インターフェイスを使用してアクセスできます。 IMFTransform は使用可能 Vista および Windows での以降のバージョンがハードウェア ベースのメディア処理をユーザー モード アプリケーションを公開するメカニズムだけ以降 Windows 7 で使用できます。

システム提供のデバイスのプロキシ、または Devproxy、モジュールは、DirectShow ストリーミング モデルで KSProxy と同じ役割を担います。 Devproxy 間の通信を仲介する*Ks.sys*カーネル モードとユーザー モードで MFT コンポーネント。

関数の処理結果として得られる、ラップされたハードウェア メディアには、デバイスのプロキシ MFT は呼び出されます。 このメカニズムを利用するには、AVStream ミニドライバーは、次の操作を行う必要があります。

-   AVStream ミニドライバーの一部である個々 の KS フィルターとして変換関数を公開します。 たとえば場合は、デバイスのデコードが、エンコード、ビデオの処理機能、これらの関数として表す 3 つの異なる KS フィルターとします。
    -   **エンコーダー**: 非圧縮形式から圧縮された形式に変換するために使用します。
    -   **デコーダー**: 圧縮された形式から NV12 を含める必要があります、圧縮されていない形式に変換するために使用します。
    -   **ビデオ プロセッサ**: スケーリング、インター レース/de-インター レースを実行し、形式変換するために使用します。 デコーダーまたはエンコーダーのフィルターでビデオの処理のサポートを含めないでください。

        ベンダーがハードウェア ベースのスケーリングのサポートを提供することを強くお勧めします。 ただし、ハードウェア ベースのスケーリングのサポートを提供していない場合は、パフォーマンスの低下のレベルでスケール操作を実行するシステム提供のビデオ処理 MFT を使用することができます。 ハードウェア ベースのスケーリングのサポートを指定しない場合、メディア ファンデーション トポロジ ビルダーは自動的に、システム提供のスケーリング MFT をトポロジに挿入します。

-   Windows 7 および Windows の以降のバージョンで利用可能な次 KS カテゴリのいずれかで KS フィルターの処理、メディアを登録します。

    -   [**KSMFT\_カテゴリ\_ビデオ\_デコーダー**](https://msdn.microsoft.com/library/windows/hardware/ff548602)
    -   [**KSMFT\_カテゴリ\_ビデオ\_エンコーダー**](https://msdn.microsoft.com/library/windows/hardware/ff548611)
    -   [**KSMFT\_カテゴリ\_ビデオ\_プロセッサ**](https://msdn.microsoft.com/library/windows/hardware/ff548613)
    -   [**KSMFT\_CATEGORY\_AUDIO\_DECODER**](https://msdn.microsoft.com/library/windows/hardware/ff548572)
    -   [**KSMFT\_CATEGORY\_AUDIO\_ENCODER**](https://msdn.microsoft.com/library/windows/hardware/ff548584)

    さらに、次のカテゴリはトランス コードの他のシナリオで使用するためも定義されます。

    -   [**KSMFT\_カテゴリ\_ビデオ\_効果**](https://msdn.microsoft.com/library/windows/hardware/ff548607)
    -   [**KSMFT\_カテゴリ\_マルチプレクサー**](https://msdn.microsoft.com/library/windows/hardware/ff548596)
    -   [**KSMFT\_カテゴリ\_デマルチプレクサー**](https://msdn.microsoft.com/library/windows/hardware/ff548594)
    -   [**KSMFT\_CATEGORY\_AUDIO\_EFFECT**](https://msdn.microsoft.com/library/windows/hardware/ff548578)
    -   [**KSMFT\_カテゴリ\_OTHER**](https://msdn.microsoft.com/library/windows/hardware/ff548601)
-   Media foundation アプリケーションを使用できますし、 [MFTEnumEx](https://go.microsoft.com/fwlink/p/?linkid=155058)関数に記載されているカテゴリを使用して、仕様として登録されているデバイスを列挙します。

 

 



