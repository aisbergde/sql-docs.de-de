---
title: CREATE ENDPOINT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENDPOINT
- CREATE ENDPOINT
- ENDPOINT_TSQL
- CREATE_ENDPOINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], endpoint
- HTTP SOAP support [SQL Server]
- CREATE ENDPOINT statement
- Availability Groups [SQL Server], configuring
- endpoints [SQL Server], creating
- SOAP [SQL Server built-in support], endpoints
- SOAP [SQL Server built-in support], sqlbatch
- DATABASE_MIRRORING option
- HTTP protocol option [SQL Server]
- SOAP [SQL Server built-in support], ad hoc
- TCP protocol option [SQL Server]
- SERVICE_BROKER option
- Availability Groups [SQL Server], endpoint
ms.assetid: 6405e7ec-0b5b-4afd-9792-1bfa5a2491f6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0a320b01433ad95f4bd695a3f700b7e7bb9ba653
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902825"
---
# <a name="create-endpoint-transact-sql"></a>CREATE ENDPOINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt Endpunkte und definiert deren Eigenschaften, einschließlich der für Clientanwendungen verfügbaren Methoden. Weitere Informationen zu entsprechenden Berechtigungen finden Sie unter [GRANT (Endpunktberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md).  
  
 Die Syntax für CREATE ENDPOINT kann logisch in zwei Komponenten unterteilt werden:  
  
-   Die erste Komponente beginnt mit AS und endet vor der FOR-Klausel.  
  
     Hier geben Sie Informationen zum Transportprotokoll (TCP) an und legen eine Überwachungsportnummer für den Endpunkt fest sowie die Methode der Endpunktauthentifizierung und/oder eine Liste der IP-Adressen (sofern vorhanden), die vom Zugriff auf den Endpunkt ausgenommen werden sollen.  
  
-   Die zweite Komponente beginnt mit der FOR-Klausel.  
  
     Hier definieren Sie die Nutzlast, die auf dem Endpunkt unterstützt wird. Für die Nutzlast sind folgende unterstützte Typen möglich: [!INCLUDE[tsql](../../includes/tsql-md.md)], Service Broker und Datenbankspiegelung. Außerdem geben Sie hier sprachspezifische Informationen ein.  
  
> **HINWEIS:** Systemeigene XML-Webdienste (SOAP-/HTTP-Endpunkte) wurden in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] entfernt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Themenlinksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE ENDPOINT endPointName [ AUTHORIZATION login ]  
[ STATE = { STARTED | STOPPED | DISABLED } ]  
AS { TCP } (  
   <protocol_specific_arguments>  
        )  
FOR { TSQL | SERVICE_BROKER | DATABASE_MIRRORING } (  
   <language_specific_arguments>  
        )  
  
<AS TCP_protocol_specific_arguments> ::=  
AS TCP (  
  LISTENER_PORT = listenerPort  
  [ [ , ] LISTENER_IP = ALL | ( xx.xx.xx.xx IPv4 address ) | ( '__:__1' IPv6 address ) ]  
  
)  
  
<FOR SERVICE_BROKER_language_specific_arguments> ::=  
FOR SERVICE_BROKER (  
   [ AUTHENTICATION = {   
            WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
      | CERTIFICATE certificate_name   
      | WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ] CERTIFICATE certificate_name   
      | CERTIFICATE certificate_name WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
    } ]  
   [ [ , ] ENCRYPTION = { DISABLED | { { SUPPORTED | REQUIRED }   
       [ ALGORITHM { AES | RC4 | AES RC4 | RC4 AES } ] }   
   ]  
   [ [ , ] MESSAGE_FORWARDING = { ENABLED | DISABLED } ]  
   [ [ , ] MESSAGE_FORWARD_SIZE = forward_size ]  
)  
  

<FOR DATABASE_MIRRORING_language_specific_arguments> ::=  
FOR DATABASE_MIRRORING (  
   [ AUTHENTICATION = {   
            WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
      | CERTIFICATE certificate_name   
      | WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ] CERTIFICATE certificate_name   
      | CERTIFICATE certificate_name WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
   [ [ [ , ] ] ENCRYPTION = { DISABLED | { { SUPPORTED | REQUIRED }   
       [ ALGORITHM { AES | RC4 | AES RC4 | RC4 AES } ] }   
  
    ]   
   [ , ] ROLE = { WITNESS | PARTNER | ALL }  
)  
```  
  
## <a name="arguments"></a>Argumente  
 *endPointName*  
 Der zugewiesene Name für den Endpunkt, den Sie erstellen. Verwenden Sie diesen Namen zum Aktualisieren oder Löschen des Endpunktes.  
  
 AUTHORIZATION *login*  
 Gibt einen gültigen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]- oder Windows-Anmeldenamen an, dem der Besitz des neu erstellen Endpunktobjekts zugewiesen wird. Falls AUTHORIZATION nicht angegeben ist, wird standardmäßig der Aufrufer zum Besitzer des neu erstellten Objekts.  
  
 Zum Zuweisen des Besitzes mithilfe von AUTHORIZATION benötigt der Aufrufer die IMPERSONATE-Berechtigung für den angegebenen *login*-Parameter.  
  
 Informationen zum Neuzuweisen des Besitzes finden Sie unter [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md).  
  
 STATE **=** { STARTED | **STOPPED** | DISABLED }  
 Der Status des Endpunktes beim Erstellen. Falls der Status beim Erstellen des Endpunktes nicht angegeben wird, ist der Standardwert STOPPED.  
  
 STARTED  
 Der Endpunkt wird gestartet und überwacht aktiv Verbindungen.  
  
 DISABLED  
 Der Endpunkt ist deaktiviert. In diesem Status lauscht der Server nach Portanforderungen, gibt jedoch Fehler an Clients zurück.  
  
 **STOPPED**  
 Der Endpunkt wird beendet. In diesem Status lauscht der Server nicht am Endpunktport und beantwortet keine Anforderungsversuche zum Verwenden des Endpunkts.  
  
 Informationen zum Ändern des Status finden Sie unter [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md).  
  
 AS { TCP }  
 Gibt das zu verwendende Transportprotokoll an.  
  
 FOR { TSQL | SERVICE_BROKER | DATABASE_MIRRORING }  
 Gibt den Nutzlasttyp an.  
  
 Aktuell gibt es keine [!INCLUDE[tsql](../../includes/tsql-md.md)]-sprachspezifischen Argumente, die im `<language_specific_arguments>`-Parameter übergeben werden.  
  
 **TCP-Protokolloption**  
  
 Die folgenden Argumente gelten nur für die TCP-Option.  
  
 LISTENER_PORT **=** _listenerPort_  
 Gibt die Portnummer an, die für Verbindungen vom Service Broker-TCP/IP überwacht wird. Gemäß der Konvention wird 4022 verwendet, aber jede Zahl zwischen 1024 und 32767 ist gültig.  
  
 LISTENER_IP **=** ALL | **(** _4-part-ip_ **)**  |  **(** "*IP-Adresse_V6*" **)**  
 Gibt die IP-Adresse an, auf der der Endpunkt lauscht. Der Standardwert ist ALL. Das bedeutet, dass die Überwachung lässt eine Verbindung an einer gültigen IP-Adresse zulässt.  
  
 Wenn Sie die Datenbankspiegelung mit einer IP-Adresse anstelle eines vollqualifizierten Domänennamens (`ALTER DATABASE SET PARTNER = partner_IP_address` oder `ALTER DATABASE SET WITNESS = witness_IP_address`) konfigurieren, müssen Sie beim Erstellen von Spiegelungsendpunkten `LISTENER_IP =IP_address` anstelle von `LISTENER_IP=ALL` angeben.  
  
 **Die Optionen SERVICE_BROKER und DATABASE_MIRRORING**  
  
 Die folgenden AUTHENTICATION- und ENCRYPTION-Argumente werden von den Optionen SERVICE_BROKER und DATABASE_MIRRORING gemeinsam verwendet.  
  
> [!NOTE]  
>  Optionen, die für SERVICE_BROKER spezifisch sind, finden Sie im Abschnitt zu den Optionen für SERVICE_BROKER weiter unten. Optionen, die für DATABASE_MIRRORING spezifisch sind, finden Sie im Abschnitt zu den Optionen für DATABASE_MIRRORING weiter unten.  
  
 AUTHENTICATION **=** \<authentication_options> gibt die TCP/IP-Authentifizierungsanforderungen für Verbindungen für diesen Endpunkt an. Der Standardwert ist WINDOWS.  
  
 Zu den unterstützten Authentifizierungsmethoden zählen NTLM und/oder Kerberos.  
  
> [!IMPORTANT]  
>  Alle Spiegelungsverbindungen auf einer Serverinstanz verwenden einen gemeinsamen Datenbankspiegelungsendpunkt. Jeder Versuch, einen zusätzlichen Datenbankspiegelungsendpunkt zu erstellen, ist fehlerhaft.  
  
 **\<authentication_options> ::=**  
  
 **WINDOWS** [ { NTLM | KERBEROS | **NEGOTIATE** } ]  
 Gibt an, dass der Endpunkt mithilfe des Windows-Authentifizierungsprotokolls die Endpunkte authentifizieren soll. Dies ist die Standardeinstellung.  
  
 Wenn Sie eine Autorisierungsmethode angeben (NTLM oder KERBEROS), wird immer diese Methode als Authentifizierungsprotokoll verwendet. Mit dem Standardwert NEGOTIATE verwendet der Endpunkt das Windows-Aushandlungsprotokoll, um NTLM oder Kerberos auszuwählen.  
  
 CERTIFICATE *certificate_name*  
 Gibt an, dass der Endpunkt die Verbindung mithilfe des von *certificate_name* angegebenen Zertifikats authentifizieren soll, um die Identität für die Autorisierung einzurichten. Der entfernte Endpunkt benötigt ein Zertifikat, dessen öffentlicher Schlüssel mit dem privaten Schlüssel des angegebenen Zertifikats übereinstimmt.  
  
 WINDOWS [ { NTLM | KERBEROS | **NEGOTIATE** } ] CERTIFICATE *certificate_name*  
 Gibt an, dass der Endpunkt mithilfe der Windows-Authentifizierung eine Verbindung herstellen soll. Falls dies nicht möglich ist, soll das angegebene Zertifikat verwendet werden.  
  
 CERTIFICATE *certificate_name* WINDOWS [ { NTLM | KERBEROS | **NEGOTIATE** } ]  
 Gibt an, dass der Endpunkt mithilfe des angegebenen Zertifikats eine Verbindung herstellen soll. Falls dies nicht möglich ist, soll die Windows-Authentifizierung verwendet werden.  
  
 ENCRYPTION = { DISABLED | SUPPORTED | **REQUIRED** } [ALGORITHM { **AES** | RC4 | AES RC4 | RC4 AES } ]  
 Gibt an, ob die Verschlüsselung für den Prozess verwendet wird. Der Standardwert ist REQUIRED.  
  
 DISABLED  
 Gibt an, dass über eine Verbindung gesendete Daten nicht verschlüsselt werden.  
  
 SUPPORTED  
 Gibt an, dass die Daten nur verschlüsselt werden, wenn der gegenüberliegende Endpunkt SUPPORTED oder REQUIRED angibt.  
  
 REQUIRED  
 Gibt an, dass für Verbindungen mit diesem Endpunkt die Verschlüsselung verwendet werden muss. Zum Herstellen einer Verbindung mit diesem Endpunkt muss deshalb für einen anderen Endpunkt ENCRYPTION auf SUPPORTED oder REQUIRED festgelegt sein.  
  
 Optional können Sie mit dem ALGORITHM-Argument die Form der vom Endpunkt verwendeten Verschlüsselung folgendermaßen angeben:  
  
 **AES**  
 Gibt an, dass der Endpunkt den AES-Algorithmus verwenden muss. In [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] und höher ist dies die Standardeinstellung.  
  
 RC4  
 Gibt an, dass der Endpunkt den RC4-Algorithmus verwenden muss. Dies ist bis [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] die Standardeinstellung.  
  
> [!NOTE]  
>  Der RC4-Algorithmus wird nur aus Gründen der Abwärtskompatibilität unterstützt. Neues Material kann nur mit RC4 oder RC4_128 verschlüsselt werden, wenn die Datenbank den Kompatibilitätsgrad 90 oder 100 besitzt. (Nicht empfohlen.) Verwenden Sie stattdessen einen neueren Algorithmus, z. B. einen der AES-Algorithmen. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und höheren Versionen kann mit RC4 oder RC4_128 verschlüsseltes Material in jedem Kompatibilitätsgrad entschlüsselt werden.  
  
 AES RC4  
 Gibt an, dass die beiden Endpunkte einen Verschlüsselungsalgorithmus aushandeln, wobei dieser Endpunkt dem AES-Algorithmus den Vorzug gibt.  
  
 RC4 AES  
 Gibt an, dass die beiden Endpunkte einen Verschlüsselungsalgorithmus aushandeln, wobei dieser Endpunkt dem RC4-Algorithmus den Vorzug gibt.  
  
> [!NOTE]  
>  Der RC4-Algorithmus ist veraltet. [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Stattdessen wird die Verwendung von AES empfohlen.  
  
 Wenn beide Endpunkte beide Algorithmen angeben, jedoch in unterschiedlicher Reihenfolge, gewinnt der Endpunkt, der die Verbindung annimmt.  
  
 **Optionen für SERVICE_BROKER**  
  
 Die folgenden Argumente gelten nur für die Option SERVICE_BROKER.  
  
 MESSAGE_FORWARDING **=** { ENABLED | **DISABLED** }  
 Bestimmt, ob von diesem Endpunkt empfangene Nachrichten für externe Dienste weitergeleitet werden.  
  
 ENABLED  
 Nachrichten werden weitergeleitet, falls eine Weiterleitungsadresse verfügbar ist.  
  
 DISABLED  
 Nachrichten für externe Dienste werden verworfen. Dies ist die Standardeinstellung.  
  
 MESSAGE_FORWARD_SIZE **=** _Weiterleitungsgröße_  
 Gibt an, wie viel Speicherplatz dem Endpunkt zum Speichern weiterzuleitender Nachrichten maximal in MB zugeordnet werden soll.  
  
 **Optionen für DATABASE_MIRRORING**  
  
 Das folgende Argument gilt nur für die Option DATABASE_MIRRORING.  
  
 ROLE **=** { WITNESS | PARTNER | ALL }  
 Gibt die Datenbank-Spiegelungsrollen an, die vom Endpunkt unterstützt werden.  
  
 WITNESS  
 Ermöglicht es dem Endpunkt, die Rolle eines Zeugen beim Spiegelungsprozess einzunehmen.  
  
> [!NOTE]  
>  Für [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] ist WITNESS die einzige verfügbare Option.  
  
 PARTNER  
 Ermöglicht es dem Endpunkt, die Rolle eines Partners beim Spiegelungsprozess einzunehmen.  
  
 ALL  
 Ermöglicht es dem Endpunkt, die Rolle eines Zeugen und eines Partners beim Spiegelungsprozess einzunehmen.  
  
 Weitere Informationen zu diesen Rollen finden Sie unter [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
> [!NOTE]  
>  Für DATABASE_MIRRORING ist kein Standardport vorhanden.  
  
## <a name="remarks"></a>Bemerkungen  
 ENDPOINT DDL-Anweisungen können nicht innerhalb einer Benutzertransaktion ausgeführt werden. ENDPOINT DDL-Anweisungen sind nicht fehlerhaft, selbst wenn eine aktive Momentaufnahmeisolationsstufen-Transaktion den Endpunkt verwendet, der geändert wird.  
  
 Folgende Personen können Anforderungen für ein ENDPOINT-Objekt ausführen:  
  
-   Mitglieder der festen Serverrolle **sysadmin**  
  
-   Der Besitzer des Endpunktes.  
  
-   Benutzer oder Gruppen, denen die CONNECT-Berechtigung für den Endpunkt erteilt wurde.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CREATE ENDPOINT-Berechtigung oder die Mitgliedschaft in der festen Serverrolle **sysadmin** . Weitere Informationen finden Sie unter [GRANT (Endpunktberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md).  
  
## <a name="example"></a>Beispiel  
  
### <a name="creating-a-database-mirroring-endpoint"></a>Erstellen eines Endpunktes für die Datenbankspiegelung  
 Im folgenden Beispiel wird ein Endpunkt für die Datenbankspiegelung erstellt. Der Endpunkt verwendet die Portnummer `7022`, wobei jede verfügbare Portnummer verwendet werden könnte. Für den Endpunkt ist die Windows-Authentifizierung nur mit Kerberos konfiguriert. Für die Option `ENCRYPTION` ist der Wert `SUPPORTED` konfiguriert (dies entspricht nicht dem Standardwert), um verschlüsselte oder unverschlüsselte Daten zu unterstützen. Für den Endpunkt wird die Unterstützung der Partner- und Zeugenrollen konfiguriert.  
  
```sql  
CREATE ENDPOINT endpoint_mirroring  
    STATE = STARTED  
    AS TCP ( LISTENER_PORT = 7022 )  
    FOR DATABASE_MIRRORING (  
       AUTHENTICATION = WINDOWS KERBEROS,  
       ENCRYPTION = SUPPORTED,  
       ROLE=ALL);  
GO  
```  

### <a name="create-a-new-endpoint-pointing-to-a-specific-ipv4-address-and-port"></a>Erstellen eines neuen Endpunkts, der auf eine bestimmte IPv4-Adresse und einen bestimmten Port verweist

```sql
CREATE ENDPOINT ipv4_endpoint_special
STATE = STARTED
AS TCP (
    LISTENER_PORT = 55555, LISTENER_IP = (10.0.75.1)
)
FOR TSQL ();

GRANT CONNECT ON ENDPOINT::[TSQL Default TCP] TO public; -- Keep existing public permission on default endpoint for demo purpose
GRANT CONNECT ON ENDPOINT::ipv4_endpoint_special
TO login_name;
```

### <a name="create-a-new-endpoint-pointing-to-a-specific-ipv6-address-and-port"></a>Erstellen eines neuen Endpunkts, der auf eine bestimmte IPv6-Adresse und einen bestimmten Port verweist

```sql
CREATE ENDPOINT ipv6_endpoint_special
STATE = STARTED
AS TCP (
    LISTENER_PORT = 55555, LISTENER_IP = ('::1')
)
FOR TSQL ();

GRANT CONNECT ON ENDPOINT::[TSQL Default TCP] TO public;
GRANT CONNECT ON ENDPOINT::ipv6_endpoint_special

```
  
## <a name="see-also"></a>Siehe auch  
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [Auswählen eines Verschlüsselungsalgorithmus](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [DROP ENDPOINT (Transact-SQL)](../../t-sql/statements/drop-endpoint-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

