---
title: Erstellen eines Dateiattributs (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating file attributes [Master Data Services]
- attributes [Master Data Services], creating file attributes
ms.assetid: d224886b-2ef1-4658-8b01-2213cc4b8df6
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ea016778880ad4254d75a567659c9d7fc428592d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906722"
---
# <a name="create-a-file-attribute-master-data-services"></a>Erstellen eines Dateiattributs (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Erstellen Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]ein Dateiattribut, um Attributwerte mit Dateien aufzufüllen.  
  
## <a name="prerequisites"></a>Vorraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
-   Eine Entität muss vorhanden sein, um das Attribut dafür erstellen zu können. Weitere Informationen finden Sie unter [Erstellen einer Entität &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
## <a name="attribute-information"></a>Attributinformationen  
 Für jedes erstellte Attribut wird dem Raster eine Zeile mit sieben Spalten hinzugefügt. In der folgenden Tabelle werden diese Spalten beschrieben.  
  
|Spalte|Beschreibung|  
|------------|-----------------|  
|Status|Der Attributstatus.<br /><br /> Wenn Sie auf „Speichern“ klicken, wird das Bild ![Symbol für den Aktualisierungsstatus](../master-data-services/media/mds-statusicon-updating.png "Icon for updating status") angezeigt, das angibt, dass das Attribut aktualisiert wird.<br /><br /> Wenn beim Erstellen oder Bearbeiten eines Attributs Fehler auftreten, wird das Bild ![Fehlerstatussymbol](../master-data-services/media/mds-statusicon-error.png "Icon for error status") angezeigt.<br /><br /> Andernfalls ist der Status „OK“, und das Bild ![Symbol für den Status OK](../master-data-services/media/mds-statusicon-ok.png "Icon for OK status") wird angezeigt.|  
|Name|Der Attributname.|  
|Anzeigename|Der Anzeigename des Attributs.|  
|Beschreibung|Die Attributbeschreibung.|  
|Pixelbreite anzeigen|Die Breite des Attributs.|  
|Typ und Eigenschaften|Die Typ- und Datentypinformationen des Attributs.|  
|Änderungsnachverfolgung aktivieren|Gibt an, ob das Attribut für die Änderungsnachverfolgung aktiviert ist, und zeigt die Gruppennummer in Klammern.|  
  
 Wenn Sie auf ein Attribut klicken, werden die folgenden Informationen angezeigt.  
  
-   **Erstellt von**: Name des Benutzers, der das Attribut erstellt hat.  
  
-   **Am**: Datum und Uhrzeit der Erstellung des Attributs.  
  
-   **Aktualisiert von**: Name des Benutzers, der das Attribut aktualisiert hat.  
  
-   **Am**: Datum und Uhrzeit der letzten Aktualisierung des Attributs.  
  
### <a name="to-create-a-file-attribute"></a>So erstellen Sie ein Dateiattribut  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Wählen Sie auf der Seite **Modell verwalten** im Raster ein Modell aus, und klicken Sie dann auf **Entitäten**.  
  
3.  Wählen Sie auf der Seite **Entität verwalten** die Zeile der Entität aus, für die Sie ein Attribut erstellen möchten.  
  
4.  Klicken Sie auf **Attribute**.  
  
5.  Führen Sie auf der Seite **Attribute verwalten** einen der folgenden Schritte aus, und klicken Sie dann auf **Hinzufügen**.  
  
    -   Wenn das Attribut für Blattelemente bestimmt ist, wählen Sie **Blatt** im Listenfeld **Elementtypen** aus.  
  
    -   Wenn das Attribut für konsolidierte Elemente bestimmt ist, wählen Sie **Konsolidiert** im Listenfeld **Elementtypen** aus.  
  
    -   Wenn das Attribut für Sammlungen bestimmt ist, wählen Sie **Sammlung** im Listenfeld **Elementtypen** aus.  
  
6.  Geben Sie im Feld **Name** einen Namen für das Attribut ein. Eine Liste von Wörtern, die nicht als Attributnamen verwendet werden sollten, finden Sie unter [Reservierte Wörter &#40;Master Data Services&#41;](../master-data-services/reserved-words-master-data-services.md).  
  
7.  Geben Sie optional einen Anzeigenamen ein und in das Feld **Beschreibung** eine Beschreibung des Attributs ein.  
  
8.  Geben Sie im Feld **Pixelbreite anzeigen** die Breite der Attributspalte ein, die im **Explorerraster** angezeigt werden soll.  
  
9. Wählen Sie in der Liste **Attributtyp** die Option **Datei**aus.  
  
10. Wählen Sie aus der Liste **Dateierweiterung** einen Dateityp aus, den ein Benutzer hochladen kann, oder akzeptieren Sie den Standardwert (*\*), um alle Dateitypen zuzulassen.  
  
11. Optional können Sie **Änderungsnachverfolgung aktivieren** auswählen, um Änderungen an Gruppen von Attributen nachzuverfolgen. Weitere Informationen finden Sie unter [Hinzufügen von Attributen zu einer Änderungsnachverfolgungsgruppe &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).  
  
12. Klicken Sie auf **Speichern**.  
  
## <a name="see-also"></a>Siehe auch  
 [Attribute &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)   
 [Ändern eines Attributnamens und Datentyps &#40;Master Data Services&#41;](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)   
 [Erstellen eines domänenbasierten Attributs &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [Erstellen eines Textattributs &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)  
  
  
