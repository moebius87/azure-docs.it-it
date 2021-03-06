---
title: Restituire le N migliori traduzioni - API Traduzione testuale
titlesuffix: Azure Cognitive Services
description: Restituire le N migliori traduzioni con l'API Traduzione testuale Microsoft.
services: cognitive-services
author: v-pawal
manager: nitinme
ms.service: cognitive-services
ms.subservice: translator-text
ms.topic: conceptual
ms.date: 12/14/2017
ms.author: v-jansko
ms.openlocfilehash: 62992122dc16003078bb80ecd87c2bd3692586dd
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60610580"
---
# <a name="how-to-return-n-best-translations"></a>Procedura per restituire le N migliori traduzioni

> [!NOTE]
> Metodo deprecato. Non è disponibile nella V3.0 dell'API Traduzione testuale.

I metodi GetTranslations() e GetTranslationsArray() dell'API di Microsoft Translator includono un flag booleano facoltativo "IncludeMultipleMTAlternatives".
Il metodo restituirà fino a maxTranslations alternative se il delta viene fornito dall'elenco N migliori del motore di traduzione.

La firma è:

**Sintassi**

| C# |
|:---|
| GetTranslationsResponse Microsoft.Translator.GetTranslations(appId, text, from, to, maxTranslations, options); |

**Parameters**

| Parametro | DESCRIZIONE |
|:---|:---|
| appId | **Obbligatorio** Se si usa l'intestazione dell'autorizzazione, lasciare vuoto il campo appid. In caso contrario specificare una stringa contenente il token di accesso "Bearer" + " " +.|
| text | **Obbligatorio** Una stringa che rappresenta il testo da tradurre. Le dimensioni del testo non devono superare 10.000 caratteri.|
| from | **Obbligatorio** Una stringa che rappresenta il codice di lingua del testo da tradurre. |
| to | **Obbligatorio** Una stringa che rappresenta il codice di lingua in cui tradurre il testo. |
| maxTranslations | **Obbligatorio** Int che rappresenta il numero massimo di traduzioni da restituire. |
| opzioni | **Facoltativo** Un oggetto TranslateOptions che contiene i valori elencati di seguito. Sono tutti facoltativi e con le impostazioni predefinite più comuni.

* Categoria: l'unica opzione supportata e impostazione predefinita è "general".
* ContentType: l'unica opzione supportata e l'impostazione predefinita è "text/plain".
* Stato: stato dell'utente per mettere in correlazione richiesta e risposta. Verrà restituito lo stesso contenuto nella risposta.
* IncludeMultipleMTAlternatives: flag per determinare se restituire una o più alternative dal motore MT. Il valore predefinito è false e include una sola alternativa.

## <a name="ratings"></a>Classificazioni
Le classificazioni vengono applicate come segue: la miglior traduzione automatica ha una classificazione pari a 5.
Le alternative di traduzione (N-migliori) generate automaticamente hanno una classificazione pari a 0 e un livello di corrispondenza di 100.

## <a name="number-of-alternatives"></a>Numero di alternative
Il numero di alternative restituite è fino a maxTranslations, ma può essere inferiore.

## <a name="language-pairs"></a>Coppie di lingue
Questa funzionalità non è disponibile per le traduzioni tra cinese semplificato e cinese tradizionale in entrambe le direzioni. È disponibile per tutte le altre coppie di lingue supportate da Microsoft Translator.
