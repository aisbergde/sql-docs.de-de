---
title: Problembehandlung bei einer PowerPivot für SharePoint Installation | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 797405386e8a6c0b9e62328699f3a73a6d845313
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892446"
---
# <a name="troubleshoot-a-powerpivot-for-sharepoint-installation"></a>Problembehandlung für eine PowerPivot für SharePoint-Installation
  Wenn Sie anstelle der erwateten Seiten und Funktionen Fehler erhalten, gehen Sie wie folgt vor.  
  
-   Lesen Sie die Versionsanmerkungen zu SharePoint sowie [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , um Problemumgehungen für bekannte Installationsprobleme zu finden. Die Versionsanmerkungen werden mit den Installationsmedien sowie auf der Microsoft-Website bereitgestellt, von der Sie die Software heruntergeladen haben.  
  
    -   [Versionsanmerkungen zu SQL Server 2014](https://technet.microsoft.com/library/dn169381\(v=sql.15\).aspx).  
  
-   Weitere Informationen finden Sie im TechNet Wiki-Thema [Behandeln von Problemen mit PowerPivot-Installationen (und anderen Add-Ins)](https://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx).  
  
## <a name="issues"></a>Probleme  
  
### <a name="powerpivot-gallery-thumbnail-images-show-as-a-red-x"></a>Miniaturbilder werden im PowerPivot-Katalog als rotes X dargestellt  
 Eine Möglichkeit besteht darin, dass die **PowerPivot-Funktionsintegration für Websitesammlungen** nichtaktiv ist. Führen Sie folgende Schritte aus:  
  
1.  Klicken Sie in der Power Pivot-Katalog Bibliothek auf **Site Einstellungen** , entweder über ![SharePoint-Einstellungen](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "das Zahnrad Symbol SharePoint") -Einstellungen oder die Liste **Home** .  
  
2.  Klicken Sie im Abschnitt **Websitesammlungsverwaltung** auf **Websitesammlungs-Features**.  
  
3.  Klicken Sie auf **Websitesammlungs-Features**.  
  
4.  Stellen Sie sicher, dass die **PowerPivot-Funktionsintegration für Websitesammlungen** auf **Aktiv**festgelegt ist.  
  
 Weitere Informationen zu diesem Problem finden Sie unter [Power Pivot-Katalog zeigt rote X-Symbole für Symbole](https://support.microsoft.com/kb/2361559) (https://support.microsoft.com/kb/2361559).  
  
  
