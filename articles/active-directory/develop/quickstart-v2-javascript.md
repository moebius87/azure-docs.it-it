---
title: Avvio rapido per l'uso di Microsoft Identity Platform con un'app JavaScript | Azure
description: Informazioni su come le applicazioni JavaScript possono chiamare un'API che richiede token di accesso generati da Microsoft Identity Platform.
services: active-directory
documentationcenter: dev-center-name
author: navyasric
manager: CelesteDG
editor: ''
ms.service: active-directory
ms.subservice: develop
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/11/2019
ms.author: nacanuma
ms.custom: aaddev
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2021c5028637a6f7e732df61b6f7c034ef79324f
ms.sourcegitcommit: 031e4165a1767c00bb5365ce9b2a189c8b69d4c0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/13/2019
ms.locfileid: "59547398"
---
# <a name="quickstart-sign-in-users-and-acquire-an-access-token-from-a-javascript-single-page-application-spa"></a>Guida introduttiva: Concedere l'accesso agli utenti e acquisire un token di accesso da un'applicazione JavaScript a pagina singola

[!INCLUDE [active-directory-develop-applies-v2-msal](../../../includes/active-directory-develop-applies-v2-msal.md)]

Questo avvio rapido illustra come usare un codice di esempio che dimostra come un'applicazione JavaScript a pagina singola possa concedere l'accesso ad account personali, di lavoro o dell'istituto di istruzione e ottenere un token di accesso per chiamare l'API Microsoft Graph o un'API Web.

![Mostra come funziona l'app di esempio generata da questo avvio rapido](media/quickstart-v2-javascript/javascriptspa-intro.svg)

## <a name="prerequisites"></a>Prerequisiti

Per questo avvio rapido è necessaria la configurazione seguente:
* Per eseguire il progetto con un server node.js
    * Installare [Node.js](https://nodejs.org/en/download/)
    * Installare [Visual Studio Code](https://code.visualstudio.com/download) per modificare i file di progetto
* Per eseguire il progetto come soluzione di Visual Studio, installare [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/).

> [!div renderon="docs"]
> ## <a name="register-and-download-your-quickstart-application"></a>Registrare e scaricare l'app dell'avvio rapido
> Per avviare l'applicazione della guida introduttiva sono disponibili due opzioni:
> * [Rapida] [Opzione 1: Registrare e configurare automaticamente l'app e quindi scaricare l'esempio di codice](#option-1-register-and-auto-configure-your-app-and-then-download-your-code-sample)
> * [Manuale] [Opzione 2: Registrare e configurare manualmente l'applicazione e il codice di esempio](#option-2-register-and-manually-configure-your-application-and-code-sample)
>
> ### <a name="option-1-register-and-auto-configure-your-app-and-then-download-your-code-sample"></a>Opzione 1: Registrare e configurare automaticamente l'app e quindi scaricare l'esempio di codice
>
> 1. Accedere al [portale di Azure](https://portal.azure.com) con un account aziendale o dell'istituto di istruzione oppure con un account Microsoft personale.
> 1. Se l'account consente di accedere a più tenant, selezionare l'account nell'angolo in alto a destra e impostare la sessione del portale sul tenant di Azure Active Directory desiderato.
> 1. Passare al nuovo riquadro [Portale di Azure - Registrazioni app](https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/applicationsListBlade/quickStartType/JavascriptSpaQuickstartPage/sourceType/docs).
> 1. Immettere un nome per l'applicazione e fare clic su **Registra**.
> 1. Seguire le istruzioni per scaricare e configurare automaticamente la nuova applicazione con un clic.
>
> ### <a name="option-2-register-and-manually-configure-your-application-and-code-sample"></a>Opzione 2: Registrare e configurare manualmente l'applicazione e il codice di esempio
>
> #### <a name="step-1-register-your-application"></a>Passaggio 1: Registrare l'applicazione
>
> 1. Accedere al [portale di Azure](https://portal.azure.com) con un account aziendale o dell'istituto di istruzione oppure con un account Microsoft personale.
> 1. Se l'account consente di accedere a più tenant, selezionare l'account nell'angolo in alto a destra e impostare la sessione del portale sul tenant di Azure Active Directory desiderato.
> 1. Passare alla pagina [Registrazioni app](https://go.microsoft.com/fwlink/?linkid=2083908) di Microsoft Identity Platform per sviluppatori.
> 1. Selezionare **Nuova registrazione**.
> 1. Nella pagina **Registra un'applicazione** visualizzata immettere il nome dell'applicazione.
> 1. In **Tipi di account supportati** selezionare **Account in qualsiasi directory organizzativa e account Microsoft personali**.
> 1. Selezionare la piattaforma **Web** nella sezione **URI di reindirizzamento** e impostare il valore su `http://localhost:30662/`.
> 1. Al termine, selezionare **Registra**.  Nella pagina **Panoramica**  dell'app prendere nota del valore del campo **ID applicazione (client)**.
> 1. Per questo avvio rapido è necessario abilitare il [flusso di concessione implicita](v2-oauth2-implicit-grant-flow.md). Nel riquadro di spostamento a sinistra dell'applicazione registrata selezionare **Autenticazione**.
> 1. Nelle **Impostazioni avanzate**, in **Concessione implicita**, selezionare entrambe le caselle di controllo **Token ID** e **Token di accesso**. I token ID e di accesso sono obbligatori perché l'app deve consentire l'accesso agli utenti e chiamare un'API.
> 1. Selezionare **Salva**.

> [!div class="sxs-lookup" renderon="portal"]
> #### <a name="step-1-configure-your-application-in-the-azure-portal"></a>Passaggio 1: Configurare l'applicazione nel portale di Azure
> Per il funzionamento dell'esempio di codice di questa guida introduttiva è necessario aggiungere un URI di reindirizzamento come `http://localhost:30662/` e abilitare l'opzione **Concessione implicita**.
> > [!div renderon="portal" id="makechanges" class="nextstepaction"]
> > [Apporta queste modifiche per me]()
>
> > [!div id="appconfigured" class="alert alert-info"]
> > ![Già configurata](media/quickstart-v2-javascript/green-check.png) L'applicazione è configurata con questi attributi.

#### <a name="step-2-download-the-project"></a>Passaggio 2: Scaricare il progetto

È possibile scegliere una di queste opzioni, in funzione dell'ambiente di sviluppo in uso.
* [Scaricare i file di progetto di base per un server Web, ad esempio Node.js](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/quickstart.zip)
* [Scaricare il progetto di Visual Studio](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/vsquickstart.zip)

Estrarre il file con estensione zip in una cartella locale, ad esempio **C:\Azure-Samples**.
Per aprire i file nella cartella, usare un editor come [Visual Studio Code](https://code.visualstudio.com/).

#### <a name="step-3-configure-your-javascript-app"></a>Passaggio 3: Configurare l'app JavaScript

> [!div renderon="docs"]
> Nella cartella *JavaScriptSPA* modificare `index.html` e impostare i valori `clientID` e `authority` in `applicationConfig`.

> [!div class="sxs-lookup" renderon="portal"]
> Nella cartella *JavaScriptSPA* modificare `index.html` e sostituire `applicationConfig` con:

```javascript
var applicationConfig = {
    clientID: "Enter_the_Application_Id_here",
    authority: "https://login.microsoftonline.com/Enter_the_Tenant_Info_Here",
    graphScopes: ["user.read"],
    graphEndpoint: "https://graph.microsoft.com/v1.0/me"
};
```
> [!div renderon="docs"]
>
> Dove:
> - `Enter_the_Application_Id_here` è l'**ID applicazione (client)** per l'applicazione registrata.
> - `Enter_the_Tenant_Info_Here` è impostato su una delle opzioni seguenti:
>   - Se l'applicazione supporta **Account solo in questa directory organizzativa**, sostituire questo valore con l'**ID tenant** o il **nome del tenant** (ad esempio, contoso.microsoft.com)
>   - Se l'applicazione supporta **Account in qualsiasi directory organizzativa**, sostituire questo valore con `organizations`
>   - Se l'applicazione supporta **Account in qualsiasi directory organizzativa e account Microsoft personali**, sostituire questo valore con `common`
>
> > [!TIP]
> > Per trovare i valori di **ID applicazione (client)**, **ID della directory (tenant)** e **Tipi di account supportati**, passare alla pagina di **panoramica** dell'app nel portale di Azure.

#### <a name="step-4-run-the-project"></a>Passaggio 4: Eseguire il progetto

* Se si usa [Node.js](https://nodejs.org/en/download/):

    1. Nella directory del progetto eseguire il comando seguente per avviare il server:

        ```batch
        npm install
        node server.js
        ```

    1. Aprire un Web browser e passare a `http://localhost:30662/`.
    1. Fare clic sul pulsante **Accedi** per effettuare l'accesso e poi chiamare l'API Microsoft Graph.


* Se si usa [Visual Studio](https://visualstudio.microsoft.com/downloads/), assicurarsi di selezionare la soluzione di progetto e quindi premere **F5** per eseguire il progetto.

Dopo che il browser ha caricato l'applicazione, fare clic su **Accedi**.  Al primo accesso viene chiesto di concedere il proprio consenso per consentire all'applicazione di accedere al profilo e completare la procedura di accesso. Se l'accesso ha esito positivo, nella pagina dovrebbero essere visualizzate le informazioni del profilo utente.

## <a name="more-information"></a>Altre informazioni

### <a name="msaljs"></a>*msal.js*

MSAL è la libreria usata per concedere l'accesso agli utenti e richiedere i token usati per accedere a un'API protetta da Microsoft Identity Platform. Il file *index.html* della guida introduttiva contiene un riferimento alla libreria:

```html
<script src="https://secure.aadcdn.microsoftonline-p.com/lib/0.2.4/js/msal.min.js"></script>
```

In alternativa, se Node è già installato, è possibile scaricarlo tramite npm:

```batch
npm install msal
```

### <a name="msal-initialization"></a>Inizializzazione della libreria MSAL

Il codice della guida introduttiva illustra anche come inizializzare la libreria:

```javascript
var myMSALObj = new Msal.UserAgentApplication(applicationConfig.clientID, applicationConfig.authority, acquireTokenRedirectCallBack, {storeAuthStateInCookie: true, cacheLocation: "localStorage"});
```

> |Where  |  |
> |---------|---------|
> |`ClientId`     |ID dell'applicazione registrata nel portale di Azure|
> |`authority`    |URL dell'autorità. Se si passa il valore *null*, l'autorità predefinita viene impostata su `https://login.microsoftonline.com/common`. Se l'app è a singolo tenant (destinata solo agli account di una directory), impostare questo valore su `https://login.microsoftonline.com/<tenant name or ID>`|
> |`tokenReceivedCallback`| Metodo di callback chiamato dopo il reindirizzamento dell'autenticazione all'app. Qui viene passato `acquireTokenRedirectCallBack`. Se si usa loginPopup, il valore è Null.|
> |`options`  |Raccolta di parametri facoltativi. In questo caso `storeAuthStateInCookie` e `cacheLocation` sono facoltativi. Vedere il [wiki](https://github.com/AzureAD/microsoft-authentication-library-for-js/wiki/MSAL-basics#configuration-options) per altri dettagli sulle opzioni. |

### <a name="sign-in-users"></a>Consentire l'accesso degli utenti

Il frammento di codice seguente illustra come consentire l'accesso degli utenti:

```javascript
myMSALObj.loginPopup(applicationConfig.graphScopes).then(function (idToken) {
    //Callback code here
})
```

> |Where  |  |
> |---------|---------|
> | `scopes`   | (Facoltativo) Contiene gli ambiti richiesti per il consenso dell'utente al momento dell'accesso, ad esempio: `[ "user.read" ]` per Microsoft Graph o `[ "<Application ID URL>/scope" ]` per le API Web personalizzate, ovvero `api://<Application ID>/access_as_user`. Qui viene passato `applicationConfig.graphScopes`. |

> [!TIP]
> In alternativa, è possibile usare il metodo `loginRedirect` per reindirizzare alla pagina corrente alla pagina di accesso anziché a una finestra popup.

### <a name="request-tokens"></a>Richiedere token

In MSAL sono disponibili tre metodi per acquisire i token: `acquireTokenRedirect`, `acquireTokenPopup` e `acquireTokenSilent`

#### <a name="get-a-user-token-silently"></a>Ottenere un token utente in modo automatico

Il metodo `acquireTokenSilent` gestisce le acquisizioni e i rinnovi dei token senza alcuna interazione da parte dell'utente. Dopo aver eseguito il metodo `loginRedirect` o `loginPopup` la prima volta, per le chiamate successive il metodo comunemente usato per ottenere i token usati per accedere a risorse protette è `acquireTokenSilent`. Le chiamate per richiedere o rinnovare i token vengono eseguite in modo invisibile per l'utente.

```javascript
myMSALObj.acquireTokenSilent(applicationConfig.graphScopes).then(function (accessToken) {
    // Callback code here
})
```

> |Where  |  |
> |---------|---------|
> | `scopes`   | Contiene gli ambiti da restituire nel token di accesso per l'API, ad esempio: `[ "user.read" ]` per Microsoft Graph o `[ "<Application ID URL>/scope" ]` per le API Web personalizzate, ovvero `api://<Application ID>/access_as_user`. Qui viene passato `applicationConfig.graphScopes`.|

#### <a name="get-a-user-token-interactively"></a>Ottenere un token utente in modo interattivo

In alcune situazioni è necessario forzare gli utenti a interagire con l'endpoint di Microsoft Identity Platform. Ad esempio: 
* Un utente deve immettere nuovamente le credenziali perché la password è scaduta
* L'applicazione richiede l'accesso ad ambiti di risorse aggiuntivi per cui è necessario il consenso dell'utente
* È necessaria l'autenticazione a due fattori

Per la maggior parte delle applicazioni, l'approccio consigliato è quello di chiamare prima `acquireTokenSilent`, quindi individuare l'eccezione e infine chiamare `acquireTokenRedirect` (o `acquireTokenPopup`) per avviare una richiesta interattiva.

Se si chiama `acquireTokenPopup(scope)`, viene visualizzata una finestra popup di accesso (mentre con `acquireTokenRedirect(scope)` gli utenti vengono reindirizzati all'endpoint di Microsoft Identity Platform) e gli utenti devono interagire confermando le proprie credenziali, dando il consenso per la risorsa necessaria o completando l'autenticazione a due fattori.

```javascript
myMSALObj.acquireTokenPopup(applicationConfig.graphScopes).then(function (accessToken) {
    // Callback code here
})
```

> [!NOTE]
> Questa guida introduttiva usa i metodi `loginRedirect` e `acquireTokenRedirect` quando il browser è Internet Explorer, per un [problema noto](https://github.com/AzureAD/microsoft-authentication-library-for-js/wiki/Known-issues-on-IE-and-Edge-Browser#issues) correlato alla gestione delle finestre popup da questo browser.

## <a name="next-steps"></a>Passaggi successivi

Per una guida più dettagliata su come creare l'applicazione per questa guida introduttiva, completare l'esercitazione su JavaScript seguente.

### <a name="learn-the-steps-to-create-the-application-for-this-quickstart"></a>Informazioni sulla procedura per creare l'applicazione necessaria per questa guida introduttiva

> [!div class="nextstepaction"]
> [Esercitazione per l'accesso e la chiamata a MS Graph](https://docs.microsoft.com/azure/active-directory/develop/guidedsetups/active-directory-javascriptspa)

### <a name="browse-the-msal-repo-for-documentation-faq-issues-and-more"></a>Consultare il repository MSAL per documentazione, domande frequenti, problemi e altro ancora

> [!div class="nextstepaction"]
> [Repository MSAL.js di GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js)
