---
title: Sysssispackages (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysdtspackages90_TSQL
- sysdtspackages90
dev_langs: TSQL
helpviewer_keywords: sysssispackages system table
ms.assetid: 66155dcd-dcdb-4e33-a242-1625828ad8d2
caps.latest.revision: "43"
author: spelluru
ms.author: spelluru
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5b694a277a235b373f1051878551ccca9537623f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysssispackages-transact-sql"></a>sysssispackages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jedes Paket, das gespeichert wird [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Der eindeutige Bezeichner des Pakets.|  
|**id**|**uniqueidentifier**|GUID des Pakets|  
|**Beschreibung**|**nvarchar**|Eine optionale Beschreibung des Pakets.|  
|**CREATEDATE**|**datetime**|Erstellungsdatum des Pakets|  
|**folderID**|**uniqueidentifier**|Die GUID des logischen Ordners, in dem das Paket von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] aufgelistet ist.|  
|**ownersid**|**varbinary**|Die eindeutige Sicherheits-ID des Benutzers, der das Paket erstellt hat|  
|**packagedata**|**image**|Das Paket.|  
|**packageformat**|**int**|Das Format, in dem das Paket gespeichert wird:<br /><br /> Der Wert 2 Gibt an, in das Paket gespeichert werden, die [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Format.<br /><br /> Der Wert 3 gibt an, das Paket gespeichert wird, im Format der [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]oder höher.|  
|**PackageType**|**int**|Der Client, der das Paket erstellt hat. Die folgenden Werte sind möglich:<br /><br /> 0 (Standardwert)<br /><br /> 1 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistent)<br /><br /> 3 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replikation)<br /><br /> 5 ([!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer)<br /><br /> 6 (Wartungsplan-Designer oder -Assistent).<br /><br /> <br /><br /> Beachten Sie, die die Werte in dieser Spalte entsprechen der <xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType> Enumeration.|  
|**VerMajor**|**int**|Die aktuelle Hauptversion des Pakets.|  
|**VerMinor**|**int**|Die aktuelle Nebenversion des Pakets.|  
|**verbuild**|**int**|Das letzte Build des Pakets.|  
|**vercomments**|**nvarchar**|Kommentare zur Paketversion|  
|**Verid**|**uniqueidentifier**|GUID der Paketversion|  
|**"IsEncrypted"**|**bit**|Ein boolescher Wert, der angibt, ob das Paket verschlüsselt ist|  
|**readrolesid**|**varbinary**|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rolle, die Pakete laden kann|  
|**writerolesid**|**varbinary**|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rolle, die Pakete speichern kann|  
  
## <a name="see-also"></a>Siehe auch  
 [Integration Services-Pakete &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md)  
  
  