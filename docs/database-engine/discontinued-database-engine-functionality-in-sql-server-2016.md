---
title: Nicht mehr unterstützte Datenbank-Engine-Funktionalität in SQL Server 2016 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- VIA protocol
- unsupported features [SQL Server]
- SQL Mail
- discontinued functionality [SQL Server]
- RESTORE WITH DBO_ONLY
- BACKUP WITH PASSWORD
- user instances enabled
- BACKUP WITH MEDIAPASSWORD
- AWE
- SQL-DMO
- '*= and =*'
- 80 compatibility levels
- COMPUTE BY
- user instance timeout
- sp_dropalias
- COMPUTE
- SSL
- WITH APPEND
- sys.database_principal_aliases
- sp_dboption
- DATABASEPROPERTY
- FASTFIRSTROW hint
- SET DISABLE_DEF_CNST_CHK
ms.assetid: d686cdf0-d11d-4dba-9ec8-de1a5f189f25
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c93aa484caf1ae6a2b7582c00f8fd6223fcf35e5
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874197"
---
# <a name="discontinued-database-engine-functionality-in-sql-server-2016"></a>Nicht mehr unterstützte Datenbank-Engine-Funktionalität in SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  In diesem Thema werden die [!INCLUDE[ssDE](../includes/ssde-md.md)] -Funktionen beschrieben, die in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]nicht mehr verfügbar sind.  
  
## <a name="discontinued-features-in-includesssql15includessssql15-mdmd"></a>Nicht mehr unterstützte Funktionen in [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]  
  
- [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] ist eine 64-Bit-Anwendung. Die 32-Bit-Installation wird eingestellt, obwohl einige Elemente als 32-Bit-Komponenten ausgeführt werden.  
  
- Kompatibilitätsgrad 90 wird nicht mehr unterstützt. Weitere Informationen finden Sie unter [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  

- Das ActiveX-Subsystem wird nicht mehr unterstützt. Verwenden Sie stattdessen die Befehlszeile oder PowerShell-Skripts.

- Startparameter **-h** und **-g**. Weitere Informationen finden Sie unter [Startoptionen für den Datenbank-Engine-Dienst](https://docs.microsoft.com/sql/database-engine/configure-windows/database-engine-service-startup-options?view=sql-server-2014).

- Die SSL-Verschlüsselung (Secure Sockets Layer) wird nicht mehr unterstützt. Verwenden Sie stattdessen Transport Layer Security (TLS). Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zur Datenbank-Engine](../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).
  
## <a name="previous-versions"></a>Vorgängerversionen  
  
- [Nicht mehr unterstützte Datenbank-Engine-Funktionalität in SQL Server 2014](https://docs.microsoft.com/sql/database-engine/discontinued-database-engine-functionality-in-sql-server-2016?view=sql-server-2014)

## <a name="see-also"></a>Weitere Informationen  
 [Als veraltet markierte Funktionen der Datenbank-Engine in SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Als veraltet markierte Funktionen der SQL Server-Replikation](../relational-databases/replication/deprecated-features-in-sql-server-replication.md)  
  
 
