---
title: Come usare l'accesso alle applicazioni self-service | Microsoft Docs
description: Abilitare l'accesso alle applicazioni self-service per consentire agli utenti di trovare le proprie applicazioni
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: celested
ms.reviewer: japere,asteen
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3afe915f4fa1d9c1c36860d23912ac0e01088724
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60294039"
---
# <a name="how-to-use-self-service-application-access"></a>Come usare l'accesso alle applicazioni self-service

Prima che gli utenti possano da soli individuare le applicazioni dal pannello di accesso, è necessario abilitare l'**accesso alle applicazioni self-service** per tutte le applicazioni per cui si desidera consentire l'individuazione e l'accesso da parte degli utenti.

Questa funzionalità è un modo efficace per consentire di risparmiare tempo e denaro al gruppo IT ed è altamente consigliata come parte di una distribuzione moderna di applicazioni con Azure Active Directory.

Questa funzionalità permette di:

-   Consentire agli utenti di individuare da soli le applicazioni dal [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) senza dover contattare il gruppo IT.

-   Aggiungere gli utenti a un gruppo pre-configurato in modo che sia possibile verificare chi ha richiesto l'accesso, rimuovere l'accesso e gestire i ruoli assegnati.

-   Facoltativamente, consentire al revisore aziendale di approvare l'accesso alle applicazioni in modo da rimuovere questa azione dalle operazioni del gruppo IT.

-   Facoltativamente, configurare un massimo di 10 persone che possono approvare l'accesso a questa applicazione.

-   Facoltativamente consentire al revisore aziendale di impostare le password usate dagli utenti per accedere all'applicazione, direttamente dal [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) del revisore aziendale.

-   Facoltativamente, assegnare automaticamente gli utenti dell'accesso self-service direttamente a un ruolo applicazione.

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a>Abilitare l'accesso alle applicazioni self-service per consentire agli utenti di trovare le proprie applicazioni

L'accesso alle applicazioni self-service è un modo efficace per consentire agli utenti di individuare da soli le applicazioni e, facoltativamente, al gruppo aziendale di approvare l'accesso a tali applicazioni. È possibile consentire al gruppo aziendale di gestire le credenziali assegnate agli utenti per il diritto di accesso alle applicazioni Single Sign-On tramite password dal pannello di accesso.

Per abilitare l'accesso self-service per un'applicazione, seguire questa procedura:

1. Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.

2. Aprire l'**estensione Azure Active Directory** facendo clic su **Tutti i servizi** nella parte superiore del menu di spostamento principale a sinistra.

3. Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.

4. Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.

5. Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.

   * Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.

6. Selezionare l'applicazione per cui si desidera abilitare l'accesso self-service dall'elenco.

7. Dopo il caricamento dell'applicazione, fare clic su **Self-service** nel menu di navigazione a sinistra dell'applicazione.

8. Per abilitare l'accesso self-service per questa applicazione, impostare l'opzione **Consentire agli utenti di richiedere l'accesso a questa applicazione?** su **Sì**.

9. Successivamente, per selezionare il gruppo al quale devono essere aggiunti gli utenti che richiedono l'accesso a questa applicazione, fare clic sul selettore accanto all'etichetta **Gruppo a cui devono essere aggiunti gli utenti assegnati** e selezionare un gruppo.

10. **Facoltativo:** se si vuole richiedere un'approvazione aziendale prima che venga consentito l'accesso agli utenti, impostare l'opzione **Richiedere l'approvazione prima di concedere l'accesso a questa applicazione?** su **Sì**.

11. **Facoltativo: per le applicazioni che usano solo l'accesso Single Sign-On tramite password,** se si vuole consentire ai responsabili approvazione aziendali di specificare le password inviate a questa applicazione per gli utenti approvati, impostare l'opzione **Consentire ai responsabili approvazione di impostare le password utente per questa applicazione?** su **Sì**.

12. **Facoltativo:** per specificare i responsabili approvazione aziendali che possono approvare l'accesso a questa applicazione, fare clic sul selettore accanto all'etichetta **Utenti autorizzati ad approvare l'accesso a questa applicazione** per selezionare fino a 10 singoli responsabili approvazione aziendali.

    * I gruppi non sono supportati.

13. **Facoltativo:** **per le applicazioni che espongono ruoli**, se si vuole assegnare un ruolo agli utenti approvati self-service, fare clic sul selettore accanto all'opzione **A quale ruolo è necessario assegnare gli utenti in questa applicazione?** per selezionare il ruolo cui devono essere assegnati questi utenti.

14. Per terminare, fare clic sul pulsante **Salva** nella parte superiore del pannello.

Dopo aver completato la configurazione dell'applicazione self-service, gli utenti possono accedere al [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) e fare clic sul pulsante **+Aggiungi** per trovare le app per cui è stato abilitato l'accesso self-service. Anche i responsabili approvazione aziendali visualizzano una notifica nel loro [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/). È possibile abilitare un messaggio di posta elettronica per informare i responsabili dell'approvazione quando un utente richiede l'accesso a un'applicazione per cui è necessaria l'approvazione. 

Tali approvazioni supportano solo flussi di lavoro di approvazione individuali. Se si specificano pertanto più responsabili approvazione, uno qualsiasi di essi potrà approvare l'accesso all'applicazione.

## <a name="next-steps"></a>Passaggi successivi
[Configurazione di Azure Active Directory per la gestione self-service dei gruppi](../users-groups-roles/groups-self-service-management.md)
