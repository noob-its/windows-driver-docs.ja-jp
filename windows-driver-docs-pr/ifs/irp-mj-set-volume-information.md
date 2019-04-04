---
title: IRP_MJ_SET_VOLUME_INFORMATION
description: IRP\_MJ\_設定\_ボリューム\_情報
ms.assetid: 7c317e8b-ffa9-47f7-ac53-23b09873fab9
keywords:
- IRP_MJ_SET_VOLUME_INFORMATION インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_SET_VOLUME_INFORMATION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c28f85258d1af00cd199d1880af78a7dde7bf122
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570655"
---
# <a name="irpmjsetvolumeinformation"></a>IRP\_MJ\_設定\_ボリューム\_情報


## <a name="when-sent"></a>送信時


IRP\_MJ\_設定\_ボリューム\_情報の要求が I/O マネージャーによって送信されます。 送信できる、たとえば、ユーザー モード アプリケーションには、Microsoft Win32 関数が呼び出されるとなど**SetVolumeLabel**します。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システム ドライバーは、抽出して、ユーザー ボリュームのオープンを表すかどうかを確認するファイル オブジェクトをデコードする必要があります。 場合は、ファイル システム ドライバーが適切なボリュームの情報を設定し、IRP の完了する必要があります。 それ以外の場合、ファイル システムは IRP を適切なボリューム情報を設定せずに完了する必要があります。

設定可能なボリューム情報の種類はファイル システムに依存するが、一般に、次の 1 つ以上が含まれます。

FileFsControlInformation

FileFsLabelInformation

FileFsObjectIdInformation

すべての可能な情報の種類の一覧を参照してください、FS\_情報\_ntifs.h でクラスの列挙体。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、スタックの次の下位ドライバーには、この IRP を渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://msdn.microsoft.com/library/windows/hardware/ff550659)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP の一連のボリューム情報の要求の処理に IRP スタックの場所は、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
設定するボリューム情報の値を含む入力バッファーへのポインター。 この情報は、次の構造体のいずれかに格納されます。

ファイル\_FS\_コントロール\_情報

ファイル\_FS\_ラベル\_情報

ファイル\_FS\_OBJECTID\_情報

<a href="" id="irp--iostatus"></a>*Irp -&gt;IoStatus*へのポインター、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)に関する最終的な完了の状態および情報を受け取る、要求された操作。

<a href="" id="irpsp--fileobject"></a>*IrpSp -&gt;FileObject*に関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_設定\_ボリューム\_情報とすることはできませんこのオプションを使用するとします。

<a href="" id="irpsp--majorfunction"></a>*IrpSp -&gt;MajorFunction* IRP を指定します\_MJ\_設定\_ボリューム\_情報。

<a href="" id="irpsp--parameters-setvolume-fsinformationclass"></a>*IrpSp -&gt;Parameters.SetVolume.FsInformationClass*ボリューム用に設定する情報の種類を指定します。 この値には、次のいずれかを指定できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>FileFsControlInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff540258" data-raw-source="[&lt;strong&gt;FILE_FS_CONTROL_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540258)"> <strong>FILE_FS_CONTROL_INFORMATION</strong> </a>ボリューム。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsLabelInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff540271" data-raw-source="[&lt;strong&gt;FILE_FS_LABEL_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540271)"> <strong>FILE_FS_LABEL_INFORMATION</strong> </a>ボリューム。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsObjectIdInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff540274" data-raw-source="[&lt;strong&gt;FILE_FS_OBJECTID_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540274)"> <strong>FILE_FS_OBJECTID_INFORMATION</strong> </a>ボリューム。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-setvolume-length"></a>*IrpSp -&gt;Parameters.SetVolume.Length*によって指し示されるバッファーの長さをバイト単位で*Irp -&gt;AssociatedIrp.SystemBuffer*します。

## <a name="see-also"></a>関連項目


[**ファイル\_FS\_コントロール\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540258)

[**ファイル\_FS\_ラベル\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540271)

[**ファイル\_FS\_OBJECTID\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540274)

[**IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_クエリ\_ボリューム\_情報**](irp-mj-query-volume-information.md)

[**ZwQueryVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567070)

[**ZwSetVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567112)

 

 





