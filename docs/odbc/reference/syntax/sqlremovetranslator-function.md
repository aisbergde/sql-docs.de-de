---
title: SQLRemoveTranslator-Funktion | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveTranslator
helpviewer_keywords:
- SQLRemoveTranslator function [ODBC]
ms.assetid: c6feda49-0359-4224-8de9-77125cf2397b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8a577a868f7b56a6677da3cb12cfb29057ea66f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024522"
---
# <a name="sqlremovetranslator-function"></a>SQLRemoveTranslator-Funktion
**Übereinstimmung mit Standards**  
 Eingeführt in Version: ODBC 3.0  
  
 **Zusammenfassung**  
 **SQLRemoveTranslator** entfernt Informationen über einen Übersetzer aus dem Abschnitt "Odbcinst.ini" Systeminformationen und verringert die Translator-Komponente Verwendungsanzahl um 1.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumente  
 *lpszTranslator*  
 [Eingabe] Der Name des Übersetzers im Schlüssel "Odbcinst.ini" die Systeminformationen registriert.  
  
 *lpdwUsageCount*  
 [Ausgabe] Die Verwendungsanzahl des konvertierers, nachdem diese Funktion aufgerufen wurde.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" bei Erfolg, FALSE, wenn ein Fehler auftritt. Wenn kein Eintrag in den Systeminformationen ist vorhanden, wenn diese Funktion aufgerufen wird, gibt die Funktion "false".  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLRemoveTranslator** gibt "false", ein zugeordnetes  *\*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Beschreibung|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die gab es keine bestimmte Installer-Fehlers.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Komponente wurde in der Registrierung nicht gefunden.|Das Installationsprogramm konnte die Translator-Informationen nicht entfernt, da sie in der Registrierung nicht vorhanden noch oder nicht in der Registrierung gefunden werden konnte.|  
|ODBC_ERROR_INVALID_NAME|Ungültiger Name für Treiber oder das Konvertierungsprogramm|Die *LpszTranslator* Argument war ungültig.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Konnte nicht inkrementiert oder dekrementiert werden die Verwendungsanzahl der Komponente|Fehler des Installationsprogramms, um die Verwendungsanzahl des Treibers zu verringern.|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund von unzureichendem Speicher nicht ausgeführt werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLRemoveTranslator** ergänzt die [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md) -Funktion und Updates zählen die Verwendung von Komponenten in den Systeminformationen. Diese Funktion sollte nur von einem Setup-Anwendung aufgerufen werden.  
  
 **SQLRemoveTranslator** die Verwendungsanzahl der Komponente wird um 1 verringert wird. Wenn die Anzahl der Zugriffe auf 0 zurückgeht, wird der Translator-Eintrag in den Systeminformationen entfernt. Der Translator-Eintrag ist an folgendem Speicherort in den Systeminformationen, unter der Translator-Name:  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator** Dateien wird nicht tatsächlich entfernt. Das aufrufende Programm ist verantwortlich für die Dateien werden gelöscht und die Verwendungsanzahl der Datei. Nur nachdem, sowohl die Verwendungsanzahl der Komponente als auch die Verwendungsanzahl der Datei erreicht haben 0 (null) eine Datei physisch gelöscht ist. Einige Dateien in einer Komponente können gelöscht werden, und andere nicht gelöscht, je nachdem, ob die Dateien von anderen Anwendungen verwendet werden, die die Anzahl der Dateien Nutzung erhöht haben.  
  
 **SQLRemoveTranslator** wird auch als Teil eines Upgradevorgangs bezeichnet. Wenn eine Anwendung erkennt, dass sie ein Upgrade durchführen und den Treiber wurde bereits installierte, sollte der Treiber entfernt und anschließend neu installiert werden. **SQLRemoveTranslator** zuerst aufgerufen werden, um verringern die Verwendungsanzahl der Komponente, und klicken Sie dann **SQLInstallTranslatorEx** aufgerufen werden, um die Verwendungsanzahl der Komponente zu erhöhen. Das Installationsprogramm der Anwendung muss die alten Dateien physisch durch die neuen Dateien ersetzen. Die Verwendungsanzahl der Datei bleibt unverändert, und andere Anwendungen, die die älteren Versionsdateien verwenden jetzt die neuere Version verwenden.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Installieren einen Übersetzer|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
