---
title: 古いメソッド - Windows 10 バージョン 1607 およびそれ以前
description: 古いメソッド - Windows 10 バージョン 1607 およびそれ以前
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 739b8a90c89372f5e3175591cfa971b4e3116df0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560747"
---
# <a name="old-method---windows-10-version-1607-and-earlier"></a>古いメソッド - Windows 10 バージョン 1607 およびそれ以前

アップグレード シナリオ (Windows 10 への Windows 7) では、技術者は、OS を変更ファームウェアから Windows 7 の SPn のレガシ ブート + CSM に Win10 UEFI-CSM (CSM) を除く必要があり、Windows 7 SPn x64 インストール メディアを持ちます。

このプロセスは次のように見えます (詳細については下)。

1. このファームウェアまたはマザーボードの使用可能なセキュリティ オプションを OEM に問い合わせてください。 すべてのセキュリティ オプションは、いくつかのファームウェアまたはマザーボードできなくなります。

2. 全体のプライマリ ブート ディスク (を保存する) のすべてのデータをバックアップします。

    > [!NOTE]
    > イメージを作成する句または having OEM リカバリ メディアがお勧めします。

3. 作成、起動可能な x64 WinPE USB フラッシュ ドライブ (UFD) または CD または DVD。

4. ファームウェアのユーザー インターフェイス (UI) を再起動し、UEFI から起動する設定を切り替える (Win7 を起動する必要がある場合は必要 CSM ここでは有効になっている)。

5. USB や CD/DVD デバイス上の WinPE をブート (**セキュア ブート**無効にする必要があります、別のブート デバイスをブートする)。

6. Diskpart.exe を使用して、プライマリ クリーン ブート ディスクをワイプします。

    > [!NOTE]
    > 1 つ以上のディスクが存在する場合は、そのディスク 0 は、プライマリ ブート デバイスのディスクをクリーンアップする前にこのプロセスは、ディスク上のすべてのデータをワイプ確認します。

7. この時点では、いくつかのオプションがあるし、IT 担当者は、特定の指示/構成オプションのシステムの OEM にお問い合わせくださいする必要があります。

    a.   クリーン インストール メディアを挿入し、setup.exe を実行します。 可能性がある、インストール プロセスが CSM の検出し、レガシ ブートと BIOS モードで再インストールされます。

    b.   手順 5 は、プライマリのブート ディスクを使用した Diskpart.exe 内でまだ選択されているから"GPT に変換"を実行します

      - 挿入、インストール メディア、再起動、および設定を使用して移動します。 同様のテキストと共にエラー メッセージが「選択したデバイスをインストールことはできません」が発生したか「ディスクの形式がサポートされていません」を起動し、デバイスが CSM を検出して、レガシ ブート MBR メソッドを起動しようとしています。

      - また、UEFI ブート メソッドの GPT ディスクを手動で構成する手順に従います。 見て[Recommended UEFI-Based ディスク パーティション構成](https://technet.microsoft.com/library/dd744301)3 番目のパーティションを対象とする setup.exe を実行します。

8. Windows 7 が実行中の (最新バージョンにパッチを適用する必要があります) と、システムがインストールされると、Windows 10 にアップグレードします。

9. Windows 10 がインストールされているし、修正プログラムを適用、CSM、無効化を使用してテストし、このシステムで使用できるセキュリティ オプションを有効にするには製造元操作します。

    > [!NOTE]
    > ファームウェアでは一部のシナリオで、UEFI に固有のブート オプションがあります。 たとえば、a) ブートを選択します。 オプションまたは b) UEFI ブート オプション。

## <a name="related-resources"></a>関連リソース

[UEFI ベースのディスク パーティションの構成をお勧めします。](https://technet.microsoft.com/library/dd744301)