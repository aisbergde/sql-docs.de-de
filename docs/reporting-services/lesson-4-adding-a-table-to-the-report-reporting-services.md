---
title: 'Lektion 4: Hinzufügen einer Tabelle zum Bericht (Reporting Services) | Microsoft-Dokumentation'
ms.date: 04/29/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 5ddf2914-bcdd-427d-8cba-0ccb8342f819
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e925dec5eb14365a6c313349599a77ffe1d7ab13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "65106008"
---
# <a name="lesson-4-adding-a-table-to-the-report-reporting-services"></a>Lektion 4: Hinzufügen einer Tabelle zum Bericht (Reporting Services)

Nach dem Definieren des Datasets können Sie mit dem Entwerfen des Berichts beginnen. Sie können ein Berichtslayout erstellen, indem Sie *Berichtsobjekte* aus der **Toolbox** auf die **Entwurfsoberfläche** ziehen. Es gibt unter anderem folgende Arten von Berichtobjekten:

- Tabelle
- Textfeld
- image
- Linie
- Rechteck
- Diagramm
- Karte

Elemente, die wiederholte Zeilen von Daten aus zugrunde liegenden Datasets enthalten, werden als *Datenbereiche*bezeichnet. Nachdem Sie einen Datenbereich hinzugefügt haben, können Sie diesem Felder hinzufügen. Ein einfacher Bericht umfasst nur einen Datenbereich. Sie können weitere Datenbereiche hinzufügen, um mehr Informationen darzustellen, z. B. ein Diagramm.

## <a name="add-a-table-data-region-and-fields-to-a-report-layout"></a>Hinzufügen von Tabellendatenbereichen und Feldern zu einem Berichtslayout

1. Wählen Sie die Registerkarte **Toolbox** im linken Bereich des Berichts-Designers aus. Klicken Sie anschließend mit der Maus auf das Objekt **Tabelle**, und ziehen Sie es auf die Entwurfsoberfläche des Berichts. Vom Berichts-Designer wird ein Tabellendatenbereich mit drei Spalten in der Mitte der Entwurfsoberfläche gezeichnet. Wenn die Registerkarte **Toolbox** nicht angezeigt wird, klicken Sie auf **Ansicht** > **Toolbox**.

    ![ssrs_ssdt_Tabelle_hinzufügen](media/ssrs-ssdt-addtable.png)

    Sie können auch dem Bericht eine Tabelle aus der Entwurfsoberfläche hinzufügen. Klicken Sie mit der rechten Maustaste auf die Entwurfsoberfläche und anschließend auf **Einfügen** > **Tabelle**.

2. Erweitern Sie im **Berichtsdatenbereich** „AdventureWorksDataset“, um die Felder anzuzeigen.

3. Ziehen Sie das Feld `[Date]` vom **Berichtsdatenbereich** in die erste Spalte der Tabelle.

    > [!IMPORTANT]
    > Wenn Sie das Feld in der ersten Spalte ablegen, werden zwei Vorgänge ausgeführt. Zunächst zeigt der Berichts-Designer den als *Feldausdruck* bezeichneten Feldnamen in der Datenzelle in eckigen Klammern (`[Date]`) an. Anschließend wird eine Spaltenbezeichnung zur Kopfzeile über dem Feldausdruck hinzugefügt. Standardmäßig entspricht die Spaltenbezeichnung dem Namen des Felds. Sie können die Spaltenbezeichnung auswählen und einen neuen Wert eingeben, wenn Sie diesen ändern möchten.

4. Ziehen Sie das Feld `[Order]` vom **Berichtsdatenbereich** in die zweite Spalte der Tabelle.

5. Ziehen Sie das Feld `[Product]` vom **Berichtsdatenbereich** in die dritte Spalte der Tabelle.

6. Ziehen Sie das Feld `[Qty]` an den rechten Rand der dritten Spalte, bis ein vertikaler Cursor angezeigt wird und der Mauszeiger ein Pluszeichen (+) anzeigt. Wenn Sie die Maustaste loslassen, wird eine vierte Spalte für den Feldausdruck `[Qty]` erstellt.

    ![ssrs_tutorial_Spalte_hinzufügen](media/ssrs-tutorial-addcolumn.png)

7. Fügen Sie das `[LineTotal]`-Feld auf dieselbe Weise hinzu, und erstellen Sie dabei eine fünfte Spalte. Als Spaltenbezeichnung wird „Line Total“ eingegeben. Der Berichts-Designer erstellt für die Spalte automatisch einen besser lesbaren Namen, indem er „LineTotal“ in zwei Wörter aufgeteilt wird.

Die folgende Abbildung zeigt einen Datenbereich einer Tabelle, der mit folgenden Feldern aufgefüllt wurde: Date, Order, Product, Qty und Line Total.
![rs_GrundlegendeTabellendetailsEntwurf](media/rs-basictabledetailsdesign.png)

## <a name="preview-your-report"></a>Vorschau des Berichts

Wenn Sie einen Bericht in der Vorschau anzeigen, können Sie den gerenderten Bericht überprüfen, ohne ihn zuvor auf einem Berichtsserver zu veröffentlichen. Rufen Sie beim Entwerfen Ihres Berichts regelmäßig die Vorschau auf. So können Sie das Design und die Datenverbindung überprüfen und somit Fehler und Probleme noch im Entwurfsprozess beheben.

### <a name="to-preview-a-report"></a>So zeigen Sie die Vorschau eines Berichts an

- Klicken Sie auf die Registerkarte **Vorschau**. Der Berichts-Designer führt den Bericht aus und zeigt ihn in der **Vorschau** an.

    ![ssrs_ssdt_preview](media/ssrs-ssdt-preview.png)

In der folgenden Abbildung wird ein Teil des Berichts in der **Vorschau** angezeigt.

   ![Vorschau, Detailzeilen der Tabelle mit fünf Spalten](media/rs-basictabledetailspreview.png "Vorschau, Detailzeilen der Tabelle mit fünf Spalten")

Sehen Sie sich die Werte für „Date“ und „Line Total“ an. In der nächsten Lektion erfahren Sie, wie Sie diese formatieren können, um die Ansicht übersichtlicher zu gestalten.

> [!NOTE]
> Klicken Sie im Menü **Datei** auf **Alle Speichern**, um den Bericht zu speichern.

## <a name="next-steps"></a>Nächste Schritte

Sie haben Ihrem Bericht erfolgreich einen Tabellendatenbereich hinzugefügt, dem Datenbereich Felder hinzugefügt und den Bericht in der Vorschau angezeigt. In der nächsten Lektion erfahren Sie, wie Spaltenüberschriften und Feldausdrücke formatiert werden. Fahren Sie mit [Lektion 5: Formatieren eines Berichts &#40;Reporting Services&#41;](lesson-5-formatting-a-report-reporting-services.md) fort.
  
## <a name="see-also"></a>Siehe auch

[Tabellen &#40;Berichts-Generator und SSRS&#41;](report-design/tables-report-builder-and-ssrs.md)  
[Datasetfeld-Auflistung &#40;Berichts-Generator und SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
