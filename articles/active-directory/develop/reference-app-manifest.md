---
title: Informazioni sul manifesto dell'app Azure Active Directory | Microsoft Docs
description: Descrizione dettagliata del manifesto dell'app Azure Active Directory, che rappresenta una configurazione dell'identità dell'applicazione in un tenant di Azure AD e che viene usato per facilitare l'autorizzazione OAuth, per l'esperienza di consenso e altro ancora.
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: 4804f3d4-0ff1-4280-b663-f8f10d54d184
ms.service: active-directory
ms.subservice: develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/13/2019
ms.author: celested
ms.custom: aaddev
ms.reviewer: sureshja
ms.collection: M365-identity-device-management
ms.openlocfilehash: 18ff5c4c54cdfe03eca572e2aa42f2330597c94d
ms.sourcegitcommit: 2028fc790f1d265dc96cf12d1ee9f1437955ad87
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/30/2019
ms.locfileid: "64918768"
---
# <a name="azure-active-directory-app-manifest"></a>Manifesto dell'app Azure Active Directory

Il manifesto dell'applicazione contiene una definizione di tutti gli attributi di un oggetto applicazione in Microsoft Identity Platform. Funge inoltre da meccanismo per laggiornamento dell'oggetto applicazione. Per altre informazioni sull'entità applicazione e il relativo schema, vedere la [documentazione sull'entità applicazione dell'API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity).

È possibile configurare gli attributi di un'app tramite il portale di Azure o a livello di codice usando [API REST](https://docs.microsoft.com/previous-versions/azure/ad/graph/api/entity-and-complex-type-reference#application-entity) oppure [PowerShell](https://docs.microsoft.com/powershell/module/azuread/?view=azureadps-2.0#applications). Tuttavia, esistono alcuni scenari in cui è necessario modificare il manifesto dell'applicazione per configurare l'attributo di un'applicazione. Tali scenari includono:

* Se l'app è stato registrato come account Microsoft personale e multi-tenant di Azure AD, è possibile modificare gli account Microsoft supportati nell'interfaccia utente. Per modificare i tipi di account supportati è necessario usare l'editor del manifesto dell'applicazione.
* Se è necessario definire le autorizzazioni e i ruoli supportati dall'applicazione, è necessario modificare il manifesto dell'applicazione.

## <a name="configure-the-app-manifest"></a>Configurare il manifesto dell'applicazione

Per configurare il manifesto dell'applicazione:

1. Accedi il [portale di Azure](https://portal.azure.com).
1. Selezionare il **Azure Active Directory** del servizio e quindi selezionare **registrazioni per l'App**.
1. Selezionare l'applicazione da configurare.
1. Nella pagina **Panoramica** dell'app selezionare la sezione **Manifesto**. Si apre un editor di manifesto basato sul Web che consente di modificare il manifesto all'interno del portale. Facoltativamente è possibile selezionare **Scarica**, modificare il manifesto in locale e quindi usare **Carica** per riapplicarlo all'applicazione.

## <a name="manifest-reference"></a>Riferimento del manifesto

> [!NOTE]
> Se non è possibile visualizzare la colonna **Valore di esempio** dopo **Descrizione**, ingrandire la finestra del browser e scorrere fino a **visualizzare la colonna**.

| Chiave  | Tipo di valore | DESCRIZIONE  | Valore di esempio |
|---------|---------|---------|---------|
| `accessTokenAcceptedVersion` | Nullable Int32 | Specifica la versione del token di accesso prevista dalla risorsa. Vengono così modificati la versione e il formato del token JWT generato indipendentemente dall'endpoint o dal client usato per richiedere il token di accesso.<br/><br/>L'endpoint usato, v1.0 o v2.0, viene scelto dal client e influisce solo sulla versione di id_tokens. Le risorse devono configurare in modo esplicito `accesstokenAcceptedVersion` per indicare il formato di token di accesso supportato.<br/><br/>I valori possibili per `accesstokenAcceptedVersion` sono 1, 2 o Null. Se il valore è Null, viene usata l'impostazione predefinita 1 che corrisponde all'endpoint v1.0. | `2` |
| `addIns` | Raccolta | Definisce il comportamento personalizzato che un servizio può usare per chiamare un'app in contesti specifici. Ad esempio, le applicazioni che eseguono il rendering di flussi di file possono impostare la proprietà addIns per la relativa funzionalità "FileHandler". Ciò consentirà a servizi come Office 365 chiamare l'applicazione nel contesto di un documento che l'utente sta lavorando. | <code>{<br>&nbsp;&nbsp;&nbsp;"id":"968A844F-7A47-430C-9163-07AE7C31D407"<br>&nbsp;&nbsp;&nbsp;"type": "FileHandler",<br>&nbsp;&nbsp;&nbsp;"properties": [<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{"key": "version", "value": "2" }<br>&nbsp;&nbsp;&nbsp;]<br>}</code>|
| `allowPublicClient` | Boolean | Specifica il tipo di applicazione di fallback. Azure AD deduce il tipo di applicazione da replyUrlsWithType per impostazione predefinita. In alcuni scenari Azure AD non è in grado di determinare il tipo di app client, ad esempio un flusso [ROPC](https://tools.ietf.org/html/rfc6749#section-4.3) in cui la richiesta HTTP viene eseguita senza reindirizzamento tramite URL. In questi casi Azure AD interpreterà il tipo di applicazione in base al valore di questa proprietà. Se questo valore è impostato su true, il tipo di applicazione di fallback è impostato come client pubblico, ad esempio un'app installata in esecuzione in un dispositivo mobile. Il valore predefinito è false, che indica che il tipo di applicazione di fallback è un client riservato, ad esempio un'app Web. | `false` |
| `availableToOtherTenants` | Boolean | true se l'applicazione viene condivisa con altri tenant; in caso contrario, false. <br><br> _Nota: È disponibile solo nell'esperienza delle App per le registrazioni (Legacy). Sostituito da `signInAudience` nella [registrazioni per l'App](https://go.microsoft.com/fwlink/?linkid=2083908) esperienza._ | |
| `appId` | string | Specifica l'identificatore univoco per l'app assegnato a un'app da Azure AD. | `"601790de-b632-4f57-9523-ee7cb6ceba95"` |
| `appRoles` | Raccolta | Specifica la raccolta di ruoli che un'app può dichiarare. Questi ruoli possono essere assegnati a utenti, gruppi o entità servizio. Per altri esempi e informazioni, vedere [Aggiungere ruoli dell'app in un'applicazione e riceverli nel token](howto-add-app-roles-in-azure-ad-apps.md) | <code>[<br>&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;"allowedMemberTypes": [<br>&emsp;&nbsp;&nbsp;&nbsp;"User"<br>&nbsp;&nbsp;&nbsp;],<br>&nbsp;&nbsp;&nbsp;"description":"Read-only access to device information",<br>&nbsp;&nbsp;&nbsp;"displayName":"Read Only",<br>&nbsp;&nbsp;&nbsp;"id":guid,<br>&nbsp;&nbsp;&nbsp;"isEnabled":true,<br>&nbsp;&nbsp;&nbsp;"value":"ReadOnly"<br>&nbsp;&nbsp;}<br>]</code>  |
| `displayName` | string | Nome visualizzato dell'app. <br><br> _Nota: È disponibile solo nell'esperienza delle App per le registrazioni (Legacy). Sostituito da `name` nella [registrazioni per l'App](https://go.microsoft.com/fwlink/?linkid=2083908) esperienza._ | `"MyRegisteredApp"` |
| `errorUrl` | string | Non è supportato. | |
| `groupMembershipClaims` | string | Configura l'attestazione `groups` rilasciata in un token di accesso utente oppure OAuth 2.0 previsto dall'app. Per impostare questo attributo, usare uno dei seguenti valori di stringa validi:<br/><br/>- `"None"`<br/>- `"SecurityGroup"` (per gruppi di sicurezza e ruoli di Azure AD)<br/>- `"All"` (verranno restituiti tutti i gruppi di sicurezza, i gruppi di distribuzione e i ruoli della directory di Azure AD a cui appartiene l'utente connesso. | `"SecurityGroup"` |
| `homepage` | string | URL della home page dell'applicazione. <br><br> _Nota: È disponibile solo nell'esperienza delle App per le registrazioni (Legacy). Sostituito da `signInUrl` nella [registrazioni per l'App](https://go.microsoft.com/fwlink/?linkid=2083908) esperienza._ | `"https://MyRegisteredApp"` |
| `objectId` | string | Identificatore univoco per l'app nella directory. <br><br> _Nota: È disponibile solo nell'esperienza delle App per le registrazioni (Legacy). Sostituito da `id` nella [registrazioni per l'App](https://go.microsoft.com/fwlink/?linkid=2083908) esperienza._ | `"f7f9acfc-ae0c-4d6c-b489-0a81dc1652dd"` |
| `optionalClaims` | string | Attestazioni facoltative restituite nel token dal servizio token di sicurezza per questa specifica app.<br>A questo punto, le app che supportano sia account personali che account Azure AD (registrati tramite il portale di registrazione delle app) non possono usare le attestazioni facoltative. Tuttavia, le app registrate solo per Azure AD usando l'endpoint v2.0 possono ottenere le attestazioni facoltative richieste nel manifesto. Per altre informazioni, vedere l'articolo relativo alle [attestazioni facoltative](active-directory-optional-claims.md). | `null` |
| `id` | string | Identificatore univoco per l'app nella directory. Questo ID non è l'identificatore usato per identificare l'app nelle transazioni di protocollo. Viene usato per fare riferimento all'oggetto nelle query di directory. | `"f7f9acfc-ae0c-4d6c-b489-0a81dc1652dd"` |
| `identifierUris` | String Array | URI definiti dall'utente che identificano in modo univoco un'app Web entro il rispettivo tenant di Azure AD oppure entro un dominio personalizzato verificato se l'app è multi-tenant. | <code>[<br>&nbsp;&nbsp;"https://MyRegisteredApp"<br>]</code> |
| `informationalUrls` | string | Specifica i collegamenti alle condizioni d'uso del servizio e all'informativa sulla privacy dell'app. Le condizioni per l'utilizzo del servizio e l'informativa sulla privacy vengono presentate agli utenti tramite l'esperienza di consenso dell'utente Per altre informazioni, vedere [Procedura: Aggiungere condizioni per l'utilizzo del servizio e informativa sulla privacy per le app di Azure AD registrate](howto-add-terms-of-service-privacy-statement.md). | <code>{<br>&nbsp;&nbsp;&nbsp;"marketing":"https://MyRegisteredApp/marketing",<br>&nbsp;&nbsp;&nbsp;"privacy":"https://MyRegisteredApp/privacystatement",<br>&nbsp;&nbsp;&nbsp;"support":"https://MyRegisteredApp/support",<br>&nbsp;&nbsp;&nbsp;"termsOfService":"https://MyRegisteredApp/termsofservice"<br>}</code> |
| `keyCredentials` | Raccolta | Contiene riferimenti a credenziali assegnate dall'app, segreti condivisi basati su stringa e certificati X.509. Queste credenziali sono utilizzate in fase di richiesta dei token di accesso (quando l'app funge da client, anziché da risorsa). | <code>[<br>&nbsp;{<br>&nbsp;&nbsp;&nbsp;"customKeyIdentifier":null,<br>&nbsp;&nbsp;&nbsp;"endDate":"2018-09-13T00:00:00Z",<br>&nbsp;&nbsp;&nbsp;"keyId":"\<guid>",<br>&nbsp;&nbsp;&nbsp;"startDate":"2017-09-12T00:00:00Z",<br>&nbsp;&nbsp;&nbsp;"type":"AsymmetricX509Cert",<br>&nbsp;&nbsp;&nbsp;"usage":"Verify",<br>&nbsp;&nbsp;&nbsp;"value":null<br>&nbsp;&nbsp;}<br>]</code> |
| `knownClientApplications` | String Array | Viene usato per unire il consenso se una soluzione contiene due parti, un'app client e un'app API Web personalizzata. Se si immette l'appID dell'app client in questo valore, l'utente deve fornire il consenso solo una volta per l'app client. Azure AD sa che il consenso al client implica il consenso all'API Web ed effettua automaticamente il provisioning delle entità servizio per il client e l'API Web contemporaneamente. Sia il client sia l'app dell'API Web devono essere registrati nello stesso tenant. | `["f7f9acfc-ae0c-4d6c-b489-0a81dc1652dd"]` |
| `logoUrl` | string | Valore di sola lettura che punta all'URL della rete CDN del logo caricato nel portale. | `"https://MyRegisteredAppLogo"` |
| `logoutUrl` | string | URL per disconnettersi dall'app. | `"https://MyRegisteredAppLogout"` |
| `name` | string | Nome visualizzato dell'app. | `"MyRegisteredApp"` |
| `oauth2AllowImplicitFlow` | Boolean | Specifica se questa app Web può richiedere token di accesso di flusso implicito OAuth 2.0. Il valore predefinito è false. Questo flag viene usato per le app basate su browser, ad esempio le app JavaScript a pagina singola. Per altre informazioni, immettere `OAuth 2.0 implicit grant flow` nel sommario e vedere gli argomenti sul flusso implicito. | `false` |
| `oauth2AllowIdTokenImplicitFlow` | Boolean | Specifica se questa app Web può richiedere token ID flusso implicito OAuth 2.0. Il valore predefinito è false. Questo flag viene usato per le app basate su browser, ad esempio le app JavaScript a pagina singola. | `false` |
| `oauth2Permissions` | Raccolta | Specifica la raccolta di ambiti di autorizzazione OAuth 2.0 che l'app dell'API Web (risorsa) espone alle app client. Questi ambiti di autorizzazione possono essere concessi alle app client durante il consenso. | <code>[<br>&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;"adminConsentDescription":"Allow the app to access resources on behalf of the signed-in user.",<br>&nbsp;&nbsp;&nbsp;"adminConsentDisplayName":"Access resource1",<br>&nbsp;&nbsp;&nbsp;"id":"\<guid>",<br>&nbsp;&nbsp;&nbsp;"isEnabled":true,<br>&nbsp;&nbsp;&nbsp;"type":"User",<br>&nbsp;&nbsp;&nbsp;"userConsentDescription":"Allow the app to access resource1 on your behalf.",<br>&nbsp;&nbsp;&nbsp;"userConsentDisplayName":"Access resources",<br>&nbsp;&nbsp;&nbsp;"value":"user_impersonation"<br>&nbsp;&nbsp;}<br>] </code>|
| `oauth2RequiredPostResponse` | Boolean | Specifica se, come parte delle richieste dei token OAuth 2.0, Azure AD consente richieste POST, anziché richieste GET. L'impostazione predefinita è false, che specifica che sono consentite solo richieste GET. | `false` |
| `parentalControlSettings` | string | `countriesBlockedForMinors` specifica i paesi in cui l'app è bloccata per i minori.<br>`legalAgeGroupRule` specifica la regola gruppo relativa all'età legale che si applica agli utenti dell'app. Può essere impostata su `Allow`, `RequireConsentForPrivacyServices`, `RequireConsentForMinors`, `RequireConsentForKids` o `BlockMinors`.  | <code>{<br>&nbsp;&nbsp;&nbsp;"countriesBlockedForMinors":[],<br>&nbsp;&nbsp;&nbsp;"legalAgeGroupRule":"Allow"<br>} </code> |
| `passwordCredentials` | Raccolta | Vedere la descrizione per la proprietà `keyCredentials`. | <code>[<br>&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;"customKeyIdentifier":null,<br>&nbsp;&nbsp;&nbsp;"endDate":"2018-10-19T17:59:59.6521653Z",<br>&nbsp;&nbsp;&nbsp;"keyId":"\<guid>",<br>&nbsp;&nbsp;&nbsp;"startDate":"2016-10-19T17:59:59.6521653Z",<br>&nbsp;&nbsp;&nbsp;"value":null<br>&nbsp;&nbsp;&nbsp;}<br>] </code> |
| `preAuthorizedApplications` | Raccolta | Elenca le applicazioni e le autorizzazioni necessarie per il consenso implicito. Richiede che un amministratore abbia fornito il consenso all'applicazione. preAuthorizedApplications non richiede il consenso utente alle autorizzazioni richieste. Le autorizzazioni elencate in preAuthorizedApplications non richiedono il consenso utente. Tuttavia, le autorizzazioni richieste aggiuntive non elencate in preAuthorizedApplications richiedono il consenso utente. | <code>[<br>&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;"appId": "abcdefg2-000a-1111-a0e5-812ed8dd72e8",<br>&nbsp;&nbsp;&nbsp;&nbsp;"permissionIds": [<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"8748f7db-21fe-4c83-8ab5-53033933c8f1"<br>&nbsp;&nbsp;&nbsp;&nbsp;]<br>&nbsp;&nbsp;}<br>]</code> |
| `publicClient` | Boolean | Specifica se l'applicazione è un client pubblico (ad esempio, un'applicazione installata in esecuzione in un dispositivo mobile). <br><br> _Nota: È disponibile solo nell'esperienza delle App per le registrazioni (Legacy). Sostituito da `allowPublicClient` nella [registrazioni per l'App](https://go.microsoft.com/fwlink/?linkid=2083908) esperienza._ | |
| `publisherDomain` | string | Il dominio autore verificato per l'applicazione. Sola lettura. | https://www.contoso.com |
| `replyUrls` | Matrice di stringhe | Questa proprietà multivalore contiene l'elenco dei valori redirect_uri registrati che Azure AD accetta come destinazioni in fase di restituzione dei token. <br><br> _Nota: È disponibile solo nell'esperienza delle App per le registrazioni (Legacy). Sostituito da `replyUrlsWithType` nella [registrazioni per l'App](https://go.microsoft.com/fwlink/?linkid=2083908) esperienza._ | |
| `replyUrlsWithType` | Raccolta | Questa proprietà multivalore contiene l'elenco dei valori redirect_uri registrati che Azure AD accetta come destinazioni in fase di restituzione dei token. Ogni valore di URI deve contenere un valore per il tipo di app associato. I valori supportati sono: `Web` e `InstalledClient`. | <code>"replyUrlsWithType":&nbsp;[<br>&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"url":&nbsp;"https://localhost:4400/services/office365/redirectTarget.html",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"type":&nbsp;"InstalledClient"&nbsp;&nbsp;&nbsp;<br>&nbsp;&nbsp;}<br>]</code> |
| `requiredResourceAccess` | Raccolta | Con il consenso dinamico, `requiredResourceAccess` attiva l'esperienza di consenso dell'amministratore e l'esperienza di consenso dell'utente per gli utenti che usano il consenso statico. Tuttavia, ciò non attiva l'esperienza di consenso dell'utente per i casi generici.<br>`resourceAppId` è l'identificatore univoco per la risorsa a cui l'app richiede l'accesso. Questo valore deve essere uguale all'appId dichiarato nell'app della risorsa di destinazione.<br>`resourceAccess` è una matrice che contiene l'elenco dei ruoli delle app e degli ambiti delle autorizzazioni OAuth 2.0 che l'app richiede dalla risorsa specificata. Contiene i valori di tipo `id` e `type` per le risorse specificate. | <code>[<br>&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;"resourceAppId":"00000002-0000-0000-c000-000000000000",<br>&nbsp;&nbsp;&nbsp;&nbsp;"resourceAccess":[<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id":"311a71cc-e848-46a1-bdf8-97ff7156d8e6",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"type":"Scope"<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}<br>&nbsp;&nbsp;&nbsp;&nbsp;]<br>&nbsp;&nbsp;}<br>] </code> |
| `samlMetadataUrl` | string | URL dei metadati SAML per l'app. | `https://MyRegisteredAppSAMLMetadata` |
| `signInUrl` | string | Specifica l'URL della home page dell'app. | `https://MyRegisteredApp` |
| `signInAudience` | string | Specifica gli account Microsoft supportati per l'applicazione corrente. I valori supportati sono:<ul><li>**AzureADMyOrg**: utenti con un account aziendale o dell'istituto di istruzione Microsoft nel tenant di Azure AD dell'organizzazione (tenant singolo)</li><li>**AzureADMultipleOrgs**: utenti con un account aziendale o dell'istituto di istruzione Microsoft nel tenant di Azure AD di qualsiasi organizzazione (multi-tenant)</li> <li>**AzureADandPersonalMicrosoftAccount**: utenti con un account Microsoft personale o un account aziendale o dell'istituto di istruzione nel tenant di Azure AD di qualsiasi organizzazione</li></ul> | `AzureADandPersonalMicrosoftAccount` |
| `tags` | String Array | Stringhe personalizzate che possono essere usate per classificare e identificare l'applicazione. | <code>[<br>&nbsp;&nbsp;"ProductionApp"<br>]</code> |

## <a name="common-issues"></a>Problemi comuni

### <a name="manifest-limits"></a>Manifesto limiti

Un manifesto dell'applicazione ha più attributi che vengono definiti gli insiemi. ad esempio, approles keycredentials, knownClientApplications, identifierUris, rediretUris, requiredResourceAccess e oauth2Permissions. Nel manifesto dell'applicazione completa per qualsiasi applicazione, il numero totale di voci in tutte le raccolte combinate è stato limitato di 1200. Se si dispone già di 100 redirect URI specificati nel manifesto dell'applicazione, si è solo a sinistra con 1100 rimanenti voci da utilizzare per tutte le altre raccolte combinati che costituiscono il manifesto.

> [!NOTE]
> Nel caso in cui si prova ad aggiungere voci oltre 1200 nel manifesto dell'applicazione, si potrebbe essere visualizzato un errore **"non è stato possibile aggiornare xxxxxx dell'applicazione. Dettagli dell'errore: Le dimensioni del manifesto ha superato il limite. Ridurre il numero di valori e ripetere la richiesta."**

### <a name="unsupported-attributes"></a>Attributi non supportati

Il manifesto dell'applicazione rappresenta lo schema del modello dell'applicazione sottostante in Azure AD. Poiché lo schema sottostante cambia, l'editor manifesto verrà aggiornato per riflettere il nuovo schema di tanto in tanto. Di conseguenza, è possibile riscontrare i nuovo attributi vengono visualizzati nel manifesto dell'applicazione. In rare occasioni, si noterà una modifica sintattica o semantica in attributi esistenti o è possibile trovare un attributo che esisteva in precedenza non sono più supportati. Ad esempio, si noterà nuovi attributi nel [registrazioni per l'App](https://go.microsoft.com/fwlink/?linkid=2083908) noti con un nome diverso nell'esperienza di registrazione (Legacy) dell'App.


| Registrazioni per l'App (Legacy)| Registrazioni per l'app           |
|---------------------------|-----------------------------|
| `availableToOtherTenants` | `signInAudience`            |
| `displayName`             | `name`                      |
| `errorUrl`                | -                           |
| `homepage`                | `signInUrl`                 |
| `objectId`                | `Id`                        |
| `publicClient`            | `allowPublicClient`         |
| `replyUrls`               | `replyUrlsWithType`         |

Per le descrizioni per questi attributi, vedere la [riferimento del manifesto](#manifest-reference) sezione.

Quando si prova a caricare un manifesto scaricato in precedenza, si può vedere uno degli errori seguenti. È probabile che l'editor manifesto supporta ora una versione più recente dello schema, che non corrisponde a quello che si sta provando a caricare.

- "**Non è stato possibile aggiornare l'applicazione xxxxxx. Dettagli errore: Identificatore di oggetto non valido 'undefined'. [].** "
- "**Non è stato possibile aggiornare l'applicazione xxxxxx. Dettagli errore: Uno o più valori delle proprietà specificati non sono validi. [].** "
- "**Non è stato possibile aggiornare l'applicazione xxxxxx. Dettagli errore: Non è consentito impostare availableToOtherTenants in questa versione dell'api per l'aggiornamento. [].** "
- "**Non è stato possibile aggiornare l'applicazione xxxxxx. Dettagli errore: Gli aggiornamenti alla proprietà 'replyUrls' non è consentita per questa applicazione. Usare la proprietà 'replyUrlsWithType'. [].** "
- "**Non è stato possibile aggiornare l'applicazione xxxxxx. Dettagli errore: È stato trovato un valore senza un nome di tipo ed non è disponibile alcun tipo previsto. Quando viene specificato il modello, ogni valore nel payload deve presentare un tipo che può essere specificato nel payload, in modo esplicito dal chiamante o dedotto in modo implicito dal valore padre. []**"

Quando si verifica uno di questi errori, si consiglia quanto segue:

1. Modificare gli attributi singolarmente nell'editor del manifesto invece di caricare un manifesto scaricato in precedenza. Usare la [riferimento del manifesto](#manifest-reference) tabella per comprendere la sintassi e semantica dei vecchi e nuovi attributi in modo che sia possibile modificare correttamente gli attributi si è interessati. 
1. Se il flusso di lavoro richiede di salvare i manifesti nel repository del codice sorgente per un uso futuro, è consigliabile la riassegnazione i manifesti salvati nel repository con quella presenti il **registrazioni per l'App** esperienza.

## <a name="next-steps"></a>Passaggi successivi

* Per altre informazioni sulla relazione tra applicazione e oggetti entità servizio di un'app, vedi [dell'applicazione e oggetti entità servizio in Azure AD](app-objects-and-service-principals.md).
* Vedere le [glossario per gli sviluppatori di Microsoft identity platform](developer-glossary.md) per le definizioni di alcuni concetti di base Microsoft identity platform developer.

Usare la sezione dei commenti seguente per offrire commenti e suggerimenti utili per migliorare e organizzare i contenuti disponibili.

<!--article references -->
[AAD-APP-OBJECTS]:app-objects-and-service-principals.md
[AAD-DEVELOPER-GLOSSARY]:developer-glossary.md
[AAD-GROUPS-FOR-AUTHORIZATION]: http://www.dushyantgill.com/blog/2014/12/10/authorization-cloud-applications-using-ad-groups/
[ADD-UPD-RMV-APP]:quickstart-v1-integrate-apps-with-azure-ad.md
[APPLICATION-ENTITY]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[APPLICATION-ENTITY-APP-ROLE]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type
[APPLICATION-ENTITY-OAUTH2-PERMISSION]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type
[AZURE-PORTAL]: https://portal.azure.com
[DEV-GUIDE-TO-AUTH-WITH-ARM]: http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/
[GRAPH-API]: active-directory-graph-api.md
[IMPLICIT-GRANT]:v1-oauth2-implicit-grant-flow.md
[INTEGRATING-APPLICATIONS-AAD]: https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
[O365-PERM-DETAILS]: https://msdn.microsoft.com/office/office365/HowTo/application-manifest
[O365-SERVICE-DAEMON-APPS]: https://msdn.microsoft.com/office/office365/howto/building-service-apps-in-office-365
[RBAC-CLOUD-APPS-AZUREAD]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
