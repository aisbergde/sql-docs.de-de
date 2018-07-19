---
title: Massenimport der Kopie Änderungen für verbesserte Datums- und Uhrzeittypen (OLE DB und ODBC) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC, bulk copy operations
- bulk copy [ODBC], changes for date/time improvements
ms.assetid: c29e0f5e-9b3c-42b3-9856-755f4510832f
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e33cc7b320f3445d0da6e7f5927fe985a668b77
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430649"
---
# <a name="bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc"></a>Massenkopieränderungen für verbesserte Datums- und Uhrzeittypen (OLE DB und ODBC)
  In diesem Thema werden die Datum-/Uhrzeiterweiterungen beschrieben, die die Massenkopierfunktionalität unterstützen. Die Informationen in diesem Thema sind für OLE DB und ODBC in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client gültig.  
  
## <a name="format-files"></a>Formatdateien  
 Beim interaktiven Erstellen von Formatdateien beschreibt die folgende Tabelle die Eingaben, die zum Angeben von Datum-/Uhrzeittypen verwendet werden, sowie die entsprechenden Datentypnamen der Hostdatei.  
  
|Dateispeichertyp|Datentyp in der Hostdatei|Als Antwort auf die Frage: "Geben Sie den Dateispeichertyp des Felds < Feldname > [\<Standardwert >]:"|  
|-----------------------|-------------------------|-----------------------------------------------------------------------------------------------------|  
|DATETIME|SQLDATETIME|d|  
|Smalldatetime|SQLDATETIM4|D|  
|date|SQLDATE|de|  
|Uhrzeit|SQLTIME|te|  
|Datetime2|SQLDATETIME2|d2|  
|Datetimeoffset|SQLDATETIMEOFFSET|do|  
  
 Das XML-Formatdatei-XSD hat die folgenden Hinzufügungen:  
  
```  
<xs:complexType name="SQLDATETIME2">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATETIMEOFFSET">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATE">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLTIME">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
```  
  
## <a name="character-data-files"></a>Zeichendatendateien  
 In zeichendatendateien werden Datums-und Uhrzeitwerte dargestellt, wie beschrieben im Abschnitt "Datenformate: Zeichenfolgen und Literale" [Datentypunterstützung für ODBC-Datum und Uhrzeit-Verbesserungen](data-type-support-for-odbc-date-and-time-improvements.md) für ODBC oder [Datentypunterstützung für OLE DB-Datum und Uhrzeit-Verbesserungen](../native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md) für OLE DB.  
  
 In systemeigenen Datendateien werden Werte für Datum und Uhrzeit für die vier neuen Typen als TDS-Entsprechungen mit einer Skala von 7 dargestellt werden (da dies die maximal unterstützte von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Bcp-Datendateien, jedoch nicht die Dezimalstellen dieser Spalten speichern). Es erfolgt keine Änderung an der Speicherung der vorhandenen `datetime`- und `smalldatetime`-Typen oder ihrer Tabular Data Stream-Entsprechungen (TDS).  
  
 Die Speichergrößen für die anderen Speichertypen sind für OLE DB wie folgt:  
  
|Dateispeichertyp|Speichergröße (in Byte)|  
|-----------------------|---------------------------|  
|DATETIME|8|  
|smalldatetime|4|  
|date|3|  
|Uhrzeit|6|  
|datetime2|9|  
|datetimeoffset|11|  
  
 Für ODBC lauten die Größen folgendermaßen: Beachten Sie, dass es nicht notwendig ist, Genauigkeit in Format- oder Datendateien zu speichern, da BCP.exe die Genauigkeit immer vom Server abruft.  
  
|Dateispeichertyp|Speichergröße (in Byte)|Speicherformat|  
|-----------------------|---------------------------|--------------------|  
|datetime (d)|8|TDS|  
|smalldatetime (D)|4|TDS|  
|date (de)|3|TDS|  
|time (te)|6|TDS|  
|datetime2 (d2)|9|TDS|  
|datetimeoffset (do)|11|TDS|  
  
## <a name="bcp-types-in-sqlnclih"></a>BCP-Typen in sqlncli.h  
 Die folgenden Typen werden in sqlncli.h definiert, um mit den BCP API-Erweiterungen für ODBC verwendet zu werden. Diese Typen werden übergeben, mit der *eUserDataType* Parameter der ibcpsession:: BCPColFmt, in der OLE DB.  
  
|Dateispeichertyp|Datentyp in der Hostdatei|Geben Sie für die Verwendung mit ibcpsession:: BCPColFmt|value|  
|-----------------------|-------------------------|-----------------------------------------------------------|-----------|  
|DATETIME|SQLDATETIME|BCP_TYPE_SQLDATETIME|0x3d|  
|Smalldatetime|SQLDATETIM4|BCP_TYPE_SQLDATETIME4|0x3a|  
|date|SQLDATE|BCP_TYPE_SQLDATE|0x28|  
|Uhrzeit|SQLTIME|BCP_TYPE_SQLTIME|0x29|  
|Datetime2|SQLDATETIME2|BCP_TYPE_SQLDATETIME2|0x2a|  
|Datetimeoffset|SQLDATETIMEOFFSET|BCP_TYPE_SQLDATETIMEOFFSET|0x2b|  
  
## <a name="bcp-data-type-conversions"></a>BCP-Datentypkonvertierungen  
 Die folgenden Tabellen enthalten Konvertierungsinformationen.  
  
 **OLE DB-Hinweis** die folgenden Konvertierungen werden von IBCPSession ausgeführt. IRowsetFastLoad verwendet OLE DB-Konvertierungen gemäß [ausgeführte Konvertierungen vom Client zum Server](../native-client-ole-db-date-time/conversions-performed-from-client-to-server.md). Beachten Sie, dass datetime-Werte auf 1/300stel einer Sekunde gerundet werden und dass für smalldatetime-Werte die Sekunden vom Server auf null festgelegt werden, nachdem die unten beschriebenen Clientkonvertierungen durchgeführt wurden. Datetime-Rundung wird durch Stunden und Minuten, aber nicht durch das Datum weitergegeben.  
  
|An --><br /><br /> Von|date|Uhrzeit|smalldatetime|DATETIME|datetime2|datetimeoffset|char|wchar|  
|------------------------|----------|----------|-------------------|--------------|---------------|--------------------|----------|-----------|  
|date|1|-|1,6|1,6|1,6|1,5,6|1,3|1,3|  
|Uhrzeit|–|1,10|1,7,10|1,7,10|1,7,10|1,5,7,10|1,3|1,3|  
|Smalldatetime|1,2|1,4,10|1|1|1,10|1,5,10|1,11|1,11|  
|DATETIME|1,2|1,4,10|1,12|1|1,10|1,5,10|1,11|1,11|  
|Datetime2|1,2|1,4,10|1,10 (ODBC)1,12 (OLE DB)|1,10|1,10|1,5,10|1,3|1,3|  
|Datetimeoffset|1,2,8|1,4,8,10|1,8,10|1,8,10|1,8,10|1,10|1,3|1,3|  
|Char/wchar (date)|9|-|9,6 (ODBC)9,6,12 (OLE DB)|9,6 (ODBC)9,6,12 (OLE DB)|9,6|9,5,6|–|–|  
|Char/wchar (time)|-|9,10|9,7,10 (ODBC)9,7,10,12 (OLE DB)|9,7,10 (ODBC)9,7,10, 12 (OLE DB)|9,7,10|9,5,7,10|–|–|  
|Char/wchar (datetime)|9,2|9,4,10|9,10 (ODBC)9,10,12 (OLE DB)|9,10 (ODBC)9,10,12 (OLE DB)|9,10|9,5,10|–|–|  
|Char/wchar (datetimeoffset)|9,2,8|9,4,8,10|9,8,10 (ODBC)9,8,10,12 (OLE DB)|9,8,10 (ODBC)9,8,10,12 (OLE DB)|9,8,10|9,10|–|–|  
  
#### <a name="key-to-symbols"></a>Aufschlüsselung der Symbole  
  
|Symbol|Bedeutung|  
|------------|-------------|  
|-|Es wird keine Konvertierung unterstützt.<br /><br /> Es wird ein ODBC-Diagnosedatensatz mit SQLSTATE 07006 und der Meldung "Attributverletzung beschränkter Datentypen" generiert.|  
|1|Wenn die bereitgestellten Daten ungültig sind, wird ein ODBC-Diagnosedatensatz mit SQLSTATE 22007 und der Meldung "Ungültiges Datetime-Format" generiert. Für datetimeoffset-Werte muss der Uhrzeitteil nach der Konvertierung in das UTC-Format innerhalb des gültigen Bereichs liegen, und zwar selbst dann, wenn keine Konvertierung in UTC angefordert wird. Das liegt daran, dass TDS und der Server immer die Uhrzeit in datetimeoffset-Werten für UTC normalisieren. Darum muss der Client überprüfen, dass sich die Zeitkomponenten innerhalb des nach Konvertierung zu UTC unterstützten Bereichs befinden.|  
|2|Die Uhrzeitkomponente wird ignoriert.|  
|3|Wenn für ODBC eine Kürzung mit Datenverlust auftritt, wird ein Diagnosedatensatz mit SQLSTATE 22001 und der Meldung 'Die Zeichenfolgedaten wurden rechts abgeschnitten' generiert. Die Anzahl der Sekundendezimalstellen wird durch die Größe der Zielspalte gemäß der folgenden Tabelle bestimmt. Für Spaltengrößen, die den Bereich in der Tabelle übersteigen, werden 7 Dezimalstellen impliziert. Diese Konvertierung sollte bis zu neun Dezimalstellen für Sekundenbruchteile ermöglichen, das von ODBC zugelassene Maximum.<br /><br /> **Typ:** DBTIME2<br /><br /> **Implizierte Dezimalstellen 0** 8<br /><br /> **Implizierte Dezimalstellen 1..7** 10,16<br /><br /> <br /><br /> **Typ:** DBTIMESTAMP<br /><br /> **Implizierte Dezimalstellen 0:** 19<br /><br /> **Implizierte Dezimalstellen 1..7:** 21..27<br /><br /> <br /><br /> **Typ:** DBTIMESTAMPOFFSET<br /><br /> **Implizierte Dezimalstellen 0:** 26<br /><br /> **Implizierte Dezimalstellen 1..7:** 28..34<br /><br /> Für OLE DB wird ein Fehler generiert, wenn eine Kürzung mit Datenverlust auftritt. Für datetime2 wird die Anzahl der Dezimalstellen für Sekundenbruchteile anhand der Größe der Zielspalte gemäß der folgenden Tabelle bestimmt: Für Spaltengrößen, die den Bereich in der Tabelle übersteigen, werden 9 Dezimalstellen impliziert. Diese Konvertierung sollte bis zu neun Dezimalstellen für Sekundenbruchteile ermöglichen, das von OLE&nbsp;DB zugelassene Maximum.<br /><br /> **Typ:** DBTIME2<br /><br /> **Implizierte Dezimalstellen 0** 8<br /><br /> **Implizierte Dezimalstellen 1..9** 1..9<br /><br /> <br /><br /> **Typ:** DBTIMESTAMP<br /><br /> **Implizierte Dezimalstellen 0:** 19<br /><br /> **Implizierte Dezimalstellen 1..9:** 21..29<br /><br /> <br /><br /> **Typ:** DBTIMESTAMPOFFSET<br /><br /> **Implizierte Dezimalstellen 0:** 26<br /><br /> **Implizierte Dezimalstellen 1..9:** 28..36|  
|4|Die Datumskomponente wird ignoriert.|  
|5|Die Zeitzone wird auf UTC festgelegt (zum Beispiel 00:00).|  
|6|Die Uhrzeit wird auf 0 (Null) festgelegt.|  
|7|Das Datum wird auf den 01.01.1900 festgelegt.|  
|8|Der Zeitzonenoffset wird ignoriert.|  
|9|Die Zeichenfolge wird analysiert und je nach dem ersten Satzzeichen und dem Vorhandensein weiterer Komponenten in einen date-, datetime-, datetimeoffset- oder time-Wert konvertiert. Die Zeichenfolge wird dann in den Zieltyp konvertiert. Dabei wird nach den Regeln am Ende dieses Themas für den Quelltyp vorgegangen, der von diesem Prozess ermittelt wird. Wenn die bereitgestellten Daten nicht ohne Fehler analysiert werden können, oder wenn sich ein Komponententeil außerhalb des zulässigen Bereichs befindet, oder wenn keine Konvertierung vom Literaltyp zum Zieltyp stattfindet, wird ein Fehler angezeigt (OLE DB), oder es wird ein ODBC-Diagnosedatensatz mit SQLSTATE 22018 und der Meldung "Ungültiger Zeichenwert für Konvertierungsangabe" generiert. Wenn die Jahresangabe außerhalb des vom datetime- und smalldatetime-Parameter unterstützten Bereichs liegt, wird ein Fehler angezeigt (OLE DB), oder es wird ein Diagnosedatensatz mit SQLSTATE 22007 und der Meldung "Ungültiges Datetime-Format" generiert.<br /><br /> Der Wert für datetimeoffset muss nach der Konvertierung in das UTC-Format innerhalb des gültigen Bereichs liegen, und zwar selbst dann, wenn keine Konvertierung in UTC angefordert wird. Der Grund dafür ist, dass der TDS und der Server das Datum stets in datetimeoffset-Werte für UTC normalisieren, weshalb der Client prüfen muss, ob die Zeitkomponenten innerhalb des nach Konvertierung in UTC unterstützten Bereichs liegen. Wenn der Wert nicht innerhalb des unterstützten UTC-Bereichs liegt, wird ein Fehler angezeigt (OLE DB), oder es wird ein Diagnosedatensatz mit SQLSTATE 22007 und der Meldung "Ungültiges Datetime-Format" generiert.|  
|10|Wenn es während einer Konvertierung vom Client zum Server zu Kürzungen mit Datenverlust kommt, wird ein Fehler angezeigt (OLE DB), und es wird ein Diagnosedatensatz mit SQLSTATE 22008 und der Meldung "Überlauf im Datetime-Feld" generiert. Dieser Fehler tritt auch dann auf, wenn der Wert außerhalb des Bereichs liegt, der vom UTC-Bereich, den der Server verwendet, dargestellt werden kann. Wenn während einer Konvertierung vom Server zum Client eine Kürzung der Sekunden oder Sekundenbruchteile auftritt, wird lediglich eine Warnung angezeigt.|  
|11|Wenn eine Kürzung mit Datenverlust auftritt, wird ein Diagnosedatensatz generiert.<br /><br /> Bei einer Konvertierung vom Server zum Client handelt es sich dabei um eine Warnung (ODBC SQLSTATE S1000).<br /><br /> Bei einer Konvertierung vom Client zum Server handelt es sich dabei um einen Fehler (ODBC SQLSTATE 22001).|  
|12|Die Sekunden werden auf null festgelegt, und die Sekundenbruchteile werden verworfen. Kein Kürzungsfehler ist möglich.|  
|–|Das Verhalten von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und früheren Versionen ist beibehalten worden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datums- / Uhrzeitverbesserungen &#40;ODBC&#41;](date-and-time-improvements-odbc.md)   
 [Datums- / Uhrzeitverbesserungen &#40;OLE-DB&#41;](../native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  