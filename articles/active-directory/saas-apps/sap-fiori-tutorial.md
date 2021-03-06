---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP Fiori | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SAP Fiori.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.reviewer: barbkess
ms.assetid: 77ad13bf-e56b-4063-97d0-c82a19da9d56
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 03/11/2019
ms.author: jeedes
ms.openlocfilehash: e94fe3156677a507eab91eee339ed29bf7b4ad2e
ms.sourcegitcommit: c174d408a5522b58160e17a87d2b6ef4482a6694
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "59257638"
---
# <a name="tutorial-azure-active-directory-integration-with-sap-fiori"></a>Esercitazione: Integrazione di Azure Active Directory con SAP Fiori

Questa esercitazione descrive come integrare SAP Fiori con Azure Active Directory (Azure AD).
L'integrazione di SAP Fiori con Azure AD offre i vantaggi seguenti:

* È possibile controllare in Azure AD chi può accedere a SAP Fiori.
* È possibile abilitare gli utenti per l'accesso automatico (Single Sign-On) a SAP Fiori con gli account Azure AD personali.
* È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis).
Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con SAP Fiori, sono necessari gli elementi seguenti:

* Una sottoscrizione di Azure AD. Se non si dispone di un ambiente di Azure AD, è possibile ottenere un [account gratuito](https://azure.microsoft.com/free/).
* Sottoscrizione di SAP Fiori abilitata per l'accesso Single Sign-On
* SAP Fiori 7.20 (versione minima)

## <a name="scenario-description"></a>Descrizione dello scenario

In questa esercitazione vengono eseguiti la configurazione e il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.

* SAP Fiori supporta l'accesso SSO avviato da **SP**

## <a name="adding-sap-fiori-from-the-gallery"></a>Aggiunta di SAP Fiori dalla raccolta

Per configurare l'integrazione di SAP Fiori in Azure AD, è necessario aggiungere SAP Fiori dalla raccolta all'elenco di app SaaS gestite.

**Per aggiungere SAP Fiori dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Pulsante Azure Active Directory](common/select-azuread.png)

2. Passare ad **Applicazioni aziendali** e quindi selezionare l'opzione **Tutte le applicazioni**.

    ![Pannello Applicazioni aziendali](common/enterprise-applications.png)

3. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![Pulsante Nuova applicazione](common/add-new-app.png)

4. Nella casella di ricerca digitare **SAP Fiori** selezionare **SAP Fiori** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

     ![SAP Fiori nell'elenco risultati](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAP Fiori usando un utente di test di nome **Britta Simon**.
Per il corretto funzionamento dell'accesso Single Sign-On, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SAP Fiori.

Per configurare e testare l'accesso Single Sign-On di Azure AD con SAP Fiori, è necessario completare le procedure di base seguenti:

1. **[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.
2. **[Configurare l'accesso Single Sign-On di SAP Fiori](#configure-sap-fiori-single-sign-on)**: per configurare le impostazioni di Single Sign-On sul lato applicazione.
3. **[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
4. **[Assegnare l'utente di test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Creare l'utente di test di SAP Fiori](#create-sap-fiori-test-user)**: per avere una controparte di Britta Simon in SAP Fiori collegata alla rappresentazione dell'utente in Azure AD.
6. **[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure.

Per configurare l'accesso Single Sign-On di Azure AD con SAP Fiori, seguire questa procedura:

1. Aprire un'altra finestra del Web browser accedere al sito aziendale di SAP Fiori come amministratore.

2. Assicurarsi che i servizi **http** e **https** siano attivi e che le porte appropriate siano assegnate nel codice di transazione **SMICM**.

3. Accedere al client aziendale del sistema SAP (T01) in cui SSO è obbligatorio e attivare la gestione della sessione di sicurezza HTTP.

    a. Passare al codice di transazione **SICF_SESSIONS**. Questo codice mostra tutti i parametri di profilo rilevanti con i valori correnti. L'aspetto è simile al seguente:
    ```
    login/create_sso2_ticket = 2
    login/accept_sso2_ticket = 1
    login/ticketcache_entries_max = 1000
    login/ticketcache_off = 0  login/ticket_only_by_https = 0 
    icf/set_HTTPonly_flag_on_cookies = 3
    icf/user_recheck = 0  http/security_session_timeout = 1800
    http/security_context_cache_size = 2500
    rdisp/plugin_auto_logout = 1800
    rdisp/autothtime = 60
    ```
    >[!NOTE]
    > Modificare i parametri indicati sopra in base alle esigenze dell'organizzazione. I valori precedenti sono solo a scopo illustrativo.

    b. Se necessario, modificare i parametri nel profilo predefinito/dell'istanza per il sistema SAP e riavviare il sistema SAP.

    c. Fare doppio clic sul client appropriato per abilitare la sessione di sicurezza HTTP.

    ![Collegamento di download del certificato](./media/sapfiori-tutorial/tutorial-sapnetweaver-profileparameter.png)

    d. Attivare i servizi SICF seguenti:
    ```
    /sap/public/bc/sec/saml2
    /sap/public/bc/sec/cdc_ext_service
    /sap/bc/webdynpro/sap/saml2
    /sap/bc/webdynpro/sap/sec_diag_tool (This is only to enable / disable trace)
    ```
4. Passare al codice di transazione **SAML2** nel client aziendale del sistema SAP [T01/122]. Verrà aperta un'interfaccia utente in un browser. In questo esempio si presuppone che il client aziendale SAP sia 122.

    ![Collegamento di download del certificato](./media/sapfiori-tutorial/tutorial-sapnetweaver-sapbusinessclient.png)

5. Fornire il nome utente e la password da immettere nell'interfaccia utente e fare clic su **Edit** (Modifica).

    ![Collegamento di download del certificato](./media/sapfiori-tutorial/tutorial-sapnetweaver-userpwd.png)

6. Sostituire **Provider Name** (Nome provider) T01122 con `http://T01122` e fare clic su **Save** (Salva).

    > [!NOTE]
    > Per impostazione predefinita, il nome del provider viene visualizzato nel formato <sid><client>, ma in Azure AD il nome deve essere specificato nel formato <protocol>://<name> mantenendo il nome del provider https://<sid><client> per consentire la configurazione di più motori ABAP di SAP Fiori in Azure AD.

    ![Collegamento di download del certificato](./media/sapfiori-tutorial/tutorial-sapnetweaver-providername.png)

7. **Generazione di metadati del provider di servizi**: una volta completata la configurazione delle impostazioni di **Local Provider** (Provider locale) e **Trusted Providers** (Provider attendibili) nell'interfaccia utente di SAML 2.0, il passaggio successivo consiste nel generare il file di metadati del provider di servizi (che contiene tutte le impostazioni, i contesti di autenticazione e altre configurazioni di SAP). Una volta generato il file, è necessario caricarlo in Azure AD.

    ![Collegamento di download del certificato](./media/sapfiori-tutorial/tutorial-sapnetweaver-generatesp.png)

    a. Passare alla scheda **Local Provider** (Provider locale).

    b. Fare clic su **Metadata** (Metadati).

    c. Salvare il **file XML dei metadati** nel computer e caricarlo nella sezione **Configurazione SAML di base** per inserire automaticamente i valori di **Identificatore** e **URL di risposta** nel portale di Azure.

8. Nella pagina di integrazione dell'applicazione **SAP Fiori** del [portale di Azure](https://portal.azure.com/) selezionare **Single Sign-On**.

    ![Collegamento Configura accesso Single Sign-On](common/select-sso.png)

9. Nella finestra di dialogo **Selezionare un metodo di accesso Single Sign-On** selezionare la modalità **SAML/WS-Fed** per abilitare il Single Sign-On.

    ![Selezione della modalità Single Sign-On](common/select-saml-option.png)

10. Nella pagina **Configura l'accesso Single Sign-On con SAML** fare clic sull'icona **Modifica** per aprire la finestra di dialogo **Configurazione SAML di base**.

    ![Modificare la configurazione SAML di base](common/edit-urls.png)

11. Nella sezione **Configurazione SAML di base** seguire questa procedura:

    a. Fare clic su **Carica file di metadati** per caricare il **file di metadati del provider di servizi** ottenuto in precedenza.

    ![Caricare file di metadati](common/upload-metadata.png)

    b. Fare clic su **logo cartella** per selezionare il file di metadati e fare quindi clic su **Upload**.

    ![Scegliere file di metadati](common/browse-upload-metadata.png)

    c. Al termine del caricamento del file di metadati, i valori di **Identificatore** e **URL di risposta** vengono inseriti automaticamente nella casella di testo della sezione **Configurazione SAML di base**, come illustrato di seguito:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di SAP Fiori](common/sp-identifier-reply.png)

    d. Nella casella di testo **URL accesso** digitare un URL nel formato seguente: `https://<your company instance of SAP Fiori>`

    > [!NOTE]
    > Alcuni clienti hanno segnalato un errore di configurazione non valida dell'URL di risposta per la propria istanza. Se viene visualizzato un tale errore, è possibile usare lo script di PowerShell seguente come metodo alternativo per impostare l'URL di risposta corretto per l'istanza:
    ```
    Set-AzureADServicePrincipal -ObjectId $ServicePrincipalObjectId -ReplyUrls "<Your Correct Reply URL(s)>"
    ``` 
    > È prima necessario impostare manualmente l'ID oggetto entità servizio; in alternativa è possibile passarlo anche qui.

12. L'applicazione SAP Fiori prevede un formato specifico per le asserzioni SAML. Configurare le attestazioni seguenti per questa applicazione. È possibile gestire i valori di questi attributi dalla sezione **Attributi utente** nella pagina di integrazione dell'applicazione. Nella pagina **Configura l'accesso Single Sign-On con SAML** fare clic sul pulsante **Modifica** per aprire la finestra di dialogo **Attributi utente**.

    ![image](common/edit-attribute.png)

13. Nella sezione **Attestazioni utente** della finestra di dialogo **Attributi utente** configurare l'attributo del token SAML come mostrato nell'immagine precedente e seguire questa procedura:

    a. Fare clic sull'**icona Modifica** per aprire la finestra di dialogo **Gestisci attestazioni utente**.

    ![image](./media/sapfiori-tutorial/nameidattribute.png)

    ![image](./media/sapfiori-tutorial/nameidattribute1.png)

    b. Nell'elenco **Trasformazione** selezionare **ExtractMailPrefix()**.

    c. Nell'elenco **Parametro 1** selezionare **user.userprinicipalname**.

    d. Fare clic su **Save**.

14. Nella pagina **Configura l'accesso Single Sign-On con SAML**, nella sezione **Certificato di firma SAML**, fare clic su **Scarica** per scaricare il file **XML metadati federazione** definito dalle opzioni specificate in base ai propri requisiti e salvarlo in questo computer.

    ![Collegamento di download del certificato](common/metadataxml.png)

15. Nella sezione **Configura SAP Fiori** copiare gli URL appropriati in base alle esigenze.

    ![Copiare gli URL di configurazione](common/copy-configuration-urls.png)

    a. URL di accesso

    b. Identificatore Azure AD

    c. URL di chiusura sessione

### <a name="configure-sap-fiori-single-sign-on"></a>Configurare l'accesso Single Sign-On di SAP Fiori

1. Accedere al sistema SAP e passare al codice transazione SAML2. Verrà visualizzata una nuova finestra del browser con la schermata di configurazione SAML.

2. Per la configurazione degli endpoint per i provider di identità attendibili (Azure AD), passare alla scheda **Trusted Providers** (Provider attendibili).

    ![Configure Single Sign-On](./media/sapfiori-tutorial/tutorial-sapnetweaver-samlconfig.png)

3. Premere **Add** (Aggiungi) e scegliere **Upload Metadata File** (Carica file di metadati) dal menu di scelta rapida.

    ![Configure Single Sign-On](./media/sapfiori-tutorial/tutorial-sapnetweaver-uploadmetadata.png)

4. Caricare il file di metadati scaricato dal portale di Azure.

    ![Configure Single Sign-On](./media/sapfiori-tutorial/tutorial-sapnetweaver-metadatafile.png)

5. Nella schermata successiva digitare il nome dell'alias. Digitare ad esempio aadsts e premere **Next** (Avanti) per continuare.

    ![Configure Single Sign-On](./media/sapfiori-tutorial/tutorial-sapnetweaver-aliasname.png)

6. Assicurarsi che il valore di **Digest Algorithm** (Algoritmo digest) sia **SHA-256** e che non siano necessarie modifiche e premere **Next** (Avanti).

    ![Configure Single Sign-On](./media/sapfiori-tutorial/tutorial-sapnetweaver-identityprovider.png)

7. In **Single Sign-On Endpoints** (Endpoint Single Sign-On) selezionare **HTTP POST** e fare clic su **Next** (Avanti) per continuare.

    ![Configure Single Sign-On](./media/sapfiori-tutorial/tutorial-sapnetweaver-httpredirect.png)

8. In **Single Logout Endpoints** (Endpoint punto di disconnessione singolo) selezionare **HTTPRedirect** e fare clic su **Next** (Avanti) per continuare.

    ![Configure Single Sign-On](./media/sapfiori-tutorial/tutorial-sapnetweaver-httpredirect1.png)

9. In **Artifact Endpoints** (Endpoint artefatto) premere **Next** (Avanti) per continuare.

    ![Configure Single Sign-On](./media/sapfiori-tutorial/tutorial-sapnetweaver-artifactendpoint.png)

10. In **Authentication Requirements** (Requisiti di autenticazione) fare clic su **Finish** (Fine).

    ![Configure Single Sign-On](./media/sapfiori-tutorial/tutorial-sapnetweaver-authentication.png)

11. Passare alla scheda **Trusted Providers** > **Identity Federation** (Provider attendibili > Federazione identità), nella parte inferiore dello schermo. Fare clic su **Modifica**.

    ![Configure Single Sign-On](./media/sapfiori-tutorial/tutorial-sapnetweaver-trustedprovider.png)

12. Fare clic su **Add** (Aggiungi) sotto **Identity Federation** (Federazione identità), nella finestra inferiore.

    ![Configure Single Sign-On](./media/sapfiori-tutorial/tutorial-sapnetweaver-addidentityprovider.png)

13. Nella finestra popup selezionare **Unspecified** (Non specificato) in **Supported NameID formats** (Formati NameID supportati) e fare clic su OK.

    ![Configure Single Sign-On](./media/sapfiori-tutorial/tutorial-sapnetweaver-nameid.png)

14. Si noti che i valori **user ID Source** (Origine ID utente) e **user ID mapping mode** (Modalità mapping ID utente) determinano il collegamento tra l'utente SAP e l'attestazione di Azure AD.  

    #### <a name="scenario-sap-user-to-azure-ad-user-mapping"></a>Scenario: Mapping tra utente SAP e utente di Azure AD.

    a. Screenshot dei dettagli di NameID in SAP.

    ![Configure Single Sign-On](./media/sapfiori-tutorial/nameiddetails.png)

    b. Screenshot con l'indicazione delle attestazioni necessarie in Azure AD.

    ![Configure Single Sign-On](./media/sapfiori-tutorial/claimsaad1.png)

    #### <a name="scenario-select-sap-user-id-based-on-configured-email-address-in-su01-in-this-case-email-id-should-be-configured-in-su01-for-each-user-who-requires-sso"></a>Scenario: Selezionare l'ID utente SAP usando l'indirizzo di posta elettronica configurato in SU01. In questo caso l'ID posta elettronica deve essere configurato in SU01 per ogni utente che richiede l'accesso SSO.

    a.  Screenshot dei dettagli di NameID in SAP.

    ![Configure Single Sign-On](./media/sapfiori-tutorial/tutorial-sapnetweaver-nameiddetails1.png)

    b. Screenshot con l'indicazione delle attestazioni necessarie in Azure AD.

    ![Configure Single Sign-On](./media/sapfiori-tutorial/claimsaad2.png)

15. Fare clic su **Save** (Salva) e quindi su **Enable** (Abilita) per abilitare il provider di identità.

    ![Configure Single Sign-On](./media/sapfiori-tutorial/configuration1.png)

16. Quando richiesto, fare clic su **OK**.

    ![Configure Single Sign-On](./media/sapfiori-tutorial/configuration2.png)

### <a name="create-an-azure-ad-test-user"></a>Creare un utente di test di Azure AD

Questa sezione descrive come creare un utente di test denominato Britta Simon nel portale di Azure.

1. Nel riquadro sinistro del portale di Azure, selezionare **Azure Active Directory**, **Utenti** e quindi **Tutti gli utenti**.

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](common/users.png)

2. Selezionare **Nuovo utente** in alto nella schermata.

    ![Pulsante Nuovo utente](common/new-user.png)

3. In Proprietà utente seguire questa procedura.

    ![Finestra di dialogo Utente](common/user-properties.png)

    a. Nel campo **Nome** immettere **BrittaSimon**.
  
    b. Nel campo **Nome utente** digitare `brittasimon@yourcompanydomain.extension`. Ad esempio: BrittaSimon@contoso.com.

    c. Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella Password.

    d. Fare clic su **Create**(Crea).

### <a name="assign-the-azure-ad-test-user"></a>Assegnare l'utente di test di Azure AD

In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a SAP Fiori.

1. Nel portale di Azure selezionare **Applicazioni aziendali**, quindi **Tutte le applicazioni** e infine **SAP Fiori**.

    ![Pannello delle applicazioni aziendali](common/enterprise-applications.png)

2. Nell'elenco delle applicazioni selezionare **SAP Fiori**.

    ![Collegamento di SAP Fiori nell'elenco delle applicazioni](common/all-applications.png)

3. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Collegamento "Utenti e gruppi"](common/users-groups-blade.png)

4. Fare clic sul pulsante **Aggiungi utente** e quindi selezionare **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Riquadro Aggiungi assegnazione](common/add-assign-user.png)

5. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti e quindi fare clic sul pulsante **Seleziona** in basso nella schermata.

6. Se si prevede un valore di ruolo nell'asserzione SAML, nella finestra di dialogo **Selezionare un ruolo** selezionare il ruolo appropriato per l'utente dall'elenco, quindi fare clic sul pulsante **Seleziona** nella parte inferiore della schermata.

7. Nella finestra di dialogo **Aggiungi assegnazione** fare clic sul pulsante **Assegna**.

### <a name="create-sap-fiori-test-user"></a>Creare l'utente di test di SAP Fiori

In questa sezione viene creato un utente di nome Britta Simon in SAP Fiori. Collaborare con il team di esperti SAP interno o con il partner SAP dell'organizzazione per aggiungere gli utenti alla piattaforma SAP Fiori.

### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

1. Una volta attivato il provider di identità Azure AD, provare ad accedere all'URL seguente per controllare l'accesso Single Sign-On (non verranno richiesti nome utente e password)

    `https://<sapurl>/sap/bc/bsp/sap/it00/default.htm`

    (oppure) usare l'URL seguente

    `https://<sapurl>/sap/bc/bsp/sap/it00/default.htm`

    > [!NOTE]
    > Sostituire sapurl con il nome host SAP effettivo.

2. L'URL precedente dovrebbe consentire di visualizzare la schermata illustrata sotto. Se viene visualizzata la pagina seguente, la configurazione dell'accesso Single Sign-On di Azure AD è stata eseguita correttamente.

    ![Configure Single Sign-On](./media/sapfiori-tutorial/testingsso.png)

3. Se vengono richiesti nome utente e password, diagnosticare il problema abilitando la traccia tramite l'URL seguente

    `https://<sapurl>/sap/bc/webdynpro/sap/sec_diag_tool?sap-client=122&sap-language=EN#`

## <a name="additional-resources"></a>Risorse aggiuntive

- [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Che cos'è l'accesso condizionale in Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)