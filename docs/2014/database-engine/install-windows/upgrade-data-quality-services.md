---
title: Aktualisieren von Data Quality Services | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f396666b-7754-4efc-9507-0fd114cc32d5
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9f1feb8292020b61d00705e662bda80d2b3af4eb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2018
ms.locfileid: "36058119"
---
# <a name="upgrade-data-quality-services"></a>Aktualisieren von Data Quality Services
  Dieses Thema enthält Informationen dazu, wie Sie die vorhandene Data Quality Services-Installation (DQS) auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2 aktualisieren. Während des Upgrades des Data Quality-Servers in DQS auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]muss auch das DQS-Datenbankschema aktualisiert werden.  
  
> [!IMPORTANT]  
>  -   Sie müssen die DQS-Datenbanken sichern, bevor Sie DQS aktualisieren, um versehentliche Datenverluste während des Schemaupgrades zu verhindern. Informationen zum Sichern von DQS-Datenbanken finden Sie unter [Backing Up and Restoring DQS Databases](../../data-quality-services/backing-up-and-restoring-dqs-databases.md).  
> -   Um eine Verbindung mit der [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Version des Data Quality-Servers herzustellen und Data Quality-Aufgaben auszuführen, können Sie die aktuelle oder eine frühere Version des Data Quality-Clients oder die [DQS-Bereinigungstransformation](../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md) in Integration Services verwenden.  
> -   Nachdem Data Quality Services und Master Data Services auf [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] CTP2 aktualisiert wurden, kann die [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1-Version des Master Data Services-Add-Ins für Excel weiterverwendet werden. Frühere Versionen des Master Data Services-Add-Ins für Excel sind nach einem Upgrade auf SQL Server 2014 CTP2 jedoch nicht funktionsfähig. Sie können die [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1-Version des Master Data Services Add-Ins für Excel aus [hier](http://go.microsoft.com/fwlink/?LinkId=328664).  
  
##  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Sie müssen als Mitglied der Administratorgruppe auf dem [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] -Computer angemeldet sein.  
  
-   Ihr Windows-Benutzerkonto muss Mitglied der festen Serverrolle sysadmin auf der SQL Server-Instanz sein, auf der der [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] installiert ist.  
  
##  <a name="Upgrade"></a> Aktualisieren von DQS  
 So aktualisieren Sie DQS  
  
1.  Sichern Sie die DQS-Datenbanken, bevor Sie den Upgradevorgang starten. Informationen zum Sichern von DQS-Datenbanken finden Sie unter [Backing Up and Restoring DQS Databases](../../data-quality-services/backing-up-and-restoring-dqs-databases.md).  
  
2.  Aktualisieren Sie die SQL Server-Instanz mit der DQS-Installation auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Führen Sie den [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Setup-Assistenten aus.  
  
    2.  Klicken Sie im linken Bereich auf **Installation**.  
  
    3.  Klicken Sie im rechten Bereich auf **Upgrade von SQL Server 2005, SQL Server 2008, SQL Server 2008 R2 oder SQL Server 2012**.  
  
    4.  Schließen Sie den Setup-Assistenten ab.  
  
        > [!NOTE]  
        >  Auf diese Weise wird die SQL Server-Instanz auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] aktualisiert. Außerdem wird der neueste Data Quality-Client installiert, wenn zuvor ein Data Quality-Client auf dem Computer installiert war. Wenn auf anderen Computern ein Data Quality-Client installiert ist, müssen Sie auf diesen Computern die Teilschritte unter Schritt 2 ausführen, um die aktuelle Version des Data Quality-Clients zu installieren. Der Setup-Assistent installiert die aktuelle Version neben der vorhandenen Version des Data Quality-Clients. Nachdem Sie das DQS-Datenbankschema aktualisiert haben, können Sie mit der aktuellen oder einer früheren Version des Data Quality-Clients eine Verbindung mit der [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Version des Data Quality-Servers herstellen.  
  
3.  Aktualisieren Sie das DQS-Datenbankschema.  
  
    1.  Starten Sie eine -Eingabeaufforderung als Administrator.  
  
    2.  Wechseln Sie an der Eingabeaufforderung zu dem Verzeichnis, in dem DQSInstaller.exe enthalten ist. Bei Verwendung der Standardinstanz von SQL Server steht die Datei DQSInstaller.exe unter C:\Programme\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn zur Verfügung:  
  
        ```  
        cd C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn  
        ```  
  
    3.  Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie die EINGABETASTE:  
  
        ```  
        dqsinstaller.exe -upgrade  
        ```  
  
    4.  Sie werden vom Installationsprogramm aufgefordert, die DQS-Datenbanken zu sichern, bevor Sie den Vorgang fortsetzen. Wenn Sie die DQS-Datenbanken bereits gesichert haben, geben Sie `Y` oder `Yes`, und drücken Sie dann die EINGABETASTE, um das Upgrade fortzusetzen.  
  
    5.  Nach dem erfolgreichen Upgrade des DQS-Datenbankschemas wird eine Abschlussmeldung angezeigt.  
  
##  <a name="Verify"></a> Überprüfen des Upgrades des DQS-Datenbankschemas  
 Um sicherzustellen, dass das DQS-Datenbankschema erfolgreich aktualisiert wurde, können Sie die aktuelle Version in den Datenbanken DQS_MAIN und DQS_PROJECTS überprüfen, indem Sie die A_DB_VERSION-Tabelle in der jeweiligen Datenbank abfragen. Gehen Sie folgendermaßen vor:  
  
1.  Starten Sie SQL Server Management Studio, und stellen Sie eine Verbindung mit der SQL Server-Instanz her, die das aktualisierte DQS-Datenbankschema enthält.  
  
2.  Führen Sie die folgende Abfrage aus:  
  
    ```  
    SELECT * FROM DQS_MAIN.dbo.A_DB_VERSION WHERE STATUS=2;  
    SELECT * FROM DQS_PROJECTS.dbo.A_DB_VERSION WHERE STATUS=2;  
    ```  
  
3.  In der Ausgabe wird ein Eintrag für jedes Upgrade zusammen mit dem Upgradedatum angezeigt. Der höchste VERSION_ID- und ASSEMBLY_VERSION-Wert zum letzten angegebenen Datum entspricht der aktuellen Version. Der Wert 2 in der STATUS-Spalte gibt die erfolgreiche Ausführung an. Falls ein Fehler aufgetreten ist, wird dieser in der ERROR-Spalte aufgeführt. Beispiel für eine Ausgabe:  
  
    |im Elementknoten &lt;Customer ID="1"|UPGRADE_DATE|VERSION_ID|ASSEMBLY_VERSION|USER_NAME|STATUS|Fehler|  
    |--------|-------------------|-----------------|-----------------------|----------------|------------|-----------|  
    |1000|2013-08-11 05:26:39.567|1200|11.0.3000.0|\<DOMÄNE\Benutzername>|2||  
    |1001|2013-09-19 15:09:37.750|1600|12.0.xxxx.0|\<DOMÄNE\Benutzername>|2||  
  
## <a name="see-also"></a>Siehe auch  
 [Installieren von Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Entfernen von Data Quality Server-Objekten](../../sql-server/install/remove-data-quality-server-objects.md)   
 [Upgrade auf SQL Server 2014](upgrade-sql-server.md)  
  
  