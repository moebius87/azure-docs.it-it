---
title: 'Guida introduttiva: Eseguire la sintesi vocale, C++ (Windows) - Servizi Voce'
titleSuffix: Azure Cognitive Services
description: Informazioni su come seguire la sintesi vocale in C++ su Windows Desktop con Speech SDK
services: cognitive-services
author: yinhew
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: quickstart
ms.date: 4/03/2019
ms.author: yinhew
ms.openlocfilehash: a9613f0839735457cf172fdacb0ef6a943ca27de
ms.sourcegitcommit: 4b9c06dad94dfb3a103feb2ee0da5a6202c910cc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/02/2019
ms.locfileid: "65020786"
---
# <a name="quickstart-synthesize-speech-in-c-on-windows-by-using-the-speech-sdk"></a>Guida introduttiva: Eseguire la sintesi vocale in C++ su Windows con Speech SDK

In questo articolo, viene creata un'applicazione console C++ per Windows. È possibile usare [Speech SDK](speech-sdk.md) di Servizi cognitivi per eseguire la sintesi vocale in tempo reale e riprodurre la voce dall'altoparlante del PC. L'applicazione si basa sul [pacchetto NuGet Speech SDK](https://aka.ms/csspeech/nuget) e su Microsoft Visual Studio 2017 (qualsiasi edizione).

La funzionalità disponibile in questo articolo è disponibile in [Speech SDK 1.5.0](https://www.nuget.org/packages/Microsoft.CognitiveServices.Speech/1.5.0).

Per un elenco completo di lingue/voci disponibili per la sintesi vocale, vedere [Supporto per le lingue](language-support.md#text-to-speech).

## <a name="prerequisites"></a>Prerequisiti

Per completare questa guida di avvio rapido, è necessaria una chiave di sottoscrizione di servizi Voce. È possibile ottenerne una gratuitamente. Per informazioni dettagliate, vedere [Provare gratuitamente servizi Voce](get-started.md).

## <a name="create-a-visual-studio-project"></a>Creare un progetto di Visual Studio

[!INCLUDE [Quickstart C++ project](../../../includes/cognitive-services-speech-service-quickstart-cpp-create-proj.md)]

## <a name="add-sample-code"></a>Aggiungere il codice di esempio

1. Aprire il file di origine *helloworld.cpp*. Sostituire tutto il codice seguente sotto l'istruzione iniziale di inclusione (`#include "stdafx.h"` o `#include "pch.h"`) con il codice seguente:

   [!code-cpp[Quickstart Code](~/samples-cognitive-services-speech-sdk/quickstart/text-to-speech/cpp-windows/helloworld/helloworld.cpp#code)]

1. Nello stesso file, sostituire la stringa `YourSubscriptionKey` con la chiave di sottoscrizione.

1. Sostituire la stringa `YourServiceRegion` con la [regione](regions.md) associata alla sottoscrizione (ad esempio, `westus` per la sottoscrizione di valutazione gratuita).

1. Salvare le modifiche apportate al progetto.

## <a name="build-and-run-the-app"></a>Compilare ed eseguire l'app

1. Compilare l'applicazione. Nella barra dei menu scegliere **Compila** > **Compila soluzione**. Il codice dovrebbe risultare compilato senza errori.

   ![Screenshot dell'applicazione Visual Studio, con l'opzione Compila soluzione selezionata](media/sdk/qs-cpp-windows-06-build.png)

1. Avviare l’applicazione. Nella barra dei menu scegliere **Debug** > **Avvia debug** o premere **F5**.

   ![Screenshot dell'applicazione Visual Studio, con l'opzione Avvio del debug selezionata](media/sdk/qs-cpp-windows-07-start-debugging.png)

1. Viene visualizzata una finestra della console che chiede di digitare un testo. Digitare alcune parole o una frase. Il testo digitato viene trasmesso ai servizi Voce e sintetizzato in voce, che viene riprodotta dall'altoparlante.

   ![Screenshot dell'output della console dopo la sintesi riuscita](media/sdk/qs-tts-cpp-windows-console-output.png)

## <a name="next-steps"></a>Passaggi successivi

Esempi aggiuntivi, ad esempio per salvare il parlato in un file audio, sono disponibili su GitHub.

> [!div class="nextstepaction"]
> [Esaminare gli esempi di codice C++ su GitHub](https://aka.ms/csspeech/samples)

## <a name="see-also"></a>Vedere anche 

- [Personalizzare i carattere voce](how-to-customize-voice-font.md)
- [Registrare esempi vocali](record-custom-voice-samples.md)
