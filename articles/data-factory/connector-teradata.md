---
title: Copiare dati da Teradata usando Azure Data Factory | Microsoft Docs
description: Informazioni sul connettore Teradata del servizio Data Factory, che consente di copiare dati da un database Teradata in archivi dati supportati da Data Factory come sink.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: conceptual
ms.date: 02/07/2018
ms.author: jingwang
ms.openlocfilehash: e9fd818990c8a985a77c2e7eeea19bf63c440e4e
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "61347752"
---
# <a name="copy-data-from-teradata-using-azure-data-factory"></a>Copiare dati da Teradata usando Azure Data Factory
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Versione 1](v1/data-factory-onprem-teradata-connector.md)
> * [Versione corrente](connector-teradata.md)

Questo articolo illustra come usare l'attività di copia in Azure Data Factory per copiare dati da un database Teradata. Si basa sull'articolo di [panoramica dell'attività di copia](copy-activity-overview.md) che presenta una panoramica generale sull'attività di copia.

## <a name="supported-capabilities"></a>Funzionalità supportate

È possibile copiare dati da un database Teradata in qualsiasi archivio dati di sink supportato. Per un elenco degli archivi dati supportati come origini/sink dall'attività di copia, vedere la tabella relativa agli [archivi dati supportati](copy-activity-overview.md#supported-data-stores-and-formats).

In particolare, il connettore Teradata supporta:

- Teradata **versione 12 e successive**.
- La copia di dati usando l'autenticazione **Di base** o **Windows**.

## <a name="prerequisites"></a>Prerequisiti

Per usare questo connettore Teradata, è necessario:

- Configurare un runtime di integrazione self-hosted. Per i dettagli, vedere l'articolo [Runtime di integrazione self-hosted](create-self-hosted-integration-runtime.md).
- Installare il [provider di dati .NET per Teradata](https://go.microsoft.com/fwlink/?LinkId=278886) versione 14 o successiva nel computer del runtime di integrazione.

## <a name="getting-started"></a>Introduzione

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

Le sezioni seguenti riportano informazioni dettagliate sulle proprietà che vengono usate per definire entità di Data Factory specifiche per il connettore Teradata.

## <a name="linked-service-properties"></a>Proprietà del servizio collegato

Per il servizio collegato di Teradata sono supportate le proprietà seguenti:

| Proprietà | Descrizione | Obbligatoria |
|:--- |:--- |:--- |
| type | La proprietà type deve essere impostata su: **Teradata** | Sì |
| server | Nome del server Teradata. | Sì |
| authenticationType | Tipo di autenticazione usato per connettersi al database Teradata.<br/>I valori consentiti sono i seguenti: **Basic** e **Windows**. | Sì |
| username | Specificare il nome utente per la connessione al database Teradata. | Sì |
| password | Specificare la password per l'account utente specificato per il nome utente. Contrassegnare questo campo come SecureString per archiviarlo in modo sicuro in Azure Data Factory oppure [fare riferimento a un segreto archiviato in Azure Key Vault](store-credentials-in-key-vault.md). | Sì |
| connectVia | Il [runtime di integrazione](concepts-integration-runtime.md) da usare per la connessione all'archivio dati. È necessario un runtime di integrazione self-hosted come indicato in [Prerequisiti](#prerequisites). |Sì |

**Esempio:**

```json
{
    "name": "TeradataLinkedService",
    "properties": {
        "type": "Teradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "Basic",
            "username": "<username>",
            "password": {
                "type": "SecureString",
                "value": "<password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a>Proprietà del set di dati

Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sui set di dati. Questa sezione presenta un elenco delle proprietà supportate dal set di dati Teradata.

Per copiare dati da Teradata, impostare la proprietà type del set di dati su **RelationalTable**. Sono supportate le proprietà seguenti:

| Proprietà | Descrizione | Obbligatoria |
|:--- |:--- |:--- |
| type | La proprietà type del set di dati deve essere impostata su: **RelationalTable** | Sì |
| tableName | Nome della tabella nel database Teradata. | No (se nell'origine dell'attività è specificato "query") |

**Esempio:**

```json
{
    "name": "TeradataDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": {
            "referenceName": "<Teradata linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {}
    }
}
```

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia

Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, vedere l'articolo sulle [pipeline](concepts-pipelines-activities.md). Questa sezione presenta un elenco delle proprietà supportate dall'origine Teradata.

### <a name="teradata-as-source"></a>Teradata come origine

Per copiare dati da Teradata, impostare il tipo di origine nell'attività di copia su **RelationalSource**. Nella sezione **origine** dell'attività di copia sono supportate le proprietà seguenti:

| Proprietà | Descrizione | Obbligatoria |
|:--- |:--- |:--- |
| type | La proprietà type dell'origine di attività di copia deve essere impostata su: **RelationalSource** | Sì |
| query | Usare la query SQL personalizzata per leggere i dati. Ad esempio: `"SELECT * FROM MyTable"`. | No (se nel set di dati è specificato "tableName") |

**Esempio:**

```json
"activities":[
    {
        "name": "CopyFromTeradata",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Teradata input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "RelationalSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="data-type-mapping-for-teradata"></a>Mapping dei tipi di dati per Teradata

Quando si copiano dati da Teradata, vengono usati i mapping seguenti tra i tipi di dati di Teradata e i tipi di dati provvisori di Azure Data Factory. Vedere [Mapping dello schema e del tipo di dati](copy-activity-schema-and-type-mapping.md) per informazioni su come l'attività di copia esegue il mapping dello schema di origine e del tipo di dati al sink.

| Tipo di dati di Teradata | Tipo di dati provvisori di Data Factory |
|:--- |:--- |
| BigInt |Int64 |
| BLOB |Byte[] |
| Byte |Byte[] |
| ByteInt |Int16 |
| Char |string |
| Clob |string |
| Data |DateTime |
| Decimal |Decimal |
| Double |Double |
| Graphic |string |
| Integer |Int32 |
| Interval Day |TimeSpan |
| Interval Day To Hour |TimeSpan |
| Interval Day To Minute |TimeSpan |
| Interval Day To Second |TimeSpan |
| Interval Hour |TimeSpan |
| Interval Hour To Minute |TimeSpan |
| Intervallo - da ora a secondo |TimeSpan |
| Interval Minute |TimeSpan |
| Interval Minute To Second |TimeSpan |
| Interval Month |string |
| Interval Second |TimeSpan |
| Interval Year |string |
| Interval Year To Month |string |
| Number |Double |
| Period(Date) |string |
| Period(Time) |string |
| Period(Time With Time Zone) |string |
| Period(Timestamp) |string |
| Period(Timestamp With Time Zone) |string |
| SmallInt |Int16 |
| Tempo |TimeSpan |
| Time With Time Zone |string |
| Timestamp |DateTime |
| Timestamp With Time Zone |DateTimeOffset |
| VarByte |Byte[] |
| VarChar |string |
| VarGraphic |string |
| Xml |string |


## <a name="next-steps"></a>Passaggi successivi
Per un elenco degli archivi dati supportati come origini o sink dall'attività di copia in Azure Data Factory, vedere gli [archivi dati supportati](copy-activity-overview.md#supported-data-stores-and-formats).
