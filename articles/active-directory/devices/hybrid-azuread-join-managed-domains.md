---
title: Configurare l'aggiunta ad Azure Active Directory ibrido per i domini gestiti | Microsoft Docs
description: Informazioni su come configurare l'aggiunta ad Azure Active Directory ibrido per i domini gestiti.
services: active-directory
documentationcenter: ''
author: MicrosoftGuyJFlo
manager: daveba
editor: ''
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.subservice: devices
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 03/20/2019
ms.author: joflore
ms.reviewer: sandeo
ms.collection: M365-identity-device-management
ms.openlocfilehash: 81a9726b73226cd940a55e316ae434aeaad6ff4d
ms.sourcegitcommit: 6da4959d3a1ffcd8a781b709578668471ec6bf1b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58519086"
---
# <a name="tutorial-configure-hybrid-azure-active-directory-join-for-managed-domains"></a>Esercitazione: Configurare l'aggiunta all'identità ibrida di Azure Active Directory per i domini gestiti

Analogamente agli utenti, i dispositivi stanno diventando un'altra identità da proteggere e da usare per proteggere le risorse in qualsiasi momento e ovunque. Questo obiettivo si raggiunge trasferendo le identità dei dispositivi in Azure AD usando uno dei metodi seguenti:

- Aggiunta ad Azure AD
- Aggiunta ad Azure AD ibrido
- Registrazione di Azure AD

Con il trasferimento dei dispositivi in Azure AD si ottimizza la produttività degli utenti tramite il Single Sign-On (SSO) in tutte le risorse locali e nel cloud. Si può al tempo stesso proteggere l'accesso alle risorse locali e nel cloud con l'[accesso condizionale](../active-directory-conditional-access-azure-portal.md).

Questa esercitazione illustra come configurare l'aggiunta ad Azure AD ibrido per dispositivi in domini gestiti.

> [!div class="checklist"]
> * Configurare l'aggiunta ad Azure AD ibrido
> * Abilitare dispositivi Windows di livello inferiore
> * Verificare i dispositivi aggiunti 
> * Risolvere problemi 


## <a name="prerequisites"></a>Prerequisiti

Questa esercitazione presuppone che l'utente abbia familiarità con:
    
-  [Introduction to device management in Azure Active Directory](../device-management-introduction.md) (Introduzione alla gestione dei dispositivi in Azure Active Directory)
    
-  [Come pianificare l'implementazione dell'aggiunta all'identità ibrida di Azure Active Directory](hybrid-azuread-join-plan.md)

-  [Come controllare l'aggiunta dei dispositivi all'identità ibrida di Azure AD](hybrid-azuread-join-control.md)
  

Per configurare lo scenario in questo articolo, sono necessari gli elementi seguenti:

- La [versione più recente di Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 o versioni successive) da installare. 

Verificare che Azure AD Connect abbia sincronizzato gli oggetti computer dei dispositivi che devono essere aggiunti ad Azure AD ibrido. Se gli oggetti computer appartengono a unità organizzative specifiche, queste unità organizzative devono essere configurate per la sincronizzazione anche in Azure AD Connect.

A partire dalla versione 1.1.819.0, in Azure AD Connect è presente una procedura guidata per configurare l'aggiunta ad Azure AD ibrido che semplifica enormemente il processo di configurazione. La configurazione guidata imposta i punti di connessione del servizio (SCP) per la registrazione dei dispositivi.

I passaggi di configurazione descritti in questo articolo si basano su questa procedura guidata. 

L'aggiunta ad Azure AD ibrido richiede che i dispositivi abbiano accesso alle risorse Microsoft seguenti dall'interno della rete dell'organizzazione:  

- https://enterpriseregistration.windows.net
- https://login.microsoftonline.com
- https://device.login.microsoftonline.com
- [https://autologon.microsoftazuread-sso.com](https://autologon.microsoftazuread-sso.com) (Se si usa o si pensa di usare Seamless SSO)

Se l'organizzazione richiede l'accesso a Internet attraverso un proxy in uscita, a partire da Windows 10 1709 è possibile [configurare le impostazioni proxy nel computer usando un oggetto Criteri di gruppo (GPO)](https://blogs.technet.microsoft.com/netgeeks/2018/06/19/winhttp-proxy-settings-deployed-by-gpo/). Se nel computer è in esecuzione una versione precedente a Windows 10 1709, è necessario implementare Web Proxy Auto-Discovery (WPAD) per consentire ai computer Windows 10 di registrare i dispositivi con Azure AD. 

Se l'organizzazione richiede l'accesso a Internet attraverso un proxy in uscita autenticato, è necessario assicurarsi che i computer Windows 10 possano eseguire l'autenticazione al proxy in uscita. Poiché i computer Windows 10 eseguono la registrazione dei dispositivi usando il contesto del computer, è necessario configurare l'autenticazione del proxy in uscita usando il contesto del computer. Per i requisiti di configurazione, contattare il provider del proxy in uscita. 



## <a name="configure-hybrid-azure-ad-join"></a>Configurare l'aggiunta ad Azure AD ibrido

Per configurare un'aggiunta ad Azure AD ibrido con Azure AD Connect, è necessario disporre degli elementi seguenti:

- Credenziali di un amministratore globale per il tenant di Azure AD.  

- Credenziali dell'amministratore dell'organizzazione per ognuna delle foreste.


**Per configurare un'aggiunta ad Azure AD ibrido con Azure AD Connect:**

1. Avviare Azure AD Connect, quindi fare clic su **Configura**.

    ![Schermata iniziale](./media/hybrid-azuread-join-managed-domains/11.png)

2. Nella pagina **Attività aggiuntive** selezionare **Configura le opzioni del dispositivo**, quindi fare clic su **Avanti**. 

    ![Attività aggiuntive](./media/hybrid-azuread-join-managed-domains/12.png)

3. Nella pagina **Panoramica** fare clic su **Avanti**. 

    ![Panoramica](./media/hybrid-azuread-join-managed-domains/13.png)

4. Nella pagina **Connessione ad Azure AD** immettere le credenziali di amministratore globale per il tenant di Azure AD.  

    ![Connessione ad Azure AD](./media/hybrid-azuread-join-managed-domains/14.png)

5. Nella pagina **Opzioni dispositivo** selezionare **Configura l'aggiunta ad Azure AD ibrido**, quindi fare clic su **Avanti**. 

    ![Opzioni del dispositivo](./media/hybrid-azuread-join-managed-domains/15.png)

6. Nella pagina **SCP**, per ogni foresta che si intende configurare a SCP tramite Azure AD Connect, attenersi ai passaggi seguenti e quindi fare clic su **Avanti**: 

    ![SCP](./media/hybrid-azuread-join-managed-domains/16.png)

    a. Selezionare la foresta.

    b. Selezionare il servizio di autenticazione.

    c. Fare clic su **Aggiungi** per immettere le credenziali di amministratore aziendale.


7. Nella pagina **Sistemi operativi del dispositivo** selezionare i sistemi operativi usati dai dispositivi nell'ambiente Active Directory, quindi fare clic su **Avanti**. 

    ![Sistema operativo del dispositivo](./media/hybrid-azuread-join-managed-domains/17.png)


8. Nella pagina **Pronto per la configurazione** fare clic su **Configura**. 

    ![Pronto per la configurazione](./media/hybrid-azuread-join-managed-domains/19.png)

9. Nella pagina **Configurazione completata** fare clic su **Esci**. 

    ![Configurazione completata](./media/hybrid-azuread-join-managed-domains/20.png)




## <a name="enable-windows-down-level-devices"></a>Abilitare dispositivi Windows di livello inferiore

Se alcuni dei dispositivi aggiunti a un dominio sono dispositivi di livello inferiore di Windows, è necessario:

- Aggiornare le impostazioni dei dispositivi
 
- Configurare le impostazioni intranet locali per la registrazione dei dispositivi

- Configurare l'accesso Single Sign-On facile (Seamless SSO)

- Controllare i dispositivi Windows di livello inferiore 


### <a name="update-device-settings"></a>Aggiornare le impostazioni dei dispositivi 

Per registrare i dispositivi Windows di livello inferiore, è necessario assicurarsi che le impostazioni dei dispositivi che consentono agli utenti di registrare i dispositivi in Azure AD siano configurate. Nel portale di Azure queste impostazioni sono disponibili in:

`Home > [Name of your tenant] > Devices - Device settings`  


    
Il criterio seguente deve essere impostato su **Tutti**: **Gli utenti possono registrare i dispositivi con Azure AD**

![Registrare i dispositivi](media/hybrid-azuread-join-managed-domains/23.png)



### <a name="configure-the-local-intranet-settings-for-device-registration"></a>Configurare le impostazioni intranet locali per la registrazione dei dispositivi

Per completare l'aggiunta ad Azure AD ibrido dei dispositivi Windows di livello inferiore e per evitare le richieste dei certificati quando i dispositivi vengano autenticati in Azure AD, è possibile eseguire il push di criteri nei dispositivi aggiunti al dominio per aggiungere gli URL seguenti all'area Intranet locale in Internet Explorer:

- `https://device.login.microsoftonline.com`

- `https://autologon.microsoftazuread-sso.com`.

È inoltre necessario abilitare **Consenti aggiornamenti barra di stato tramite script** nell'area Intranet locale dell'utente.


### <a name="configure-seamless-sso"></a>Configurare l'accesso Seamless SSO

Per completare correttamente l'aggiunta ad Azure AD ibrido dei dispositivi Windows di livello inferiore in un dominio gestito che usa Autenticazione pass-through o Sincronizzazione hash password come metodo di autenticazione cloud di Azure Active Directory, è anche necessario [configurare l'accesso Seamless SSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso-quick-start#step-2-enable-the-feature). 


### <a name="control-windows-down-level-devices"></a>Controllare i dispositivi Windows di livello inferiore 

Per registrare i dispositivi Windows di livello inferiore, è necessario scaricare e installare un pacchetto di Windows Installer (con estensione msi) dall'Area download. Per altre informazioni, fare clic [qui](hybrid-azuread-join-control.md#control-windows-down-level-devices). 


## <a name="verify-the-registration"></a>Verificare la registrazione

Per verificare lo stato di registrazione del dispositivo nel tenant di Azure, è possibile usare il cmdlet **[Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice)** nel **[modulo PowerShell di Azure Active Directory](/powershell/azure/install-msonlinev1?view=azureadps-2.0)**.

Quando si usa il cmdlet **Get-MSolDevice** per controllare i dettagli del servizio:

- Deve essere presente un oggetto con **ID dispositivo** corrispondente all'ID nel client Windows.
- Il valore di **DeviceTrustType** deve essere **Aggiunto a un dominio**. Questo valore equivale allo stato **Aggiunto ad Azure AD ibrido** nella pagina dei dispositivi nel portale di Azure AD.
- Per i dispositivi usati nell'accesso condizionale, il valore **Abilitato** deve essere **True** e **DeviceTrustLevel** deve essere **Gestito**. 


**Per controllare i dettagli del servizio:**

1. Aprire **Windows PowerShell** come amministratore.

2. Digitare `Connect-MsolService` per eseguire la connessione al tenant di Azure desiderato.  

3. Digitare `get-msoldevice -deviceId <deviceId>`.

6. Verificare che **Abilitato** sia impostato su **True**.





## <a name="troubleshoot-your-implementation"></a>Risolvere i problemi di implementazione

Se si verificano problemi durante il completamento dell'aggiunta ad Azure AD ibrido per dispositivi Windows aggiunti al dominio, vedere:

- [Risoluzione dei problemi relativi all'aggiunta ad Azure AD ibrido per dispositivi Windows correnti](troubleshoot-hybrid-join-windows-current.md)
- [Risoluzione dei problemi relativi all'aggiunta ad Azure AD ibrido per dispositivi Windows di livello inferiore](troubleshoot-hybrid-join-windows-legacy.md)


## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Configure hybrid Azure Active Directory join for federated domains](hybrid-azuread-join-federated-domains.md) (Configurare l'aggiunta ad Azure Active Directory ibrido per domini federati)
> [Configure hybrid Azure Active Directory join manually](hybrid-azuread-join-manual.md) (Configurare l'aggiunta ad Azure Active Directory ibrido manualmente)

