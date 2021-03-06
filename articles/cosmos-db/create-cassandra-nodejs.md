---
title: 'Guida introduttiva: API Cassandra con Node.js - Azure Cosmos DB'
description: Questa guida introduttiva illustra come usare l'API Cassandra di Azure Cosmos DB per creare un'applicazione di profilo con Node.js
author: SnehaGunda
ms.author: sngun
ms.service: cosmos-db
ms.subservice: cosmosdb-cassandra
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 09/24/2018
ms.openlocfilehash: a8698bf74d8be4a57d5928b8be74bcf35cee008f
ms.sourcegitcommit: 7723b13601429fe8ce101395b7e47831043b970b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/21/2019
ms.locfileid: "56586138"
---
# <a name="quickstart-build-a-cassandra-app-with-nodejs-sdk-and-azure-cosmos-db"></a>Avvio rapido: Creare un'app Cassandra con Node.js SDK e Azure Cosmos DB

> [!div class="op_single_selector"]
> * [.NET](create-cassandra-dotnet.md)
> * [Java](create-cassandra-java.md)
> * [Node.js](create-cassandra-nodejs.md)
> * [Python](create-cassandra-python.md)
>  

Questa guida introduttiva mostra come usare Node.js e l'[API Cassandra](cassandra-introduction.md) di Azure Cosmos DB per creare un'app di profilo clonando un esempio di GitHub. La guida introduttiva illustra anche come usare il portale di Azure basato sul Web per creare un account Azure Cosmos DB.

Azure Cosmos DB è il servizio di database di Microsoft multimodello distribuito a livello globale. È possibile creare ed eseguire rapidamente query su database di documenti, tabelle, valori chiave e grafi, sfruttando in ognuno dei casi i vantaggi offerti dalle funzionalità di scalabilità orizzontale e distribuzione globale alla base di Azure Cosmos DB. 

## <a name="prerequisites"></a>Prerequisiti

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]In alternativa, è possibile [provare gratuitamente Microsoft Azure Cosmos DB](https://azure.microsoft.com/try/cosmosdb/) senza una sottoscrizione di Azure e senza impegno.

È anche necessario:
* [Node.js](https://nodejs.org/en/) 0.10.29 o versione successiva
* [Git](https://git-scm.com/)

## <a name="create-a-database-account"></a>Creare un account di database

Prima di poter creare un database di documenti, è necessario creare un account di Cassandra con Azure Cosmos DB.

[!INCLUDE [cosmos-db-create-dbaccount-cassandra](../../includes/cosmos-db-create-dbaccount-cassandra.md)]

## <a name="clone-the-sample-application"></a>Clonare l'applicazione di esempio

Clonare ora un'app per le API Cassandra da GitHub, impostare la stringa di connessione ed eseguirla. Come si noterà, è facile usare i dati a livello di codice. 

1. Aprire un prompt dei comandi. Creare una nuova cartella denominata `git-samples`, quindi chiudere il prompt dei comandi.

    ```bash
    md "C:\git-samples"
    ```

2. Aprire una finestra del terminale Git, ad esempio Git Bash. Usare il comando `cd` per passare alla nuova cartella e installare l'app di esempio.

    ```bash
    cd "C:\git-samples"
    ```

3. Eseguire il comando seguente per clonare l'archivio di esempio. Questo comando crea una copia dell'app di esempio nel computer in uso.

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-cassandra-nodejs-getting-started.git
    ```

## <a name="review-the-code"></a>Esaminare il codice

Questo passaggio è facoltativo. Per comprendere in che modo il codice crea le risorse del database, è possibile esaminare i frammenti di codice seguenti. I frammenti di codice provengono tutti dal file `uprofile.js` nella cartella `C:\git-samples\azure-cosmos-db-cassandra-nodejs-getting-started`. In alternativa, è possibile passare ad [Aggiornare la stringa di connessione](#update-your-connection-string). 

* I valori di nome utente e password sono stati impostati usando la pagina della stringa di connessione nel portale di Azure. `path\to\cert` consente di specificare il percorso di un certificato X509. 

   ```javascript
   var ssl_option = {
        cert : fs.readFileSync("path\to\cert"),
        rejectUnauthorized : true,
        secureProtocol: 'TLSv1_2_method'
        };
   const authProviderLocalCassandra = new cassandra.auth.PlainTextAuthProvider(config.username, config.password);
   ```

* `client` viene inizializzato con le informazioni di contactPoint. Il valore di contactPoint viene recuperato dal portale di Azure.

    ```javascript
    const client = new cassandra.Client({contactPoints: [config.contactPoint], authProvider: authProviderLocalCassandra, sslOptions:ssl_option});
    ```

* `client` si connette all'API Cassandra di Azure Cosmos DB.

    ```javascript
    client.connect(next);
    ```

* Viene creato un nuovo keyspace.

    ```javascript
    function createKeyspace(next) {
        var query = "CREATE KEYSPACE IF NOT EXISTS uprofile WITH replication = {\'class\': \'NetworkTopologyStrategy\', \'datacenter1\' : \'1\' }";
        client.execute(query, next);
        console.log("created keyspace");    
  }
    ```

* Viene creata una nuova tabella.

   ```javascript
   function createTable(next) {
    var query = "CREATE TABLE IF NOT EXISTS uprofile.user (user_id int PRIMARY KEY, user_name text, user_bcity text)";
        client.execute(query, next);
        console.log("created table");
   },
   ```

* Le entità chiave/valore vengono inserite.

    ```javascript
    ...
       {
          query: 'INSERT INTO  uprofile.user  (user_id, user_name , user_bcity) VALUES (?,?,?)',
          params: [5, 'IvanaV', 'Belgaum', '2017-10-3136']
        }
    ];
    client.batch(queries, { prepare: true}, next);
    ```

* Eseguire una query per ottenere tutti i valori di chiave.

    ```javascript
   var query = 'SELECT * FROM uprofile.user';
    client.execute(query, { prepare: true}, function (err, result) {
      if (err) return next(err);
      result.rows.forEach(function(row) {
        console.log('Obtained row: %d | %s | %s ',row.user_id, row.user_name, row.user_bcity);
      }, this);
      next();
    });
    ```  
    
* Eseguire una query per ottenere un valore di chiave.

    ```javascript
    function selectById(next) {
        console.log("\Getting by id");
        var query = 'SELECT * FROM uprofile.user where user_id=1';
        client.execute(query, { prepare: true}, function (err, result) {
        if (err) return next(err);
            result.rows.forEach(function(row) {
            console.log('Obtained row: %d | %s | %s ',row.user_id, row.user_name, row.user_bcity);
        }, this);
        next();
        });
    }
    ```  

## <a name="update-your-connection-string"></a>Aggiornare la stringa di connessione

Tornare ora al portale di Azure per recuperare le informazioni sulla stringa di connessione e copiarle nell'app. La stringa di connessione consente all'app di comunicare con il database ospitato.

1. Nel [portale di Azure](https://portal.azure.com/) selezionare **Stringa di connessione**. 

    Usare il ![Pulsante Copia](./media/create-cassandra-nodejs/copy.png) pulsante sul lato destro della schermata per copiare il primo valore, PUNTO DI CONTATTO.

    ![Visualizzare e copiare i valori di PUNTO DI CONTATTO, NOME UTENTE e PASSWORD dalla pagina della stringa di connessione del portale di Azure](./media/create-cassandra-nodejs/keys.png)

2. Aprire il file `config.js` . 

3. Incollare il valore di PUNTO DI CONTATTO dal portale su `<FillMEIN>` nella riga 4.

    La riga 4 è ora simile alla seguente: 

    `config.contactPoint = "cosmos-db-quickstarts.cassandra.cosmosdb.azure.com:10350"`

4. Copiare il valore di NOME UTENTE dal portale e incollarlo su `<FillMEIN>` nella riga 2.

    La riga 2 è ora simile alla seguente: 

    `config.username = 'cosmos-db-quickstart';`
    
5. Copiare il valore di PASSWORD dal portale e incollarlo su `<FillMEIN>` nella riga 3.

    La riga 3 è ora simile alla seguente:

    `config.password = '2Ggkr662ifxz2Mg==';`

6. Salvare il file.`config.js`
    
## <a name="use-the-x509-certificate"></a>Usare il certificato X509

1. Scaricare il certificato Baltimore CyberTrust Root in locale da [https://cacert.omniroot.com/bc2025.crt](https://cacert.omniroot.com/bc2025.crt). Rinominare il file usando l'estensione file `.cer`.

   Il certificato ha il numero di serie `02:00:00:b9` e l'impronta digitale SHA1 `d4🇩🇪20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`.

2. Aprire `uprofile.js` e cambiare `path\to\cert` in modo che punti al nuovo certificato.

3. Salvare `uprofile.js`.

## <a name="run-the-nodejs-app"></a>Eseguire l'app Node.js

1. Nella finestra del terminale Git eseguire `npm install` per installare i moduli npm necessari.

2. Eseguire `node uprofile.js` per avviare l'applicazione Node.js.

3. Verificare i risultati previsti dalla riga di comando.

    ![Visualizzare e verificare l'output](./media/create-cassandra-nodejs/output.png)

    Premere CTRL+C per interrompere l'esecuzione del programma e chiudere la finestra della console. 

4. Nel portale di Azure aprire **Esplora dati** per modificare e usare questi nuovi dati, nonché eseguire query su di essi. 

    ![Visualizzare i dati in Esplora dati](./media/create-cassandra-nodejs/data-explorer.png) 

## <a name="review-slas-in-the-azure-portal"></a>Esaminare i contratti di servizio nel portale di Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Pulire le risorse

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a>Passaggi successivi

In questa guida introduttiva si è appreso come creare un account Azure Cosmos DB, come creare un contenitore con Esplora dati e come eseguire un'app. È ora possibile importare dati aggiuntivi nell'account Cosmos DB. 

> [!div class="nextstepaction"]
> [Importare i dati di Cassandra in Azure Cosmos DB](cassandra-import-data.md)


