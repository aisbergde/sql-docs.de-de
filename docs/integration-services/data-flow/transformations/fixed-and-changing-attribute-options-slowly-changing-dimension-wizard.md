---
title: Optionen für feste und veränderliche Attribute (Assistent für langsam veränderliche Dimensionen) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.attriboption.f1
ms.assetid: c841345c-7d03-452f-9379-1c8c464f029c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c5dd0fcdf9cceb0e1290f56bd4c6eb2459e6da3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67944406"
---
# <a name="fixed-and-changing-attribute-options-slowly-changing-dimension-wizard"></a>Optionen für feste und veränderliche Attribute (Assistent für langsam veränderliche Dimensionen)

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Geben Sie mithilfe des Dialogfelds **Optionen für feste und veränderliche Attribute** an, wie auf Änderungen bei festen und veränderlichen Attributen reagiert werden soll.  
  
 Weitere Informationen zu diesem Assistenten finden Sie unter [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>enthalten  
 **Feste Attribute**  
 Geben Sie für feste Attribute an, ob der Task fehlschlagen soll, wenn bei einem festen Attribut eine Änderung festgestellt wird.  
  
 **Veränderliche Attribute**  
 Geben Sie für veränderliche Attribute an, ob der Task zusätzlich zu aktuellen Datensätzen veraltete oder abgelaufene Datensätze ändern soll, wenn bei einem veränderlichen Attribut eine Änderung erkannt wird. Ein abgelaufener Datensatz ist ein Datensatz, der durch eine Änderung in einem Verlaufsattribut (eine Änderung vom Typ 2) durch einen neueren Datensatz ersetzt wurde. Das Auswählen dieser Option verursacht möglicherweise zusätzliche Verarbeitungsanforderungen für ein im relationalen Data Warehouse erstelltes mehrdimensionales Objekt.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Konfiguration von Ausgaben mithilfe des Assistenten für langsam veränderliche Dimensionen](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
