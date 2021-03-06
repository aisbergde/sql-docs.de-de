---
title: Unterstützung des JDBC-Treibers für Hochverfügbarkeit und Notfallwiederherstellung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 62de4be6-b027-427d-a7e5-352960e42877
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a959292b7adc2b5bb547d447f67f2a392de8af4c
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027956"
---
# <a name="jdbc-driver-support-for-high-availability-disaster-recovery"></a>JDBC-Treiber-Unterstützung für hohe Verfügbarkeit, Notfallwiederherstellung
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  In diesem Artikel wird die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]-Unterstützung für Hochverfügbarkeit und Notfallwiederherstellung ([!INCLUDE[ssHADR](../../includes/sshadr_md.md)]) thematisiert. Weitere Informationen über [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]finden Sie in der [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] -Onlinedokumentation.  
  
 Ab Version 4.0 von [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] können Sie den Verfügbarkeitsgruppenlistener einer Verfügbarkeitsgruppe (Hochverfügbarkeit, Notfallwiederherstellung) in der Verbindungseigenschaft angeben. Wenn eine [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]-Anwendung mit einer Always On-Datenbank verbunden ist, für die ein Failover ausgeführt wird, wird die ursprüngliche Verbindung unterbrochen, und die Anwendung muss eine neue Verbindung öffnen, damit ihre Ausführung nach dem Failover fortgesetzt werden kann. Die folgenden [Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md) wurden in [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] eingeführt:  
  
-   **multiSubnetFailover**  
  
-   **applicationIntent**
 
Geben Sie immer „multiSubnetFailover=true“ an, wenn Sie eine Verbindung mit dem Verfügbarkeitsgruppenlistener einer Verfügbarkeitsgruppe oder einer Failoverclusterinstanz herstellen. Beachten Sie, dass **multisubnetfailover** standardmäßig "false" ist. Verwenden Sie **applicationintent** , um den Typ der Anwendungs Arbeitsauslastung zu deklarieren. Weitere Informationen finden Sie in den nachfolgenden Abschnitten.
 
Ab Version 6,0 des Microsoft JDBC-Treibers für SQL Server wird eine neue Verbindungs Eigenschaft " **transparentnetworkipresolution** " (tnir) für eine transparente Verbindung mit Always on-Verfügbarkeitsgruppen oder einem Server mit mehreren IP-Adressen hinzugefügt. ierter. Wenn **transparentnetworkipresolution** den Wert true hat, versucht der Treiber, eine Verbindung mit der ersten verfügbaren IP-Adresse herzustellen. Wenn beim ersten Versuch ein Fehler auftritt, versucht der Treiber, eine parallele Verbindung mit allen IP-Adressen herzustellen, bis das Timeout abläuft, wobei alle ausstehenden Verbindungsversuche verworfen werden, wenn einer dieser Versuche erfolgreich ist.   

Beachten Sie Folgendes:
* transparentnetworkipresolution ist standardmäßig auf "true" fest.
* "transparentnetworkipresolution" wird ignoriert, wenn multisubnetfailover "true" ist.
* transparentnetworkipresolution wird ignoriert, wenn die Daten Bank Spiegelung verwendet wird.
* "transparentnetworkipresolution" wird ignoriert, wenn mehr als 64 IP-Adressen vorhanden sind.
* Wenn transparentnetworkipresolution auf true festgelegt ist, wird für den ersten Verbindungsversuch ein Timeout Wert von 500 ms verwendet. Der Rest der Verbindungsversuche folgt der gleichen Logik wie im multisubnetfailover-Feature. 

> [!NOTE]
> Wenn Sie den [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Microsoft JDBC-Treiber 4,2 (oder niedriger) für SQL Server verwenden und **multisubnetfailover** false ist, versucht, eine Verbindung mit der ersten IP-Adresse herzustellen. Wenn [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] keine Verbindung mit der ersten IP-Adresse herstellen kann, tritt ein Verbindungsfehler auf. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] versucht nicht, eine Verbindung mit einer der nachfolgenden IP-Adressen herzustellen, die dem Server zugeordnet sind. 
> 
> 
> [!NOTE]
>  Das Erhöhen des Verbindungstimeouts sowie die Implementierung von Verbindungswiederholungslogik erhöhen die Wahrscheinlichkeit, dass eine Anwendung eine Verbindung zu einer Verfügbarkeitsgruppe herstellt. Da zudem eine Verbindung aufgrund eines Verfügbarkeitsgruppenfailovers fehlschlagen kann, empfiehlt sich die Implementierung von Verbindungswiederholungslogik, wodurch im Fall einer fehlgeschlagenen Verbindung bis zur erneuten Verbindung Wiederholungsversuche erfolgen.  
  
 
  
## <a name="connecting-with-multisubnetfailover"></a>Verbinden mit multiSubnetFailover  
 Geben Sie immer **multiSubnetFailover=true** an, wenn Sie eine Verbindung mit dem Verfügbarkeitsgruppenlistener einer [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]-Verfügbarkeitsgruppe oder einer [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]-Failoverclusterinstanz herstellen. **multiSubnetFailover** ermöglicht einen schnelleren Failover für alle Verfügbarkeitsgruppen und Failoverclusterinstanzen in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und verringert die Failoverzeit für Always On-Topologien mit einem oder mehreren Subnetzen deutlich. Während eines Multisubnetzfailovers versucht der Client Verbindungen parallel. Während eines Subnetz-Failovers unternimmt [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] aggressive Wiederholungsversuche zum Herstellen der TCP-Verbindung.  
  
 Die **multiSubnetFailover**-Verbindungseigenschaft gibt an, dass die Anwendung in einer Verfügbarkeitsgruppe oder einer Failoverclusterinstanz bereitgestellt wird und [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] versucht, eine Verbindung mit der Datenbank auf der primären [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz herzustellen, indem mit allen IP-Adressen der Verfügbarkeitsgruppe Verbindungsversuche unternommen werden. Wenn **MultiSubnetFailover=true** für eine Verbindung angegeben wird, wiederholt der Client TCP-Verbindungsversuche schneller als dies bei den standardmäßigen TCP-Neuübertragungsintervallen des Betriebssystems der Fall ist. Auf diese Weise kann die Verbindung nach einem Failover einer AlwaysOn-Verfügbarkeitsgruppe oder einer AlwaysOn-Failoverclusterinstanz schneller wiederhergestellt werden. Diese Einstellung gilt sowohl für Einzelsubnetz- als auch Multisubnetz-Verfügbarkeitsgruppen und -Failoverclusterinstanzen.  
  
 Weitere Informationen zu Verbindungs Zeichenfolgen-Schlüssel [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]Wörtern in finden Sie unter [Festlegen der Verbindungs Eigenschaften](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Das Angeben von **multiSubnetFailover=true** für ein anderes Verbindungsziel als einen Verfügbarkeitsgruppenlistener oder eine Failoverclusterinstanz kann die Leistung beeinträchtigen und wird nicht unterstützt.  
  
 Wenn der Sicherheits-Manager nicht installiert ist, werden virtuelle IP-Adressen (VIPs) von der Java Virtual Machine für einen begrenzten Zeitraum zwischengespeichert. Die jeweilige Dauer wird durch Ihre JDK-Implementierung und die Java-Eigenschaften networkaddress.cache.ttl und networkaddress.cache.negative.ttl bestimmt. Wenn der JDK-Sicherheits-Manager installiert ist, werden VIPs von der Java Virtual Machine zwischengespeichert, und der Cache wird standardmäßig nicht aktualisiert. Es empfiehlt sich die Gültigkeitsdauer, d. h. "time-to-live" (networkaddress.cache.ttl), für den Cache der Java Virtual Machine auf einen Tag festzulegen. Wenn Sie den Standardwert nicht auf einen Tag oder eine ähnliche Einstellung festlegen, wird der alte Wert beim Hinzufügen oder Aktualisieren einer VIP nicht aus dem Java Virtual Machine-Cache gelöscht. Weitere Informationen zu networkAddress. Cache. TTL und networkAddress. Cache. negative. TTL finden [https://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html](https://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html)Sie unter.  
  
 Befolgen Sie beim Herstellen einer Verbindung mit einem Server in einer Verfügbarkeitsgruppe oder einer Failoverclusterinstanz die folgenden Richtlinien:  
  
-   Der Treiber generiert einen Fehler, wenn die **instanceName** -Verbindungs Eigenschaft in derselben Verbindungs Zeichenfolge wie die **multisubnetfailover** -Verbindungs Eigenschaft verwendet wird. Dies spiegelt den Umstand wider, dass der SQL Browser-Dienst in Verfügbarkeitsgruppen nicht verwendet wird. Wenn jedoch die **PortNumber** -Verbindungs Eigenschaft ebenfalls angegeben wird, ignoriert der Treiber **instanceName** und verwendet **PortNumber**.  
  
-   Verwenden Sie die **multiSubnetFailover**-Verbindungseigenschaft, wenn Sie eine Verbindung mit einem oder mehreren Subnetzen herstellen. Dadurch wird die Leistung auf beiden Seiten verbessert.  
  
-   Um eine Verbindung mit einer Verfügbarkeitsgruppe herzustellen, geben Sie in der Verbindungszeichenfolge den Verfügbarkeitsgruppenlistener der Verfügbarkeitsgruppe als Server an. Beispiel: jdbc:sqlserver://VNN1.  
  
-   Ein Verbindungsversuch mit einer mit mehr als 64 IP-Adressen konfigurierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz verursacht einen Verbindungsfehler.  
  
-   Das Verhalten einer Anwendung, die die **multiSubnetFailover** -Verbindungseigenschaft verwendet, wird nicht vom Authentifizierungstyp beeinflusst: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung, Kerberos-Authentifizierung oder Windows-Authentifizierung.  
  
-   Erhöhen Sie den Wert von **loginTimeout**, um die Failoverzeit zu berücksichtigen und Wiederholungsversuche für Anwendungsverbindungen zu reduzieren.  
  
-   Verteilte Transaktionen werden nicht unterstützt.  
  
 Wenn das schreibgeschützte Routing nicht aktiviert ist, scheitert das Herstellen der Verbindung mit einem sekundären Replikatspeicherort in einer Verfügbarkeitsgruppe in den folgenden Situationen:  
  
1.  Wenn der sekundäre Replikatspeicherort nicht zum Akzeptieren von Verbindungen konfiguriert ist.  
  
2.  Wenn eine Anwendung **applicationIntent=ReadWrite** verwendet (weiter unten erläutert) und der sekundäre Replikatspeicherort für schreibgeschützten Zugriff konfiguriert ist  
  
 Es kann keine Verbindung hergestellt werden, wenn ein primäres Replikat so konfiguriert ist, dass schreibgeschützte Arbeitslasten abgelehnt werden, und die Verbindungszeichenfolge **ApplicationIntent=ReadOnly**enthält.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Aktualisieren zur Verwendung von Multisubnetzclustern aus Datenbankspiegelung  
 Wenn Sie eine [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]-Anwendung aktualisieren, die derzeit Datenbankspiegelung in einem Multisubnetz-Szenario verwendet, müssen Sie die **failoverPartner** -Verbindungseigenschaft entfernen und durch **multiSubnetFailover** festgelegt auf **TRUE** ersetzen sowie den Servernamen in der Verbindungszeichenfolge durch einen Verfügbarkeitsgruppenlistener ersetzen. Wenn eine Verbindungszeichenfolge **failoverPartner** und **multiSubnetFailover=true** verwendet, generiert der Treiber einen Fehler. Wenn eine Verbindungszeichenfolge jedoch **failoverPartner** und **multiSubnetFailover=false** (oder **ApplicationIntent=ReadWrite**) verwendet, greift die Anwendung auf Datenbankspiegelung zurück.  
  
 Der Treiber gibt einen Fehler zurück, wenn die Datenbankspiegelung in der primären Datenbank in der Verfügbarkeitsgruppe und **multiSubnetFailover=true** in der Verbindungszeichenfolge verwendet werden, die anstatt mit einem Verfügbarkeitsgruppenlistener eine Verbindung mit einer primären Datenbank herstellt.  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="new-methods-supporting-multisubnetfailover-and-applicationintent"></a>Neue Methoden, die multiSubnetFailover und applicationIntent unterstützen  
 Mit den folgenden Methoden erhalten Sie programmgesteuerten Zugriff auf die Verbindungs Zeichenfolgen-Schlüsselwörter **multisubnetfailover**, **applicationintent** und **transparentnetworkipresolution** :  
  
-   [SQLServerDataSource.getApplicationIntent](../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setApplicationIntent](../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.getMultiSubnetFailover](../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setMultiSubnetFailover](../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDriver.getPropertyInfo](../../connect/jdbc/reference/getpropertyinfo-method-sqlserverdriver.md)  

-   SQLServerDataSource.setTransparentNetworkIPResolution

-   SQLServerDataSource.getTransparentNetworkIPResolution
  
 Die Methoden **getmultisubnetfailover**, **setmultisubnetfailover**, **getapplicationintent**, **setapplicationintent**, **gettransparentnetworkipresolution** und **settransparentnetworkipresolution** sind wird auch der [SQLServerDataSource-Klasse](../../connect/jdbc/reference/sqlserverdatasource-class.md), der [SQLServerConnectionPoolDataSource-Klasse](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)und der [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md)-Klasse hinzugefügt.  
  
## <a name="ssl-certificate-validation"></a>SSL-Zertifikatüberprüfung  
 Eine Verfügbarkeitsgruppe besteht aus mehreren physischen Servern. In [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] wird die Unterstützung von **alternativen Antragstellernamen** in SSL-Zertifikaten eingeführt, sodass einem Zertifikat mehrere Hosts zugeordnet werden können. Weitere Informationen zu SSL finden Sie Untergrund Legendes zur [SSL-Unterstützung](../../connect/jdbc/understanding-ssl-support.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verbinden mit SQL Server mit dem JDBC-Treiber](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)   
 [Festlegen von Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md)  
  
  
