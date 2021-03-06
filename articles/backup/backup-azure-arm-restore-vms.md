---
title: 'Backup di Azure: Ripristinare macchine virtuali tramite il portale di Azure'
description: Ripristinare una macchina virtuale di Azure da un punto di ripristino con il portale di Azure
services: backup
author: geethalakshmig
manager: vijayts
keywords: ripristinare il backup; come ripristinare; punto di ripristino.
ms.service: backup
ms.topic: conceptual
ms.date: 03/28/2019
ms.author: geg
ms.openlocfilehash: b0408aa296dcbff0c73f2c192e24c290d51fec5f
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60647821"
---
# <a name="restore-azure-vms"></a>Ripristinare VM di Azure

Questo articolo descrive come ripristinare i dati delle macchine virtuali di Azure dai punti di ripristino archiviati negli insiemi di credenziali di Servizi di ripristino di [Backup di Azure](backup-overview.md).



### <a name="restore-options"></a>Opzioni di ripristino

Backup di Azure offre diversi modi per ripristinare una macchina virtuale.

**Opzione di ripristino** | **Dettagli**
--- | ---
**Create a new VM** (Crea una nuova macchina virtuale) | Crea e rende operativa rapidamente una macchina virtuale di base a partire da un punto di ripristino.<br/><br/> È possibile specificare un nome per la macchina virtuale, selezionare il gruppo di risorse e la rete virtuale in cui inserirla, nonché specificare un tipo di archiviazione.
**Restore disk** (Ripristina disco) | Ripristina un disco della macchina virtuale che può quindi essere usato per creare una nuova macchina virtuale.<br/><br/> Backup di Azure offre un modello che consente di personalizzare e creare una macchina virtuale. <br/><br/> Questa opzione copia i dischi rigidi virtuali nell'account di archiviazione specificato. Il processo di ripristino genera un modello che può essere scaricato e usato per specificare impostazioni della macchina virtuale personalizzate e creare una macchina virtuale.<br/><br/> L'account di archiviazione deve essere nella stessa località dell'insieme di credenziali. Se non ne è già disponibile uno, creare un account di archiviazione.<br/><br/> Verrà visualizzato il tipo di replica dell'account di archiviazione. L'archiviazione con ridondanza della zona non è supportata.<br/><br/> In alternativa, è possibile collegare il disco a una macchina virtuale esistente o creare una nuova macchina virtuale usando PowerShell.<br/><br/> Questa opzione è utile se si vuole personalizzare la macchina virtuale, aggiungere impostazioni di configurazione non presenti al momento del backup o aggiungere impostazioni che devono essere configurate usando il modello o PowerShell.
**Sostituisci esistente** | È possibile ripristinare un disco e usarlo per sostituire un disco nella macchina virtuale esistente.<br/><br/> Deve essere presente la macchina virtuale corrente. Se è stata eliminata non è possibile usare questa opzione.<br/><br/> Backup di Azure crea uno snapshot della macchina virtuale esistente prima di sostituire il disco. Lo snapshot viene archiviato nel percorso di gestione temporanea specificato. I dischi esistenti connessi alla macchina virtuale vengono quindi sostituiti usando il punto di ripristino selezionato.<br/><br/> Lo snapshot che è stato creato viene copiato nell'insieme di credenziali e conservato in conformità con i criteri di conservazione specificati. <br/><br/> L'opzione Sostituisci esistente è supportata per le macchine virtuali gestite non crittografate. Non è supportata per i dischi non gestiti, le [macchine virtuali generalizzate](https://docs.microsoft.com/azure/virtual-machines/windows/capture-image-resource) o le macchine virtuali [create usando immagini personalizzate](https://azure.microsoft.com/resources/videos/create-a-custom-virtual-machine-image-in-azure-resource-manager-with-powershell/).<br/><br/> Se il punto di ripristino ha un numero maggiore o minore di dischi rispetto alla macchina virtuale corrente, il numero di dischi nel punto di ripristino rifletterà solo la configurazione della macchina virtuale.<br/><br/>

> [!NOTE]
> È anche possibile ripristinare file e cartelle specifici in una macchina virtuale di Azure. [Altre informazioni](backup-azure-restore-files-from-vm.md)
>
> Se si esegue la [versione più recente](backup-instant-restore-capability.md) di Backup di Azure per macchine virtuali di Azure (noto come Ripristino istantaneo), gli snapshot possono essere conservati fino a un massimo di sette giorni ed è possibile ripristinare una macchina virtuale dagli snapshot prima che i dati di backup vengano inviati all'insieme di credenziali. Se si vuole ripristinare una macchina virtuale da un backup degli ultimi sette giorni, è più rapido effettuare il ripristino dallo snapshot anziché dall'insieme di credenziali.

## <a name="before-you-start"></a>Prima di iniziare

Ripristinare una macchina virtuale (Crea una nuova macchina virtuale) assicurarsi di avere il controllo di accesso corretti in base al ruolo (RBAC) [autorizzazioni](backup-rbac-rs-vault.md#mapping-backup-built-in-roles-to-backup-management-actions) per l'operazione di ripristino della macchina virtuale.

Se non si dispone delle autorizzazioni, è possibile [ripristinare un disco](#restore-disks), quindi dopo che il disco ripristinato, è possibile [usare il modello](#use-templates-to-customize-a-restored-vm) che è stato generato come parte dell'operazione di ripristino per creare una nuova macchina virtuale.



## <a name="select-a-restore-point"></a>Selezionare un punto di ripristino

1. Nell'insieme di credenziali associato alla macchina virtuale da ripristinare, fare clic su **Elementi di backup** > **Macchina virtuale di Azure**.
2. Fare clic su una macchina virtuale. Per impostazione predefinita, nel dashboard della macchina virtuale verranno visualizzati i punti di ripristino degli ultimi 30 giorni. È possibile visualizzare punti di ripristino antecedenti a 30 giorni o applicare un filtro per trovare punti di ripristino in base a date, intervalli di tempo e tipi diversi di coerenza degli snapshot.
3. Per ripristinare la macchina virtuale, fare clic su **Ripristina macchina virtuale**.

    ![Punto di ripristino](./media/backup-azure-arm-restore-vms/restore-point.png)

4. Selezionare un punto di ripristino da usare per il ripristino.

## <a name="choose-a-vm-restore-configuration"></a>Scegliere una configurazione di ripristino per la macchina virtuale

1. In **Configurazione di ripristino** selezionare un'opzione di ripristino:
    - **Crea nuovo**: Usare questa opzione se si vuole creare una nuova macchina virtuale. È possibile creare una macchina virtuale con impostazioni semplici o ripristinare un disco e creare una macchina virtuale personalizzata.
    - **Sostituisci esistente**. Usare questa opzione se si vuole sostituire dischi in una macchina virtuale esistente.

        ![Configurazione guidata di ripristino](./media/backup-azure-arm-restore-vms/restore-configuration.png)

2. Specificare le impostazioni per l'opzione di ripristino selezionata.

## <a name="create-a-vm"></a>Creare una macchina virtuale

Tra le [opzioni di ripristino](#restore-options) è possibile creare rapidamente una macchina virtuale con le impostazioni di base da un punto di ripristino.

1. In **Configurazione di ripristino** > **Crea nuovo** > **Tipo di ripristino** selezionare **Crea macchina virtuale**.
2. In **Nome della macchina virtuale** specificare una macchina virtuale che non è presente nella sottoscrizione.
3. In **Gruppo di risorse** selezionare un gruppo di risorse esistente per la nuova macchina virtuale o crearne uno nuovo con un nome univoco globale. Se si assegna un nome già esistente, Azure assegnerà al gruppo lo stesso nome della macchina virtuale.
4. In **Rete virtuale** selezionare la rete virtuale in cui verrà inserita la macchina virtuale. Vengono visualizzate tutte le reti virtuali associate alla sottoscrizione. Selezionare la subnet. La prima subnet è selezionata per impostazione predefinita.
5. In **Posizione di archiviazione** specificare il tipo di archiviazione usato per la macchina virtuale.

    ![Configurazione guidata di ripristino](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard1.png)

6. In **Configurazione di ripristino** selezionare **OK**. In **Ripristino** fare clic su **Ripristina** per attivare l'operazione di ripristino.


## <a name="restore-disks"></a>Ripristinare i dischi

Tra le [opzioni di ripristino](#restore-options) è possibile creare un disco da un punto di ripristino. Con il disco è quindi possibile eseguire una di queste operazioni:

- Usare il modello generato durante l'operazione di ripristino per personalizzare le impostazioni e attivare la distribuzione della macchina virtuale. Modificare le impostazioni predefinite del modello e inviare il modello per la distribuzione della macchina virtuale.
- [Collegare i dischi ripristinati](https://docs.microsoft.com/azure/virtual-machines/windows/attach-managed-disk-portal) a una macchina virtuale esistente.
- [Creare una nuova VM](https://docs.microsoft.com/azure/backup/backup-azure-vms-automation#create-a-vm-from-restored-disks) dai dischi ripristinati tramite PowerShell.

1. In **Configurazione di ripristino** > **Crea nuovo** > **Tipo di ripristino** selezionare **Dischi di ripristino**.
2. In **Gruppo di risorse** selezionare un gruppo di risorse per i dischi ripristinati o crearne uno nuovo con un nome univoco globale.
3. In **Account di archiviazione** specificare l'account in cui copiare i dischi rigidi virtuali. Verificare che l'account si trovi nella stessa area dell'insieme di credenziali.

    ![Configurazione di ripristino completata](./media/backup-azure-arm-restore-vms/trigger-restore-operation1.png)

4. In **Configurazione di ripristino** selezionare **OK**. In **Ripristino** fare clic su **Ripristina** per attivare l'operazione di ripristino.

Durante il ripristino di VM, Backup di Azure non Usa account di archiviazione. Ma in caso di **ripristinare i dischi** e **ripristino istantaneo**, account di archiviazione viene usato per l'archiviazione dei modelli.

### <a name="use-templates-to-customize-a-restored-vm"></a>Usare i modelli per personalizzare una VM ripristinata

Dopo il ripristino del disco, usare il modello generato come parte dell'operazione di ripristino per personalizzare e creare una nuova macchina virtuale:

1. Aprire **Ripristina - Dettagli processo** per il processo pertinente.

2. In **Ripristino - Dettagli processo** selezionare **Deploy Template** (Distribuisci modello) per avviare la distribuzione del modello.

    ![Drill-down del processo di ripristino](./media/backup-azure-arm-restore-vms/restore-job-drill-down1.png)

3. Per personalizzare l'impostazione della macchina virtuale inclusa nel modello, fare clic su **Modifica modello**. Se si vuole aggiungere altre personalizzazioni, fare clic su **Modifica parametri**.
    - [Vedere altre informazioni](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template) sulla distribuzione delle risorse da un modello personalizzato.
    - [Vedere altre informazioni](../azure-resource-manager/resource-group-authoring-templates.md) sulla creazione di modelli.

   ![Caricare la distribuzione del modello](./media/backup-azure-arm-restore-vms/edit-template1.png)

4. Immettere i valori personalizzati per la macchina virtuale, accettare quanto dichiarato in **Condizioni** e fare clic su **Acquista**.

   ![Inviare la distribuzione del modello](./media/backup-azure-arm-restore-vms/submitting-template1.png)


## <a name="replace-existing-disks"></a>Sostituire i dischi esistenti

Tra le [opzioni di ripristino](#restore-options) è possibile sostituire un disco di macchina virtuale esistente con il punto di ripristino selezionato. [Rivedere](#restore-options) tutte le opzioni di ripristino.

1. In **Configurazione di ripristino** fare clic su **Sostituisci esistente**.
2. In **Tipo ripristino** selezionare **Replace disk/s** (Sostituisci dischi). Questo è il punto di ripristino che verrà usato per sostituire i dischi delle macchine virtuali esistenti.
3. In **Posizione per la gestione temporanea** specificare dove salvare snapshot dei dischi gestiti correnti.

   ![Configurazione guidata del ripristino - Sostituisci esistente](./media/backup-azure-arm-restore-vms/restore-configuration-replace-existing.png)


## <a name="restore-vms-with-special-configurations"></a>Ripristino di macchine virtuali con configurazioni speciali

Esistono diversi scenari comuni in cui potrebbe essere necessario ripristinare le macchine virtuali.

**Scenario** | **Materiale sussidiario**
--- | ---
**Ripristino di macchine virtuali con vantaggio Hybrid Use** | Se una macchina virtuale Windows usa la [licenza per il vantaggio Hybrid Use (HUB)](../virtual-machines/windows/hybrid-use-benefit-licensing.md), ripristinare i dischi e creare una nuova macchina virtuale usando il modello fornito (con **Tipo di licenza** impostato su **Windows_Server**) o PowerShell.  È possibile applicare questa impostazione anche dopo aver creato la macchina virtuale.
**Ripristino di macchine virtuali durante un'emergenza nel data center di Azure** | Se l'insieme di credenziali usa l'archiviazione con ridondanza geografica e il data center principale per la macchina virtuale si arresta, Backup di Azure supporta il ripristino delle macchine virtuali sottoposte a backup nel data center associato. Selezionare un account di archiviazione nel data center associato e ripristinare come di consueto. Backup di Azure usa il servizio di calcolo nella posizione associata per creare la macchina virtuale ripristinata. [Vedere altre informazioni](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md) sulla resilienza dei data center.
**Ripristino di una macchina virtuale con controller di dominio singolo in un dominio singolo** | Ripristinare la macchina virtuale come qualsiasi altra macchina virtuale. Si noti che:<br/><br/> Da una prospettiva di Active Directory, la macchina virtuale di Azure è come qualsiasi altra macchina virtuale.<br/><br/> È anche disponibile Modalità ripristino servizi directory (Directory Services Restore Mode, DSRM), in modo che tutti gli scenari di ripristino di Active Directory siano attuabili. [Vedere altre informazioni](https://docs.microsoft.com/windows-server/identity/ad-ds/get-started/virtual-dc/virtualized-domain-controllers-hyper-v) sul backup e il ripristino dei controller di dominio virtualizzati.
**Ripristino di macchine virtuali con più controller di dominio in un dominio singolo** | Se altri controller di dominio nello stesso dominio può essere raggiunto tramite la rete, il controller di dominio può essere ripristinato come qualsiasi altra macchina virtuale. Se si tratta dell'ultimo controller di dominio restante nel dominio o viene eseguito un ripristino in una rete isolata, effettuare un [ripristino della foresta](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/ad-forest-recovery-single-domain-in-multidomain-recovery).
**Ripristino di domini multipli in una foresta** | È consigliabile eseguire un [ripristino della foresta](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/ad-forest-recovery-single-domain-in-multidomain-recovery).
**Ripristino bare metal** | La differenza principale tra le macchine virtuali di Azure e gli hypervisor locali consiste nel fatto che in Azure non è disponibile una console per macchine virtuali. La console è obbligatoria per alcuni scenari, ad esempio per il ripristino tramite un backup di tipo di ripristino bare metal (BMR). Tuttavia, il ripristino della macchina virtuale dall'insieme di credenziali è una sostituzione completa con il ripristino bare metal.
**Ripristino di macchine virtuali con configurazioni di rete speciali** | Configurazioni di rete speciali includono macchine virtuali con bilanciamento del carico interno o esterno, con più schede di interfaccia di rete o con più indirizzi IP riservati. Per ripristinare queste macchine virtuali, usare l'[opzione relativa al disco di ripristino](#restore-disks). Questa opzione Crea una copia di dischi rigidi virtuali in account di archiviazione specificato e quindi è possibile creare una macchina virtuale con un [interno](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/) oppure [esterno](https://azure.microsoft.com/documentation/articles/load-balancer-internet-getstarted/) servizio di bilanciamento del carico [più schede di rete](../virtual-machines/windows/multiple-nics.md), o [più indirizzi IP riservati](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md), in conformità con la configurazione.
**Gruppo di sicurezza di rete (NSG) sulla scheda di rete/Subnet** | Backup delle VM di Azure supporta le informazioni di Backup e ripristino configurazione di sicurezza di rete nella rete virtuale, subnet e a livello di interfaccia di rete.
**Zona aggiunto macchine virtuali** | Backup di Azure supporta il backup e ripristino di macchine virtuali bloccate suddiviso in zone. [Altre informazioni](https://azure.microsoft.com/global-infrastructure/availability-zones/)

## <a name="track-the-restore-operation"></a>Tenere traccia dell'operazione di ripristino
Dopo l'attivazione dell'operazione di ripristino, il servizio di backup crea un processo per tenerne traccia. Backup di Azure consente di visualizzare le notifiche relative al processo nel portale. Se non sono visibili, fare clic sul simbolo **Notifiche** per visualizzarle.

![Ripristino attivato](./media/backup-azure-arm-restore-vms/restore-notification1.png)

 Tenere traccia del ripristino come segue:

1. Per visualizzare le operazioni relative al processo, fare clic sul collegamento ipertestuale relativo alle notifiche. In alternativa, nell'insieme di credenziali fare clic su **Processi di backup** e quindi sulla macchina virtuale pertinente.

    ![Elenco di VM in un insieme di credenziali](./media/backup-azure-arm-restore-vms/restore-job-in-progress1.png)

2. Per monitorare lo stato di un ripristino, fare clic su un processo di ripristino con stato **In corso**. Verrà visualizzato l'indicatore di stato che fornisce informazioni sullo stato di avanzamento del ripristino:

    - **Estimated time of restore** (Tempo di ripristino stimato): indica inizialmente il tempo impiegato per il completamento dell'operazione di ripristino. Con il progressivo avanzamento dell'operazione, il tempo impiegato si riduce fino a raggiungere il valore 0 al termine dell'operazione di ripristino.
    - **Percentage of restore** (Percentuale di ripristino): mostra la percentuale di completamento dell'operazione di ripristino.
    - **Number of bytes transferred** (Numero di byte trasferiti): se si sta eseguendo il ripristino creando una nuova macchina virtuale, mostra i byte trasferiti a fronte del numero totale di byte da trasferire.

## <a name="post-restore-steps"></a>Operazioni successive al ripristino

Esistono diversi aspetti di cui tenere conto dopo il ripristino di una macchina virtuale:

- Le estensioni presenti durante la configurazione del backup vengono installate, ma non abilitate. Se si verifica un problema, reinstallare le estensioni.
- Se la macchina virtuale sottoposta a backup era associata a un indirizzo IP statico, la macchina virtuale ripristinata avrà un indirizzo IP dinamico per evitare conflitti. È possibile [aggiungere un indirizzo IP statico alla macchina virtuale ripristinata](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm).
- Una macchina virtuale ripristinata non ha un set di disponibilità. Se si usa l'opzione relativa al disco di ripristino, è possibile [specificare un set di disponibilità](../virtual-machines/windows/tutorial-availability-sets.md) quando si crea una macchina virtuale dal disco usando il modello fornito o PowerShell.
- Se si usa una distribuzione Linux basata su cloud-init, ad esempio Ubuntu, per motivi di sicurezza la password verrà bloccata dopo il ripristino. Per [reimpostare la password](../virtual-machines/linux/reset-password.md) nella VM ripristinata, usare l'estensione VMAccess. È consigliabile usare chiavi SSH in queste distribuzioni in modo da non dover reimpostare la password dopo il ripristino.


## <a name="backing-up-restored-vms"></a>Backup di macchine virtuali ripristinate

- Se una macchina virtuale è stata ripristinata nello stesso gruppo di risorse con lo stesso nome della macchina virtuale di cui è stato originariamente eseguito il backup, l'operazione di backup continuerà nella macchina virtuale dopo il ripristino.
- Se la macchina virtuale è stata ripristinata in un gruppo di risorse diverso o si è specificato un nome diverso per la macchina virtuale ripristinata, sarà necessario configurare il backup per la macchina virtuale ripristinata.

## <a name="next-steps"></a>Passaggi successivi

- In caso di difficoltà durante il processo di ripristino, [esaminare](backup-azure-vms-troubleshoot.md#restore) i problemi e gli errori comuni.
- Dopo il ripristino della macchina virtuale, vedere altre informazioni sulla [gestione delle macchine virtuali](backup-azure-manage-vms.md).
