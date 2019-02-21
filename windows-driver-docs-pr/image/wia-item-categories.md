---
title: WIA 項目のカテゴリ
description: WIA 項目のカテゴリ
ms.assetid: b201e365-60d8-4c3b-a9cf-4bbaa318337f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a42aa3a5ddbe5ba30916fc12190a7d9bc18c7862
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538611"
---
# <a name="wia-item-categories"></a>WIA 項目のカテゴリ





このトピックには、Windows Vista 以降が適用されます。

WIA 項目ツリー内のすべての項目をサポートする必要があります、 [ **WIA\_IPA\_項目\_カテゴリ**](https://msdn.microsoft.com/library/windows/hardware/ff551581)プロパティ。 このプロパティは、項目が属する機能のカテゴリを識別します。 カテゴリは、WIA 項目のフラグと、項目に関連付けられている WIA プロパティのセットを決定します。

WIA では、次の項目のカテゴリを定義します。

<a href="" id="wia-category-root"></a>WIA\_カテゴリ\_ルート  
*ルート項目*項目に WIA スキャナーのデバイスのツリーが全体としてデバイスを表します。 デバイスには、フラット ベッド、ADF またはフィルム スキャン関数が含まれている場合、これらの入力ソースを表す項目、ルート項目の子です。 デバイスにストレージが含まれている場合、デバイスの記憶域階層の最上位フォルダーの項目は、ルート項目の子です。 アプリケーションは、状態、id に、ルート項目で実装された WIA プロパティからのアクセス権など、デバイスに関する情報にアクセスできます。 詳細については、ルート項目のプロパティでのディスカッションを参照してください[を実装するフラット ベッド スキャナーの項目のツリー](implementing-flatbed-scanner-item-trees.md)、[フィーダー スキャナー項目ツリーを実装する](implementing-feeder-scanner-item-trees.md)、および[フィルム スキャナーを実装する。項目のツリー](implementing-film-scanner-item-trees.md)します。

<a href="" id="wia-category-flatbed"></a>WIA\_カテゴリ\_ベッド  
A*ベッド項目*WIA スキャナーのデバイスのスキャンのフラット ベッド (スキャン プラテンとも呼ばれます) を表します。 スキャンのフラット ベッドを使用したデバイスの WIA 項目のツリーには、ルート項目の子であるベッド項目を含める必要があります。 さらに、WIA デバイスは、セグメント化をサポートしている場合 (たとえば、[セグメンテーション フィルター](wia-segmentation-filter.md)) マルチリー ジョンのスキャン、またはこのベッド項目する必要があります子を持つ、ベッドの項目はまたで個々 のスキャンの領域を表すフラット ベッドします。 子項目は、存在する場合に、同じ WIA に属する必要があります\_カテゴリ\_ベッドのカテゴリを親としてしたり、同じ WIA プロパティをサポート (と同じ初期プロパティ値を持つ) 必要があります、親 - を除くと、位置と子項目のエクステントは、それが表すスキャンのリージョンに制限されます。 アプリケーション フィルターを使用、WIA ドライバーのセグメント化 (提供されている) 場合、スキャンの領域を作成または、ミニドライバーが自動的に検出してスキャン領域自体を作成します。 アプリケーションは、フラット ベッド項目 (または項目) で実装された WIA プロパティを使用して関数をスキャン デバイスのベッドにアクセスできます。 詳細については、次を参照してください。[を実装するフラット ベッド スキャナーの項目のツリー](implementing-flatbed-scanner-item-trees.md)します。

<a href="" id="wia-category-feeder"></a>WIA\_カテゴリ\_フィーダー  
A*フィーダー項目*WIA スキャナーのデバイスで自動ドキュメント フィーダー (ADF) を表します。 (この項目のカテゴリでは、フィーダーを表すことができますも完全に自動でないと、ユーザーによる手動の支援が必要ですが、ここでは、WIA ミニドライバーは、次のドキュメント ページが高度なフィーダーをスキャンする前に検証を行うページです。)ADF を使用したデバイスは、その WIA 項目のツリーでフィーダー項目を含める必要があります。 フィーダー項目は、ルート項目の子です。 アプリケーションは、フィーダー項目で実装された WIA プロパティを使用して関数をスキャン デバイスの ADF にアクセスできます。 詳細については、次を参照してください。[フィーダー スキャナー項目ツリーを実装する](implementing-feeder-scanner-item-trees.md)します。

ADF は双方向のスキャンを実行できる場合 (つまり、スキャン、ドキュメントのページの両方の側)、およびドキュメント ページのフロント エンドとバックエンドの辺をスキャンするための別のコントロールの設定をサポートし、WIA ミニドライバーは、フィーダー フロント項目とフィーダー バック項目としてを実装する必要がありますフィーダー項目の子です。 アプリケーションは ADF の前面にアクセスし、WIA プロパティを使用して関数を戻すスキャン フィーダー フロント項目上で実装され、フィーダーの項目をバックアップします。 これら 2 つの項目の詳細については、次のカテゴリの説明を参照してください。

<a href="" id="wia-category-feeder-front"></a>WIA\_カテゴリ\_フィーダー\_フロント  
A*フィーダー フロント項目*スキャン、ドキュメント内のページの前面にあるのため、ADF 設定を表します。 この項目は、スキャナー デバイスの場合、双方向のスキャンを実行して、ドキュメント ページのフロント エンドとバックエンドの辺をスキャンするための別のコントロールの設定をサポートする adf WIA ミニドライバーで実装する必要があります。 Adf のドキュメント ページの両方の側を常に同じ設定を使用するデバイスでは、この項目は必要はありません。 フィーダー フロント項目は、フィーダー項目の子です。 アプリケーションは、フィーダー フロント項目で実装された WIA プロパティを使用して関数をスキャンする ADF 前面にアクセスできます。 詳細については、次を参照してください。[フィーダー スキャナー項目ツリーを実装する](implementing-feeder-scanner-item-trees.md)します。

<a href="" id="wia-category-feeder-back"></a>WIA\_カテゴリ\_フィーダー\_戻る  
A*フィーダー バック項目*スキャン、ドキュメント内のページの背面にあるのため、ADF 設定を表します。 この項目は、スキャナー デバイスの場合、双方向のスキャンを実行して、ドキュメント ページのフロント エンドとバックエンドの辺をスキャンするための別のコントロールの設定をサポートする adf WIA ミニドライバーで実装する必要があります。 Adf のドキュメント ページの両方の側を常に同じ設定を使用するデバイスでは、この項目は必要はありません。 フィーダー バック項目は、フィーダー項目の子です。 アプリケーションは、フィーダー バック項目で実装された WIA プロパティを使用して関数を戻すスキャン ADF にアクセスできます。 詳細については、次を参照してください。[フィーダー スキャナー項目ツリーを実装する](implementing-feeder-scanner-item-trees.md)します。

<a href="" id="wia-category-film"></a>WIA\_カテゴリ\_フィルム  
A*フィルム項目*フィルム スキャン WIA スキャナーのデバイスで関数を表します。 専用のフィルム スキャナーまたは透明度アダプター (TPA) を備えたフラット ベッド スキャナーは、デバイスは、その WIA 項目のツリーでフィルムの 1 つ以上の項目を含める必要があります。 フィルム項目は、ルート項目のまたは別のフィルムの項目の子です。 ルート アイテムの子であるフィルム項目は、全体のスキャンの画面を表し、このフィルム項目は、フィルムの個々 のフレームに対応するスキャンの画面の領域を表すフィルム アイテムである子を持つ可能性があります。 アプリケーションは、デバイスの映画のフィルムの項目 (または項目) で実装された WIA プロパティを使用して関数をスキャンでアクセスできます。 詳細については、次を参照してください。[を実装するフィルム スキャナーの項目のツリー](implementing-film-scanner-item-trees.md)します。

<a href="" id="wia-category-folder"></a>WIA\_カテゴリ\_フォルダー  
A*フォルダー項目*WIA スキャナーのデバイスの内部記憶域にあるフォルダーを表します。 フォルダー アイテムは、ルート項目のまたは別のフォルダー アイテムの子です。 フォルダーの項目に子がある場合は、子、完成したファイルの項目とフォルダーのアイテムの組み合わせです。 項目のツリーで最上位フォルダー項目では、ルート項目の子です。 アプリケーションは、フォルダー項目で実装される WIA プロパティを介して、フォルダーの内容と、フォルダーの情報にアクセスできます。 詳細については、次を参照してください。 [WIA スキャナー ストレージ](wia-scanner-storage.md)します。

<a href="" id="wia-category-finished-file"></a>WIA\_カテゴリ\_FINISHED\_ファイル  
A*完成したファイルの項目*WIA スキャナーのデバイス上のフォルダーに格納されている完成したファイルを表します。 完成したファイルは、ファイル内容は変更されません。 この定義では、ファイルの内容が動的に変更できる、例については、スキャナーを取得し、プロセスの画像データを除外します。 完成したファイルの項目は、フォルダー項目の子です。 アプリケーションでは、完成したファイルおよびファイルに関する情報を完成したファイルの項目で実装された WIA プロパティからアクセスできます。 詳細については、次を参照してください。 [WIA スキャナー ストレージ](wia-scanner-storage.md)します。

<a href="" id="wia-category-auto"></a>WIA\_カテゴリ\_自動  
Windows 7 以降では、[自動項目](auto-item.md)WIA スキャナーのデバイスをサポートする自動構成設定を表す[スキャンの自動構成](auto-configured-scanning.md)します。 この種類のデバイスでは、デスクトップ コンピューターで実行されている WIA アプリケーションを構成する設定を必要とするのではなく、独自のスキャン設定を構成できます。 たとえば、デバイスがデバイスからスキャン操作を開始するユーザーを有効 (の代わりに、アプリケーションのユーザー インターフェイスから) およびデバイスから、操作の入力ソースを選択するアプリケーションは、オフロードを自動項目を使用して、デバイスを選択した入力ソースを構成するタスク。 自動アイテムは、ルート項目の子です。 次の 1 つ以上が、自動の項目を含む WIA ツリーに含めることも必要があります: ベッド項目、フィーダー項目、またはフィルム項目。 アプリケーションは、ルート項目と自動の項目を実装 WIA プロパティを介して、デバイスの自動構成済みのスキャン機能にアクセスできます。 詳細については、次を参照してください。 [WIA して自動アイテムのプロパティがサポートされている](wia-properties-supported-by-an-auto-item.md)します。

各 WIA 項目のカテゴリには、WIA 項目の必要なフラグと、カテゴリ内の項目をサポートする必要があります、し、オプションとして、項目をサポートできるフラグとプロパティのセットをさらに、WIA プロパティのセットがあります。 フラグとさまざまな項目のカテゴリに関連付けられているプロパティの概要については、次を参照してください。 [ **WIA\_IPA\_項目\_カテゴリ**](https://msdn.microsoft.com/library/windows/hardware/ff551581)します。 WIA 項目のフラグの完全な一覧を参照してください。 [ **WIA\_IPA\_項目\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff551585)します。

 

 



