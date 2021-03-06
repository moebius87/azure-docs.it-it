---
title: File di inclusione
description: File di inclusione
services: active-directory
documentationcenter: dev-center-name
author: jmprieur
manager: CelesteDG
editor: ''
ms.service: active-directory
ms.devlang: na
ms.topic: include
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/17/2018
ms.author: jmprieur
ms.custom: include file
ms.openlocfilehash: dcfc341b89a3cfebcb5538f88481fd2fbb2936a7
ms.sourcegitcommit: c174d408a5522b58160e17a87d2b6ef4482a6694
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "59505818"
---
## <a name="set-up-your-project"></a>Configurare il progetto

Questa sezione illustra la procedura per l'installazione e la configurazione della pipeline di autenticazione tramite middleware OWIN in un progetto ASP.NET mediante OpenID Connect.

> Se invece si preferisce scaricare questo progetto Visual Studio di esempio, [Scaricare un progetto](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) e passare direttamente al [passaggio di configurazione](#register-your-application) per configurare il codice di esempio prima di eseguirlo.

### <a name="create-your-aspnet-project"></a>Creare un progetto ASP.NET

1. In Visual Studio: `File` > `New` > `Project`
2. In *Visual C#\Web* selezionare `ASP.NET Web Application (.NET Framework)`
3. Assegnare un nome all'applicazione e fare clic su *OK*
4. Selezionare `Empty` e quindi selezionare la casella di controllo per aggiungere i riferimenti `MVC`

## <a name="add-authentication-components"></a>Aggiungere i componenti per l'autenticazione

1. In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Aggiungere *pacchetti NuGet del middleware OWIN* digitando quanto segue nella finestra della Console di Gestione pacchetti:

    ```powershell
    Install-Package Microsoft.Owin.Security.OpenIdConnect
    Install-Package Microsoft.Owin.Security.Cookies
    Install-Package Microsoft.Owin.Host.SystemWeb
    ```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a>Informazioni sulle librerie
> Le librerie precedenti abilitano l'accesso Single Sign-On (SSO) usando OpenID Connect tramite l'autenticazione basata su cookie. Al termine dell'autenticazione e dopo l'invio del token che rappresenta l'utente all'applicazione, il middleware OWIN crea un cookie di sessione. Il browser usa quindi questo cookie nelle richieste successive, in modo che l'utente non debba digitare di nuovo la password e non siano necessarie operazioni di verifica aggiuntive.
<!--end-collapse-->

## <a name="configure-the-authentication-pipeline"></a>Configurare la pipeline di autenticazione

La procedura seguente consente di creare una classe di avvio del middleware OWIN per configurare l'autenticazione OpenID Connect. Questa classe verrà eseguita automaticamente all'avvio del processo di IIS.

> [!TIP]
> Se il progetto non include alcun file `Startup.cs` nella cartella radice:
> 1. Fare clic con il pulsante destro del mouse sulla cartella radice del progetto: > `Add` > `New Item...` > `OWIN Startup class`<br/>
> 2. Assegnare il nome `Startup.cs`
>
>> Assicurarsi che la classe selezionata sia una classe di avvio di OWIN e non una classe C# standard. Per confermarlo, verificare se `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` viene visualizzato sopra lo spazio dei nomi.

1. Aggiungere i riferimenti *OWIN* e *Microsoft.IdentityModel* a `Startup.cs`:

    ```csharp
    using Microsoft.Owin;
    using Owin;
    using Microsoft.IdentityModel.Protocols.OpenIdConnect;
    using Microsoft.IdentityModel.Tokens;
    using Microsoft.Owin.Security;
    using Microsoft.Owin.Security.Cookies;
    using Microsoft.Owin.Security.OpenIdConnect;
    using Microsoft.Owin.Security.Notifications;
    ```

2. Sostituire la classe di avvio con il codice seguente:

    ```csharp
    public class Startup
    {
        // The Client ID is used by the application to uniquely identify itself to Azure AD.
        string clientId = System.Configuration.ConfigurationManager.AppSettings["ClientId"];

        // RedirectUri is the URL where the user will be redirected to after they sign in.
        string redirectUri = System.Configuration.ConfigurationManager.AppSettings["RedirectUri"];

        // Tenant is the tenant ID (e.g. contoso.onmicrosoft.com, or 'common' for multi-tenant)
        static string tenant = System.Configuration.ConfigurationManager.AppSettings["Tenant"];

        // Authority is the URL for authority, composed by Azure Active Directory v2.0 endpoint and the tenant name (e.g. https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0)
        string authority = String.Format(System.Globalization.CultureInfo.InvariantCulture, System.Configuration.ConfigurationManager.AppSettings["Authority"], tenant);

        /// <summary>
        /// Configure OWIN to use OpenIdConnect 
        /// </summary>
        /// <param name="app"></param>
        public void Configuration(IAppBuilder app)
        {
            app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

            app.UseCookieAuthentication(new CookieAuthenticationOptions());
            app.UseOpenIdConnectAuthentication(
                new OpenIdConnectAuthenticationOptions
                {
                    // Sets the ClientId, authority, RedirectUri as obtained from web.config
                    ClientId = clientId,
                    Authority = authority,
                    RedirectUri = redirectUri,
                    // PostLogoutRedirectUri is the page that users will be redirected to after sign-out. In this case, it is using the home page
                    PostLogoutRedirectUri = redirectUri,
                    Scope = OpenIdConnectScope.OpenIdProfile,
                    // ResponseType is set to request the id_token - which contains basic information about the signed-in user
                    ResponseType = OpenIdConnectResponseType.IdToken,
                    // ValidateIssuer set to false to allow personal and work accounts from any organization to sign in to your application
                    // To only allow users from a single organizations, set ValidateIssuer to true and 'tenant' setting in web.config to the tenant name
                    // To allow users from only a list of specific organizations, set ValidateIssuer to true and use ValidIssuers parameter
                    TokenValidationParameters = new TokenValidationParameters()
                    {
                        ValidateIssuer = false // This is a simplification
                    },
                    // OpenIdConnectAuthenticationNotifications configures OWIN to send notification of failed authentications to OnAuthenticationFailed method
                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed
                    }
                }
            );
        }

        /// <summary>
        /// Handle failed authentication requests by redirecting the user to the home page with an error in the query string
        /// </summary>
        /// <param name="context"></param>
        /// <returns></returns>
        private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> context)
        {
            context.HandleResponse();
            context.Response.Redirect("/?errormessage=" + context.Exception.Message);
            return Task.FromResult(0);
        }
    }
    ```

> [!NOTE]
> L'impostazione di `ValidateIssuer = false` è una semplificazione per questo avvio rapido. Nelle applicazioni reali è necessario convalidare l'autorità di certificazione. Vedere gli esempi per comprendere come eseguire questa operazione.

<!--start-collapse-->
> ### <a name="more-information"></a>Altre informazioni
> I parametri forniti in *OpenIDConnectAuthenticationOptions* fungeranno da coordinate per consentire all'applicazione di comunicare con Azure AD. Poiché il middleware OpenID Connect usa i cookie in background, è anche necessario configurare l'autenticazione dei cookie, come illustrato nel codice precedente. Il valore *ValidateIssuer* segnala a OpenIdConnect di non limitare l'accesso a un'organizzazione specifica.
<!--end-collapse-->
