---
title: Creare un'app Web ASP.NET Framework C# - Servizio app di Azure | Microsoft Docs
description: Informazioni su come eseguire app Web nel servizio app di Azure distribuendo l'app Web ASP.NET in C# predefinita.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
ms.assetid: 04a1becf-7756-4d4e-92d8-d9471c263d23
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 09/05/2018
ms.author: cephalin
ms.custom: seodec18
ms.openlocfilehash: 8dc062a1c9490a03aa5369dc103db750d7531140
ms.sourcegitcommit: c94cf3840db42f099b4dc858cd0c77c4e3e4c436
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2018
ms.locfileid: "53635273"
---
# <a name="create-an-aspnet-framework-web-app-in-azure"></a>Creare un'app Web del framework ASP.NET in Azure

[Servizio app di Azure](overview.md) offre un servizio di hosting Web con scalabilità elevata e funzioni di auto-correzione.  Questa guida introduttiva illustra come distribuire la prima app Web ASP.NET nel servizio app di Azure. Al termine, si avrà un gruppo di risorse costituito da un piano di servizio app e da un'app del servizio app con un'applicazione Web distribuita.

![](./media/app-service-web-get-started-dotnet-framework/published-azure-web-app.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a>Prerequisiti

Per completare questa esercitazione, installare <a href="https://www.visualstudio.com/downloads/" target="_blank">Visual Studio 2017</a> con il carico di lavoro **Sviluppo ASP.NET e Web**.

Se Visual Studio 2017 è già installato:

- Installare gli aggiornamenti più recenti in Visual Studio facendo clic su **?** > **Controlla la disponibilità di aggiornamenti**.
- Aggiungere il carico di lavoro facendo clic su **Strumenti** > **Ottieni strumenti e funzionalità**.

## <a name="create-an-aspnet-web-app"></a>Creare un'app Web ASP.NET

In Visual Studio creare un progetto selezionando **File > Nuovo > Progetto**. 

Nella finestra di dialogo **Nuovo progetto** selezionare **Visual C# > Web > Applicazione Web ASP.NET (.NET Framework)**.

Assegnare all'applicazione il nome _myFirstAzureWebApp_ e fare clic su **OK**.
   
![Finestra di dialogo Nuovo progetto](./media/app-service-web-get-started-dotnet-framework/new-project.png)

È possibile distribuire qualsiasi tipo di app Web ASP.NET in Azure. Per questa guida introduttiva, selezionare il modello **MVC** e verificare che l'autenticazione sia impostata su **Nessuna autenticazione**.
      
Selezionare **OK**.

![Finestra di dialogo Nuovo progetto ASP.NET](./media/app-service-web-get-started-dotnet-framework/select-mvc-template.png)

Nel menu selezionare **Debug > Avvia senza eseguire debug** per eseguire l'app Web in locale.

![Eseguire l'app in locale](./media/app-service-web-get-started-dotnet-framework/local-web-app.png)

## <a name="launch-the-publish-wizard"></a>Avviare la procedura guidata di pubblicazione

In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **myFirstAzureWebApp** e scegliere **Pubblica**.

![Pubblicare da Esplora soluzioni](./media/app-service-web-get-started-dotnet-framework/solution-explorer-publish.png)

La procedura guidata di pubblicazione viene avviata automaticamente. Selezionare **Servizio app** > **Pubblica** per aprire la finestra di dialogo **Crea servizio app**.

![Pubblicare dalla pagina di panoramica progetto](./media/app-service-web-get-started-dotnet-framework/publish-to-app-service.png)

## <a name="sign-in-to-azure"></a>Accedere ad Azure

Nella finestra di dialogo **Crea servizio app** fare clic su **Aggiungi un account** e accedere alla sottoscrizione di Azure. Se è già stato eseguito l'accesso, selezionare l'account contenente la sottoscrizione desiderata dall'elenco a discesa.

> [!NOTE]
> Se si è già connessi, non selezionare ancora l'opzione **Crea**.
>
>
   
![Accedere ad Azure](./media/app-service-web-get-started-dotnet-framework/sign-in-azure.png)

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

Accanto a **Gruppo di risorse** selezionare **Nuovo**.

Assegnare al gruppo di risorse il nome **myResourceGroup** e selezionare **OK**.

## <a name="create-an-app-service-plan"></a>Creare un piano di servizio app

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Accanto a **Piano di hosting** selezionare **Nuovo**. 

Nella finestra di dialogo **Configura piano di hosting** usare le impostazioni della tabella riportata sotto lo screenshot.

![Creare un piano di servizio app](./media/app-service-web-get-started-dotnet-framework/configure-app-service-plan.png)

| Impostazione | Valore consigliato | Descrizione |
|-|-|-|
|Piano di servizio app| myAppServicePlan | Nome del piano di servizio app. |
| Località | Europa occidentale | Data center in cui è ospitata l'app Web. |
| Dimensione | Gratuito | [Piano tariffario](https://azure.microsoft.com/pricing/details/app-service/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) che determina le funzionalità di hosting. |

Selezionare **OK**.

## <a name="create-and-publish-the-web-app"></a>Creare e pubblicare l'app Web

In **Nome app** immettere un nome univoco dell'app, usando i caratteri validi `a-z`, `0-9` e `-`, o accettare il nome univoco generato automaticamente. L'URL dell'app Web è `http://<app_name>.azurewebsites.net`, dove `<app_name>` è il nome dell'app.

Selezionare **Crea** per avviare la creazione delle risorse di Azure.

![Configurare il nome dell'app](./media/app-service-web-get-started-dotnet-framework/web-app-name.png)

Al termine della procedura guidata, l'app Web ASP.NET viene pubblicata in Azure e avviata nel browser predefinito.

![App Web ASP.NET pubblicata in Azure](./media/app-service-web-get-started-dotnet-framework/published-azure-web-app.png)

Il nome dell'app specificato nel passaggio relativo alla [creazione e pubblicazione](#create-and-publish-the-web-app) viene usato come prefisso dell'URL nel formato `http://<app_name>.azurewebsites.net`.

L'app Web ASP.NET è ora in esecuzione nel servizio app di Azure.

## <a name="update-the-app-and-redeploy"></a>Aggiornare e ridistribuire l'app

Da **Esplora soluzioni** aprire _Views\Home\Index.cshtml_.

Trovare il tag HTML `<div class="jumbotron">` in alto e sostituire l'intero elemento con il codice seguente:

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how to deploy a .NET app to Azure App Service.</p>
</div>
```

Per la ridistribuzione in Azure, fare clic con il pulsante destro del mouse sul progetto **myFirstAzureWebApp** in **Esplora soluzioni** e selezionare **Pubblica**.

Nella pagina di pubblicazione selezionare **Pubblica**.
![Pagina di riepilogo della pubblicazione di Visual Studio](./media/app-service-web-get-started-dotnet-framework/publish-summary-page.png)

Al termine del processo di pubblicazione, Visual Studio avvia un browser sull'URL dell'app Web.

![App Web ASP.NET aggiornata in Azure](./media/app-service-web-get-started-dotnet-framework/updated-azure-web-app.png)

## <a name="manage-the-azure-app"></a>Gestire l'app Azure

Accedere al <a href="https://portal.azure.com" target="_blank">portale di Azure</a> per visualizzare l'app Web.

Nel menu a sinistra scegliere **Servizi app** e quindi selezionare il nome dell'app Azure.

![Passaggio all'app di Azure nel portale](./media/app-service-web-get-started-dotnet-framework/access-portal.png)

Verrà visualizzata la pagina di panoramica dell'app Web. Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app. 

![Pannello del servizio app nel portale di Azure](./media/app-service-web-get-started-dotnet-framework/web-app-blade.png)

Il menu a sinistra fornisce varie pagine per la configurazione dell'app. 

## <a name="video"></a>Video

Guardare il video per osservare il funzionamento di questa guida introduttiva e quindi seguire personalmente la procedura per pubblicare la prima app .NET in Azure.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [ASP.NET con database SQL](app-service-web-tutorial-dotnet-sqldatabase.md)
