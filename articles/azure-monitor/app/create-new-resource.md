---
title: Creare una nuova risorsa di Azure Application Insights | Microsoft Docs
description: Impostare manualmente il monitoraggio di Application Insights per una nuova applicazione live.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.topic: conceptual
ms.date: 12/02/2016
ms.author: mbullwin
ms.openlocfilehash: 5daf0944212dc4b8040a39e6efbf5bb25f7f39f0
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60901798"
---
# <a name="create-an-application-insights-resource"></a>Creare una risorsa di Application Insights
Application Insights di Azure visualizza dati relativi all'applicazione in una *risorsa* di Microsoft Azure. La creazione di una nuova risorsa fa dunque parte della [configurazione di Application Insights per monitorare una nuova applicazione][start]. In molti casi, la creazione di una risorsa può essere eseguita automaticamente dall'IDE. In alcuni casi si crea tuttavia una risorsa manualmente, ad esempio per disporre di risorse separate per le compilazioni di sviluppo e produzione dell'applicazione.

Dopo aver creato la risorsa, si ottiene la relativa chiave di strumentazione, che consente di configurare l'SDK nell'applicazione. La chiave della risorsa collega i dati di telemetria alla risorsa.

## <a name="sign-up-to-microsoft-azure"></a>Iscriversi a Microsoft Azure
Se non si ha ancora un [account Microsoft, è possibile ottenerne uno ora](https://live.com). (se si usano servizi come Outlook.com, OneDrive, Windows Phone o XBox Live, si ha già un account Microsoft).

È necessaria anche una sottoscrizione di [Microsoft Azure](https://azure.com). Se il team o l'organizzazione ha una sottoscrizione di Azure, il proprietario potrà aggiungere l'utente alla sottoscrizione usando Windows Live ID. Si paga solo l'uso effettivo. Il piano Basic predefinito consente di accedere a un certo uso sperimentale gratuito.

Dopo aver ottenuto una sottoscrizione, accedere ad Application Insights all'indirizzo [https://portal.azure.com](https://portal.azure.com) e usare il proprio Live ID.

## <a name="create-an-application-insights-resource"></a>Creare una risorsa di Application Insights
In [portal.azure.com](https://portal.azure.com)aggiungere una nuova risorsa di Application Insights:

![Fare clic su Nuovo, Application Insights](./media/create-new-resource/01-new.png)

* Il **tipo di applicazione** influisce sul contenuto del pannello Panoramica e sulle proprietà disponibili in [Esplora metriche][metrics]. Se il tipo dell'app non è visualizzato, scegliere Generale.
* **sottoscrizione** è il proprio account di pagamento in Azure.
* **gruppo di risorse** è utile per gestire le proprietà come il controllo di accesso. Se sono già state create altre risorse di Azure, è possibile inserire questa nuova risorsa nello stesso gruppo.
* Il **percorso** è la posizione in cui vengono conservati i dati.
* **Aggiungi al dashboard** inserisce un riquadro di accesso rapido alla risorsa nella home page di Azure. Consigliato.

Dopo aver creato l'app, verrà visualizzato un nuovo pannello che mostra i dati sulle prestazioni e l'utilizzo dell'app. 

Per visualizzare di nuovo questo pannello al successivo accesso ad Azure, cercare il riquadro di avvio rapido dell'app nella schermata iniziale. In alternativa, fare clic su Sfoglia per cercarlo.

## <a name="copy-the-instrumentation-key"></a>Eseguire una copia della chiave di strumentazione
La chiave di strumentazione identifica la risorsa creata. È necessario fornirla all'SDK.

![Fare clic su Informazioni di base, quindi sulla chiave di strumentazione e infine premere CTRL+C.](./media/create-new-resource/02-props.png)

## <a name="install-the-sdk-in-your-app"></a>Installare l’SDK nell'app
Installare Application Insights SDK nell'app. Questo passaggio dipende dal tipo di applicazione. 

Usare la chiave di strumentazione per configurare l'[SDK installato nell'applicazione][start].

L'SDK include i moduli standard che inviano dati di telemetria senza che occorra scrivere codice. Per rilevare le azioni degli utenti o diagnosticare i problemi in modo più dettagliato, [usare l'API][api] per inviare dati di telemetria personalizzati.

## <a name="monitor"></a>Visualizzare i dati di telemetria
Chiudere il pannello di avvio rapido per tornare al pannello dell'applicazione nel portale di Azure.

Fare clic sul riquadro Cerca per vedere [Diagnostic Search][diagnostic] (Ricerca diagnostica), ovvero la finestra in cui vengono visualizzati i primi eventi. 

Se si prevedono più dati, fare clic su **Aggiorna** dopo pochi secondi.

## <a name="creating-a-resource-automatically"></a>Creazione automatica di una risorsa
È possibile scrivere uno [script di PowerShell](../../azure-monitor/app/powershell.md) per creare automaticamente una risorsa.

## <a name="next-steps"></a>Passaggi successivi
* [Creare un dashboard](../../azure-monitor/app/app-insights-dashboards.md)
* [Ricerca diagnostica](../../azure-monitor/app/diagnostic-search.md)
* [Esplorare le metriche](../../azure-monitor/app/metrics-explorer.md)
* [Scrivere query di Analisi](../../azure-monitor/app/analytics.md)

<!--Link references-->

[api]: ../../azure-monitor/app/api-custom-events-metrics.md
[diagnostic]: ../../azure-monitor/app/diagnostic-search.md
[metrics]: ../../azure-monitor/app/metrics-explorer.md
[start]: ../../azure-monitor/app/app-insights-overview.md

