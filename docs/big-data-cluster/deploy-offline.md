---
title: Offlinebereitstellung
titleSuffix: SQL Server big data clusters
description: Erfahren Sie, wie Sie eine Offlinebereitstellung von Big Data-Clustern für SQL Server durchführen.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 243771141bbd255e045ef0a1667235f1c414777b
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155266"
---
# <a name="perform-an-offline-deployment-of-a-sql-server-big-data-cluster"></a>Durchführen einer Offlinebereitstellung von Big Data-Clustern für SQL Server

In diesem Artikel wird beschrieben, wie Sie eine Offline Bereitstellung einer [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]ausführen. Big Data-Cluster müssen Zugriff auf ein Docker-Repository haben, aus dem Containerimages gepullt werden. Bei einer Offlineinstallation werden die erforderlichen Images in einem privaten Docker-Repository abgelegt. Dieses private Repository wird dann als Imagequelle für eine neue Bereitstellung verwendet.

## <a name="prerequisites"></a>Erforderliche Komponenten

- Docker-Engine 1.8 und höher auf unterstütztem Linux-Betriebssystem oder Docker für Mac bzw. Windows. Weitere Informationen finden Sie unter [Install Docker (Installieren von Docker)](https://docs.docker.com/engine/installation/).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="load-images-into-a-private-repository"></a>Laden von Images in ein privates Repository

In den folgenden Schritten wird beschrieben, wie Sie die Containerimages des Big Data-Clusters aus dem Microsoft-Repository abrufen und anschließend in Ihr privates Repository pushen.

> [!TIP]
> Die folgenden Schritte erläutern den Prozess. Um die Aufgabe zu vereinfachen, können Sie jedoch das [automatisierte Skript](#automated) verwenden, anstatt diese Befehle manuell auszuführen.

1. Pullen Sie die Big Data-Cluster-Containerimages, indem Sie den folgenden Befehl wiederholen. Ersetzen Sie `<SOURCE_IMAGE_NAME>` durch den jeweiligen [Imagenamen](#images). Ersetzen `<SOURCE_DOCKER_TAG>` Sie dies durch das Tag für die Big Data Cluster Version, z. b. **2019-RC1-Ubuntu**.  

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG>
   ```

1. Melden Sie sich bei der privaten Docker-Zielregistrierung an.

   ```PowerShell
   docker login <TARGET_DOCKER_REGISTRY> -u <TARGET_DOCKER_USERNAME> -p <TARGET_DOCKER_PASSWORD>
   ```

1. Markieren Sie die lokalen Images jeweils mit dem folgenden Befehl:

   ```PowerShell
   docker tag mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG> <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

1. Pushen Sie die lokalen Images in das private Docker-Repository:

   ```PowerShell
   docker push <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

### <a id="images"></a> Big Data-Cluster-Containerimages

Die folgenden Big Data-Cluster-Containerimages sind für eine Offlineinstallation erforderlich:
- **mssql-app-service-proxy**
- **MSSQL-Control-Watchdog**
- **mssql-controller**
- **MSSQL-DNS**
- **mssql-hadoop**
- **mssql-mleap-serving-runtime**
- **mssql-mlserver-py-runtime**
- **mssql-mlserver-r-runtime**
- **mssql-monitor-collectd**
- **mssql-monitor-elasticsearch**
- **mssql-monitor-fluentbit**
- **mssql-monitor-grafana**
- **mssql-monitor-influxdb**
- **mssql-monitor-kibana**
- **mssql-monitor-telegraf**
- **MSSQL-Security-domainctl**
- **mssql-security-knox**
- **mssql-security-support**
- **mssql-server**
- **mssql-server-controller**
- **mssql-server-data**
- **MSSQL-Server-ha**
- **mssql-service-proxy**
- **mssql-ssis-app-runtime**


## <a id="automated"></a> Automatisiertes Skript

Sie können ein automatisiertes Python-Skript verwenden, das automatisch alle benötigten Containerimages pullt und sie in ein privates Repository überträgt.

> [!NOTE]
> Python ist eine Voraussetzung für die Verwendung des Skripts. Weitere Informationen über die Installation von Python finden Sie in der [Python-Dokumentation](https://wiki.python.org/moin/BeginnersGuide/Download).

1. Laden Sie das Skript per Bash oder PowerShell mit **curl** herunter:

   ```PowerShell
   curl -o push-bdc-images-to-custom-private-repo.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/offline/push-bdc-images-to-custom-private-repo.py"
   ```

1. Führen Sie das Skript mit einem der folgenden Befehle aus:

   **Windows:**

   ```PowerShell
   python deploy-sql-big-data-aks.py
   ```

   **Linux:**

   ```bash
   sudo python deploy-sql-big-data-aks.py
   ```

1. Befolgen Sie die Anweisungen zum Eingeben des Microsoft-Repositorys und Ihrer privaten Repository-Informationen. Nach Abschluss des Skripts sollten sich alle erforderlichen Images in Ihrem privaten Repository befinden.

## <a name="install-tools-offline"></a>Offlineinstallation von Tools

Big Data-Cluster Bereitstellungen erfordern mehrere Tools, einschließlich **python**, `azdata`und **kubectl**. Führen Sie die folgenden Schritte aus, um diese Tools auf einem Offlineserver zu installieren.

### <a id="python"></a> Offlineinstallation von Python

1. Laden Sie auf einem Computer mit Internetzugriff eine der folgenden komprimierten Dateien herunter, die Python enthalten:

   | Betriebssystem | Herunterladen |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. Kopieren Sie die komprimierte Datei auf den Zielcomputer, und extrahieren Sie sie in einen Ordner Ihrer Wahl.

1. Führen Sie `installLocalPythonPackages.bat` nur unter Windows in diesem Ordner aus, und übergeben Sie den vollständigen Pfad zu demselben Ordner als Parameter.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

### <a id="azdata"></a> Offlineinstallation von azdata

1. Führen Sie auf einem Computer mit Internet Zugriff und [python](https://wiki.python.org/moin/BeginnersGuide/Download)den folgenden Befehl aus, um alle `azdata` Pakete aus dem aktuellen Ordner herunterzuladen.

   ```PowerShell
   pip download -r https://aka.ms/azdata
   ```

1. Kopieren Sie die heruntergeladenen Pakete `requirements.txt` und die Datei auf den Zielcomputer.

1. Führen Sie den folgenden Befehl auf dem Zielcomputer aus, und geben Sie dabei den Ordner an, in den Sie die vorherigen Dateien kopiert haben.

   ```PowerShell
   pip install --no-index --find-links <path-to-packages> -r <path-to-requirements.txt>
   ```

### <a id="kubectl"></a> Offlineinstallation von kubectl

Führen Sie die folgenden Schritte aus, um **kubectl** auf einem Offlinecomputer zu installieren.

1. Verwenden Sie **curl**, um **kubectl** in einen Ordner Ihrer Wahl herunterzuladen. Weitere Informationen finden Sie unter [Install kubectl binary using curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl) (Installieren von kubectl mit curl).

1. Kopieren Sie den Ordner auf den Zielcomputer.

## <a name="deploy-from-private-repository"></a>Bereitstellen aus privatem Repository

Verwenden Sie zum Bereitstellen über das private Repository die im [Bereitstellungshandbuch](deployment-guidance.md) beschriebenen Schritte, und verwenden Sie unbedingt eine benutzerdefinierte Bereitstellungskonfigurationsdatei, die die Informationen zu Ihrem privaten Docker-Repository enthält. Die folgenden `azdata` Befehle veranschaulichen, wie die Docker-Einstellungen in einer benutzerdefinierten Bereitstellungs Konfigurationsdatei namens `control.json`geändert werden:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.repository=<your-docker-repository>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.registry=<your-docker-registry>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.imageTag=<your-docker-image-tag>"
```

In der Bereitstellung werden Sie aufgefordert, den docker-Benutzernamen und das Kennwort einzugeben `DOCKER_USERNAME` , `DOCKER_PASSWORD` oder Sie können Sie in den Umgebungsvariablen und angeben.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Big Data Cluster Bereitstellungen finden [Sie [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] unter Bereitstellen von auf Kubernetes](deployment-guidance.md).
