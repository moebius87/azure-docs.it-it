---
title: Creare un modulo Python personalizzato - Azure IoT Edge | Microsoft Docs
description: Questa esercitazione illustra come creare un modulo per IoT Edge con codice Python e distribuirlo in un dispositivo perimetrale.
services: iot-edge
author: shizn
manager: philmea
ms.reviewer: kgremban
ms.author: xshi
ms.date: 03/24/2019
ms.topic: tutorial
ms.service: iot-edge
ms.custom: mvc, seodec18
ms.openlocfilehash: 0affd965bbfc587933a9cdbf5b96c470a6e4dd6a
ms.sourcegitcommit: c63fe69fd624752d04661f56d52ad9d8693e9d56
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2019
ms.locfileid: "58578289"
---
# <a name="tutorial-develop-and-deploy-a-python-iot-edge-module-to-your-simulated-device"></a>Esercitazione: Sviluppare e distribuire un modulo Python per IoT Edge in un dispositivo simulato

È possibile usare i moduli di Azure IoT Edge per distribuire codice che implementa la logica di business direttamente nei dispositivi di IoT Edge. Questa esercitazione illustra la creazione e distribuzione di un modulo IoT Edge che filtra i dati del sensore nel dispositivo IoT Edge configurato nell'argomento di avvio rapido. In questa esercitazione si apprenderà come:    

> [!div class="checklist"]
> * Usare Visual Studio Code per creare un modulo Python per IoT Edge.
> * Usare Visual Studio Code e Docker per creare un'immagine Docker e pubblicarla nel registro.
> * Distribuire il modulo nel dispositivo IoT Edge.
> * Visualizzare i dati generati.


Il modulo di IoT Edge creato in questa esercitazione filtra i dati relativi alla temperatura generati dal dispositivo. Invia messaggi upstream solo quando la temperatura è superiore a una soglia specificata. Questo tipo di analisi alla rete perimetrale è utile per ridurre la quantità di dati comunicati e archiviati nel cloud. 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]


## <a name="prerequisites"></a>Prerequisiti

Un dispositivo Azure IoT Edge:

* È possibile usare una macchina virtuale di Azure come dispositivo IoT Edge seguendo la procedura illustrata nell'argomento di avvio rapido per [Linux](quickstart-linux.md).
* I moduli Python per IoT Edge non supportano i contenitori Windows.

Risorse cloud:

* Un [hub IoT](../iot-hub/iot-hub-create-through-portal.md) di livello Gratuito o Standard in Azure. 

Risorse per lo sviluppo:

* [Visual Studio Code](https://code.visualstudio.com/). 
* [Strumenti di Azure IoT](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-edge) per Visual Studio Code.
* [Estensione Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) per Visual Studio Code. 
* [Python](https://www.python.org/downloads/).
* [Pip](https://pip.pypa.io/en/stable/installing/#installation) per l'installazione di pacchetti Python (generalmente incluso con l'installazione di Python).
* [Docker CE](https://docs.docker.com/install/). 
  * Per lo sviluppo in un computer Windows, verificare che Docker sia [configurato per l'uso di contenitori Linux](https://docs.docker.com/docker-for-windows/#switch-between-windows-and-linux-containers). 

>[!Note]
>Assicurarsi che la cartella `bin` sia nel percorso per la piattaforma, in genere `~/.local/` per UNIX e macOS o `%APPDATA%\Python` in Windows.

## <a name="create-a-container-registry"></a>Creare un registro contenitori

In questa esercitazione vengono usati gli strumenti di Azure IoT per Visual Studio Code per creare un modulo e un'**immagine del contenitore** dai file. Eseguire quindi il push dell'immagine in un **registro** che archivia e gestisce le immagini. Distribuire infine l'immagine dal registro nel dispositivo IoT Edge.  

È possibile usare qualsiasi registro compatibile con Docker per inserire le immagini dei contenitori. Due servizi di registro Docker molto diffusi sono [Registro Azure Container](https://docs.microsoft.com/azure/container-registry/) e [Hub Docker](https://docs.docker.com/docker-hub/repos/#viewing-repository-tags). Questa esercitazione usa il Registro Azure Container. 

Se non è ancora disponibile alcun registro contenitori, seguire questa procedura per crearne uno nuovo in Azure:

1. Nel [portale di Azure](https://portal.azure.com) selezionare **Crea una risorsa** > **Contenitori** > **Registro Container**.

2. Specificare i valori seguenti per creare il registro contenitori:

   | Campo | Valore | 
   | ----- | ----- |
   | Nome registro | Specificare un nome univoco. |
   | Sottoscrizione | Selezionare una sottoscrizione nell'elenco a discesa. |
   | Gruppo di risorse | È consigliabile usare lo stesso gruppo di risorse per tutte le risorse di test create durante le esercitazioni e le guide introduttive di IoT Edge. Ad esempio, **IoTEdgeResources**. |
   | Località | Scegliere una località vicina. |
   | Utente amministratore | Impostare su **Abilita**. |
   | SKU | Selezionare **Basic**. | 

5. Selezionare **Create**.

6. Dopo aver creato il registro contenitori, passare al registro e quindi selezionare **Chiavi di accesso**. 

7. Copiare i valori nei campi **Server di accesso**, **Nome utente** e **Password**. Usare questi valori più avanti nell'esercitazione per fornire l'accesso al registro contenitori. 

## <a name="create-an-iot-edge-module-project"></a>Creare un progetto di modulo IoT Edge
La procedura seguente consente di creare un modulo Python per IoT Edge tramite Visual Studio Code e gli strumenti di Azure IoT.

### <a name="create-a-new-solution"></a>Creare una nuova soluzione

Usare il pacchetto Python **cookiecutter** per creare un modello di soluzione Python a partire dalla quale eseguire la compilazione. 

1. In Visual Studio Code selezionare **Visualizza** > **Terminale** per aprire il terminale integrato di Visual Studio Code.

2. Nel terminale immettere il comando seguente per installare o aggiornare **cookiecutter**, usato per creare il modello di soluzione IoT Edge:

    ```cmd/sh
    pip install --upgrade --user cookiecutter
    ```
   >[!Note]
   >Assicurarsi che la directory in cui verrà installato cookiecutter sia nell'elemento PATH dell'ambiente in modo che sia possibile richiamarlo da un prompt dei comandi. La directory è inclusa nell'output dello script di installazione, ad esempio `C:\Users\{user}\AppData\Roaming\Python\Python{version}\Scripts`.
   >
   >Riavviare Visual Studio Code per rendere effettive le modifiche apportate a PATH. 

3. Selezionare **Visualizza** > **Riquadro comandi** per aprire il riquadro comandi di VS Code. 

4. Nel riquadro comandi immettere ed eseguire il comando **Azure: Accedere** e seguire le istruzioni per accedere all'account Azure. Se è stato già effettuato l'accesso, è possibile ignorare questo passaggio.

5. Nel riquadro comandi immettere ed eseguire il comando **Azure IoT Edge: Nuova soluzione IoT Edge**. Seguire i prompt e specificare le informazioni seguenti per creare la soluzione:

   | Campo | Valore |
   | ----- | ----- |
   | Selezionare la cartella | Nel computer di sviluppo scegliere la posizione in cui Visual Studio Code dovrà creare i file della soluzione. |
   | Provide a solution name (Specificare un nome per la soluzione) | Immettere un nome descrittivo per la soluzione oppure accettare quello predefinito **EdgeSolution**. |
   | Select module template (Selezionare un modello di modulo) | Scegliere **Modulo Python**. |
   | Provide a module name (Specificare un nome per il modulo) | Assegnare al modulo il nome **PythonModule**. |
   | Provide Docker image repository for the module (Specificare il repository di immagini Docker per il modulo) | Un repository di immagini include il nome del registro contenitori e il nome dell'immagine del contenitore. L'immagine del contenitore viene preinserita in base al nome specificato nell'ultimo passaggio. Sostituire **localhost:5000** con il valore del server di accesso in Registro Azure Container. È possibile recuperare il server di accesso dalla pagina Panoramica del registro contenitori nel portale di Azure. <br><br>Il repository di immagini finale sarà simile a \<nome registro\>.azurecr.io/pythonmodule. |
 
   ![Specificare il repository di immagini Docker](./media/tutorial-python-module/repository.png)

La finestra di VS Code carica l'area di lavoro della soluzione IoT Edge. L'area di lavoro della soluzione contiene cinque componenti di livello superiore. La cartella **modules** contiene il codice Python per il modulo e i Dockerfile per creare il modulo come un'immagine del contenitore. Il file **\.env** archivia le credenziali del registro contenitori. Il file **deployment.template.json** contiene le informazioni che il runtime IoT Edge usa per distribuire i moduli in un dispositivo. Il file **deployment.debug.template.json** contiene invece la versione di debug dei moduli. In questa esercitazione non verranno modificati né la cartella **\.vscode** né il file **\.gitignore**.  

Se non è stato specificato un registro contenitori durante la creazione della soluzione, ma è stato accettato il valore predefinito localhost:5000, non sarà presente il file con estensione \. env. 

<!--
   ![Python solution workspace](./media/tutorial-python-module/workspace.png)
-->

### <a name="add-your-registry-credentials"></a>Aggiungere le credenziali del registro

Il file dell'ambiente archivia le credenziali per il repository di contenitori e le condivide con il runtime IoT Edge. Queste credenziali sono necessarie al runtime per eseguire il pull delle immagini private nel dispositivo IoT Edge. 

1. Nello strumento di esplorazione di VS Code aprire il file con estensione **env**. 
2. Aggiornare i campi con i valori di **nome utente** e **password** copiati dal registro contenitori di Azure. 
3. Salvare il file con estensione env. 

### <a name="update-the-module-with-custom-code"></a>Aggiornare il modulo con il codice personalizzato

In ogni modello è incluso il codice di esempio, che accetta i dati del sensore simulato dal modulo **tempSensor** e li indirizza all'hub IoT. In questa sezione aggiungere il codice che espande **PythonModule** per analizzare i messaggi prima di inviarli. 

1. Nello strumento di esplorazione di VS Code aprire **modules** > **PythonModule** > **main.py**.

2. All'inizio del file **main.py** importare la libreria **json**:

    ```python
    import json
    ```

3. Aggiungere le variabili **TEMPERATURE_THRESHOLD** e **TWIN_CALLBACKS** nei contatori globali. La soglia della temperatura imposta il valore che la temperatura del computer misurata deve superare per inviare i dati all'hub IoT.

    ```python
    TEMPERATURE_THRESHOLD = 25
    TWIN_CALLBACKS = 0
    ```

4. Sostituire la funzione **receive_message_callback** con il codice seguente:

    ```python
    # receive_message_callback is invoked when an incoming message arrives on the specified 
    # input queue (in the case of this sample, "input1").  Because this is a filter module, 
    # we forward this message to the "output1" queue.
    def receive_message_callback(message, hubManager):
        global RECEIVE_CALLBACKS
        global TEMPERATURE_THRESHOLD
        message_buffer = message.get_bytearray()
        size = len(message_buffer)
        message_text = message_buffer[:size].decode('utf-8')
        print ( "    Data: <<<%s>>> & Size=%d" % (message_text, size) )
        map_properties = message.properties()
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        RECEIVE_CALLBACKS += 1
        print ( "    Total calls received: %d" % RECEIVE_CALLBACKS )
        data = json.loads(message_text)
        if "machine" in data and "temperature" in data["machine"] and data["machine"]["temperature"] > TEMPERATURE_THRESHOLD:
            map_properties.add("MessageType", "Alert")
            print("Machine temperature %s exceeds threshold %s" % (data["machine"]["temperature"], TEMPERATURE_THRESHOLD))
        hubManager.forward_event_to_output("output1", message, 0)
        return IoTHubMessageDispositionResult.ACCEPTED
    ```

5. Aggiungere una nuova funzione denominata **module_twin_callback**. Questa funzione viene richiamata quando le proprietà desiderate vengono aggiornate.

    ```python
    # module_twin_callback is invoked when the module twin's desired properties are updated.
    def module_twin_callback(update_state, payload, user_context):
        global TWIN_CALLBACKS
        global TEMPERATURE_THRESHOLD
        print ( "\nTwin callback called with:\nupdateStatus = %s\npayload = %s\ncontext = %s" % (update_state, payload, user_context) )
        data = json.loads(payload)
        if "desired" in data and "TemperatureThreshold" in data["desired"]:
            TEMPERATURE_THRESHOLD = data["desired"]["TemperatureThreshold"]
        if "TemperatureThreshold" in data:
            TEMPERATURE_THRESHOLD = data["TemperatureThreshold"]
        TWIN_CALLBACKS += 1
        print ( "Total calls confirmed: %d\n" % TWIN_CALLBACKS )
    ```

6. Nella classe **HubManager** aggiungere una nuova riga al metodo **__init__** per inizializzare la funzione **module_twin_callback** appena aggiunta:

    ```python
    # Sets the callback when a module twin's desired properties are updated.
    self.client.set_module_twin_callback(module_twin_callback, self)
    ```

7. Salvare il file main.py.

8. Nello strumento di esplorazione di VS Code aprire il file **deployment.template.json** nell'area di lavoro della soluzione IoT Edge. Questo file indica all'agente di IoT Edge quali moduli distribuire, in questo caso **tempSensor** e **PythonModule**, e indica all'hub di IoT Edge come indirizzare i messaggi tra i moduli. L'estensione di Visual Studio Code popola automaticamente la maggior parte delle informazioni necessarie nel modello di distribuzione, ma occorre assicurarsi che le informazioni siano appropriate per la soluzione specifica: 

   1. La piattaforma predefinita del dispositivo IoT Edge è impostata su **amd64** nella barra di stato di VS Code, di conseguenza **PythonModule** è impostato sulla versione amd64 Linux dell'immagine. Cambiare la piattaforma predefinita nella barra di stato da **amd64** a **arm32v7** se corrisponde all'architettura del dispositivo IoT Edge. 

      ![Aggiornare la piattaforma di immagini del modulo](./media/tutorial-python-module/image-platform.png)

   2. Verificare che il modello abbia il nome modulo corretto, non il nome **SampleModule** predefinito che è stato modificato durante la creazione della soluzione IoT Edge.

   3. La sezione **registryCredentials** archivia le credenziali del registro Docker, in modo che l'agente di IoT Edge possa eseguire il pull dell'immagine del modulo. Le coppie effettive di username e password vengono archiviate nel file ENV, che viene ignorato da Git. Aggiungere le credenziali al file con estensione env, se non è già stato fatto.  

   4. Per altre informazioni sui manifesti della distribuzione, vedere [Informazioni su come distribuire moduli e definire route in IoT Edge](module-composition.md).

9. Aggiungere il modulo gemello **PythonModule** al manifesto della distribuzione. Inserire il contenuto JSON seguente alla fine della sezione **moduleContent** dopo il modulo gemello **$edgeHub**: 

   ```json
       "PythonModule": {
           "properties.desired":{
               "TemperatureThreshold":25
           }
       }
   ```

   ![Aggiungere il modulo gemello al modello di distribuzione](./media/tutorial-python-module/module-twin.png)

10. Salvare il file deployment.template.json.

## <a name="build-and-push-your-solution"></a>Compilare ed eseguire il push della soluzione

Nella sezione precedente è creata una soluzione IoT Edge ed è stato aggiunto a **PythonModule** il codice per filtrare i messaggi in cui la temperatura del computer segnalata è inferiore alla soglia accettabile. È ora necessario compilare la soluzione come immagine del contenitore ed eseguirne il push nel registro contenitori. 

1. Accedere a Docker immettendo il comando seguente nel terminale integrato di Visual Studio Code. È quindi possibile eseguire il push dell'immagine del modulo nel registro contenitori di Azure: 
     
   ```csh/sh
   docker login -u <ACR username> -p <ACR password> <ACR login server>
   ```
   Usare il nome utente, la password e il server di accesso copiati dal registro contenitori di Azure nella prima sezione. È anche possibile recuperare questi valori dalla sezione **Chiavi di accesso** del registro nel portale di Azure.

   È possibile che venga visualizzato un avviso di sicurezza in cui si consiglia l'uso del parametro --password-stdin. Sebbene il suo utilizzo non rientri nell'ambito di questo articolo, si raccomanda di seguire questa procedura consigliata. Per altre informazioni, vedere la guida comandi di [accesso di Docker](https://docs.docker.com/engine/reference/commandline/login/#provide-a-password-using-stdin). 


2. Nello strumento di esplorazione di Visual Studio Code fare clic con il pulsante destro del mouse sul file deployment.template.json e scegliere **Build and Push IoT Edge solution** (Compila ed esegui il push della soluzione IoT Edge). 

Quando si comunica a Visual Studio Code di compilare la soluzione, prima di tutto con le informazioni del modello di distribuzione viene generato un file deployment.json in una nuova cartella denominata **config**. Vengono quindi eseguiti due comandi nel terminale integrato: `docker build` e `docker push`. Questi due comandi compilano il codice, includono il codice Python in un contenitore e ne eseguono il push nel registro contenitori specificato quando è stata inizializzata la soluzione. 

È possibile visualizzare l'indirizzo completo dell'immagine del contenitore con tag nel comando `docker build` eseguito nel terminale integrato di VS Code. L'indirizzo dell'immagine è costituito dalle informazioni presenti nel file module.json nel formato \<repository\>:\<versione\>-\<piattaforma\>. Per questa esercitazione il risultato sarà simile a registryname.azurecr.io/pythonmodule:0.0.1-amd64.

>[!TIP]
>Se quando si prova a compilare ed eseguire il push del modulo viene visualizzato un errore, effettuare i controlli seguenti:
>* L'accesso a Docker in Visual Studio Code è stato eseguito con le credenziali del registro contenitori? Queste credenziali sono diverse rispetto a quelle usate per accedere al portale di Azure.
>* Il repository di contenitori è corretto? Aprire **modules** > **PythonModule** > **module.json** e trovare il campo **repository**. Il repository di immagini sarà simile a **\<nomeregistro\>.azurecr.io/pythonmodule**. 
>* Si sta compilando lo stesso tipo di contenitori eseguito dal computer di sviluppo? L'impostazione predefinita in Visual Studio Code è costituita dai contenitori Linux amd64. Se il computer di sviluppo esegue contenitori Linux arm32v7, aggiornare la piattaforma sulla barra di stato blu nella parte inferiore della finestra di VS Code in modo che corrisponda. I moduli Python non supportano i contenitori Windows. 

## <a name="deploy-and-run-the-solution"></a>Distribuire ed eseguire la soluzione

Nell'articolo della guida introduttiva usato per configurare il dispositivo IoT Edge è stato distribuito un modulo usando il portale di Azure. È possibile distribuire i moduli anche usando l'estensione Azure hub IoT Toolkit (in precedenza estensione Azure IoT Toolkit) per Visual Studio Code. Il manifesto della distribuzione, il file **deployment.json**, è già disponibile per questo scenario. Ora è sufficiente selezionare un dispositivo che riceverà la distribuzione.

1. Nel riquadro comandi di VS Code eseguire **hub IoT di Azure: Selezionare l'hub IoT**. 

2. Scegliere la sottoscrizione e l'hub IoT che contiene il dispositivo IoT Edge che si vuole configurare. 

3. Nello strumento di esplorazione di VS Code espandere la sezione **Azure IoT Hub dispositivi** (Dispositivi dell'hub IoT di Azure). 

4. Fare clic con il pulsante destro del mouse sul nome del dispositivo IoT Edge, quindi selezionare **Create Deployment for Single Device** (Crea la distribuzione per un unico dispositivo). 

   ![Create deployment for single device (Crea la distribuzione per un unico dispositivo)](./media/tutorial-python-module/create-deployment.png)

5. Selezionare il file **deployment.amd64** o **deployment.arm32v7** (a seconda dell'architettura di destinazione) nella cartella **config** e quindi fare clic su **Select Edge Deployment Manifest** (Seleziona il manifesto della distribuzione di Edge). Non usare il file deployment.template.json. 

6. Fare clic sul pulsante Aggiorna. Dovrebbe essere visualizzato il nuovo **PythonModule** in esecuzione insieme al modulo **TempSensor** e a **$edgeAgent** e **$edgeHub**. 

## <a name="view-generated-data"></a>Visualizzare i dati generati

Dopo aver applicato il manifesto della distribuzione al dispositivo IoT Edge, il runtime di IoT Edge nel dispositivo raccoglie le informazioni della nuova distribuzione e si avvia all'interno di questa. Tutti i moduli in esecuzione nel dispositivo che non sono inclusi nel manifesto della distribuzione vengono arrestati. Tutti i moduli mancanti dal dispositivo vengono avviati. 

È possibile visualizzare lo stato del dispositivo IoT Edge tramite la sezione **Azure IoT Hub Devices** (Dispositivi hub IoT di Azure) della finestra di esplorazione di Visual Studio Code. Espandere i dettagli del dispositivo per visualizzare un elenco dei moduli distribuiti e in esecuzione. 

Nel dispositivo IoT Edge stesso è possibile visualizzare lo stato dei moduli della distribuzione usando il comando `iotedge list`. Devono essere presenti quattro moduli: i due moduli di runtime di IoT Edge, tempSensor e il modulo personalizzato creato in questa esercitazione. L'avvio di tutti i moduli può richiedere qualche minuto. Rieseguire quindi il comando se inizialmente non sono visualizzati tutti. 

Per visualizzare i messaggi generati da un qualsiasi modulo, usare il comando `iotedge logs <module name>`. 

È possibile visualizzare i messaggi man mano che arrivano nell'hub IoT tramite Visual Studio Code. 

1. Per monitorare i dati che arrivano all'hub IoT, selezionare i puntini di sospensione (**...**) e quindi selezionare **Start Monitoring D2C Messages** (Avvia il monitoraggio dei messaggi D2C).
2. Per monitorare il messaggio D2C per un dispositivo specifico, fare clic con il pulsante destro del mouse sul dispositivo nell'elenco e scegliere **Start Monitoring D2C Messages** (Avvia il monitoraggio dei messaggi D2C).
3. Per interrompere il monitoraggio dei dati, eseguire il comando **hub IoT di Azure: Interrompere il monitoraggio di messaggi D2C** nel riquadro comandi. 
4. Per visualizzare o aggiornare il modulo gemello, fare clic con il pulsante destro del mouse sul modulo nell'elenco e scegliere **Edit module twin** (Modifica il modulo gemello). Per aggiornare il modulo gemello, salvare il file JSON gemello, fare clic con il pulsante destro del mouse sull'area degli editor e scegliere **Update Module Twin** (Aggiorna il modulo gemello).
5. Per visualizzare i log di Docker, installare l'[estensione Docker per Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=PeterJausovec.vscode-docker). È possibile trovare i moduli in esecuzione in locale nello strumento di esplorazione di Docker. Dal menu di scelta rapida scegliere **Mostra log** per visualizzarli nel terminale integrato. 

## <a name="clean-up-resources"></a>Pulire le risorse 

Se si intende continuare con il prossimo articolo consigliato, è possibile conservare le risorse e le configurazioni create e riutilizzarle. È anche possibile continuare a usare lo stesso dispositivo IoT Edge come dispositivo di test. 

In caso contrario, è possibile eliminare le risorse di Azure e le configurazioni locali create in questo articolo per evitare addebiti. 

[!INCLUDE [iot-edge-clean-up-cloud-resources](../../includes/iot-edge-clean-up-cloud-resources.md)]


## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è stato creato un modulo di IoT Edge con codice per filtrare i dati non elaborati generati dal dispositivo di IoT Edge. È possibile continuare con le esercitazioni successive per ottenere informazioni sugli altri modi in cui Azure IoT Edge può contribuire alla trasformazione dei dati in informazioni dettagliate aziendali nei dispositivi perimetrali.

> [!div class="nextstepaction"]
> [Distribuire Funzioni di Azure come modulo](tutorial-deploy-function.md)
> [Distribuire Analisi di flusso di Azure come modulo](tutorial-deploy-stream-analytics.md)
