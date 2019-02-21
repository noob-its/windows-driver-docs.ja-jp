---
title: SystemWake
description: SystemWake
ms.assetid: 77390637-bb92-4634-a407-9a409a8a8acd
keywords:
- SystemWake
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a982f012809b803cf6c74dbe979b67f9d942427
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528297"
---
# <a name="systemwake"></a>SystemWake





**SystemWake**のメンバー [**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)デバイスが、システムを wake 最低 (最小を利用した) システム電源の状態が含まれています、または**PowerSystemUnspecified**デバイスは、システムをスリープ解除できない場合。

バス ドライバーは、デバイスを列挙したときにこの値を設定します。 高度なドライバーは、パワー状態値を変更できますが、低電力状態に変更できません。 たとえば、バス ドライバー設定**SystemWake** S3 には、デバイス スタック サポート ウェイク アップ S2 からのみのドライバーをさらより高度なドライバーは、S2 に値を変更できます。 ドライバーが変更された場合**SystemWake**を変更する必要がありますも[ **DeviceWake**](devicewake.md)、次のセクションで説明するようにします。

ドライバーはほとんどデバイス スタックの下方の変更された値を伝達する必要があります。 変更より制限の厳しいデバイス機能を作成、ため、下位のドライバーに要求を処理できないものは表示されません。 前の例より高度なドライバーは、下位のドライバーにかかわらない、このような要求のために s2 の場合より低電力状態からシステムをスリープ解除するための要求を失敗します。 ただし場合、下位のドライバーは、すべての変更である必要があります、送信できる、PnP [ **IRP\_MN\_クエリ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff551664)の処理中に、独自デバイス スタックを[ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)します。

両方、 **SystemWake**と**DeviceWake**メンバーは、0 以外の場合 (つまり、いない**PowerSystemUnspecified**)、後、デバイスとそのドライバーのサポート、ウェイク アップのこのシステムで。

非 ACPI のハードウェアでこのメンバー常に含まれます 0 (**PowerSystemUnspecified**)。

 

 



