---
title: Confronto basato sulle funzionalità dei livelli di Gestione API di Azure | Microsoft Docs
description: Questo articolo mette a confronto i livelli di Gestione API basati sulle funzionalità offerte.
services: api-management
documentationcenter: ''
author: vladvino
manager: erikre
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/26/2018
ms.author: apimpm
ms.openlocfilehash: eae36aa6e60e3da03c59952a1d9e035e6a773d2d
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60531083"
---
# <a name="feature-based-comparison-of-the-azure-api-management-tiers"></a>Confronto basato sulle funzionalità dei livelli di Gestione API di Azure

Ogni [piano tariffario](https://aka.ms/apimpricing) di Gestione API offre un set diverso di funzionalità e di[ capacità](api-management-capacity.md) per unità. La tabella seguente riepiloga le funzionalità chiave disponibili in ciascuno dei livelli. Alcune funzionalità potrebbero funzionare diversamente o avere capacità diverse a seconda del livello. In questi casi le differenze vengono indicate negli articoli della documentazione, i quali descrivono le singole funzionalità.

| Funzionalità                                                                                      | <sup>ANTEPRIMA</sup> di consumo | Developer      | Basic          | Standard       | Premium        |
| -------------------------------------------------------------------------------------------- | ----------------------------- | -------------- | -------------- | -------------- | -------------- |
| Integrazione di Azure AD<sup>1</sup>                                                             | No                             | Sì            | No              | Sì            | Sì            |
| Supporto della Rete virtuale di Microsoft Azure (VNet)                                                               | No                             | Sì            | No              | No              | Sì            |
| Distribuzione in più aree                                                                      | No                             | No              | No              | No              | Sì            |
| Più nomi di dominio personalizzati                                                                 | No                             | No              | No              | No              | Sì            |
| Portale per sviluppatori<sup>2</sup>                                                                 | No                             | Sì            | Sì            | Sì            | Sì            |
| Cache incorporata                                                                               | No                             | Sì            | Sì            | Sì            | Sì            |
| Analisi incorporata                                                                           | No                             | Sì            | Sì            | Sì            | Sì            |
| [Impostazioni SSL](api-management-howto-manage-protocols-ciphers.md)                             | No                             | Sì            | Sì            | Sì            | Sì            |
| [Cache esterna](https://aka.ms/apimbyoc)                                                    | Sì                           | N.<sup>3</sup> | N.<sup>3</sup> | N.<sup>3</sup> | N.<sup>3</sup> |
| [Autenticazione con certificato client](api-management-howto-mutual-certificates-for-clients.md) | N.<sup>4</sup>                | Sì            | Sì            | Sì            | Sì            |
| [Backup e ripristino](api-management-howto-disaster-recovery-backup-restore.md)               | No                             | Sì            | Sì            | Sì            | Sì            |
| [Gestione tramite Git](api-management-configuration-repository-git.md)                        | No                             | Sì            | Sì            | Sì            | Sì            |
| API di gestione diretta                                                                        | No                             | Sì            | Sì            | Sì            | Sì            |
| Metriche e log di Monitoraggio di Azure                                                               | N.<sup>5</sup>                | Sì            | Sì            | Sì            | Sì            |

<sup>1</sup> Consente l'utilizzo di Azure AD (e Azure AD B2C) come provider di identità per l'accesso dell'utente al portale per sviluppatori.<br/>
<sup>2</sup> Sono incluse le funzionalità correlate, ad esempio utenti, gruppi, problemi, modelli di posta elettronica e applicazioni, nonché notifiche.<br/>
<sup>3</sup> Il supporto della cache esterna per questo livello sarà presto disponibile.<br/>
<sup>4</sup> L'autenticazione dei certificati client verrà aggiunta al livello di consumo prima della relativa Disponibilità generale.<br/>
<sup>5</sup> Il supporto completo di Monitoraggio di Azure verrà aggiunto al livello di consumo.
