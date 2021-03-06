---
title: CREATE SERVICE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_SERVICE_TSQL
- SERVICE
- CREATE SERVICE
- SERVICE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- services [Service Broker], creating
- CREATE SERVICE statement
- contracts [Service Broker], service creation
ms.assetid: fb804fa2-48eb-4878-a12f-4e0d5f4bc9e3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 761a04baca38ee1301c8f51d8b69564f409fac1e
ms.sourcegitcommit: a97d551b252b76a33606348082068ebd6f2c4c8c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70745397"
---
# <a name="create-service-transact-sql"></a>CREATE SERVICE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Erstellt einen neuen Dienst. Bei einem [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Dienst handelt es sich um einen Namen für einen bestimmten Task oder eine Gruppe von Tasks. [!INCLUDE[ssSB](../../includes/sssb-md.md)] verwendet den Namen des Diensts zum Weiterleiten von Nachrichten, zum Übermitteln von Nachrichten an die richtige Warteschlange innerhalb einer Datenbank und zum Erzwingen des Vertrags für eine Konversation.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Themenlinksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE SERVICE service_name  
   [ AUTHORIZATION owner_name ]  
   ON QUEUE [ schema_name. ]queue_name  
   [ ( contract_name | [DEFAULT][ ,...n ] ) ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *service_name*  
 Der Name des zu erstellenden Diensts. Ein neuer Dienst wird in der aktuellen Datenbank erstellt. Der Besitzer dieses neuen Diensts ist der in der AUTHORIZATION-Klausel angegebene Prinzipal. Server-, Datenbank- und Schemaname können nicht angegeben werden. Bei *service_name* muss es sich um einen gültigen **sysname**-Wert handeln.  
  
> [!NOTE]  
> Erstellen Sie keinen Dienst, der das Schlüsselwort ANY für *service_name* verwendet. Wenn Sie `ANY` für einen Dienstnamen in `CREATE BROKER PRIORITY` festlegen, wird die Priorität für alle Dienste berücksichtigt. ANY steht nicht für einen Dienst mit dem Namen ANY.  
  
 AUTHORIZATION *owner_name*  
 Legt den Besitzer des Diensts auf den angegebenen Datenbankbenutzer bzw. die angegebene Rolle fest. Ist der aktuelle Benutzer **dbo** oder **sa**, kann *owner_name* der Name eines beliebigen gültigen Benutzers bzw. einer beliebigen gültigen Rolle sein. Andernfalls muss *owner_name* der Name des aktuellen Benutzers, der Name eines Benutzers, für den der aktuelle Benutzer IMPERSONATE-Berechtigungen besitzt, oder der Name einer Rolle sein, der der aktuelle Benutzer angehört.  
  
 ON QUEUE [ _schema_name_ **.** ] *queue_name*  
 Gibt den Namen der Warteschlange an, die Nachrichten für den Dienst empfängt. Die Warteschlange muss in der gleichen Datenbank vorhanden sein wie der Dienst. Wird *schema_name* nicht bereitgestellt, handelt es sich bei dem Schema um das Standardschema für den Benutzer, der die Anweisung ausführt.  
  
 *contract_name*  
 Gibt einen Vertrag an, der diesen Dienst zum Ziel haben kann. Dienstprogramme initiieren Konversationen mit diesem Dienst mithilfe der angegebenen Verträge. Werden keine Verträge angegeben, kann der Dienst nur Konversationen initiieren.  
  
 **[** DEFAULT **]**  
 Gibt an, dass der Dienst das Ziel von Konversationen sein kann, die dem DEFAULT-Vertrag entsprechen. Im Kontext dieser Klausel ist DEFAULT kein Schlüsselwort und muss als Bezeichner begrenzt sein. Der DEFAULT-Vertrag ermöglicht es beiden Seiten der Konversation, Nachrichten vom Nachrichtentyp DEFAULT zu senden. Der Nachrichtentyp DEFAULT verwendet für die Überprüfung NONE.  
  
## <a name="remarks"></a>Remarks  
 Ein Dienst macht die Funktionalität verfügbar, die von den Verträgen bereitgestellt wird, denen er zugeordnet ist, sodass sie von anderen Diensten verwendet werden können. Die `CREATE SERVICE`-Anweisung gibt die Verträge an, deren Ziel dieser Dienst ist. Ein Dienst kann nur ein Ziel für Konversationen sein, die die von dem Dienst angegebenen Verträge verwenden. Ein Dienst, der keine Verträge angibt, macht keine Funktionalität für andere Dienste verfügbar.  
  
 Konversationen, die von diesem Dienst initiiert werden, können einen beliebigen Vertrag verwenden. Sie erstellen einen Dienst ohne Angabe von Verträgen, wenn der Dienst nur Konversationen initiiert.  
  
 Wenn [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine neue Konversation von einem Remotedienst annimmt, bestimmt der Name des Zieldiensts die Warteschlange, in der der Broker Nachrichten in der Konversation anordnet.  
  
## <a name="permissions"></a>Berechtigungen  
 Die Berechtigung zum Erstellen eines Diensts liegt standardmäßig bei Mitgliedern der festen Datenbankrollen `db_ddladmin` oder `db_owner` bzw. der festen Serverrolle `sysadmin`. Der Benutzer, der die `CREATE SERVICE`-Anweisung ausführt, muss über die `REFERENCES`-Berechtigung für die Warteschlange und alle angegebenen Verträge verfügen.  
  
 Standardmäßig verfügen der Besitzer des Diensts, Mitglieder der festen Datenbankrollen `db_ddladmin` oder `db_owner` bzw. Mitglieder der festen Serverrolle `sysadmin` über die `REFERENCES`-Berechtigung für einen Dienst. `SEND`-Berechtigungen für einen Dienst liegen standardmäßig beim Besitzer des Diensts, bei Mitgliedern der festen Datenbankrolle `db_owner` oder bei Mitgliedern der festen Serverrolle `sysadmin`.  
  
 Ein Dienst kann kein temporäres Objekt sein. Dienstnamen, die mit **#** beginnen, sind zulässig. Hierbei handelt es sich jedoch um dauerhafte Objekte.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-service-with-one-contract"></a>A. Erstellen eines Diensts mit einem Vertrag  
 Im folgenden Beispiel wird der Dienst `//Adventure-Works.com/Expenses` in der `ExpenseQueue`-Warteschlange im `dbo`-Schema erstellt. Dialoge, die diesen Dienst zum Ziel haben, müssen dem Vertrag `//Adventure-Works.com/Expenses/ExpenseSubmission` entsprechen.  
  
```sql  
CREATE SERVICE [//Adventure-Works.com/Expenses]  
    ON QUEUE [dbo].[ExpenseQueue]  
    ([//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
### <a name="b-creating-a-service-with-multiple-contracts"></a>B. Erstellen eines Diensts mit mehreren Verträgen  
 Im folgenden Beispiel wird der Dienst `//Adventure-Works.com/Expenses` für die `ExpenseQueue`-Warteschlange erstellt. Dialoge, die diesen Dienst zum Ziel haben, müssen entweder dem Vertrag `//Adventure-Works.com/Expenses/ExpenseSubmission` oder dem Vertrag `//Adventure-Works.com/Expenses/ExpenseProcessing` entsprechen.  
  
```sql  
CREATE SERVICE [//Adventure-Works.com/Expenses] ON QUEUE ExpenseQueue  
    ([//Adventure-Works.com/Expenses/ExpenseSubmission],  
     [//Adventure-Works.com/Expenses/ExpenseProcessing]) ;  
```  
  
### <a name="c-creating-a-service-with-no-contracts"></a>C. Erstellen eines Diensts ohne Verträge  
 Im folgenden Beispiel wird die Dienstwarteschlange `//Adventure-Works.com/Expenses on the ExpenseQueue` erstellt. Dieser Dienst verfügt über keine Vertragsinformationen. Daher kann der Dienst nur der Initiator eines Dialogs sein.  
  
```sql  
CREATE SERVICE [//Adventure-Works.com/Expenses] ON QUEUE ExpenseQueue ;  
```  
  
## <a name="see-also"></a>Weitere Informationen  
 [ALTER SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-service-transact-sql.md)   
 [DROP SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
