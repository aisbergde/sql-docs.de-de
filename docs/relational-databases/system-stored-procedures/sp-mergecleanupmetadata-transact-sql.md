---
title: sp_mergecleanupmetadata (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergecleanupmetadata_TSQL
- sp_mergecleanupmetadata
helpviewer_keywords:
- sp_mergecleanupmetadata
ms.assetid: 892f8628-4cbe-4cc3-b959-ed45ffc24064
author: stevestein
ms.author: sstein
ms.openlocfilehash: a62445553364fc7756444986a5bd8cf57d576ecd
ms.sourcegitcommit: a1ddeabe94cd9555f3afdc210aec5728f0315b14
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2019
ms.locfileid: "70123097"
---
# <a name="sp_mergecleanupmetadata-transact-sql"></a>sp_mergecleanupmetadata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Sollte nur in Replikationstopologien verwendet werden, die Server enthalten [!INCLUDE[msCoName](../../includes/msconame-md.md)] , auf [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] denen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vor Service Pack 1 ausgeführt werden. **sp_mergecleanupmetadata** ermöglicht Administratoren das Bereinigen von Metadaten in den Systemtabellen **MSmerge_genhistory**, **MSmerge_contents** und **MSmerge_tombstone** . Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungs Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_mergecleanupmetadata [ [ @publication = ] 'publication' ]  
    [ , [ @reinitialize_subscriber = ] 'reinitialize_subscriber' ]  
```  
  
## <a name="arguments"></a>Argumente  
`[ @publication = ] 'publication'`Der Name der Veröffentlichung. *Publication* ist vom **%** **Datentyp vom Datentyp sysname**und hat den Standardwert, mit dem Metadaten für alle Veröffentlichungen bereinigt werden. Die Veröffentlichung muss bereits vorhanden sein, wenn sie explizit angegeben wird.  
  
`[ @reinitialize_subscriber = ] 'subscriber'`Gibt an, ob der Abonnent erneut initialisiert werden soll. der *Abonnent* ist vom Datentyp **nvarchar (5)** . der Wert kann **true** oder **false**sein. der Standardwert ist **true**. **True**gibt an, dass Abonnements für die erneute Initialisierung markiert werden. Wenn der Wert **false**ist, werden die Abonnements nicht für die erneute Initialisierung gekennzeichnet.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **sp_mergecleanupmetadata** sollte nur in Replikationstopologien verwendet werden, die Server enthalten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , auf [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] denen Versionen von vor Service Pack 1 ausgeführt werden. Topologien mit ausschließlich [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1 oder höher sollten eine auf Metadatencleanup basierende automatische Beibehaltung verwenden. Beim Ausführen dieser gespeicherten Prozedur müssen Sie beachten, dass die Protokolldatei auf dem Computer, auf dem die gespeicherte Prozedur ausgeführt wird, stark anwachsen kann.  
  
> [!CAUTION]
>  Nach dem Ausführen von **sp_mergecleanupmetadata** werden standardmäßig alle Abonnements auf den Abonnenten von Veröffentlichungen, die in **MSmerge_genhistory**, **MSmerge_contents** und **MSmerge_tombstone** gespeicherte Metadaten enthalten, als markiert. die erneute Initialisierung, alle ausstehenden Änderungen auf dem Abonnenten gehen verloren, und die aktuelle Momentaufnahme ist als veraltet markiert.  
> 
> [!NOTE]
>  Wenn mehrere Veröffentlichungen in einer Datenbank vorhanden sind und eine dieser Veröffentlichungen eine unbegrenzte Beibehaltungs Dauer für=die Veröffentlichung verwendet ( **\@Beibehaltung** **0**), wird durch das Ausführen von **sp_mergecleanupmetadata** nicht bereinigt. Änderungs nach Verfolgungs Metadaten für die Mergereplikation für die Datenbank. Aus diesem Grund sollten Sie die unbegrenzte Aufbewahrungsdauer für Veröffentlichungen mit Vorsicht verwenden.  
  
 Wenn Sie diese gespeicherte Prozedur ausführen, können Sie auswählen, ob Abonnenten erneut initialisiert werden sollen, indem Sie den  **\@reinitialize_subscriber** -Parameter auf **true** (Standardeinstellung) oder **false**festlegen. Wenn **sp_mergecleanupmetadata** ausgeführt wird und der  **\@reinitialize_subscriber** -Parameter auf **true**festgelegt ist, wird eine Momentaufnahme auf dem Abonnenten erneut angewendet, auch wenn das Abonnement ohne eine Anfangs Momentaufnahme erstellt wurde (für Beispiel: Wenn die Momentaufnahme Daten und das Schema manuell angewendet wurden oder bereits auf dem Abonnenten vorhanden waren). Das Festlegen des Parameters auf **false** sollte mit Bedacht verwendet werden, denn wenn die Veröffentlichung nicht erneut initialisiert wird, müssen Sie sicherstellen, dass die Daten auf dem Verleger und dem Abonnenten synchronisiert werden.  
  
 Unabhängig vom Wert von  **\@reinitialize_subscriber**schlägt **sp_mergecleanupmetadata** fehl, wenn laufende Mergeprozesse vorhanden sind, die versuchen, Änderungen auf einen Verleger oder einen wieder Veröffentlichungs Abonnenten zu dem Zeitpunkt hochzuladen, an dem die gespeicherte die Prozedur wird aufgerufen.  
  
 **Ausführen von sp_mergecleanupmetadata \@mit reinitialize_subscriber = true:**  
  
1.  Es ist nicht vorgeschrieben, wird jedoch empfohlen, alle Updates der Veröffentlichungs- und Abonnementdatenbanken zu beenden. Falls Updates fortgesetzt werden, gehen alle seit der letzten Zusammenführung beim Abonnenten vorgenommenen Updates beim erneuten Initialisieren der Veröffentlichung verloren. Die Datenkonvergenz bleibt jedoch erhalten.  
  
2.  Ausführen eines Mergeprozesses durch Ausführen des Merge-Agents. Es wird empfohlen, die Befehlszeilenoption **-Validate** Agent bei jedem Abonnenten zu verwenden, wenn Sie die Merge-Agent ausführen. Wenn Sie fortlaufende Modus-Zusammenführungen ausführen, finden Sie weitere Informationen im Abschnitt *Überlegungen zum fortlaufenden Modus* weiter unten in diesem Abschnitt.  
  
3.  Nachdem alle Zusammenführungen abgeschlossen wurden, führen Sie **sp_mergecleanupmetadata**aus.  
  
4.  Führen Sie **sp_reinitmergepullsubscription** auf allen Abonnenten aus, die das benannte oder anonyme Pullabonnement verwenden, um Daten Konvergenz  
  
5.  Wenn Sie fortlaufende Modus-Zusammenführungen ausführen, finden Sie weitere Informationen im Abschnitt *Überlegungen zum fortlaufenden Modus* weiter unten in diesem Abschnitt.  
  
6.  Generieren Sie Snaphotdateien für alle beteiligten Mergeveröffentlichungen auf allen Ebenen erneut. Wenn Sie das Zusammenführen versuchen, ohne die Momentaufnahme zuvor erneut zu generieren, wird eine Eingabeaufforderung angezeigt, die Sie dazu auffordert, die Momentaufnahme erneut zu generieren.  
  
7.  Sichern Sie die Veröffentlichungsdatenbank. Wenn dies versäumt wird, kann es zu einem Mergefehler führen, nachdem die Veröffentlichungsdatenbank wiederhergestellt wurde.  
  
 **Ausführen von sp_mergecleanupmetadata \@mit reinitialize_subscriber = FALSE:**  
  
1.  Beendet **alle** Updates der Veröffentlichungs-und Abonnement Datenbanken.  
  
2.  Ausführen eines Mergeprozesses durch Ausführen des Merge-Agents. Es wird empfohlen, die Befehlszeilenoption **-Validate** Agent bei jedem Abonnenten zu verwenden, wenn Sie die Merge-Agent ausführen. Wenn Sie fortlaufende Modus-Zusammenführungen ausführen, finden Sie weitere Informationen im Abschnitt *Überlegungen zum fortlaufenden Modus* weiter unten in diesem Abschnitt.  
  
3.  Nachdem alle Zusammenführungen abgeschlossen wurden, führen Sie **sp_mergecleanupmetadata**aus.  
  
4.  Wenn Sie fortlaufende Modus-Zusammenführungen ausführen, finden Sie weitere Informationen im Abschnitt *Überlegungen zum fortlaufenden Modus* weiter unten in diesem Abschnitt.  
  
5.  Generieren Sie Snaphotdateien für alle beteiligten Mergeveröffentlichungen auf allen Ebenen erneut. Wenn Sie das Zusammenführen versuchen, ohne die Momentaufnahme zuvor erneut zu generieren, wird eine Eingabeaufforderung angezeigt, die Sie dazu auffordert, die Momentaufnahme erneut zu generieren.  
  
6.  Sichern Sie die Veröffentlichungsdatenbank. Wenn dies versäumt wird, kann es zu einem Mergefehler führen, nachdem die Veröffentlichungsdatenbank wiederhergestellt wurde.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 **Besondere Überlegungen zu Zusammenführungen im kontinuierlichen Modus**  
  
 Wenn Sie Mergeprozesse im fortlaufenden Modus ausführen, müssen Sie einen der folgenden Schritte ausführen:  
  
-   Beendet den Merge-Agent und führt dann einen weiteren Merge aus, ohne dass der **-Continuous-** Parameter angegeben wird.  
  
-   Deaktivieren Sie die Veröffentlichung mit **sp_changemergepublication** , um sicherzustellen, dass alle Zusammenführungen im fortlaufenden Modus, die den Veröffentlichungsstatus abrufen, fehlschlagen.  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'inactive'  
    ```  
  
 Wenn Sie Schritt 3 unter Ausführen von **sp_mergecleanupmetadata**abgeschlossen haben, können Sie fortlaufende Modus-Zusammenführungen basierend auf ihrer Beendigung fortsetzen. Führen Sie einen der folgenden Schritte aus:  
  
-   Fügen Sie den **-Continuous-** Parameter für die Merge-Agent zurück.  
  
-   Reaktivieren Sie die Veröffentlichung mit **sp_changemergepublication.**  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'active'  
    ```  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Server Rolle **sysadmin** oder der festen Daten Bank Rolle **db_owner** können **sp_mergecleanupmetadata**ausführen.  
  
 Zum Verwenden dieser gespeicherten Prozedur muss der Verleger [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ausführen. Auf den Abonnenten muss entweder [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7,0, Service Pack 2 ausgeführt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [MSmerge_genhistory &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)   
 [MSmerge_contents &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)   
 [MSmerge_tombstone &#40;(Transact-SQL)&#41;](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)  
  
  
