---
title: バグ チェック 0x1C7 STORE_DATA_STRUCTURE_CORRUPTION
description: STORE_DATA_STRUCTURE_CORRUPTION のバグ チェックでは、0x000001C7 の値を持ちます。 これは、ストア コンポーネントに、そのデータ構造体で破損が検出されたことを示します。
keywords:
- バグ チェック 0x1C7 STORE_DATA_STRUCTURE_CORRUPTION
- STORE_DATA_STRUCTURE_CORRUPTION
ms.date: 01/28/2019
topic_type:
- apiref
api_name:
- STORE_DATA_STRUCTURE_CORRUPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9fd80ca748b3293b2b4202fdf36e081966d1d140
ms.sourcegitcommit: 1a5d7884cec9dd8d2b85242bee78b56a1cf8e4c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/01/2019
ms.locfileid: "58761825"
---
# <a name="bug-check-0x1c7-storedatastructurecorruption"></a>バグ チェック 0x1C7 の。ストア\_データ\_構造\_破損

ストア\_データ\_構造\_破損バグ チェックが 0x000001C7 の値を持ちます。 これは、ストア コンポーネントに、そのデータ構造体で破損が検出されたことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。
 

## <a name="storedatastructurecorruption-parameters"></a>ストア\_データ\_構造\_破損パラメーター

|パラメーター|説明|
|-------- |---------- |
|1|破損の id。 次の値を参照してください。 |
|2| 次の値を参照してください。 |
|3| 次の値を参照してください。 |
|4| 次の値を参照してください。 |


**破損の ID**

```text
 0x0 : A chunk heap buffer's hash doesn't match.
    2 - Chunk heap buffer whose hash didn't match.
    3 - Expected buffer hash.
    4 - Page frame number of the corrupted page.

 0x1 : An unhandled exception occurred on the store thread and a chunk heap buffer's hash doesn't match, which is likely the source of the exception.
    2 - Chunk heap buffer whose hash didn't match.
    3 - Expected buffer hash.
    4 - Page frame number of the corrupted page.

 0x2 : Page data appears corrupt during a read and the corresponding page record's heap buffer hash doesn't match.
    2 - Chunk heap buffer whose hash didn't match containing the page record of the data being read.
    3 - Expected buffer hash.
    4 - Page frame number of the corrupted page.
 
 0x3 : Page data appears corrupt during a read and the corresponding page record has changed since the start of the read operation.
    2 - Pointer to the page location information snapped from the page record that was found when the read was initiated.
    3 - Pointer to the page record currently in the page tree for the same page key.
    4 - Reserved.
```

## <a name="cause"></a>原因
-----

ストアのコンポーネントには、そのデータ構造体で破損が検出されました。

このバグチェックに物理メモリ アクセスによるメモリの破損によって発生します。 物理メモリの破損の原因は次のとおりです。

1.  欠陥のある RAM ハードウェア
2.  ドライバーまたはデバイスが正しくない DMA 操作または関連付けられている MDL 経由で物理ページを正しく変更します。
3.  ハードウェア デバイスまたはファームウェアのファームウェアが不正に電力の変化全体で物理的なページの変更などのメモリの破損が原因で破損しています。

Windows メモリ マネージャーの詳細については、[内部 7 の Windows エディションのパート 1](https://docs.microsoft.com/en-us/sysinternals/learn/windows-internals) Pavel Yosifovich、E. のある Mark Russinovich、David A. Solomon、Alex Ionescu でを参照してください。

## <a name="resolution"></a>解決方法
-----

**Windows メモリ診断ツール**

このバグ チェックが RAM ハードウェアの欠陥によって発生した場合、調査には、Windows メモリ診断ツールを実行します。 コントロール パネルの検索ボックスには、メモリを入力し、クリックして *、コンピューターのメモリの問題を診断*します。テストの実行後は、イベント ビューアーを使用して、システム ログで結果を表示します。 探して、 *MemoryDiagnostics 結果*結果を表示するエントリ。

## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

[Windows カーネル モードのメモリ マネージャー](https://docs.microsoft.com/en-us/windows-hardware/drivers/kernel/windows-kernel-mode-memory-manager)