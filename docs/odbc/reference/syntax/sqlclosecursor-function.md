---
title: SQLCloseCursor-Funktion | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCloseCursor
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLCloseCursor
helpviewer_keywords:
- SQLCloseCursor function [ODBC]
ms.assetid: 05b0a054-e28d-4e16-b5b0-07418486b372
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ef336a4deb734c0e44f9c15ae7f9faf0dcb32d93
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343146"
---
# <a name="sqlclosecursor-function"></a>SQLCloseCursor-Funktion
**Konformitäts**  
 Eingeführte Version: Konformität der ODBC 3,0-Standards: ISO 92  
  
 **Zusammenfassung**  
 **SQLCloseCursor** schließt einen Cursor, der für eine-Anweisung geöffnet wurde, und verwirft ausstehende Ergebnisse.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
  
SQLRETURN SQLCloseCursor(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 Der Anweisungs Handle.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLCloseCursor** "SQL_ERROR" oder "SQL_SUCCESS_WITH_INFO" zurückgibt, kann ein zugeordneter SQLSTATE-Wert durch Aufrufen von **SQLGetDiagRec** mit dem *Typ* "SQL_HANDLE_STMT" und einem *handle* von " *StatementHandle*" abgerufen werden. In der folgenden Tabelle werden die SQLSTATE-Werte aufgelistet, die häufig von **SQLCloseCursor** zurückgegeben werden, und die einzelnen Werte werden im Kontext dieser Funktion erläutert. die Notation "(DM)" geht vor den Beschreibungen von Sqlstates vor, die vom Treiber-Manager zurückgegeben werden. Der Rückgabecode, der den einzelnen SQLSTATE-Werten zugeordnet ist, lautet SQL_ERROR, sofern nichts anderes angegeben ist.  
  
|SQLSTATE|Fehler|Beschreibung|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiber spezifische Informations Meldung. (Die Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|24000|Ungültiger Cursorstatus|Für " *StatementHandle*" war kein Cursor geöffnet. (Dies wird nur von ODBC 3 zurückgegeben. *x* -Treiber.)|  
|HY000|Allgemeiner Fehler|Es ist ein Fehler aufgetreten, bei dem kein spezifischer SQLSTATE vorhanden war und für den kein Implementierungs spezifischer SQLSTATE definiert wurde. Die von **SQLGetDiagRec** im  *\*MessageText* -Puffer zurückgegebene Fehlermeldung beschreibt den Fehler und die Ursache.|  
|HY001|Fehler bei der Speicher Belegung|Der Treiber konnte keinen Arbeitsspeicher zuweisen, der zur Unterstützung der Ausführung oder Beendigung der Funktion erforderlich ist.|  
|HY010|Funktions Sequenz Fehler|(DM) eine asynchron ausgeführte Funktion wurde für das dem *StatementHandle* zugeordnete Verbindungs Handle aufgerufen und ausgeführt, als diese Funktion aufgerufen wurde.<br /><br /> (DM) eine asynchron ausgeführte Funktion wurde für das *StatementHandle* aufgerufen und ausgeführt, als diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, die *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor Daten für alle Data-at-Execution-Parameter oder-Spalten gesendet wurden.|  
|HY013|Speicher Verwaltungsfehler|Der Funktions Aufrufwert konnte nicht verarbeitet werden, da auf die zugrunde liegenden Speicher Objekte nicht zugegriffen werden konnte, möglicherweise aufgrund von wenig Arbeitsspeicher.|  
|HY117|Die Verbindung wurde aufgrund eines unbekannten Transaktions Zustands angehalten. Nur Disconnect-und Read-Only-Funktionen sind zulässig.|(DM) Weitere Informationen zum angehaltenen Status finden Sie unter [SQLEndTran Function](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungs Timeout abgelaufen|Der Verbindungs Timeout Zeitraum ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Der Timeout Zeitraum für die Verbindung wird über **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT festgelegt.|  
|IM001|Der Treiber unterstützt diese Funktion nicht.|(DM) der dem *StatementHandle* zugeordnete Treiber unterstützt die-Funktion nicht.|  
  
## <a name="comments"></a>Kommentare  
 **SQLCloseCursor** gibt SQLSTATE 24000 (Ungültiger Cursor Zustand) zurück, wenn kein Cursor geöffnet ist. Das Aufrufen von **SQLCloseCursor** entspricht dem Aufrufen von **SQLFreeStmt** mit der SQL_CLOSE-Option, mit der Ausnahme, dass **SQLFreeStmt** mit SQL_CLOSE keine Auswirkung auf die Anwendung hat, wenn kein Cursor in der Anweisung geöffnet ist, während  **SQLCloseCursor** gibt SQLSTATE 24000 (Ungültiger Cursor Zustand) zurück.  
  
> [!NOTE]  
>  Wenn eine ODBC-3. *x* Anwendung mit einer ODBC 2. *X* Treiber ruft **SQLCloseCursor** , wenn kein Cursor geöffnet ist, ist SQLSTATE 24000 (Ungültiger Cursorstatus) wird nicht zurückgegeben, da der Treiber-Manager zugeordnet **SQLCloseCursor** zu **SQLFreeStmt** mit SQL_CLOSE.  
  
 Weitere Informationen finden Sie unter [Schließen des Cursors](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
## <a name="code-example"></a>Codebeispiel  
 Weitere Informationen finden Sie unter [sqlbrowseconnetct-Funktion](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) und [SQLCONNECT-Funktion](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Abbrechen der Anweisungs Verarbeitung|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Freigeben eines Handles|[SQLFreeHandle-Funktion](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Verarbeiten mehrerer Resultsets|[SQLMoreResults-Funktion](../../../odbc/reference/syntax/sqlmoreresults-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
