---
title: 非 PnP ドライバーをインストールします。
description: 非 PnP ドライバーをインストールします。
ms.assetid: 99676d85-feb2-482c-a91b-cfc48be5904c
keywords:
- カーネル モード ドライバー フレームワーク WDK は、ドライバーをインストールします。
- フレームワーク ベースのドライバー WDK KMDF をインストールします。
- INF ファイル WDK KMDF、非 PnP ドライバー
- 非 PnP ドライバー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 103fd39ae6400c661a3277acbd9da5ab0466965c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560315"
---
# <a name="installing-a-non-pnp-driver"></a>非 PnP ドライバーをインストールします。


ドライバーがプラグ アンド プレイ (PnP) デバイスをサポートしていない場合、ドライバー パッケージは、INF を含む INF ファイルを含める必要があります<em>DDInstall</em>**します。CoInstallers**セクションと INF <em>DDInstall</em>**します。WDF**セクションで説明されている[KMDF 共同インストーラーを使用して](installing-the-framework-s-co-installer.md)します。

さらに、インストーラーを読み込むには、ドライバー、フレームワークの共同インストーラーを提供する必要があります。 共同インストーラーでは、 [ **WdfPreDeviceInstall**](https://msdn.microsoft.com/library/windows/hardware/ff548835)、 [ **WdfPreDeviceInstallEx**](https://msdn.microsoft.com/library/windows/hardware/ff548839)、 [ **WdfPostDeviceInstall**](https://msdn.microsoft.com/library/windows/hardware/ff548829)、 [ **WdfPreDeviceRemove**](https://msdn.microsoft.com/library/windows/hardware/ff548840)、および[ **WdfPostDeviceRemove** ](https://msdn.microsoft.com/library/windows/hardware/ff548833)関数をドライバーのインストーラーを呼び出す必要があります。

非 PnP ドライバーのインストーラーを作成する方法の例は、インストーラーに含まれているを参照してください、[非 PNP](sample-kmdf-drivers.md)サンプル。

 

 




