---
title: 機能のトポロジ
description: 機能のトポロジ
ms.assetid: f25b3581-5561-4668-8549-65506b03815d
keywords:
- WDK BDA 機能のトポロジ
- WDK BDA のノードを制御します。
- テンプレートのトポロジ WDK BDA
- WDK AVStream の種類をピン留め
- WDK AVStream のノード
- Guid の WDK BDA のノードの説明
- 実際のトポロジ WDK BDA
- Guid の WDK BDA
- 制御ノード WDK BDA 復調器します。
- チューナー制御ノード WDK BDA
- ブロードキャスト ドライバー アーキテクチャ WDK AVStream、制御ノード
- BDA WDK AVStream、制御ノード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 223e090fcbed413dc60cd871b602ff52a8d8a377
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570960"
---
# <a name="functional-topology"></a>機能のトポロジ





ブロードキャストのアーキテクチャは、使い慣れたフィルター グラフの概念をさまざまな種類のネットワークに適している方法でフィルター グラフをブロードキャスト レシーバーの構築およびのチューナーとデコーダーの場合、たとえば、ハードウェアとソフトウェアの実装を有効にするにはDirectShow からの概念にそれを抽象化し、*機能トポロジ*します。 フィルター グラフなどの機能のトポロジでは、受信シグナルへの一連の発生する変換について説明します。 ただし、フィルター グラフとは異なり、機能のトポロジについては説明しません実際のフィルターや、ソフトウェア モジュールです。または、ソフトウェアまたはハードウェアで、操作を実装する方法。 代わりに、abstract の構成について説明します*制御ノード*のそれぞれがいくつかの一般的な独立した操作を表します。

別のフィルターをグラフの構成で結果ことができます、同じ機能のトポロジによっては、コンピューターにインストールされているハードウェアおよびソフトウェア コンポーネントの種類または*実際トポロジ*します。 たとえば、ハードウェア ベンダーが、同じ回線カードにチューナーと、復調器を実装する場合は、 [(KS) proxy モジュールのカーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff560877)として 2 つの 1 つのフィルターでフィルター グラフには、このハードウェア デバイスを表します内部制御ノード。 BDA デバイス フィルターと区別自体は、従来の DirectShow フィルターのため、1 つの BDA デバイス フィルターが同数ハードウェア機能 (管理ノードの実装) 1 つの機能モジュール (たとえば、回路に組み込まれているとカプセル化できます。カードまたはチップ)。

制御ノードを提供する関数は、GUID によって一意に識別されます。 GUID のノードの説明の定義は、次を参照してください。 [BDA ノード カテゴリ Guid](https://msdn.microsoft.com/library/windows/hardware/ff556529)します。 グラフ作成プロセス中にネットワーク プロバイダーのフィルターはこれらの Guid を使用してどのノードが特定のネットワークの種類をサポートしているまたは領域の調整で役に立ちますかを確認します。 ブロードキャスト レシーバー フィルターのグラフのフィルターは、COM インターフェイス、ノードの種類およびサポートされる pin の種類を示します。 フィルターの BDA ドライバーでは、KS プロパティ セットによってこの同じ情報を示します。 フィルターには、そのノードの種類、暗証番号 (pin) の種類、および pin とノードを接続することができますを方法を記述するデータ構造が含まれています。 この情報は、フィルターのと呼ばれる*テンプレート トポロジ*します。 次の図は、テンプレートのトポロジを示しています。

![テンプレートのトポロジを示す図](images/bapinnod.png)

前の図に、テンプレートのトポロジには、5 つの異なるノード型と 4 つのピン留めするさまざまな型が含まれています。 暗証番号 (pin) とノード型の数値は、フィルターによって割り当てられている任意の識別子です。 ただし、各ノード タイプは、ノードの記述を調べることができます、ネットワーク プロバイダー GUID に関連付けられます。 トポロジでは、各ノードの種類を 1 回だけ発生できますが、フィルターは、ノードの種類に任意に識別子を割り当てます、ため同じコントロールのノード GUID は、複数のノード型に関連付けられて。 たとえば、1 および 3 の番号で識別されるノードの種類は、2 つの異なる出力パスと同じコントロール ノード GUID を表すことができます。 テンプレートのトポロジでは、このシナリオに 2 つの個別のノード タイプを表す必要があります。 テンプレートのトポロジでのこれらのピン留めしてノード型をつなぐ線は、フィルターがサポートされているパスを表示します。

ネットワーク プロバイダーは、このトポロジの確認し、任意の特定のグラフ内の信号をフィルターを実行する変換を決定する必要があります。 テンプレートのトポロジを記述するデータ構造の詳細については、次を参照してください。[ドライバー アーキテクチャ ミニドライバーのブロードキャスト](broadcast-driver-architecture-minidrivers.md)します。

 

 



