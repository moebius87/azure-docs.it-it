---
title: Esempi e scenari comuni- App per la logica di Azure | Microsoft Docs
description: Esempi, scenari comuni, esercitazioni e procedure dettagliate per le app per la logica di Azure
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.topic: article
ms.assetid: e06311bc-29eb-49df-9273-1f05bbb2395c
ms.date: 01/31/2018
ms.openlocfilehash: 89e0294db3178cedd3b14aada0b505787b17c75e
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60303690"
---
# <a name="common-scenarios-examples-tutorials-and-walkthroughs-for-azure-logic-apps"></a>Scenari comuni, esempi, esercitazioni e procedure dettagliate per le app per la logica di Azure

[Le app per la logica di Azure](../logic-apps/logic-apps-overview.md) consentono di orchestrare e integrare servizi diversi fornendo [connettori pronti all'uso da 100+](../connectors/apis-list.md), andando dal Server SQL o SAP in locale ai servizi cognitivi Microsoft. Il servizio delle App per la logica è "senza server", quindi non è necessario preoccuparsi per la scala o le istanze. È necessario solo definire il flusso di lavoro con un trigger e le azioni eseguite dal flusso di lavoro. La piattaforma sottostante gestisce scalabilità, disponibilità e prestazioni. Le app per la logica sono particolarmente utili per i casi d'uso e gli scenari in cui è necessario coordinare più azioni tra più sistemi.

Per fornire maggiori informazioni sui numerosi modelli e sulle funzionalità supportate dalle [app per la logica di Azure](../logic-apps/logic-apps-overview.md), di seguito sono elencati alcuni esempi e scenari comuni.

## <a name="popular-starting-points-for-logic-app-workflows"></a>Punti iniziali generali per i flussi di lavoro dell'app per la logica

Ogni app per la logica inizia con un [*trigger*](../logic-apps/logic-apps-overview.md#logic-app-concepts) e un solo trigger, che avvia il flusso di lavoro dell'app per la logica e passa tutti i dati come parte del trigger. Alcuni connettori forniscono trigger, che sono disponibili sotto questi tipi:

* *Trigger di polling*: Controlla periodicamente un endpoint del servizio per i nuovi dati. In presenza di nuovi dati, il trigger crea ed esegue una nuova istanza del flusso di lavoro con i dati come input.

* *Trigger di push*: È in attesa di dati a un endpoint del servizio e attende fino a quando non si verifica un evento specifico. Quando si verifica l'evento, il trigger viene attivato immediatamente, creando ed eseguendo una nuova istanza del flusso di lavoro che usa tutti i dati disponibili come input.

Ecco alcuni esempi comuni di trigger:

* Polling: 

  * [**Pianificazione - ricorrenza** trigger](../connectors/connectors-native-recurrence.md) consente di impostare la data di inizio, l'ora e la ricorrenza per l'attivazione dell'app per la logica. 
  Ad esempio, è possibile selezionare i giorni della settimana e le ore del giorno per l'attivazione dell'app per la logica.

  * Il trigger "Quando viene ricevuto un messaggio di posta elettronica" consente all'app per la logica di verificare i nuovi messaggi di posta elettronica da qualsiasi provider di posta elettronica supportato dalle App per la logica, ad esempio, [Outlook di Office 365](../connectors/connectors-create-api-office365-outlook.md), [Gmail](https://docs.microsoft.com/connectors/gmail/), [Outlook.com](https://docs.microsoft.com/connectors/outlook/) e così via.

  * Il [**trigger** HTTP](../connectors/connectors-native-http.md) consente all'app per la logica di verificare un endpoint del servizio specifico comunicando su HTTP.
  
* Push:

  * Il [**trigger** Richiesta/Risposta - Richiesta](../connectors/connectors-native-reqres.md) consente all'app per la logica di ricevere richieste HTTP e di rispondere in qualche modo in tempo reale agli eventi.

  * Il [**trigger** HTTP Webhook](../connectors/connectors-native-webhook.md) è sottoscritto a un endpoint del servizio registrando un *URL di callback* con tale servizio. 
  In questo modo, il servizio può solo notificare il trigger quando si verifica l'evento specificato, in modo che il trigger non ha bisogno di eseguire il polling del servizio.

Dopo aver ricevuto una notifica riguardante i nuovi dati o un evento, il trigger viene attivato, crea una nuova istanza di flusso di lavoro dell'app per la logica ed esegue le azioni nel flusso di lavoro. È possibile accedere a tutti i dati dal trigger in tutto il flusso di lavoro. Ad esempio, il trigger "In un nuovo tweet" passa il contenuto del tweet nell'esecuzione dell'app per la logica. 

## <a name="respond-to-triggers-and-extend-actions"></a>Rispondere ai trigger ed estendere le azioni

Per i sistemi e i servizi che non potrebbero non avere connettori pubblicati, è anche possibile estendere le app per la logica.

* [Creare trigger o azioni personalizzate](../logic-apps/logic-apps-create-api-app.md)
* [Configurare azioni con esecuzione prolungata per l'esecuzione dei flussi di lavoro](../logic-apps/logic-apps-create-api-app.md)
* [Rispondere ad azioni ed eventi esterni con webhook](../logic-apps/logic-apps-create-api-app.md)
* [Chiamare, attivare o annidare flussi di lavoro con risposte sincrone alle richieste HTTP](../logic-apps/logic-apps-http-endpoint.md)
* [Esercitazione: Creare un dashboard social basato su intelligenza artificiale in pochi minuti con App per la logica e Power BI](https://aka.ms/logicappsdemo)
* [Video: Rispondere ai webhook SMS di Twilio e inviare una risposta di testo](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-Logic-Apps-Walkthrough-Webhook-Functions-and-an-SMS-Bot)

## <a name="control-flow-error-handling-and-logging-capabilities"></a>Flusso di controllo, gestione degli errori e funzionalità di registrazione

Le app per la logica includono funzionalità sofisticate per il flusso di controllo avanzato, come condizioni, istruzioni switch, cicli e ambiti. Per garantire soluzioni resilienti, è anche possibile implementare la gestione degli errori e delle eccezioni nei flussi di lavoro. Per i log di notifica e di diagnostica per lo stato di esecuzione dei flussi di lavoro, le app per la logica di Azure forniscono inoltre monitoraggio e avvisi.

* Eseguire azioni diverse in base alle [istruzioni condizionali](../logic-apps/logic-apps-control-flow-conditional-statement.md) e alle [istruzioni switch](../logic-apps/logic-apps-control-flow-switch-statement.md)
* [Ripetere passaggi o elementi del processo in matrici e raccolte con cicli](../logic-apps/logic-apps-control-flow-loops.md)
* [Raggruppare le azioni con gli ambiti](../logic-apps/logic-apps-control-flow-run-steps-group-scopes.md)
* [Creare la gestione degli errori e delle eccezioni in un flusso di lavoro](../logic-apps/logic-apps-exception-handling.md)
* [Caso d'uso: Modo in cui un'organizzazione sanitaria utilizza per la logica app gestione delle eccezioni per i flussi di lavoro HL7 FHIR](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [Attivare il monitoraggio, la registrazione e gli avvisi per le app per la logica esistenti](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Abilitare il monitoraggio e la registrazione diagnostica durante la creazione di app per la logica](../logic-apps/logic-apps-monitor-your-logic-apps-oms.md)

## <a name="deploy-and-manage-logic-apps"></a>Distribuire e gestire app per la logica

È possibile sviluppare e distribuire interamente app per la logica con Visual Studio, Azure DevOps o qualsiasi altro strumento di controllo del codice sorgente e compilazione automatica. Per supportare la distribuzione per i flussi di lavoro e le connessioni dipendenti in un modello di risorse, le app per la logica usano i modelli di distribuzione delle risorse di Azure. Gli strumenti di Visual Studio generano automaticamente questi modelli, che è possibile archiviare per il controllo del codice sorgente finalizzato al controllo delle versioni.

* [Creare e distribuire app per la logica con Visual Studio](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md)
* [Attivare il monitoraggio, la registrazione e gli avvisi per le app per la logica esistenti](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Creare un modello di distribuzione automatizzato](../logic-apps/logic-apps-create-deploy-template.md)

## <a name="content-types-conversions-and-transformations-within-a-run"></a>Tipi di contenuto, conversioni e trasformazioni durante un'esecuzione

È possibile accedere, convertire e trasformare più tipi di contenuto usando le numerose funzioni del [linguaggio di definizione del flusso di lavoro](https://aka.ms/logicappsdocs) delle app per la logica di Azure. Ad esempio, è possibile eseguire la conversione tra una stringa, il formato JSON e il formato XML con le espressioni del flusso di lavoro `@json()` e `@xml()`. Il motore delle app per la logica mantiene i tipi di contenuto per supportare il trasferimento del contenuto senza perdita di dati tra i servizi.

* [Funzionamento delle espressioni del flusso di lavoro nelle app per la logica](../logic-apps/logic-apps-author-definitions.md)
* [Gestire i tipi di contenuto non JSON](../logic-apps/logic-apps-content-type.md), come `application/xml`, `application/octet-stream` e `multipart/formdata`
* [Schema del linguaggio di definizione del flusso di lavoro per App per la logica di Azure](https://aka.ms/logicappsdocs)

## <a name="other-integrations-and-capabilities"></a>Altre integrazioni e funzionalità

Le app per la logica offrono inoltre l'integrazione con molti servizi, come Funzioni di Azure, Gestione API di Azure, Servizi app di Azure e gli endpoint HTTP personalizzati, ad esempio REST e SOAP.

* [Create a real-time social dashboard with Azure Serverless](../logic-apps/logic-apps-scenario-social-serverless.md) (Creare un dashboard di social networking in tempo reale senza server di Azure)
* [Chiamare Funzioni di Azure da app per la logica](../logic-apps/logic-apps-azure-functions.md)
* [Esercitazione: Trigger di App per la logica con funzioni di Azure](../logic-apps/logic-apps-scenario-function-sb-trigger.md)
* [Esercitazione: Monitorare le modifiche alla macchina virtuale con griglia di eventi di Azure e App per la logica](../event-grid/monitor-virtual-machine-changes-event-grid-logic-app.md)
* [Esercitazione: Creare una funzione che si integra con App per la logica di Azure e servizi cognitivi Microsoft per analizzare i sentiment nei post di Twitter](../azure-functions/functions-twitter-email.md)
* [Esercitazione: Monitoraggio remoto IoT e notifiche con App per la logica di Azure ci si connette all'hub IoT e cassetta postale](../iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps.md)
* [Blog: Chiamare gli endpoint SOAP da App per la logica](https://blogs.msdn.microsoft.com/logicapps/2016/04/07/using-soap-services-with-logic-apps/)

## <a name="end-to-end-scenarios"></a>Scenari end-to-end

* [White paper: Integrazione di gestione dei casi end-to-end con servizi di Azure, ad esempio App per la logica](https://aka.ms/enterprise-integration-e2e-case-management-utilities-logic-apps)

## <a name="customer-stories"></a>Casi di successo dei clienti

Informazioni su come App per la logica di Azure, con altri servizi di Azure e prodotti Microsoft, ha consentito a [queste società](https://aka.ms/logic-apps-customer-stories) di migliorare la flessibilità e di concentrarsi sulle principali attività commerciali semplificando, organizzando, automatizzando e orchestrando processi complessi.

## <a name="next-steps"></a>Passaggi successivi

* [Compilare in base alle definizioni di app per la logica con JSON](../logic-apps/logic-apps-author-definitions.md)
* [Gestire errori ed eccezioni nelle app per la logica](../logic-apps/logic-apps-exception-handling.md)
* [Inviare domande, commenti o suggerimenti su come migliorare le app per la logica di Azure](https://feedback.azure.com/forums/287593-logic-apps)
