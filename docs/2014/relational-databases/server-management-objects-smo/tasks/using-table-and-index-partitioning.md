---
title: Verwenden von Tabellen- und Indexpartitionierung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- partitions [SMO]
- storing data [SMO]
- partitioned tables [SQL Server], SMO
- partitioned indexes [SQL Server], SMO
ms.assetid: 0e682d7e-86c3-4d73-950d-aa692d46cb62
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 73a106a4e17ea770517c7662dfecd98fe58e36b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270737"
---
# <a name="using-table-and-index-partitioning"></a>Verwenden von Tabellen- und Indexpartitionierung
  Daten können mit den von [Partitioned Tables and Indexes](../../partitions/partitioned-tables-and-indexes.md)bereitgestellten Speicheralgorithmen gespeichert werden. Die Partitionierung kann bewirken, dass sich große Tabellen und Indizes besser verwalten und skalieren lassen.  
  
## <a name="index-and-table-partitioning"></a>Index- und Tabellenpartitionierung  
 Die Funktion aktiviert Index- und Tabellendaten, die auf mehrere Dateigruppen in Partitionen verteilt werden. Eine Partitionsfunktion definiert, wie die Zeilen einer Tabelle oder eines Index basierend auf den Werten bestimmter Spalten, den so genannten Partitionierungsspalten, einem Satz von Partitionen zugeordnet werden. Ein Partitionierungsschema ordnet die durch die Partitionsfunktion angegebenen Partitionen jeweils einer Dateigruppe zu. Hierdurch können Sie Archivierungsstrategien entwickeln, die es ermöglichen, dass Tabellen, und damit physische Medien, dateigruppenübergreifend skaliert werden können.  
  
 Das <xref:Microsoft.SqlServer.Management.Smo.Database>-Objekt enthält eine Auflistung von <xref:Microsoft.SqlServer.Management.Smo.PartitionFunction>-Objekten, die die implementierten Partitionsfunktionen darstellen, und eine Auflistung von <xref:Microsoft.SqlServer.Management.Smo.PartitionScheme>-Objekten, die beschreiben, wie Daten Dateigruppen zugeordnet werden.  
  
 Jedes <xref:Microsoft.SqlServer.Management.Smo.Table>- und <xref:Microsoft.SqlServer.Management.Smo.Index>-Objekt legt fest, welches Partitionsschema es in der <xref:Microsoft.SqlServer.Management.Smo.PartitionScheme>-Eigenschaft verwendet, und legt die Spalten in <xref:Microsoft.SqlServer.Management.Smo.PartitionSchemeParameterCollection> fest.  
  
## <a name="example"></a>Beispiel  
 Für das folgende Codebeispiel müssen Sie die Programmierungsumgebung, die Programmiervorlage und die Programmiersprache auswählen, um Ihre Anwendung zu erstellen. Weitere Informationen finden Sie unter [erstellen Sie eine Visual Basic-SMO-Projekts in Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) und [Erstellen eines Visual C&#35; SMO-Projekts in Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-visual-basic"></a>Einrichten eines Partitionsschemas für eine Tabelle in Visual Basic  
 Das Codebeispiel veranschaulicht, wie eine Partitionsfunktion und ein Partitionsschema für die `TransactionHistory` -Tabelle in der Beispieldatenbank [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] erstellt werden. Die Partitionen sind nach Datum aufgeteilt, um alte Datensätze in die `TransactionHistoryArchive` -Tabelle auszugliedern.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBPartition1](SMO How to#SMO_VBPartition1)]  -->  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-visual-c"></a>Einrichten eines Partitionsschemas für eine Tabelle in Visual C#  
 Das Codebeispiel veranschaulicht, wie eine Partitionsfunktion und ein Partitionsschema für die `TransactionHistory` -Tabelle in der Beispieldatenbank [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] erstellt werden. Die Partitionen sind nach Datum aufgeteilt, um alte Datensätze in die `TransactionHistoryArchive` -Tabelle auszugliedern.  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Define and create three new file groups on the database.   
FileGroup fg2;   
fg2 = new FileGroup(db, "Second");   
fg2.Create();   
FileGroup fg3;   
fg3 = new FileGroup(db, "Third");   
fg3.Create();   
FileGroup fg4;   
fg4 = new FileGroup(db, "Fourth");   
fg4.Create();   
//Define a partition function by supplying the parent database and name arguments in the constructor.   
PartitionFunction pf;   
pf = new PartitionFunction(db, "TransHistPF");   
//Add a partition function parameter that specifies the function uses a DateTime range type.   
PartitionFunctionParameter pfp;   
pfp = new PartitionFunctionParameter(pf, DataType.DateTime);   
pf.PartitionFunctionParameters.Add(pfp);   
//Specify the three dates that divide the data into four partitions.   
object[] val;   
val = new object[] {"1/1/2003", "1/1/2004", "1/1/2005"};   
pf.RangeValues = val;   
//Create the partition function.   
pf.Create();   
//Define a partition scheme by supplying the parent database and name arguments in the constructor.   
PartitionScheme ps;   
ps = new PartitionScheme(db, "TransHistPS");   
//Specify the partition function and the filegroups required by the partition scheme.   
ps.PartitionFunction = "TransHistPF";   
ps.FileGroups.Add("PRIMARY");   
ps.FileGroups.Add("second");   
ps.FileGroups.Add("Third");   
ps.FileGroups.Add("Fourth");   
//Create the partition scheme.   
ps.Create();   
}   
```  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-powershell"></a>Einrichten eines Partitionsschemas für eine Tabelle in PowerShell  
 Das Codebeispiel veranschaulicht, wie eine Partitionsfunktion und ein Partitionsschema für die `TransactionHistory` -Tabelle in der Beispieldatenbank [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] erstellt werden. Die Partitionen sind nach Datum aufgeteilt, um alte Datensätze in die `TransactionHistoryArchive` -Tabelle auszugliedern.  
  
```powershell  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
$db = $srv.Databases["AdventureWorks"]  
#Create four filegroups  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "First"  
$fg2 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Second"  
$fg3 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Third"  
$fg4 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Fourth"  
  
#Define a partition function by supplying the parent database and name arguments in the constructor.  
$pf =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionFunction -argumentlist $db, "TransHistPF"  
$T = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$T  
$T.GetType()  
#Add a partition function parameter that specifies the function uses a DateTime range type.  
$pfp =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionFunctionParameter -argumentlist $pf, $T  
  
#Specify the three dates that divide the data into four partitions.   
#Create an array of type object to hold the partition data  
$val = "1/1/2003"."1/1/2004","1/1/2005"  
$pf.RangeValues = $val  
$pf  
#Create the partition function  
$pf.Create()  
  
#Create partition scheme  
$ps = New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionScheme -argumentlist $db, "TransHistPS"  
$ps.PartitionFunction = "TransHistPF"  
  
#add the filegroups to the scheme   
$ps.FileGroups.Add("PRIMARY")  
$ps.FileGroups.Add("Second")  
$ps.FileGroups.Add("Third")  
$ps.FileGroups.Add("Fourth")  
  
#Create it at the server  
$ps.Create()  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Partitioned Tables and Indexes](../../partitions/partitioned-tables-and-indexes.md)  
  
  
