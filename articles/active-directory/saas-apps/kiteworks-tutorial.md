---
title: 'Esercitazione: Integrazione di Azure Active Directory con Kiteworks | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Kiteworks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 73c352c0d60bc8dca969092210e9cff0a733765a
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60262942"
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a>Esercitazione: Integrazione di Azure Active Directory con Kiteworks

Questa esercitazione descrive come integrare Kiteworks con Azure Active Directory (Azure AD).

L'integrazione di Kiteworks con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a Kiteworks
- È possibile abilitare gli utenti per l'accesso automatico a Kiteworks (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con Kiteworks, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di Kiteworks abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di Kiteworks dalla raccolta
1. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-kiteworks-from-the-gallery"></a>Aggiunta di Kiteworks dalla raccolta
Per configurare l'integrazione di Kiteworks in Azure AD, è necessario aggiungere Kiteworks dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere Kiteworks dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

1. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![APPLICAZIONI][2]
    
1. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![APPLICAZIONI][3]

1. Nella casella di ricerca digitare **Kiteworks**.

    ![Creazione di un utente test di Azure AD](./media/kiteworks-tutorial/tutorial_kiteworks_search.png)

1. Nel pannello dei risultati selezionare **Kiteworks** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Kiteworks mediante un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Kiteworks corrisponde a un determinato utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Kiteworks.

Per stabilire la relazione di collegamento, in Kiteworks assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con Kiteworks, è necessario completare i blocchi predefiniti seguenti:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.
1. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
1. **[Creazione di un utente test di Kiteworks](#creating-a-kiteworks-test-user)**: per avere una controparte di Britta Simon in Kiteworks collegata alla rappresentazione dell'utente in Azure AD.
1. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Kiteworks.

**Per configurare l'accesso Single Sign-On di Azure AD con Kiteworks, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Kiteworks** del portale di Azure fare clic su **Single Sign-On**.

    ![Configure Single Sign-On][4]

1. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

1. Nella sezione **URL e dominio Kiteworks** seguire questa procedura:

    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_kiteworks_url.png)

    a. Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.kiteworks.com`

    b. Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi. Per ottenere questi valori contattare il [team di supporto clienti di Kiteworks](https://accellion.com/support). 
 
1. Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.

    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

1. Fare clic sul pulsante **Salva** .

    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_general_400.png)

1. Nella sezione **Configurazione di Kiteworks** fare clic su **Configura Kiteworks** per aprire la finestra **Configura accesso**. Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**

    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_kiteworks_configure.png) 

1. Accedere al sito aziendale di Kiteworks come amministratore.

1. Nel barra degli strumenti in alto fare clic su **Impostazioni**.
   
    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_kiteworks_06.png) 

1. Nella sezione **Authentication and Authorization** (Autenticazione e autorizzazione) fare clic su **SSO Setup** (Configurazione SSO). 
   
    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_kiteworks_07.png)
 
1. Nella pagina di configurazione dell’accesso Single Sign-On, seguire questa procedura:
   
    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_kiteworks_09.png)   

    a. Selezionare **Autentica tramite Single Sign-On**.

    b. Selezionare **Avvia richiesta autenticazione**.

    c. Nella casella di testo **IdP Entity ID** (ID entità IdP) incollare il valore **SAML Entity ID** (ID entità SAML) copiato dal portale di Azure. 

    d. Nella casella di testo **URL servizio Single Sign-On** incollare il valore **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiato dal portale di Azure.

    e. Nella casella di testo **URL servizio punto di disconnessione singolo** incollare il valore di **Sign-Out URL** (URL di disconnessione) copiato dal portale di Azure.

    f. Aprire il certificato scaricato nel Blocco note, copiare il contenuto e incollarlo nella casella di testo **RSA Public Key Certificate** .
 
    g. Fare clic su **Save**.

> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili qui: [Documentazione incorporata di Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/kiteworks-tutorial/create_aaduser_01.png) 

1. Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.
    
    ![Creazione di un utente test di Azure AD](./media/kiteworks-tutorial/create_aaduser_02.png) 

1. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.
 
    ![Creazione di un utente test di Azure AD](./media/kiteworks-tutorial/create_aaduser_03.png) 

1. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:
 
    ![Creazione di un utente test di Azure AD](./media/kiteworks-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Create**(Crea).
 
### <a name="creating-a-kiteworks-test-user"></a>Creazione di un utente test per Kiteworks

Questa sezione descrive come creare un utente chiamato Britta Simon in Kiteworks.

Kiteworks supporta il provisioning JIT (just-in-time), che è abilitato per impostazione predefinita. Non è necessario alcun intervento dell'utente in questa sezione. Durante un tentativo di accesso a Kiteworks viene creato un nuovo utente, se questo non esiste già.

>[!NOTE]
>Per creare un utente manualmente è necessario contattare il [team di supporto di Kiteworks](https://accellion.com/support).
 

### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Kiteworks.

![Assegna utente][200] 

**Per assegnare Britta Simon a Kiteworks, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

1. Nell'elenco di applicazioni selezionare **Kiteworks**.

    ![Configure Single Sign-On](./media/kiteworks-tutorial/tutorial_kiteworks_app.png) 

1. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202] 

1. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

1. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

1. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

1. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.  

Quando si fa clic sul riquadro Kiteworks nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Kiteworks.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/kiteworks-tutorial/tutorial_general_203.png

