---
title: Personalizzare un modello Person con Video Indexer - Azure
titlesuffix: Azure Media Services
description: Questo articolo fornisce informazioni generali sul modello Person in Video Indexer e come personalizzarlo.
services: media-services
author: anikaz
manager: johndeu
ms.service: media-services
ms.topic: article
ms.date: 03/19/2019
ms.author: anzaman
ms.openlocfilehash: b491120639421d85d2fbb1a0efb2b6dd09ec1d4c
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60553726"
---
# <a name="customize-a-person-model-in-video-indexer"></a>Personalizzare un modello Person con Video Indexer

Video Indexer supporta il riconoscimento di celebrità nei video. La funzionalità di identificazione di celebrità include circa un milione di visi basandosi su origini dati di uso comune, ad esempio IMDB, Wikipedia e i principali influencer di LinkedIn. Visi non riconosciute da indicizzatore Video vengono comunque rilevati ma rimangono senza nome. I clienti possono creare modelli di persona personalizzati e consentire all'indicizzatore Video di riconoscere i visi non riconosciuti per impostazione predefinita. I clienti possono creare questi modelli persona mediante l'associazione di un nome di persona con i file di immagine del viso della persona.  

Se l'account si occupa dei diversi casi d'uso, è possibile trarre vantaggio dalla possibilità di creare più modelli di persona per ogni account. Ad esempio, se il contenuto nell'account deve essere ordinato in canali diversi, è possibile creare un modello di persona separato per ogni canale. 

> [!NOTE]
> Ogni modello di persona supporta fino a 1 milione di persone e ogni account prevede un limite di 50 modelli persona. 

Dopo aver creato un modello, è possibile usarlo specificando l'ID modello di un modello Persona specifico quando si carica un video o lo si indicizza una o più volte. Training di un nuovo viso per un video, aggiorna il modello personalizzato specifico che il video è stato associato. 

Se non è necessario il supporto di più modelli Persona, non assegnare un ID di modello Persona al video durante il caricamento, l'indicizzazione o la reindicizzazione. In questo caso, Video Indexer userà il modello di utente predefinito nell'account. 

È possibile usare il sito Web di indicizzatore Video per modificare i volti rilevati in un video e gestire più modelli di persona personalizzati nell'account, come descritto nel [personalizzare un modello di persona con un sito Web](customize-person-model-with-website.md) argomento. È anche possibile usare l'API, come descritto in [personalizzare un modello di persona usando le API](customize-person-model-with-api.md).