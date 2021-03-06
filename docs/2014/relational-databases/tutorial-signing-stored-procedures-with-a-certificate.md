---
title: 'Tutorial: Signieren von gespeicherten Prozeduren mit einem Zertifikat | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- signing stored procedures tutorial [SQL Server]
ms.assetid: a4b0f23b-bdc8-425f-b0b9-e0621894f47e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: daf80492cd6a0d8040d1497e71600c798e7ef96c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "62524093"
---
# <a name="tutorial-signing-stored-procedures-with-a-certificate"></a>Tutorial: Signieren von gespeicherten Prozeduren mit einem Zertifikat
  In diesem Lernprogramm wird erläutert, wie gespeicherte Prozeduren mit einem Zertifikat signiert werden können, das von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]generiert wurde.  
  
> [!NOTE]  
>  Damit Sie den Code ausführen können, der in diesem Lernprogramm enthalten ist, müssen Sie die Sicherheit für den gemischte Modus konfiguriert und die [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] -Datenbank installiert haben. Szenario  
  
 Das Signieren einer gespeicherten Prozedur mit einem Zertifikat bietet sich an, wenn Berechtigungen für die gespeicherte Prozedur erforderlich sein sollen, Sie einem Benutzer diese Berechtigungen aber nicht explizit erteilen möchten. Zwar gibt es für das Ausführen dieser Aufgabe mehrere Möglichkeiten (z. B. können Sie die EXECUTE AS-Anweisung verwenden), das Verwenden eines Zertifikats ermöglicht aber das Verwenden einer Ablaufverfolgung, um die Person ausfindig zu machen, von der die gespeicherte Prozedur ursprünglich aufgerufen wurde. Auf diese Weise erreichen Sie ein hohes Maß an Überwachung, insbesondere bei der Sicherheit von DDL-Vorgängen (Data Definition Language, Datendefinitionssprache).  
  
 Sie können ein Zertifikat in der master-Datenbank erstellen, damit Berechtigungen auf Serverebene möglich sind. Sie können aber auch ein Zertifikat in einer beliebigen Benutzerdatenbank erstellen, damit Berechtigungen auf Datenbankebene möglich sind. In diesem Szenario muss ein Benutzer, der keine Berechtigungen für die Basistabellen hat, auf eine gespeicherte Prozedur in der [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] -Datenbank zugreifen. Außerdem soll in diesem Szenario der Objektzugriffspfad überwacht werden. Dazu erstellen Sie ein Server- und ein Datenbank-Benutzerkonto ohne Berechtigungen für die Basisobjekte sowie ein Datenbank-Benutzerkonto, das Berechtigungen für eine Tabelle und eine gespeicherte Prozedur hat. Andere Methoden für Besitzketten werden nicht verwendet. Sowohl die gespeicherte Prozedur als auch das zweite Datenbank-Benutzerkonto werden mit einem Zertifikat gesichert. Das zweite Datenbank-Benutzerkonto hat Zugriff auf alle Objekte und erteilt dem ersten Datenbank-Benutzerkonto die Berechtigung zum Zugreifen auf die gespeicherte Prozedur.  
  
 In diesem Szenario erstellen Sie zunächst ein Datenbankzertifikat, eine gespeicherte Prozedur und einen Benutzer. Anschließend testen Sie den Prozess durch Ausführen der folgenden Schritte:  
  
1.  Konfigurieren der Umgebung.  
  
2.  Erstellen eines Zertifikats.  
  
3.  Erstellen einer gespeicherten Prozedur und Signieren der Prozedur mithilfe des Zertifikats.  
  
4.  Erstellen eines Zertifikatkontos mithilfe des Zertifikats.  
  
5.  Erteilen der Datenbankberechtigungen für das Zertifikatkonto.  
  
6.  Anzeigen des Zugriffskontexts.  
  
7.  Zurücksetzen der Umgebung.  
  
 Jeder Codeblock dieses Beispiels wird jeweils sofort erläutert. Informationen, wie Sie das vollständige Beispiel kopieren können, finden Sie unter [Vollständiges Beispiel](#CompleteExample) am Ende dieses Lernprogramms.  
  
## <a name="1-configure-the-environment"></a>1. Konfigurieren der Umgebung  
 Zum Festlegen des Anfangskontexts für das Beispiel öffnen Sie in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] eine neue Abfrage und führen den folgenden Code aus, um die [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] -Datenbank zu öffnen. Dieser Code ändert den Datenbankkontext zu `AdventureWorks2012` und erstellt eine neue Serveranmeldung sowie ein neues Datenbank-Benutzerkonto (`TestCreditRatingUser`), wobei ein Kennwort verwendet wird.  
  
```  
USE AdventureWorks2012;  
GO  
-- Set up a login for the test user  
CREATE LOGIN TestCreditRatingUser  
   WITH PASSWORD = 'ASDECd2439587y'  
GO  
CREATE USER TestCreditRatingUser  
FOR LOGIN TestCreditRatingUser;  
GO  
```  
  
 Weitere Informationen zur CREATE USER-Anweisung finden Sie unter [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql). Weitere Informationen zur CREATE LOGIN-Anweisung finden Sie unter [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql).  
  
## <a name="2-create-a-certificate"></a>2. Erstellen eines Zertifikats  
 Zertifikate können Sie auf dem Server erstellen, indem Sie die master-Datenbank, eine Benutzerdatenbank oder beide als Kontext verwenden. Für das Sichern eines Zertifikats gibt es mehrere Optionen. Weitere Informationen zum Erstellen eines Zertifikats finden Sie unter [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql).  
  
 Führen Sie den folgenden Code aus, um ein Datenbankzertifikat zu erstellen und mit einem Kennwort zu sichern.  
  
```  
CREATE CERTIFICATE TestCreditRatingCer  
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
      WITH SUBJECT = 'Credit Rating Records Access',   
      EXPIRY_DATE = '12/05/2014';  
GO  
```  
  
## <a name="3-create-and-sign-a-stored-procedure-using-the-certificate"></a>3. Erstellen einer gespeicherten Prozedur und Signieren der Prozedur mithilfe des Zertifikats  
 Erstellen Sie mit dem folgenden Code eine gespeicherte Prozedur, die Daten aus der `Vendor` -Tabelle `Purchasing` -Datenbankschema auswählt, wobei der Zugriff auf Unternehmen beschränkt wird, die die Bonität (CreditRating) 1 haben. Der erste Abschnitt der gespeicherten Prozedur zeigt den Kontext des Benutzerkontos an, unter dem die gespeicherte Prozedur ausgeführt wird. Hiermit sollen lediglich die Konzepte verdeutlicht werden. Es ist nicht erforderlich, die Anforderungen zu erfüllen.  
  
```  
CREATE PROCEDURE TestCreditRatingSP  
AS  
BEGIN  
   -- Show who is running the stored procedure  
   SELECT SYSTEM_USER 'system Login'  
   , USER AS 'Database Login'  
   , NAME AS 'Context'  
   , TYPE  
   , USAGE   
   FROM sys.user_token     
  
   -- Now get the data  
   SELECT AccountNumber, Name, CreditRating   
   FROM Purchasing.Vendor  
   WHERE CreditRating = 1  
END  
GO  
```  
  
 Führen Sie den folgenden Code aus, um die gespeicherte Prozedur mit dem Datenbankzertifikat zu signieren und dazu ein Kennwort zu verwenden.  
  
```  
ADD SIGNATURE TO TestCreditRatingSP   
   BY CERTIFICATE TestCreditRatingCer  
    WITH PASSWORD = 'pGFD4bb925DGvbd2439587y';  
GO  
```  
  
 Weitere Informationen zum Aufrufen von gespeicherten Prozeduren finden Sie unter [Gespeicherte Prozeduren &#40;Datenbank-Engine&#41;](stored-procedures/stored-procedures-database-engine.md).  
  
 Weitere Informationen zum Signieren von gespeicherten Prozeduren finden Sie unter [ADD SIGNATURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/add-signature-transact-sql).  
  
## <a name="4-create-a-certificate-account-using-the-certificate"></a>4. Erstellen eines Zertifikatkontos mithilfe des Zertifikats  
 Führen Sie den folgenden Code aus, um über das Zertifikat einen Datenbankbenutzer (`TestCreditRatingcertificateAccount`) zu erstellen. Das Konto hat keine Serveranmeldung und steuert ausschließlich den Zugriff auf die zugrunde liegenden Tabellen.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE USER TestCreditRatingcertificateAccount  
   FROM CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
## <a name="5-grant-the-certificate-account-database-rights"></a>5. Erteilen der Datenbankberechtigungen für das Zertifikatkonto  
 Führen Sie den folgenden Code aus, damit `TestCreditRatingcertificateAccount` die Berechtigungen für die Basistabellen und die gespeicherte Prozedur erteilt werden.  
  
```  
GRANT SELECT   
   ON Purchasing.Vendor   
   TO TestCreditRatingcertificateAccount;  
GO  
  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingcertificateAccount;  
GO  
```  
  
 Weitere Informationen zum Erteilen von Berechtigungen für Objekte finden Sie unter [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql).  
  
## <a name="6-display-the-access-context"></a>6. Anzeigen des Zugriffskontexts  
 Damit die Berechtigungen angezeigt werden können, die mit dem Zugriff über die gespeicherte Prozedur verknüpft sind, führen Sie den folgenden Code aus. Der Code erteilt dem Benutzer `TestCreditRatingUser` die Berechtigung, die gespeicherte Prozedur auszuführen.  
  
```  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingUser;  
GO  
```  
  
 Führen Sie nun den folgenden Code aus, um die gespeicherte Prozedur mit der dbo-Anmeldung auszuführen, die Sie auf dem Server verwendet haben. Sehen Sie sich die Informationen an, die für den Benutzerkontext ausgegeben wurden. Die Informationen zeigen, dass das Konto dbo der Kontext mit seinen eigenen Berechtigungen ist, die Berechtigungen also nicht über eine Gruppenmitgliedschaft erteilt wurden.  
  
```  
EXECUTE TestCreditRatingSP;  
GO  
```  
  
 Führen Sie den folgenden Code aus. In dem Code wird die `EXECUTE AS` -Anweisung dazu verwendet, die gespeicherte Prozedur unter dem Konto `TestCreditRatingUser` auszuführen. Diesmal ist zu sehen, dass der Kontext auf den USER MAPPED TO CERTIFICATE-Kontext (Einem Zertifikat zugeordneter Datenbankbenutzer) festgelegt ist.  
  
```  
EXECUTE AS LOGIN = 'TestCreditRatingUser';  
GO  
EXECUTE TestCreditRatingSP;  
GO  
```  
  
 Auf diese Weise wird die Überwachung demonstriert, die verfügbar ist, weil Sie die gespeicherte Prozedur signiert haben.  
  
> [!NOTE]  
>  Verwenden Sie EXECUTE AS zum Wechseln des Kontexts in einer Datenbank.  
  
## <a name="7-reset-the-environment"></a>7. Zurücksetzen der Umgebung  
 Im folgenden Code wird die `REVERT`-Anweisung verwendet, um den Kontext des aktuellen Kontos auf dbo zurückzusetzen, und dann die Umgebung zurückgesetzt.  
  
```  
REVERT;  
GO  
DROP PROCEDURE TestCreditRatingSP;  
GO  
DROP USER TestCreditRatingcertificateAccount;  
GO  
DROP USER TestCreditRatingUser;  
GO  
DROP LOGIN TestCreditRatingUser;  
GO  
DROP CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
 Weitere Informationen zur REVERT-Anweisung finden Sie unter [REVERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/revert-transact-sql).  
  
##  <a name="CompleteExample"></a> Vollständiges Beispiel  
 In diesem Abschnitt wird der vollständige Beispielcode angezeigt.  
  
```  
/* Step 1 - Open the AdventureWorks2012 database */  
USE AdventureWorks2012;  
GO  
-- Set up a login for the test user  
CREATE LOGIN TestCreditRatingUser  
   WITH PASSWORD = 'ASDECd2439587y'  
GO  
CREATE USER TestCreditRatingUser  
FOR LOGIN TestCreditRatingUser;  
GO  
  
/* Step 2 - Create a certificate in the AdventureWorks2012 database */  
CREATE CERTIFICATE TestCreditRatingCer  
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
      WITH SUBJECT = 'Credit Rating Records Access',   
      EXPIRY_DATE = '12/05/2014';  
GO  
  
/* Step 3 - Create a stored procedure and  
sign it using the certificate */  
CREATE PROCEDURE TestCreditRatingSP  
AS  
BEGIN  
   -- Shows who is running the stored procedure  
   SELECT SYSTEM_USER 'system Login'  
   , USER AS 'Database Login'  
   , NAME AS 'Context'  
   , TYPE  
   , USAGE   
   FROM sys.user_token;     
  
   -- Now get the data  
   SELECT AccountNumber, Name, CreditRating   
   FROM Purchasing.Vendor  
   WHERE CreditRating = 1;  
END  
GO  
  
ADD SIGNATURE TO TestCreditRatingSP   
   BY CERTIFICATE TestCreditRatingCer  
    WITH PASSWORD = 'pGFD4bb925DGvbd2439587y';  
GO  
  
/* Step 4 - Create a database user for the certificate.   
This user has the ownership chain associated with it. */  
USE AdventureWorks2012;  
GO  
CREATE USER TestCreditRatingcertificateAccount  
   FROM CERTIFICATE TestCreditRatingCer;  
GO  
  
/* Step 5 - Grant the user database rights */  
GRANT SELECT   
   ON Purchasing.Vendor   
   TO TestCreditRatingcertificateAccount;  
GO  
  
GRANT EXECUTE  
   ON TestCreditRatingSP   
   TO TestCreditRatingcertificateAccount;  
GO  
  
/* Step 6 - Test, using the EXECUTE AS statement */  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingUser;  
GO  
  
-- Run the procedure as the dbo user, notice the output for the type  
EXEC TestCreditRatingSP;  
GO  
  
EXECUTE AS LOGIN = 'TestCreditRatingUser';  
GO  
EXEC TestCreditRatingSP;  
GO  
  
/* Step 7 - Clean up the example */  
REVERT;  
GO  
DROP PROCEDURE TestCreditRatingSP;  
GO  
DROP USER TestCreditRatingcertificateAccount;  
GO  
DROP USER TestCreditRatingUser;  
GO  
DROP LOGIN TestCreditRatingUser;  
GO  
DROP CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheitscenter für SQL Server-Datenbank-Engine und Azure SQL-Datenbank](security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
