---
title: Visualizzare le prenotazioni per le risorse di Azure | Microsoft Docs
description: Informazioni su come visualizzare le prenotazioni per Azure nel portale di Azure.
documentationcenter: ''
author: yashesvi
manager: yashar
editor: ''
ms.service: billing
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/13/2019
ms.author: banders
ms.openlocfilehash: 872837c774368820527b12778b1a7dd4ddc5c7af
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60369168"
---
# <a name="view-azure-reservations-in-the-azure-portal"></a>Visualizzare le prenotazioni di Azure nel portale di Azure

A seconda del tipo di sottoscrizione e le autorizzazioni, esistono un paio di modi per visualizzare le prenotazioni per Azure.

## <a name="view-purchased-reservations"></a>Visualizzare le prenotazioni acquistate

Per impostazione predefinita, quando si acquista una prenotazione, l'utente e l'amministratore dell'account possono visualizzare la prenotazione. Utenti e amministratore account ottengono automaticamente il ruolo di proprietario sull'ordine di prenotazione e sulla prenotazione. Per consentire ad altri utenti di visualizzare la prenotazione, è necessario aggiungerli come un **Owner** oppure **lettore** in ordine di prenotazione o di prenotazione.

Per altre informazioni vedere [Aggiungere o modificare gli utenti che possono gestire una prenotazione](billing-manage-reserved-vm-instance.md#add-or-change-users-who-can-manage-a-reservation).

Per visualizzare una prenotazione come proprietario o lettore,

1. Accedere al [portale di Azure](https://portal.azure.com).
2. Cercare **Prenotazioni**.
    ![Screenshot che mostra una ricerca del portale di Azure](./media/billing-view-reservation/portal-reservation-search.png)  
3. L'elenco Mostra tutte le prenotazioni in cui si dispone del ruolo di proprietario o lettore. Ogni prenotazione Mostra la percentuale di utilizzo noti ultimo.  
    ![Esempio che mostra un elenco delle prenotazioni](./media/billing-view-reservation/view-reservations.png)
4. Selezionare una prenotazione e visualizzare la tendenza di utilizzo per gli ultimi cinque giorni.  
    ![Tendenze di utilizzo di esempio che mostra la prenotazione](./media/billing-view-reservation/reservation-utilization.png)
5. È anche possibile ottenere il [utilizzo di prenotazione](/rest/api/billing/enterprise/billing-enterprise-api-reserved-instance-usage) usando l'API di utilizzo delle istanze riservate e con la [pacchetto di contenuto di Power BI Insights il consumo di Microsoft Azure](/power-bi/service-connect-to-azure-consumption-insights).

Se è necessario modificare l'ambito di una prenotazione, dividere una prenotazione, oppure modificare chi può gestire una prenotazione, vedere [gestire le prenotazioni Azure](billing-manage-reserved-vm-instance.md).

## <a name="view-reservation-transactions-for-enterprise-enrollments"></a>Visualizzare le transazioni di prenotazione per le registrazioni Enterprise

 Se si dispone di una registrazione Enterprise gestita dal partner, visualizzare le prenotazioni in **Report** nel portale EA. Per altre registrazioni Enterprise, è possibile visualizzare le prenotazioni nel portale EA e nel portale di Azure. È necessario essere un amministratore EA per visualizzare le transazioni di prenotazione.

Per visualizzare le transazioni di prenotazione nel portale di Azure,

1. Accedere al [portale di Azure](https://portal.azure.com).
1. Eseguire ricerche in **Gestione dei costi e fatturazione**.

    ![Screenshot che mostra una ricerca nel portale di Azure](./media/billing-view-reservation/portal-cm-billing-search.png)

1. Selezionare **Transazioni di prenotazione**.
1. Per filtrare i risultati, selezionare **Intervallo di tempo**, **Tipo**, o **Descrizione**.
1. Selezionare **Applica**.

    ![Screenshot che mostra i risultati delle transazioni di prenotazione](./media/billing-view-reservation/portal-billing-reservation-transaction-results.png)

Per ottenere i dati usando un'API, vedere [Get Reserved Instance transaction charges for enterprise customers](/rest/api/billing/enterprise/billing-enterprise-api-reserved-instance-charges) (Ottenere le tariffe di transazione di istanza riservata per i clienti Enterprise).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle prenotazioni di Azure, vedere gli articoli seguenti:

- [Quali sono le prenotazioni per Azure?](billing-save-compute-costs-reservations.md)
- [Gestire le prenotazioni per Azure](billing-manage-reserved-vm-instance.md)

Acquista un piano di servizio:

- [Pagare in anticipo la capacità riservata di Azure Cosmos DB](../cosmos-db/cosmos-db-reserved-capacity.md)
- [Pagare in anticipo le risorse di calcolo del database SQL con capacità riservata del database SQL di Azure](../sql-database/sql-database-reserved-capacity.md)
- [Pagare in anticipo le macchine virtuali tramite le istanze di macchina virtuale riservate di Azure](../virtual-machines/windows/prepay-reserved-vm-instances.md)

Acquista un piano software:

- [Pagare in anticipo per i piani software Red Hat dalle prenotazioni di Azure](../virtual-machines/linux/prepay-rhel-software-charges.md)
- [Pagare in anticipo per i piani software SUSE dalle prenotazioni di Azure](../virtual-machines/linux/prepay-suse-software-charges.md)

Informazioni su utilizzo:

- [Informazioni sull'utilizzo della prenotazione per la sottoscrizione con pagamento in base al consumo](billing-understand-reserved-instance-usage.md)
- [Informazioni sull'utilizzo della prenotazione per l'iscrizione Enterprise](billing-understand-reserved-instance-usage-ea.md)
- [Informazioni sull'utilizzo della prenotazione per sottoscrizioni CSP](https://docs.microsoft.com/partner-center/azure-reservations)

## <a name="need-help-contact-us"></a>Richiesta di assistenza Contatti

Se si hanno domande o assistenza, [creare una richiesta di supporto](https://go.microsoft.com/fwlink/?linkid=2083458).
