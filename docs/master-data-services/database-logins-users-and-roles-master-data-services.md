---
title: Datenbankanmeldenamen, -benutzer und -rollen (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- security [Master Data Services], database roles
- database [Master Data Services], users
- security [Master Data Services], database users
- database [Master Data Services], roles
- database [Master Data Services], logins
- security [Master Data Services], database logins
ms.assetid: 72ee383e-a619-461b-9f9d-1cac162ab0c5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: b12e077e337cedcdcdd3bb23b12e1fb8dc6f704e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094416"
---
# <a name="database-logins-users-and-roles-master-data-services"></a>Datenbankanmeldenamen, -benutzer und -rollen (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] enthält Anmeldenamen, Benutzer und Rollen, die automatisch auf der [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] -Instanz installiert werden, die die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank hostet. Diese Anmeldenamen, Benutzer und Rollen sollten nicht geändert werden.  
  
## <a name="logins"></a>Anmeldungen  
  
|Anmeldename|Beschreibung|  
|-----------|-----------------|  
|**mds_dlp_login**|Ermöglicht die Erstellung von UNSAFE-Assemblys. Weitere Informationen finden Sie unter [Creating an Assembly](../relational-databases/clr-integration/assemblies/creating-an-assembly.md).<br /><br /> –Deaktivierter Anmeldename mit willkürlich generiertem Kennwort.<br /><br /> \- Wird für die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank dbo zugeordnet.<br /><br /> \- Für msdb wird mds_clr_user diesem Anmeldenamen zugeordnet.|  
|**mds_email_login**|Aktiviert den für Benachrichtigungen verwendeten Anmeldenamen.<br /><br /> Für msdb und die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank wird mds_email_user diesem Anmeldenamen zugeordnet.|  
  
## <a name="msdb-users"></a>msdb-Benutzer  
  
|Benutzer|Beschreibung|  
|----------|-----------------|  
|**mds_clr_user**|Wird nicht verwendet. Wird mds_dlp_login zugeordnet.|  
|**mds_email_user**|Wird für Benachrichtigungen verwendet.<br /><br /> \- Wird mds_email_login zugeordnet.<br /><br /> –Ist ein Element folgender Rolle: DatabaseMailUserRole.|  
  
## <a name="master-data-services-database-users"></a>Master Data Services-Datenbankbenutzer  
  
|Benutzer|Beschreibung|  
|----------|-----------------|  
|**mds_email_user**|Wird für Benachrichtigungen verwendet.<br /><br /> \- Verfügt über die SELECT-Berechtigung für das mdm-Schema.<br /><br /> \- Verfügt über die EXECUTE-Berechtigung für den benutzerdefinierten Tabellentyp mdm.MemberGetCriteria.<br /><br /> \- Verfügt über die EXECUTE-Berechtigung für die gespeicherte Prozedur mdm.udpNotificationQueueActivate.|  
|**mds_schema_user**|Besitzt die mdm- und mdq-Schemas. Das Standardschema ist mdm.<br /><br /> Ist keinem Anmeldenamen zugeordnet.|  
|**mds_ssb_user**|Wird zum Ausführen von Service Broker-Tasks verwendet.<br /><br /> –Verfügt über die Berechtigungen DELETE, INSERT, REFERENCES, SELECT und UPDATE für alle Schemas.<br /><br /> –Ist keinem Anmeldenamen zugeordnet.|  
  
## <a name="master-data-services-database-role"></a>Master Data Services-Datenbankrolle  
  
|Rolle|Beschreibung|Berechtigungen|  
|----------|-----------------|-----------------|  
|**mds_exec**|Diese Rolle enthält das Konto, das Sie in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] festlegen, wenn Sie eine [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung erstellen und ein Konto für den Anwendungspool festlegen.|EXECUTE-Berechtigung für alle Schemas<br /><br /> <br /><br /> Berechtigung ALTER, INSERT und SELECT für die folgenden Tabellen:<br /><br /> mdm.tblStgMember<br /><br /> mdm.tblStgMemberAttribute<br /><br /> mdm.tbleStgRelationship<br /><br /> <br /><br /> SELECT-Berechtigung für die folgenden Tabellen:<br /><br /> mdm.tblUser<br /><br /> mdm.tblUserGroup<br /><br /> mdm.tblUserPreference<br /><br /> <br /><br /> SELECT-Berechtigung für die folgenden Sichten:<br /><br /> mdm.viw_SYSTEM_SECURITY_NAVIGATION<br /><br /> mdm.viw_SYSTEM_SECURITY_ROLE_ACCCESSCONTROL<br /><br /> mdm.viw_SYSTEM_SECURITY_ROLE_ACCCESSCONTROL_MEMBER<br /><br /> mdm.viw_SYSTEM_SECURITY_USER_MODEL|  
  
## <a name="schemas"></a>Schemas  
  
|Rolle|Beschreibung|  
|----------|-----------------|  
|**mdm**|Enthält alle [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank- und Service Broker-Objekte außer die im mdq-Schema enthaltenen Funktionen.|  
|**mdq**|Enthält [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbankfunktionen, die sich auf das Filtern von Elementergebnissen auf Grundlage von regulären Ausdrücken oder Ähnlichkeiten beziehen und die zum Formatieren von Benachrichtigungs-E-Mails vorgesehen sind.|  
|**stg**|Enthält [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbanktabellen, gespeicherte Prozeduren und Sichten, die sich auf den Stagingprozess beziehen. Löschen Sie keines dieser Objekte. Weitere Informationen zum Stagingprozess finden Sie unter [Übersicht: Importieren von Daten aus Tabellen &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md).|  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheit von Datenbankobjekten &#40;Master Data Services&#41;](../master-data-services/database-object-security-master-data-services.md)  
  
  
