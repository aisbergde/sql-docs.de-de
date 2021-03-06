---
title: Ausführen von Onlineindexvorgängen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index online operations [SQL Server]
- online index operations
- ONLINE option
ms.assetid: 1e43537c-bf67-4db3-9908-3cb45c6fdaa1
author: MikeRayMSFT
ms.author: mikeray
ms.prod_service: table-view-index, sql-database
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ac1c10bfefd80a121e858cc0175f08b6ee68ab6f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909605"
---
# <a name="perform-index-operations-online"></a>Ausführen von Onlineindexvorgängen
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie Sie Indizes in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]online erstellen, neu erstellen oder löschen. Die ONLINE-Option ermöglicht, dass Benutzer während dieser Indexvorgänge gleichzeitig auf die dem Index zugrunde liegende Tabelle oder auf Daten eines gruppierten Indexes sowie auf alle eventuell damit verbundenen nicht gruppierten Indizes zugreifen können. Während beispielsweise ein gruppierter Index von einem Benutzer neu erstellt wird, kann dieser Benutzer – und alle anderen Benutzer – weiterhin die dem Index zugrunde liegenden Daten aktualisieren oder abfragen. Wenn Sie DDL-Vorgänge (Datendefinitionssprache) wie das Erstellen oder Neuerstellen eines gruppierten Indexes offline ausführen, richten diese Vorgänge exklusive Sperren für die dem Index zugrunde liegenden Daten und damit verbundene Indizes ein. Damit werden Änderungen und Abfragen der zugrunde liegenden Daten verhindert, bis der Indexvorgang abgeschlossen ist.  
  
> [!NOTE]  
>  Onlineindexvorgänge sind nicht in jeder Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbar. Weitere Informationen finden Sie unter „Von den SQL Server 2016-Editionen unterstützte Funktionen“.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Security](#Security)  
  
-   **Onlineneuerstellung eines Indexes mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Onlineindexvorgänge werden in Geschäftsumgebungen empfohlen, die rund um die Uhr und 7 Tage die Woche aktiv sind, für die also eine gleichzeitige Benutzeraktivität während Indexvorgängen unabdingbar ist.  
  
-   Die ONLINE-Option ist in folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen verfügbar:  
  
    -   [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)  
  
    -   [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)  
  
    -   [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)  
  
    -   [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) (zum Hinzufügen oder Löschen von UNIQUE- oder PRIMARY KEY-Einschränkungen mit der CLUSTERED-Indexoption)  
  
-   Weitere Einschränkungen und Einschränkungen im Zusammenhang mit der Onlineerstellung, -neuerstellung und -löschung von Indizes finden Sie unter [Richtlinien für Onlineindexvorgänge](../../relational-databases/indexes/guidelines-for-online-index-operations.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung in der Tabelle oder Sicht.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-rebuild-an-index-online"></a>Sie erstellen Sie einen Index online neu  
  
1.  Klicken Sie im Objekt-Explorer auf das Pluszeichen, um die Datenbank mit der Tabelle zu erweitern, in der Sie einen Index online neu erstellen möchten.  
  
2.  Erweitern Sie den Ordner **Tabellen** .  
  
3.  Klicken Sie auf das Pluszeichen, um die Tabelle zu erweitern, für die Sie einen Index online neu erstellen möchten.  
  
4.  Erweitern Sie den Ordner **Indizes** .  
  
5.  Klicken Sie mit der rechten Maustaste auf den Index, den Sie online neu erstellen möchten, und wählen Sie **Eigenschaften**aus.  
  
6.  Wählen Sie unter **Seite auswählen**die Option **Optionen**aus.  
  
7.  Wählen Sie **DML-Onlineverarbeitung zulassen**aus, und wählen Sie dann in der Liste **True** aus.  
  
8.  Klicken Sie auf **OK**.  
  
9. Klicken Sie mit der rechten Maustaste auf den Index, den Sie online neu erstellen möchten, und wählen Sie **Neu erstellen**aus.  
  
10. Überprüfen Sie im Dialogfeld **Indizes neu erstellen** , dass der richtige Index im Raster **Neu zu erstellende Indizes** ausgewählt ist, und klicken sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
### <a name="to-create-rebuild-or-drop-an-index-online"></a>So können Sie einen Index online erstellen, neu erstellen oder löschen  
  
Im folgenden Beispiel wird ein vorhandener Onlineindex in der AdventureWorks-Datenbank erneut erstellt.
  
 ```sql  
 ALTER INDEX AK_Employee_NationalIDNumber
   ON HumanResources.Employee  
   REBUILD WITH (ONLINE = ON)
;
```  
  
Im folgenden Beispiel wird ein gruppierter Index online gelöscht, und die daraus resultierende Tabelle (Heap) wird in die Dateigruppe `NewGroup` verschoben, wofür die `MOVE TO` -Klausel verwendet wird. Die Katalogsichten `sys.indexes`, `sys.tables`und `sys.filegroups` werden abgefragt, um die Platzierung von Index und Tabelle in den Dateigruppen vor und nach der Verschiebung zu prüfen.  
  
[!code-sql[IndexDDL#DropIndex4](../../relational-databases/indexes/codesnippet/tsql/perform-index-operations_1.sql)]  
  
Weitere Informationen finden Sie unter [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
