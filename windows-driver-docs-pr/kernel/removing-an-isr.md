---
title: ISR を削除します。
description: ISR を削除します。
ms.assetid: 23d84edb-763f-4383-b05c-832b4249b604
keywords:
- isr を特定の削除、割り込みサービス ルーチン WDK カーネル
- 割り込みオブジェクト WDK カーネルは、isr を特定の削除
- Isr WDK カーネル、isr を特定の削除
- WDK の isr を特定のカーネルを削除します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebb2bd039c9b372df276eb1f87459ac4ed05fefd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532342"
---
# <a name="removing-an-isr"></a>ISR を削除します。


ドライバーに登録されている ISR を削除できます[ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)呼び出して[ **IoDisconnectInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff549093)します。 **IoDisconectInterruptEx**を 1 つ受け取り*パラメーター*ポインターであるパラメーターを[ **IO\_切断\_INTERRUPT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff550569)構造体。 構造体のメンバーに使用される値は、ISR を登録するために使用するバージョンによって異なります。

ドライバーは、後でそれを削除する ISR を登録するときに特定の情報を保存する必要があります。 接続の\_行\_ベースおよび CONNECT\_完全\_指定されたバージョンでは、ドライバーがで指定された値を保存する必要があります、 **LineBased.InterruptObject**または**FullySpecified.InterruptObject**のメンバー [ **IO\_CONNECT\_INTERRUPT\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff550541)します。 接続の\_メッセージ\_ベース バージョンについては、ドライバーがで指定された値を保存する必要があります、**バージョン**と**MessageBased.ConnectionContext**のメンバー **IO\_CONNECT\_INTERRUPT\_パラメーター**します。

 

 



