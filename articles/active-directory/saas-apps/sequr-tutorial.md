---
title: 'Esercitazione: Integrazione di Azure Active Directory con Sequr | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Sequr.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a491e2ce-b4e8-41b8-8f4a-a2e263e462c3
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/8/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 007989d51ad111fb6a3ef21daee6a7c484bd154d
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60341823"
---
# <a name="tutorial-azure-active-directory-integration-with-sequr"></a>Esercitazione: Integrazione di Azure Active Directory con Sequr

Questa esercitazione descrive come integrare Sequr con Azure Active Directory (Azure AD).

L'integrazione di Sequr con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a Sequr.
- È possibile abilitare gli utenti per l'accesso automatico a Sequr (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con Sequr, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Una sottoscrizione abilitata per l'accesso Single Sign-On a Sequr

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di Sequr dalla raccolta
1. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-sequr-from-the-gallery"></a>Aggiunta di Sequr dalla raccolta
Per configurare l'integrazione di Sequr in Azure AD, è necessario aggiungere Sequr dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere Sequr dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Pulsante Azure Active Directory][1]

1. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![Pannello Applicazioni aziendali][2]
    
1. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![Pulsante Nuova applicazione][3]

1. Nella casella di ricerca digitare **Sequr**, selezionare **Sequr** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Sequr nell'elenco dei risultati](./media/sequr-tutorial/tutorial_sequr_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Sequr con un utente di test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Sequr che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Sequr.

Per stabilire la relazione di collegamento, in Sequr assegnare il valore di **nome utente** di Azure AD come valore di **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con Sequr, è necessario completare i blocchi predefiniti seguenti:

1. **[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.
1. **[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
1. **[Creare un utente di test di Sequr](#create-a-sequr-test-user)**: per avere una controparte di Britta Simon in Sequr collegata alla rappresentazione dell'utente in Azure AD.
1. **[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
1. **[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Sequr.

**Per configurare l'accesso Single Sign-On di Azure AD con Sequr, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Sequr** del portale di Azure fare clic su **Single Sign-On**.

    ![Collegamento Configura accesso Single Sign-On][4]

1. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Finestra di dialogo Single Sign-On](./media/sequr-tutorial/tutorial_sequr_samlbase.png)

1. Nella sezione **URL e dominio Sequr**, se si vuole configurare l'applicazione in modalità avviata da **IDP** seguire questa procedura:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Sequr](./media/sequr-tutorial/tutorial_sequr_url.png)

    Nella casella di testo **Identificatore** digitare l'URL: `https://login.sequr.io`

1. Selezionare **Mostra impostazioni URL avanzate** e seguire questa procedura se si vuole configurare l'applicazione in modalità avviata da **SP**:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Sequr](./media/sequr-tutorial/tutorial_sequr_url1.png)

    a. Nella casella di testo **URL accesso** digitare l'URL: `https://login.sequr.io`

    b. Nella casella di testo **Stato dell'inoltro** si otterrà questo valore, che verrà spiegato più avanti nell'esercitazione.
     
1. Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.

    ![Collegamento di download del certificato](./media/sequr-tutorial/tutorial_sequr_certificate.png) 

1. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/sequr-tutorial/tutorial_general_400.png)
    
1. Nella sezione **Configurazione di Sequr** fare clic su **Configura Sequr** per aprire la finestra **Configura accesso**. Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**

    ![Configurazione di Sequr](./media/sequr-tutorial/tutorial_sequr_configure.png)

1. In un'altra finestra del Web browser accedere al sito aziendale di Sequr come amministratore.

1. Fare clic su **Integrazioni** nel pannello di spostamento a sinistra.

    ![Configurazione di Sequr](./media/sequr-tutorial/configure1.png)

1. Scorrere verso il basso fino alla sezione **Single Sign-On**, quindi fare clic su **Gestisci**.

    ![Configurazione di Sequr](./media/sequr-tutorial/configure2.png)

1. Nella sezione **Manage Single Sign-On** (Gestione Single Sign-On) seguire questa procedura:

    ![Configurazione di Sequr](./media/sequr-tutorial/configure3.png)

    a. Nella casella di testo **URL di accesso Single Sign-On del provider di identità** incollare il valore di **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiato dal portale di Azure.

    b. Trascinare il file del **certificato** scaricato dal portale di Azure oppure immettere manualmente il contenuto del certificato.

    c. Dopo aver salvato la configurazione, verrà generato il valore dello stato dell'inoltro. Copiare il valore dello **stato dell'inoltro** e incollarlo nella casella di testo **Stato dell'inoltro** della sezione **URL e dominio Sequr** del portale di Azure.

    d. Fare clic su **Save**.

> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili qui: [Documentazione incorporata di Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

   ![Creare un utente test di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.

    ![Pulsante Azure Active Directory](./media/sequr-tutorial/create_aaduser_01.png)

1. Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/sequr-tutorial/create_aaduser_02.png)

1. Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.

    ![Pulsante Aggiungi](./media/sequr-tutorial/create_aaduser_03.png)

1. Nella finestra di dialogo **Utente** seguire questa procedura:

    ![Finestra di dialogo Utente](./media/sequr-tutorial/create_aaduser_04.png)

    a. Nella casella **Nome** digitare **BrittaSimon**.

    b. Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.

    c. Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.

    d. Fare clic su **Create**(Crea).
 
### <a name="create-a-sequr-test-user"></a>Creare un utente di test di Sequr

In questa sezione viene creato un utente di nome Britta Simon in Sequr. Collaborare con il  [team di supporto clienti di Sequr](mailto:support@sequr.io)  per aggiungere gli utenti alla piattaforma Sequr. Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On. 

### <a name="assign-the-azure-ad-test-user"></a>Assegnare l'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Sequr.

![Assegnare il ruolo utente][200] 

**Per assegnare Britta Simon a Sequr, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

1. Nell'elenco delle applicazioni selezionare **Sequr**.

    ![Collegamento di Sequr nell'elenco delle applicazioni](./media/sequr-tutorial/tutorial_sequr_app.png)  

1. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Collegamento "Utenti e gruppi"][202]

1. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Riquadro Aggiungi assegnazione][203]

1. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

1. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

1. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro Sequr nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Sequr.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al pannello di accesso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/sequr-tutorial/tutorial_general_01.png
[2]: ./media/sequr-tutorial/tutorial_general_02.png
[3]: ./media/sequr-tutorial/tutorial_general_03.png
[4]: ./media/sequr-tutorial/tutorial_general_04.png

[100]: ./media/sequr-tutorial/tutorial_general_100.png

[200]: ./media/sequr-tutorial/tutorial_general_200.png
[201]: ./media/sequr-tutorial/tutorial_general_201.png
[202]: ./media/sequr-tutorial/tutorial_general_202.png
[203]: ./media/sequr-tutorial/tutorial_general_203.png

