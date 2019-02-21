---
title: UWP デバイス アプリの手順 2. 作成デバイス メタデータ
description: このトピックでは、デバイス メタデータの作成ウィザードを使用して、UWP デバイス アプリをデバイスに関連付けられる新しいデバイスのメタデータを作成する方法を説明します。
ms.assetid: 61A3AE1B-2256-4034-AE9F-86E6900D9093
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f17cc44c5827959cbe3c2fd1306cb16d672ef25
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550931"
---
# <a name="step-2-create-device-metadata-for-your-uwp-device-app"></a>手順 2:UWP デバイス アプリのデバイス メタデータを作成します。

![デバイス アプリのワークフロー、手順 2](images/2-device-app-workflow.png)

このトピックでは、使用する方法を説明します、**デバイス メタデータの作成ウィザード**UWP デバイス アプリをデバイスに関連付けられる新しいデバイス メタデータを作成します。 ウィザードで作成できますも、 **StoreManfest.xml**ファイルを次の手順で、アプリを追加する必要があります。

UWP デバイスのアプリは、内部や周辺機器デバイスに対応するとして機能するデバイスの製造元が作成した UWP アプリの特別な種類です。 デバイス メタデータを使用すると、デバイス アプリは、特権操作を実行して、デバイスが接続されているときに自動的にインストールします。 UWP デバイスのアプリに関する詳細については、次を参照してください。[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)します。

**注**このトピックはステップ バイ ステップの一連の一部です。 参照してください[ステップ バイ ステップの UWP デバイスのアプリをビルド](build-a-uwp-device-app-step-by-step.md)導入します。

## <a name="before-you-begin"></a>始める前に

使用する、**デバイス メタデータの作成ウィザード**、Microsoft Visual Studio Professional、Microsoft、Visual Studio Ultimate をインストールする必要がありますまたは[スタンドアロン Windows 8.1 の SDK](https://go.microsoft.com/fwlink/p/?linkid=309209)、完了する前に、このトピックの手順を実行します。 Microsoft Visual Studio Express for Windows をインストールすると、ウィザードが含まれていない SDK のバージョンがインストールされます。

## <a name="create-new-device-metadata"></a>新しいデバイス メタデータを作成します。

**デバイス メタデータの作成ウィザード**新しいデバイスのメタデータを作成するために使用します。

### <a name="to-create-new-device-metadata"></a>新しいデバイスのメタデータを作成するには

1. 開始、**デバイス メタデータの作成ウィザード**から *%programfiles (x86) %*\\Windows キット\\8.1\\bin\\をダブルクリックして、x86**DeviceMetadataWizard.exe**します。

2. クリックして**新しいデバイスのメタデータ**します。

3. **メタデータ パッケージの種類を選択**] ページで [ **UWP デバイス アプリのメタデータ**、順にクリックします**次**。

4. **デバイス カテゴリの選択**ページで、デバイスに割り当てる必要があるデバイス カテゴリを選択します。 デバイスが複数のデバイス カテゴリに属することができますが、1 つだけの主なカテゴリを割り当てることができます。 **[次へ]** をクリックします。

5. **ロケールを指定** ページで、デバイス メタデータ パッケージに関連付けられている必要のある少なくとも 1 つのロケールを選択します。 ロケール固有のパッケージがコンピューターで利用できない場合に使用される既定のロケールを設定することもできます。 **[次へ]** をクリックします。

6. **デバイスについて説明する**ページで、デバイスを接続するエンドユーザーに表示される情報を入力します。 製造元とモデルの名前は、各ロケールの必要があります。

7. **ハードウェア情報を指定して** ページで、少なくとも 1 つのハードウェア ID と 1 つのモデル ID の追加 ハードウェア ID では、会社のベンダーの ID を含める必要があります。 モデル ID は GUID であり、モデル ID をサポートするデバイスとデバイスのメタデータを関連付けることをお勧めの方法 **[次へ]** をクリックします。

8. **指定 UWP デバイスのアプリ情報**ページ。

   - 有効にする場合[自動インストール](auto-install-for-uwp-device-apps.md)デバイス アプリの拡張、または、[カメラ](uwp-device-apps-for-webcams.md)または[プリンター](uwp-device-apps-for-printers.md) (する場合は自動インストールが必要です) が発生する、入力、Microsoft Store アプリの情報で、 **UWP デバイス アプリ**ボックス。 をクリックして**インポート UWP アプリのマニフェスト ファイル**自動的に入力する、**パッケージ名**、**パブリッシャー名**と**UWP アプリの ID**します。

     > [!Warning]
     > 自動インストール機能が提供しないことを通知をユーザーにアプリがインストールされている場合に注意してください。 一部のユーザーは、混乱とフラストレーション、このエクスペリエンスを検索し、アプリに不適切な評価を可能性があります。

   - 場合は、アプリは、プリンターの通知の登録は、入力、**通知ハンドラー**ボックス。 **イベント ID**、印刷イベント ハンドラーの名前を入力します。 **イベント資産**、そのコードが存在するファイルの名前を入力します。

   - 特権のあるアプリとしてアプリを指定する場合は、その情報を入力します。、**特権付きアプリケーション**ボックス。 特権を持つアプリの指定により、UWP デバイスのアプリを実行[デバイスの更新プログラム](device-sync-and-update-for-uwp-device-apps.md)ファームウェアの更新など。 Oem こともでき、コンポーネント サプライヤー用のアプリを開発する[内部デバイス](uwp-device-apps-for-specialized-devices.md)します。

9. すべての自動インストールと特権を持つアプリの詳細の指定を完了したら、クリックして **[次へ]**

10. **Windows 設定を指定** ページで、切断されている場合、自動再生のアクティブ化する必要があります、デバイスが応答する方法と、デバイスはデバイス マネージャーに表示されている場合を構成できます。

    アプリにし、デバイスの既定の自動再生ハンドラーを指定したい場合**UWP デバイスのアプリを使用して**で、**自動再生ハンドラー**ボックス。 UWP アプリや UWP デバイスのアプリを選択することができますが、そのアプリがデバイスの自動再生のアクティブ化を処理し、アプリのパッケージ マニフェストの ID が発生する、対応するを指定する必要があります (」の説明に従って[UWP デバイス アプリの自動再生](autoplay-for-uwp-device-apps.md))。

    - **パッケージ名**:アプリ パッケージ マニフェストでの Identity 要素の Name 属性になります。

    - **発行元名**:アプリ パッケージ マニフェストでは、Identity 要素の Publisher 属性です。

    - **アプリ ID**:アプリ パッケージ マニフェストでアプリケーションの要素の ID 属性です。

    - **動詞**:これは、自動再生のアクティブ化の識別子です。 アプリをデバイスからアクティブ化が付属しているかを判断に使用します。 動詞設定では、任意の値を使用するには除く**開く**は予約されています。

    - **自動再生イベントの種類**:としてのままに**デバイス**します。 デバイス メタデータ、ウィザードでは UWP デバイス アプリに関連付けられているエクスペリエンスの ID を指定することが自動的に。

    他のアプリを選択し、デバイスの自動再生ハンドラーとして機能できるようにする場合**登録済みのアプリの自動再生を有効にする**します。

    自動再生の詳細については、次を参照してください。 [UWP デバイス アプリの自動再生](autoplay-for-uwp-device-apps.md)します。

11. 続行する準備ができたら、クリックして**次**します。

12. **デバイス メタデータ パッケージの確認** ページで、すべての設定が正しいことを確認します。 ローカルのメタデータ ストアで使用できるこのデバイス メタデータ パッケージを実行する場合に、選択、**デバイス メタデータ パッケージをローカル コンピューター上のメタデータ ストアにコピー**チェック ボックスをオンにして**保存**.

13. デバイス メタデータ パッケージを送信する準備ができたとき、または編集する必要がある場合は、.devicemanifest ms ファイルを使用する必要があります。 デバイス メタデータをローカルでのテストにのみ .devicemetadata ms ファイルを使用する必要があります。

## <a name="next-step"></a>次の手順

[手順 3:アプリに、エクスペリエンスの ID を追加します。](step-3--add-an-experience-id-to-the-app.md)

## <a name="related-topics"></a>関連トピック

[UWP デバイス アプリをビルドします。](the-workflow.md)

[デバイスとの同期と UWP デバイス アプリの更新](device-sync-and-update-for-uwp-device-apps.md)

[内部デバイス用の UWP デバイス アプリ](uwp-device-apps-for-specialized-devices.md)