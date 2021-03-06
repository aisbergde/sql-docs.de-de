---
title: 'Aufgabe 8: Erstellen einer Verbunddomänenregel | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: cff3b662-7876-4445-9bdd-96be35b3ca0c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7e40ec982a9b2c43c3d55ec60179ac9a0b80e8a1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489630"
---
# <a name="task-8-creating-a-composite-domain-rule"></a>Aufgabe 8: Erstellen einer Verbunddomänenregel
  In dieser Aufgabe erstellen Sie eine Regel für die **Address Validation** verbunddomäne. Sie definieren eine domänenübergreifende Regel: Wenn **City** ist **Berlin**, **Zustand** muss **Zertifizierungsstelle** , in denen **City** und **Zustand** zwei Domänen sind.  
  
1.  Wechseln Sie im rechten Bereich die **VD-Regeln** Registerkarte.  
  
2.  Klicken Sie auf **Fügt eine neue domänenregel hinzu** auf der Symbolleiste.  
  
3.  Typ **City Regel** für **Namen** , und drücken Sie **EINGABETASTE**.  
  
4.  In der **erstellen Sie eine Regel** wählen Sie im Bereich **City** in der Domänenliste aus, und wählen Sie die Bedingung **Wert ist gleich** und **Berlin** für die -Wert.  
  
5.  In der **dann** wählen Sie im Bereich **Zustand** in der Domänenliste aus, und wählen **Wert ist gleich**, Typ **Zertifizierungsstelle** für Wert ein, und drücken Sie **Registerkarte**.  
  
     ![Verbunddomänenregel](../../2014/tutorials/media/et-creatingacompositedomainrule.jpg "Verbunddomänenregel")  
  
6.  Klicken Sie auf **schließen** Schaltfläche am unteren Rand der Seite auf der Hauptseite des DQS-Client wechseln. In der nächsten Lektion veröffentlichen Sie die Wissensdatenbank. Beachten Sie, dass die Wissensdatenbank gesperrt ist (Schlosssymbol).  
  
## <a name="next-step"></a>Nächster Schritt  
 [Aufgabe 9: Konfigurieren eines Reference Data Service](../../2014/tutorials/task-9-configuring-a-reference-data-service.md)  
  
  
