---
title: Verschlüsseln einer Datenspalte | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/02/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], columns
- cryptography [SQL Server], columns
- column level encryption
- cell level encryption
ms.assetid: 38e9bf58-10c6-46ed-83cb-e2d76cda0adc
author: aliceku
ms.author: aliceku
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 11f30f1f2d4d3435c66792a462ba277fd00350f7
ms.sourcegitcommit: 949e55b32eff6610087819a93160a35af0c5f1c9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/05/2019
ms.locfileid: "70383523"
---
# <a name="encrypt-a-column-of-data"></a>Verschlüsseln einer Datenspalte
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  In diesem Artikel wird beschrieben, wie Sie eine Datenspalte mithilfe der symmetrischen Verschlüsselung in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[tsql](../../../includes/tsql-md.md)]verschlüsseln können. Dies wird manchmal als Verschlüsselung auf Spaltenebene oder Verschlüsselung auf Zellenebene bezeichnet.  

## <a name="security"></a>Security  
  
### <a name="permissions"></a>Berechtigungen  
 Die folgenden Berechtigungen sind notwendig, um die Schritte unten auszuführen:  
  
- CONTROL-Berechtigung für die Datenbank.  
  
- CREATE CERTIFICATE-Berechtigung für die Datenbank. Nur Windows-Anmeldenamen, SQL Server-Anmeldenamen und Anwendungsrollen können eigene Zertifikate besitzen. Gruppen und Rollen können keine Zertifikate besitzen.  
  
- ALTER-Berechtigung für die Tabelle.  
  
- Einige Berechtigungen für den Schlüssel und die VIEW DEFINITION-Berechtigung dürfen nicht verweigert worden sein.  
  
## <a name="using-transact-sql"></a>Verwenden von Transact-SQL  

Um die folgenden Beispiele verwenden zu können, müssen Sie über einen Datenbankhauptschlüssel verfügen. Wenn Ihre Datenbank noch nicht über einen Datenbank-Hauptschlüssel verfügt, führen Sie die folgende Anweisung aus, und geben Sie dabei Ihr Kennwort an, um einen solchen Schlüssel zu erstellen:

```sql  
CREATE MASTER KEY ENCRYPTION BY   
PASSWORD = '<some strong password>';  
```  

Erstellen Sie immer eine Sicherung Ihres Datenbankhauptschlüssels. Weitere Informationen zum Erstellen von Datenbank-Hauptschlüsseln finden Sie unter [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md).

### <a name="to-encrypt-a-column-of-data-using-symmetric-encryption-that-includes-an-authenticator"></a>So verschlüsseln Sie Datenspalten mithilfe der symmetrischen Verschlüsselung unter Einbeziehung eines Authentifikators  
  
1. Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../../includes/ssde-md.md)]-Instanz her.  
  
2. Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3. Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    ```sql
    USE AdventureWorks2012;  
    GO  
  
    CREATE CERTIFICATE Sales09  
       WITH SUBJECT = 'Customer Credit Card Numbers';  
    GO  
  
    CREATE SYMMETRIC KEY CreditCards_Key11  
        WITH ALGORITHM = AES_256  
        ENCRYPTION BY CERTIFICATE Sales09;  
    GO  
  
    -- Create a column in which to store the encrypted data.  
    ALTER TABLE Sales.CreditCard   
        ADD CardNumber_Encrypted varbinary(160);   
    GO  
  
    -- Open the symmetric key with which to encrypt the data.  
    OPEN SYMMETRIC KEY CreditCards_Key11  
       DECRYPTION BY CERTIFICATE Sales09;  
  
    -- Encrypt the value in column CardNumber using the  
    -- symmetric key CreditCards_Key11.  
    -- Save the result in column CardNumber_Encrypted.    
    UPDATE Sales.CreditCard  
    SET CardNumber_Encrypted = EncryptByKey(Key_GUID('CreditCards_Key11')  
        , CardNumber, 1, HashBytes('SHA1', CONVERT( varbinary  
        , CreditCardID)));  
    GO  
  
    -- Verify the encryption.  
    -- First, open the symmetric key with which to decrypt the data.  
  
    OPEN SYMMETRIC KEY CreditCards_Key11  
       DECRYPTION BY CERTIFICATE Sales09;  
    GO  
  
    -- Now list the original card number, the encrypted card number,  
    -- and the decrypted ciphertext. If the decryption worked,  
    -- the original number will match the decrypted number.  
  
    SELECT CardNumber, CardNumber_Encrypted   
        AS 'Encrypted card number', CONVERT(nvarchar,  
        DecryptByKey(CardNumber_Encrypted, 1 ,   
        HashBytes('SHA1', CONVERT(varbinary, CreditCardID))))  
        AS 'Decrypted card number' FROM Sales.CreditCard;  
    GO  
    ```  
  
### <a name="to-encrypt-a-column-of-data-using-a-simple-symmetric-encryption"></a>So verschlüsseln Sie eine Datenspalte mithilfe einer einfachen symmetrischen Verschlüsselung  
  
1. Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../../includes/ssde-md.md)]-Instanz her.  
  
2. Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3. Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```sql
    USE AdventureWorks2012;  
    GO  
  
    CREATE CERTIFICATE HumanResources037  
       WITH SUBJECT = 'Employee Social Security Numbers';  
    GO  
  
    CREATE SYMMETRIC KEY SSN_Key_01  
        WITH ALGORITHM = AES_256  
        ENCRYPTION BY CERTIFICATE HumanResources037;  
    GO  
  
    USE [AdventureWorks2012];  
    GO  
  
    -- Create a column in which to store the encrypted data.  
    ALTER TABLE HumanResources.Employee  
        ADD EncryptedNationalIDNumber varbinary(128);   
    GO  
  
    -- Open the symmetric key with which to encrypt the data.  
    OPEN SYMMETRIC KEY SSN_Key_01  
       DECRYPTION BY CERTIFICATE HumanResources037;  
  
    -- Encrypt the value in column NationalIDNumber with symmetric   
    -- key SSN_Key_01. Save the result in column EncryptedNationalIDNumber.  
    UPDATE HumanResources.Employee  
    SET EncryptedNationalIDNumber = EncryptByKey(Key_GUID('SSN_Key_01'), NationalIDNumber);  
    GO  
  
    -- Verify the encryption.  
    -- First, open the symmetric key with which to decrypt the data.  
    OPEN SYMMETRIC KEY SSN_Key_01  
       DECRYPTION BY CERTIFICATE HumanResources037;  
    GO  
  
    -- Now list the original ID, the encrypted ID, and the   
    -- decrypted ciphertext. If the decryption worked, the original  
    -- and the decrypted ID will match.  
    SELECT NationalIDNumber, EncryptedNationalIDNumber   
        AS 'Encrypted ID Number',  
        CONVERT(nvarchar, DecryptByKey(EncryptedNationalIDNumber))   
        AS 'Decrypted ID Number'  
        FROM HumanResources.Employee;  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter den folgenden Links:  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
-   [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)  
  
-   [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/open-symmetric-key-transact-sql.md)  
