---
title: Storport のポート設定の構成情報
description: Storport のポート設定の構成情報
ms.assetid: dcc2cb3c-2fe6-4f70-814b-66b59a237dd9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3451b741796457e6ef103e4d5eaf205bef73a10a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537532"
---
# <a name="setting-port-configuration-information-with-storport"></a>Storport のポート設定の構成情報


## <span id="ddk_setting_port_configuration_information_with_storport_kg"></span><span id="DDK_SETTING_PORT_CONFIGURATION_INFORMATION_WITH_STORPORT_KG"></span>


Microsoft Windows PnP マネージャーでは、Storport によって管理アダプターを検出、Storport ドライバーを開始することを通知します。 次に、ミニポート ドライバーの呼び出す Storport [ **HwStorFindAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff557390)ルーチンに渡すこと、 [**ポート\_構成\_情報 (STORPORT)** ](https://msdn.microsoft.com/library/windows/hardware/ff563901)構造体。

Storport によって管理されるすべてのアダプターは、の PnP デバイスであるため*HwStorFindAdapter*アダプターの物理的には検索しません。 このミニポート ドライバー ルーチンが、ポートで指定されたパラメーターを使用して、アダプターの初期化を試みる代わりに、\_構成\_情報構造体とポートの初期化が完了した\_構成\_については、ポートにそれらの値を格納する\_構成\_情報 Storport がデバイスの拡張機能を初期化するために必要があります。

詳細については、次を参照してください[**ポート\_構成\_情報 (SCSI)** ](https://msdn.microsoft.com/library/windows/hardware/ff563900)と[**ポート\_構成\_。情報 (STORPORT)**](https://msdn.microsoft.com/library/windows/hardware/ff563901)します。

 

 



