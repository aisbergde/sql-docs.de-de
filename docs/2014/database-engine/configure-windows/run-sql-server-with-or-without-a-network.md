---
title: Ausführen von SQL Server mit oder ohne Netzwerk | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- verifying Server service has been started
- net start [SQL Server]
- command prompt [SQL Server], connections
- SQL Server services, networks
- status information [SQL Server], Server service
- running SQL Server
- networking [SQL Server], SQL Server with or without
- services [SQL Server], networks
- starting Server service
- SQL Server, running
ms.assetid: 54eac961-5c7a-4481-982d-f93a64b5c2f4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 050986f4c78fc285e936b206c82faef90b89d75e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "62810358"
---
# <a name="run-sql-server-with-or-without-a-network"></a>Ausführen von SQL Server mit oder ohne Netzwerk
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann mit und ohne Netzwerk ausgeführt werden.  
  
## <a name="running-sql-server-on-a-network"></a>Ausführen von SQL Server in einem Netzwerk  
 Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] über ein Netzwerk kommunizieren soll, muss der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst ausgeführt werden. Standardmäßig wird der integrierte [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Dienst automatisch von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows gestartet. Wenn Sie feststellen möchten, ob der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst gestartet wurde, geben Sie Folgendes an der Eingabeaufforderung ein:  
  
 **net start**  
  
 Wenn die Dienste für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestartet wurden, werden in der Ausgabe von **net start** folgende Dienste angezeigt:  
  
-   SQL Server Analysis Services (MSSQLSERVER)  
  
-   SQL Server (MSSQLSERVER)  
  
-   SQL Server-Agent (MSSQLSERVER)  
  
## <a name="running-sql-server-without-a-network"></a>Ausführen von SQL Server ohne Netzwerk  
 Wenn eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ohne Netzwerk ausgeführt wird, müssen Sie den integrierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst nicht starten. Da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], der SQL Server-Konfigurations-Manager und die Befehle **net start** und **net stop** immer funktionsfähig sind, sogar ohne Netzwerk, sind daher die Verfahren für das Starten und Beenden einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit und ohne Netzwerk identisch.  
  
 Wenn Sie von einem lokalen Client (z.B. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sqlcmd **) eine Verbindung mit einer eigenständigen Instanz von**herstellen, wird das Netzwerk umgangen. Die Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfolgt direkt mithilfe einer lokalen Pipe. Der Unterschied zwischen einer lokalen Pipe und einer Netzwerkpipe besteht darin, dass bei letzterer ein Netzwerk verwendet wird. Sowohl lokale Pipes als auch Netzwerkpipes stellen eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe der Standardpipe her (\\\\.\pipe\sql\query), sofern nichts anderes festgelegt wird.  
  
 Wenn Sie ohne Angabe eines Servernamens eine Verbindung mit einer lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen, verwenden Sie eine lokale Pipe. Wenn Sie jedoch bei der Verbindung mit einer lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explizit einen Servernamen angeben, verwenden Sie entweder eine Netzwerkpipe oder einen anderen Mechanismus für die prozessübergreifende Kommunikation (IPC, Interprocess Communication) in Netzwerken, wie z. B. IPX/SPX (unter der Annahme, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die Verwendung mehrerer Netzwerke konfiguriert wurde). Da ein eigenständiger Computer mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Netzwerkpipes nicht unterstützt, dürfen Sie das nicht notwendige **/** _<Servername>_ -Argument nicht verwenden, wenn Sie von einem Client eine Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen. Um z.B. mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] osql **eine Verbindung mit einer eigenständigen Instanz von**herzustellen, geben Sie Folgendes ein:  
  
 **osql /Usa /P** _\<saPassword>_  
  
  
