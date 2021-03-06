---
title: 'Esercitazione: Integrazione di Azure Active Directory con xMatters OnDemand | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e xMatters OnDemand.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2018
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b5ec711f0e43d9d29d962d43ed8b1d86338db87
ms.sourcegitcommit: 61c8de2e95011c094af18fdf679d5efe5069197b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62114943"
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a>Esercitazione: Integrazione di Azure Active Directory con xMatters OnDemand

Questa esercitazione descrive come integrare xMatters OnDemand con Azure Active Directory (Azure AD).

L'integrazione di xMatters OnDemand con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a xMatters OnDemand
- È possibile abilitare gli utenti per l'accesso automatico Single Sign-On a xMatters OnDemand con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con xMatters OnDemand sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di xMatters OnDemand abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di xMatters OnDemand dalla raccolta
1. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-xmatters-ondemand-from-the-gallery"></a>Aggiunta di xMatters OnDemand dalla raccolta
Per configurare l'integrazione di xMatters OnDemand in Azure AD è necessario aggiungere xMatters OnDemand dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere xMatters OnDemand dalla raccolta seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

1. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![APPLICAZIONI][2]
    
1. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![APPLICAZIONI][3]

1. Nella casella di ricerca digitare **xMatters OnDemand**.

    ![Creazione di un utente test di Azure AD](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

1. Nel pannello dei risultati selezionare **xMatters OnDemand** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con xMatters OnDemand usando un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di xMatters OnDemand corrisponde a un determinato utente di Azure AD. In altre parole è necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in xMatters OnDemand.

Per stabilire la relazione di collegamento, in xMatters OnDemand assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con xMatters OnDemand è necessario completare i blocchi predefiniti seguenti:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.
1. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
1. **[Creazione di un utente test di xMatters OnDemand](#creating-a-xmatters-ondemand-test-user)**: per avere una controparte di Britta Simon in xMatters OnDemand collegata alla rappresentazione dell'utente in Azure AD.
1. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione xMatters OnDemand.

**Per configurare l'accesso Single Sign-On di Azure AD con xMatters OnDemand, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **xMatters OnDemand** del portale di Azure fare clic su **Single Sign-On**.

    ![Configure Single Sign-On][4]

1. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.

    ![Configure Single Sign-On](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

1. Nella sezione **URL e dominio xMatters OnDemand** seguire questa procedura:

    ![Configure Single Sign-On](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    a. Nella casella di testo **Identificatore** digitare l'URL adottando il criterio seguente:

    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    b. Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente:
    
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > Poiché questi non sono i valori reali, è necessario aggiornarli con l'identificatore e l'URL di risposta effettivi. Per ottenere questi valori, contattare il [team di supporto di xMatters OnDemand](https://www.xmatters.com/company/contact-us/).

1. Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato in locale come **c:\\XMatters OnDemand.cer**.

    ![Configure Single Sign-On](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)

    > [!IMPORTANT]
    > Inoltrare il certificato al [team di supporto di xMatters OnDemand](https://www.xmatters.com/company/contact-us/). Per poter completare la configurazione di Single Sign-On, è necessario che il certificato venga caricato dal team di supporto xMatters. 

1. Fare clic sul pulsante **Salva** .

    ![Configure Single Sign-On](./media/xmatters-ondemand-tutorial/tutorial_general_400.png)

1. Nella sezione **Configurazione di xMatters OnDemand** fare clic su **Configura xMatters OnDemand** per aprire la finestra **Configura accesso**. Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**

    ![Configure Single Sign-On](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

1. In un'altra finestra del Web browser accedere al sito aziendale di XMatters OnDemand come amministratore.

1. Sulla barra degli strumenti in alto fare clic su **Admin** e quindi su **Company Details** (Dettagli società) sulla barra di spostamento a sinistra.

    ![Amministratore](./media/xmatters-ondemand-tutorial/IC776795.png "Amministratore")

1. Nella pagina **Configurazione SAML** seguire la procedura seguente:

    ![Configurazione SAML](./media/xmatters-ondemand-tutorial/IC776796.png "Configurazione SAML")

    a. Selezionare **Enable SAML**.

    b. Nella casella di testo **ID provider di identità** incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure.

    c. Nella casella di testo **URL Single Sign-On** incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.

    d. Nella casella di testo **Single Logout URL** (URL di disconnessione singola), incollare l'**URL di disconnessione** copiato dal portale di Azure.

    e. Nella parte superiore della pagina Informazioni sull’azienda fare clic su **Salva modifiche**.

    ![Dettagli dell'azienda](./media/xmatters-ondemand-tutorial/IC776797.png "Dettagli dell'azienda")

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/xmatters-ondemand-tutorial/create_aaduser_01.png) 

1. Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.

    ![Creazione di un utente test di Azure AD](./media/xmatters-ondemand-tutorial/create_aaduser_02.png) 

1. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.

    ![Creazione di un utente test di Azure AD](./media/xmatters-ondemand-tutorial/create_aaduser_03.png) 

1. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:

    ![Creazione di un utente test di Azure AD](./media/xmatters-ondemand-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Create**(Crea).

### <a name="creating-a-xmatters-ondemand-test-user"></a>Creazione di un utente test di xMatters OnDemand

L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in xMatters OnDemand.

**Per creare un utente manualmente, seguire questa procedura:**

1. Accedere al tenant di **XMatters OnDemand** .

1. Fare clic sulla scheda **Users** (Utenti) e quindi fare clic su **Add User** (Aggiungi utente).

   ![Utenti](./media/xmatters-ondemand-tutorial/IC781048.png "Utenti")

1. Nella sezione **Aggiungi un utente** eseguire la procedura seguente:

    ![Aggiungere un utente](./media/xmatters-ondemand-tutorial/IC781049.png "Aggiungere un utente")

    a. Selezionare **Active**.

    b. Nella casella di testo **User ID** (ID utente) digitare l'ID dell'utente, ad esempio Brittasimon@contoso.com.

    c. Digitare il nome dell'utente, ad esempio Britta, nella casella di testo **First Name** (Nome).

    d. Digitare il cognome dell'utente, ad esempio Simon, nella casella di testo **Last Name** (Cognome).

    e. Nella casella di testo **Site** (Sito) immettere il sito valido di un account di Azure AD valido di cui si vuole eseguire il provisioning.

    f. Fare clic su **Save**.

### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione si abilita Britta Simon per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a xMatters OnDemand.

![Assegna utente][200] 

**Per assegnare Britta Simon a xMatters OnDemand, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

1. Nell'elenco delle applicazioni selezionare **xMatters OnDemand**.

    ![Configure Single Sign-On](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

1. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202] 

1. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

1. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

1. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

1. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro xMatters OnDemand nel pannello di accesso si accede automaticamente all'applicazione xMatters OnDemand.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/xmatters-ondemand-tutorial/tutorial_general_203.png
