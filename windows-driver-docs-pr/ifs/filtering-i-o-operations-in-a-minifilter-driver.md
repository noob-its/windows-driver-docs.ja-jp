---
title: ミニフィルター ドライバーでの I/O 操作のフィルタリング
description: ミニフィルター ドライバーでの I/O 操作のフィルタリング
ms.assetid: e35944c1-fcc6-44e0-838c-da8d24f95d51
keywords:
- preoperation コールバック ルーチン WDK ファイル システム ミニフィルター、ガイドライン
- postoperation コールバック ルーチン WDK ファイル システム ミニフィルター、ガイドライン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60d3dc0f9729f1421a8dc83f06eb6c98589fad92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572946"
---
# <a name="filtering-io-operations-in-a-minifilter-driver"></a>ミニフィルター ドライバーでの I/O 操作のフィルタリング


## <span id="ddk_filtering_io_operations_in_a_minifilter_driver_if"></span><span id="DDK_FILTERING_IO_OPERATIONS_IN_A_MINIFILTER_DRIVER_IF"></span>


次の一覧には、ファイル システム ミニフィルター ドライバーでの I/O 操作の特定の種類をフィルター処理するためのいくつかのガイドラインについて説明します。

-   [ **Preoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551109) IRP の\_MJ\_を作成することはできませんクエリまたはため、ファイル、ストリーム、またはストリームのハンドルは、コンテキストを設定済み作成時に、ファイルまたはストリーム (ある場合) を作成することが決定されていません。

-   [ **Postoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551107) IRP の\_MJ\_閉じるを設定またはいるため、ファイル、ストリーム、またはストリームのハンドルは、コンテキストを照会できませんシステム内部構造これらの項目が関連付けられているは、後の終了ルーチンを呼び出す前に、解放します。

-   ミニフィルター ドライバーは IRP に失敗することは決して\_MJ\_クリーンアップまたは IRP\_MJ\_閉じる操作。 これらの操作は、保留、フィルター マネージャーに返されるか、状態で完了しました\_成功します。 ただし、preoperation コールバック ルーチンでは、これらの操作が失敗しない必要があります。

-   ミニフィルター ドライバーは IRP の postoperation コールバック ルーチンを登録することはできません\_MJ\_シャット ダウンします。

 

 



