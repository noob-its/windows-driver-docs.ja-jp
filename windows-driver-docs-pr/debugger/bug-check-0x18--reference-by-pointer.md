---
title: バグ チェック 0x18 REFERENCE_BY_POINTER
description: REFERENCE_BY_POINTER のバグ チェックでは、0x00000018 の値を持ちます。 これは、オブジェクトの参照カウントがオブジェクトの現在の状態に対して有効であることを示します。
ms.assetid: 911fa821-5e59-4f20-a31b-148064e6c113
keywords:
- バグ チェック 0x18 REFERENCE_BY_POINTER
- REFERENCE_BY_POINTER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- REFERENCE_BY_POINTER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aed4bfbfb4786ceb17a510581efccbd9e874fbd3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536842"
---
# <a name="bug-check-0x18-referencebypointer"></a>バグ チェック 0x18 の。参照\_BY\_ポインター


参照\_BY\_ポインターのバグ チェックが 0x00000018 の値を持ちます。 これは、オブジェクトの参照カウントがオブジェクトの現在の状態に対して有効であることを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="referencebypointer-parameters"></a>参照\_BY\_ポインター パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>参照カウントが削減されているオブジェクトのオブジェクトの種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>参照カウントが削減されているオブジェクト。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

オブジェクトの参照カウントは、オブジェクトの現在の状態を使用できません。 ドライバーは、オブジェクトへのポインターを使用するたびに、ドライバーは、オブジェクトの参照カウントを 1 ずつ増加するカーネル ルーチンを呼び出します。 ドライバーは、ポインターでは、ドライバーはいずれかによって、参照カウントを減らす別のカーネル ルーチンを呼び出します。

ドライバーが増加するルーチンの呼び出しと一致する必要があります (*参照*) を増減 (*逆参照*)、参照カウントします。 このバグ チェックは、オブジェクトの参照カウントの不整合が原因です。 通常、オブジェクトを逆参照される余分な呼び出しを行っても多くの場合、オブジェクトの参照カウントを減らすドライバーによって不整合が発生します。 このバグ チェックは、オブジェクトの参照カウントがゼロには引き続き、オブジェクトへのハンドルを開くために発生することができます。 可能性がありますも発生するオブジェクトの参照カウントが 0 を下回ると、オブジェクトを開いているハンドルがあるかどうか。

<a name="resolution"></a>解決方法
----------

ドライバーが、オブジェクトの参照カウントを増減するルーチンの呼び出しと一致することを確認します。 ドライバーが、オブジェクトを逆参照するルーチンに余分な呼び出しを行わないことを確認します (パラメーター 2 を参照してください)。

この問題を分析するために、デバッガーを使用することができます。 詳細については、次を参照してください。 [Windows デバッガー (WinDbg) を使用してクラッシュ ダンプ分析](crash-dump-files.md)します。 [ **! 分析**](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるには非常に役に立ちます。

ハンドルとポインターがオブジェクトの数を確認する、 **! オブジェクト**デバッガー コマンド。

kd&gt; ! オブジェクト*アドレス*

場所*アドレス*パラメーター 2 で指定されたオブジェクトのアドレスです。

また、この停止コードに至るまで、コードにブレークポイントを設定、エラーが発生したコードをシングル ステップ転送しようし、することができますも。

Windows デバッガーを使用してこの問題に取り組むを備えていない場合は、基本的なトラブルシューティングの手法を使用できます。

-   デバイスまたはこのバグ チェックが原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。

-   バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

-   インストールされている新しいハードウェアが Windows のインストールされているバージョンと互換性があることを確認します。 たとえばに必要なハードウェアに関する情報を取得できます[Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)します。

-   その他の一般的なトラブルシューティング情報を参照してください。 [**青い画面データ**](blue-screen-data.md)します。

 

 



