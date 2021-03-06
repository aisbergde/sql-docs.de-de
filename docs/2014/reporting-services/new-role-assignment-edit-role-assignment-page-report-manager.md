---
title: 'Neue Rollenzuweisung: Bearbeiten Sie die Rolle ", Seite" Zuweisung "(Berichts-Manager) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 3319ced0-4b86-42af-b18d-da41a625113c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a9480b0729e7c08117ba5633c6934eca1903a61b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108158"
---
# <a name="new-role-assignment-edit-role-assignment-page-report-manager"></a>Neue Rollenzuweisung: Bearbeiten Sie die Rolle ", Seite" Zuweisung "(Berichts-Manager)
  Verwenden Sie die Seite Neue Rollenzuweisung oder Rollenzuweisung bearbeiten, um Elementen und Vorgängen des Berichtsservers Berechtigungen zu erteilen. Jeder Benutzer, der auf den Berichtsserver zugreifen möchte, muss über eine Rollenzuweisung verfügen, die die Zugriffsebene definiert. Sie können Rollenzuweisungen im Stammknoten oder in einem bestimmten Bericht, Modell, Ordner, einer bestimmten Ressource oder freigegebenen Datenquelle erstellen. Die Sicherheit in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] wird durch Rollenzuweisungen erzwungen, die Sie auf Elemente anwenden. Eine Rollenzuweisung ordnet eine Gruppe oder einen Benutzer einer Rollendefinition zu, wobei jede Rollendefinition die Aufgaben identifiziert, die Gruppen oder Benutzer in Bezug auf ein spezifisches Element ausführen können.  
  
 Rollenzuweisungen auf Elementebene können weit reichende Auswirkungen haben. Obwohl sie in der Regel mit einem einzelnen Bericht oder Ordner verbunden sind, können sie auch auf einer höheren Ebene in der Ordnerhierarchie definiert werden und von Ordnern und Elementen weiter unten in der Struktur geerbt werden. Weitere Informationen finden Sie unter [Gewähren von Benutzerzugriff auf einen Berichtsserver &#40;Berichts-Manager&#41;](security/grant-user-access-to-a-report-server.md)sollten nur sehr wenige Benutzer zugewiesen werden.  
  
## <a name="navigation"></a>Navigation  
 Verwenden Sie folgendes Verfahren, um zu dieser Position in der Benutzeroberfläche zu navigieren.  
  
###### <a name="to-open-the-new-role-assignment-or-edit-role-assignment-page"></a>So öffnen Sie die Seite Neue Rollenzuweisung oder Rollenzuweisung bearbeiten  
  
1.  Öffnen Sie den Berichts-Manager, und suchen Sie ein Element, für das Sie eine neue Rollenzuweisung hinzufügen oder eine Rollenzuweisung bearbeiten möchten.  
  
2.  Zeigen Sie auf das Element, und klicken Sie auf den Dropdownpfeil.  
  
3.  Klicken Sie im Dropdownmenü auf **Sicherheit**. Dadurch wird die Eigenschaftenseite Sicherheit für das Element geöffnet.  
  
4.  Wenn Sie eine neue Rollenzuweisung hinzufügen möchten, klicken Sie auf der Symbolleiste auf **Neue Rollenzuweisung**. Um eine Rollenzuweisung zu bearbeiten, klicken Sie neben dem Namen der Gruppe bzw. des Benutzers, die oder der bearbeitet werden soll, auf **Bearbeiten** .  
  
    > [!NOTE]  
    >  Falls ein Element aktuell die Sicherheitseinstellungen eines übergeordneten Elements erbt, klicken Sie auf der Symbolleiste auf **Elementsicherheit bearbeiten** , um die Sicherheitseinstellungen zu ändern.  
  
## <a name="options"></a>Optionen  
 **Gruppen- oder Benutzernamen ein**  
 Geben Sie den Namen eines Gruppen- oder Benutzerkontos ein, für das die Rollenzuweisung erstellt wird. Der Gruppen- oder Benutzername muss ein gültiges Windows-Domänenkonto sein. Geben Sie das Konto im folgenden Format: \<Domäne >\\< Konto\>.  
  
> [!NOTE]  
>  Dieses Feld ist nur auf der Seite Neue Rollenzuweisung verfügbar.  
  
 **Rolle**  
 Zeigt alle auf dem Berichtsserver definierten Rollen an, die zum Definieren der Sicherheit für Elemente verwendet werden können. Wenn Sie die Rollenzuweisung für einen Bericht oder Ordner erstellen oder bearbeiten, wählen Sie eine oder mehrere Rollen aus, bis die kombinierten Aufgaben die Aktionen beschreiben, die der Benutzer ausführen darf. Verwenden Sie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], um die Gruppe der von einer Rolle unterstützten Aufgaben anzuzeigen. Sie können im Berichts-Manager keine Rollen anzeigen, erstellen, ändern oder löschen. Anweisungen hierzu finden Sie unter [erstellen, löschen oder Ändern einer Rolle &#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md).  
  
 **Beschreibung**  
 Zeigt zusätzliche Informationen zur Rolle an. Bei vordefinierten Rollen wie z. B. **Browser** oder **Inhalts-Manager**werden in der Beschreibung die Aufgaben zusammengefasst, die von einer Rolle unterstützt werden.  
  
 **Rollenzuweisung löschen**  
 Klicken Sie auf diese Schaltfläche, um eine vorhandene Rollenzuweisung für einen Benutzer oder eine Gruppe zu löschen. Die letzte Rollenzuweisung kann nicht gelöscht werden, da jedes Element über mindestens eine Rollenzuweisung verfügen muss.  
  
> [!NOTE]  
>  Diese Schaltfläche ist nur auf der Seite Rollenzuweisung bearbeiten verfügbar.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen, Löschen oder Ändern einer Rolle &#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md)   
 [Erteilen von Berechtigungen für einen Berichtsserver im einheitlichen Modus](security/granting-permissions-on-a-native-mode-report-server.md)   
 [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Berichts-Manager-F1-Hilfe](../../2014/reporting-services/report-manager-f1-help.md)   
 [Rollenzuweisungen](security/role-assignments.md)   
 [Gewähren von Benutzerzugriff auf einen Berichtsserver &#40;Berichts-Manager&#41;](security/grant-user-access-to-a-report-server.md)  
  
  
