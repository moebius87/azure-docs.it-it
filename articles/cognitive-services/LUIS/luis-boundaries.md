---
title: Limiti
titleSuffix: Language Understanding - Azure Cognitive Services
description: Questo articolo illustra i limiti di LUIS (Language Understanding) dei Servizi cognitivi di Azure. LUIS dispone di diverse aree di limiti. Il limite modello controlla finalità, entità e funzionalità in LUIS. I limiti di quota si basano sul tipo di chiave. La combinazione di tasti controlla il sito Web di LUIS.
services: cognitive-services
author: diberry
manager: nitinme
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: article
ms.date: 04/18/2019
ms.author: diberry
ms.custom: seodec18
ms.openlocfilehash: 357ed4c42cc2758766b9ccd45a3fafa541338d11
ms.sourcegitcommit: f6ba5c5a4b1ec4e35c41a4e799fb669ad5099522
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65154563"
---
# <a name="boundaries-for-your-luis-model-and-keys"></a>Limiti per il modello LUIS e le chiavi
LUIS dispone di diverse aree di limiti. La prima è il [limite modello](#model-boundaries), che controlla finalità, entità e funzionalità in LUIS. La seconda area è [limiti di quota](#key-limits) basata sul tipo di chiave. Una terza area di limiti è rappresentata dalla [combinazione di tasti](#keyboard-controls) per il controllo del sito Web LUIS. Una quarta area è data dal [mapping dell'area globale](luis-reference-regions.md) tra il sito Web di creazione LUIS e le API dell'[endpoint LUIS](luis-glossary.md#endpoint). 


## <a name="model-boundaries"></a>Limiti di modello

Se l'app supera i limiti del modello LUIS, è consigliabile usare un'app [dispatch LUIS](luis-concept-enterprise.md#dispatch-tool-and-model) o un [contenitore LUIS](luis-container-howto.md). 

|Area|Limite|
|--|:--|
| [Nome app][luis-get-started-create-app] | *Numero max predefinito di caratteri |
| [Test di batch][batch-testing]| 10 set di dati, 1000 espressioni per ogni set di dati|
| Elenco esplicito | 50 per applicazione|
| Entità esterne | senza limiti |
| [Finalità][intents]|500 per ogni applicazione: 499 finalità personalizzate e la finalità _None_ obbligatoria.<br>Applicazione [basata su invio](https://aka.ms/dispatch-tool) con 500 origini di spedizione corrispondenti.|
| [Elenca entità](./luis-concept-entity-types.md) | Padre: 50, figlio: 20.000 elementi. Il nome canonico è il *numero max predefinito di caratteri. I sinonimi non hanno restrizioni di lunghezza. |
| [Entità apprese macchina + ruoli](./luis-concept-entity-types.md):<br> Composita,<br>semplice,<br>ruolo entità|Un limite di 100 entità padre o 330 entità, a seconda di quale limita i riscontri utente prima di tutto. Un ruolo viene conteggiata come un'entità ai fini questo limite. È un esempio è un composita con un semplice entità che ha 2 ruoli: 1 semplice composta + 1 + 2 ruoli = 4 330 entità.|
| [Anteprima - elenco dinamico di entità](https://aka.ms/luis-api-v3-doc#dynamic-lists-passed-in-at-prediction-time)|2 elenchi di circa 1 KB per ogni richiesta dell'endpoint stima query|
| [Criteri](luis-concept-patterns.md)|500 criteri per ogni applicazione.<br>Il criterio può contenere al massimo 400 caratteri.<br>3 entità pattern.any per criterio<br>Il criterio può contenere al massimo 2 testi facoltativi annidati|
| [Pattern.any](./luis-concept-entity-types.md)|100 per applicazione, 3 entità pattern.any per criterio |
| [Elenco di frasi][phrase-list]|10 elenchi di frase, 5.000 elementi per ogni elenco|
| [Entità predefinite](./luis-prebuilt-entities.md) | nessun limite|
| [Entità di espressione regolare](./luis-concept-entity-types.md)|20 entità<br>È consentito un numero massimo di 500 caratteri. per ogni criterio di entità di espressione regolare|
| [Ruoli](luis-concept-roles.md)|300 ruoli per ogni applicazione. 10 per entità|
| [Espressione][utterances] | 500 caratteri|
| [Espressioni][utterances] | 15.000 per ogni applicazione - non sono previsti limiti al numero di espressioni per finalità|
| [Versioni](luis-concept-version.md)| nessun limite |
| [Nome della versione][luis-how-to-manage-versions] | 10 caratteri limitati a caratteri alfanumerici e punto (.) |

*Il numero max predefinito di caratteri è 50. 

<a name="intent-and-entity-naming"></a>

## <a name="object-naming"></a>Denominazione degli oggetti

Non utilizzare i seguenti caratteri nei nomi seguenti.

|Object|Escludere i caratteri|
|--|--|
|Nomi di ruolo, entità e finalità|`:`<br>`$`|
|Nome della versione|`\`<br> `/`<br> `:`<br> `?`<br> `&`<br> `=`<br> `*`<br> `+`<br> `(`<br> `)`<br> `%`<br> `@`<br> `$`<br> `~`<br> `!`<br> `#`|

## <a name="key-usage"></a>Uso della chiave

Language Understanding ha chiavi separate, un tipo per la creazione e un tipo per l'esecuzione di query sull'endpoint di stima. Per altre informazioni sulle differenze tra i tipi di chiave, vedere [Chiavi di creazione e di endpoint per query di stima in LUIS](luis-concept-keys.md).

## <a name="key-limits"></a>Limiti delle chiavi

La chiave di creazione presenta diversi limiti per creazione e endpoint. La chiave endpoint del servizio LUIS è valida solo per le query di endpoint.


|Chiave|Creazione|Endpoint|Scopo|
|--|--|--|--|
|Creazione/Avvio di Language Understanding|1 milione/mese, 5/secondo|1.000/mese, 5/secondo|Creazione di app LUIS|
|[Sottoscrizione][pricing] di Language Understanding - F0 - livello gratuito |non valido|10.000/mese, 5/secondo|Esecuzione di query per l'endpoint LUIS|
|[Sottoscrizione][pricing] di Language Understanding - S0 - livello Basic|non valido|50/secondo|Esecuzione di query per l'endpoint LUIS|
|[Sottoscrizione][pricing] di Servizi cognitivi- S0 - livello Standard|non valido|50/secondo|Esecuzione di query per l'endpoint LUIS|
|[Integrazione dell'Analisi del sentiment](luis-how-to-publish-app.md#enable-sentiment-analysis)|non valido|nessun addebito|Aggiunta di informazioni sentiment inclusa l'estrazione dei dati di frase chiave |
|Integrazione riconoscimento vocale|non valido|Richieste di endpoint $5,50 USD/1.000|Converte un'espressione parlata in un espressione di testo e restituisce i risultati LUIS|

## <a name="keyboard-controls"></a>Controlli tastiera

|Input tastiera | DESCRIZIONE | 
|--|--|
|Controllo + E|passa dai token alle entità nell'elenco delle espressioni|

## <a name="website-sign-in-time-period"></a>Periodo di tempo per l'accesso al sito Web

Il periodo di tempo di accesso è di **60 minuti**. Trascorso questo tempo, si verificherà il seguente errore. Sarà necessario eseguire nuovamente l'accesso.

[luis-get-started-create-app]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-get-started-create-app
[batch-testing]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-concept-test#batch-testing
[intents]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-concept-intent
[phrase-list]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-concept-feature
[utterances]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-concept-utterance
[luis-how-to-manage-versions]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-how-to-manage-versions
[pricing]: https://azure.microsoft.com/pricing/details/cognitive-services/language-understanding-intelligent-services/
<!-- TBD: fix this link -->
[speech-to-intent-pricing]: https://azure.microsoft.com/pricing/details/cognitive-services/language-understanding-intelligent-services/
