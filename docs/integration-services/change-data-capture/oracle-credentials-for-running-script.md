---
title: Oracle-Anmeldeinformationen zum Ausführen von Skripts | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4a301cb0-2f5b-41ba-81bf-46b41d07f137
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 66bb8f1853515f88fc43770fce2d36b767f23de3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096714"
---
# <a name="oracle-credentials-for-running-script"></a>Oracle Credentials for Running Script

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Um das ergänzende Oracle-Protokollierungsskript in der Oracle CDC Designer Console auszuführen, werden Sie vom Programm zum Angeben der Anmeldeinformationen des Oracle-Benutzers aufgefordert, der das Skript ausführt. Zum Ausführen dieses Skripts muss der Oracle-Benutzer über die ALTER TABLE-Berechtigung für alle zu erfassenden Tabellen und die SELECT-Berechtigung für die DBA_LOG_GROUPS-Sicht verfügen.  
  
## <a name="task-list"></a>Aufgabenliste  
 Geben Sie in diesem Dialogfeld Folgendes ein:  
  
 **Authentifizierung**  
  
 Wählen Sie eine der folgenden Optionen aus:  
  
-   **Windows-Authentifizierung:** Wählen Sie diese Option aus, um die aktuellen Anmeldeinformationen für die Windows-Domäne zu verwenden. Sie können diese Option nur verwenden, wenn die Oracle-Datenbank für die Nutzung der Windows-Authentifizierung konfiguriert ist.  
  
-   **Oracle-Authentifizierung:** Wenn Sie diese Option aktivieren, müssen Sie **Benutzername** und **Kennwort** für den Benutzer der Oracle-Quelldatenbank eingeben, mit der Sie eine Verbindung herstellen.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Verwalten einer CDC-Instanz](../../integration-services/change-data-capture/how-to-manage-a-cdc-instance.md)   
 [Überprüfen und Generieren ergänzender Protokollierungsskripts](../../integration-services/change-data-capture/review-and-generate-supplemental-logging-scripts.md)  
  
  
