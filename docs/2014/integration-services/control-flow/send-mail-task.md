---
title: Mail senden (Task) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sendmailtask.f1
helpviewer_keywords:
- mail [Integration Services]
- Send Mail task
- e-mail [Integration Services]
- messages [Integration Services]
- sending messages
ms.assetid: fe0b7cbc-fe8e-4fe2-95b4-2953efff5869
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3308899190aa63ebb9be93c4c9af15d5e0f94600
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "62830394"
---
# <a name="send-mail-task"></a>Mail senden (Task)
  Der Task 'Mail senden' sendet eine E-Mail. Mithilfe des Tasks 'Mail senden' kann ein Paket Nachrichten senden, wenn Tasks im Paket-Workflow erfolgreich ausgeführt werden oder einen Fehler erzeugen, oder Nachrichten als Antwort auf ein Ereignis senden, das vom Paket zur Laufzeit ausgelöst wird. Beispielsweise kann mit diesem Task ein Datenbankadministrator über das erfolgreiche Ausführen des Tasks Datenbank sichern benachrichtigt werden.  
  
 Es gibt folgende Möglichkeiten, um den Task Mail senden zu konfigurieren:  
  
-   Geben Sie den Nachrichtentext für die E-Mail-Nachricht ein.  
  
-   Geben Sie ein Betreffzeile für die E-Mail-Nachricht ein.  
  
-   Legen Sie die Prioritätsstufe der Nachricht fest. Dieser Task unterstützt drei Prioritätsebenen: normal, niedrig und hoch.  
  
-   Geben Sie in den Zeilen An, Cc und Bcc die Empfänger an. Falls für den Task mehrere Empfänger angegeben sind, werden sie durch Semikolons getrennt.  
  
    > [!NOTE]  
    >  Die Zeilen An, Cc und Bcc sind auf 256 Zeichen in Übereinstimmung mit den Internetstandards begrenzt.  
  
-   Fügen Sie Anlagen hinzu. Falls für den Task mehrere Anlagen angegeben sind, werden sie durch einen senkrechten Strich (|) getrennt.  
  
    > [!NOTE]  
    >  Falls beim Ausführen des Pakets eine Anlagedatei nicht vorhanden ist, wird ein Fehler gemeldet.  
  
-   Geben Sie den zu verwendenden SMTP-Verbindungs-Manager an.  
  
    > [!IMPORTANT]  
    >  Der SMTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Windows-Authentifizierung. Er unterstützt keine Standardauthentifizierung.  
  
 Der Nachrichtentext kann eine von Ihnen eingegebene Zeichenfolge sein, eine Verbindung mit einer Datei, die den Text enthält, oder der Name einer Variablen, die den Text enthält. Dieser Task verwendet einen Dateiverbindungs-Manager, um eine Verbindung mit einer Datei herzustellen. Weitere Informationen finden Sie unter [Flat File Connection Manager](../connection-manager/file-connection-manager.md).  
  
 Dieser Task verwendet einen SMTP-Verbindungs-Manager, um eine Verbindung mit einem Mailserver herzustellen. Weitere Informationen finden Sie unter [SMTP Connection Manager](../connection-manager/smtp-connection-manager.md).  
  
## <a name="custom-logging-messages-available-on-the-send-mail-task"></a>Verfügbare benutzerdefinierte Meldungen für die Protokollierung für den Task 'Mail senden'  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task 'Mail senden' aufgelistet. Weitere Informationen finden Sie unter [Integration Services-Protokollierung &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) und [Benutzerdefinierte Meldungen für die Protokollierung](../custom-messages-for-logging.md).  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|`SendMailTaskBegin`|Zeigt an, dass das Senden einer E-Mail-Nachricht begonnen wurde.|  
|`SendMailTaskEnd`|Zeigt an, dass das Senden einer E-Mail-Nachricht beendet wurde.|  
|`SendMailTaskInfo`|Enthält beschreibende Informationen zum Task.|  
  
## <a name="configuring-the-send-mail-task"></a>Konfigurieren des Tasks Mail senden  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Editor für den Task „Mail senden“ &#40;Seite „Allgemein“&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor für den Task „Mail senden“ &#40;Seite „E-Mail“&#41;](../send-mail-task-editor-mail-page.md)  
  
-   [Seite Ausdrücke](../expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.SendMailTask.SendMailTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 Klicken Sie auf [!INCLUDE[ssIS](../../includes/ssis-md.md)] Festlegen der Eigenschaften eines Tasks oder Containers [, um Informationen zum Festlegen dieser Eigenschaften im](../set-the-properties-of-a-task-or-container.md)-Designer zu erhalten.  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   Technischer Artikel [Vorgehensweise: Senden von E-Mails mit Zustellungsbenachrichtigung in C#](https://go.microsoft.com/fwlink/?LinkId=237625)(Gewusst wie: Senden von E-Mails mit Zustellungsbenachrichtigung in C#) auf shareourideas.com  
  
## <a name="see-also"></a>Siehe auch  
 [Integration Services-Tasks](integration-services-tasks.md)   
 [Ablaufsteuerung](control-flow.md)  
  
  
