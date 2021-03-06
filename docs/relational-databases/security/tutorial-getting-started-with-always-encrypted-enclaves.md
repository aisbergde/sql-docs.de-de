---
title: 'Lernprogramm: Erste Schritte mit Always Encrypted mit Secure Enclaves mithilfe von SSMS | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 08/07/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: de030c3982fb3e3ed64603707b7e6915779fb4d8
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028808"
---
# <a name="tutorial-getting-started-with-always-encrypted-with-secure-enclaves-using-ssms"></a>Lernprogramm: Erste Schritte mit Always Encrypted mit Secure Enclaves mithilfe von SSMS
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

In diesem Tutorial werden Ihnen die erste Schritte mit [Always Encrypted mit Secure Enclaves](encryption/always-encrypted-enclaves.md) vermittelt. Es wird Folgendes gezeigt:
- Erstellen einer einfachen Umgebung zum Testen und Auswerten von Always Encrypted mit Secure Enclaves
- Direktes Verschlüsseln von Daten und Ausgeben umfangreicher Abfragen für verschlüsselte Spalten mithilfe von SQL Server Management Studio (SSMS)

## <a name="prerequisites"></a>Voraussetzungen

Für die ersten Schritte mit Always Encrypted mit Secure Enclaves benötigen Sie mindestens zwei Computer (dies können virtuelle Computer sein):

- SQL Server-Computer als Host für SQL Server und SSMS
- HGS-Computer zum Ausführen des Host-Überwachungsdiensts, der für den Enclave-Nachweis erforderlich ist

### <a name="sql-server-computer-requirements"></a>SQL Server-Computeranforderungen

- [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)] oder höher.
- Windows 10 Enterprise, Version 1809, oder Windows Server 2019 Datacenter.
- Wenn Ihr SQL Server-Computer ein physischer Computer ist, muss er die [Hardwareanforderungen für Hyper-V](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/hyper-v-requirements#hardware-requirements) erfüllen:
   - 64-Bit-Prozessor mit Second Level Address Translation (SLAT)
   - CPU-Unterstützung für VM-Überwachungsmoduserweiterung (VT-c bei Intel-CPUs)
   - Virtualisierungsunterstützung aktiviert (Intel VT-x- oder AMD-V)
- Wenn Ihr SQL Server-Computer eine VM (virtueller Computer) ist, muss die VM so konfiguriert sein, dass die virtualisierungsbasierte Sicherheit (VBS) zugelassen wird.
   - Verwenden Sie für Hyper-V 2016 oder höher eine VM der Generation 1, und [aktivieren Sie geschachtelte Virtualisierungserweiterungen](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization#configure-nested-virtualization) für den VM-Prozessor, oder verwenden Sie eine VM der Generation 2. Weitere Informationen zu VM-Generationen finden Sie unter [Sollte ich einen virtuellen Computer der Generation 1 oder 2 in Hyper-V erstellen?](https://docs.microsoft.com/windows-server/virtualization/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v). 
   - Stellen Sie sicher, dass Sie eine VM-Größe in Azure betreiben, die eine der folgenden Optionen unterstützt:
      - Geschachtelte Virtualisierung, z. B. VMs der Serien Dv3 und Ev3. Siehe [Erstellen einer schachtelungsfähigen Azure-VM](https://docs.microsoft.com/azure/virtual-machines/windows/nested-virtualization#create-a-nesting-capable-azure-vm).
      - VMs der Generation 2, z. B. VMs der Serien Dsv3 und Esv3. Siehe [Unterstützung für VMs der Generation 2 in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/generation-2).
   - Bei VMware vSphere 6.7 oder höher aktivieren Sie die Unterstützung für virtualisierungsbasierte Sicherheit für den virtuellen Computer, wie in der [VMware-Dokumentation](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.vm_admin.doc/GUID-C2E78F3E-9DE2-44DB-9B0A-11440800AADD.html) beschrieben.
   - Andere Hypervisoren und Public Clouds unterstützen möglicherweise die Verwendung von Always Encrypted mit Secure Enclaves auf einem virtuellen Computer, solange Virtualisierungserweiterungen (manchmal als „geschachtelte Virtualisierung“ bezeichnet) für den virtuellen Computer verfügbar gemacht werden. Informationen zur Kompatibilität und Konfigurationsanweisungen finden Sie in der Dokumentation zu Ihrer Virtualisierungslösung.
- [SQL Server Management Studio (SSMS) 18.0 oder höher](../../ssms/download-sql-server-management-studio-ssms.md)

Alternativ können Sie SSMS auf einem anderen Computer installieren.

> [!WARNING]
> In Produktionsumgebungen sollten Sie niemals SSMS oder andere Tools zum Verwalten von Always Encrypted-Schlüsseln oder Ausführen von Abfragen für verschlüsselte Daten auf dem SQL Server-Computer verwenden, da dies den Zweck der Verwendung von Always Encrypted mindern oder vollständig zunichte machen kann. Weitere Informationen finden Sie unter [Sicherheitsüberlegungen für die Schlüsselverwaltung](encryption/overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management).

### <a name="hgs-computer-requirements"></a>HGS-Computeranforderungen

- Windows Server 2019 Standard oder Datacenter Edition
- 2 CPUs
- 8 GB RAM
- 100 GB Speicher

> [!NOTE]
> Der HGS-Computer sollte nicht mit einer Domäne verknüpft werden, bevor Sie beginnen.

## <a name="step-1-configure-the-hgs-computer"></a>Schritt 1: Konfigurieren des HGS-Computers

In diesem Schritt konfigurieren Sie den HGS-Computer zum Ausführen des Host-Überwachungsdiensts, der den Hostschlüsselnachweis unterstützt.

1. Melden Sie sich beim HGS-Computer als Administrator (lokaler Administrator) an, öffnen Sie eine Windows PowerShell-Konsole mit erhöhten Rechten, und fügen Sie die Rolle für den Host-Überwachungsdienst hinzu, indem Sie den folgenden Befehl ausführen:

   ```powershell
   Install-WindowsFeature -Name HostGuardianServiceRole -IncludeManagementTools -Restart
   ```

2. Nach dem Neustart des HGS-Computers melden Sie sich erneut mit Ihrem Administratorkonto an, öffnen Sie eine Windows PowerShell-Konsole mit erhöhten Rechten, und führen Sie die folgenden Befehle aus, um den Host-Überwachungsdienst zu installieren und dessen Domäne zu konfigurieren. Das hier von Ihnen angegebene Kennwort gilt nur für das Kennwort des Reparaturmodus für Verzeichnisdienste für Active Directory. Das Anmeldekennwort Ihres Administratorkontos wird dadurch nicht geändert. Sie können einen Domänennamen Ihrer Wahl für „-HgsDomainName“ angeben.

   ```powershell
   $adminPassword = ConvertTo-SecureString -AsPlainText '<password>' -Force
   Install-HgsServer -HgsDomainName 'bastion.local' -SafeModeAdministratorPassword $adminPassword -Restart
   ```

3. Nach dem wiederholten Neustart des Computers melden Sie sich mit Ihrem Administratorkonto an (das nun auch ein Domänenadministrator ist), öffnen Sie eine Windows PowerShell-Konsole mit erhöhten Rechten, und konfigurieren Sie den Hostschlüsselnachweis für Ihre HGS-Instanz. 

   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustHostKey  
   ```

4. Führen Sie den folgenden Befehl aus, um die IP-Adresse des HGS-Computers zu suchen. Speichern Sie diese IP-Adresse für spätere Schritte.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

   ```powershell
   Get-NetIPAddress  
   ```

> [!NOTE]
> Wenn Sie auf Ihren HGS-Computer mit einem DNS-Namen verweisen möchten, können Sie eine Weiterleitung von den DNS-Servern Ihres Unternehmens an den neuen HGS-Domänencontroller einrichten.  

## <a name="step-2-configure-the-sql-server-computer-as-a-guarded-host"></a>Schritt 2: Konfigurieren des SQL Server-Computers als überwachter Host
In diesem Schritt konfigurieren Sie den SQL Server-Computer als überwachten Host, der beim Host-Überwachungsdienst mit Hostschlüsselnachweis registriert ist.

> [!WARNING]
> Der Hostschlüsselnachweis wird nur zur Verwendung in Testumgebungen empfohlen. Für Produktionsumgebungen sollten Sie den TPM-Nachweis verwenden.

1. Melden Sie sich beim SQL Server-Computer als Administrator an. Öffnen Sie eine Windows PowerShell-Konsole mit erhöhten Rechten, und rufen Sie den Namen Ihres Computers durch Zugreifen auf die Variable „computername“ ab.

   ```powershell
   $env:computername 
   ```

2. Installieren Sie die Funktion für überwachten Host, mit der auch Hyper-V installiert wird (sofern nicht bereits erfolgt).

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All
   ```

3. Starten Sie den SQL Server-Computer bei Aufforderung erneut, um die Installation von Hyper-V abzuschließen.

4. Wenn Ihr SQL Server-Computers ein virtueller Computer ist, oder wenn es sich um einen älteren physischen Computer handelt, der keinen sicheren UEFI-Start unterstützt oder nicht mit IOMMU ausgestattet ist, müssen Sie die VBS-Anforderung für die Plattformsicherheitsfunktionen entfernen.
    1. Entfernen Sie die Anforderung in der Windows-Registrierung.

        ```powershell
       Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Name RequirePlatformSecurityFeatures -Value 0
       ```

    1. Starten Sie den Computer neu, damit VBS mit den niedrigeren Anforderungen online geht.

        ```powershell
       Restart-Computer
       ```

5. Melden Sie sich erneut beim SQL Server-Computer als Administrator an, öffnen Sie eine Windows PowerShell-Konsole mit erhöhten Rechten, generieren Sie einen eindeutigen Hostschlüssel, und exportieren Sie den resultierenden öffentlichen Schlüssel in eine Datei.

   ```powershell
   Set-HgsClientHostKey 
   Get-HgsClientHostKey -Path $HOME\Desktop\hostkey.cer
   ```

6. Kopieren Sie manuell die Hostschlüsseldatei, die im vorherigen Schritt generiert wurde, auf den HGS-Computer. Bei den folgenden Anweisungen wird davon ausgegangen, dass der Dateiname „hostkey.cer“ lautet und Sie diese Datei auf Ihren Desktop auf dem HGS-Computer kopieren.

7. Öffnen Sie auf dem HGS-Computer eine Windows PowerShell-Konsole mit erhöhten Rechten, und registrieren Sie den Hostschlüssel Ihres SQL Server-Computers beim Host-Überwachungsdienst:

   ```powershell
   Add-HgsAttestationHostKey -Name <your SQL Server computer name> -Path $HOME\Desktop\hostkey.cer
   ```

8. Führen Sie auf dem SQL Server-Computer den folgenden Befehl in einer Windows PowerShell-Konsole mit erhöhten Rechten aus, um dem SQL Server-Computer den Ort für den Nachweis anzugeben. Vergewissern Sie sich, dass Sie die IP-Adresse oder den DNS-Namen des HSG-Computers an beiden Adressstellen angeben. 

   ```powershell
   # use http, and not https
   Set-HgsClientConfiguration -AttestationServerUrl http://<IP address or DNS name>/Attestation -KeyProtectionServerUrl http://<IP address or DNS name>/KeyProtection/  
   ```

Das Ergebnis des oben gezeigten Befehls sollte „AttestationStatus = Passed“ lauten.

Wenn Sie eine Fehlermeldung vom Typ „HostUnreachable“ erhalten, bedeutet dies, dass Ihr SQL Server-Computer nicht mit dem Host-Überwachungsdienst kommunizieren kann. Stellen Sie sicher, dass Sie den HGS Computer pingen können.

Ein Fehler vom Typ „UnauthorizedHost“ weist darauf hin, dass der öffentliche Schlüssel nicht beim HGS-Server registriert wurde. Wiederholen Sie die Schritte 5 und 6, um den Fehler zu beheben.

Wenn andere Fehler auftreten, führen Sie „Clear-HgsClientHostKey“ aus, und wiederholen Sie die Schritte 4 bis 7.

## <a name="step-3-enable-always-encrypted-with-secure-enclaves-in-sql-server"></a>Schritt 3: Aktivieren von Always Encrypted mit Secure Enclaves in SQL Server

In diesem Schritt aktivieren Sie die Funktionen von Always Encrypted mithilfe von Enclaves in Ihrer SQL Server-Instanz.

1. Verbinden Sie sich per SSMS als „sysadmin“ mit Ihrer SQL Server-Instanz, **ohne** dass Always Encrypted für die Datenverbindung aktiviert ist.
    1. Starten Sie SSMS.
    1. Geben Sie im Dialogfeld **Mit Server verbinden** Ihren Servernamen, eine Authentifizierungsmethode und Ihre Anmeldeinformationen an.
    1. Klicken Sie auf **Optionen >>** , und wählen Sie die Registerkarte **Always Encrypted** aus.
    1. Stellen Sie sicher, dass das Kontrollkästchen **Always Encrypted aktivieren (Spaltenverschlüsselung)** **nicht** ausgewählt ist.
    1. Wählen Sie **Verbinden**.

2. Öffnen Sie ein neues Abfragefenster, und führen Sie die folgende Anweisung, um den Typ der Secure Enclave auf virtualisierungsbasierte Sicherheit (VBS) festzulegen.

   ```sql
   EXEC sys.sp_configure 'column encryption enclave type', 1;
   RECONFIGURE;
   ```

3. Starten Sie Ihre SQL Server-Instanz neu, damit die vorherige Änderung übernommen wird. Sie können die Instanz in SSMS neu starten, indem Sie im Objekt-Explorer mit der rechten Maustaste darauf klicken und „Neustart“ auswählen. Stellen Sie nach dem Neustart der Instanz eine neue Verbindung her.

4. Vergewissern Sie sich, dass die Secure Enclave geladen ist, indem Sie die folgende Abfrage ausführen:

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type';
   ```

    Die Abfrage sollte folgendes Ergebnis haben:  

    | NAME                           | Wert | value_in_use |
    | ------------------------------ | ----- | -------------- |
    | column encryption enclave type | 1     | 1              |

5. Um umfangreiche Berechnungen mit verschlüsselten Spalten zu aktivieren, führen Sie die folgende Abfrage aus:

   ```sql
   DBCC traceon(127,-1);
   ```

    > [!NOTE]
    > Umfangreiche Berechnungen sind in [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)] standardmäßig deaktiviert. Sie müssen über die oben genannte Anweisung nach jedem Neustart der SQL Server-Instanz aktiviert werden.

## <a name="step-4-create-a-sample-database"></a>Schritt 4: Erstellen einer Beispieldatenbank
In diesem Schritt erstellen Sie eine Datenbank mit einigen Beispieldaten, die Sie später verschlüsseln.

1. Führen Sie unter Verwendung der SSMS-Instanz aus dem vorherigen Schritt die folgende Anweisung in einem Abfragefenster aus, um eine neue Datenbank mit dem Namen **ContosoHR** zu erstellen.

    ```sql
    CREATE DATABASE [ContosoHR];
    ```

1. Erstellen Sie eine neue Tabelle mit dem Namen **Employees**.

    ```sql
    USE [ContosoHR];
    GO

    CREATE TABLE [dbo].[Employees]
    (
        [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
        [SSN] [char](11) NOT NULL,
        [FirstName] [nvarchar](50) NOT NULL,
        [LastName] [nvarchar](50) NOT NULL,
        [Salary] [money] NOT NULL
    ) ON [PRIMARY];
    ```

1. Fügen Sie der Tabelle **Employees** einige Mitarbeiterdatensätze hinzu.

    ```sql
    USE [ContosoHR];
    GO

    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('795-73-9838'
            , N'Catherine'
            , N'Abel'
            , $31692);

    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('990-00-6818'
            , N'Kim'
            , N'Abercrombie'
            , $55415);
    ```

## <a name="step-5-provision-enclave-enabled-keys"></a>Schritt 5: Bereitstellen Enclave-fähiger Schlüssel

In diesem Schritt erstellen Sie einen Spaltenhauptschlüssel und einen Spaltenverschlüsselungsschlüssel, die Enclave-Berechnungen zulassen.

1. Erweitern Sie Ihre Datenbank im **Objekt-Explorer** mit der SSMS-Instanz aus dem vorherigen Schritt, und navigieren Sie zu **Sicherheit** > **Always Encrypted-Schlüssel**.
1. Stellen Sie einen neuen Enclave-fähigen Spaltenhauptschlüssel bereit:
    1. Klicken Sie mit der rechten Maustaste auf **Always Encrypted-Schlüssel**, und wählen Sie **Neuer Spaltenhauptschlüssel** aus.
    2. Wählen Sie den Namen des Spaltenhauptschlüssels aus: **CMK1**.
    3. Stellen Sie sicher, dass Sie entweder **Windows-Zertifikatspeicher (Aktueller Benutzer oder lokaler Computer)** oder **Azure Key Vault** auswählen.
    4. Wählen Sie **Enclave-Berechnungen zulassen**.
    5. Wenn Sie Azure Key Vault ausgewählt haben, melden Sie sich bei Azure an, und wählen Sie Ihren Schlüsseltresor. Weitere Informationen zum Erstellen eines Schlüsseltresors für Always Encrypted finden Sie unter [Verwalten Ihrer Schlüsseltresore im Azure-Portal](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/).
    6. Wählen Sie Ihr Zertifikat oder Ihren Azure-Schlüsselwertschlüssel aus, wenn bereits vorhanden, oder klicken Sie auf die Schaltfläche **Zertifikat generieren**, um ein neues zu erstellen.
    7. Wählen Sie **OK**.

        ![Enclave-Berechnungen zulassen](encryption/media/always-encrypted-enclaves/allow-enclave-computations.png)

1. Erstellen Sie einen neuen Enclave-fähigen Spaltenverschlüsselungsschlüssel:

    1. Klicken Sie mit der rechten Maustaste auf **Always Encrypted-Schlüssel**, und wählen Sie **Neuer Spaltenverschlüsselungsschlüssel**.
    2. Geben Sie einen Namen für den neuen Spaltenverschlüsselungsschlüssel ein: **CEK1**.
    3. Wählen Sie in der Dropdownliste **Spaltenhauptschlüssel** den in den vorherigen Schritten erstellten Spaltenhauptschlüssel.
    4. Wählen Sie **OK**.

## <a name="step-6-encrypt-some-columns-in-place"></a>Schritt 6: Direktes Verschlüsseln einiger Spalten

In diesem Schritt verschlüsseln Sie die in den Spalten **SSN** und **Salary** gespeicherten Daten in der serverseitigen Enclave und testen dann eine SELECT-Abfrage der Daten.

1. Öffnen Sie eine neue SSMS-Instanz, und verbinden Sie sich mit Ihrer SQL Server-Instanz, wenn Always Encrypted für die Datenverbindung aktiviert **ist**.
    1. Starten Sie eine neue SSMS-Instanz.
    1. Geben Sie im Dialogfeld **Mit Server verbinden** Ihren Servernamen, eine Authentifizierungsmethode und Ihre Anmeldeinformationen an.
    1. Klicken Sie auf **Optionen >>** , und wählen Sie die Registerkarte **Always Encrypted** aus.
    1. Aktivieren Sie das Kontrollkästchen **Always Encrypted aktivieren (Spaltenverschlüsselung)** und geben Sie Ihre Enclave-Nachweis-URL an (z.B. ht<span>tp://</span>hgs.bastion.local/Attestation).
    1. Wählen Sie **Verbinden**.
    1. Wenn Sie aufgefordert werden, die Parametrisierung für Always Encrypted zu aktivieren, klicken Sie auf **Aktivieren**.

1. Öffnen Sie mit derselben SSMS-Instanz (Always Encrypted ist aktiviert) ein neues Abfragefenster, und verschlüsseln Sie die Spalten **SSN** und **Salary**, indem Sie die folgenden Abfragen ausführen.

    ```sql
    USE [ContosoHR];
    GO

    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [SSN] [char] (11) COLLATE Latin1_General_BIN2
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON);

    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [Salary] [money]
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON);

    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```

    > [!NOTE]
    > Achten Sie auf die ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE-Anweisung, die den Abfrageplancache für die Datenbank im obigen Skript löscht. Nachdem Sie die Tabelle bearbeitet haben, müssen Sie die Pläne für alle Batches und gespeicherten Prozeduren leeren, die Zugriff auf die Tabelle haben, um die Informationen für die Parameterverschlüsselung zu aktualisieren. 

1. Um zu überprüfen, ob die Spalten **SSN** und **Salary** nun verschlüsselt sind, öffnen Sie ein neues Abfragefenster in der SSMS-Instanz, **ohne** dass Always Encrypted für die Datenbankverbindung aktiviert ist, und führen Sie die folgende Anweisung aus. Das Abfragefenster sollte verschlüsselte Werte in den Spalten **SSN** und **Salary** zurückgeben. Wenn Sie die gleiche Abfrage mit der SSMS-Instanz ausführen, bei der Always Encrypted aktiviert ist, sollten die Daten entschlüsselt angezeigt werden.

    ```sql
    SELECT * FROM [dbo].[Employees];
    ```

## <a name="step-7-run-rich-queries-against-encrypted-columns"></a>Schritt 7: Ausführen umfangreicher Abfragen für verschlüsselte Spalten

Sie können nun umfangreiche Abfragen für verschlüsselte Spalten ausführen. Ein Teil der Abfrageverarbeitung wird in der serverseitigen Enclave ausgeführt. 

1. Stellen Sie in der SSMS-Instanz **mit** aktiviertem Always Encrypted sicher, dass auch die Parametrisierung für Always Encrypted aktiviert ist.
    1. Wählen Sie im Hauptmenü von SSMS **Tools** aus.
    2. Wählen Sie **Optionen...** aus.
    3. Navigieren Sie zu **Abfrageausführung** > **SQL Server** > **Erweitert**.
    4. Stellen Sie sicher, dass **Parametrisierung für Always Encrypted aktivieren** aktiviert ist.
    5. Wählen Sie **OK**.
2. Öffnen Sie ein neues Abfragefenster, fügen Sie die folgenden Abfrage ein, und führen Sie sie anschließend aus. Die Abfrage sollte Klartextwerte und Zeilen zurückgeben, die den angegebenen Suchkriterien entsprechen.

    ```sql
    DECLARE @SSNPattern [char](11) = '%6818';
    DECLARE @MinSalary [money] = $1000;
    SELECT * FROM [dbo].[Employees]
    WHERE SSN LIKE @SSNPattern AND [Salary] >= @MinSalary;
    ```

3. Versuchen Sie dieselbe Abfrage erneut in der SSMS-Instanz, in der Always Encrypted nicht aktiviert ist, und notieren Sie den auftretenden Fehler.

## <a name="next-steps"></a>Next Steps
Lesen Sie das [Tutorial: Erstellen und Verwenden von Indizes für Enclave-fähige Spalten mit zufälliger Verschlüsselung](./tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md), das die Fortsetzung dieses Tutorials ist.

Informationen zu anderen Anwendungsfällen für Always Encrypted mit Secure Enclaves finden Sie in [Konfigurieren von Always Encrypted mit Secure Enclaves](encryption/configure-always-encrypted-enclaves.md). Beispiel:

- [Konfigurieren des TPM-Nachweises](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs-tpm-mode)
- [Konfigurieren von HTTPS für die HGS-Instanz](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-https)
- Entwickeln von Anwendungen, die umfangreiche Abfragen für verschlüsselte Spalten ausgeben
