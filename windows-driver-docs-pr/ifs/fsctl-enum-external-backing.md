---
title: FSCTL_ENUM_EXTERNAL_BACKING 制御コード
description: FSCTL\_ENUM\_外部\_バッキング制御コードを開始またはバックアップ ソースがあるボリューム上のファイルの列挙を続行します。
ms.assetid: 86B07858-2F10-48EF-AEB5-7F4A23A55F7F
keywords:
- FSCTL_ENUM_EXTERNAL_BACKING 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_ENUM_EXTERNAL_BACKING
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b69caecfa9f04c1d53ef7d8dced05e45ac7f3f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558660"
---
# <a name="fsctlenumexternalbacking-control-code"></a>FSCTL\_ENUM\_外部\_バッキング制御コード


**FSCTL\_ENUM\_外部\_バックアップ**制御コードを開始またはバックアップ ソースがあるボリューム上のファイルの列挙を続行します。 各正常に終了要求のバックアップ ファイルの識別子が返されます。 外部プロバイダーは、そのバックに関係なく、すべてのバックアップ ファイルが列挙されます。 連続する**FSCTL\_ENUM\_外部\_バックアップ**ボリューム上のすべてのバックアップ ファイルを列挙する要求が必要です。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**パラメーター**

<a href="" id="instance--in-"></a>*インスタンス\[で\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 呼び出し元のポインターを不透明なインスタンス。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fileobject--in-"></a>*FileObject\[で\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 マウントを解除するボリュームを指定する、ファイル ポインター オブジェクト。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle--in-"></a>*FileHandle\[で\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 マウントを解除するボリュームのファイル ハンドル。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode\[で\]*  
操作のコードを制御します。 使用**FSCTL\_ENUM\_外部\_バックアップ**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
なし。 設定**NULL**します。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength\[で\]*  
0 に設定します。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[アウト\]*  
1 つまたは複数を受信するのに十分な大きさのサイズを持つ必要がある出力バッファーへのポインター **WOF\_外部\_ファイル\_ID**構造体。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength\[アウト\]*  
出力バッファーのサイズが指す*OutputBuffer*します。 *OutputBufferLength*あります&gt; =  **sizeof**(WOF\_外部\_ファイル\_ID)。

<a href="" id="lengthreturned--out-"></a>*LengthReturned\[アウト\]*  
書き込まれたバイト数を指定します*OutputBuffer*が正常に完了します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_操作が成功した場合は成功します。 それ以外の場合、適切な関数では NTSTATUS 値は次のいずれかを返す可能性があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>リクエスターでは、管理者特権はありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>によって示される出力バッファーの長さ<em>OutputBuffer</em>とで指定した<em>OutputBufferLength</em>が小さすぎます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_NO_MORE_FILES</strong></p></td>
<td align="left"><p>ボリュームのファイルでは、バックアップ元があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INTERNAL_ERROR</strong></p></td>
<td align="left"><p>要求されたボリュームにアクセスできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>バックアップ サービスが存在しないか開始されていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**WOF\_外部\_ファイル\_ID**で返される構造体*OutputBuffer*バックアップ ファイルの一意のファイル識別子を格納します。 構造体は、次のよう ntifs.h で定義されます。

```ManagedCPlusPlus
typedef struct _WOF_EXTERNAL_FILE_ID {
    FILE_ID_128 FileId;
} WOF_EXTERNAL_FILE_ID, *PWOF_EXTERNAL_FILE_ID;
```

A **FSCTL\_ENUM\_外部\_バックアップ**ソースのバックアップがボリューム上の各ファイルの識別子を取得する要求を連続して発行します。 すべてのファイルが列挙されると、ステータス\_いいえ\_詳細\_ファイルのステータス コードが返されます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8.1 Update 以降を利用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h または Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

[**FSCTL\_取得\_外部\_バックアップ**](fsctl-get-external-backing.md)

 

 





