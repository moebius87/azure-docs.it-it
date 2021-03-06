---
title: Ridimensionare l'elaborazione di contenuti mediante il portale di Azure | Microsoft Docs
description: Questa esercitazione descrive i passaggi per ridimensionare l'elaborazione multimediale mediante il portale di Azure.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/19/2019
ms.author: juliako
ms.openlocfilehash: c840764dc978a8dacb3450c0aca5e5d93284b8a6
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "61127542"
---
# <a name="change-the-reserved-unit-type"></a>Modificare il tipo di unità riservata
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portale](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Panoramica

Un account di Servizi multimediali è associato a un tipo di unità riservata che determina la velocità dei processi di elaborazione dei multimedia. È possibile scegliere uno dei seguenti tipi di unità riservata: **S1**, **S2** o **S3**. Lo stesso processo di codifica viene eseguito più velocemente quando si usa ad esempio il tipo di unità riservata **S2** rispetto al tipo **S1**.

Oltre al tipo di unità riservata, è possibile specificare il provisioning dell'account con **Unità riservate** (UR). Il numero delle UR sottoposte a provisioning determina il numero di attività multimediali che possono essere elaborate contemporaneamente in un determinato account.

>[!NOTE]
>UR di lavoro per la parallelizzazione di tutta l'elaborazione di supporti di memorizzazione, tra cui l'indicizzazione di processi tramite Azure Media Indexer. Tuttavia, a differenza della codifica, l'indicizzazione di processi non viene elaborata più velocemente con unità riservate più veloci.

> [!IMPORTANT]
> Per altre informazioni sul ridimensionamento dell'elaborazione multimediale, vedere questo argomento di [panoramica](media-services-scale-media-processing-overview.md) .
> 
> 

## <a name="scale-media-processing"></a>Ridimensionare l'elaborazione di contenuti multimediali
Per modificare il tipo di unità riservata e il numero di unità riservate, effettuare le operazioni seguenti:

1. Nel [portale di Azure ](https://portal.azure.com/) selezionare l'account Servizi multimediali di Azure.
2. Nella finestra **Impostazioni** selezionare **Media Reserved Unit**.
   
    Per cambiare il numero di unità riservate per il tipo selezionato, usare il dispositivo di scorrimento **Unità riservate multimediali** nella parte superiore della schermata.
   
    Per cambiare il valore di **TIPO DI UNITÀ RISERVATA**, fare clic sulla barra **Velocità delle unità di elaborazione riservate**. Selezionare quindi il piano tariffario desiderato: S1, S2 o S3.
   
3. Fare clic sul pulsante SAVE per salvare le modifiche apportate.
   
    Le nuove unità riservate vengono allocate quando si fa clic su SALVA.

## <a name="next-steps"></a>Passaggi successivi
Analizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

