---
title: Creare un ciclo di feedback - Personalizza esperienze
titleSuffix: Azure Cognitive Services
description: Personalizzare il contenuto in questa guida di avvio rapido di C# con il servizio Personalizza esperienze.
services: cognitive-services
author: edjez
manager: nitinme
ms.service: cognitive-services
ms.subservice: personalizer
ms.topic: overview
ms.date: 05/07/2019
ms.author: edjez
ms.openlocfilehash: c566d1fd4b151efc0d28b7059504e60a1451c034
ms.sourcegitcommit: 4b9c06dad94dfb3a103feb2ee0da5a6202c910cc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/02/2019
ms.locfileid: "65025510"
---
# <a name="quickstart-personalize-content-using-c"></a>Guida introduttiva: Personalizzare il contenuto con C# 

Visualizzare il contenuto personalizzato in questa guida di avvio rapido di C# con il servizio Personalizza esperienze.

Questo esempio illustra come usare la libreria client di Personalizzazione per C# per eseguire le azioni seguenti: 

 * Classificare un elenco di azioni per la personalizzazione.
 * Segnalare la ricompensa da assegnare all'azione nella posizione più alta in classifica in base alla selezione dell'utente per l'evento specificato.

L'introduzione a Personalizzazione include i passaggi seguenti:

1. Aggiunta del riferimento all'SDK. 
1. Scrittura del codice per classificare le azioni che si vogliono mostrare agli utenti.
1. Scrittura del codice per inviare le ricompense per il training del ciclo.

## <a name="prerequisites"></a>Prerequisiti

* Sono necessari una chiave di sottoscrizione e l'URL del servizio di emissione dei token.
* [Visual Studio 2015 o 2017](https://visualstudio.microsoft.com/downloads/).
* Pacchetto NuGet Microsoft.Azure.CognitiveServices.Personalization dell'SDK. Le istruzioni di installazione sono disponibili più avanti.

## <a name="creating-a-new-console-app-and-referencing-the-personalizer-sdk"></a>Creazione di una nuova app console e aggiunta del riferimento a Personalizer SDK 

<!--
Get the latest code as a Visual Studio solution from [GitHub] (add link).
-->

1. Creare una nuova app console Visual C# in Visual Studio.
1. Installare il pacchetto NuGet della libreria client di Personalizzazione. Nel menu selezionare **Strumenti**, **Gestione pacchetti NuGet** e quindi **Gestisci pacchetti NuGet per la soluzione**.
1. Selezionare la scheda **Sfoglia** e nella casella di **ricerca** digitare `Microsoft.Azure.CognitiveServices.Personalization`.
1. Selezionare la voce **Microsoft.Azure.CognitiveServices.Personalization** quando viene visualizzata.
1. Selezionare la casella di controllo accanto al nome del progetto e scegliere **Installa**.

## <a name="add-the-code-and-put-in-your-personalizer-and-azure-keys"></a>Aggiungere il codice e inserire le chiavi di Personalizza esperienze e Azure

1. Sostituire Program.cs con il codice seguente. 
1. Sostituire il valore `serviceKey` con la chiave di sottoscrizione di Personalizza esperienze valida.
1. Sostituire `serviceEndpoint` con l'endpoint servizio. Un esempio è `https://westus2.api.cognitive.microsoft.com/`.
1. Eseguire il programma.

## <a name="add-code-to-rank-the-actions-you-want-to-show-to-your-users"></a>Aggiungere il codice per classificare le azioni che si vogliono mostrare agli utenti

Il codice C# seguente è un listato completo per passare le informazioni utente, le funzionalità, le informazioni sul contenuto e le _azioni_ a Personalizza esperienze usando l'SDK. Personalizza esperienze restituisce l'azione nella posizione più alta in classifica da visualizzare l'utente.  

```csharp
using Microsoft.Azure.CognitiveServices.Personalization;
using Microsoft.Azure.CognitiveServices.Personalization.Models;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net.Http;

namespace PersonalizationExample
{
    class Program
    {
        // The key specific to your personalization service instance; e.g. "0123456789abcdef0123456789ABCDEF"
        private const string serviceKey = "";

        // The endpoint specific to your personalization service instance; e.g. https://westus2.api.cognitive.microsoft.com/
        private const string serviceEndpoint = "";

        static void Main(string[] args)
        {
            int iteration = 1;
            bool runLoop = true;

            Uri url = new Uri(serviceEndpoint);

            // Get the actions list to choose from personalization with their features.
            IList<RankableAction> actions = GetActions();

            // Initialize Personalization client.
            PersonalizationClient client = InitializePersonalizationClient(url);

            do
            {
                Console.WriteLine("\nIteration: " + iteration++);

                // Get context information from the user.
                string timeOfDayFeature = GetUsersTimeOfDay();
                string tasteFeature = GetUsersTastePreference();

                // Create current context from user specified data.
                IList<object> currentContext = new List<object>() {
                    new { time = timeOfDayFeature },
                    new { taste = tasteFeature }
                };

                // Exclude an action for personalization ranking. This action will be held at its current position.
                IList<string> excludeActions = new List<string> { "juice" };

                // Generate an ID to associate with the request.
                string eventId = Guid.NewGuid().ToString();

                // Rank the actions
                var request = new RankRequest(actions, currentContext, excludeActions, eventId);
                RankResponse response = client.Rank(request);

                Console.WriteLine("\nPersonalization service thinks you would like to have: " + response.RewardActionId + ". Is this correct? (y/n)");

                float reward = 0.0f;
                string answer = GetKey();

                if (answer == "Y")
                {
                    reward = 1;
                    Console.WriteLine("\nGreat! Enjoy your food.");
                }
                else if (answer == "N")
                {
                    reward = 0;
                    Console.WriteLine("\nYou didn't like the recommended food choice.");
                }
                else
                {
                    Console.WriteLine("\nEntered choice is invalid. Service assumes that you didn't like the recommended food choice.");
                }

                Console.WriteLine("\nPersonalization service ranked the actions with the probabilities as below:");
                foreach (var rankedResponse in response.Ranking)
                {
                    Console.WriteLine(rankedResponse.Id + " " + rankedResponse.Probability);
                }

                // Send the reward for the action based on user response.
                client.Reward(response.EventId, new RewardRequest(reward));

                Console.WriteLine("\nPress q to break, any other key to continue:");
                runLoop = !(GetKey() == "Q");

            } while (runLoop);
        }

        /// <summary>
        /// Initializes the personalization client.
        /// </summary>
        /// <param name="url">Azure endpoint</param>
        /// <returns>Personalization client instance</returns>
        static PersonalizationClient InitializePersonalizationClient(Uri url)
        {
            PersonalizationClient client = new PersonalizationClient(url,
            new ApiKeyServiceClientCredentials(serviceKey),
            new DelegatingHandler[] { });

            return client;
        }

        /// <summary>
        /// Get users time of the day context.
        /// </summary>
        /// <returns>Time of day feature selected by the user.</returns>
        static string GetUsersTimeOfDay()
        {
            string[] timeOfDayFeatures = new string[] { "morning", "afternoon", "evening", "night" };

            Console.WriteLine("\nWhat time of day is it (enter number)? 1. morning 2. afternoon 3. evening 4. night");
            if (!int.TryParse(GetKey(), out int timeIndex) || timeIndex < 1 || timeIndex > timeOfDayFeatures.Length)
            {
                Console.WriteLine("\nEntered value is invalid. Setting feature value to " + timeOfDayFeatures[0] + ".");
                timeIndex = 1;
            }

            return timeOfDayFeatures[timeIndex - 1];
        }

        /// <summary>
        /// Gets user food preference.
        /// </summary>
        /// <returns>Food taste feature selected by the user.</returns>
        static string GetUsersTastePreference()
        {
            string[] tasteFeatures = new string[] { "salty", "sweet" };

            Console.WriteLine("\nWhat type of food would you prefer (enter number)? 1. salty 2. sweet");
            if (!int.TryParse(GetKey(), out int tasteIndex) || tasteIndex < 1 || tasteIndex > tasteFeatures.Length)
            {
                Console.WriteLine("\nEntered value is invalid. Setting feature value to " + tasteFeatures[0] + ".");
                tasteIndex = 1;
            }

            return tasteFeatures[tasteIndex - 1];
        }

        /// <summary>
        /// Creates personalization actions feature list.
        /// </summary>
        /// <returns>List of actions for personalization.</returns>
        static IList<RankableAction> GetActions()
        {
            IList<RankableAction> actions = new List<RankableAction>
            {
                new RankableAction
                {
                    Id = "pasta",
                    Features =
                    new List<object>() { new { taste = "salty", spiceLevel = "medium" }, new { nutritionLevel = 5, cuisine = "italian" } }
                },

                new RankableAction
                {
                    Id = "ice cream",
                    Features =
                    new List<object>() { new { taste = "sweet", spiceLevel = "none" }, new { nutritionalLevel = 2 } }
                },

                new RankableAction
                {
                    Id = "juice",
                    Features =
                    new List<object>() { new { taste = "sweet", spiceLevel = "none" }, new { nutritionLevel = 5 }, new { drink = true } }
                },

                new RankableAction
                {
                    Id = "salad",
                    Features =
                    new List<object>() { new { taste = "salty", spiceLevel = "low" }, new { nutritionLevel = 8 } }
                }
            };

            return actions;
        }

        private static string GetKey()
        {
            return Console.ReadKey().Key.ToString().Last().ToString().ToUpper();
        }
    }
}
```

## <a name="run-the-program"></a>Eseguire il programma

Compilare ed eseguire il programma. Il programma di avvio rapido pone alcune domande per raccogliere le preferenze utente, note come funzionalità, quindi restituisce l'azione più comune.

![Il programma di avvio rapido pone alcune domande per raccogliere le preferenze utente, note come funzionalità, quindi restituisce l'azione più comune.](media/csharp-quickstart-commandline-feedback-loop/quickstart-program-feedback-loop-example.png)

## <a name="clean-up-resources"></a>Pulire le risorse
Dopo aver completato la procedura illustrata, rimuovere tutti i file creati in questa guida introduttiva. 

## <a name="next-steps"></a>Passaggi successivi

[Funzionamento di Personalizza esperienze](how-personalizer-works.md)


