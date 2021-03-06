---
title: Abfragen von HDFS-Daten im Speicherpool
titleSuffix: SQL Server big data clusters
description: In diesem Tutorial wird veranschaulicht, wie HDFS-Daten [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]in einer abgefragt werden. Sie erstellen eine externe Tabelle für Daten im Speicherpool und führen dann eine Abfrage aus.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7ba5721ef461fe327a3309431cc994a5ed377be7
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652443"
---
# <a name="tutorial-query-hdfs-in-a-sql-server-big-data-cluster"></a>Tutorial: Abfragen von HDFS in einem Big-Data-Cluster für SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

In diesem Tutorial wird veranschaulicht, wie HDFS-Daten [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]in einer abgefragt werden.

In diesem Tutorial lernen Sie Folgendes:

> [!div class="checklist"]
> * Erstellen einer externen Tabelle, die auf HDFS-Daten in einem Big Data-Cluster zeigt
> * Verknüpfen dieser Daten mit hochwertigen Daten in der Masterinstanz

> [!TIP]
> Wenn Sie möchten, können Sie ein Skript für die Befehle in diesem Tutorial herunterladen und ausführen. Anweisungen finden Sie in den [Beispielen zur Datenvirtualisierung](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization) auf GitHub.

## <a id="prereqs"></a> Erforderliche Komponenten

- [Big-Data-Tools](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Erweiterung von SQL Server 2019**
- [Laden von Beispieldaten in Ihren Big Data-Cluster](tutorial-load-sample-data.md)

## <a name="create-an-external-table-to-hdfs"></a>Erstellen einer externen Tabelle für HDFS

Der Speicherpool enthält Daten zu Webclickstreams in einer in HDFS gespeicherten CSV-Datei. Führen Sie die folgenden Schritte aus, um eine externe Tabelle zu definieren, die auf die Daten in dieser Datei zugreifen kann.

1. Stellen Sie in Azure Data Studio eine Verbindung mit der SQL Server-Masterinstanz Ihres Big Data-Clusters her. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit der SQL Server-Masterinstanz](connect-to-big-data-cluster.md#master).

1. Doppelklicken Sie im Fenster **Server** auf die Verbindung, um das Serverdashboard der SQL Server-Masterinstanz anzuzeigen. Wählen Sie **Neue Abfrage** aus.

   ![Abfrage der SQL Server-Masterinstanz](./media/tutorial-query-hdfs-storage-pool/sql-server-master-instance-query.png)

1. Führen Sie den folgenden Transact-SQL-Befehl aus, um den Kontext in der Masterinstanz in die **Sales**-Datenbank zu ändern.

   ```sql
   USE Sales
   GO
   ```

1. Definieren Sie das Format der CSV-Datei, die aus HDFS gelesen werden soll. Drücken Sie zum Ausführen der Anweisung die Taste F5.

   ```sql
   CREATE EXTERNAL FILE FORMAT csv_file
   WITH (
       FORMAT_TYPE = DELIMITEDTEXT,
       FORMAT_OPTIONS(
           FIELD_TERMINATOR = ',',
           STRING_DELIMITER = '"',
           FIRST_ROW = 2,
           USE_TYPE_DEFAULT = TRUE)
   );
   ```

1. Erstellen Sie eine externe Datenquelle für den Speicherpool, wenn diese nicht bereits vorhanden ist.

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
   BEGIN
     CREATE EXTERNAL DATA SOURCE SqlStoragePool
     WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   END
   ```

1. Erstellen Sie eine externe Tabelle, die `/clickstream_data` aus dem Speicherpool lesen kann. Auf den **SqlStoragePool** kann von der Masterinstanz eines Big Data-Clusters aus zugegriffen werden.

   ```sql
   CREATE EXTERNAL TABLE [web_clickstreams_hdfs]
   ("wcs_click_date_sk" BIGINT , "wcs_click_time_sk" BIGINT , "wcs_sales_sk" BIGINT , "wcs_item_sk" BIGINT , "wcs_web_page_sk" BIGINT , "wcs_user_sk" BIGINT)
   WITH
   (
       DATA_SOURCE = SqlStoragePool,
       LOCATION = '/clickstream_data',
       FILE_FORMAT = csv_file
   );
   GO
   ```

## <a name="query-the-data"></a>Abfragen der Daten

Führen Sie die folgende Abfrage aus, um die HDFS-Daten in der externen Tabelle `web_clickstream_hdfs` mit den relationalen Daten in der lokalen Datenbank `Sales` zu verknüpfen.

```sql
SELECT  
    wcs_user_sk,
    SUM( CASE WHEN i_category = 'Books' THEN 1 ELSE 0 END) AS book_category_clicks,
    SUM( CASE WHEN i_category_id = 1 THEN 1 ELSE 0 END) AS [Home & Kitchen],
    SUM( CASE WHEN i_category_id = 2 THEN 1 ELSE 0 END) AS [Music],
    SUM( CASE WHEN i_category_id = 3 THEN 1 ELSE 0 END) AS [Books],
    SUM( CASE WHEN i_category_id = 4 THEN 1 ELSE 0 END) AS [Clothing & Accessories],
    SUM( CASE WHEN i_category_id = 5 THEN 1 ELSE 0 END) AS [Electronics],
    SUM( CASE WHEN i_category_id = 6 THEN 1 ELSE 0 END) AS [Tools & Home Improvement],
    SUM( CASE WHEN i_category_id = 7 THEN 1 ELSE 0 END) AS [Toys & Games],
    SUM( CASE WHEN i_category_id = 8 THEN 1 ELSE 0 END) AS [Movies & TV],
    SUM( CASE WHEN i_category_id = 9 THEN 1 ELSE 0 END) AS [Sports & Outdoors]
  FROM [dbo].[web_clickstreams_hdfs]
  INNER JOIN item it ON (wcs_item_sk = i_item_sk
                        AND wcs_user_sk IS NOT NULL)
GROUP BY  wcs_user_sk;
GO
```

## <a name="clean-up"></a>Bereinigung

Verwenden Sie den folgenden Befehl, um die in diesem Tutorial erstellte externe Tabelle zu entfernen.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_hdfs];
GO
```

## <a name="next-steps"></a>Nächste Schritte

Fahren Sie mit dem nächsten Artikel fort, um zu lernen, wie Sie Oracle aus einem Big Data-Cluster abfragen.
> [!div class="nextstepaction"]
> [Abfragen externer Daten in Oracle](tutorial-query-oracle.md)
