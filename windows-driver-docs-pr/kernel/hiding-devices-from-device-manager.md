---
title: デバイス マネージャーからデバイスを非表示
description: デバイス マネージャーからデバイスを非表示
ms.assetid: dd362ae1-ab14-44ee-982e-f972454c2623
keywords:
- デバイス マネージャーの WDK、非表示のデバイス
- デバイスからデバイス マネージャーを非表示の WDK
- WDK の非表示のデバイス
- WDK のデバイスを非表示
- NoDisplayClass 値 WDK デバイスのインストール
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd9a2483d39287f6dd2f0dc6a8ab0737e84b02d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553704"
---
# <a name="hiding-devices-from-device-manager"></a>デバイス マネージャーからデバイスを非表示


既定では、デバイス マネージャーは、コンピューター上のすべてのデバイスの状態を示します。 状況によっては、特定のデバイスでデバイス マネージャーに表示されないようにする場合があります。 たとえば、マザーボードには、CardBus コント ローラーではないユーザーがアクセスできるスロットがあります。 ユーザーが、スロットを使用できないため、デバイスに関する情報を表示するデバイス マネージャーをしないようにします。

デバイス マネージャーでデバイスを非表示にするには、としてデバイスをマークすることができます、*非表示デバイス*します。 通常、デバイス マネージャーでは、非表示のデバイスは表示されません。 (ただし、ユーザーがこの設定を上書きしても、デバイス マネージャー内のすべてのデバイスを表示できますでものを表示します。 この設定を上書きする方法の詳細については、次を参照してください[非表示のデバイスを表示する](https://msdn.microsoft.com/library/windows/hardware/ff553955)。)。

デバイスの非表示としてマークする 2 つの方法があります。 デバイスのドライバーや、ACPI BIOS を使用しています。

### <a name="hiding-devices-from-within-a-driver"></a>ドライバー内からデバイスを非表示

ドライバーをドライバーを非表示としてマークする 2 つの方法があります。

-   関数のドライバーまたはフィルター ドライバーの関数が応答することで正常に開始されたデバイスを非表示にするオペレーティング システムを問い合わせることができる、 [ **IRP\_MN\_クエリ\_PNP\_デバイス\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff551698) IRP します。 ドライバー、PNP を設定する必要があります、IRP が到着すると、\_デバイス\_不要\_表示\_UI ビット**IoStatus.Information**に**TRUE**ドライバーのルーチンをディスパッチします。

-   Windows XP および Windows オペレーティング システムの以降のバージョンでは、バス ドライバーまたはバス フィルター ドライバーを非表示に任意のデバイスでは、開始、またはそれ以外の場合、応答することで、 [ **IRP\_MN\_クエリ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff551664) IRP します。 IRP が到着すると、ドライバーを設定する必要があります、 **Parameters.DeviceCapabilities.NoDisplayInUI**メンバー **TRUE**ドライバーのディスパッチ ルーチンでします。 場合によっては、bus フィルター ドライバーが完了ルーチンで、このビットを設定する必要があります。 基になるバス ドライバーのディスパッチ ルーチンが他のドライバーの設定機能のすべてのフィールドを正しく消去時に、この余分な手順が必要です。

### <a name="hiding-devices-by-using-the-acpi-bios"></a>ACPI BIOS を使用してデバイスを非表示

ACPI BIOS で非表示としてデバイスをマークすることができます。 BIOS を公開できます、\_デバイスの STA メソッド。 \_STA メソッドは、ビットマスクを返します。 ビット 2 (マスク 0x4) では、かどうかデバイス マネージャーは、デバイス表示されるように既定でを指定します。 デバイスに表示され、0 それ以外の場合場合、このビットは 1 にする必要があります。

たとえば、次のコード例は、ルート バス上の USB コント ローラーは非表示にする方法を示します。

```cpp
Device(PCI0) // Root PCI bus
_HID *PNP0A03 
...
    Device(UCTL)  // USB controller
    _ADR 0xddddffff // dddd = device, ffff = function
    _STA 0xB // Device present, but not shown
```

Microsoft Windows 2000 でのみ開始、デバイスの操作を非表示にできます。 Windows XP と Windows の以降のバージョンもに切断されたデバイスを非表示にすることができます。 によって返されるビット 3 (マスク 0x8)、 \_STA メソッドでは、デバイスが正常に動作しているかどうかを示します。 デバイスが正常に動作し、0 をそれ以外の場合は場合、このビットは 1 です。 たとえば、次のコード例では、BIOS が USB コント ローラーが切断され、非表示にする必要がありますをどのように指定する方法を示しています。

```cpp
Device(PCI0) // Root PCI bus 
_HID *PNP0A03 
...
    Device(UCTL) // USB controller
    _ADR 0xddddffff //  dddd = device, ffff = function
    _STA 0x3 // Present, but broken and not shown 
```

**注**   「デコード」ビット (0x2) で説明されているデバイスの関連性を持たない\_ADR メソッド。 前のコード例は、デコード ビットが設定されていないでも動作します。 BIOS ライターで説明されているデバイスに対してのみデコードの状態を追跡する必要があります\_HID メソッド。

 

 

 



