---
title: Erstellen von Proxyklassen für den Master Data Manager-Webdienst | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 8bdab026-a0c0-41f3-9d36-f3919c23247f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c44e1830b1f04b1a7686bf7db1efea4549ae143e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479557"
---
# <a name="create-master-data-manager-web-service-proxy-classes"></a>Erstellen von Proxyklassen für den Master Data Manager-Webdienst
  Der [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] -Webdienst ermöglicht die programmgesteuerte Verwendung der Funktionen von [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] an jedem Computer, der auf die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] -Website zugreifen kann. Vor dem Schreiben des Codes für den Zugriff auf den Webdienst sind Proxyklassen zu erstellen. Die Hauptproxyklasse, mit der Sie Webdienstvorgänge ausführen, ist die <xref:Microsoft.MasterDataServices.ServiceClient>-Klasse, welche die <xref:Microsoft.MasterDataServices.IService>-Schnittstelle implementiert.  
  
## <a name="enable-web-service-metadata-publishing"></a>Aktivieren der Veröffentlichung von Webdienst-Metadaten  
 Bevor Sie Proxyklassen generieren können, ist die Veröffentlichung der Webdienst-Metadaten zu aktivieren. Gehen Sie dazu folgendermaßen vor:  
  
1.  Öffnen Sie die Datei „Web.config“ von [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] in einem Text-Editor. Diese Datei befindet sich im Ordner "WebApplication" des [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]-Installationspfads.  
  
2.  Suchen der `mdsWsHttpBehavior` unter Abschnitt  **\<ServiceBehaviors >** . Für die  **\<ServiceMetadata >** -Elementgruppe, `httpGetEnabled` zu `true`.  
  
    > [!NOTE]  
    >  Wenn Sie Webdienste über Secure Sockets Layer (SSL) aktivieren möchten, legen Sie im Abschnitt `httpsGetEnabled` der Datei web.config `true` auf `mdsWsHttpBehavior` fest. Sie müssen außerdem `mdsWsHTTPBinding` ändern, damit auch hier eine Konfiguration für SSL vorliegt, und den Nicht-SSL-Abschnitt auskommentieren.  
  
3.  Speichern Sie die an der Datei vorgenommenen Änderungen.  
  
4.  Testen Sie die Metadaten-Veröffentlichung durch Navigieren zur Dienst-URL, beispielsweise: http://yourserver/MDS/service/service.svc. Ist die Metadaten-Veröffentlichung aktiviert, wird eine Seite angezeigt. Diese beginnt mit:   
    „You have created a service.“ (Sie haben einen Dienst erstellt.)  
  
## <a name="creating-proxy-classes-by-using-visual-studio"></a>Erstellen von Proxyklassen mit Visual Studio  
 Ist Visual Studio 2010 installiert, lassen sich Proxyklassen am einfachsten durch das Hinzufügen eines **Dienstverweises** zum Projekt erstellen. Die Adresse des Dienstverweises ist die URL der [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]-Webanwendung, wobei "/service/service.svc" angefügt wird. Beispiel: http://yourserver/MDS/service/service.svc. Weitere Informationen finden Sie unter [Vorgehensweise: Hinzufügen, aktualisieren oder Entfernen eines Dienstverweises](https://go.microsoft.com/fwlink/?LinkId=221167).  
  
## <a name="creating-proxy-classes-by-using-svcutilexe"></a>Erstellen von Proxyklassen mit "Svcutil.exe"  
 Damit „Svcutil.exe“ auf dem Computer verfügbar ist, muss [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] oder das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows SDK installiert sein. Wenn Sie [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] verwenden, müssen Sie den Befehl über die [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]-Eingabeaufforderung ausführen. Weitere Informationen finden Sie unter [ServiceModel Metadata Utility-Tool (Svcutil.exe)](https://go.microsoft.com/fwlink/?LinkId=165027) und [Generieren eines WCF-Clients aus Dienstmetadaten](https://go.microsoft.com/fwlink/?LinkId=164821).  
  
 Verwenden Sie zum Erstellen mehrerer C#-Proxyklassen mit "Svcutil.exe" einen Befehl wie folgt:  
  
```  
svcutil.exe http://<server_name:port>/<virtual_path>/Service/Service.svc   
/out:<proxy_name>.cs /messageContract /tcv:Version35   
/noconfig /ct:System.Collections.ObjectModel.Collection`1   
/namespace:*,Microsoft.MasterDataServices  
```  
  
 Erläuterungen:  
  
-   *servername*:*port* entspricht dem Computernamen und der Portnummer des Computers, auf dem [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] gehostet wird.  
  
-   *virtual_path* ist der virtuelle Pfad von [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] in den Internetinformationsdiensten (IIS).  
  
-   *proxy_name* ist der Name für die generierte Proxydatei.  
  
## <a name="see-also"></a>Siehe auch  
 [Kategorisierte Webdienstvorgänge &#40;Master Data Services&#41;](categorized-web-service-operations-master-data-services.md)  
  
  
