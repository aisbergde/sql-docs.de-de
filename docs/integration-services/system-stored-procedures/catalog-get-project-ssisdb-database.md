---
title: catalog.get_project (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: f263c9e4-a7db-4888-a458-70ae99b1f729
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b6eaef69d6984494543dc730e19a8436a3a9b658
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68007831"
---
# <a name="cataloggetproject-ssisdb-database"></a>catalog.get_project (SSISDB-Datenbank)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Ruft den binären Datenstrom eines Projekts ab, das auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Server bereitgestellt wurde.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.get_project [ @folder_name = ] folder_name , [ @project_name = ] project_name   
```  
  
## <a name="arguments"></a>Argumente  
 [ @folder_name = ] *folder_name*  
 Der Name des Ordners, der das Projekt enthält. *folder_name* ist **nvarchar(128)**  
  
 [ @project_name = ] *project_name*  
 Der Name des Projekts. *project_name* ist **nvarchar(128)**  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Der binäre Datenstrom des Projekts wird als **varbinary(MAX)** zurückgegeben. Wenn der Ordner oder das Projekt nicht gefunden wird, werden keine Ergebnisse zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigungen für das Projekt  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden Bedingungen beschrieben, die möglicherweise bewirken, dass die gespeicherte Prozedur „get_project“ einen Fehler auslöst:  
  
-   Das Projekt ist nicht vorhanden.  
  
-   Der Ordner ist nicht vorhanden.  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
  
