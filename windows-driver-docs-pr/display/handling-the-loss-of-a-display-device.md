---
title: ディスプレイ デバイスの損失を処理
description: ディスプレイ デバイスの損失を処理
ms.assetid: 7af8d7e6-733d-4976-a516-7b41fa74dd5d
keywords:
- OPM WDK ディスプレイ、デバイスの紛失
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70740e4ce89c1aaebe5b9230019826dbd51941c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538371"
---
# <a name="handling-the-loss-of-a-display-device"></a>ディスプレイ デバイスの損失を処理


次のシナリオは、表示のミニポート ドライバーに呼び出しを開始する[ **DxgkDdiOPMDestroyProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559708)グラフィックス アダプターのコンテンツの保護のコネクタがありますの出力中に関数有効になります。

-   表示モードの変更

-   アタッチまたはデタッチ Windows デスクトップからの監視

-   全画面表示のコマンド プロンプト ウィンドウを入力します。

-   任意の DirectDraw または Direct3D 排他モード アプリケーションの開始

-   ユーザーの簡易切り替えを実行します。

-   ワークステーションをロックまたは CTRL + ALT + DEL キーを押します

-   リモート デスクトップ接続を使用して、ワークステーションへのアタッチ

-   たとえば、中断または休止状態に省電力モードの場合--

-   アプリケーション予期せずに終了 - たとえば、ページ フォールトを

 

 




