---
title: PropertyIdx-Eigenschaftswert (ClientNetworkProtocolProperty-Klasse) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- PropertyIdx Property (ClientNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PropertyIdx property
ms.assetid: d7845962-ac68-4435-9c59-70ec450fec88
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1b9c9f1adde1e60ffaae8186691daee051c9e56b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040778"
---
# <a name="propertyidx-property-clientnetworkprotocolproperty-class"></a>PropertyIdx-Eigenschaft (ClientNetworkProtocolProperty-Klasse)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Ruft den Indexwert der Eigenschaft in dem Eigenschaftsarray ab, auf das durch die [Properties-Eigenschaft (ClientNetworkProtocol-Klasse)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/properties-property-clientnetworkprotocol-class.md) des [ClientNetworkProtocol-Klassenobjekts](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) verwiesen wird, oder legt diesen fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.PropertyIdx [= value]  
```  
  
## <a name="parts"></a>Teile  
 *object*  
 A [ClientNetworkProtocolProperty-Klassenobjekt](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) , das ein Attribut des vom [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Client verwendeten Netzwerkprotokolls darstellt.  
  
## <a name="property-valuereturn-value"></a>Eigenschaftswert/Rückgabewert  
 Ein **uint32** -Wert, der den Array-Indexwert der aktuellen Eigenschaft angibt.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren von Clientprotokollen](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
