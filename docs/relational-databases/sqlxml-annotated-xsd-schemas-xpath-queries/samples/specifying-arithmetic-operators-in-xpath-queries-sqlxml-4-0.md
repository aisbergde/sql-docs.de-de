---
title: Angeben von arithmetischen Operatoren in XPath-Abfragen (SQLXML 4.0) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- arithmetic operators
- XPath operators [SQLXML]
- XPath queries [SQLXML], arithmetic operators
- operators [SQLXML]
ms.assetid: fdfbc87d-759f-4abc-acf5-a21de01f78d3
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4594fadb7c12ac187219c16cf8505dd77fa0c479
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119450"
---
# <a name="specifying-arithmetic-operators-in-xpath-queries-sqlxml-40"></a>Angeben von arithmetischen Operatoren in XPath-Abfragen (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Im folgenden Beispiel wird gezeigt, wie arithmetische Operatoren in XPath-Abfragen angegeben werden. Die XPath-Abfragen in diesem Beispiel werden für das in SampleSchema1.xml enthaltene Zuordnungsschema angegeben. Weitere Informationen zu diesem Beispielschema finden Sie unter [Annotated XSD-Beispielschema für XPath-Beispiele &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-specify-the--arithmetic-operator"></a>A. Angeben des arithmetischen *-Operators  
 Diese XPath-Abfrage gibt  **\<OrderDetail >** Elemente, die angegebene Prädikat erfüllen:  
  
```  
/child::OrderDetail[@UnitPrice * @Quantity = 12.350]  
```  
  
 In der Abfrage `child` ist die Achse und `OrderDetail` ist der Knotentest (TRUE, wenn **OrderDetail** ist ein  **\<Elementknoten >** , da die  **\< Element >** Knoten ist der primäre Knoten für die **untergeordneten** Achse). Für alle der  **\<OrderDetail >** Elementknoten, der Test im Prädikat angewendet wird, und nur die Knoten, die die Bedingung erfüllen, werden zurückgegeben.  
  
> [!NOTE]  
>  Die in XPath verwendeten Zahlen sind Gleitkommazahlen mit doppelter Genauigkeit, durch Vergleich der Gleitkommazahlen wie im Beispiel werden die Werte gerundet.  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>So testen Sie die XPath-Abfrage mit dem Zuordnungsschema  
  
1.  Kopieren der [Schema Beispielcode](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) und fügen Sie ihn in eine Textdatei. Speichern Sie die Datei unter dem Dateinamen SampleSchema1.xml.  
  
2.  Erstellen Sie die folgende Vorlage (ArithmeticOperatorA.xml), und speichern Sie sie in dem Verzeichnis, in dem SampleSchema1.xml gespeichert ist.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /OrderDetail[@UnitPrice * @OrderQty = 12.350]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungsschema (SampleSchema1.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     For more information, see [Using ADO to Execute SQLXML 4.0 Queries](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
```  
Here is the partial result set of the template execution:    
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-710" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
   ...  
</ROOT>  
```  
  
  
