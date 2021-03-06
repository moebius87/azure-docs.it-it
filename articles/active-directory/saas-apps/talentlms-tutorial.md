---
title: 'Esercitazione: Integrazione di Azure Active Directory con TalentLMS | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e TalentLMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8fa78ec2b5623dfd010a8fe5709916a47e221a9e
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60732340"
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a>Esercitazione: Integrazione di Azure Active Directory con TalentLMS

Questa esercitazione descrive come integrare TalentLMS con Azure Active Directory (Azure AD).

L'integrazione di TalentLMS con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a TalentLMS
- È possibile abilitare gli utenti per l'accesso automatico a TalentLMS (Single Sign-On) con gli account Azure AD
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con TalentLMS, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di TalentLMS abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si ha un ambiente di valutazione di Azure AD, è possibile ottenere una versione di valutazione di un mese qui: [Offerta per la versione di valutazione](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di TalentLMS dalla raccolta
1. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-talentlms-from-the-gallery"></a>Aggiunta di TalentLMS dalla raccolta
Per configurare l'integrazione di TalentLMS in Azure AD, è necessario aggiungere TalentLMS dalla raccolta all'elenco di app SaaS gestite.

**Per aggiungere TalentLMS dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

1. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![APPLICAZIONI][2]
    
1. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![APPLICAZIONI][3]

1. Nella casella di ricerca digitare **TalentLMS**.

    ![Creazione di un utente test di Azure AD](./media/talentlms-tutorial/tutorial_talentlms_search.png)

1. Nel pannello dei risultati selezionare **TalentLMS** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TalentLMS usando un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve individuare l'utente di TalentLMS corrispondente a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in TalentLMS.

Per stabilire la relazione di collegamento, in TalentLMS assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con TalentLMS, è necessario completare i blocchi predefiniti seguenti:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.
1. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
1. **[Creazione di un utente test di TalentLMS](#creating-a-talentlms-test-user)**: per avere una controparte di Britta Simon in TalentLMS collegata alla relativa rappresentazione in Azure AD.
1. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione TalentLMS.

**Per configurare l'accesso Single Sign-On di Azure AD con TalentLMS, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **TalentLMS** del portale di Azure fare clic su **Single Sign-On**.

    ![Configure Single Sign-On][4]

1. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Configure Single Sign-On](./media/talentlms-tutorial/tutorial_talentlms_samlbase.png)

1. Nella sezione **URL e dominio TalentLMS** seguire questa procedura:

    ![Configure Single Sign-On](./media/talentlms-tutorial/tutorial_talentlms_url.png)

    a. Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<tenant-name>.TalentLMSapp.com`

    b. Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `http://<tenant-name>.talentlms.com`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi. Per ottenere questi valori, contattare il [team di supporto clienti di TalentLMS](https://www.talentlms.com/contact). 
 
1. Nella sezione **Certificato di firma SAML** copiare il valore **IDENTIFICAZIONE PERSONALE** del certificato.

    ![Configure Single Sign-On](./media/talentlms-tutorial/tutorial_talentlms_certificate.png) 

1. Fare clic sul pulsante **Salva** .

    ![Configure Single Sign-On](./media/talentlms-tutorial/tutorial_general_400.png)

1. Nella sezione **Configurazione di TalentLMS** fare clic su **Configura TalentLMS** per visualizzare la finestra **Configura accesso**. Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**

    ![Configure Single Sign-On](./media/talentlms-tutorial/tutorial_talentlms_configure.png)  

1. In un'altra finestra del Web browser accedere al sito aziendale TalentLMS come amministratore.

1. Nella sezione **Account & Settings** (Account e impostazioni) fare clic sulla scheda **Users** (Utenti).
   
    ![Impostazioni e account](./media/talentlms-tutorial/IC777296.png "Impostazioni e account")

1. Fare clic su **Single Sign-On (SSO)**.

1. Nella sezione Single Sign-On seguire questa procedura:
   
    ![Single Sign-On](./media/talentlms-tutorial/IC777297.png "Single Sign-On")   

    a. Dall'elenco **SSO integration type** (Tipo integrazione SSO) selezionare **SAML 2.0**.

    b. Nella casella di testo **Identity Provider (IDP)** (Provider di identità (IDP)) incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure.
 
    c. Incollare il valore **Identificazione personale** dal portale di Azure nella casella di testo **Certificate Fingerprint** (Impronta digitale certificato).    

    d.  Nella casella di testo **Remote sign-in URL** (URL di accesso remoto) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.
 
    e. Nella casella di testo **Remote sign-out URL** (URL di disconnessione remota) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.

    f. Specificare le informazioni seguenti: 

    * Nella casella di testo **TargetedID** (ID destinazione) digitare `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`
     
    * Nella casella di testo **First name** (Nome) digitare `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`
    
    * Nella casella di testo **Last name** (Cognome) digitare `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`
    
    * Nella casella di testo **Email** (Posta elettronica) digitare `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`
    
1. Fare clic su **Save**.
 
> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili qui: [Documentazione incorporata di Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/talentlms-tutorial/create_aaduser_01.png) 

1. Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.
    
    ![Creazione di un utente test di Azure AD](./media/talentlms-tutorial/create_aaduser_02.png) 

1. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.
 
    ![Creazione di un utente test di Azure AD](./media/talentlms-tutorial/create_aaduser_03.png) 

1. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:
 
    ![Creazione di un utente test di Azure AD](./media/talentlms-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Create**(Crea).
 
### <a name="creating-a-talentlms-test-user"></a>Creazione di un utente test di TalentLMS

Per consentire agli utenti di Azure AD di accedere a TalentLMS, è necessario eseguirne il provisioning in TalentLMS. Nel caso di TalentLMS, il provisioning è un'attività manuale.

**Per eseguire il provisioning di un account utente, seguire questa procedura:**

1. Accedere al tenant **TalentLMS** .

1. Fare clic su **Users** (Utenti), quindi fare clic su **Add User** (Aggiungi utente).

1. Nella pagina della finestra di dialogo **Add User** seguire questa procedura:
   
    ![Aggiungere un utente](./media/talentlms-tutorial/IC777299.png "Aggiungere un utente")  

    a. Nella casella di testo **First name** (Nome) immettere il nome dell'utente, ad esempio **Britta**.

    b. Nella casella di testo **Last name** (Cognome) immettere il cognome dell'utente, ad esempio **Simon**.
 
    c. Nella casella di testo **Email Address** (Indirizzo di posta elettronica) immettere l'indirizzo di posta elettronica dell'utente, ad esempio **brittasimon\@contoso.com**.

    d. Fare clic su **Add User**.

>[!NOTE]
>È possibile utilizzare qualsiasi altro strumento di creazione di account utente di TalentLMS o le API fornite da TalentLMS per effettuare il provisioning degli account utente di AAD.
 

### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a TalentLMS.

![Assegna utente][200] 

**Per assegnare Britta Simon a TalentLMS, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

1. Nell'elenco di applicazioni selezionare **TalentLMS**.

    ![Configure Single Sign-On](./media/talentlms-tutorial/tutorial_talentlms_app.png) 

1. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202] 

1. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

1. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

1. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

1. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro TalentLMS nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione TalentLMS

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/talentlms-tutorial/tutorial_general_01.png
[2]: ./media/talentlms-tutorial/tutorial_general_02.png
[3]: ./media/talentlms-tutorial/tutorial_general_03.png
[4]: ./media/talentlms-tutorial/tutorial_general_04.png

[100]: ./media/talentlms-tutorial/tutorial_general_100.png

[200]: ./media/talentlms-tutorial/tutorial_general_200.png
[201]: ./media/talentlms-tutorial/tutorial_general_201.png
[202]: ./media/talentlms-tutorial/tutorial_general_202.png
[203]: ./media/talentlms-tutorial/tutorial_general_203.png

