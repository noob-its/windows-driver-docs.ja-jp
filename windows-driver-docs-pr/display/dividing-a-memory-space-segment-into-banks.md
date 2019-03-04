---
title: 銀行メモリ領域のセグメントに分割
description: 銀行メモリ領域のセグメントに分割
ms.assetid: 7fdbe511-ae92-44c2-9651-51b3ead11425
keywords:
- メモリのセグメントの WDK 表示、銀行
- バンク メモリ WDK の表示
- WDK の銀行を表示します。
- 線形のメモリ領域のセグメントの WDK の表示
- メモリのセグメントの WDK 表示、線形のメモリ領域のセグメント
- WDK の表示メモリ領域の線形セグメントに分割
- メモリ空間のセグメントの WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46ff8dffa2daa21d4336d1e313ffbbd2f9aaafc0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552548"
---
# <a name="dividing-a-memory-space-segment-into-banks"></a>銀行メモリ領域のセグメントに分割


## <span id="ddk_dividing_a_memory_space_segment_into_banks_gg"></span><span id="DDK_DIVIDING_A_MEMORY_SPACE_SEGMENT_INTO_BANKS_GG"></span>


ディスプレイのミニポート ドライバーはビデオ メモリ マネージャー内でのビデオのリソースの割り当ての最適な配置にきめ細かなヒントを提供することができます、[セグメントの線形のメモリ領域](linear-memory-space-segments.md)バンク メモリ (セグメントに分割して銀行)。 ドライバーは、銀行に線形のメモリ領域のセグメントを分割する場合、ドライバーを設定する必要があります、 **UseBanking**でフラグをビット フィールド、**フラグ**のメンバー、 [ **DXGK\_SEGMENTDESCRIPTOR** ](https://msdn.microsoft.com/library/windows/hardware/ff562035)セグメントの構造体。 ドライバーはバンク メモリについてのヒントを返します、 **HintedBank**のメンバー [ **DXGK\_ALLOCATIONINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff560960)割り当ての構造とビデオ メモリマネージャーは、ドライバーの[ **DxgkDdiCreateAllocation** ](https://msdn.microsoft.com/library/windows/hardware/ff559606)関数。 詳細については、次を参照してください。[割り当てを作成するときにセグメントを指定する](specifying-segments-when-creating-allocations.md)します。

割り当ては、セグメント内で完全に含まれる必要があります、中に、割り当ては、銀行、セグメント内の境界を越えることができます。

銀行を使用している場合、ドライバーには銀行のセグメントの全体のアドレス空間する必要がありますについて説明します。 最初の銀行が常に、セグメント内のオフセット 0 から開始し、最後の銀行が常に、セグメントの末尾で終了します。 銀行では、連続してあり、それらの間の空き領域がありません。

 

 




