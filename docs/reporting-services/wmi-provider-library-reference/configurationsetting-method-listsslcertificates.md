---
title: 'ListSSLCertificates-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft-Dokumentation'
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- ListSSLCertificates method
ms.assetid: 88cd0936-b202-4ab8-90f2-d9c3f66d37f4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1e39c771872b0afbb614257145f447d1a47386a1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571339"
---
# <a name="configurationsetting-method---listsslcertificates"></a>ConfigurationSetting-Methode: ListSSLCertificates
  Gibt eine Liste der Zertifikate auf dem Berichtsservercomputer zurück  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Sub CreateSSLCertificateBinding (ByRef CertificateHash() as String, _  
    ByRef CertName() as String, ByRef HostName() as String, ByRef Length as Int32, _   
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListSSLCertificates(out string[] CertificateHash,   
    out string[] CertName, out string[] Hostname, out Int32 length,   
    out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameter  
 *CertificateHash[]*  
 [out] Der Hash der Zertifikate  
  
 *CertName[]*  
 [out] Die Namen des Zertifikats.  
  
 *HostName[]*  
 [out] Die Hostnamen der Zertifikate  
  
 *Länge*  
 [out] stellt die Länge der Arrays *CertificateHash*, *CertName* und *HostName* dar.  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Fehlercode gibt an, dass der Aufruf nicht erfolgreich war.  
  
## <a name="remarks"></a>Bemerkungen  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Weitere Informationen  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
