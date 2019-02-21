---
title: ファイル システム フィルター ドライバーの INF ファイルを作成します。
description: ファイル システム フィルター ドライバーの INF ファイルを作成します。
ms.assetid: 1e8d0e59-eabd-4bdb-9675-e693a0b364ca
keywords:
- INF ファイル WDK ファイル システムを作成します。
- SetupAPI WDK ファイル システム
- 文字列は、WDK のファイル システムをセクションします。
- DefaultUninstall セクション WDK ファイル システム
- ServiceInstall セクション WDK ファイル システム
- DefaultInstall セクション WDK ファイル システム
- SourceDisksNames セクション WDK ファイル システム
- DestinationDirs セクション WDK ファイル システム
- WDK のファイル システムのバージョン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73d45c4d091bb26839400d7dd54dbe615a0be7c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530768"
---
# <a name="creating-an-inf-file-for-a-file-system-filter-driver"></a>ファイル システム フィルター ドライバーの INF ファイルを作成します。


## <span id="ddk_creating_an_inf_file_for_a_file_system_filter_driver_if"></span><span id="DDK_CREATING_AN_INF_FILE_FOR_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


Windows セットアップとデバイスのインストーラー サービスと総称[SetupAPI](https://msdn.microsoft.com/library/windows/hardware/ff550855)Windows のセットアップとドライバーのインストールを制御する機能を提供します。 インストール プロセスは、INF ファイルによって制御されます。

ファイル システム フィルター ドライバーの INF ファイルでは、SetupAPI を使用してドライバーをインストールする手順を説明します。 INF ファイルは、ドライバー ファイルをドライバーを実行し、ソースと変換先のディレクトリに存在する必要があるファイルを指定するテキスト ファイルです。 INF ファイルには、SetupAPI がレジストリに格納するドライバーの構成情報も含まれていますなど、ドライバーのスタートアップの種類および順序グループをロードします。

INF ファイルとの作成方法の詳細については、次を参照してください。 [INF ファイルを作成する](https://msdn.microsoft.com/library/windows/hardware/ff549520)と[INF ファイルのセクションとディレクティブ](https://msdn.microsoft.com/library/windows/hardware/ff547433)します。 ドライバーの署名の詳細については、次を参照してください。[ドライバーの署名](https://msdn.microsoft.com/library/windows/hardware/ff544865)します。

Windows オペレーティング システムの複数のバージョンでは、ドライバーをインストールする 1 つの INF ファイルを作成することができます。 このような INF ファイルを作成する方法の詳細については、次を参照してください。 [INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](https://msdn.microsoft.com/library/windows/hardware/ff540206)と[International INF ファイルの作成](https://msdn.microsoft.com/library/windows/hardware/ff540208)です。

以降では、64 ビット バージョンの Windows Vista では、すべてのカーネル モード コンポーネントでは、ファイル システム ドライバー (ファイル システム、従来のフィルターおよびミニフィルター ドライバー) などの非 PnP (プラグ アンド プレイ) ドライバーを含む署名が必要読み込みおよび実行するためにします。 これらの Windows オペレーティング システムのバージョンでは、次の一覧には、ファイル システム フィルター ドライバーに関連する情報が含まれます。

-   ファイル システム ドライバーなど、非 PnP ドライバーの INF ファイルを格納する必要はありません\[製造元\]または\[モデル\]セクション。

-   [ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)にある、コマンド ライン ツール、 \\bin\\WDK のインストール ディレクトリの SelfSign ディレクトリを直接「記号を埋め込む」を使用するドライバー SYS実行可能ファイルです。 パフォーマンス上の理由から、ブート開始ドライバーが埋め込みの署名を含める必要があります。

-   INF ファイルでは、指定された、 [ **Inf2Cat** ](https://msdn.microsoft.com/library/windows/hardware/ff547089)コマンド ライン ツールは、ドライバー パッケージのカタログ (.cat) ファイルを作成するために使用できます。 カタログ ファイルのみを受信できる[WHQL](https://go.microsoft.com/fwlink/p/?linkid=8705)ロゴ署名します。

-   管理者特権で未署名のドライバを Windows Vista 以降の x64 ベース システムでインストールもできます。 ドライバーを読み込む (およびため、実行する) に失敗するただし、署名されていないためです。

-   運転署名プロセスの詳細については、運転、署名の 64 ビット バージョンの Windows Vista では、プロセスを参照してください[カーネル モード コード署名のチュートリアル](https://go.microsoft.com/fwlink/p/?linkid=79445)します。

-   カスタム カーネル モード開発ツールを含むすべてのカーネル モード コンポーネントに署名する必要があります。 詳細については、次を参照してください。[開発およびテスト (Windows Vista 以降) の中にドライバーの署名](https://msdn.microsoft.com/library/windows/hardware/ff552275)します。

レジストリから情報を読み取る、またはユーザー モード アプリケーションを起動する INF ファイルを使用できません。

INF ファイルを作成するには後、は、セットアップ アプリケーションの通常のソース コードを記述します。 セットアップ アプリケーションは、ユーザー モードに INF ファイルの情報にアクセスし、インストール操作を実行するセットアップ関数を呼び出します。

独自フィルター ドライバーの INF ファイルを作成するには、サンプル ファイル システム フィルター ドライバーの INF ファイルをテンプレートとして使用します。 使用することができます、 [ChkINF](https://msdn.microsoft.com/library/windows/hardware/ff543461) INF ファイルの構文を確認するためのツール。

ファイル システム フィルター ドライバーの INF ファイルには、次のセクションでは、一般に含まれています。

-   バージョン (必須)

-   DestinationDirs (推奨されるが、省略可能)

-   SourceDisksNames (必須)

-   SourceDisksFiles (必須)

-   DefaultInstall (必須)

-   DefaultInstall.Services (必須)

-   ServiceInstall (必須)

-   DefaultUninstall (省略可能)

-   DefaultUninstall.Services (省略可能)

-   文字列 (必須)

### <a name="span-idversionsectionrequiredspanspan-idversionsectionrequiredspanspan-idversionsectionrequiredspanversion-section-required"></a><span id="Version_Section__required_"></span><span id="version_section__required_"></span><span id="VERSION_SECTION__REQUIRED_"></span>バージョンのセクション (必須)

[**バージョン**](https://msdn.microsoft.com/library/windows/hardware/ff547502)セクション クラスを指定します、GUID、フィルターの種類によって決定される次のコード例に示すようにします。

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Class       = "ActivityMonitor"
ClassGuid   = {b86dff51-a31e-4bac-b3cf-e8cfe75c9fc2}
Provider    = %Msft%
DriverVer   = 08/28/2000,1.0.0.1
CatalogFile = 
```

次の表は、値で、ファイル システム フィルター ドライバーを指定する必要があります、 [**バージョン**](https://msdn.microsoft.com/library/windows/hardware/ff547502)セクション。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エントリ</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>署名</strong></p></td>
<td align="left"><p>&quot;$WINDOWS NT $&quot;</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>クラス</strong></p></td>
<td align="left"><p>参照してください<a href="file-system-filter-driver-classes-and-class-guids.md" data-raw-source="[File System Filter Driver Classes and Class GUIDs](file-system-filter-driver-classes-and-class-guids.md)">ファイル システム フィルター ドライバーのクラスとクラス Guid</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ClassGuid</strong></p></td>
<td align="left"><p>参照してください<a href="file-system-filter-driver-classes-and-class-guids.md" data-raw-source="[File System Filter Driver Classes and Class GUIDs](file-system-filter-driver-classes-and-class-guids.md)">ファイル システム フィルター ドライバーのクラスとクラス Guid</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロバイダー</strong></p></td>
<td align="left"><p>INF ファイルでは、Microsoft 以外のプロバイダーを指定してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>DriverVer</strong></p></td>
<td align="left"><p>参照してください<a href="https://msdn.microsoft.com/library/windows/hardware/ff547394" data-raw-source="[&lt;strong&gt;INF DriverVer directive&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547394)"> <strong>INF DriverVer ディレクティブ</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>CatalogFile</strong></p></td>
<td align="left"><p>このエントリは空白のままにします。 今後、署名されたドライバーの WHQL が指定したカタログ ファイルの名前が含まれます。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddestinationdirssectionoptionalbutrecommendedspanspan-iddestinationdirssectionoptionalbutrecommendedspanspan-iddestinationdirssectionoptionalbutrecommendedspandestinationdirs-section-optional-but-recommended"></a><span id="DestinationDirs_Section__optional_but_recommended_"></span><span id="destinationdirs_section__optional_but_recommended_"></span><span id="DESTINATIONDIRS_SECTION__OPTIONAL_BUT_RECOMMENDED_"></span>DestinationDirs セクション (推奨されるが、省略可能)

[ **DestinationDirs** ](https://msdn.microsoft.com/library/windows/hardware/ff547383)セクションでは、フィルター ドライバーおよびアプリケーションのファイルのコピー先ディレクトリを指定します。

このセクションで、 **ServiceInstall**  セクションで、システム定義の数値を使用してよく知られているシステムのディレクトリを指定することができます。 これらの値の一覧は、次を参照してください。 [ **INF DestinationDirs セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547383)します。 次のコード例では、「12」の値はドライバー ディレクトリを指します (%windir%\\system32\\ドライバー)、Windows ディレクトリ (%windir%) を参照して、値「10」とします。

```cpp
[DestinationDirs]
DefaultDestDir             = 12
MyLegacyFilter.DriverFiles = 12
MyLegacyFilter.UserFiles   = 10,MyLegacyFilter
```

### <a name="span-idsourcedisksnamessectionrequiredspanspan-idsourcedisksnamessectionrequiredspanspan-idsourcedisksnamessectionrequiredspansourcedisksnames-section-required"></a><span id="SourceDisksNames_Section__required_"></span><span id="sourcedisksnames_section__required_"></span><span id="SOURCEDISKSNAMES_SECTION__REQUIRED_"></span>(必須) SourceDisksNames セクション

[ **SourceDisksNames** ](https://msdn.microsoft.com/library/windows/hardware/ff547478)セクションを使用する配布メディアを指定します。

次のコード例で、 [ **SourceDisksNames** ](https://msdn.microsoft.com/library/windows/hardware/ff547478)セクションには、1 つの配布メディアが一覧表示されます。 メディアの一意の識別子には 1 です。 定義されているディスク 1% % トークンによって、メディアの名前が指定されて、 [**文字列**](https://msdn.microsoft.com/library/windows/hardware/ff547485) INF ファイルのセクション。

```cpp
[SourceDisksNames]
1 = %Disk1%
```

### <a name="span-idsourcedisksfilessectionrequiredspanspan-idsourcedisksfilessectionrequiredspanspan-idsourcedisksfilessectionrequiredspansourcedisksfiles-section-required"></a><span id="SourceDisksFiles_Section__required_"></span><span id="sourcedisksfiles_section__required_"></span><span id="SOURCEDISKSFILES_SECTION__REQUIRED_"></span>(必須) SourceDisksFiles セクション

[ **SourceDisksFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff547472)セクションは、コピーするファイルの名前と場所を指定します。

次のコード例で、 [ **SourceDisksFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff547472)セクションは、ドライバーをコピーするファイルを一覧表示し、ファイルにある一意の識別子を持つ 1 (これは、メディアを指定します。識別子が定義されて、 [ **SourceDisksNames** ](https://msdn.microsoft.com/library/windows/hardware/ff547478) INF ファイルのセクションです)。

```cpp
[SourceDisksFiles]
myLegacyFilter.exe = 1
myLegacyFilter.sys = 1
```

### <a name="span-iddefaultinstallsectionrequiredspanspan-iddefaultinstallsectionrequiredspanspan-iddefaultinstallsectionrequiredspandefaultinstall-section-required"></a><span id="DefaultInstall_Section__required_"></span><span id="defaultinstall_section__required_"></span><span id="DEFAULTINSTALL_SECTION__REQUIRED_"></span>(必須) DefaultInstall セクション

[ **DefaultInstall** ](https://msdn.microsoft.com/library/windows/hardware/ff547356) ] セクションで、 [ **CopyFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff546346)ディレクティブは、ファイル システム フィルター ドライバーのドライバー ファイルをコピーし、ユーザー アプリケーション ファイルで指定されている変換先を[ **DestinationDirs** ](https://msdn.microsoft.com/library/windows/hardware/ff547383)セクション。

**注**  、 [ **CopyFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff546346)ディレクティブが、カタログ ファイルまたは INF ファイル自体を参照する必要がありますSetupAPI では、これらのファイルが自動的にコピーします。

 

Windows オペレーティング システムの複数のバージョンでは、ドライバーをインストールする 1 つの INF ファイルを作成することができます。 この種類の INF ファイルを作成して追加する[ **DefaultInstall**](https://msdn.microsoft.com/library/windows/hardware/ff547356)、 [ **DefaultInstall.Services**](https://msdn.microsoft.com/library/windows/hardware/ff547360)、 **DefaultUninstall**、および**DefaultUninstall.Services**セクションの各オペレーティング システムのバージョン。 各セクションのラベルでは、*装飾*(.ntx86、.ntia64、または .nt など) を適用するオペレーティング システムのバージョンを指定します。 この種類の INF ファイルを作成する方法の詳細については、次を参照してください。 [INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](https://msdn.microsoft.com/library/windows/hardware/ff540206)します。

次のコード例で、 [ **CopyFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff546346)ディレクティブは、INF ファイルのセクションの MyLegacyFilter.DriverFiles と MyLegacyFilter.UserFiles セクションに記載されているファイルをコピーします。

```cpp
[DefaultInstall]
OptionDesc = %MyLegacyFilterServiceDesc%
CopyFiles = MyLegacyFilter.DriverFiles, MyLegacyFilter.UserFiles
```

### <a name="span-iddefaultinstallservicessectionrequiredspanspan-iddefaultinstallservicessectionrequiredspanspan-iddefaultinstallservicessectionrequiredspandefaultinstallservices-section-required"></a><span id="DefaultInstall.Services_Section__required_"></span><span id="defaultinstall.services_section__required_"></span><span id="DEFAULTINSTALL.SERVICES_SECTION__REQUIRED_"></span>(必須) DefaultInstall.Services セクション

[ **DefaultInstall.Services** ](https://msdn.microsoft.com/library/windows/hardware/ff547360)セクションが含まれています、 [ **AddService** ](https://msdn.microsoft.com/library/windows/hardware/ff546326)方法とタイミングを制御するディレクティブのサービスを特定のドライバーが読み込まれます。

次のコード例で、 [ **AddService** ](https://msdn.microsoft.com/library/windows/hardware/ff546326)ディレクティブは、オペレーティング システムに MyLegacyFilter サービスを追加します。 %Mylegacyfilterservicename% トークンにはで定義されているサービス名の文字列が含まれています、 [**文字列**](https://msdn.microsoft.com/library/windows/hardware/ff547485) INF ファイルのセクション。 MyLegacyFilter.Service のドライバーの例の名前は、 **ServiceInstall**セクション。

```cpp
[DefaultInstall.Services]
AddService = %MyLegacyFilterServiceName%,,MyLegacyFilter.Service
```

### <a name="span-idddkserviceinstallsectionifspanspan-idddkserviceinstallsectionifspanserviceinstall-section-required"></a><span id="ddk_serviceinstall_section_if"></span><span id="DDK_SERVICEINSTALL_SECTION_IF"></span>(必須) ServiceInstall セクション

**ServiceInstall**セクションでは、サブキーを追加します。 または、値をレジストリに名前と値を設定します。 名前、 **ServiceInstall**にセクションを表示する必要があります、 [ **AddService** ](https://msdn.microsoft.com/library/windows/hardware/ff546326)ディレクティブで、 [ **DefaultInstall.Services**](https://msdn.microsoft.com/library/windows/hardware/ff547360)セクション。

次のコード例は、 **ServiceInstall** MyLegacyFilter ドライバーの例のセクション。

```cpp
[MyLegacyFilter.Service]
DisplayName    = %MyLegacyFilterServiceName%
Description    = %MyLegacyFilterServiceDesc%
ServiceBinary  = %12%\myLegacyFilter.sys
ServiceType    = 2 ;    SERVICE_FILE_SYSTEM_DRIVER
StartType      = 3 ;    SERVICE_DEMAND_START
ErrorControl   = 1 ;    SERVICE_ERROR_NORMAL
LoadOrderGroup = "FSFilter Activity Monitor"
AddReg         = MyLegacyFilter.AddRegistry
```

**DisplayName**エントリは、サービスの名前を指定します。 定義されている %mylegacyfilterservicename% トークンによって前の例では、サービス名の文字列が指定された、 [**文字列**](https://msdn.microsoft.com/library/windows/hardware/ff547485) INF ファイルのセクション。

**説明**エントリは、サービスを説明する文字列を指定します。 定義されている %mylegacyfilterservicedesc% トークンによって前の例では、この文字列が指定された、 [**文字列**](https://msdn.microsoft.com/library/windows/hardware/ff547485) INF ファイルのセクション。

**ServiceBinary**エントリは、サービスの実行可能ファイルへのパスを指定します。 前の例では、値 12 は、ドライバーのディレクトリを指します (%windir%\\system32\\ドライバー)。

**ServiceType**エントリは、サービスの種類を指定します。 次の表に、可能な値**ServiceType**とその対応するサービスの種類。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000001</p></td>
<td align="left"><p>SERVICE_KERNEL_DRIVER (デバイス ドライバー サービス)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000002</p></td>
<td align="left"><p>SERVICE_FILE_SYSTEM_DRIVER (ファイル システムまたはファイル システム フィルター ドライバー サービス)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000010</p></td>
<td align="left"><p>SERVICE_WIN32_OWN_PROCESS (独自のプロセスで実行されている Microsoft Win32 サービス)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000020</p></td>
<td align="left"><p>SERVICE_WIN32_SHARE_PROCESS (プロセスを共有する Win32 サービス)</p></td>
</tr>
</tbody>
</table>

 

**ServiceType**エントリは、サービスに常に設定する必要があります\_ファイル\_システム\_ファイル システム フィルター ドライバーのドライバーです。

**StartType**エントリでは、サービスを開始するタイミングを指定します。 次の表に、可能な値**StartType**とそれに対応する型を開始します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000000</p></td>
<td align="left"><p>SERVICE_BOOT_START</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000001</p></td>
<td align="left"><p>SERVICE_SYSTEM_START</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000002</p></td>
<td align="left"><p>SERVICE_AUTO_START</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000003</p></td>
<td align="left"><p>SERVICE_DEMAND_START</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000004</p></td>
<td align="left"><p>SERVICE_DISABLED</p></td>
</tr>
</tbody>
</table>

 

これらの詳細については、型をスタートを参照してください。[何を決定しますと、ドライバーが読み込まれる](what-determines-when-a-driver-is-loaded.md)します。

ドライバーのスタートアップの種類がサービスの場合\_ブート\_開始 (これは、ドライバーがブート開始ドライバーがある) も確認する必要があります、 **LoadOrderGroup**エントリはフィルターの種類に適した開発しています。 ロード順序グループを選択するを参照してください。[順序グループをファイル システム フィルター ドライバーの読み込み](load-order-groups-for-file-system-filter-drivers.md)します。 さらに、以降 Windows Vista の x64 ベース システムでは、ブート開始ドライバーのバイナリ イメージ ファイルは埋め込みの署名を含める必要があります。 この要件により、起動パフォーマンスの最適なシステムです。 詳細については、次を参照してください。[カーネル モード コード署名のチュートリアル](https://go.microsoft.com/fwlink/p/?linkid=79445)します。

方法については**StartType**と**LoadOrderGroup**エントリが特定のドライバーが読み込まれるときを参照してください[何を決定しますと、ドライバーが読み込まれる](what-determines-when-a-driver-is-loaded.md)します。

**ErrorControl**エントリは、システムの起動時に開始するサービスが失敗した場合に実行されるアクションを指定します。 次の表に、可能な値**ErrorControl**とその対応するエラーの値を制御します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">アクション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000000</p></td>
<td align="left"><p>SERVICE_ERROR_IGNORE (、エラーを記録およびシステムの起動を続行します)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000001</p></td>
<td align="left"><p>SERVICE_ERROR_NORMAL (、エラーを記録、ユーザーにメッセージを表示およびシステムの起動を続行します)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000002</p></td>
<td align="left"><p>SERVICE_ERROR_SEVERE (レジストリに切り替える&#39;s 前回正常起動時のセットの制御し、システムの起動を続行します)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000003</p></td>
<td align="left"><p>SERVICE_ERROR_CRITICAL (システムの起動時には、レジストリを使用していない場合&#39;s 前回正常起動時のコントロールの設定、前回正常起動時に切り替えるし、もう一度やり直してください。 起動が失敗した場合は、バグ チェック ルーチンを実行します。 システムが起動するために必要なドライバーのみがこの値を指定、INF ファイルにします。)</p></td>
</tr>
</tbody>
</table>

 

**LoadOrderGroup**を開発している、ファイル システム フィルター ドライバーの種類に適したロード順序グループ エントリを設定する必要があります。 ロード順序グループを選択するを参照してください。[順序グループをファイル システム フィルター ドライバーの読み込み](load-order-groups-for-file-system-filter-drivers.md)します。

[ **AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)ライター定義されている 1 つまたは複数の INF を指す**AddRegistry**のレジストリに格納される情報が含まれているセクションで、新しくサービスをインストールします。

**注**   INF ファイルも使用する場合は、最初のインストールに含まれるエントリの後に、ドライバーをアップグレードするため、 **AddRegistry**セクションは、0x00000002 を指定する必要があります (FLG\_ADDREG\_NOCLOBBER) フラグ。 このフラグを指定するには、HKLM レジストリ エントリが保持されます。\\CurrentControlSet\\サービスの後続のファイルがインストールされている場合。 次に、例を示します。

 

```cpp
[ExampleFileSystem.AddRegistry]
HKR,Parameters,ExampleParameter,0x00010003,1
```

### <a name="span-iddefaultuninstallsectionoptionalspanspan-iddefaultuninstallsectionoptionalspanspan-iddefaultuninstallsectionoptionalspandefaultuninstall-section-optional"></a><span id="DefaultUninstall_Section__optional_"></span><span id="defaultuninstall_section__optional_"></span><span id="DEFAULTUNINSTALL_SECTION__OPTIONAL_"></span>DefaultUninstall セクション (省略可能)

**DefaultUninstall**セクションは省略可能ですが、ドライバーをアンインストールする場合はお勧めします。 含まれている[ **DelFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff547363)と[**して**](https://msdn.microsoft.com/library/windows/hardware/ff547374)ディレクティブをファイルおよびレジストリ エントリを削除します。

次のコード例で、 [ **DelFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff547363)ディレクティブは、ドライバーの INF ファイルのセクションの MyLegacyFilter.DriverFiles と MyLegacyFilter.UserFiles セクションに記載されているファイルを削除します。

```cpp
[DefaultUninstall]
DelFiles   = MyLegacyFilter.DriverFiles, MyLegacyFilter.UserFiles
DelReg     = MyLegacyFilter.DelRegistry
```

[**して**](https://msdn.microsoft.com/library/windows/hardware/ff547374)ディレクティブを指すライター定義されている 1 つまたは複数の INF **DelRegistry**セクションでは、サービスのレジストリから削除する情報が含まれています。アンインストールしています。

### <a name="span-iddefaultuninstallservicessectionoptionalspanspan-iddefaultuninstallservicessectionoptionalspanspan-iddefaultuninstallservicessectionoptionalspandefaultuninstallservices-section-optional"></a><span id="DefaultUninstall.Services_Section__optional_"></span><span id="defaultuninstall.services_section__optional_"></span><span id="DEFAULTUNINSTALL.SERVICES_SECTION__OPTIONAL_"></span>DefaultUninstall.Services セクション (省略可能)

**DefaultUninstall.Services**セクションは省略可能ですが、ドライバーをアンインストールする場合はお勧めします。 含まれている[ **DelService** ](https://msdn.microsoft.com/library/windows/hardware/ff547377)ディレクティブをファイル システムを削除するドライバーのサービスをフィルター処理します。

次のコード例で、 [ **DelService** ](https://msdn.microsoft.com/library/windows/hardware/ff547377)ディレクティブは、オペレーティング システムから MyLegacyFilter サービスを削除します。

```cpp
[DefaultUninstall.Services]
DelService = MyLegacyFilter,0x200
```

**注**   、 [ **DelService** ](https://msdn.microsoft.com/library/windows/hardware/ff547377)ディレクティブは、0x200 を常に指定する必要があります (SPSVCINST\_STOPSERVICE) が削除される前に、サービスを停止するフラグ。

 

### <a name="span-idstringssectionrequiredspanspan-idstringssectionrequiredspanspan-idstringssectionrequiredspanstrings-section-required"></a><span id="Strings_Section__required_"></span><span id="strings_section__required_"></span><span id="STRINGS_SECTION__REQUIRED_"></span>文字列のセクション (必須)

[**文字列**](https://msdn.microsoft.com/library/windows/hardware/ff547485)セクションは、次の例に示すように、INF ファイルで使用されている各 %strkey% トークンを定義します。

```cpp
[Strings]
Msft                      = "Microsoft Corporation"
MyLegacyFilterServiceDesc = "MyLegacyFilterFilter Driver"
MyLegacyFilterServiceName = "MyLegacyFilter"
MyLegacyFilterRegistry    = "system\currentcontrolset\services\MyLegacyFilter"
MyLegacyFilterMaxRecords  = "MaxRecords"
MyLegacyFilterMaxNames    = "MaxNames"
MyLegacyFilterDebugFlags  = "DebugFlags"
Disk1                     = "MyLegacyFilter Source Media"
```

1 つの国際 INF ファイルを作成するにはロケールに固有の追加を作成して[**文字列**。](https://msdn.microsoft.com/library/windows/hardware/ff547485) *LanguageID* INF ファイルのセクション。 国際対応の INF ファイルの詳細については、次を参照してください。 [International INF ファイルの作成](https://msdn.microsoft.com/library/windows/hardware/ff540208)です。

 

 



