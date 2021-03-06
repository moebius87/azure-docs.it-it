---
title: Cos'è Azure Active Directory Identity Protection (aggiornato)? | Microsoft Docs
description: Cos'è Azure Active Directory Identity Protection (aggiornato)?
services: active-directory
keywords: azure active directory identity protection, cloud app discovery, gestione applicazioni, sicurezza, rischio, livello di rischio, vulnerabilità, criteri di sicurezza
documentationcenter: ''
author: MicrosoftGuyJFlo
manager: mtillman
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.subservice: identity-protection
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2018
ms.author: joflore
ms.reviewer: sahandle
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1d533e6aac9ae1a486d018414a86a9dc3fe742c2
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60294286"
---
# <a name="what-is-azure-active-directory-identity-protection-refreshed"></a>Cos'è Azure Active Directory Identity Protection (aggiornato)?

L'esperienza di Identity Protection è stata aggiornata per migliorare la protezione delle identità dell'organizzazione. L’esperienza aggiornata offre:

- Nuovo approccio all’amministrazione, incentrato sui rischi che interessano maggiormente l’utente: il rischio utente e il rischio di accesso

- Potenti funzionalità di indagine con supporto per opzioni di filtro, ordinamento e download intelligenti

- Miglioramento del calcolo del rischio utente per assegnare la priorità agli interventi verso gli utenti con probabilità di compromissione più elevata

- Supporto di una nuova API per abilitare l'accesso a livello di codice ai dati sui rischi

- Processo di feedback di amministrazione semplificato, che consente di proteggere immediatamente gli utenti

- Nuova funzionalità di apprendimento automatico con supervisione per migliorare l'accuratezza delle valutazioni dei rischi



La sicurezza è una priorità assoluta per le organizzazioni di oggi. La maggior parte delle violazioni della sicurezza si verifica quando utenti malintenzionati ottengono l'accesso a un ambiente impadronendosi dell'identità di un utente. Nel corso degli anni gli utenti malintenzionati hanno messo a punto tecniche sempre più efficaci per sfruttare le violazioni di terze parti e sferrare sofisticati attacchi di phishing. L'accesso a un account utente, anche quelli con privilegi limitati, permette agli utenti malintenzionati di accedere immediatamente a risorse aziendali importanti in modo piuttosto semplice tramite il movimento laterale. 

Per rispondere a queste minacce, Azure AD Identity Protection consente di: 

- Impedire in modo proattivo l'uso improprio delle identità compromesse 

- Contenere automaticamente i rischi quando viene rilevata un'attività sospetta 

- Analizzare gli utenti e gli accessi a rischio per risolvere potenziali vulnerabilità  

- Essere avvisati qualora il rischio di un utente raggiunge una soglia specificata 

 

Azure AD Identity Protection è una funzionalità di Azure Active Directory Premium P2 che consente di configurare i criteri per rispondere automaticamente quando viene compromessa l'identità di un utente o quando un utente diverso dal proprietario dell'account sta tentando di accedere usando l’identità di quest’ultimo. Questi criteri, con altri controlli di accesso condizionale forniti da Azure AD, possono eseguire il blocco automatico dell’accesso o avviare azioni di mitigazione, come la reimpostazione della password o l'applicazione dell'autenticazione a più fattori. Inoltre, Identity Protection offre funzionalità di monitoraggio e creazione di report per ottenere informazioni più approfondite sui rischi e sulle potenziali compromissioni all'interno dell'organizzazione. 

>[!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RWsS6Q]


## <a name="risk-events"></a>Eventi di rischio

Azure AD Identity Protection rileva gli eventi di rischio seguenti: 

 

| Tipo di evento di rischio | DESCRIZIONE | Tipo di rilevamento |
| ---             | ---         | ---            |
| Trasferimento atipico | Accesso da una posizione insolita in base agli accessi recenti dell'utente. | Offline |
| Indirizzo IP anonimo | Accesso da indirizzo IP anonimo (ad esempio Tor Browser, VPN per navigazione in anonimato). | Tempo reale |
| Proprietà di accesso insolite | Accesso con proprietà non osservate di recente per l'utente specificato. | Tempo reale |
| Indirizzo IP collegato a malware | Accesso da indirizzo IP collegato a malware | Offline |
| Credenziali perse | Questo evento di rischio indica che le credenziali valide dell'utente sono andate perse | Offline |





## <a name="types-of-risk"></a>Tipi di rischio 

Identity Protection si basa su due tipi di rischio:

- Rischio di accesso

- Rischio utente

### <a name="sign-in-risk"></a>Rischio di accesso

Un rischio di accesso rappresenta la probabilità che una richiesta di autenticazione specificata non sia stata autorizzata dal proprietario dell'identità.

Esistono due valutazioni del rischio di accesso: 

- **Rischio di accesso (in tempo reale)** - Il rischio di accesso (in tempo reale) si basa su tutti i rilevamenti in tempo reale che si attivano durante l'elaborazione dell’accesso.  

- **Rischio di accesso (aggregazione)** - Il rischio di accesso (aggregazione) è il rischio complessivo di un accesso. Viene calcolato tramite un modello di machine learning che prende in considerazione:

    - Rilevamenti in tempo reale (descritti in precedenza)
    
    - Rilevamenti offline (che vengono generati dopo l’esecuzione dell'accesso) 
    
    - Tutte le altre funzionalità dell’accesso


### <a name="user-risk"></a>Rischio utente

Un rischio utente rappresenta la probabilità che un'identità specificata sia compromesso. 

Il rischio utente viene calcolato considerando tutti i rischi associati all'utente:

- Tutti gli accessi a rischio
- Tutti gli eventi di rischio non collegati a un accesso
- Il rischio utente corrente
- Eventuali azioni di correzione o rimozione dei rischi eseguite per l'utente fino alla data corrente



## <a name="how-identity-protection-detects-risk"></a>Rilevamento del rischio in Identity Protection  

Azure AD usa l’apprendimento automatico per rilevare anomalie ed eventuali attività sospette, sfruttando sia i segnali rilevati in tempo reale durante gli accessi, sia quelli non in tempo reale correlati agli utenti e alle loro attività di accesso. Usando questi dati, Identity Protection calcola un rischio di accesso in tempo reale ogni volta che un utente esegue l'autenticazione, oltre a determinare un livello di rischio utente complessivo per ogni utente. Identity Protection consente di eseguire azioni automatiche sui rilevamenti di rischio tramite la configurazione dei criteri per rischi utente e rischi di accesso.  

 

Per capire come Identity Protection rileva i rischi, è necessario spiegare due concetti importanti: rischio utente e rischio di accesso. Un rischio di accesso rappresenta la probabilità che una richiesta di autenticazione specificata non sia stata autorizzata dal proprietario dell'identità. Esistono due tipi di rischi di accesso: in tempo reale e totale. Il rischio di accesso in tempo reale viene rilevato durante il tentativo di accesso specificato (ad esempio, accessi da indirizzi IP anonimi). Il rischio di accesso totale è l'aggregazione dei rischi di accesso in tempo reale rilevati oltre a eventuali eventi di rischio non in tempo reale successivi associati agli accessi dell'utente (ad esempio comunicazione impossibile). Il rischio utente rappresenta la probabilità complessiva che una determinata identità sia stata compromessa da un utente malintenzionato. Il rischio utente contiene tutte le attività di rischio per un determinato utente, tra cui:

- Rischio di accesso in tempo reale
- Rischi di accesso successivi
- Rilevamenti di utenti a rischio.   

 

 
 ![Flusso](./media/overview-v2/01.png)
 

 

Il flusso di base per il rilevamento dei rischi e la risposta di Identity Protection in relazione a qualsiasi accesso specificato è riepilogato nella figura precedente.  

 

 

 

## <a name="common-scenarios"></a>Scenari comuni 

Esaminiamo l'esempio di Sarah, dipendente di Contoso. 

1. Sarah tenta di accedere a Exchange Online da Tor Browser. Al momento dell'accesso, Azure AD rileva gli eventi di rischio in tempo reale. 

2. Azure AD rileva che Sarah esegue l'accesso da un indirizzo IP anonimo, attivando un livello di rischio di accesso medio. 

3. Sarah visualizza una richiesta di verifica tramite prompt di autenticazione a più fattori (MFA), perché l’amministratore IT di Contoso ha configurato i criteri di accesso condizionale per il rischio di accesso di Identity Protection. I criteri richiedono l'autenticazione a più fattori per un rischio di accesso di livello medio o superiore. 

4. Sarah supera la richiesta di autenticazione a più fattori e accede a Exchange Online, con un livello di rischio utente inalterato. 

Cosa è successo dietro le quinte? Il tentativo di accesso da Tor Browser ha attivato un rischio di accesso in tempo reale in Azure AD per l'indirizzo IP anonimo. Durante l’elaborazione della richiesta, Azure AD ha applicato il criterio di rischio di accesso configurato in Identity Protection poiché il livello di rischio di accesso di Sarah corrispondeva alla soglia (Medio). Poiché Sarah aveva in precedenza effettuato la registrazione per l’autenticazione a più fattori, è stata in grado di rispondere e di superare la richiesta di verifica MFA. La sua capacità di superare correttamente la verifica MFA ha segnalato ad Azure AD che probabilmente si trattava del legittimo proprietario dell’identità e quindi il suo livello di rischio utente non aumenta. 


Ma cosa sarebbe successo se Sara non fosse stata l’utente che tentava di accedere? 

1. Un utente malintenzionato con le credenziali di Sarah teta di accedere all’account Exchange Online di Sarah da Tor Browser, poiché desidera nascondere il proprio indirizzo IP. 

2. Azure AD rileva che il tentativo di accesso avviene da un indirizzo IP anonimo, attivando un rischio di accesso in tempo reale. 

3. L’utente malintenzionato visualizza una richiesta di verifica tramite prompt di autenticazione a più fattori (MFA), perché l’amministratore IT di Contoso ha configurato i criteri di accesso condizionale per il rischio di accesso di Identity Protection in modo richiedere l’autenticazione a più fattori quando il rischio di accesso è medio o superiore. 

4. L'attore malintenzionato non riesce a superare la richiesta di verifica MFA e non può accedere all'account Exchange Online di Sarah. 

5. Il prompt MFA non superato ha attivato la registrazione di un evento di rischio, aumentando il rischio utente di Sarah per gli accessi futuri. 

Ora che un utente malintenzionato ha provato ad accedere all'account di Sarah, vediamo cosa accade nel momento del successivo tentativo di accesso di Sarah. 

1. Sarah tenta di accedere a Exchange Online da Outlook. Al momento dell'accesso, Azure AD rileva gli eventi di rischio in tempo reale, nonché qualsiasi rischio utente precedente. 

2. Azure AD non rileva alcun rischio di accesso in tempo reale, ma un rischio utente più elevato dovuto all’attività rischiosa degli scenari precedenti.  

3. Sarah visualizzata una richiesta di verifica tramite prompt di reimpostazione della password, perché l’amministratore IT di Contoso ha configurato i criteri di rischio utente di Identity Protection affinché sia richiesta la modifica della password all'accesso di un utente ad alto rischio. 

4. Poiché Sarah ha effettuato la registrazione per la reimpostazione della password self-service e l’autenticazione a più fattori, può reimpostare correttamente la propria password. 

5. Reimpostando la password, le credenziali di Sarah non sono più compromesse e la sua identità torna in uno stato sicuro. 

6. Gli eventi di rischio precedenti di Sarah vengono risolti e il suo livello di rischio utente viene reimpostato automaticamente in risposta all’attenuazione del rischio di compromissione delle credenziali. 

## <a name="how-do-i-configure-identity-protection"></a>Come si configura Identity Protection? 

Per iniziare a usare Identity Protection, per prima cosa è necessario configurare i criteri di rischio utente e di rischio di accesso. Una volta configurati questi criteri e applicati a un gruppo di test, è possibile simulare eventi di rischio per comprendere la risposta di Identity Protection nell'ambiente in uso. Le guide di avvio rapido seguenti offrono una procedura dettagliata su come configurare i criteri indicati in precedenza ed effettuarne il test nel proprio ambiente. 

 

Identity Protection supporta 3 ruoli in Azure AD per bilanciare le attività di gestione nella distribuzione: 

| Ruolo | Operazione consentita | Operazione non consentita |
| --- | --- | --- |
| Amministratore globale | Accesso completo a Identity Protection, implementazione di Identity Protection | |
| Amministratore della sicurezza | Accesso completo a Identity Protection | Implementazione di Identity Protection, reimpostazione delle password per un utente |
| Ruolo con autorizzazioni di lettura per la sicurezza | Accesso in sola lettura a Identity Protection | Implementazione di Identity Protection, correzione degli utenti, configurazione dei criteri, reimpostazione delle password| 

Per altri dettagli, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](../users-groups-roles/directory-assign-admin-roles.md)

 
## <a name="licensing"></a>Licenze

>[!NOTE]
> Durante l'anteprima pubblica di Identity Protection (aggiornato), solo i clienti di Azure AD Premium P2 avranno accesso ai report degli utenti a rischio e degli accessi a rischio.



| Funzionalità | Azure AD P2 Premium | Azure AD Premium P1 | Azure AD Basic/Gratuito |
| --- | --- | --- | --- |
| Criteri di rischio utente | Sì | No  | No  |
| Criteri di rischio di accesso | Sì | No  | No  |
| Report utenti a rischio | Accesso completo | Informazioni limitate | Informazioni limitate |
| Report sugli accessi a rischio | Accesso completo | Informazioni limitate | Informazioni limitate |
| Criteri di registrazione MFA | Sì | No  | No  |







## <a name="next-steps"></a>Passaggi successivi 

Per iniziare a usare Identity Protection, vedere [Configurare i criteri di rischio di accesso](quickstart-sign-in-risk-policy.md). 






