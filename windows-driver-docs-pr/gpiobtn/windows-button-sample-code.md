---
title: Windows ボタンのサンプル コード
description: このトピックには、特定の Windows ボタンを切り替えるためのコード サンプルが含まれています。 ダウンおよびそれ以降。
ms.assetid: DB43A64C-66A0-43BD-A657-D4EE11159543
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d9cec035e2cf84bbe8fd01c0281e1b8ba30ba6b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553019"
---
# <a name="windows-button-sample-code"></a>Windows ボタンのサンプル コード


このトピックには、特定の Windows ボタンを切り替えるためのコード サンプルが含まれています。 ダウンおよびそれ以降。

```cpp
int __cdecl InjectButtonPress(
    __in int argc,
    __in_ecount(argc) char **argv)
{
    LPWSTR DevicePath;
    HANDLE FileHandle;
    BOOL b;
    BYTE buffer;
    HWND hwnd;
    MSG msg;

    DevicePath = GetDevicePath((LPGUID)&amp;GUID_GPIOBUTTONS_NOTIFY_INTERFACE);

    FileHandle = CreateFile(DevicePath,
                            GENERIC_WRITE,
                            0,
                            NULL,
                            OPEN_EXISTING,
                            0,
                            NULL);
   
    buffer = GPIO_BUTTON_WINDOWS; //using GPIOBUTTONS_BUTTON_TYPE enum defined above
    WriteFile(FileHandle, &amp;buffer, sizeof(buffer), NULL, NULL); // send button down
    buffer = GPIO_BUTTON_WINDOWS;
    WriteFile(FileHandle, &amp;buffer, sizeof(buffer), NULL, NULL); // send button up

    return 0;
}
```

 

 



