---
title: IServerVirtualDevice::CloseDevice
titlesuffix: SQL Server VDI reference
description: In diesem Artikel erhalten Sie Referenzinformationen zum Befehl „IServerVirtualDevice::CloseDevice“.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: c73649e2a4301e94f8e68504222cc0122061f25f
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847431"
---
# <a name="iservervirtualdeviceclosedevice-vdi"></a>IServerVirtualDevice::CloseDevice (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Mit der Funktion **CloseDevice** wird ein virtuelles Gerät geschlossen, das mit „IServerVirtualDeviceSet2::OpenDevice“ geöffnet wurde.

## <a name="syntax"></a>Syntax

```c
HRESULT IServerVirtualDevice::CloseDevice ();
```

## <a name="return-value"></a>Rückgabewert

|Rückgabewert | Erklärung |
|---|---|
| VD_E_CLOSE | Das Gerät ist bereits geschlossen. |
| VD_E_ABORT | Die Schnittstelle befindet sich im Zustand „Abbruch“. |

## <a name="remarks"></a>Remarks

Wurde „SignalAbort“ zum Erzwingen einer unplanmäßigen Beendigung verwendet, ist die Verwendung von „CloseDevice“ nicht mehr erforderlich. Wenn „CloseDevice“ nach der Verwendung von „SignalAbort“ aufgerufen wird, wird keine Aktion ausgeführt.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen finden Sie in der [Referenz zur Schnittstelle für virtuelle Geräte in SQL Server](reference-virtual-device-interface.md).