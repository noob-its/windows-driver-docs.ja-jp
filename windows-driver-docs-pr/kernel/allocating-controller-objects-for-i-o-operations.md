---
title: I/O 操作用のコント ローラー オブジェクトの割り当てください。
description: I/O 操作用のコント ローラー オブジェクトの割り当てください。
ms.assetid: 8a5e3741-f8ea-4e27-bb7f-6c20da1d618d
keywords:
- コント ローラー オブジェクトの WDK カーネルの割り当て
- ControllerControl ルーチン、コント ローラー オブジェクトの割り当て
- IoAllocateController
- コント ローラーのオブジェクトを割り当てください。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3b548c844942ef099a9dbcc761d7ba14529e34e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548700"
---
# <a name="allocating-controller-objects-for-io-operations"></a>I/O 操作用のコント ローラー オブジェクトの割り当てください。





コント ローラー オブジェクトを使用するドライバーがそのデバイスを起動した後、プロセス Irp がそのオブジェクトはターゲット デバイスに送信する準備が。 IRP が I/O 操作のコント ローラーのオブジェクトによって表される物理デバイスのプログラムにドライバーを必要とされるたびに、ドライバーが呼び出す[ **IoAllocateController**](https://msdn.microsoft.com/library/windows/hardware/ff548224)します。 次の図は、このような呼び出しを示しています。

![i/o コント ローラー オブジェクトの割り当てを示す図](images/3ctlaloc.png)

前の図に示すようにドライバーを指定する必要がありますよりも多く*ControllerObject*によって返されたポインター [ **IoCreateController** ](https://msdn.microsoft.com/library/windows/hardware/ff548395) 呼び出し時に[ **IoAllocateController**](https://msdn.microsoft.com/library/windows/hardware/ff548224)します。 このポインターと共に、ドライバーが提供する現在の I/O 要求の対象を表すデバイス オブジェクト、ポインターを渡す必要があります、 [ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049)ルーチン、およびどのに*コンテキスト*その*ControllerControl*ルーチンは、要求された I/O 操作のデバイスを設定する必要があります。

**IoAllocateController**ドライバーによって提供されるキュー *ControllerControl*ルーチンの場合は、コント ローラー オブジェクトによって表されるデバイスがビジー状態です。 それ以外の場合、 *ControllerControl*ルーチンは、上記の図に示すように入力パラメーターを使用してすぐに呼び出されます。 入力*コンテキスト*へのポインター **IoAllocateController**ドライバーに渡される*ControllerControl*ルーチンを実行した場合。

コンテキスト情報を格納するのに場所を特定するのにには、次のガイドラインを使用します。

-   コント ローラー拡張機能で、ドライバーは、物理コント ローラーで別の操作を開始する前に完了するまで各 IRP を処理しない限り、ドライバーによって提供されるコンテキストの領域がすることはできません。 それ以外の場合、または新しい IRP の受信時にその他のドライバーのルーチンでコント ローラー拡張機能でコンテキストの領域は上書きされることができます。

-   ドライバーには、デバイス別のデバイス オブジェクトの I/O 操作が重なっていると、場合でも、ターゲット デバイス オブジェクトの拡張機能でデバイス コンテキストの領域を上書きできません。

-   特定のデバイス オブジェクトの別の I/O 要求が行われ、ドライバーは場合、 [ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858) 、日常的なデバイスの拡張機能内のコンテキストの領域も上書きできません受信 IRP があるため、ドライバーを呼び出すときにキューに置かれた[ **IoStartPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550370)と同じ IRP はキューに残ります、デバイス ドライバー呼び出しまで[**います**](https://msdn.microsoft.com/library/windows/hardware/ff550358)直前にそのデバイス オブジェクトの現在の IRP を完了します。

I/O マネージャーへのポインターを渡す、*デバイス オブジェクト*-&gt;**CurrentIrp**を*ControllerControl*ルーチンの場合、ドライバーは、 *StartIo*ルーチン。 かどうか、ドライバーは Irp の専用キューではなくを管理、 *StartIo* I/O マネージャーを与えることはできません、日常的な*ControllerControl*ルーチン現在 IRP へのポインター。 ドライバーを呼び出すと**IoAllocateController**、現在の IRP の一部として渡すか、*コンテキスト*-アクセス可能なデータ。

ドライバーのルーチンを呼び出す**IoAllocateController** IRQL で実行する必要があります = ディスパッチ\_レベルの呼び出しが発生した場合。 この呼び出しからは、ドライバー、 *StartIo*ルーチンがディスパッチで既に実行されている\_レベル。

*ControllerControl*ルーチンが IRP の要求された操作の物理的なコント ローラーを設定します。

前の図に示すように、 *ControllerControl*ルーチンは、型の値を返します[ **IO\_割り当て\_アクション**](https://msdn.microsoft.com/library/windows/hardware/ff550534)、なることができます次のシステム定義の値のいずれか:

-   場合、 *ControllerControl*返すか、物理コント ローラーで別の操作を起動できるは、ルーチン、 **DeallocateObject**次に I/O 操作が要求されたため、ドライバーが重複することができます。

    たとえば場合、 *ControllerControl*ルーチンは、プログラムの 1 つのディスクのシーク操作のディスク コント ローラー、その IRP の完了、および戻り値**DeallocateObject**、 *ControllerControl*ルーチンは、転送要求は、他のディスクにキューが現在場合、その他のディスク上の転送操作のディスク コント ローラーをプログラムをもう一度呼び出すことができます。

-   現在の IRP では、その他のドライバー ルーチンでさらに処理が必要な場合、 *ControllerControl*ルーチンを返す必要があります**KeepObject**します。

    たとえば、ドライバーは、転送操作のディスク コント ローラーのプログラムが、転送が完了するまで、IRP を完了することはできません、 *ControllerControl*ルーチンを返す必要があります**KeepObject**します。

ときに、 *ControllerControl*ルーチンを返します**KeepObject**、デバイスが割り込み、ときに、ドライバーの ISR が通常実行し、その[ *DpcForIsr* 。](https://msdn.microsoft.com/library/windows/hardware/ff544079)または[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)ルーチンでは、I/O 操作と対象のデバイス オブジェクトの現在の IRP が完了するとします。

たびに、 *ControllerControl*ルーチンを返します**KeepObject**、IRP を完了するルーチンを呼び出す必要があります[ **IoFreeController** ](https://msdn.microsoft.com/library/windows/hardware/ff549104). このようなドライバーのルーチンを呼び出す必要があります**IoFreeController**次のデバイスの I/O 操作をすぐ設定できるように、できるだけ早くします。

 

 



