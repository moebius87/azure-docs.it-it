---
title: Come assegnare gli utenti alle applicazioni | Microsoft Docs
description: Comprendere come vengono assegnati gli utenti a un'applicazione nel tenant
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: celested
ms.collection: M365-identity-device-management
ms.openlocfilehash: be36bfeb0991dc4a4b7fce723cadb6b508c0d6a3
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60291025"
---
# <a name="how-to-assign-users-to-applications"></a>Come assegnare gli utenti alle applicazioni

Questo articolo consente di comprendere come vengono assegnati gli utenti a un'applicazione nel tenant.

## <a name="how-do-users-get-assigned-to-an-application-in-azure-ad"></a>Come vengono assegnati gli utenti a un'applicazione in Azure AD?

Un utente deve prima essere assegnato a un'applicazione per potervi accedere. L'assegnazione può essere eseguita da un amministratore, da un delegato aziendale o, talvolta, dall'utente stesso. Di seguito vengono descritti i modi in cui gli utenti possono essere assegnati alle applicazioni:

1.  Un amministratore [assegna un utente](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) direttamente all'applicazione

2.  Un amministratore [assegna un gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal), del quale l'utente è membro, all'applicazione, inclusi:

    * Un gruppo che è stato sincronizzato da locale

    * Un gruppo di sicurezza statico creato nel cloud

    * Un [gruppo di sicurezza dinamico](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) creato nel cloud

    * Un gruppo di Office 365 creato nel cloud

    * Il gruppo [Tutti gli utenti](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups)

3.  Un amministratore abilita l'[Accesso all'applicazione self-service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) per consentire all'utente di aggiungere un'applicazione usando la funzionalità **Aggiungi app** del [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **senza l'approvazione aziendale**

4.  Un amministratore abilita l'[Accesso all'applicazione self-service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) per consentire all'utente di aggiungere un'applicazione usando la funzionalità **Aggiungi app** del [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction), ma solo **con l'approvazione previa di una serie di responsabili approvazione aziendali selezionati**

5.  Un amministratore abilita la [Gestione gruppi self-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) per consentire a un utente di partecipare a un gruppo assegnato a un'applicazione **senza l'approvazione aziendale**

6.  Un amministratore abilita la [Gestione gruppi self-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) per consentire a un utente di partecipare a un gruppo assegnato a un'applicazione, ma solo **con l'approvazione previa di una serie di responsabili approvazione aziendali selezionati**

7.  Un amministratore assegna una licenza direttamente a un utente per un'applicazione prodotta per esempio da [Microsoft Office 365](https://products.office.com/)

8.  Un amministratore assegna una licenza a un gruppo del quale l'utente è membro a un'applicazione prodotta per esempio da [Microsoft Office 365](https://products.office.com/)

9.  Un [amministratore dà il consenso a un'applicazione](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview) per essere usata da tutti gli utenti e quindi un utente effettua l'accesso all'applicazione

10. Un utente [dà il consenso a un'applicazione](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview) da solo effettuando l'accesso all'applicazione

## <a name="next-steps"></a>Passaggi successivi
[Gestione di applicazioni con Azure Active Directory](what-is-application-management.md)
