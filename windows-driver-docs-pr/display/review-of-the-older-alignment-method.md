---
title: 以前の配置方法の確認
description: 以前の配置方法の確認
ms.assetid: 4efc380f-6303-42e1-8651-c9d64498942a
keywords:
- 描画サーフェスの整列 WDK DirectDraw を拡張します。
- DirectDraw surface 配置 WDK Windows 2000 の表示を拡張します。
- サーフェスの WDK DirectDraw、配置の拡張
- WDK DirectDraw surface の配置の拡張
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75e34887915424364e5893f3aac3581aefcf84db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530328"
---
# <a name="review-of-the-older-alignment-method"></a>以前の配置方法の確認


## <span id="ddk_review_of_the_older_alignment_method_gg"></span><span id="DDK_REVIEW_OF_THE_OLDER_ALIGNMENT_METHOD_GG"></span>


DirectDraw DirectX 5.0 前に、のバージョンでは、線形のヒープのピッチの配置要件を表現するドライバーを許可します。 この説明のためには、DirectDraw によってこれらのアラインメント要件の使用は、3 つの手順で確認できます。

1.  サーフェスを作成し、配置された入力**lPitch**ドライバーのグローバルのアラインメント要件に基づいて、メンバー (に返される、 [ **VIDEOMEMORYINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff570172)構造) と、画面の**ddsCaps**メンバー。 適切なアラインメント要件の倍数になるまでこのピッチが向上します。

2.  ドライバーの呼び出す[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)コールバック、定義されている場合。 ドライバーを変更できる、 **lPitch** Microsoft Windows 2000 以降の値がこの変更は無視されます。

3.  ドライバーの呼び出しが処理されない場合、または割り当てを要求した場合は、ドライバーのヒープのいずれかからサーフェイスでの表示メモリを割り当てます。 固定ピッチ手順 1 で確認し、手順 2. で、ドライバーによって変更されていない限り、割り当てられた画面の幅が取得されます。

ドライバーが実装されている場合、 [ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)コールバック、そのことを確認できます、入力方向の画面が必要があるその**lPitch**メンバー、固定値に設定します。 旧バージョンと互換性のためこの動作は引き続き存在します。 ドライバーが公開されている場合を除き、手順 3 がまったく同じ動作を維持する**GetHeapAlignment**エントリ ポイント (を参照してください、 [ **DD\_GETHEAPALIGNMENTDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551572)構造)。 、このエントリ ポイントが定義されている場合のみ、以前に計算された**lPitch**配置が破棄され、GUID を使用して報告要件に準拠しているすべてのサーフェスの整列\_GetHeapAlignment します。 ドライバーを保つことができます、 [ **VIDEOMEMORYINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff570172)アラインメント要件を構造体は、その古い DirectDraw ランタイムで実行されると、同じ配置動作を期待します。 この配置動作 DirectX 5.0 およびそれ以降のバージョンの DirectDraw ランタイムは完全に置き換えられました。 公開することに注意してください**GetHeapAlignment** GUID のものだけでなく、すべてのヒープの場合は、この従来の配置手順をオフに\_GetHeapAlignment アラインメント要件を報告します。

 

 




