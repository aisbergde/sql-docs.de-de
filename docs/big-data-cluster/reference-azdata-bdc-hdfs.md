---
title: Referenz zu „azdata bdc hdfs“
titleSuffix: SQL Server big data clusters
description: Referenzartikel zu „azdata bdc hdfs“-Befehlen.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d63d0cbd9d3d36d2d76d5b1fa01337d17084306d
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155233"
---
# <a name="azdata-bdc-hdfs"></a>azdata bdc hdfs

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

Dieser Artikel ist ein Referenz Artikel für **azdata**. 

## <a name="commands"></a>Befehle
|     |     |
| --- | --- |
[azdata BDC HDFS-Status](reference-azdata-bdc-hdfs-status.md) | Status Befehle des HDFS-Dienstanbieter.
[azdata bdc hdfs shell](#azdata-bdc-hdfs-shell) | Die HDFS-Shell ist eine einfache interaktive Befehlsshell für das HDFS-Dateisystem.
[azdata bdc hdfs ls](#azdata-bdc-hdfs-ls) | Auflisten des Status der angegebenen Datei bzw. des angegebenen Verzeichnisses.
[azdata bdc hdfs exists](#azdata-bdc-hdfs-exists) | Bestimmen, ob eine Datei oder ein Verzeichnis vorhanden ist.  Gibt „True“ bei Vorhandensein zurück, andernfalls „False“.
[azdata bdc hdfs mkdir](#azdata-bdc-hdfs-mkdir) | Erstellen eines Verzeichnisses im angegebenen Pfad.
[azdata bdc hdfs mv](#azdata-bdc-hdfs-mv) | Verschieben der angegebenen Datei bzw. des angegebenen Pfads an den angegebenen Speicherort.
[azdata bdc hdfs create](#azdata-bdc-hdfs-create) | Erstellen der Textdatei am angegebenen Speicherort.  Einfacher Textinhalt kann über den Datenparameter hinzugefügt werden.
[azdata bdc hdfs cat](#azdata-bdc-hdfs-cat) | Lesen des Inhalts einer Datei.  Offset und Länge in Bytes sind optionale Parameter.
[azdata bdc hdfs rm](#azdata-bdc-hdfs-rm) | Entfernen einer Datei oder eines Verzeichnisses.
[azdata bdc hdfs rmr](#azdata-bdc-hdfs-rmr) | Rekursives Entfernen einer Datei oder eines Verzeichnisses.
[azdata bdc hdfs chmod](#azdata-bdc-hdfs-chmod) | Ändern der Berechtigung für die angegebene Datei oder das angegebene Verzeichnis.
[azdata bdc hdfs chown](#azdata-bdc-hdfs-chown) | Ändern des Besitzers oder der Gruppe der angegebenen Datei.
[azdata bdc hdfs mount](reference-azdata-bdc-hdfs-mount.md) | Verwalten des Einbindens von Remotespeichern in HDFS.
## <a name="azdata-bdc-hdfs-shell"></a>azdata bdc hdfs shell
Die HDFS-Shell ist eine einfache interaktive Befehlsshell für das HDFS-Dateisystem.
```bash
azdata bdc hdfs shell 
```
### <a name="examples"></a>Beispiele
Starten der Shell.
```bash
azdata bdc hdfs shell
```
### <a name="global-arguments"></a>Globale Argumente
#### `--debug`
Ausführlichkeit der Protokollierung erhöhen, um alle Debugprotokolle anzuzeigen.
#### `--help -h`
Zeigen Sie diese Hilfemeldung an, und schließen Sie sie.
#### `--output -o`
Ausgabeformat.  Zulässige Werte: json, jsonc, table, tsv.  Standardwert: json.
#### `--query -q`
JMESPath-Abfragezeichenfolge. Weitere Informationen und Beispiele finden Sie unter [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Ausführlichkeit der Protokollierung erhöhen. „--debug“ für vollständige Debugprotokolle verwenden.
## <a name="azdata-bdc-hdfs-ls"></a>azdata bdc hdfs ls
Auflisten des Status der angegebenen Datei bzw. des angegebenen Verzeichnisses.
```bash
azdata bdc hdfs ls --path -p 
                   
```
### <a name="examples"></a>Beispiele
Auflisten des Status
```bash
azdata bdc hdfs ls --path '/tmp'
```
### <a name="required-parameters"></a>Erforderliche Parameter
#### `--path -p`
Der Pfad zum Auflisten des Status.
### <a name="global-arguments"></a>Globale Argumente
#### `--debug`
Ausführlichkeit der Protokollierung erhöhen, um alle Debugprotokolle anzuzeigen.
#### `--help -h`
Zeigen Sie diese Hilfemeldung an, und schließen Sie sie.
#### `--output -o`
Ausgabeformat.  Zulässige Werte: json, jsonc, table, tsv.  Standardwert: json.
#### `--query -q`
JMESPath-Abfragezeichenfolge. Weitere Informationen und Beispiele finden Sie unter [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Ausführlichkeit der Protokollierung erhöhen. „--debug“ für vollständige Debugprotokolle verwenden.
## <a name="azdata-bdc-hdfs-exists"></a>azdata bdc hdfs exists
Bestimmen, ob eine Datei oder ein Verzeichnis vorhanden ist.  Gibt „True“ bei Vorhandensein zurück, andernfalls „False“.
```bash
azdata bdc hdfs exists --path -p 
                       
```
### <a name="examples"></a>Beispiele
Überprüfen, ob die Datei oder das Verzeichnis vorhanden ist.
```bash
azdata bdc hdfs exists --path '/tmp'
```
### <a name="required-parameters"></a>Erforderliche Parameter
#### `--path -p`
Pfad, dessen Vorhandensein überprüft wird.
### <a name="global-arguments"></a>Globale Argumente
#### `--debug`
Ausführlichkeit der Protokollierung erhöhen, um alle Debugprotokolle anzuzeigen.
#### `--help -h`
Zeigen Sie diese Hilfemeldung an, und schließen Sie sie.
#### `--output -o`
Ausgabeformat.  Zulässige Werte: json, jsonc, table, tsv.  Standardwert: json.
#### `--query -q`
JMESPath-Abfragezeichenfolge. Weitere Informationen und Beispiele finden Sie unter [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Ausführlichkeit der Protokollierung erhöhen. „--debug“ für vollständige Debugprotokolle verwenden.
## <a name="azdata-bdc-hdfs-mkdir"></a>azdata bdc hdfs mkdir
Erstellen eines Verzeichnisses im angegebenen Pfad.
```bash
azdata bdc hdfs mkdir --path -p 
                      
```
### <a name="examples"></a>Beispiele
Erstellen eines Verzeichnisses.
```bash
azdata bdc hdfs mkdir --path '/tmp'
```
### <a name="required-parameters"></a>Erforderliche Parameter
#### `--path -p`
Name des zu erstellenden Verzeichnisses.
### <a name="global-arguments"></a>Globale Argumente
#### `--debug`
Ausführlichkeit der Protokollierung erhöhen, um alle Debugprotokolle anzuzeigen.
#### `--help -h`
Zeigen Sie diese Hilfemeldung an, und schließen Sie sie.
#### `--output -o`
Ausgabeformat.  Zulässige Werte: json, jsonc, table, tsv.  Standardwert: json.
#### `--query -q`
JMESPath-Abfragezeichenfolge. Weitere Informationen und Beispiele finden Sie unter [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Ausführlichkeit der Protokollierung erhöhen. „--debug“ für vollständige Debugprotokolle verwenden.
## <a name="azdata-bdc-hdfs-mv"></a>azdata bdc hdfs mv
Verschieben der angegebenen Datei bzw. des angegebenen Pfads an den angegebenen Speicherort.
```bash
azdata bdc hdfs mv --source-path -s 
                   --target-path -t
```
### <a name="examples"></a>Beispiele
Verschieben von Datei oder Verzeichnis.
```bash
azdata bdc hdfs mv --source-path '/tmp' --target-path '/dest'
```
### <a name="required-parameters"></a>Erforderliche Parameter
#### `--source-path -s`
Das Verzeichnis, das verschoben werden soll.
#### `--target-path -t`
Der Speicherort, zu dem verschoben werden soll.
### <a name="global-arguments"></a>Globale Argumente
#### `--debug`
Ausführlichkeit der Protokollierung erhöhen, um alle Debugprotokolle anzuzeigen.
#### `--help -h`
Zeigen Sie diese Hilfemeldung an, und schließen Sie sie.
#### `--output -o`
Ausgabeformat.  Zulässige Werte: json, jsonc, table, tsv.  Standardwert: json.
#### `--query -q`
JMESPath-Abfragezeichenfolge. Weitere Informationen und Beispiele finden Sie unter [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Ausführlichkeit der Protokollierung erhöhen. „--debug“ für vollständige Debugprotokolle verwenden.
## <a name="azdata-bdc-hdfs-create"></a>azdata bdc hdfs create
Erstellen der Textdatei am angegebenen Speicherort.  Einfacher Textinhalt kann über den Datenparameter hinzugefügt werden.
```bash
azdata bdc hdfs create --path -p 
                       --data -d
```
### <a name="examples"></a>Beispiele
Datei erstellen.
```bash
azdata bdc hdfs create --path '/tmp/test.txt' --data "This is a test."
```
### <a name="required-parameters"></a>Erforderliche Parameter
#### `--path -p`
Name der Datei, die erstellt werden soll.
#### `--data -d`
Inhalt der Datei.  Für einfachen Textinhalt vorgesehen.
### <a name="global-arguments"></a>Globale Argumente
#### `--debug`
Ausführlichkeit der Protokollierung erhöhen, um alle Debugprotokolle anzuzeigen.
#### `--help -h`
Zeigen Sie diese Hilfemeldung an, und schließen Sie sie.
#### `--output -o`
Ausgabeformat.  Zulässige Werte: json, jsonc, table, tsv.  Standardwert: json.
#### `--query -q`
JMESPath-Abfragezeichenfolge. Weitere Informationen und Beispiele finden Sie unter [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Ausführlichkeit der Protokollierung erhöhen. „--debug“ für vollständige Debugprotokolle verwenden.
## <a name="azdata-bdc-hdfs-cat"></a>azdata bdc hdfs cat
Lesen des Inhalts einer Datei.  Offset und Länge in Bytes sind optionale Parameter.
```bash
azdata bdc hdfs cat --path -p 
                    --offset  
                    --length -l
```
### <a name="examples"></a>Beispiele
Datei lesen.
```bash
azdata bdc hdfs cat --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Erforderliche Parameter
#### `--path -p`
Name der Datei, die gelesen wird.
#### `--offset`
Offset in der zu lesenden Datei in Anzahl der Bytes.
#### `--length -l`
Länge der zu lesenden Daten.
### <a name="global-arguments"></a>Globale Argumente
#### `--debug`
Ausführlichkeit der Protokollierung erhöhen, um alle Debugprotokolle anzuzeigen.
#### `--help -h`
Zeigen Sie diese Hilfemeldung an, und schließen Sie sie.
#### `--output -o`
Ausgabeformat.  Zulässige Werte: json, jsonc, table, tsv.  Standardwert: json.
#### `--query -q`
JMESPath-Abfragezeichenfolge. Weitere Informationen und Beispiele finden Sie unter [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Ausführlichkeit der Protokollierung erhöhen. „--debug“ für vollständige Debugprotokolle verwenden.
## <a name="azdata-bdc-hdfs-rm"></a>azdata bdc hdfs rm
Entfernen einer Datei oder eines Verzeichnisses.
```bash
azdata bdc hdfs rm --path -p 
                   
```
### <a name="examples"></a>Beispiele
Entfernen einer Datei oder eines Verzeichnisses.
```bash
azdata bdc hdfs rm --path '/tmp'
```
### <a name="required-parameters"></a>Erforderliche Parameter
#### `--path -p`
Name der Datei, die entfernt werden soll.
### <a name="global-arguments"></a>Globale Argumente
#### `--debug`
Ausführlichkeit der Protokollierung erhöhen, um alle Debugprotokolle anzuzeigen.
#### `--help -h`
Zeigen Sie diese Hilfemeldung an, und schließen Sie sie.
#### `--output -o`
Ausgabeformat.  Zulässige Werte: json, jsonc, table, tsv.  Standardwert: json.
#### `--query -q`
JMESPath-Abfragezeichenfolge. Weitere Informationen und Beispiele finden Sie unter [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Ausführlichkeit der Protokollierung erhöhen. „--debug“ für vollständige Debugprotokolle verwenden.
## <a name="azdata-bdc-hdfs-rmr"></a>azdata bdc hdfs rmr
Rekursives Entfernen einer Datei oder eines Verzeichnisses.
```bash
azdata bdc hdfs rmr --path -p 
                    
```
### <a name="examples"></a>Beispiele
Rekursives Entfernen des Verzeichnisses.
```bash
azdata bdc hdfs rmr --path '/tmp'
```
### <a name="required-parameters"></a>Erforderliche Parameter
#### `--path -p`
Name der Datei, die rekursiv entfernt werden soll.
### <a name="global-arguments"></a>Globale Argumente
#### `--debug`
Ausführlichkeit der Protokollierung erhöhen, um alle Debugprotokolle anzuzeigen.
#### `--help -h`
Zeigen Sie diese Hilfemeldung an, und schließen Sie sie.
#### `--output -o`
Ausgabeformat.  Zulässige Werte: json, jsonc, table, tsv.  Standardwert: json.
#### `--query -q`
JMESPath-Abfragezeichenfolge. Weitere Informationen und Beispiele finden Sie unter [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Ausführlichkeit der Protokollierung erhöhen. „--debug“ für vollständige Debugprotokolle verwenden.
## <a name="azdata-bdc-hdfs-chmod"></a>azdata bdc hdfs chmod
Ändern der Berechtigung für die angegebene Datei oder das angegebene Verzeichnis.
```bash
azdata bdc hdfs chmod --path -p 
                      --permission
```
### <a name="examples"></a>Beispiele
Ändern der Datei- oder Verzeichnisberechtigung.
```bash
azdata bdc hdfs chmod --permission 775 --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Erforderliche Parameter
#### `--path -p`
Name der Datei oder des Verzeichnisses, wofür Berechtigungen festgelegt werden sollen.
#### `--permission`
Festzulegende Berechtigungsoktette.  Beispiel „775“.
### <a name="global-arguments"></a>Globale Argumente
#### `--debug`
Ausführlichkeit der Protokollierung erhöhen, um alle Debugprotokolle anzuzeigen.
#### `--help -h`
Zeigen Sie diese Hilfemeldung an, und schließen Sie sie.
#### `--output -o`
Ausgabeformat.  Zulässige Werte: json, jsonc, table, tsv.  Standardwert: json.
#### `--query -q`
JMESPath-Abfragezeichenfolge. Weitere Informationen und Beispiele finden Sie unter [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Ausführlichkeit der Protokollierung erhöhen. „--debug“ für vollständige Debugprotokolle verwenden.
## <a name="azdata-bdc-hdfs-chown"></a>azdata bdc hdfs chown
Ändern des Besitzers oder der Gruppe der angegebenen Datei.
```bash
azdata bdc hdfs chown --path -p 
                      --owner  
                      --group -g
```
### <a name="examples"></a>Beispiele
Ändern von Besitzer und Gruppe.
```bash
azdata bdc hdfs chown --owner hdfs --group superusergroup --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Erforderliche Parameter
#### `--path -p`
Name der Datei oder des Verzeichnisses, wofür der Besitzer geändert werden soll.
#### `--owner`
Festzulegender Besitzername.
#### `--group -g`
Festzulegender Gruppenname.
### <a name="global-arguments"></a>Globale Argumente
#### `--debug`
Ausführlichkeit der Protokollierung erhöhen, um alle Debugprotokolle anzuzeigen.
#### `--help -h`
Zeigen Sie diese Hilfemeldung an, und schließen Sie sie.
#### `--output -o`
Ausgabeformat.  Zulässige Werte: json, jsonc, table, tsv.  Standardwert: json.
#### `--query -q`
JMESPath-Abfragezeichenfolge. Weitere Informationen und Beispiele finden Sie unter [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Ausführlichkeit der Protokollierung erhöhen. „--debug“ für vollständige Debugprotokolle verwenden.

## <a name="next-steps"></a>Nächste Schritte

- Weitere Informationen zu anderen **azdata**-Befehlen finden Sie unter [azdata](reference-azdata.md). 

- Weitere Informationen zum Installieren des Tools **azdata** finden Sie unter [Install azdata to manage SQL Server 2019 big data clusters (Installieren von azdata zum Verwalten von Big-Data-Clustern von SQL Server 2019)](deploy-install-azdata.md).
