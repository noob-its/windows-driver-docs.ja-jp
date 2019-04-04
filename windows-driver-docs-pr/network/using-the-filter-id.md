---
title: フィルター ID の使用
description: フィルター ID の使用
ms.assetid: 005AD1CF-37EB-44E8-BFA0-676ACCF69D47
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f65bd0a76e721999b7516d7f58a83fdddf1641ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580611"
---
# <a name="using-the-filter-id"></a>フィルター ID の使用


ドライバーのダウンロードを後続の OID メソッド要求を発行してミニポート ドライバーにフィルターを受信[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)します。 各受信フィルター ミニポート ドライバーにダウンロードするには、NDIS によって生成される一意のフィルタ識別子 (ID) があります。 上にあるドライバーは、以下を実行するためにこのフィルター ID 以降の OID 要求で使用する必要があります。

-   受信のフィルター パラメーターをクエリします。 受信フィルターのパラメーターをクエリする方法の詳細については、[クエリを実行するパケット結合受信フィルター](querying-packet-coalescing-receive-filters.md)を参照してください。

-   受信のフィルター パラメーターを変更します。 受信フィルターのパラメーターを変更する方法の詳細については、[変更パケット結合受信フィルター](modifying-packet-coalescing-receive-filters.md)を参照してください。

-   無料、または*オフ*、受信フィルター。 フィルターをクリアに受信する方法の詳細については、[クリア パケット結合受信フィルター](clearing-packet-coalescing-receive-filters.md)を参照してください。

ミニポート ドライバーでは、割り当てられた受信のフィルターのフィルター Id を保持する必要があります。 ミニポート ドライバーが OID 要求で指定したフィルター ID の前の OID メソッド要求から、割り当てられた受信フィルターが一致することを確認する必要がありますを変更し、クエリ、または、受信フィルターを無料の OID 要求を受信した場合[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)します。 フィルター ID が割り当てられている受信フィルターを一致しない場合、ミニポート ドライバーは、失敗したステータスの OID 要求を完了する必要があります。

 

 




