---
ms.assetid: bf92ab5f-9e54-4faa-8ae9-5cbe43434514
title: ドライバーへの署名
description: 64 ビット バージョンの Windows で実行されるすべてのドライバーには、Windows によって読み込まれる前に署名する必要があります。 ただし、ドライバーの署名は 32 ビット バージョンの Windows では必要ありません。Visual Studio がドライバー パッケージに署名します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af4e7e65df105ae2951d5ad9165552efb68250db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518320"
---
# <a name="signing-a-driver"></a>ドライバーへの署名

64 ビット バージョンの Windows で実行されるすべてのドライバーには、Windows によって読み込まれる前に署名する必要があります。 ただし、ドライバーの署名は 32 ビット バージョンの Windows では必要ありません。

ドライバーに署名するには、証明書が必要です。 開発中とテスト中に、ドライバーの署名に使う独自の証明書を作成できます。 ただし、一般リリースするためには、信頼されたルート機関によって発行された証明書でドライバーに署名する必要があります。

**注**  "*ドライバー パッケージ プロジェクト*" では、他のプロジェクトの出力をパッケージ化できます。 ドライバー パッケージ プロジェクトをビルドすると、Microsoft Visual Studio によって、そのプロジェクトが依存している他のプロジェクトがビルドされます。 ドライバー パッケージ プロジェクトには他の依存プロジェクトから切り離された独自のドライバー署名プロパティがあり、そのドライバー署名プロパティは、ドライバー パッケージ プロジェクトによって生成されたカタログ (存在する場合) に "*のみ*" 適用されます。 つまり、ドライバー パッケージ プロジェクトは他のプロジェクトによって生成されたドライバー バイナリに埋め込み署名を自動的には追加しません。その理由は、他のドライバー プロジェクトへの署名にテスト証明書などの異なる証明書が使用される可能性があり、その場合は、ドライバー パッケージのバイナリへの署名には一方の証明書が使われ、パッケージ カタログへの署名には異なる証明書が使われることになるためです。 この結果、パフォーマンスが低下することがあります。 たとえば、ブート開始ドライバー バイナリの埋め込み署名が無効である場合、Windows は、署名に使われた証明書を使ってバイナリを検証できません。 代わりに Windows はカタログの署名に対してバイナリを検証しなければならず、起動時間が延びます。

 

ここでは、Visual Studio を使ってドライバー パッケージに署名する方法について説明します。

-   [開発中とテスト中のドライバーへの署名](signing-a-driver-during-development-and-testing.md)
-   [一般リリース用のドライバーへの署名](signing-a-driver-for-public-release.md)

 

 




