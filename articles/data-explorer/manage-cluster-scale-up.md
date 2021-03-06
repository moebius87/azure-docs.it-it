---
title: Aumentare le prestazioni di un cluster di Esplora dati di Azure per soddisfare la richiesta di modifica
description: Questo articolo descrive i passaggi per aumentare le prestazioni e ridurre un cluster di Esplora dati di Azure basato su richiesta di modifica.
author: radennis
ms.author: radennis
ms.reviewer: orspodek
ms.service: data-explorer
ms.topic: conceptual
ms.date: 04/05/2019
ms.openlocfilehash: 1f130f79b6b6924559e1693e1eef8ced2972b3d5
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60758692"
---
# <a name="manage-cluster-scale-up-to-accommodate-changing-demand"></a>Gestire l'aumento delle prestazioni di un cluster per rispondere al cambiamento della domanda

Esistono due flussi di lavoro per il ridimensionamento di un cluster di Esplora dati di Azure: scalabilità verticale e [scalabilità orizzontale](manage-cluster-scale-out.md). Questo articolo illustra come gestire cluster scalabilità verticale.

Ridimensionare un cluster in modo appropriato è fondamentale per garantire le prestazioni di Esplora dati di Azure. Ma la domanda in un cluster non è possibile prevedere con accuratezza assoluto. Una dimensione del cluster statico può causare sottoutilizzo o di Sovrautilizzo, nessuno dei quali è ideale. Un approccio migliore consiste *scalabilità* un cluster, aggiungendo e rimuovendo la capacità e risorse della CPU con la richiesta di modifica. 

## <a name="steps-to-scale-up"></a>Passaggi per la scalabilità verticale
1. Passare al cluster. Sotto **le impostazioni**, selezionare **aumentare**.

    Si è illustrato un elenco degli SKU disponibili. Nella figura seguente, ad esempio, solo quattro SKU sono disponibili.

    ![Aumentare le prestazioni](media/manage-cluster-scale-up/scale-up.png)

    Gli SKU sono disabilitati perché si tratta dello SKU corrente oppure non sono disponibili nell'area in cui si trova il cluster.

1. Per modificare lo SKU, selezionare lo SKU desiderato e scegliere il **seleziona** pulsante.

> [!NOTE]
> Il processo di scalabilità verticale può richiedere alcuni minuti e durante tale periodo verrà sospeso il cluster. Si noti che, riducendo le prestazioni, si può compromettere l'efficienza del cluster.

Ora effettuata un'operazione di aumento o riduzione delle prestazioni per il cluster di Esplora dati di Azure.

## <a name="next-steps"></a>Passaggi successivi
È anche possibile [gestire i cluster di scalabilità orizzontale](manage-cluster-scale-out.md) ridimensionare in modo dinamico il numero di istanze in base alle metriche che specificano out.

Se occorre assistenza per problemi di ridimensionamento del cluster [aprire una richiesta di supporto](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) nel portale di Azure.

Monitorare l'utilizzo delle risorse seguendo questo articolo: [Monitorare le prestazioni di Esplora dati di Azure, integrità e sull'utilizzo con le metriche](using-metrics.md).
