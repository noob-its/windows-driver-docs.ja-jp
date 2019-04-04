---
title: AVCSTRM\_書き込み
description: AVCSTRM\_書き込み
ms.assetid: de11778d-21ab-40ae-8e7f-5229acfeea42
keywords:
- AVCSTRM_WRITE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVCSTRM_WRITE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6171fcf669ff755677cdfa6f4428f20a1ab8f7e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581227"
---
# <a name="avcstrmwrite"></a>AVCSTRM\_書き込み


## <span id="ddk_avcstrm_write_ks"></span><span id="DDK_AVCSTRM_WRITE_KS"></span>


**AVCSTRM\_書き込み**関数のコードは、指定したストリームに送信するデータ バッファーを送信するために使用します。

### <a name="io-status-block"></a>I/O ステータス ブロック

成功した場合、 *avcstrm.sys*設定**Irp -&gt;IoStatus.Status**ステータス\_成功します。

値には、可能性のあるエラーが返されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>エラーの状態</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STATUS_DEVICE_REMOVED</p></td>
<td><p>対応するデバイス、 <strong>AVCSTRM_READ</strong>操作が存在しません。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_CANCELLED</p></td>
<td><p>要求は完了できませんでした。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_INVALID_PARAMETER</p></td>
<td><p>IRP で指定されたパラメーターが正しくないです。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td><p>要求を完了するための十分なシステム リソースがありませんでした。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_PENDING</p></td>
<td><p>要求を受け取りましたが、さらに処理が必要です。 I/O 完了ルーチンでは、最後の応答を処理します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>コメント

この関数を使用して、 **BufferStruct**のメンバー、 **CommandData**共用体、AVC の\_ストリーム\_要求\_ブロック構造の下に示すようにします。

```cpp
typedef struct _AVC_STREAM_REQUEST_BLOCK {
  ULONG  SizeOfThisBlock;
  ULONG  Version;
  AVCSTRM_FUNCTION  Function;
  .
  .
  PVOID AVCStreamContext;
  .
  .
  union _tagCommandData {
    .
    .
    AVCSTRM_BUFFER_STRUCT  BufferStruct;
    .
    .
  } CommandData;
} AVC_STREAM_REQUEST_BLOCK, *PAVC_STREAM_REQUEST_BLOCK;
```

### <a name="requirements"></a>必要条件

**ヘッダー:** 宣言されている*avcstrm.h*します。 含める*avcstrm.h*します。

### <a name="span-idavcstreamrequestblockinputspanspan-idavcstreamrequestblockinputspanavcstreamrequestblock-input"></a><span id="avc_stream_request_block_input"></span><span id="AVC_STREAM_REQUEST_BLOCK_INPUT"></span>AVC\_ストリーム\_要求\_ブロックの入力

<span id="SizeOfThisBlock__Version_and_Function"></span><span id="sizeofthisblock__version_and_function"></span><span id="SIZEOFTHISBLOCK__VERSION_AND_FUNCTION"></span>**SizeOfThisBlock、バージョン、および関数**  
使用して、 [ **INIT\_AVCSTRM\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff560750)マクロをこれらのメンバーを初期化します。 渡す**AVCSTRM\_書き込み**マクロの要求の引数にします。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
によって以前返されるストリームのコンテキスト (ハンドル) を指定します**AVCSTRM\_オープン**データの書き込み操作について、ターゲットで呼び出すされています。

<span id="BufferStruct"></span><span id="bufferstruct"></span><span id="BUFFERSTRUCT"></span>**BufferStruct**  
バッファーの書き込み操作からのデータを取得する必要がありますを指定します。

サブユニット ドライバーは IRP を割り当てる必要があります最初、 [ **AVC\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff554194)構造体。 次に、使用する必要があります、 [ **INIT\_AVCSTRM\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff560750) 、AVC を初期化するためにマクロ\_ストリーム\_要求\_ブロック構造体渡す**AVCSTRM\_読み取り**マクロに要求の引数として。 次に、サブユニット ドライバーの設定、 **AVCStreamContext**メンバー データの書き込み操作の対象となっているストリームのストリーム コンテキスト (ハンドル) にします。 最後に、サブユニット ドライバーの設定、 **BufferStruct**のメンバー、 **CommandData**バッファー書き込み操作を記述する共用体からのデータを取得します。

この要求を送信するには、サブユニットの送信、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)で IRP、 **IoControlCode** IRP のメンバーに設定[ **IOCTL\_AVCSTRM\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff560778)と **[引数 1]** IRP のメンバーに設定AVC\_ストリーム\_要求\_行わへの書き込み操作を記述するブロック構造体。

このコマンドは、非同期的に完了します。 完了したら、IRP で設定する I/O 完了ルーチンが呼び出されます。

この関数のコードは、IRQL で呼び出す必要があります = パッシブ\_レベル。

### <a name="see-also"></a>関連項目

[**AVC\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff554194)、 [ **INIT\_AVCSTRM\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff560750)、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)、 [ **IOCTL\_AVCSTRM\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff560778)、 [ **AVCSTRM\_バッファー\_構造体**](https://msdn.microsoft.com/library/windows/hardware/ff554108)、 [ **AVCSTRM\_関数**](https://msdn.microsoft.com/library/windows/hardware/ff554120)

 

 




