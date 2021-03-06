---
title: Eseguire il failover e riproteggere le VM di Azure replicate in un'area di Azure secondaria per il ripristino di emergenza con il servizio Azure Site Recovery
description: Informazioni su come eseguire il failover e riproteggere le VM di Azure replicate in un'area di Azure secondaria per il ripristino di emergenza con il servizio Azure Site Recovery.
services: site-recovery
author: rayne-wiselman
manager: carmonm
ms.service: site-recovery
ms.topic: tutorial
ms.date: 04/08/2019
ms.author: raynew
ms.custom: mvc
ms.openlocfilehash: 96e3c0b761a9ed4c5f84d8ece1ba504bd5aacf6f
ms.sourcegitcommit: c174d408a5522b58160e17a87d2b6ef4482a6694
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "59797568"
---
# <a name="fail-over-and-reprotect-azure-vms-between-regions"></a>Eseguire il failover e riproteggere le VM di Azure tra aree

Il servizio [Azure Site Recovery](site-recovery-overview.md) favorisce l'attuazione della strategia di ripristino di emergenza gestendo e coordinando le operazioni di replica, failover e failback di computer locali e macchine virtuali di Azure.

Questa esercitazione illustra come eseguire il failover di una VM di Azure in un'area di Azure secondaria. Dopo aver eseguito il failover, si riproteggerà la VM. In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Eseguire il failover della macchina virtuale di Azure
> * Riproteggere la macchina virtuale secondaria di Azure in modo che possa essere replicata nell'area primaria.

> [!NOTE]
> Questa esercitazione contiene il percorso più semplice, con impostazioni predefinite e personalizzazione minima. Per scenari più complessi, usare gli articoli sulle procedure per le VM di Azure.

## <a name="prerequisites"></a>Prerequisiti

- Assicurarsi di avere completato un'[analisi di ripristino di emergenza](azure-to-azure-tutorial-dr-drill.md) per verificare che tutto funzioni come previsto.
- Verificare le proprietà della macchina virtuale prima di eseguire il failover di test. La macchina virtuale deve essere conforme ai [requisiti di Azure](azure-to-azure-support-matrix.md#replicated-machine-operating-systems).

## <a name="run-a-failover-to-the-secondary-region"></a>Eseguire un failover nell'area secondaria

1. In **Elementi replicati** selezionare la macchina virtuale di cui si vuole eseguire il failover e scegliere **Failover**

   ![Failover](./media/azure-to-azure-tutorial-failover-failback/failover.png)

2. In **Failover** selezionare un **Punto di ripristino** in cui eseguire il failover. È possibile usare una delle opzioni seguenti.

   * **Più recente** (impostazione predefinita): determina l'elaborazione di tutti i dati nel servizio Site Recovery e offre il valore RPO (Recovery Point Objective) più basso.
   * **Elaborato più recente**: ripristina la macchina virtuale all'ultimo punto di ripristino che è stato elaborato dal servizio Site Recovery.
   * **Personalizzato**: consente di eseguire il failover in un determinato punto di ripristino ed è particolarmente utile per eseguire un failover di test.

3. Selezionare **Arrestare la macchina prima di iniziare il failover** se si vuole provare ad arrestare le macchine virtuali di origine tramite Site Recovery prima di attivare il failover. Il failover continua anche se l'arresto ha esito negativo. Site Recovery non esegue la pulizia dell'origine dopo il failover.

4. Nella pagina **Processi** è possibile seguire lo stato di avanzamento del failover.

5. Dopo il failover, convalidare la macchina virtuale eseguendo l'accesso ad essa. Per passare a un altro punto di ripristino per la macchina virtuale, è possibile usare l'opzione **Modifica punto di ripristino**.

6. Quando la macchina virtuale sottoposta a failover è pronta, è possibile eseguire il **commit** del failover.
   Questa operazione elimina tutti i punti di ripristino disponibili con il servizio. Non sarà possibile modificare il punto di ripristino.

## <a name="reprotect-the-secondary-vm"></a>Riproteggere la macchina virtuale secondaria

Dopo aver eseguito il failover della macchina virtuale, è necessario proteggerla in modo che possa essere nuovamente replicata nell'area primaria.

1. Assicurarsi che lo stato della macchina virtuale sia **Commit del failover eseguito** e verificare che l'area primaria sia disponibile e che sia possibile creare e accedere alle nuove risorse presenti al suo interno.
2. In **Insieme di credenziali** > **Elementi replicati**, fare clic con il pulsante destro del mouse sulla macchina virtuale di cui è stato eseguito il failover e quindi scegliere **Riproteggi**.

   ![Fare clic con il pulsante destro del mouse per riproteggere](./media/azure-to-azure-tutorial-failover-failback/reprotect.png)

2. Verificare che la direzione di protezione, dall'area secondaria a quella primaria, sia già selezionata.
3. Rivedere le informazioni contenute in **Gruppo di risorse, Rete, Archiviazione e Set di disponibilità**. Eventuali risorse contrassegnate come nuove verranno create nell'ambito dell'operazione di riprotezione.
4. Fare clic su **OK** per avviare un processo di riprotezione. Con questo processo il sito di destinazione viene aggiornato con i dati più recenti e i valori delta vengono replicati nell'area primaria. La macchina virtuale si trova ora in uno stato protetto.

## <a name="next-steps"></a>Passaggi successivi
- Dopo la riprotezione, vedere come [eseguire il failback](azure-to-azure-tutorial-failback.md) nell'area primaria quando torna disponibile.
- [Altre informazioni](azure-to-azure-how-to-reprotect.md#what-happens-during-reprotection) sul flusso di riprotezione.
