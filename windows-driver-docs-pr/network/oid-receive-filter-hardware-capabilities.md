---
title: OID_RECEIVE_FILTER_HARDWARE_CAPABILITIES
description: 上にあるドライバーは、ネットワーク アダプターの受信フィルタ リングのハードウェア機能を取得する OID_RECEIVE_FILTER_HARDWARE_CAPABILITIES の OID クエリ要求を発行します。
ms.assetid: 2b80944e-5309-4cb0-a69a-331f8fd3f7a4
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_HARDWARE_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 78d64ecb4baf0db3fcb15af9de2d75002ec0a8c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574604"
---
# <a name="oidreceivefilterhardwarecapabilities"></a>OID\_受信\_フィルター\_ハードウェア\_機能


上にあるドライバーは、OID の OID クエリ要求を発行\_受信\_フィルター\_ハードウェア\_ネットワーク アダプターのハードウェアの機能をフィルター処理、受信を取得する機能。

OID のクエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体ポインターが含まれています、[**NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)構造体。

<a name="remarks"></a>コメント
-------

NDIS フィルターが表示される次の NDIS インターフェイスで使用されます。

-   [NDIS パケット結合](https://msdn.microsoft.com/library/windows/hardware/hh451601)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[管理パケット結合受信フィルター](https://msdn.microsoft.com/library/windows/hardware/hh464026)します。

-   [シングル ルート I/O 仮想化 (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[仮想ポートで受信フィルターを設定](https://msdn.microsoft.com/library/windows/hardware/hh440224)します。

-   [バーチャル マシン キュー (VMQ)](https://msdn.microsoft.com/library/windows/hardware/ff571035)。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[設定および VMQ のフィルターをクリアする](https://msdn.microsoft.com/library/windows/hardware/ff570780)します。

[ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)構造体には、ネットワーク アダプターのハードウェアの機能をフィルター処理、受信に関する情報が含まれています. これらの機能は、INF ファイルの設定、または、現在無効になっているハードウェア機能を含めることができます、**詳細**プロパティ ページ。

**注**  の OID の OID クエリ要求をすべて受信フィルタ リングのハードウェア機能のネットワーク アダプターが返されます\_受信\_フィルター\_ハードウェア\_機能、関係なく、機能が有効か無効か。

 

受信ネットワーク アダプターのフィルタ リングのハードウェア機能を現在有効なレジスタ NDIS 6.20、以降のミニポート ドライバーとその[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数が呼び出されます。 ミニポート ドライバーでは、次の手順でこれらの機能を登録します。

1.  ドライバーの初期化、 [ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)受信フィルタ リングのハードウェア機能を含む構造体。

2.  ドライバーの初期化、 [ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)構造と設定、**CurrentReceiveFilterCapabilities**メンバーへのポインターを[ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)構造体。

3.  ミニポート ドライバーの呼び出し、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数とセット、 *MiniportAttributes*パラメーターへのポインターを[ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)構造体。

### <a name="return-status-codes"></a>リターン状態コード

OID の OID のクエリ要求を処理する NDIS\_受信\_フィルター\_ハードウェア\_ミニポート ドライバー、および次のステータス コードを返します。 1 つの機能。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。 **InformationBuffer**を指す、 [ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)構造体。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_PENDING  
完了待ちになっています。 NDIS 渡します最終的な状態コードと結果を呼び出し元の OID 要求の完了ハンドラーに要求が完了した後。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状態\_無効な\_長さ  
情報バッファーが小さすぎます。 NDIS セット、**データ。クエリ\_情報。BytesNeeded**内のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体に必要な最小バッファー サイズ。

<a href="" id="ndis-status-not-supported"></a>NDIS\_状態\_いない\_サポートされています。  
ネットワーク アダプターがサポートしていない受信フィルター処理します。

<a href="" id="ndis-status-failure"></a>NDIS\_状態\_エラー  
他の理由から、要求が失敗しました。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>以降では、NDIS 6.20 が動作をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_バインド\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff564832)

[**NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)

 

 



