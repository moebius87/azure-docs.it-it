---
author: cynthn
ms.service: virtual-machines
ms.topic: include
ms.date: 10/26/2018
ms.author: cynthn
ms.openlocfilehash: ccc2b574ea054a1b0ecf32a1e59691050fb66fcf
ms.sourcegitcommit: 61c8de2e95011c094af18fdf679d5efe5069197b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62108294"
---
## <a name="tagging-a-virtual-machine-through-templates"></a>Assegnazione di tag a una macchina virtuale tramite modelli
In primo luogo, diamo un'occhiata ai tag tramite modelli. [Questo modello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) inserisce i tag per le risorse seguenti: Calcolo (macchina virtuale), archiviazione (Account di archiviazione) e rete (indirizzo IP pubblico, rete virtuale e interfaccia di rete). Questo modello riguarda una VM Windows ma può essere adattato per le VM Linux.

Fare clic sul pulsante **Distribuisci in Azure** dal [collegamento modello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags). Verrà visualizzato il [portale di Azure](https://portal.azure.com/) in cui è possibile distribuire il modello.

![Distribuzione semplice di tag](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

Questo modello include i seguenti tag: *Reparto*, *Application*, e *creati da*. È possibile aggiungere o modificare questi tag direttamente nel modello se si desiderano diversi nomi di tag.

![Tag di Azure in un modello](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

Come si può vedere, i tag vengono definiti come coppie chiave/valore, separate da due punti (:). I tag devono essere definiti in questo formato:

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

Salvare il file di modello al termine della modifica, con i tag di propria scelta.

Successivamente, nella sezione **Modifica parametri** , è possibile compilare i valori per i tag.

![Modificare i tag nel portale di Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

Fare clic su **Crea** per distribuire il modello con i valori dei tag.

## <a name="tagging-through-the-portal"></a>Assegnazione di tag tramite il portale
Dopo aver creato le risorse con i tag, è possibile visualizzare, aggiungere ed eliminare i tag nel portale.

Selezionare l'icona di tag per visualizzare i tag:

![Icona di tag nel portale di Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

Aggiungere un nuovo tag tramite il portale definendo la propria coppia chiave/valore e salvarlo.

![Aggiungi nuovo Tag nel portale di Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

Il nuovo tag verrà visualizzato nell'elenco dei tag per la risorsa.

![Nuovo Tag salvato nel portale di Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

