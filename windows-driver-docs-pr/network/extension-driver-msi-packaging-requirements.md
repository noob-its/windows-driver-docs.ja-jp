---
title: 拡張機能のドライバー MSI パッケージの要件
description: スイッチ拡張機能は、サイレント モードでインストール可能な MSI ファイルにパッケージ化する必要があります。
ms.assetid: 300118F9-D9C7-4AFA-B54A-59666BC680F1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06fa51361afe23d74523b1bc58df1ef16b077a48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532332"
---
# <a name="extension-driver-msi-packaging-requirements"></a>拡張機能のドライバー MSI パッケージの要件


スイッチ拡張機能は、サイレント モードでインストール可能な MSI ファイルにパッケージ化する必要があります。 このファイルは、場所に拡張子が管理アプリケーションによって自動的に使用がコンピューターに展開できます。

MSI ファイルには、次の要件を満たす必要があります。

-   ドライバーをパッケージ化され、標準の MSI パッケージ形式で配布する必要があります。
-   MSI パッケージをサイレント モードでアンインストール可能にする必要があります。
-   MSI パッケージは、拡張機能の 1 つだけを含めることができます。
-   MSI パッケージは、MSI のテーブルのフィールドで説明されているフィールドは、以下に示す必要なテーブルを含める必要があります。 さらに、MSI ファイルがドライバーの .sys、.inf、およびドライバーで説明されているパラメーターを使用して動作するために必要な補足的なファイルをサイレント モードでインストールすることにある必要があります、 *DriverInstallParams*の MSI プロパティ テーブルのフィールド以下のフィールドの一覧。

| フィールド                           | 必須 | 種類       | 詳細                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|---------------------------------|----------|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **説明**                 | 必須 | **文字列** | 表示される拡張機能の説明です。                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **製造元**                | 必須 | **文字列** | 拡張機能ドライバーを公開する会社の名前です。 ローカライズされた文字列を格納することができます。                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **ProductVersion**              | 必須 | **文字列** | このバージョンの MSI パッケージ。 以下に例を示します。1.0.0.0                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **ProductName**                 | 必須 | **文字列** | ドライバーの名前。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **DriverID**                    | 必須 | **文字列** | Msvm に一致する必要があります\_InstalledEthernetSwitchExtension.Name フィールド、ドライバーをインストールした後に使用されると、ドライバーの INF ファイルでドライバーの ID。                                                                                                                                                                                                                                                                                                                                                    |
| **driverVersion**               | 必須 | **文字列** | このパッケージに含まれているドライバーのバージョン。 以下に例を示します。1.0.0.0                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **ExtensionType**               | 必須 | **文字列** | 拡張機能の型。 値:転送するには、キャプチャ、フィルターを監視します。                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| **DriverInstallParams**         | 必須 | **文字列** | このドライバーをサイレント モードでインストールするために使用するパラメーターです。 例:/q                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| **IsManagedByExtensionManager** | 省略可能 | **文字列** | 存在し、0 以外 = [はい] を 0 または存在しない = いいえ                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| **MinApplicableOSVersion**      | 必須 | **文字列** | この拡張機能で実行される Windows オペレーティング システムの最小バージョン。 オペレーティング システムのバージョン番号は、オペレーティング システムのバージョンを参照してください。 注 HYPER-V 拡張可能スイッチの機能が追加されたことで Windows Server 2012 では、そのためこのフィールドの最小有効値は、「6.2」です。                                                                                                                                                                                                                    |
| **MaxApplicableOSVersion**      | 省略可能 | **文字列** | この拡張機能で実行される Windows オペレーティング システムの最大バージョン。 参照してください[オペレーティング システムのバージョン](https://msdn.microsoft.com/library/windows/desktop/ms724832)オペレーティング システムのバージョン番号。 HYPER-V 拡張可能スイッチの機能が追加されたことで Windows Server 2012 では、そのためこのフィールドの最小有効値に注意してください「6.2」またはの値は、 **MinApplicableOSVersion**、高い方します。 このフィールドは省略可能です。 値が指定されていない場合、拡張機能がで実行が**MinApplicableOSVersion**以降。 |

 

 

 




