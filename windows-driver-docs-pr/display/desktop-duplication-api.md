---
title: デスクトップの重複
description: Windows 8 には、デスクトップのコラボレーションとリモート デスクトップ アクセスのシナリオをサポートするために、独立系ソフトウェア ベンダー (Isv) が容易に新しい Microsoft DirectX Graphics Infrastructure DXGI ベースの API が導入されています。
ms.assetid: 5D4CBEA1-3C13-4B5C-A43D-7E6DBBB1A80F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7b9e7d6792d60a231da694ff409c7e502a734a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560814"
---
# <a name="desktop-duplication"></a>デスクトップの重複


Windows 8 には、デスクトップのコラボレーションとリモート デスクトップ アクセスのシナリオをサポートするために、独立系ソフトウェア ベンダー (Isv) が容易に新しい Microsoft DirectX Graphics Infrastructure DXGI ベースの API が導入されています。

このようなアプリケーションは、エンタープライズおよび教育のシナリオで広く使用されます。 これらのアプリケーションは、一般的な要件を共有します。 リモートの場所にコンテンツを転送する機能と共に、デスクトップの内容にアクセスします。 Windows 8 デスクトップ重複 Api では、デスクトップの内容へのアクセスを提供します。

現時点では、Windows API には、このシナリオをシームレスに実装するアプリケーションは許可されません。 そのため、アプリケーションを使用してミラー ドライバー、画面が不要になった機能およびその他の独自の方法、デスクトップの内容にアクセスします。 ただし、これらのメソッドでは、次の制限事項のセットがあります。

-   パフォーマンスを最適化することが難しい場合がします。
-   これらのソリューションでは、製品を出荷した後に、Api がリリースされるため、新しいグラフィックス レンダリングの Api はサポート可能性があります。
-   Windows では、最適化を支援する豊富なメタデータは常に提供されません。
-   すべてのソリューションは、Windows Vista 以降のバージョンの Windows でデスクトップ コンポジション互換性があります。

Windows 8 と呼ばれる DXGI ベースの API が導入されています*デスクトップ重複 API*します。 この API は、ビットマップと関連付けられているメタデータの最適化を使用して、デスクトップの内容へのアクセスを提供します。 この API を使用して、有効にすると、Aero のテーマで動作、グラフィックス API を使用するアプリケーションに依存することはありません。 ユーザーは、ローカルのコンソールでアプリケーションを表示することができます、いる場合は、コンテンツをリモートでも表示できます。 これには、そのでも全画面 DirectX アプリケーションを複製することを意味します。 API が保護されたビデオ コンテンツへのアクセスに対する保護を提供することに注意してください。

API は、モニターの境界に沿ってデスクトップの内容にアクセスできるように Windows を要求するアプリケーションを使用できます。 アプリケーションには、1 つまたは複数のアクティブな表示を複製できます。 アプリケーションでは、重複が要求を以下の処理が行われます。

-   Windows では、デスクトップを表示し、アプリケーションへのコピーを提供します。
-   レンダリングされた各フレームは、GPU のメモリに格納されます。
-   次のメタデータにはレンダリングされた各フレームできます。
    -   ダーティ領域
    -   画面に移動します
    -   マウスのカーソルに関する情報
-   アプリケーションでは、フレームとメタデータへのアクセスが提供されます。
-   アプリケーションは、各フレームの処理を担当します。
    -   アプリケーションは、ダーティ領域に基づく最適化を選択できます。
    -   ハードウェア アクセラレータを使用して、移動、およびマウスのデータを処理するアプリケーションを選択できます。
    -   圧縮をストリーミングする前にハードウェア アクセラレータを使用するアプリケーションを選択できます。

詳細なドキュメントとサンプルでは、次を参照してください。[デスクトップ重複 API](https://msdn.microsoft.com/library/windows/desktop/hh404487)します。

 

 




