---
title: WIA プロパティの変更 - 特殊なケースがない必要があります。
description: WIA プロパティの変更 - 特殊なケースがない必要があります。
ms.assetid: 4ed02c01-efe8-4728-a54a-26fe27aa403c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64c997952055b0c72f9463b4f99558cd2793d6bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531832"
---
# <a name="mapping-wia-properties-that-need-no-changes---special-cases"></a>WIA プロパティの変更 - 特殊なケースがない必要があります。


互換レイヤーが失敗する場合は次のとおりです。

-   不足している破損している Windows XP プロパティが必要な Windows Vista のプロパティに関連する互換性レイヤーを使用できないレンダリング可能性があります。 このような場合は、現在のセッションは失敗です。項目の構造とプロパティ (このような場合で、アプリケーションの COM プロキシに機能しない) Windows XP および Windows Vista のドライバーとアプリケーション間の違いにより続行のオプションは使用できません。 [ **WIA\_DPS\_ドキュメント\_処理\_選択**](https://msdn.microsoft.com/library/windows/hardware/ff551384)と[ **WIA\_DPS\_ドキュメント\_処理\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff551379)プロパティは、特殊なケースは theWindows Vista のフラット ベッド項目のみが変換されます、Windows XP ドライバーによってサポートされていない場合アプリケーション

-   しない限り、その特定のコンテキストを設定すると、またはこれらのプロパティがコンテキストごとに異なる有効であり、現在の値がある可能性がありますに (フラット ベッドを送り、またはプロパティ コンテキスト) は、特定のコンテキストに依存する特定の Windows XP ルート プロパティを使用できない可能性があります。 WIA\_DPS\_ドキュメント\_処理\_正しいフィーダー/ベッド コンテキストを設定する選択が使用されます。、フィーダー (および必要な場合に双方向) に設定されますまたは Windows XP ドライバーのルート項目のフラット ベッドします。 その他のすべてのケースでコンテキスト設定してください、適切なプロパティ。 これは、場合も、Windows XP のデバイスは、フィーダーと、フラット ベッドの両方をサポートし、すべてのルートのプロパティは、Windows Vista のフラット ベッドとフィーダーの両方の項目に変換可能性があります。

-   重複する Windows Vista プロパティは、Windows XP の一意のプロパティを変換、WIA サービスについては、同じプロパティを別の Windows Vista 項目から別の値に設定されているケースを処理する方法を決定する必要があります。 ソリューションでは、コンテキストが変更されるたびに、すべての Windows XP A-AIT アイテムのプロパティを再初期化します。 このように別々 のプロパティのセットは、Windows Vista のドライバーのフィーダーとフラット ベッドの項目を Windows XP のアプリケーションからネゴシエートでした。

-   Windows Vista ドライバー フィーダーまたはベッドの項目を実装していないかどうか (たとえば、ドライバー実装フィルム/TPA(transparency adapter) や記憶域アイテムだけです)、互換性レイヤーは使用できません。 汎用の Windows XP の子項目は Windows Vista のフィルム/TPA やストレージの項目を常に作成できますと仮定する安全ではありません。 さらに、Windows Vista ドライバーがフィルム/TPA とストレージの両方のアイテムを実装している場合、さらに多くの問題が発生する可能性が。 そのため、少なくとも、ベッドまたはフィーダー項目を実装していない Windows Vista のドライバーの互換性レイヤが機能しません。

-   ドライバーは、部分的には、新しい Windows Vista 項目構造のサポートを実装が、Windows Vista のイメージの完全なサポートを提供する失敗する場合、Windows XP ドライバーが例については、正しい Windows XP 項目構造 (ルートと子項目をスキャン) を実装しない場合転送では、プロパティまたは項目の互換性レイヤが無効にして、現在のセッションは失敗します。

 

 



