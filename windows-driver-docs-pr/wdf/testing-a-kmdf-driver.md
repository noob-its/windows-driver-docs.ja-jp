---
title: WDF ドライバー (KMDF または UMDF) のテスト
description: このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) またはユーザー モード ドライバー フレームワーク (UMDF) バージョン 2 のドライバーをテストするための推奨事項について説明します。
ms.assetid: 05545488-0114-49f5-bf8a-006a868911e8
keywords:
- カーネル モード ドライバー WDK KMDF のテスト
- KMDF WDK、ドライバーのテスト
- カーネル モード ドライバー フレームワーク WDK は、ドライバーのテスト
- フレームワーク ベースのドライバー WDK KMDF のテスト
- ドライバー WDK、framework ベースのドライバーのテスト
- VerifierOn レジストリ値 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92d84578cfe5b43c04ea1cbc809a53c9abf83eb7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372314"
---
# <a name="testing-a-wdf-driver-kmdf-or-umdf"></a>WDF ドライバー (KMDF または UMDF) のテスト


このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) またはユーザー モード ドライバー フレームワーク (UMDF) バージョン 2 のドライバーをテストするための推奨事項について説明します。

ドライバーをテストするときに次の操作を行う必要があります。

-   設定、 **VerifierOn**フレームワークのドライバーの検証機能を有効にするレジストリ値。 詳細については**VerifierOn** 、ドライバーのテスト、デバッグする際に使用できるその他のレジストリ値を参照してくださいと[KMDF Verifier を使用して](using-kmdf-verifier.md)と[UMDFVerifierを使用します](using-umdf-verifier.md)。 フレームワークのドライバーの検証機能を使用するのに役立つアプリケーションについては、次を参照してください。 [WDF Verifier コントロール アプリケーション](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)します。

-   UMDF バージョン 1 と 2 両方を有効にする[Application Verifier (AppVerif.exe)](https://www.microsoft.com/download/details.aspx?id=20028) Wudfhost.exe にします。 例:
    ```cpp
    appverif -enable handles locks heaps memory exceptions TLS -for WudfHost.exe
    ```

    フレームワークの組み込みの検証を行うために自動的にオンにします。
-   このドキュメントで説明されているドライバー検証ツールを使用します。 これらの重要なツールの詳細についてを参照してください。
    -   [WdfTester:WDF ドライバー テスト ツールセット](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdftester--wdf-driver-testing-toolset)
    -   [ドライバーの検証用ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-verifying-drivers)
    -   [ドライバーのテスト用ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-testing-drivers)

ドライバーを徹底的にテストするには、フレームワークのドライバーの検証機能とドライバーの検証ツールの両方を使用する必要があります。

Microsoft Visual Studio と Windows Driver Kit (WDK) を使用してドライバーのテストについては、次を参照してください。[ドライバーのテスト](https://docs.microsoft.com/windows-hardware/drivers/develop/testing-a-driver)と[WDF ドライバーのテスト](https://docs.microsoft.com/windows-hardware/drivers/wdf/testing-a-kmdf-driver)します。

 

 





