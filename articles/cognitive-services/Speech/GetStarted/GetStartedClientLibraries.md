---
title: Introduzione all'API Riconoscimento vocale Bing tramite le librerie client | Microsoft Docs
titlesuffix: Azure Cognitive Services
description: Usare le librerie client di Riconoscimento vocale Bing in Servizi cognitivi Microsoft per sviluppare applicazioni per la conversione di audio parlato in testo.
services: cognitive-services
author: zhouwangzw
manager: wolfma
ms.service: cognitive-services
ms.subservice: bing-speech
ms.topic: article
ms.date: 09/18/2018
ms.author: zhouwang
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: 89eb18a2b4af76f6489442dc66ab12d0840e92c7
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60515241"
---
# <a name="get-started-with-bing-speech-service-client-libraries"></a>Introduzione alle librerie client del Servizio Riconoscimento vocale Bing

[!INCLUDE [Deprecation note](../../../../includes/cognitive-services-bing-speech-api-deprecation-note.md)]

Oltre a eseguire richieste HTTP dirette tramite un'API REST, Servizio Riconoscimento vocale Bing fornisce agli sviluppatori delle librerie client per il riconoscimento vocale in varie lingue. Le librerie client per il riconoscimento vocale:

- Supportano funzionalità più avanzate di riconoscimento vocale, ad esempio risultati intermedi in tempo reale, flussi audio lunghi (fino a 10 minuti) e riconoscimento continuo.
- Forniscono un'API semplice e idiomatica nella lingua scelta.
- Nascondono i dettagli delle comunicazioni di basso livello.

Attualmente sono disponibili le seguenti librerie client per Servizio Riconoscimento vocale Bing:

- [Libreria desktop C#](GetStartedCSharpDesktop.md)
- [Libreria di servizi C#](GetStartedCSharpServiceLibrary.md)
- [Libreria JavaScript](GetStartedJSWebsockets.md)
- [Libreria Java per Android](GetStartedJavaAndroid.md)
- [Libreria Objective-C per iOS](Get-Started-ObjectiveC-iOS.md)

## <a name="additional-resources"></a>Risorse aggiuntive

- La pagina degli [esempi](../samples.md) fornisce degli esempi completi per usare le librerie client per il riconoscimento vocale.
- Se è necessaria una libreria client che non è ancora supportata, è possibile creare il proprio SDK. Implementare il [protocollo WebSocket di Riconoscimento vocale](../API-Reference-REST/websocketprotocol.md) nella piattaforma e usare la lingua scelta.

## <a name="license"></a>Licenza

Tutti gli SDK e gli esempi di Servizi cognitivi sono concessi su licenza con la licenza MIT. Per altre informazioni, vedere [Licenza](https://github.com/Microsoft/Cognitive-Speech-STT-JavaScript/blob/master/LICENSE.md).
