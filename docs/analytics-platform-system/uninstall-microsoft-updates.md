---
title: Deinstallieren von Microsoft-Updates (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df61570a-210d-4154-822f-98acd721f075
caps.latest.revision: "19"
ms.openlocfilehash: c801918cbac5d0762384a0cd3adcca9ddf8f346a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="uninstall-microsoft-updates"></a>Deinstallieren von Microsoft-Updates
Dieses Thema beschreibt die Vorgehensweise beim Deinstallieren eines zuvor installierten Microsoft-Updates auf dem Gerät Analytics Platform System.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
  
### <a name="prerequisites"></a>Erforderliche Komponenten  
Um diese Schritte ausführen zu können, benötigen Sie Folgendes:  
  
-   Mit Berechtigungen zum Zugriff auf die Admin-Konsole zum Überwachen der Einheit Analytics Platform System anmelden.  
  
-   Kenntnisse über die Fabric-Domänenadministratorkonto zum Anmelden die  *<Fabric Domain>*  **-HST01** Knoten.  
  
## <a name="HowToUninstallMSFT"></a>So deinstallieren Sie Microsoft-updates  
  
1.  Melden Sie sich die  *<Fabric Domain>*  **-HST01** als Domänenadministrator Fabric-Knoten.  
  
2.  Um alle Updates zu deinstallieren, die für die WSUS für die Deinstallation genehmigt ist, öffnen Sie ein Eingabeaufforderungsfenster, und geben Sie den folgenden Befehl aus. Ersetzen Sie die Platzhalterelemente *< >* mit den entsprechenden Informationen.  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="see-also"></a>Siehe auch  
[Herunterladen und Anwenden von Microsoft Updates &#40; Analyseplattformsystem &#41;](download-and-apply-microsoft-updates.md)  
[Anwenden von Analytics Platform System Hotfixes &#40; Analyseplattformsystem &#41;](apply-analytics-platform-system-hotfixes.md)  
[Vorgehensweise: Deinstallieren Sie Analytics Platform System Hotfixes &#40; Analyseplattformsystem &#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Wartung von Software &#40; Analyseplattformsystem &#41;](software-servicing.md)  
  