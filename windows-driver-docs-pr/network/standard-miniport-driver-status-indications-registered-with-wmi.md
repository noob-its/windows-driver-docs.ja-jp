---
title: WMI に登録されている標準のミニポート ドライバーの状態インジケーター
description: WMI に登録されている標準のミニポート ドライバーの状態インジケーター
ms.assetid: afebd0a2-c811-4534-9320-02b9292ba81b
keywords:
- 状態インジケーターの WDK ネットワー キング、WMI
- WMI の WDK は、ネットワーク状態インジケーター
- Windows Management Instrumentation WDK ネットワー キング、状態インジケーター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59931c1d6eddabb3638ada77c9f75afa8bc43ea5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552334"
---
# <a name="standard-miniport-driver-status-indications-registered-with-wmi"></a>WMI に登録されている標準のミニポート ドライバーの状態インジケーター





NDIS が自動的に登録 Guid wmi のミニポート ドライバーを示す NDIS 状態インジケーターの[ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)または[ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)関数。 全般的なステータス インジケーターの一覧は、次を参照してください。[状態インジケーター](https://msdn.microsoft.com/library/windows/hardware/ff570879)します。

WMI クライアント登録される WMI NDIS WMI イベントを受信すると場合、NDIS は WMI イベントに対応する NDIS 状態表示に変換し、すべてのイベントに登録されている WMI クライアントにイベントを報告します。

NDIS ドライバーは、カスタムの状態インジケーターを生成することもできます。 カスタムの状態インジケーターと WMI の詳細については、次を参照してください。 [Oid のカスタマイズと状態インジケーター](customized-oids-and-status-indications.md)します。

 

 




