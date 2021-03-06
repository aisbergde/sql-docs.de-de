---
title: Wideworldimporters OLTP-Daten Bank Katalog-SQL | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2560043ca6acc4b5df141bcbc898ac09b21f97a8
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811530"
---
# <a name="wideworldimporters-database-catalog"></a>Wideworldimporters-Daten Bank Katalog
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Die Datenbank "wideworldimporters" enthält alle Transaktionsinformationen und täglichen Daten für Verkäufe und Einkäufe sowie Sensordaten für Fahrzeuge und kalte Räume.

## <a name="schemas"></a>Schemas

Wideworldimporters verwendet Schemas für verschiedene Zwecke, z. b. das Speichern von Daten, das definieren, wie Benutzer auf die Daten zugreifen können, und das Bereitstellen von Objekten für die Data Warehouse Entwicklung und Integration.

### <a name="data-schemas"></a>Daten Schemas

Diese Schemas enthalten die Daten. Eine Reihe von Tabellen werden von allen anderen Schemas benötigt und befinden sich im Anwendungsschema.

|Schema|Beschreibung|
|-----------------------------|---------------------|
|Application|Anwendungs weite Benutzer, Kontakte und Parameter. Dies enthält auch Verweis Tabellen mit Daten, die von mehreren Schemas verwendet werden.|
|Purchasing|Bestands Artikel Käufe von Lieferanten und Details zu Zulieferern.|  
|Sales|Bestands Element Verkäufe bei Einzelhandelskunden und Details zu Kunden und Vertriebsmitarbeitern. |  
|Warehouse|Inventur und Transaktionen von Aktien Elementen.|  

### <a name="secure-access-schemas"></a>Sichere Zugriffs Schemas

Diese Schemas werden für externe Anwendungen verwendet, die nicht direkt auf die Datentabellen zugreifen dürfen. Sie enthalten Sichten und gespeicherte Prozeduren, die von externen Anwendungen verwendet werden.

|Schema|Beschreibung|
|-----------------------------|---------------------|
|Website|Der gesamte Zugriff auf die Datenbank von der Unternehmenswebsite erfolgt über dieses Schema.|
|Berichte|Der gesamte Zugriff auf die Datenbank aus Reporting Services Berichten erfolgt über dieses Schema.|
|PowerBI|Der gesamte Zugriff auf die Datenbank aus den Power BI Dashboards über das Enterprise-Gateway erfolgt über dieses Schema.|

Beachten Sie, dass die Berichte und die powerbi-Schemas in der ersten Version der-Beispieldatenbank nicht verwendet werden. Alle Reporting Services-und Power BI Beispiele, die auf dieser Datenbank basieren, werden jedoch empfohlen, diese Schemas zu verwenden.

### <a name="development-schemas"></a>Entwicklungs Schemas

Sonderschemas

|Schema|Beschreibung|
|-----------------------------|---------------------|
|Integration|Für Data Warehouse Integration erforderliche Objekte und Prozeduren (d. h. die Daten werden in die wideworldimportersdw-Datenbank migriert).|
|Sequenzen|Enthält Sequenzen, die von allen Tabellen in der Anwendung verwendet werden.|

## <a name="tables"></a>Tabellen

Alle Tabellen in der Datenbank befinden sich in den Daten Schemas.

### <a name="application-schema"></a>Anwendungs Schema

Details zu Parametern und Personen (Benutzer und Kontakte) zusammen mit allgemeinen Verweis Tabellen (gemeinsame Verwendung mehrerer anderer Schemas).

|Tabelle|Beschreibung|
|-----------------------------|---------------------|
|SystemParameters|Enthält systemweite konfigurierbare Parameter.|
|Personen|Enthält Benutzernamen, Kontaktinformationen, für alle Benutzer, die die Anwendung verwenden, und für die Personen, mit denen sich die weltweiten Importierer bei Kundenorganisationen beschäftigt. Dazu zählen Mitarbeiter, Kunden, Lieferanten und andere Kontakte. Für Personen, denen die Berechtigung erteilt wurde, das System oder die Website zu verwenden, enthält die Informationen Anmelde Informationen.|
|Städte|Im System werden viele Adressen gespeichert, für Personen, Lieferadressen der Kundenorganisation, Abhol Adressen bei Lieferanten usw. Wenn eine Adresse gespeichert wird, gibt es einen Verweis auf eine Stadt in dieser Tabelle. Es gibt auch einen räumlichen Standort für jede Stadt.|
|StateProvinces|Städte sind Teil der Bundesstaaten oder Provinzen. Diese Tabelle enthält Details zu diesen, einschließlich räumlicher Daten, die die Grenzen der einzelnen Bundesstaaten oder Provinzen beschreiben.|
|Länder|Staaten oder Provinzen sind Teil der Länder. Diese Tabelle enthält Details zu diesen, einschließlich räumlicher Daten, die die Grenzen der einzelnen Länder beschreiben.|
|DeliveryMethods|Auswahlmöglichkeiten für die Bereitstellung von Aktien Elementen (z. b. LKW/van, Post, Pickup, Courier usw.)|
|Paymentmethods|Auswahlmöglichkeiten für Zahlungen (z. b. Bargeld, Überprüfung, EFT usw.)|
|TransactionTypes|Typen von Kunden-, Lieferanten-oder Aktientransaktionen (z. b. Rechnung, Gutschrift usw.)|

### <a name="purchasing-schema"></a>Kauf Schema

Details zu Lieferanten und Bestands Element Käufen.

|Tabelle|Beschreibung|
|-----------------------------|---------------------|
|Suppliers|Haupt Entitäts Tabelle für Zulieferer (Organisationen)|
|Suppliercategories|Kategorien für Lieferanten (z. b. Neuheiten, Toys, Bekleidung, Verpacken usw.)|
|Suppliertransactions|Alle im Lieferanten zusammenhängenden Finanztransaktionen (Rechnungen, Zahlungen)|
|"PurchaseOrders|Details zu Lieferanten Bestellungen|
|PurchaseOrderLines|Detail Zeilen von Lieferanten Bestellungen|

 
### <a name="sales-schema"></a>Sales-Schema

Details zu Kunden, Vertriebsmitarbeitern und Bestands Element Verkäufen.

|Tabelle|Beschreibung|
|-----------------------------|---------------------|
|Customers|Haupt Entitäts Tabellen für Kunden (Organisationen oder Einzelpersonen)|
|Customercategories|Kategorien für Kunden (z. b. Neuheits Geschäfte, Supermärkte usw.)|
|Buyinggroups|Kundenorganisationen können Teil von Gruppen sein, die eine größere Kauf Leistung haben.|
|Customertransactions|Alle Finanztransaktionen, die Kunden bezogen sind (Rechnungen, Zahlungen)|
|Specialdeals|Sonderpreise. Dies kann festes Preis, Rabatt in Dollar oder Rabatt in Prozent enthalten.|
|Orders|Details der Kunden Bestellungen|
|OrderLines|Detail Zeilen von Kunden Bestellungen|
|Rechnungen|Details zu Kunden Rechnungen|
|Invoicelines|Detail Zeilen von Kunden Rechnungen|

### <a name="warehouse-schema"></a>Warehouse-Schema

Details zu Aktien Elementen, deren Bestand und Transaktionen.

|Tabelle|Beschreibung|
|-----------------------------|---------------------|
|StockItems|Haupt Entitäts Tabelle für Aktien Elemente|
|StockItemHoldings|Nicht Temporale Spalten für Aktien Elemente. Dabei handelt es sich um häufig aktualisierte Spalten.|
|Stockgroups|Gruppen zum kategorialisieren von Aktien Elementen (z. b. Neuheiten, Spielsachen, essbare Neuheiten usw.)|
|StockItemStockGroups|Welche Aktien Elemente sind in welchen Aktien Gruppen (n zu viele)|
|Farben|Aktien Elemente können (optional) über Farben verfügen.|
|PackageTypes|Möglichkeiten zum Packen von Bestands Elementen (z. b. Box, Karton, Palette, kg usw.)|
|StockItemTransactions|Transaktionen, die alle Bewegungen aller Aktien Elemente abdecken (Receipt, Sale, Write-off)|
|Vehicletemperaturen|Regelmäßig aufgezeichnete Temperatur von fahrzeugchillern|
|ColdRoomTemperatures|Regelmäßig aufgezeichnete Temperaturen von kalt Raum chillern|


## <a name="design-considerations"></a>Entwurfs Überlegungen

Der Daten bankentwurf ist subjektiv, und es gibt keine Rechte oder falsche Methode zum Entwerfen einer Datenbank. In den Schemas und Tabellen in dieser Datenbank werden Ideen zum Entwerfen Ihrer eigenen Datenbank angezeigt.

### <a name="schema-design"></a>Schema Entwurf

Wideworldimporters verwendet eine kleine Anzahl von Schemas, sodass es einfach ist, das Datenbanksystem zu verstehen und Daten bankprinzipien zu veranschaulichen.  

Wenn möglich, werden Tabellen, die häufig zusammen im selben Schema abgefragt werden, von der Datenbank zusammengefasst, um die Komplexität des Joins zu minimieren.

Das Datenbankschema wurde basierend auf einer Reihe von Metadatentabellen in einem anderen Daten Bank WWI_Preparation Code generiert. Dadurch erhält wideworldimporters einen sehr hohen Grad an Entwurfs Konsistenz, namens Konsistenz und Vollständigkeit. Ausführliche Informationen zur Generierung des Schemas finden Sie im Quellcode: [Wide-World-importierungs-/WWI-Database-Scripts](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts) .

### <a name="table-design"></a>Tabellen Entwurf

- Alle Tabellen haben Primärschlüssel für einzelne Spalten für die Einfachheit der Verknüpfung.
- Alle Schemas, Tabellen, Spalten, Indizes und Check-Einschränkungen verfügen über eine erweiterte Beschreibungs Eigenschaft, die zum Identifizieren des Zwecks des Objekts oder der Spalte verwendet werden kann. Speicher optimierte Tabellen stellen eine Ausnahme dar, da Sie zurzeit keine erweiterten Eigenschaften unterstützen.
- Alle Fremdschlüssel werden automatisch indiziert, es sei denn, es gibt einen anderen nicht gruppierten Index, der über dieselbe Linke Komponente verfügt.
- Die automatische Nummerierung in Tabellen basiert auf Sequenzen. Diese Sequenzen sind für verknüpfte Server und ähnliche Umgebungen einfacher als Identitäts Spalten. Für Speicher optimierte Tabellen werden Identitäts Spalten verwendet, da Sie in SQL Server 2016 nicht unterstützt werden.
- Für diese Tabellen wird eine einzelne Sequenz (transaktionid) verwendet: Customertransactions, suppliertransactions und stockitemtransactions. Dadurch wird veranschaulicht, wie eine Gruppe von Tabellen eine einzelne Sequenz aufweisen kann.
- Einige Spalten verfügen über geeignete Standardwerte.

### <a name="security-schemas"></a>Sicherheits Schemas

Aus Sicherheitsgründen lässt wideworldimporters nicht zu, dass externe Anwendungen direkt auf Daten Schemas zugreifen. Um den Zugriff zu isolieren, verwendet wideworldimporters Sicherheits Zugriffs Schemas, die keine Daten enthalten, aber Sichten und gespeicherte Prozeduren enthalten. Externe Anwendungen verwenden die Sicherheits Schemas, um die Daten abzurufen, die Sie anzeigen dürfen.  Auf diese Weise können Benutzer nur die Sichten und gespeicherten Prozeduren in den Schemas für den sicheren Zugriff ausführen.

Dieses Beispiel enthält z. b. Power BI Dashboards. Eine externe Anwendung greift auf diese Power BI Dashboards vom Power BI Gateway aus als Benutzer, der über die Berechtigung schreibgeschützt für das Power BI-Schema verfügt.  Für die schreibgeschützte Berechtigung benötigt der Benutzer nur die SELECT-und EXECUTE-Berechtigung für das Power BI-Schema. Ein Datenbankadministrator bei WWI weist diese Berechtigungen nach Bedarf zu.

## <a name="stored-procedures"></a>Gespeicherte Prozeduren

Gespeicherte Prozeduren werden in Schemas organisiert. Die meisten Schemas werden für Konfigurations-oder Beispiel Zwecke verwendet.

Das `Website` Schema enthält die gespeicherten Prozeduren, die von einem Web-Front-End verwendet werden können.

Die `Reports` Schemas und `PowerBI` sind für Reporting Services und Power BI vorgesehen. Es wird empfohlen, diese Schemas für Berichts Zwecke zu verwenden.

### <a name="website-schema"></a>Website Schema

Dies sind die Verfahren, die von einer Client Anwendung verwendet werden, z. b. ein Web-Front-End.

|Prozedur|Zweck|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|Ermöglicht es einer Person ( `Application.People`von), Zugriff auf die Website zu haben.|
|ChangePassword|Ändert das Kennwort eines Benutzers (für Benutzer, die keine externen Authentifizierungsmechanismen verwenden).|
|Insertcustomerorders|Ermöglicht das Einfügen von einem oder mehreren Kunden Bestellungen (einschließlich der Bestell Zeilen).|
|Invoicecustomerorders|Führt eine Liste der Bestellungen aus, die in Rechnung gestellt werden, und verarbeitet die Rechnungen.|
|RecordColdRoomTemperatures|Nimmt eine Sensordaten Liste als Tabellenwert Parameter (TVP) an und wendet die Daten auf die `Warehouse.ColdRoomTemperatures` Temporale Tabelle an.|
|Recordvehicletemperatur|Nimmt ein JSON-Array an und verwendet es `Warehouse.VehicleTemperatures`, um zu aktualisieren.|
|Searchforcustomers|Sucht nach Kunden anhand des Namens oder eines Teils des Namens (entweder Firmenname oder Personen Name).|
|SearchForPeople|Sucht nach Personen anhand des Namens oder eines Teils des Namens.|
|SearchForStockItems|Sucht nach Aktien Elementen anhand des Namens oder eines Teils der Namens-oder Marketing Kommentare.|
|SearchForStockItemsByTags|Sucht nach Aktien Elementen nach Tags.|
|Searchforsuppliers|Sucht nach Lieferanten anhand des Namens oder eines Teils des Namens (entweder Firmenname oder Personen Name).|

### <a name="integration-schema"></a>Integrations Schema

Die gespeicherten Prozeduren in diesem Schema werden vom ETL-Prozess verwendet. Sie erhalten die benötigten Daten aus verschiedenen Tabellen für den Zeitraum, der für das [ETL-Paket](wide-world-importers-perform-etl.md)erforderlich ist.

### <a name="dataloadsimulation-schema"></a>Dataloadsimulation-Schema

Simuliert eine Arbeitsauslastung, die Verkäufe und Einkäufe einfügt. Die Haupt gespeicherte Prozedur ist `PopulateDataToCurrentDate`, mit der Beispiel Daten bis zum aktuellen Datum eingefügt werden.

|Prozedur|Zweck|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|Erstellt die für die Daten Lade Simulation erforderlichen Prozeduren neu. Dies ist erforderlich, um Daten bis zum aktuellen Datum zu verschieben.|
|Configuration_RemoveDataLoadSimulationProcedures|Dadurch werden die Prozeduren nach Abschluss der Daten Simulation wieder entfernt.|
|DeactivateTemporalTablesBeforeDataLoad|Entfernt die zeitliche Natur aller temporalen Tabellen und wendet ggf. einen---------------------Typ an|
|Populatedatatocurrentdate|Wird verwendet, um die Daten bis zum aktuellen Datum zu verschieben. Sollte vor allen anderen Konfigurationsoptionen ausgeführt werden, nachdem die Datenbank aus einer ersten Sicherung wieder hergestellt wurde.|
|ReactivateTemporalTablesAfterDataLoad|Stellt die temporalen Tabellen wieder her, einschließlich der Überprüfung der Datenkonsistenz. (Entfernt die zugeordneten Trigger).|


### <a name="application-schema"></a>Anwendungs Schema

Diese Prozeduren werden verwendet, um das Beispiel zu konfigurieren. Sie dienen zum Anwenden von Enterprise Edition-Features auf die Standard Edition-Version des Beispiels sowie zum Hinzufügen von Überwachungen und Volltextindizierung.

|Prozedur|Zweck|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|Fügt einer Rolle ein Mitglied hinzu, wenn der Member nicht bereits in der Rolle vorhanden ist.|
|Configuration_ApplyAuditing|Fügt eine Überwachung hinzu. Die Server Überwachung wird für Standard Edition-Datenbanken angewendet. für Enterprise Edition wird eine zusätzliche Daten Bank Überwachung hinzugefügt.|
|Configuration_ApplyColumnstoreIndexing|Wendet die columnstore-- `Sales.OrderLines` Indizierung entsprechend auf und `Sales.InvoiceLines` und neu auf.|
|Configuration_ApplyFullTextIndexing|Wendet Volltextindizes auf `Application.People`, `Sales.Customers`, `Purchasing.Suppliers`und `Warehouse.StockItems`an. Ersetzt `Website.SearchForPeople`, `Website.SearchForSuppliers`, `Website.SearchForCustomers`, durch`Website.SearchForStockItems`ErsatzProzeduren, die die Volltextindizierung verwenden. `Website.SearchForStockItemsByTags`|
|Configuration_ApplyPartitioning|Wendet die Tabellenpartitionierung `Purchasing.SupplierTransactions`auf und an `Sales.CustomerTransactions` und ordnet die Indizes entsprechend an.|
|Configuration_ApplyRowLevelSecurity|Wendet die Sicherheit auf Zeilenebene an, um Kunden nach Vertriebs Gebiets bezogenen Rollen zu filtern.|
|Configuration_ConfigureForEnterpriseEdition|Wendet die columnstore--Indizierung, den vollständigen Text, den in-Memory, polybase und die Partitionierung an.|
|Configuration_EnableInMemory|Fügt eine Speicher optimierte Datei Gruppe hinzu (wenn Sie nicht in Azure funktioniert), `Warehouse.ColdRoomTemperatures`ersetzt `Warehouse.VehicleTemperatures` mit in-Memory-Entsprechungen und migriert die `Website.OrderIDList`Daten, erstellt die Tabellen `Website.OrderList`Typen, `Website.SensorDataList` , `Website.OrderLineList`, mit Speicher optimierte Entsprechungen, löscht und erstellt die `Website.InvoiceCustomerOrders`Prozeduren `Website.InsertCustomerOrders`,, `Website.RecordColdRoomTemperatures` und, die diese Tabellentypen verwenden.|
|Configuration_RemoveAuditing|Entfernt die Überwachungskonfiguration.|
|Configuration_RemoveRowLevelSecurity|Entfernt die Sicherheitskonfiguration auf Zeilenebene (Dies wird für Änderungen an den zugeordneten Tabellen benötigt).|
|CreateRoleIfNonExistant|Erstellt eine Daten Bank Rolle, wenn Sie nicht bereits vorhanden ist.|


### <a name="sequences-schema"></a>Sequenz Schema

Prozeduren zum Konfigurieren der Sequenzen in der Datenbank.

|Prozedur|Zweck|
|-----------------------------|---------------------|
|Reseedallsequenzen|Ruft die Prozedur reseedsequencebeyondtablevalue für alle Sequenzen auf.|
|ReseedSequenceBeyondTableValue|Wird verwendet, um den nächsten Sequenzwert hinter dem Wert in einer Tabelle, die dieselbe Sequenz verwendet, neu zu positionieren. (Z. b. eine DBCC CHECKIDENT für Identitäts Spalten, die für Sequenzen gleichwertig sind, aber über potenziell mehrere Tabellen hinweg|
