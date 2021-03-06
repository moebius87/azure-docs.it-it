---
title: Scegliere le dimensioni delle macchine virtuali per i pool - Azure Batch | Microsoft Docs
description: Come scegliere tra le dimensioni delle macchine virtuali disponibili per i nodi di calcolo nei pool di Azure Batch
services: batch
documentationcenter: ''
author: laurenhughes
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: batch
ms.workload: ''
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/25/2019
ms.author: lahugh
ms.custom: seodec18
ms.openlocfilehash: 43094839c9da9b00c97d1dffd53f98a3acd119d5
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60775730"
---
# <a name="choose-a-vm-size-for-compute-nodes-in-an-azure-batch-pool"></a>Scegliere le dimensioni delle macchine virtuali per i nodi di calcolo in un pool di Azure Batch

Quando si selezionano le dimensioni del nodo per un pool di Azure Batch, è possibile scegliere tra quasi tutte le dimensioni di VM disponibili in Azure. Azure offre un'ampia gamma di dimensioni per le VM Linux e Windows per carichi di lavoro diversi.

Esistono alcune eccezioni e limitazioni nella scelta delle dimensioni delle macchine virtuali:

* Alcune famiglie o dimensioni di VM non sono supportati in Azure Batch. 
* Alcune dimensioni delle macchine virtuali sono soggette a restrizioni e devono essere abilitate specificamente prima che sia possibile allocarle.

## <a name="supported-vm-families-and-sizes"></a>Famiglie e dimensioni di VM supportati

### <a name="pools-in-virtual-machine-configuration"></a>Pool in configurazione di tipo macchina virtuale

I pool di Batch in configurazione macchina virtuale supportano tutte le dimensioni di VM ([Linux](../virtual-machines/linux/sizes.md), [Windows](../virtual-machines/windows/sizes.md)) *tranne* le seguenti:

| Famiglia  | Dimensioni non supportate  |
|---------|---------|
| Serie A Basic | Basic_A0 (A0) |
| Serie A | Standard_A0 |
| Serie B | Tutti |
| Serie DC | Tutti |
| Con ottimizzazione estrema per la memoria | Tutti |
| Serie Hb<sup>1,2</sup> | Tutti |
| Serie Hc<sup>1,2</sup> | Tutti |
| Serie Lsv2 | Tutti |
| Serie NDv2<sup>1,2</sup> | Tutti |
| Serie NDv2<sup>1</sup> | Tutti |
| SAP HANA | Tutti |


<sup>1</sup> Pianificato per il supporto.  
<sup>2</sup> Può essere usato dagli account Batch in modalità sottoscrizione utente. Nell'account Batch della modalità sottoscrizione utente deve essere impostata la quota di core. Per altre informazioni, vedere la [configurazione per la modalità sottoscrizione utente](batch-account-create-portal.md#additional-configuration-for-user-subscription-mode).

Le dimensioni seguenti di VM sono supportate solo per i nodi per priorità bassa:

| Famiglia  | Dimensioni supportate  |
|---------|---------|
| Serie M | Standard_M64ms |
| Serie M | Standard_M128s |

Altre dimensioni di VM della famiglia della serie M non sono attualmente supportate.

### <a name="pools-in-cloud-service-configuration"></a>Pool in configurazione di tipo servizio cloud

I pool di Batch in configurazione servizio cloud supportano tutte le [dimensioni di VM per i servizi cloud](../cloud-services/cloud-services-sizes-specs.md) *tranne* le seguenti:

| Famiglia  | Dimensioni non supportate  |
|---------|---------|
| Serie A | Molto piccola |
| Serie Av2 | Standard_A1_v2, Standard_A2_v2, Standard_A2m_v2 |

## <a name="restricted-vm-families"></a>Famiglie di VM con restrizioni

Le famiglie di VM seguenti possono essere allocate in pool di Batch, ma è necessario richiedere uno specifico aumento della quota (vedere [questo articolo](batch-quota-limit.md#increase-a-quota)):

* Serie NCv2
* Serie NCv3
* Serie ND

Queste dimensioni possono essere usate solo in pool nella configurazione della macchina virtuale.

## <a name="size-considerations"></a>Considerazioni sulle dimensioni

* **Requisiti dell'applicazione**: tenere in considerazione le caratteristiche e i requisiti delle applicazioni che si eseguiranno nei nodi. Per determinare la dimensioni del nodo più appropriate e convenienti, considerare vari aspetti, ad esempio se si tratta di un'applicazione multithreading e la quantità di memoria che utilizza. Per [carichi di lavoro MPI](batch-mpi.md) a istanze multiple o applicazioni CUDA, prendere in considerazione rispettivamente le dimensioni specializzate [HPC](../virtual-machines/linux/sizes-hpc.md) o [abilitate per GPU](../virtual-machines/linux/sizes-gpu.md). Vedere [Usare istanze con supporto per RDMA o abilitate per GPU in pool di Batch](batch-pool-compute-intensive-sizes.md).

* **Attività per nodo**: le dimensioni del nodo vengono in genere selezionate presupponendo che in un nodo venga eseguita un'attività alla volta. Tuttavia, può risultare utile che più attività (e quindi più istanze dell'applicazione) vengano [eseguite in parallelo](batch-parallel-node-tasks.md) nei nodi di calcolo durante l'esecuzione del processo. In questo caso, è normale scegliere una dimensione multicore per il nodo per soddisfare la richiesta più elevata di esecuzione di attività parallele.

* **Livelli di carico per attività diverse**: tutti i nodi in un pool hanno le stesse dimensioni. Se si prevede di eseguire applicazioni con requisiti di sistema e/o livelli di carico diversi, è consigliabile usare pool separati. 

* **Disponibilità a livello di area**: è possibile che una famiglia o dimensione di VM non sia disponibile nelle aree in cui si crea l'account Batch. Per verificare la disponibilità di una dimensione, vedere [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/services/).

* **Quote** : la [quota di core](batch-quota-limit.md#resource-quotas) nell'account Batch può limitare il numero di nodi con le dimensioni specificate che possono essere aggiunti a un pool di Batch. Per richiedere un aumento delle quote, vedere [questo articolo](batch-quota-limit.md#increase-a-quota). 

* **Configurazione del pool**: in generale, quando si crea un pool in configurazione macchina virtuale si hanno più opzioni di dimensioni delle VM rispetto alla configurazione servizio cloud.

## <a name="next-steps"></a>Passaggi successivi

* Per una panoramica dettagliata di Batch, vedere [Sviluppare soluzioni di calcolo parallele su larga scala con Batch](batch-api-basics.md).
* Per informazioni sull'uso di dimensioni delle VM a elevato utilizzo di calcolo, vedere [Usare istanze con supporto per RDMA o abilitate per GPU in pool di Batch](batch-pool-compute-intensive-sizes.md).
