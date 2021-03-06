---
title: Impostazioni di offerta di applicazione SaaS Azure | Azure Marketplace
description: Configurare le impostazioni per un'offerta di applicazione SaaS in Azure Marketplace.
services: Azure, Marketplace, Cloud Partner Portal,
author: dan-wesley
ms.service: marketplace
ms.topic: conceptual
ms.date: 04/24/2019
ms.author: pabutler
ms.openlocfilehash: 6903226ecfe1478b340e390c783c4e57af778f3e
ms.sourcegitcommit: c53a800d6c2e5baad800c1247dce94bdbf2ad324
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/30/2019
ms.locfileid: "64943534"
---
# <a name="saas-application-offer-settings-tab"></a>Scheda Impostazioni dell'offerta per un'applicazione SaaS

Questo articolo descrive come configurare le impostazioni dell'offerta.

La pagina **App SaaS > Nuova offerta** si apre con la scheda **Impostazioni dell'offerta** visualizzata. 

Usare la scheda Impostazioni dell'offerta per configurare **Offer Identity** (Identità offerta), come illustrato nella schermata successiva. Un asterisco (*) alla fine del nome del campo indica che si tratta di un campo obbligatorio.

![Scheda Impostazioni dell'offerta](./media/saas-new-offer.png)

## <a name="offer-identity-settings"></a>Impostazioni di identità dell'offerta

In Offer Identity (Identità offerta) è necessario specificare le informazioni per i campi descritti nella tabella seguente. I campi obbligatori sono indicati da un asterisco (*).

|    Nome campo      |    DESCRIZIONE    |
|  ---------------   |  ---------------  |
|  **ID offerta\***    |  Un identificatore univoco dell'offerta in un profilo di pubblicazione. Questo ID sarà visibile negli URL dei prodotti e nei report di fatturazione. Può essere composto solo da caratteri alfanumerici minuscoli o trattini (-). L'ID non può terminare con un trattino e può contenere al massimo 50 caratteri. Si noti che questo campo è bloccato dopo la pubblicazione dell'offerta. Ad esempio, se l'editore Contoso pubblica un'offerta con ID offerta sample-vm, in Azure Marketplace l'offerta viene visualizzata come: https://azuremarketplace.microsoft.com/marketplace/apps/contoso.sample-vm?tab=Overview.                 |
|  **ID dell'editore\***    |  L'ID editore rappresenta il proprio identificatore univoco in Marketplace. È consigliabile associare a tutte le proprie offerte il proprio ID editore. L'ID editore non può essere modificato dopo aver salvato l'offerta.                |
|  **Nome\***      |   Nome visualizzato dell'offerta. Nome che verrà visualizzato in Azure Marketplace e nel portale di Azure. Può contenere massimo 50 caratteri. Includere un nome di marchio riconoscibile per il prodotto. Non includere il nome della società, a meno che non corrisponda al nome con cui viene commercializzato. Se si sta proponendo questa offerta nel proprio sito Web, assicurarsi che il nome corrisponda esattamente a quello con cui viene visualizzato nel sito Web.               |
|  |  |

Selezionare **Save** (Salva) per salvare le voci immesse.

## <a name="next-steps"></a>Passaggi successivi

[Scheda Informazioni tecniche](./cpp-technical-info-tab.md)
