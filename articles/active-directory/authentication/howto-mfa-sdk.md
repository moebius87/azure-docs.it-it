---
title: Azure software development kit MFA per le app personalizzate - Azure Active Directory
description: In questo articolo viene spiegato come scaricare e usare l'SDK MFA di Azure per abilitare la verifica in due passaggi per le app personalizzate.
services: multi-factor-authentication
ms.service: active-directory
ms.subservice: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: michmcla
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b6f5def70dcb2564e92c04e53b5d2ef5f0631fd
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60414886"
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a>Compilazione di Multi-Factor Authentication in app personalizzate (SDK)

> [!IMPORTANT]
> Azure Multi-Factor Authentication Software Development Kit (SDK) è deprecato. Questa funzionalità non è più supportata per i nuovi clienti. I clienti correnti possono continuare a usare l'SDK fino al 14 novembre 2018. Dopo tale periodo, le chiamate all'SDK avranno esito negativo. 

Il Software Development Kit (SDK) di Azure Multi-Factor Authentication consente di compilare la verifica in due passaggi direttamente nei processi di accesso o di transazione delle applicazioni nel tenant di Azure AD.

L'SDK di Multi-Factor Authentication è disponibile per C#, Visual Basic (.NET), Java, Perl, PHP e Ruby. L'SDK fornisce un wrapper sottile per la verifica in due passaggi. Include tutto ciò che occorre per scrivere il codice, inclusi i file di codice sorgente commentati, i file di esempio e un file ReadMe dettagliato. Ogni SDK include anche un certificato e una chiave privata univoci per il provider Multi-Factor Authentication per crittografare le transazioni. Fino a quando si dispone di un provider, è possibile scaricare l'SDK in tutti i formati e le lingue necessari.

La struttura delle API nell'SDK di Multi-Factor Authentication è semplice. Eseguire una sola funzione di chiamata a un'API con i parametri di opzione a più fattori (ad esempio la modalità di verifica) e dati utente (come il numero di telefono da chiamare o il numero PIN da convalidare). Le API convertono la chiamata di funzione in richieste di servizi web per il servizio Azure Multi-Factor Authentication. Tutte le chiamate devono includere un riferimento al certificato privato incluso in ogni SDK.

Poiché le API non hanno accesso agli utenti registrati in Azure Active Directory, è necessario fornire le informazioni sull'utente in un file o database. Inoltre, le API non forniscono funzionalità di gestione di registrazione o dell'utente, pertanto è necessario creare questi processi nell'applicazione.

> [!IMPORTANT]
> Per scaricare l'SDK, è necessario creare un provider di Azure Multi-Factor Authentication, anche se si dispone di licenze di Azure MFA, AAD Premium o EMS. Se si crea un provider di Azure Multi-Factor Authentication a tale scopo e si dispone già di licenze, creare il provider con il modello **Per utente abilitato**. Collegare quindi il Provider alla directory contenente le licenze di Azure MFA, Azure AD Premium o EMS. Con questa configurazione verranno eseguiti addebiti solo se il numero di utenti singoli che usano l'SDK è maggiore del numero di licenze possedute.


## <a name="download-the-sdk"></a>Scaricare l'SDK
Per scaricare l'SDK Multi-Factor di Azure è necessario un [provider di Multi-Factor Authentication](concept-mfa-authprovider.md).  Questo richiede una sottoscrizione di Azure completa, anche se si possiedono licenze di Azure MFA, Azure AD Premium o Enterprise Mobility Suite. I metodi pubblici di download dell'SDK sono stati ritirati da quando l'SDK è stato deprecato. Se è necessario scaricare l'SDK, è consigliabile aprire un caso di supporto presso Microsoft. L'SDK è offerto solo ai clienti che già stanno usando l'SDK. Non è previsto l'onboarding di nuovi clienti.

## <a name="whats-in-the-sdk"></a>Contenuto dell'SDK
L'SDK include gli elementi seguenti:

* **README**. Viene illustrato come usare le API di Multi-Factor Authentication in un'applicazione nuova o esistente.
* **File di origine** per Multi-Factor Authentication
* **Certificato client** usato per comunicare con il servizio Multi-Factor Authentication
* **Chiave privata** per il certificato
* **Risultati delle chiamate.**  Un elenco di codici risultato chiamata. Per aprire questo file, usare un'applicazione con formattazione del testo, come ad esempio WordPad. Usare i codici risultato chiamata per verificare e risolvere l'implementazione di autenticazione Multi-Factor Authentication nell'applicazione. Non sono codici di stato di autenticazione.
* **Esempi.**  Codice di esempio per un'implementazione di base funzionante di Multi-Factor Authentication.

> [!WARNING]
> Il certificato client è un certificato privato univoco generato per un utente specifico. Non condividere o perdere questo file. È la chiave per garantire la sicurezza delle comunicazioni con il servizio di autenticazione Multi-Factor Authentication.

## <a name="code-sample"></a>Esempio di codice
Questo esempio di codice illustra come usare le API nell'SDK di Azure Multi-Factor Authentication per aggiungere all'applicazione una verifica tramite chiamata vocale in modalità standard. La modalità standard è una telefonata a cui l'utente risponde premendo il tasto #.

In questo esempio viene usato l'SDK di Multi-Factor Authentication C# .NET 2.0 in un'applicazione ASP.NET con logica sul lato server C#, ma il processo è simile in altri linguaggi. Poiché l'SDK include file di origine, file non eseguibili, è possibile compilare i file e farvi riferimento o includerli direttamente nell'applicazione.

> [!NOTE]
> Quando si implementa Multi-Factor Authentication, usare i metodi aggiuntivi (telefonata o SMS) come verifica secondaria o terziaria per integrare il metodo di autenticazione principale (nome utente e password). Questi metodi non sono progettati come metodi di autenticazione principale.

### <a name="code-sample-overview"></a>Panoramica dell'esempio di codice
Questo codice di esempio per un'applicazione demo Web semplice usa una chiamata con risposta mediante il tasto # per verificare l'autenticazione dell'utente. Questo fattore telefonata è noto in Multi-Factor Authentication come modalità standard.

Il codice sul lato client non include elementi specifici di autenticazione Multi-Factor Authentication. Poiché i fattori di autenticazione aggiuntivi sono indipendenti dall'autenticazione principale, è possibile aggiungerli senza modificare l'interfaccia di accesso esistente. Le API negli SDK di Multi-Factor consentono di personalizzare l'esperienza dell'utente, ma potrebbe non essere necessario apportare alcuna modifica.

Il codice lato server aggiunge l'autenticazione in modalità standard nel passaggio 2. Crea un oggetto PfAuthParams con i parametri necessari per la verifica della modalità standard: nome utente, numero, modalità e il percorso verso il certificato del client (CertFilePath), che è necessario in ogni chiamata. Per una dimostrazione di tutti i parametri in PfAuthParams, vedere il file di esempio nel SDK.

Successivamente, il codice passa l'oggetto PfAuthParams alla funzione pf_authenticate(). Il valore restituito indica l'esito positivo o negativo dell'autenticazione. I parametri out, callStatus ed errorID, contengono informazioni aggiuntive sul risultato della chiamata. I codici di risultato della chiamata sono documentati nel file dei risultati della chiamata nel SDK.

Questa implementazione minima può essere scritta in poche righe. Nel codice di produzione, tuttavia, è necessario includere la gestione degli errori più sofisticati, il codice di database aggiuntivo e un'esperienza utente avanzata.

### <a name="web-client-code"></a>Codice client web
Di seguito è riportato il codice di client web per una pagina demo.

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="https://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a>Codice lato server
Nel seguente codice lato server, la Multi-Factor Authentication è configurata ed eseguita nel passaggio 2. La modalità standard (MODE_STANDARD) è una telefonata a cui l'utente risponde premendo il tasto #.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate the username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from the user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains the private key for the client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
