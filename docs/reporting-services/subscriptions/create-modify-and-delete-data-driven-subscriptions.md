---
title: Erstellen, Ändern und Löschen von datengesteuerten Abonnements | Microsoft-Dokumentation
ms.date: 06/12/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- query-based subscriptions [Reporting Services]
- queries [Reporting Services], data-driven subscriptions
- subscriptions [Reporting Services], data-driven
- data-driven subscriptions
ms.assetid: 0ba2093e-9393-4eb6-af06-9da10988cfaf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b385e04cf2efa103dba4a66d4e794a7984814fb4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "67140270"
---
# <a name="create-modify-and-delete-data-driven-subscriptions"></a>Erstellen, Ändern und Löschen von datengesteuerten Abonnements
  Ein datengesteuertes Abonnement ist ein abfragebasiertes Abonnement, das die Datenwerte abfragt, die zum Verarbeiten des Abonnements zur Laufzeit verwendet werden. Wenn das Abonnement ausgelöst wird, wird eine Abfrage verarbeitet, die aktuelle Informationen über Empfänger, Berichtsübermittlungsoptionen, Renderingformate und Parametereinstellungen abruft. Die Abfrageergebnisse werden mit der Abonnementdefinition kombiniert. Dabei wird ein dynamisches Abonnement erstellt, das  Daten verwendet, die bereits in einer Mitarbeiterdatenbank, einer Kundendatenbank oder einer beliebigen Datenbank liegen und Informationen enthalten,  die als Abonnentendaten verwendbar sind.  
  
 Verwenden Sie zum Erstellen eines neuen datengesteuerten Abonnements, oder ändern ein vorhandenes Abonnement, das **verwalten** > **Abonnements** der Webportal auf der Seite. Die **Abonnements** Seite führt Sie durch jeden Schritt erstellen oder Ändern eines Abonnements. Ein bereits erstelltes Abonnement öffnen Sie mithilfe der Seite **Meine Abonnements** oder der Liste „Abonnements“ eines Berichts. Erfahren Sie, wie Sie ein datengesteuertes Abonnement erstellen, indem Sie die Seite [Erstellen eines datengesteuerten Abonnements (SSRS-Tutorial)](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md) aufrufen.  
  
 Inhalt dieses Artikels:  
  
-   [Verwalten und Löschen eines datengesteuerten Abonnements](#bkmk_manage_and_delete)  
  
-   [Erstellen und Ändern eines datengesteuerten Abonnements](#bkmk_create_and_modify)  
  
-   [Definieren einer Abfrage zum Abrufen von Abonnementdaten](#bkmk_define_query)  
  
-   [Ausführen eines Abonnements](#bkmk_run_subscription)  
  
##  <a name="bkmk_manage_and_delete"></a> Verwalten und Löschen eines datengesteuerten Abonnements  
 Ein datengesteuertes Abonnement, die in Bearbeitung ist nicht beendet oder gelöscht wird, über das Webportal. Aus diesem Grund ist es vorteilhaft, einen freigegebenen Zeitplan zu verwenden, um ein datengesteuertes Abonnement auszulösen. Falls Sie die Verarbeitung eines Abonnements vorübergehend unterbinden möchten, können Sie den Zeitplan anhalten, mit dem das Abonnement ausgelöst wird. Weitere Informationen finden Sie unter [Erstellen und Verwalten von Abonnements für Berichtsserver im einheitlichen Modus](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md).  
  
 Um ein datengesteuertes Abonnement zu löschen, wählen Sie das Kontrollkästchen neben dem Bericht auf dem **Abonnements** Seite, und wählen Sie dann **löschen**.  
  
 Anweisungen zum Abbrechen eines datengesteuerten Abonnements finden Sie unter [Verwalten eines ausgeführten Prozesses](../../reporting-services/subscriptions/manage-a-running-process.md).  
  
##  <a name="bkmk_create_and_modify"></a> Erstellen und Ändern eines datengesteuerten Abonnements  
 Um ein datengesteuertes Abonnement zu erstellen, wählen Sie einen Bericht aus, der gespeicherte oder keine Anmeldeinformationen verwendet. Beim Erstellen des datengesteuerten Abonnements sollten Sie eine Benennungskonvention für das Beschreibungsfeld festlegen, damit Standardabonnements problemlos von datengesteuerten Abonnements unterschieden werden können.  
  
### <a name="to-create-a-data-driven-subscription-native-mode"></a>So erstellen Sie ein datengesteuertes Abonnement (einheitlicher Modus)  
  
1. Im Webportal, navigieren Sie zu dem Ordner, der den Bericht enthält, mit der rechten Maustaste in des Berichts und wählen Sie **verwalten** aus dem Dropdownmenü aus.  
  
2. Wählen Sie die Registerkarte **Abonnements** aus.  
  
3. Wählen Sie **+ neues Abonnement** auf die **Abonnements** Seite.  
  
### <a name="to-create-a-data-driven-subscription-sharepoint-mode"></a>So erstellen Sie ein datengesteuertes Abonnement (SharePoint-Modus)  
  
1. Zeigen Sie in der SharePoint-Dokumentbibliothek auf den Bericht, öffnen Sie das Menü "Optionen", und klicken Sie auf **Abonnements verwalten**.  
  
2. Klicken Sie auf **Datengesteuertes Abonnement hinzufügen**.  
  
### <a name="to-modify-an-existing-data-driven-subscription-native-mode"></a>So ändern Sie ein vorhandenes datengesteuertes Abonnement (einheitlicher Modus)  
  
1. Im Webportal, navigieren Sie zu dem Ordner, der den Bericht enthält, mit der rechten Maustaste in des Berichts und wählen Sie **verwalten** aus dem Dropdownmenü aus.  
  
2. Wählen Sie die Registerkarte **Abonnements** aus.  
  
3. Aktivieren Sie das Kontrollkästchen neben dem Abonnement, das Sie ändern möchten, und wählen Sie **bearbeiten**. Datengesteuerte Abonnements waren, werden der Wert "datengesteuerten" in der **Typ** Spalte.  
  
### <a name="to-modify-an-existing-data-driven-subscription-sharepoint-mode"></a>So ändern Sie ein vorhandenes datengesteuertes Abonnement (SharePoint-Modus)  
  
1.  Zeigen Sie in der SharePoint-Dokumentbibliothek auf den Bericht, öffnen Sie das Menü "Optionen", und klicken Sie auf **Abonnements verwalten**.  
  
2.  Wählen Sie das Abonnement aus, das Sie ändern möchten.  
  
    > [!NOTE]  
    > Jeder angegebene Wert kann geändert werden. Alle Werte werden so wie beim Erstellen angezeigt, außer dem Kennwort, mit dem auf den Abonnentendatenspeicher zugegriffen wird. Sie müssen das Kennwort bei jeder Änderung von Werten auf der zweiten Seite oder einer beliebigen nachfolgenden Seite erneut eingeben.  
  
  Bevor Sie ein datengesteuertes Abonnement erstellen können, müssen die folgenden Anforderungen erfüllt sein:  
  
-   **Berichtsanforderungen**. Der Bericht muss gespeicherte oder keine Anmeldeinformationen zum Abrufen des Inhalts zur Laufzeit verwenden. Sie können keine Berichte abonnieren, die angenommene oder delegierte Anmeldeinformationen zum Verbinden mit einer externen Datenquelle verwenden. Die Anmeldeinformationen des Benutzers, der das Abonnement erstellt oder besitzt, sind zum Zeitpunkt der Verarbeitung des Abonnements nicht verfügbar. Bei den gespeicherten Anmeldeinformationen kann es sich um ein Windows-Konto oder ein Datenbank-Benutzerkonto handeln. Weitere Informationen finden Sie unter [Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
     Sie können keine mit dem Berichts-Generator erstellten Berichte abonnieren, die ein Modell als Datenquelle verwenden, das Sicherheitseinstellungen für Modellelemente enthält. Diese Einschränkung bezieht sich nur auf Berichte, die Sicherheitseinstellungen für Modellelemente verwenden.  
  
     Sie können keine datengesteuerten Abonnements für Berichte erstellen, die den `User!UserID` -Ausdruck enthalten.  
  
-   **Datenanforderungen**. Es muss eine externe Datenquelle mit Abonnentendaten vorhanden sein, auf die zugegriffen werden kann.  
  
-   **Benutzeranforderungen**. Der Autor des Abonnements benötigt die Berechtigungen "Berichte verwalten" sowie "Alle Abonnements verwalten". Weitere Informationen zu Berechtigungen auf Elementebene finden Sie unter [Aufgaben und Berechtigungen](../../reporting-services/security/tasks-and-permissions.md). Außerdem muss er über die notwendigen Anmeldeinformationen für den Zugriff auf die externe Datenquelle mit Abonnentendaten verfügen.  
  
##  <a name="bkmk_define_query"></a> Definieren einer Abfrage zum Abrufen von Abonnementdaten  
 Für ein datengesteuertes Abonnement muss eine Abfrage oder ein Befehl zum Abrufen von Abonnentendaten angegeben werden. Die Abfrage sollte pro Abonnent eine Zeile generieren. Falls Sie die E-Mail-Übermittlungserweiterung verwenden, sollte die Abfrage für jeden Abonnenten einen gültigen E-Mail-Alias zurückgeben. Die Anzahl von durchgeführten Übermittlungen basiert auf der Anzahl der von der Abfrage zurückgegebenen Zeilen. Besteht das Rowset aus 10.000 Zeilen, übermittelt das Abonnement 10.000 Berichte.  
  
 Wenn die Ausführung der Abfrage zeitaufwändig ist, können Sie den Timeoutwert erhöhen, um eine schnellere Verarbeitung zu ermöglichen.  
  
 Für diesen Schritt muss die Abfrage überprüft werden. Erst dann können Sie den Vorgang fortsetzen. Bei der Überprüfung wird die Abfrage nicht verarbeitet, es wird jedoch eine Liste aller Spalten im Rowset zurückgegeben, sodass Sie später auf diese Spalten verweisen können. Falls die Überprüfung der Abfrage fehlschlägt, können Sie den Vorgang nicht fortsetzen. Dies ist der Fall, wenn die Verbindung zur Datenquelle ungültig ist oder die Abfragesyntax fehlerhaft ist. Klicken Sie auf die Schaltfläche **Zurück** , um die Angaben zur Datenquelle zu korrigieren.  
  
##  <a name="bkmk_run_subscription"></a> Ausführen eines Abonnements  
 Sie müssen Bedingungen für die Abonnementverarbeitung angeben. Sie können einen Zeitplan angeben oder mit den Updates einer Momentaufnahme zur Berichtsausführung die Verarbeitung des Abonnements auslösen. Das Verarbeiten von datengesteuerten Abonnements ist mit der Verarbeitung von Standardabonnements identisch.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Verwalten von Abonnements für Berichtsserver im einheitlichen Modus](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [Abonnements und Übermittlung &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Das Webportal eines Berichtsservers (einheitlicher SSRS-Modus)](../../reporting-services/web-portal-ssrs-native-mode.md)   
 [Erstellen und Verwalten von Abonnements für Berichtsserver im einheitlichen Modus](create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [Arbeiten mit Abonnements (Webportal)](../../reporting-services/working-with-subscriptions-web-portal.md) [verwenden Meine Abonnements (Native Mode Report Server)](../../reporting-services/subscriptions/use-my-subscriptions-native-mode-report-server.md)  
 