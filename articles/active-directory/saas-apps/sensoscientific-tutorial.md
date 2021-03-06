---
title: 'Esercitazione: Integrazione di Azure Active Directory con SensoScientific Wireless Temperature Monitoring System | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SensoScientific Wireless Temperature Monitoring System.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 33a625e82f41bee1b8e3980192076d24a7471953
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60340716"
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a>Esercitazione: Integrazione di Azure Active Directory con SensoScientific Wireless Temperature Monitoring System

Questa esercitazione descrive come integrare SensoScientific Wireless Temperature Monitoring System con Azure Active Directory (Azure AD).

L'integrazione di SensoScientific Wireless Temperature Monitoring System con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a SensoScientific Wireless Temperature Monitoring System
- È possibile abilitare gli utenti per l'accesso automatico a SensoScientific Wireless Temperature Monitoring System (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con SensoScientific Wireless Temperature Monitoring System, è necessario quanto segue:

- Sottoscrizione di Azure AD
- Una sottoscrizione abilitata per l'accesso Single Sign-On per SensoScientific Wireless Temperature Monitoring System

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di SensoScientific Wireless Temperature Monitoring System dalla raccolta
1. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-the-gallery"></a>Aggiunta di SensoScientific Wireless Temperature Monitoring System dalla raccolta
Per configurare l'integrazione di SensoScientific Wireless Temperature Monitoring System in Azure AD, è necessario aggiungerlo all'elenco di app SaaS gestite dalla raccolta.

**Per aggiungere SensoScientific Wireless Temperature Monitoring System dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

1. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![APPLICAZIONI][2]
    
1. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![APPLICAZIONI][3]

1. Nella casella di ricerca digitare **SensoScientific Wireless Temperature Monitoring System**.

    ![Creazione di un utente test di Azure AD](./media/sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

1. Nel riquadro dei risultati selezionare **SensoScientific Wireless Temperature Monitoring System**, quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SensoScientific Wireless Temperature Monitoring System con un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di SensoScientific Wireless Temperature Monitoring System che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SensoScientific Wireless Temperature Monitoring System.

La relazione di collegamento viene stabilita assegnando al valore di **nome utente** in Azure AD lo stesso valore di **Username** (Nome utente) in SensoScientific Wireless Temperature Monitoring System.

Per configurare e testare l'accesso Single Sign-On di Azure AD con SensoScientific Wireless Temperature Monitoring System, è necessario completare i blocchi predefiniti seguenti:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.
1. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
1. **[Creazione di un utente test di SensoScientific Wireless Temperature Monitoring System](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**: per avere una controparte di Britta Simon in SensoScientific Wireless Temperature Monitoring System collegata alla relativa rappresentazione in Azure AD.
1. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione SensoScientific Wireless Temperature Monitoring System.

**Per configurare l'accesso Single Sign-On di Azure AD con SensoScientific Wireless Temperature Monitoring System, seguire questa procedura:**

1. Nel portale di Azure, nella pagina di integrazione dell'applicazione **SensoScientific Wireless Temperature Monitoring System** fare clic su **Single Sign-On**.

    ![Configure Single Sign-On][4]

1. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Configure Single Sign-On](./media/sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

1. Nella sezione **URL e dominio SensoScientific Wireless Temperature Monitoring System** non è necessario eseguire alcun passaggio dal momento che l'app è già preintegrata in Azure:

    ![Configure Single Sign-On](./media/sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

1. Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.

    ![Configure Single Sign-On](./media/sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

1. Fare clic sul pulsante **Salva** .

    ![Configure Single Sign-On](./media/sensoscientific-tutorial/tutorial_general_400.png)

1. Nella sezione **Configurazione di SensoScientific Wireless Temperature Monitoring System** fare clic su **Configura SensoScientific Wireless Temperature Monitoring System** per aprire la finestra **Configura accesso**. Copiare l'**URL di disconnessione, l'ID di entità SAML** e l'**URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido**.

    ![Configure Single Sign-On](./media/sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

1. Accedere all'applicazione SensoScientific Wireless Temperature Monitoring System come amministratore.

1. Nel menu di navigazione nella parte superiore, fare clic su **Configuration** (Configurazione) e passare a **Configure** (Configura) in **Single Sign-On** per aprire Single Sign-On Settings (Impostazioni Single Sign-On).

    ![Configure Single Sign-On](./media/sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

1. Nella pagina **Single Sign-On Settings** seguire questa procedura:
 
    a. Selezionare il **Nome autorità emittente** come Azure AD.
    
    b. Incollare l'**ID entità SAML** copiato dal portale di Azure nella casella di testo URL dell'autorità di certificazione.
    
    c. Incollare l'**URL servizio Single Sign-On SAML** copiato dal portale di Azure nella casella di testo URL servizio Single Sign-On.

    d. Incollare l'**URL di disconnessione** copiato dal portale di Azure nella casella di testo URL servizio Single Sign-Out.

    e. Cercare il certificato scaricato dal portale di Azure e caricarlo qui.
    
    f. Fare clic su **Save**.
  
> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili qui: [Documentazione incorporata di Azure AD](https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/sensoscientific-tutorial/create_aaduser_01.png) 

1. Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.
    
    ![Creazione di un utente test di Azure AD](./media/sensoscientific-tutorial/create_aaduser_02.png) 

1. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.
 
    ![Creazione di un utente test di Azure AD](./media/sensoscientific-tutorial/create_aaduser_03.png) 

1. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:
 
    ![Creazione di un utente test di Azure AD](./media/sensoscientific-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Create**(Crea).
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a>Creazione di un utente test di SensoScientific Wireless Temperature Monitoring System

Per consentire agli utenti di Azure AD di accedere a SensoScientific Wireless Temperature Monitoring System, è necessario eseguirne il provisioning in SensoScientific Wireless Temperature Monitoring System. Per aggiungere utenti alla piattaforma SensoScientific Wireless Temperature Monitoring System, collaborare con il  [team di supporto di SensoScientific Wireless Temperature Monitoring System](https://www.sensoscientific.com/contact-us/) . Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On. 

### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a SensoScientific Wireless Temperature Monitoring System.

![Assegna utente][200] 

**Per assegnare Britta Simon a SensoScientific Wireless Temperature Monitoring System, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

1. Nell'elenco delle applicazioni selezionare **SensoScientific Wireless Temperature Monitoring System**.

    ![Configure Single Sign-On](./media/sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

1. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202] 

1. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

1. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

1. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

1. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso. Fare clic sul riquadro SensoScientific Wireless Temperature Monitoring System nel pannello di accesso; si accederà automaticamente all'applicazione SensoScientific Wireless Temperature Monitoring System. Per altre informazioni sul Pannello di accesso, vedere [Introduzione al Pannello di accesso](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/sensoscientific-tutorial/tutorial_general_203.png

