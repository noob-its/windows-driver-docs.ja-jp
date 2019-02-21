---
title: ハードウェア Id を指定するためのベスト プラクティス
description: ハードウェア Id を指定するためのベスト プラクティス
ms.assetid: 95dcf1b1-b2cd-473f-9660-a91fda20ffc2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e4d0487a3f14a456896014a30802902dbddf939
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538576"
---
# <a name="best-practices-for-specifying-hardware-ids"></a>ハードウェア Id を指定するためのベスト プラクティス


[ **HardwareIDList** ](https://msdn.microsoft.com/library/windows/hardware/ff546121)要素は、デバイスの 1 つまたは複数のハードウェアの識別文字列を指定します。 各文字列がで指定された、 [ **HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114) XML 要素。 オペレーティング システムが最初の識別文字列については、デバイスを照会し、しを持つデバイス メタデータ パッケージを読み込み、 **HardwareID**この文字列と一致する値。

各**HardwareID**要素の値である必要があります、[ハードウェア ID](hardware-ids.md)デバイスに固有です。 使用しないで、[互換性 ID](compatible-ids.md) USB クラス ID、'HID_DEVICE' または 'HID_DEVICE_SYSTEM_KEYBOARD' など、デバイスの場合。

各必ず[ **HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114)メタデータ パッケージで指定されている要素が正確に関連する値を持つ、[ハードウェア ID](hardware-ids.md)を物理デバイスのレポート。 たとえば、ID が物理デバイス、デバイス メタデータのファミリ間で再利用のハードウェアをパッケージ化する場合ことを指定します**HardwareID**要素の値がデバイスのファミリ全体に関連付けられています。

ここでは、次のトピックを指定するためのベスト プラクティスに[ハードウェア Id](hardware-ids.md)特定の種類のデバイス。

[Bluetooth デバイスのハードウェア Id を指定します。](specifying-hardware-ids-for-a-bluetooth-device.md)

[コンピューターのハードウェア Id を指定します。](specifying-hardware-ids-for-a-computer.md)

[多機能デバイスのハードウェア Id を指定します。](specifying-hardware-ids-for-a-multifunction-device.md)

形式の要件の詳細については、 **HardwareID** 、XML 要素を参照してください[ **HardwareID**](https://msdn.microsoft.com/library/windows/hardware/ff546114)します。

 

 




