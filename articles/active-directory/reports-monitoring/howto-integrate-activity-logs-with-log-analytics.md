---
title: Stream i log di Azure Active Directory per i log di monitoraggio di Azure | Microsoft Docs
description: Descrive come integrare i log di Azure Active Directory con i log di monitoraggio di Azure
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: daveba
editor: ''
ms.assetid: 2c3db9a8-50fa-475a-97d8-f31082af6593
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.subservice: report-monitor
ms.date: 04/18/2019
ms.author: markvi
ms.reviewer: dhanyahk
ms.collection: M365-identity-device-management
ms.openlocfilehash: 213fb6e73ae2fc4314320d0e3e593632d8eb7f85
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60437313"
---
# <a name="integrate-azure-ad-logs-with-azure-monitor-logs"></a>Integrare i log di Azure AD con i log di monitoraggio di Azure

[!INCLUDE [azure-monitor-log-analytics-rebrand](../../../includes/azure-monitor-log-analytics-rebrand.md)]

I log di Monitoraggio di Azure consentono di eseguire query sui dati per trovare eventi specifici, analizzare le tendenze ed eseguire la correlazione su varie origini dati. L'integrazione dei log attività di Azure AD nei log di Monitoraggio di Azure consente ora di eseguire attività quali:

 * Confrontare i log di accesso di Azure AD con i log di sicurezza pubblicati dal Centro sicurezza di Azure

 * Risolvere i problemi di colli di bottiglia delle prestazioni nella pagina di accesso dell'applicazione tramite la correlazione dei dati sulle prestazioni delle applicazioni da Azure Application Insights.  

Il video seguente di una sessione di Ignite illustra i vantaggi derivanti dall'utilizzo dei log di Monitoraggio di Azure per i log di Azure AD in scenari utente pratici.

> [!VIDEO https://www.youtube.com/embed/MP5IaCTwkQg?start=1894]

Questo articolo illustra come integrare i log di Azure Active Directory (Azure AD) con Monitoraggio di Azure.

## <a name="supported-reports"></a>Report supportati

È possibile indirizzare i log attività di controllo e i log attività di accesso ai log di Monitoraggio di Azure per ulteriori analisi. 

* **Log di controllo**: Il [report delle attività del log di controllo](concept-audit-logs.md) consente di accedere alla cronologia di ogni attività eseguita nel tenant.
* **Log di accesso**: Il [report delle attività di accesso](concept-sign-ins.md) consente di determinare chi ha eseguito le attività segnalate nei log di controllo.

> [!NOTE]
> I log attività di controllo e di accesso correlati a B2C non sono al momento supportati.
>

## <a name="prerequisites"></a>Prerequisiti 

Per usare questa funzionalità, sono necessari:

* Una sottoscrizione di Azure. Se non si ha una sottoscrizione di Azure, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/free/).
* Un tenant di Azure AD.
* Un utente con il ruolo di *amministratore globale* o *amministratore della sicurezza* per il tenant di Azure AD.
* Un'area di lavoro Log Analytics nella sottoscrizione di Azure. Informazioni su [come creare un'area di lavoro Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace).

## <a name="send-logs-to-azure-monitor"></a>Inviare i log al monitoraggio di Azure

1. Accedere al [portale di Azure](https://portal.azure.com). 

2. Selezionare **Azure Active Directory** > **Impostazioni di diagnostica** -> **Aggiungi impostazioni di diagnostica**. È anche possibile selezionare **Esporta impostazioni** dalla pagina **Log di controllo** o **Accessi** per visualizzare la pagina di configurazione delle impostazioni di diagnostica.  
    
3. Nel menu **Impostazioni di diagnostica** selezionare la casella di controllo **Send to Log Analytics workspace** (Invia ad area di lavoro Log Analytics) e quindi selezionare **Configura**.

4. Selezionare l'area di lavoro Log Analytics a cui si vogliono inviare i log oppure creare una nuova area di lavoro nella finestra di dialogo visualizzata.  

5. Eseguire una di queste operazioni o entrambe:
    * Per inviare i log di controllo all'area di lavoro Log Analytics, selezionare la casella di controllo **AuditLogs**. 
    * Per inviare i log di accesso all'area di lavoro Log Analytics, selezionare la casella di controllo **SignInLogs**.

6. Selezionare **Salva** per salvare l'impostazione.

    ![Impostazioni di diagnostica](./media/howto-integrate-activity-logs-with-log-analytics/Configure.png)

7. Dopo circa 15 minuti, verificare che gli eventi vengano trasmessi all'area di lavoro Log Analytics.

## <a name="next-steps"></a>Passaggi successivi

* [Analizzare i log attività di Azure AD con i log di Monitoraggio di Azure](howto-analyze-activity-logs-log-analytics.md)
* [Installare e usare le viste di analisi dei log per Azure Active Directory](howto-install-use-log-analytics-views.md)