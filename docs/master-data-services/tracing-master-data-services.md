---
title: Ablaufverfolgung (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 45823fc8-723a-49f2-9a11-94d241245cfd
author: lrtoyou1223
ms.author: lle
manager: erikre
ms.openlocfilehash: d1c438eff7f3543b22fc2c0e4e2a7264cd1a91ee
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263981"
---
# <a name="tracing-master-data-services"></a>Ablaufverfolgung (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Die Datei "Web.config" enthält einen Ablaufverfolgungsabschnitt, wie unten dargestellt. Dieser Abschnitt ist neu in . [!INCLUDE[ssSQL15](../includes/sssql15-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]  
  
```  
<sources>  
      <!-- Adjust the switch value to control the types of messages that should be logged.   
           https://msdn.microsoft.com/library/system.diagnostics.sourcelevels  
           Use the a switchValue of Verbose to generate a full log. Please be aware that   
           the trace file can get quite large very quickly -->  
      <source name="MDS" switchType="System.Diagnostics.SourceSwitch" switchValue="Warning, ActivityTracing">  
        <listeners>  
          <!-- Set a directory path where the service account you chose while setting up Master Data Services has read and write privileges.  
               Default path is Logs in WebApplication folder, for example C:\Program Files\Microsoft SQL Server\130\Master Data Services\WebApplication  
               New log file will be created every day or every 10 mb.  
               When directory size hits the 200mb limitation, the oldest file will be deleted.-->  
          <add name="FileTraceListener"  
               type="Microsoft.MasterDataServices.Core.Logging.FileTraceListener, Microsoft.MasterDataServices.Core"   
               initializeData="DirectoryPath = Logs; FileSizeInMb = 10; MaxDirectorySizeInMb = 200"/>  
          <remove name="Default"/>  
        </listeners>  
      </source>  
    </sources>  
  
```  
  
 Folgendes Verhalten ist das Standardverhalten für die Ablaufverfolgung.  
  
-   Ablaufverfolgung wird für Warnungs- und ActivityTracing-Nachrichten aktiviert.  
  
     Weitere Informationen finden Sie unter [SourceLevels-Enumeration](https://msdn.microsoft.com/library/system.diagnostics.sourcelevels).  
  
-   Die Protokolle werden im Ordner "Logs" unter dem Ordner "WebApplication" gespeichert. Der Standardspeicherort ist "C:\Programme\Microsoft SQL Server\130\Master Data Services\WebApplication\Logs".  
  
-   Die Datei wird für jeden Tag oder für jeweils 10 MB erstellt.  
  
-   Wenn die Größe 200 MB erreicht, wird das älteste Protokoll gelöscht.  
  
-   Das Protokollformat ist CSV. In der folgenden Tabelle wird das Protokollformat beschrieben.  
  
    |Element|Beschreibung|  
    |-------------|-----------------|  
    |Uhrzeit|Zeitpunkt des Ablaufverfolgungseintrags.|  
    |CorrelationID|Eine Korrelations-ID wird für jede Anforderung zugewiesen. Alle Ablaufverfolgungen, die durch diese Anforderung ausgelöst werden, haben die gleiche Korrelations-ID.<br /><br /> Tritt ein Fehler in der Benutzeroberfläche auf, wird die Korrelations-ID in der Fehlermeldung angezeigt.|  
    |Vorgang|Vorgangsname anfordern. Wenn die Anforderung eine Web-UI-Anforderung ist, ist der Vorgangsname die URL. Wenn die Anforderung eine API-Anforderung ist, ist der Vorgangsname der Dienstname.|  
    |Ebene|Ebene dieses Ablaufverfolgungseintrags.|  
    |Meldung|Nachrichtentext der Ablaufverfolgung|  
  
## <a name="external-resources"></a>Externe Ressourcen  
 Blogbeitrag [Troubleshooting Logging Improvement](https://go.microsoft.com/fwlink/p/?LinkId=615377)(Problembehandlung der Protokollierungsverbesserung) auf msdn.com.  
  
  
