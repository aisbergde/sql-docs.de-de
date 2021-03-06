---
title: PowerPivot-Konfiguration, die mithilfe von Windows PowerShell | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4d83e53e-04f1-417d-9039-d9e81ae0483d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1b57ea1f69933d4d2c73ec12cc4cc18ff86d112d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071302"
---
# <a name="powerpivot-configuration-using-windows-powershell"></a>PowerPivot-Konfiguration mit Windows PowerShell
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] enthält Windows PowerShell-Cmdlets, mit denen Sie eine Installation von [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]konfigurieren können. Für die vollständige Konfiguration einer Installation mit PowerShell ist die Verwendung von SharePoint-Cmdlets und PowerPivot für SharePoint-Cmdlets erforderlich. Ein Großteil der Konfiguration kann mithilfe eines der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Tools ausgeführt werden. Weitere Informationen zu den Tools finden Sie unter [PowerPivot-Konfigurationstools](power-pivot-configuration-tools.md).  
  
> [!IMPORTANT]  
>  Für eine SharePoint 2010-Farm muss SharePoint 2010 SP1 installiert sein, bevor Sie PowerPivot für SharePoint oder eine SharePoint-Farm konfigurieren können, die einen [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]"-Datenbankserver verwendet. Wenn Sie das Service Pack noch nicht installiert haben, installieren Sie es, bevor Sie mit der Serverkonfiguration beginnen.  
  
## <a name="benefits-of-configuring-powerpivot-for-sharepoint-using-powershell"></a>Vorteile der Konfiguration von PowerPivot für SharePoint mithilfe von PowerShell  
 Sie können Windows PowerShell-Skriptdateien (.ps1) erstellen, um Konfigurationstasks zu automatisieren. Dieser Ansatz wird empfohlen, wenn Sie skriptbasierte Installation und Konfigurationsschritte benötigen, die Sie auf jedem Server ausführen können. Sie benötigen ein solches Skript möglicherweise als Teil eines Notfallwiederherstellungsplans zum Neuerstellen eines Servers im Fall eines Hardwarefehlers.  
  
## <a name="view-a-list-of-the-powerpivot-cmdlets-on-a-server"></a>Anzeigen einer Liste der PowerPivot-Cmdlets auf einem Server  
 Um die Inhalte und Beispiele finden Sie unter den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Cmdlets finden Sie in [PowerShell-Referenz für PowerPivot für SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint).  
  
 So zeigen Sie mithilfe von PowerShell eine Liste der PowerPivot-Cmdlets an  
  
1.  Öffnen Sie die SharePoint-Verwaltungsshell unter Verwendung der Option **Als Administrator ausführen** .  
  
2.  Geben Sie den folgenden Befehl ein:  
  
    ```  
    Get-help *powerpivot*  
    ```  
  
     Eine Liste von Cmdlets sollte angezeigt werden, die im Cmdlet-Namen PowerPivot enthalten. Beispiel: `Get-PowerPivotServiceApplication`. Wie viele Cmdlets verfügbar sind, hängt von der verwendeten Analysis Services-Version ab.  
  
    -   10 Cmdlets mit SQL Server 2012 SP1 Analysis Services-Server, der im SharePoint-Modus konfiguriert ist, und SharePoint 2013. Die 2012 SP1-Version verwendet eine neue Architektur, die die Ausführung des Analysis-Servers außerhalb der SharePoint-Farm zulässt und weniger Windows PowerShell-Cmdlets für die Verwaltung erfordert.  
  
    -   17 Cmdlets mit SQL Server 2012 Analysis Services-Server, der im SharePoint-Modus konfiguriert ist, und SharePoint 2010.  
  
     Wenn keine Befehle in der Liste zurückgegeben werden, oder Sie eine Fehlermeldung ähnlich wie sehen "`get-help could not find *powerpivot* in a help file in this session.`", finden Sie im nächsten Abschnitt dieses Themas Anweisungen zum Aktivieren der PowerPivot-Cmdlets auf dem Server.  
  
     Alle Cmdlets verfügen über eine Onlinehilfe. Im folgenden Beispiel wird erläutert, wie die Onlinehilfe für das `New-PowerPivotServiceApplication`-Cmdlet angezeigt wird:  
  
    ```  
    Get-help new-powerpivotserviceapplication -full  
    ```  
  
     Oder verwenden Sie die folgende Syntax, um nur die Beispiele anzuzeigen:  
  
    ```  
    Get-help new-powerpivotserviceapplication -example  
    ```  
  
## <a name="enable-powerpivot-cmdlets-on-a-server"></a>Aktivieren der PowerPivot-Cmdlets auf einem Server  
 PowerPivot-Cmdlets sind verfügbar, nachdem Sie PowerPivot für SharePoint installiert und die Farmlösung bereitgestellt haben. Die Lösungen werden bereitgestellt, wenn Sie das PowerPivot-Konfigurationstool ausführen. Führen Sie folgende Schritte aus, um die Verwendung von Cmdlets zu aktivieren:  
  
1.  Öffnen Sie die SharePoint-Verwaltungsshell unter Verwendung der Option **Als Administrator ausführen** .  
  
2.  Führen Sie das erste Cmdlet aus:  
  
    ```  
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     Das Cmdlet gibt den Namen der Lösung, deren Lösungs-ID und "Deployed=False" zurück. Im nächsten Schritt wird die Lösung bereitgestellt.  
  
3.  Führen Sie das zweite Cmdlet aus, um die Lösung bereitzustellen:  
  
    ```  
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
4.  Schließen Sie das Fenster. Öffnen Sie es erneut mit der Option **Als Administrator ausführen** .  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [PowerPivot-Serververwaltung und -konfiguration in der Zentraladministration](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [PowerPivot-Konfigurationstools](power-pivot-configuration-tools.md)  
  
 [PowerShell-Referenz für PowerPivot für SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
  
  
