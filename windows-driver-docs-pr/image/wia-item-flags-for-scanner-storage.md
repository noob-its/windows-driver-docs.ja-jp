---
title: WIA 項目がストレージのスキャナーをフラグします。
description: WIA 項目がストレージのスキャナーをフラグします。
ms.assetid: 493b7c4f-d36a-4447-92a3-34b42ef58397
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 075692e00073bdde61b002a8b8591d52445eb7fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560405"
---
# <a name="wia-item-flags-for-scanner-storage"></a>WIA 項目がストレージのスキャナーをフラグします。


このトピックでは、ルート項目とストレージのスキャナー項目ツリーの子項目の必須および省略可能な WIA 項目フラグを使用します。 WIA 項目のフラグとその定義の完全な一覧を参照してください。 [ **WIA\_IPA\_項目\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff551585)します。

### <a name="required-wia-item-flags-for-scanners-storage"></a>WIA 項目フラグのストレージのスキャナーが必要

WIA ストレージのスキャナー フォルダー項目 (WIA\_カテゴリ\_フォルダー) が次 WIA 項目のフラグをサポートするために必要です。

<a href="" id="wiaitemtypefolder"></a>**WiaItemTypeFolder**  
アイテムはフォルダーです。 このフラグは、フォルダー アイテムでのみ必要です。

<a href="" id="wiaitemtypestorage"></a>**WiaItemTypeStorage**  
WIA 項目は、ストレージ アイテムを含む可能性のあるフォルダーです。 このフラグは、フォルダー アイテムでのみ必要です。

WIA ストレージのスキャナー ファイル項目 (WIA\_カテゴリ\_FINISHED\_ファイル) が次 WIA 項目のフラグをサポートするために必要です。

<a href="" id="wiaitemtypefile"></a>**WiaItemTypeFile**  
項目には、転送に使用できるデータが含まれています。 このフラグはでも必要です、 **WiaItemTypeImage**フラグ。

<a href="" id="wiaitemtypetransfer"></a>**WiaItemTypeTransfer**  
WIA 項目は、データ転送に使用できます。 フラット ベッド スキャナーの項目をデータ転送に使用できるため、このフラグが必要です。

### <a name="optional-wia-item-flags-for-scanners-storage"></a>スキャナーの記憶域に対するフラグの省略可能な WIA アイテム

WIA ストレージのスキャナー フォルダー項目 (WIA\_カテゴリ\_フォルダー) オプションで、WIA 項目の次のフラグをサポートできます。

<a href="" id="wiaitemtypedeleted"></a>**WiaItemTypeDeleted**  
項目を削除することができます必要に応じて、このフラグを使用できます。

WIA ストレージのスキャナー ファイル項目 (WIA\_カテゴリ\_FINISHED\_ファイル) オプションで、WIA 項目の次のフラグをサポートできます。

<a href="" id="wiaitemtypeaudio"></a>**WiaItemTypeAudio**  
項目は、オーディオ ファイルです。 ファイルがオーディオ データを格納しも設定されている項目に対してのみ有効ですが、このフラグは必要な**WiaItemTypeFile**フラグを設定します。

<a href="" id="wiaitemtypedeleted"></a>**WiaItemTypeDeleted**  
項目を削除することができます必要に応じて、このフラグを使用できます。

<a href="" id="wiaitemtypeimage"></a>**WiaItemTypeImage**  
項目は、イメージです。 ファイルは、イメージ データが含まれています。 され、も設定されている項目に対してのみ有効では場合は、このフラグは必要、 **WiaItemTypeFile**フラグを設定します。

 

 



