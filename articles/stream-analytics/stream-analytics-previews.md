---
title: Funzionalità in anteprima di Analisi di flusso di Azure
description: Questo articolo elenca le funzionalità di Analisi di flusso di Azure attualmente in anteprima.
services: stream-analytics
author: mamccrea
ms.author: mamccrea
ms.reviewer: jasonh
ms.service: stream-analytics
ms.topic: conceptual
ms.date: 02/05/2019
ms.openlocfilehash: 08430f3eee858cdb6c9a7fbdfe11bd4c00ef148d
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "61485676"
---
# <a name="azure-stream-analytics-preview-features"></a>Funzionalità in anteprima di Analisi di flusso di Azure

Questo articolo riepiloga tutte le funzionalità attualmente in anteprima per Analisi di flusso di Azure. Non è consigliabile usare le funzionalità in anteprima in un ambiente di produzione.

## <a name="public-previews"></a>Anteprime pubbliche

Nell'anteprima pubblica sono disponibili le funzionalità seguenti. È possibile sfruttare queste funzionalità adesso, ma non usarle nell'ambiente di produzione.

### <a name="anomaly-detection"></a>Anomaly Detection

In Analisi di flusso di Azure sono stati introdotti nuovi modelli di apprendimento automatico con il supporto per il rilevamento di *picchi* e *flessioni*, oltre che per il rilevamento di tendenze bidirezionali, positive lente e negative lente. Per altre informazioni, visitare [rilevamento di anomalie in Azure Stream Analitica](stream-analytics-machine-learning-anomaly-detection.md).

### <a name="sql-database-reference-data"></a>Dati di riferimento del database SQL

Analisi di flusso di Azure supporta il database SQL di Azure come origine di input per i dati di riferimento. È possibile usare i dati contenuti in un database SQL come dati di riferimento per un processo di Analisi di flusso nel portale di Azure e in Visual Studio con gli strumenti di Analisi di flusso. Per altre informazioni, vedere [Usare dati di riferimento da un database SQL per un processo di Analisi di flusso di Azure](sql-reference-data.md).

### <a name="integration-with-azure-machine-learning"></a>Integrazione con Azure Machine Learning

È possibile per ridimensionare i processi di Analisi di flusso con funzioni di Machine Learning (ML). Per altre informazioni su come è possibile usare le funzioni ML nel processo di Analisi di flusso, vedere [Ridimensionare il processo di Analisi di flusso con funzioni di Azure Machine Learning](stream-analytics-scale-with-machine-learning-functions.md). Per uno scenario reale, vedere [Analisi del sentiment con Analisi di flusso di Azure e Azure Machine Learning](stream-analytics-machine-learning-integration-tutorial.md).

### <a name="javascript-user-defined-aggregate"></a>Aggregazione JavaScript definita dall'utente

Analisi di flusso di Azure supporta le aggregazioni definite dall'utente scritte in JavaScript, che consentono di implementare la logica di business con stato complessa. Per informazioni su come usare le aggregazioni definite dall'utente, vedere il documento [Aggregazioni JavaScript definite dall'utente in Analisi di flusso di Azure](stream-analytics-javascript-user-defined-aggregates.md). 

### <a name="live-data-testing-in-visual-studio"></a>Test dei dati live in Visual Studio

Gli strumenti di Visual Studio per Analisi di flusso di Azure migliorano la funzionalità di test locale che consente di testare le query nei flussi di eventi live da origini cloud come l'hub eventi o l'hub IoT. Per informazioni, vedere [Testare i dati live in locale usando gli strumenti di Analisi di flusso di Azure per Visual Studio](stream-analytics-live-data-local-testing.md).

### <a name="net-user-defined-functions-on-iot-edge"></a>Funzioni .NET definite dall'utente in IoT Edge

Con le funzioni .NET Standard definite dall'utente, è possibile eseguire il codice .NET Standard come parte della pipeline di streaming. È possibile creare semplici classi C# o importare librerie e progetti completi. In Visual Studio è supportata l'esperienza completa di creazione e debug. Per altre informazioni, vedere [Sviluppare funzioni .NET Standard definite dall'utente per i processi di Analisi di flusso di Azure in IoT Edge](stream-analytics-edge-csharp-udf-methods.md).

## <a name="private-previews"></a>Anteprime private

Nell'anteprima privata sono disponibili le funzionalità seguenti.

### <a name="c-custom-deserializer-for-azure-stream-analytics-on-iot-edge"></a>Deserializzatore personalizzato C# per Analisi di flusso di Azure in IoT Edge

Gli sviluppatori possono ora implementare deserializzatori personalizzati in C# per deserializzare gli eventi ricevuti da Analisi di flusso di Azure. Gli esempi di formati che possono essere deserializzati includono Parquet, Protobuf, XML o qualsiasi altro formato binario.

### <a name="visual-studio-code-for-azure-stream-analytics"></a>Visual Studio Code per Analisi di flusso di Azure

I processi di Analisi di flusso di Azure possono essere creati in Visual Studio Code. Per accedere a strumenti dell'anteprima privata delle funzionalità, contattare *ASAToolsfeedback\@microsoft.com*.

## <a name="next-steps"></a>Passaggi successivi

* [Eight new features in Azure Stream Analytics (Otto nuove funzionalità in Analisi di flusso di Azure)](https://azure.microsoft.com/blog/eight-new-features-in-azure-stream-analytics/)

* [Four new features now available in Azure Stream Analytics (Quattro nuove funzionalità disponibili in Analisi di flusso di Azure)](https://azure.microsoft.com/blog/4-new-features-now-available-in-azure-stream-analytics/)
