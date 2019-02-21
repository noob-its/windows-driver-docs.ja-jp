---
title: 要件
description: 要件
ms.assetid: d939a319-f321-455e-a34d-220a3faf6092
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ba9938a61ce6830ff53cd94fb9659602e8752b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550344"
---
# <a name="requirements"></a>要件


記憶域のサイロ driver のシステムでは、次の要件を満たします。

-   対象となるシステムには、Windows XP、Windows Vista、および Windows 7 が含まれます。

-   エンドユーザーが発生するの 1667 UFD デバイスのレガシ UFD デバイス エクスペリエンス一貫性を維持する必要があります。

-   Windows XP および Vista の以前のバージョンでは、この USBStor.sys 以外の任意の既存システム バイナリの変更が依存しないでください。

-   記憶域のサイロ driver のシステムでは、柔軟性が確保、ハードウェア ベンダーのイノベーションのためのプラットフォームとして提供している 1667 認証クラスのソリューションを使用できます。 すべてのサード パーティ製の拡張機能ポイントがユーザー モード コードを使用してベンダーに提供されます。

-   サイロ ドライバーによって要求されていないこのサイロに許可されている排他的でないアクセスをサード パーティ製のアプリケーションはサポートされているものとします。

-   サイロの排他的所有権を主張するサード パーティ製 UMDF ドライバーがサポートされています。 アプリケーションまたはその他のドライバーでは、このドライバーを通じてサイロをアクセスできますのみ。

-   サード パーティの認証サイロ ドライバーでは、承認ワークフロー、ACT への参加を許可します。 仕入先は、発行された認証 DDI を実装する UMDF ドライバーを作成します。

-   旧バージョンとの互換性により、それ以外の場合 1667 デバイス用に予約されたプラットフォーム エクスペリエンスに参加する従来の非 1667 デバイスです。

-   記憶域のサイロ driver のシステムでは、Windows グループ ポリシーに従って、ホスト上のデバイスへのアクセスを管理します。 ポリシーは、デバイスまたは個別のサイロ レベルの粒度で適用することがあります。

-   ホストに動的に変化する ACL は、環境の複数のユーザーまたは高速なユーザー切り替え内のユーザー データへのアクセスを保護するセキュリティで保護されたソリューションを提供するために、一度に 1 人の承認されたユーザーへの排他の ACT アクセス権を付与します。

 

 



