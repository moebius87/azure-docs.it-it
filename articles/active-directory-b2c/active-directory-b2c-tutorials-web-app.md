---
title: "Esercitazione: Abilitare l'autenticazione in un'applicazione Web - Azure Active Directory B2C | Microsoft Docs"
description: Esercitazione su come usare Azure Active Directory B2C per consentire l'accesso degli utenti a un'applicazione Web ASP.NET.
services: active-directory-b2c
author: davidmu1
manager: celestedg
ms.author: davidmu
ms.date: 02/04/2019
ms.custom: mvc
ms.topic: tutorial
ms.service: active-directory
ms.subservice: B2C
ms.openlocfilehash: 243df4457263a3653c501c7a409d2c3a77ee07e1
ms.sourcegitcommit: 44a85a2ed288f484cc3cdf71d9b51bc0be64cc33
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64690159"
---
# <a name="tutorial-enable-authentication-in-a-web-application-using-azure-active-directory-b2c"></a>Esercitazione: Abilitare l'autenticazione in un'applicazione Web con Azure Active Directory B2C

Questa esercitazione illustra come usare Azure Active Directory (Azure AD) B2C per l'iscrizione e l'accesso degli utenti in un'applicazione Web ASP.NET. Azure AD B2C consente alle applicazioni di eseguire l'autenticazione ad account di social network, aziendali e di Azure Active Directory usando protocolli standard aperti.

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Aggiornare l'applicazione in Azure AD B2C
> * Configurare l'esempio per l'uso dell'applicazione
> * Iscriversi usando il flusso utente

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a>Prerequisiti

- [Creare flussi utente](tutorial-create-user-flows.md) per abilitare le esperienze utente nell'applicazione. 
- Installare [Visual Studio 2017](https://www.visualstudio.com/downloads/) con il carico di lavoro **Sviluppo ASP.NET e Web**.

## <a name="update-the-application"></a>Aggiornare l'applicazione

Nell'esercitazione completata come parte dei prerequisiti è stato aggiunta un'applicazione Web in Azure AD B2C. Per consentire la comunicazione con l'esempio in questa esercitazione, è necessario aggiungere un URI di reindirizzamento all'applicazione in Azure AD B2C.

1. Accedere al [portale di Azure](https://portal.azure.com).
2. Assicurarsi di usare la directory che contiene il tenant di Azure AD B2C. A tale scopo, fare clic sul **filtro delle directory e delle sottoscrizioni** nel menu in alto e scegliere la directory che contiene il tenant.
3. Scegliere **Tutti i servizi** nell'angolo in alto a sinistra nel portale di Azure e quindi cercare e selezionare **Azure AD B2C**.
4. Selezionare **Applicazioni** e quindi l'applicazione *webapp1*.
5. In **URL di risposta** aggiungere `https://localhost:44316`.
6. Selezionare **Salva**.
7. Nella pagina delle proprietà prendere nota dell'ID applicazione, che verrà usato durante la configurazione dell'applicazione Web.
8. Selezionare **Chiavi**, **Genera chiave** e quindi **Salva**. Prendere nota della chiave, che verrà usata durante la configurazione dell'applicazione Web.

## <a name="configure-the-sample"></a>Configurare l'esempio

In questa esercitazione si configura un esempio che è possibile scaricare da GitHub. L'esempio usa ASP.NET per offrire un semplice elenco attività e [componenti middleware Microsoft OWIN](https://docs.microsoft.com/aspnet/aspnet/overview/owin-and-katana/). [Scaricare un file ZIP](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi/archive/master.zip) o clonare l'esempio da GitHub. Assicurarsi di estrarre il file di esempio in una cartella il cui percorso sia costituito da un numero totale di caratteri minore di 260.

```
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

I due progetti inclusi nella soluzione di esempio sono i seguenti:

- **TaskWebApp** crea e modifica un elenco attività. L'esempio usa il flusso utente di **iscrizione o accesso** per l'iscrizione o l'accesso degli utenti.
- **TaskService** supporta le funzionalità di creazione, lettura, aggiornamento ed eliminazione dell'elenco attività. L'API è protetta da Azure AD B2C e viene chiamata da TaskWebApp.

Modificare l'esempio per usare l'applicazione registrata nel tenant in uso, con l'ID applicazione e la chiave annotati in precedenza. Configurare anche i flussi utente creati. L'esempio definisce i valori di configurazione come impostazioni nel file Web.config. Per modificare le impostazioni:

1. Aprire la soluzione **B2C-WebAPI-DotNet** in Visual Studio.
2. Nel progetto **TaskWebApp** aprire il file **Web.config**. Sostituire il valore di `ida:Tenant` con il nome del tenant creato. Sostituire il valore di `ida:ClientId` con l'ID applicazione registrato. Sostituire il valore di `ida:ClientSecret` con la chiave registrata.
3. Nel file **Web.config** sostituire il valore di `ida:SignUpSignInPolicyId` con `b2c_1_signupsignin1`. Sostituire il valore di `ida:EditProfilePolicyId` con `b2c_1_profileediting1`. Sostituire il valore di `ida:ResetPasswordPolicyId` con `b2c_1_passwordreset1`.

## <a name="run-the-sample"></a>Eseguire l'esempio

1. In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **TaskWebApp** e quindi scegliere **Imposta come progetto di avvio**.
2. Premere **F5**. Il browser predefinito si apre con l'indirizzo del sito Web locale `https://localhost:44316/`.

### <a name="sign-up-using-an-email-address"></a>Iscriversi usando un indirizzo di posta elettronica

1. Fare clic su **Sign up / Sign in** per iscriversi come utente dell'applicazione. Verrà usato il flusso utente **b2c_1_signupsignin1**.
2. Azure AD B2C presenta una pagina di accesso con un collegamento di iscrizione. Dato che non si ha ancora un account, selezionare **Iscriversi adesso**. Il flusso di lavoro per l'iscrizione presenta una pagina per raccogliere e verificare l'identità dell'utente usando un indirizzo e-mail. Il flusso di lavoro per l'iscrizione raccoglie anche la password dell'utente e gli attributi richiesti definiti nel flusso utente.
3. Usare un indirizzo e-mail valido ed eseguire la convalida usando un codice di verifica. Impostare una password. Immettere i valori per gli attributi richiesti. 

    ![Flusso di lavoro di iscrizione](media/active-directory-b2c-tutorials-web-app/sign-up-workflow.png)

4. Fare clic su **Crea** per creare un account locale nel tenant di Azure AD B2C.

Ora l'utente può usare il proprio indirizzo di posta elettronica per accedere all'applicazione Web e usarla.

## <a name="next-steps"></a>Passaggi successivi

Questa esercitazione illustra come:

> [!div class="checklist"]
> * Aggiornare l'applicazione in Azure AD B2C
> * Configurare l'esempio per l'uso dell'applicazione
> * Iscriversi usando il flusso utente

> [!div class="nextstepaction"]
> [Esercitazione: Usare Azure Active Directory B2C per proteggere un'API Web ASP.NET](active-directory-b2c-tutorials-web-api.md)
