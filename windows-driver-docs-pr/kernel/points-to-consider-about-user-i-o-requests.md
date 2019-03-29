---
title: ユーザーの I/O 要求について考慮すべき点
description: ユーザーの I/O 要求について考慮すべき点
ms.assetid: e8143055-4ad7-4e39-a2f2-64d9e79d33a0
keywords:
- デバイスに固有の I/O 制御コード WDK カーネル
- プライベートの I/O 制御コード WDK カーネル
- 階層化ドライバー IRP の処理の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb2cfc121bb0f6f32cf9fdc077c0e46317a8a635
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578537"
---
# <a name="points-to-consider-about-user-io-requests"></a>ユーザーの I/O 要求について考慮すべき点





カーネル モード ドライバーを設計するときに、次の点に注意してくださいにしてください。

- ドライバーは、階層化できます、され、1 つ以上のドライバーが 1 つの I/O 要求 (IRP) を処理できます。

- ドライバーは、どのような想定を他のドライバーがデバイス スタック内になりますをことはできません。 したがって、各ドライバーでは、他のすべてのドライバーから要求を受信することがあり、すべての潜在的なエラー ケースを処理する必要があります。

- ドライバーは IRP の I/O の状態のブロックで要求された I/O 操作の成否を通信します。 I/O マネージャーは、ユーザー モードの要求者に要求された I/O 操作の成否を通信します。

- ドライバーは必要はありません、アプリケーション固有のサポートを提供する設計できないする必要があります。 保護されたサブシステムまたはそのサブシステムに固有では、ユーザー モード ドライバーはこの種のサポートを提供します。 このルールを 1 つの例外が発生: アプリケーション専用のデバイスに依存している MS-DOS アプリケーションは、デバイスを制御するためのカーネル モード ドライバーと密接に結合された Win32 ユーザー モード仮想デバイス ドライバー (VDD) を要求できます。 VDDs の詳細については、Windows ドライバー開発キット (DDK) で仮想デバイス ドライバーのマニュアルを参照してください。 (前に、DDK、Windows Driver Kit \[WDK\])。

- 新しいドライバーは、同じセットを処理する必要があります**IRP\_MJ\_* XXX*** としてのシステム提供のドライバーに置き換えられます。 I/O マネージャーがステータスを返します\_無効な\_デバイス\_そのドライバーがそのため、エントリ ポイントを定義していない場合は、ターゲット デバイスに特定の I/O 要求の要求<strong>IRP\_MJ\_* XXX</strong><em>.デバイス ドライバーもの同じ I/O 制御コードを処理する必要があります[ </em> *IRP\_MJ\_デバイス\_コントロール** ](<https://msdn.microsoft.com/library/windows/hardware/ff550744>)要求をいずれかとしてシステムによって提供されるドライバーに置き換えられます。 つまり、新しいデバイス ドライバー「中断してはいけませんアプリケーション」で同じ種類のデバイスの既存のドライバーよりも低い機能を実装します。

- 既存のドライバーのチェーンに挿入された新しい中間ドライバーでの同じセットを認識する必要があります**IRP\_MJ\_* XXX*** として変位させますが、ドライバー。 新しいドライバーは、下位レベルの次のドライバーには処理されませんそれらの要求の Irp で単に渡すことができます。 ただし、新しい中間ドライバーする必要がありますいないドライバーが上記の「チェーンが破壊」とエントリの定義を無視して、その下のポイントし、 **IRP\_MJ\_* XXX*** 要求を新しく変位させられた、次の下位のレベルドライバーが処理します。

- 最下位レベルのドライバーのみ独自 I/O スタック内の場所に送信されるすべての IRP にアクセスできます。 高度なドライバーにのみアクセスできます、独自および送信する任意の IRP で、[次へ] の下位レベルのドライバーの I/O スタックの場所。

- I/O マネージャーが、チェーン内の各ドライバーとして I/O スタックの対応する場所をゼロであるために、すべてのドライバーの Irp の I/O 状態ブロック内でのみの通信情報をより高度なドライバー (および最終的に I/O マネージャーを使用してユーザー モード アプリケーションを)IRP を完了します。 その移植性とその他のドライバーは、次から 1 つの Windows プラットフォームまたはバージョンの相互運用性の高い (またはそれ以下) の特定のドライバーの侵害との通信をバック ドアを実装しようとしています。 新しいドライバー。

- ドライバーのペアは、デバイスに固有のセットを定義できます (とも呼ばれる*プライベート*) のコードを I/O 制御[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)大きい方の値のペアを送信できるペアの下位に要求します。 ただし、ドライバーのようなペア従う必要がありますすべて、上記のガイドラインのポータブルと 1 つの Windows プラットフォームまたはバージョンから別の他のドライバーと相互運用を維持している場合。 プライベート インターフェイスとドライバーのペアを設計する場合は、慎重に定義されている I/O 制御コードのセットを検討してください。 可能な限り、一般に役立つものし、上記のガイドラインに従うようにする (または他のユーザー) できます再利用、置換、または 1 つの Windows プラットフォームまたはバージョンから移行する際、新しいドライバーの一方または両方を簡単にリプレース ペアになっているドライバーの設計別の。

 

 



