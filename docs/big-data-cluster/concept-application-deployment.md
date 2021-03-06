---
title: Was ist Anwendungsbereitstellung?
titleSuffix: Big Data Clusters for SQL Server 2019
description: In diesem Artikel wird die Anwendungs Bereitstellung in einem Big Data-Cluster für SQL Server 2019 beschrieben.
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: da497f8d7c435a807ba530ae619ff91a6f2dff71
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653007"
---
# <a name="what-is-application-deployment-on-a-sql-server-2019-big-data-cluster"></a>Was ist Anwendungsbereitstellung auf einem Big Data-Cluster für SQL Server 2019?

Die Anwendungsbereitstellung ermöglicht die Bereitstellung von Anwendungen auf dem Big Data-Cluster durch die Bereitstellung von Schnittstellen zum Erstellen, Verwalten und Ausführen von Anwendungen. Anwendungen, die auf dem Big Data-Cluster bereitgestellt werden, profitieren von der Rechenleistung des Clusters und können auf die Daten zugreifen, die auf dem Cluster verfügbar sind. Dadurch wird die Skalierbarkeit und Leistung der Anwendungen erhöht, während die Anwendungen, in denen sich die Daten befinden, verwaltet werden.
In den folgenden Abschnitten werden die Architektur und die Funktionalität der Anwendungsbereitstellung beschrieben.

## <a name="application-deployment-architecture"></a>Architektur der Anwendungsbereitstellung

Die Anwendungsbereitstellung besteht aus einem Controller und App-Runtime-Handlern. Beim Erstellen einer Anwendung wird eine Spezifikationsdatei (`spec.yaml`) bereitgestellt. Diese `spec.yaml`-Datei enthält alles, was der Controller wissen muss, um die Anwendung erfolgreich bereitzustellen. Im Folgenden finden Sie ein Beispiel für den Inhalt für `spec.yaml`:

```yaml
#spec.yaml
name: add-app #name of your python script
version: v1  #version of the app
runtime: Python #the language this app uses (R or Python)
src: ./add.py #full path to the location of the app
entrypoint: add #the function that will be called upon execution
replicas: 1  #number of replicas needed
poolsize: 1  #the pool size that you need your app to scale
inputs:  #input parameters that the app expects and the type
  x: int
  y: int
output: #output parameter the app expects and the type
  result: int
```

Der Controller überprüft die `runtime`, die in der `spec.yaml`-Datei angegeben ist, und ruft den entsprechenden Runtimehandler auf. Der Runtimehandler erstellt die Anwendung. Zuerst wird ein Kubernetes-ReplicaSet erstellt, das einen oder mehrere Pods enthält, von denen jeder die bereitzustellende Anwendung enthält. Die Anzahl von Pods wird durch den `replicas`-Parametersatz definiert, der in der `spec.yaml`-Datei für die Anwendung festgelegt ist. Jeder Pod kann über einen von mehreren Pools verfügen. Die Anzahl von Pools wird durch den `poolsize`-Parametersatz definiert, der in der `spec.yaml`-Datei festgelegt ist.

Diese Einstellungen wirken sich auf die Anzahl der Anforderungen aus, die die Bereitstellung parallel verarbeiten kann. Die maximale Anzahl von Anforderungen zu einem bestimmten Zeitpunkt entspricht dem Produkt aus `replicas` und `poolsize`. Wenn Sie über 5 Replikate und 2 Pools pro Replikat verfügen, kann die Bereitstellung 10 Anforderungen parallel verarbeiten. Das folgende Bild zeigt eine grafische Darstellung von `replicas` und `poolsize`:

![Poolgröße und Replikate](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

Nachdem das ReplicaSet erstellt und die Pods gestartet wurden, wird ein Cron-Auftrag erstellt, wenn ein `schedule` in der `spec.yaml`-Datei festgelegt wurde. Zum Schluss wird ein Kubernetes-Dienst erstellt, der zum Verwalten und Ausführen der Anwendung verwendet werden kann (siehe unten).

Wenn eine Anwendung ausgeführt wird, leitet der Kubernetes-Dienst für die Anwendung die Anforderungen an ein Replikat weiter und gibt die Ergebnisse zurück.

## <a name="how-to-work-with-application-deployment"></a>Vorgehensweise: Arbeiten mit der Anwendungsbereitstellung

Die zwei Hauptschnittstellen für die Anwendungsbereitstellung lauten wie folgt: 
- [Befehlszeilenschnittstelle`azdata`](big-data-cluster-create-apps.md)
- [Visual Studio Code und Erweiterung Azure Data Studio](app-deployment-extension.md)

Es ist auch möglich, dass eine Anwendung mit einem RESTful-Webdienst ausgeführt wird. Weitere Informationen finden Sie unter [Nutzen von Anwendungen auf Big Data-Clustern](big-data-cluster-consume-apps.md).

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zum Erstellen und Ausführen von Anwendungen unter [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]finden Sie in den folgenden Bereichen:

- [Bereitstellen von Anwendungen mit „azdata“](big-data-cluster-create-apps.md)
- [Vorgehensweise: Verwenden von Visual Studio Code zum Bereitstellen von Anwendungen für SQL Server-Big Data-Cluster](app-deployment-extension.md)
- [Verwenden von Anwendungen auf Big Data-Clustern](big-data-cluster-consume-apps.md)

Weitere Informationen [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]zum finden Sie in der folgenden Übersicht:

- [Was sind [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
