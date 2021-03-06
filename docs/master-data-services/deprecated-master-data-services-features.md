---
title: Veraltete Funktionen von Master Data Services | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d8506bda-66dd-45a4-bfc9-3a10fa665acc
author: lrtoyou1223
ms.author: lle
manager: erikre
ms.openlocfilehash: b5212af4f19cdf26f6c332a83877880c80bc3741
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267034"
---
# <a name="deprecated-master-data-services-features"></a>Veraltete Funktionen von Master Data Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In diesem Thema werden die als veraltet markierten Funktionen von [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] beschrieben, die in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]noch verfügbar sind. Diese Funktionen werden voraussichtlich in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]entfernt. Als veraltet markierte Funktionen sollten in neuen Anwendungen nicht verwendet werden.  
  
## <a name="explicit-hierarchies-collections-and-related-components"></a>Explizite Hierarchien, Sammlungen und zugehörige Komponenten  
 Explizite Hierarchien, Sammlungen und zugehörige Komponenten sind veraltet. Elemente, die als konsolidierte Elemente modelliert wurden (übergeordnetes Element in einer expliziten Hierarchie), und Elementtypen aus Sammlungen werden in abgeleiteten Hierarchien als Blattelemente gestaltet. Die folgenden neuen Funktionen aktivieren abgeleitete Hierarchien, sodass diese an die Stelle der expliziten Hierarchien treten.  
  
-   Rekursive abgeleitete Hierarchien können nun auch verwendet werden, um Elementsicherheitsberechtigungen zuzuweisen.  
  
     Eine explizite Hierarchie entspricht einer rekursiven abgeleiteten Hierarchie mit einer einzelnen, nicht rekursiven Ebene unterhalb der rekursiven Ebene. Eine rekursive abgeleitete Hierarchie kann komplex sein und eine oder mehrere Ebenen unterhalb und/oder unterhalb einer rekursiven Ebene beinhalten.  
  
-   Die Seite „Abgeleitete Hierarchie“ im Explorer zeigt nun die nicht zugewiesenen (nicht verwendeten) Elemente für jede Ebene der Hierarchie. Nicht verwendete Knoten sind nach Hierarchieebene gruppiert. Elemente können per Drag & Drop oder Ausschneiden und Einfügen zwischen den nicht verwendeten Knoten und den Stammknoten verschoben werden.  
  
     In der Systemverwaltung werden nicht verwendete Knoten im Bereich **Vorschau** angezeigt. Im Bereich „Sicherheit“ werden die nicht verwendeten Knoten in den **Hierarchieelementberechtigungen** angezeigt. Jedem Element unter dem **Stammknoten** oder dem Knoten **Nicht verwendet** kann eine Berechtigung zugewiesen werden. Sowohl den **Stammelementen**, als auch den **nicht verwendeten**Elementen und den **nicht verwendeten** Pseudoelementen können ebenfalls Berechtigungen zugewiesen werden.  
  
-   Die gespeicherte Prozedur „mdm.udpConvertCollectionAndConsolidatedMembersToLeaf“ konvertiert explizite Hierarchien in abgeleitete rekursive Hierarchien. Außerdem konvertiert sie konsolidierte Elemente und Sammlungselemente in Blattelemente.  
  
     Explizite Hierarchien, konsolidierte Elementtypen und Sammlungselementtypen werden immer noch unterstützt. Die Ausführung der Prozedur ist daher optional. Wenn Sie diese Elemente verwenden, sollten Sie die gespeicherte Prozedur ausführen, da die Elemente veraltet sind.  
  
 Informationen zu expliziten Hierarchien, Sammlungen und konsolidierten Elementen finden Sie in den folgenden Themen.  
  
-   [Explizite Hierarchien &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [Sammlungen &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
-   [Elemente &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)  
  
## <a name="attribute-entity-transaction-log-type"></a>Transaktionsprotokolltyp von Entitäten  
Der Transaktionsprotokolltyp von Entitäten „Attribut“ ist veraltet, bitte migrieren Sie zum Transaktionsprotokolltyp von Entitäten „Element“. Informationen zu Transaktionsprotokolltypen von Entitäten finden Sie in folgendem Thema:
* [Ändern des Transaktionsprotokolltyps von Entitäten (Master Data Services)](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)
* [Elementrevisionsverlauf](../master-data-services/member-revision-history-master-data-services.md)
  
## <a name="external-resources"></a>Externe Ressourcen  
 Blogbeitrag: [Deprecated: Explicit Hierarchies and Collections (Veraltet: Explizite Hierarchien und Sammlungen)](https://go.microsoft.com/fwlink/p/?LinkId=615373) auf msdn.com.  
  
## <a name="see-also"></a>Siehe auch  
 [Eingestellte Master Data Services-Funktionen](../master-data-services/discontinued-master-data-services-features.md)  
  
  
