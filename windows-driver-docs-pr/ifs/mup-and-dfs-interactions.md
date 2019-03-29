---
title: MUP と DFS の対話
description: MUP と DFS の対話
ms.assetid: 39c1f1e3-fb2d-46e7-b3dc-3d4bfab9608c
keywords:
- DFS WDK ネットワーク リダイレクター
- 分散ファイル システムの WDK ネットワーク リダイレクター
- カーネル ネットワーク リダイレクター WDK、MUP
- MUP WDK ネットワーク リダイレクター
- 複数 UNC プロバイダー WDK ネットワーク リダイレクター
- UNC WDK ネットワーク リダイレクター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d94b1ee73289183e0b71dc00bc8bc697ddbbc432
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570133"
---
# <a name="mup-and-dfs-interactions"></a>MUP と DFS の対話


アプリケーションでは、汎用名前付け規則 (UNC) パスを使用する場合に使用するには、どのネットワーク プロバイダーを決定する、要求が複数 UNC プロバイダー (MUP) に送信されます。 MUP はチャネルがリモート ファイル システムの要求を処理できる適切なネットワーク リダイレクター (UNC プロバイダー) への要求です。 MUP が最初に、特定の要求を渡す、分散ファイル システム (DFS) クライアントが有効になっている場合"\\\\server\\共有"DFS クライアント要求が DFS のかを判断するには、通常のリモート ファイル共有ではなく共有します。

既定の動作は、DFS クライアントが有効になっています。 DFS クライアントは、次の下にあるレジストリ エントリの値に応じて無効になっています。

```cpp
HKLM\System\CurrentControlSet\Services\Mup
```

DisableDfs のレジストリ エントリは、1 の DWORD 値を持つ、DFS クライアントが無効になります。

MUP、(有効) の場合、DFS クライアントによって保持されるプレフィックスのキャッシュにない名前ベースの操作で指定されたパスのプレフィックスと仮定すると暗黙的にすべてリダイレクターよりも優先されます。 DFS クライアントが指定した UNC パスが DFS パスであるかどうかを確認しようとするとします。 この機能を使用するには、適切なサーバーの IPC$ 共有に参照の要求を送信します。 パスを判断して、DFS のパスを指定する、DFS クライアントが操作を処理します。 それ以外の場合、DFS クライアントは、名前に基づく要求を MUP の適切なリダイレクターによって処理されるプレフィックスの解決に渡します。

IPC$ 共有にアクセスする要求がシステムに送信されると、LAN Manager サーバー (SMB サーバーとも呼ばれます)、srv.sys が無効にするか (UNIX システムの例) にインストールされていないに接続するいくつかの試行が行われるため、遅延がある可能性があります、IPC$ 共有します。 この遅延は 5 ~ 7 (秒単位) では通常が、速度と接続するネットワーク インフラストラクチャとその他の条件の待機時間に基づくなくなりました。

 

 



