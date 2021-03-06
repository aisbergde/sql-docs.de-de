---
title: sqlservr-Anwendung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/01/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server], sqlservr
- command prompt [SQL Server], pausing/resuming instance of SQL Server
- starting instance of SQL Server
- command prompt [SQL Server], continuing instance of SQL Server
- sqlservr utility
- pausing instance of SQL Server
- stopping instance of SQL Server
- resuming SQL Server
- command prompt [SQL Server], stopping instance of SQL Server
- command prompt [SQL Server], starting instance of SQL Server
- continuing instance of SQL Server
ms.assetid: 60e8ef0a-0851-41cf-a6d8-cca1e04cbcdb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1feb0cfe509f4dec4e77076021757045628e2e7a
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028971"
---
# <a name="sqlservr-application"></a>sqlservr (Anwendung)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Mithilfe der Anwendung **sqlservr** können Sie die Ausführung einer [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz von der Eingabeaufforderung aus starten, beenden, anhalten und fortsetzen.

## <a name="syntax"></a>Syntax

```cmd
sqlservr [-s instance_name] [-c] [-d master_path] [-f] 
     [-e error_log_path] [-l master_log_path] [-m]
     [-n] [-T trace#] [-v] [-x]
```

## <a name="arguments"></a>Argumente

**-s** *Instanzname* Gibt die Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] für die Verbindung an. Wenn keine benannte Instanz angegeben wird, startet **sqlservr** die Standardinstanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

> [!IMPORTANT]
>Wenn Sie eine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz starten, müssen Sie die **sqlservr** -Anwendung verwenden, die sich im entsprechenden Verzeichnis für diese Instanz befindet. Bei der Standardinstanz führen Sie **sqlservr** aus dem Verzeichnis „\MSSQL\Binn“ aus. Bei einer benannten Instanz führen Sie **sqlservr** aus dem Verzeichnis „\MSSQL$*instance_name*\Binn“ aus.

 **-c**: Gibt an, dass eine Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] unabhängig vom Windows-Dienststeuerungs-Manager gestartet wird. Diese Option wird verwendet, wenn [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] von einer Eingabeaufforderung gestartet wird, um die erforderliche Zeit für das Starten von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zu verkürzen.

> [!NOTE]
>Wenn Sie diese Option verwenden, ist es nicht möglich, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Dienst-Managers oder des Befehls **net stop** zu beenden. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] wird beendet, wenn Sie sich vom Computer abmelden.

**-d** *master_path*: Gibt den vollqualifizierten Pfad für die **master**-Datenbankdatei an. Zwischen **-d** und *master_path*darf sich kein Leerzeichen befinden. Wenn diese Option nicht bereitgestellt wird, werden die vorhandenen Registrierungsparameter verwendet.

**-f**: Startet eine Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mit Minimalkonfiguration. Dies ist hilfreich, wenn der Server aufgrund der Einstellung eines Konfigurationswerts (z. B. aufgrund von Arbeitsspeichermangel) nicht gestartet werden kann.

**-e** *error_log_path*: Gibt den vollqualifizierten Pfad der Fehlerprotokolldatei an. Wenn nicht angegeben, ist `*\<Drive>*:\Program Files\Microsoft SQL Server\MSSQL\Log\Errorlog` der Standard Speicherort für die Standard Instanz und `*\<Drive>*:\Program Files\Microsoft SQL Server\MSSQL$*instance_name*\Log\Errorlog` für eine benannte Instanz. Zwischen **-e** und *error_log_path*darf sich kein Leerzeichen befinden.

**-l** *master_log_path*: Gibt den vollqualifizierten Pfad für die Transaktionsprotokolldatei der **master**-Datenbank an. Zwischen **-l** und *master_log_path*darf sich kein Leerzeichen befinden.

**-m**: Gibt an, dass eine Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] im Einzelbenutzermodus gestartet werden soll. Wenn [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] im Einzelbenutzermodus gestartet wurde, kann nur ein Benutzer eine Verbindung herstellen. Der CHECKPOINT-Mechanismus, der sicherstellt, dass abgeschlossene Transaktionen regelmäßig aus dem Datenträgercache auf die Datenbankmedien geschrieben werden, wird nicht gestartet. (Diese Option wird normalerweise verwendet, wenn Sie Probleme mit Systemdatenbanken erkennen, die eine Reparatur erfordern.) Diese Option aktiviert die Option **sp_configure allow updates** (Updates zulassen). Standardmäßig ist **allow updates** deaktiviert.

**-n**: Ermöglicht es Ihnen, eine benannte Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zu starten. Wurde der **-s** -Parameter nicht festgelegt, versucht die Standardinstanz zu starten. Sie müssen an der Eingabeaufforderung in das entsprechende BINN-Verzeichnis für die Instanz wechseln, bevor Sie **sqlservr.exe**starten. Wenn Instanz 1 beispielsweise das Verzeichnis „\mssql$Instance1“ für die zugehörigen Binärdateien verwendet, muss der Benutzer zum Verzeichnis „\mssql$Instance1\binn“ wechseln, um **sqlservr.exe -s instance1**starten zu können. Wenn Sie eine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz mit der Option **-n** starten, sollten Sie auch die Option **-e** verwenden, da sonst keine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Ereignisse protokolliert werden.

**-T** *trace#* : Gibt an, dass eine Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] so gestartet werden soll, dass ein bestimmtes Ablaufverfolgungsflag (*trace#* ) wirksam wird. Ablaufverfolgungsflags werden verwendet, um den Server mit nicht standardmäßigem Verhalten zu starten. Weitere Informationen finden Sie unter [Ablaufverfolgungsflags &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).

>[!IMPORTANT]
>Wenn Sie ein Ablaufverfolgungsflag angeben, sollten Sie **-T** verwenden, um die Nummer des Ablaufverfolgungsflags zu übergeben. Der Kleinbuchstabe „t“ ( **-t**) wird von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]akzeptiert. Mit **-t** werden jedoch andere interne Ablaufverfolgungsflags festgelegt, die von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Supporttechnikern benötigt werden.

**-v**: Zeigt die Serverversionsnummer an.

**-x**: Deaktiviert die Beibehaltung der CPU-Zeit und der Statistik für die Cachetrefferquote. Ermöglicht die maximale Leistung.

## <a name="remarks"></a>Bemerkungen
In den meisten Fällen wird das Programm sqlserver.exe nur zur Problembehandlung oder für größere Wartungsarbeiten verwendet. Wenn [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe von „sqlservr.exe“ von der Eingabeaufforderung aus gestartet wird, wird [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nicht als Dienst gestartet. Es ist daher nicht möglich, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe von **net** -Befehlen zu beenden. Benutzer können eine Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]herstellen, aber die Tools von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zeigen den Status des Dienstes an. Der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Konfigurations-Manager gibt daher vollkommen richtig an, dass der Dienst beendet wurde. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] kann eine Verbindung zum Server herstellen, gibt jedoch ebenfalls an, dass der Dienst beendet wurde.

## <a name="compatibility-support"></a>Kompatibilitätsunterstützung
Die folgenden Parameter sind veraltet und werden in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]nicht unterstützt.

|Parameter | Weitere Informationen|
|:-----|:-----|
|**-h** | Wurde in früheren Versionen der 32-Bit-Instanzen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwendet, um virtuellen Adressraum für Hot-Add-Arbeitsspeichermetadaten zu reservieren, wenn AWE aktiviert ist. Unterstützt [!INCLUDE[sssql14](../includes/sssql14-md.md)]durch. Weitere Informationen finden Sie unter [Nicht mehr unterstützte SQL Server-Funktionen in SQL Server 2016](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md).|
|**-g** | *memory_to_reserve*<br/><br>Gilt für frühere Versionen von 32-Bit-Instanzen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]von. Unterstützt [!INCLUDE[sssql14](../includes/sssql14-md.md)]durch. Gibt in Form einer ganzen Zahl an, wie viele Megabytes (MB) des Arbeitsspeichers [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] für Speicherbelegungen innerhalb des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Prozesses, jedoch außerhalb des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Speicherpools übrig lässt. Weitere Informationen finden Sie [in der Dokumentation zu SQL Server 2014 unter Konfigurationsoptionen für den Server Arbeitsspeicher](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options?view=sql-server-2014).|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Weitere Informationen
 [Startoptionen für den Datenbank-Engine-Dienst](../database-engine/configure-windows/database-engine-service-startup-options.md)
