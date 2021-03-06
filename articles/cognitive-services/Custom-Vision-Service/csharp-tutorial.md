---
title: "Guida introduttiva: Creare un progetto di classificazione immagini con l'SDK Servizio visione artificiale personalizzato per C#"
titlesuffix: Azure Cognitive Services
description: Creare un progetto, aggiungere i tag, caricare le immagini, eseguire il training del progetto ed effettuare una stima usando .NET SDK con C#.
services: cognitive-services
author: anrothMSFT
manager: nitinme
ms.service: cognitive-services
ms.subservice: custom-vision
ms.topic: quickstart
ms.date: 03/21/2019
ms.author: anroth
ms.openlocfilehash: 9b6d01908265791a83ee311375fa50fcca995f79
ms.sourcegitcommit: fbfe56f6069cba027b749076926317b254df65e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/26/2019
ms.locfileid: "58472728"
---
# <a name="quickstart-create-an-image-classification-project-with-the-custom-vision-net-sdk"></a>Guida introduttiva: Creare un progetto di classificazione immagini con .NET SDK Servizio visione artificiale personalizzato

Questo articolo fornisce informazioni e codice di esempio utili per iniziare a usare Custom Vision SDK con C# per compilare un modello di classificazione delle immagini. Dopo la creazione, è possibile aggiungere tag, caricare immagini, eseguire il training del progetto, ottenere l'URL dell'endpoint predefinito per la stima del progetto e usare l'endpoint per un test a livello di codice dell'immagine. Usare questo esempio come modello per la creazione di un'applicazione .NET personalizzata. Se si preferisce eseguire la procedura di compilazione e utilizzo di un modello di classificazione _senza_ codice, vedere le [indicazioni basate su browser](getting-started-build-a-classifier.md).

## <a name="prerequisites"></a>Prerequisiti

- Qualsiasi edizione di [Visual Studio 2015 o 2017](https://www.visualstudio.com/downloads/).

## <a name="get-the-custom-vision-sdk-and-sample-code"></a>Ottenere Custom Vision SDK e il codice di esempio

Per scrivere un'app .NET che usa Visione personalizzata saranno necessari i pacchetti NuGet di Visione personalizzata. Questi sono inclusi nel progetto di esempio che si scaricherà, ma è possibile accedervi singolarmente qui.

- [Microsoft.Azure.CognitiveServices.Vision.CustomVision.Training](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Vision.CustomVision.Training/)
- [Microsoft.Azure.CognitiveServices.Vision.CustomVision.Prediction](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Vision.CustomVision.Prediction/)

Clonare o scaricare il progetto [Cognitive Services .NET Samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples). Passare alla cartella **CustomVision/ImageClassification** e aprire _ImageClassification.csproj_ in Visual Studio.

Questo progetto di Visual Studio crea un nuovo progetto di Visione personalizzata denominato __My New Project__, accessibile tramite il [sito Web di Visione personalizzata](https://customvision.ai/). Quindi carica le immagini per eseguire il training e testare un classificatore. In questo progetto il classificatore ha lo scopo di determinare se un albero è un __abete canadese__ o un __ciliegio giapponese__.

[!INCLUDE [get-keys](includes/get-keys.md)]

## <a name="understand-the-code"></a>Informazioni sul codice

Aprire il file _Program.cs_ ed esaminare il codice. Inserire le chiavi di sottoscrizione nelle definizioni appropriate nel metodo **Main**.

[!code-csharp[](~/cognitive-services-dotnet-sdk-samples/CustomVision/ImageClassification/Program.cs?range=21-30)]

Il parametro Endpoint deve puntare all'area in cui è stato creato il gruppo di risorse di Azure contenente le risorse di Servizio visione artificiale personalizzato. Per questo esempio si presuppone l'area Stati Uniti centro-meridionali e si procede come segue:

[!code-csharp[](~/cognitive-services-dotnet-sdk-samples/CustomVision/ImageClassification/Program.cs?range=14-14)]

Le righe di codice seguenti eseguono la funzionalità principale del progetto.

### <a name="create-a-new-custom-vision-service-project"></a>Creare un nuovo progetto di Servizio visione artificiale personalizzato

Il progetto creato verrà visualizzato nel [sito Web di Visione personalizzata](https://customvision.ai/) visitato in precedenza. 

[!code-csharp[](~/cognitive-services-dotnet-sdk-samples/CustomVision/ImageClassification/Program.cs?range=32-34)]

### <a name="create-tags-in-the-project"></a>Creare tag nel progetto

[!code-csharp[](~/cognitive-services-dotnet-sdk-samples/CustomVision/ImageClassification/Program.cs?range=36-38)]

### <a name="upload-and-tag-images"></a>Caricare e contrassegnare le immagini

Le immagini per questo progetto sono incluse. Sono referenziate nel metodo **LoadImagesFromDisk** in _Program.cs_.

[!code-csharp[](~/cognitive-services-dotnet-sdk-samples/CustomVision/ImageClassification/Program.cs?range=40-55)]

### <a name="train-the-classifier-and-publish"></a>Training del classificatore e pubblicazione

Questo codice crea la prima iterazione del progetto e quindi la pubblica nell'endpoint di stima. Il nome assegnato all'iterazione pubblicata può essere usato per inviare le richieste di stima. L'iterazione è disponibile nell'endpoint di stima solo dopo che è stata pubblicata.

```csharp
// The returned iteration will be in progress, and can be queried periodically to see when it has completed
while (iteration.Status == "Training")
{
        Thread.Sleep(1000);

        // Re-query the iteration to get it's updated status
        iteration = trainingApi.GetIteration(project.Id, iteration.Id);
}

// The iteration is now trained. Publish it to the prediction end point.
var publishedModelName = "treeClassModel";
var predictionResourceId = "<target prediction resource ID>";
trainingApi.PublishIteration(project.Id, iteration.Id, publishedModelName, predictionResourceId);
Console.WriteLine("Done!\n");
```

### <a name="set-the-prediction-endpoint"></a>Impostare l'endpoint di stima

L'endpoint di stima è il riferimento che è possibile usare per inviare un'immagine al modello corrente e ottenere una stima di classificazione.

```csharp
// Create a prediction endpoint, passing in obtained prediction key
CustomVisionPredictionClient endpoint = new CustomVisionPredictionClient()
{
        ApiKey = predictionKey,
        Endpoint = SouthCentralUsEndpoint
};
```

### <a name="submit-an-image-to-the-default-prediction-endpoint"></a>Inviare un'immagine all'endpoint di stima predefinito

Questo script, l'immagine di test viene caricata nel metodo **LoadImagesFromDisk** e l'output delle stime del modello deve essere visualizzato nella console.

```csharp
// Make a prediction against the new project
Console.WriteLine("Making a prediction:");
var result = endpoint.ClassifyImage(project.Id, publishedModelName, testImage);

// Loop over each prediction and write out the results
foreach (var c in result.Predictions)
{
        Console.WriteLine($"\t{c.TagName}: {c.Probability:P1}");
}
```

## <a name="run-the-application"></a>Eseguire l'applicazione

Quando l'applicazione viene eseguita, dovrebbe aprire una finestra della console e scrivere l'output seguente:

```
Creating new project:
        Uploading images
        Training
Done!

Making a prediction:
        Hemlock: 95.0%
        Japanese Cherry: 0.0%
```

Si può quindi verificare che all'immagine di test (disponibile in **Images/Test/**) siano stati applicati i tag appropriati. Premere un tasto qualsiasi per uscire dall'applicazione. È anche possibile tornare al [sito Web di Visione personalizzata](https://customvision.ai) e vedere lo stato corrente del progetto appena creato.

[!INCLUDE [clean-ic-project](includes/clean-ic-project.md)]

## <a name="next-steps"></a>Passaggi successivi

In questa guida si è appreso come eseguire ogni passaggio del processo di classificazione delle immagini nel codice. Questo esempio esegue una sola iterazione del training, ma spesso è necessario eseguire il training e il test del modello più volte per ottenere una maggiore precisione.

> [!div class="nextstepaction"]
> [Testare un modello e ripeterne il training](test-your-model.md)
