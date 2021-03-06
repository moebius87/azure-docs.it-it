---
title: Copiare dati da Azure Data Lake Storage Gen1 in Gen2 con Azure Data Factory
description: Usare Azure Data Factory per copiare dati da Azure Data Lake Storage Gen1 in Gen2
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.topic: conceptual
ms.date: 02/15/2019
ms.author: jingwang
ms.openlocfilehash: e3a27ab15c72289dd28e31d832b81407a66dc754
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60546275"
---
# <a name="copy-data-from-azure-data-lake-storage-gen1-to-gen2-with-azure-data-factory"></a>Copiare dati da Azure Data Lake Storage Gen1 in Gen2 con Azure Data Factory

Azure Data Lake Storage Gen2 è un set di funzionalità dedicate all'analisi dei Big Data e integrate in [Archiviazione BLOB di Azure](../storage/blobs/storage-blobs-introduction.md). Consente di interagire con i dati approfittando dei paradigmi sia del file system che dell'archiviazione di oggetti.

Se attualmente si usa Azure Data Lake Storage Gen1, è possibile valutare la nuova funzionalità Gen2 copiando i dati da Data Lake Storage Gen1 a Gen2 usando Azure Data Factory.

Azure Data Factory è un servizio di integrazione dei dati completamente gestito e basato sul cloud. È possibile usare il servizio per popolare il lake con i dati provenienti da un set completo di archivi dati locali e basati sul cloud e risparmiare tempo durante la compilazione di soluzioni di analisi. Per un elenco dettagliato di connettori supportati, vedere la tabella degli [archivi dati supportati](copy-activity-overview.md#supported-data-stores-and-formats).

Azure Data Factory offre una soluzione di spostamento dei dati gestita e scale-out. ADF, grazie all'architettura scale-out, può inserire i dati a una velocità effettiva elevata. Per informazioni, vedere [Prestazioni dell'attività di copia](copy-activity-performance.md).

Questo articolo illustra come usare lo strumento Copia dati di Data Factory per copiare dati da _Azure Data Lake Storage Gen1_ in _Azure Data Lake Storage Gen2_. È possibile seguire una procedura simile a quella usata per copiare dati da altri tipi di archivi dati.

## <a name="prerequisites"></a>Prerequisiti

* Sottoscrizione di Azure: Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/) prima di iniziare.
* Account Data Lake Storage Gen1 contenente dati.
* Account di Archiviazione di Azure con Data Lake Storage Gen2 abilitato: Se non hai un account di archiviazione [creare un account](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM).

## <a name="create-a-data-factory"></a>Creare una data factory

1. Nel menu a sinistra selezionare **Crea una risorsa** > **Dati e analisi** > **Data factory**:
   
   ![Selezione di Data Factory nel riquadro "Nuovo"](./media/quickstart-create-data-factory-portal/new-azure-data-factory-menu.png)

2. Nella pagina **Nuova data factory** specificare i valori per i campi mostrati nell'immagine seguente: 
      
   ![Pagina Nuova data factory](./media/load-azure-data-lake-storage-gen2-from-gen1/new-azure-data-factory.png)
 
    * **Nome**: immettere un nome univoco globale per la data factory di Azure. Se viene visualizzato l'errore "Il nome \"LoadADLSDemo\" per la data factory non è disponibile", immettere un nome diverso per la data factory. Ad esempio, è possibile usare il nome _**nomeutente**_**ADFTutorialDataFactory**. Riprovare a creare la data factory. Per informazioni sulle regole di denominazione per gli elementi di Data Factory, vedere [Azure Data Factory - Regole di denominazione](naming-rules.md).
    * **Sottoscrizione** selezionare la sottoscrizione di Azure in cui creare la data factory. 
    * **Gruppo di risorse**: selezionare un gruppo di risorse esistente nell'elenco a discesa oppure selezionare l'opzione **Crea nuovo** e immettere il nome di un gruppo di risorse. Per informazioni sui gruppi di risorse, vedere l'articolo relativo all'[uso di gruppi di risorse per la gestione delle risorse di Azure](../azure-resource-manager/resource-group-overview.md).  
    * **Versione**: selezionare **V2**.
    * **Località**: Selezionare la località per la data factory. Nell'elenco a discesa vengono mostrate solo le località supportate. Gli archivi dati usati dalla data factory possono trovarsi in altre località e aree. 

3. Selezionare **Create**.
4. Al termine della creazione, accedere alla data factory. Verrà visualizzata la home page **Data factory**, come mostrato nell'immagine seguente: 
   
   ![Home page di Data factory](./media/load-azure-data-lake-storage-gen2-from-gen1/data-factory-home-page.png)

   Selezionare il riquadro **Crea e monitora** per avviare l'applicazione Integrazione dati in una scheda separata.

## <a name="load-data-into-azure-data-lake-storage-gen2"></a>Caricare dati in Azure Data Lake Storage Gen2

1. Nella pagina **Attività iniziali** selezionare il riquadro **Copia dati** per avviare lo strumento Copia dati: 

   ![Riquadro dello strumento Copia dati](./media/load-azure-data-lake-storage-gen2-from-gen1/copy-data-tool-tile.png)
2. Nella pagina **Proprietà** specificare **CopyFromADLSGen1ToGen2** per il campo **Nome attività**, quindi selezionare **Avanti**:

    ![Pagina Proprietà](./media/load-azure-data-lake-storage-gen2-from-gen1/copy-data-tool-properties-page.png)
3. Nella pagina **Archivio dati di origine** fare clic su **+ Crea nuova connessione**:

    ![Pagina Archivio dati di origine](./media/load-azure-data-lake-storage-gen2-from-gen1/source-data-store-page.png)
    
    Selezionare **Azure Data Lake Storage Gen1** dalla raccolta di connettori e selezionare **Continua**
    
    ![Pagina Archivio dati di origine per Azure Data Lake Storage Gen1](./media/load-azure-data-lake-storage-gen2-from-gen1/source-data-store-page-adls-gen1.png)
    
4. Nella pagina delle **connessioni per Azure Data Lake Storage Gen1** seguire questa procedura:
   1. Selezionare la propria istanza di Data Lake Storage Gen1 per il nome dell'account e specificare o convalidare il **Tenant**.
   2. Fare clic su **Connessione di test** per convalidare le impostazioni, quindi selezionare **Fine**.
   3. Si noterà che viene creata una nuova connessione. Selezionare **Avanti**.
   
   > [!IMPORTANT]
   > In questa procedura dettagliata si usa un'identità gestita per le risorse di Azure per autenticare l'istanza di Data Lake Storage Gen1. Assicurarsi di concedere le autorizzazioni appropriate all'entità del servizio gestita in Azure Data Lake Storage Gen1 seguendo [queste istruzioni](connector-azure-data-lake-store.md#managed-identity).
   
   ![Specificare un account di Azure Data Lake Storage Gen1](./media/load-azure-data-lake-storage-gen2-from-gen1/specify-adls-gen1-account.png)
      
5. Nella pagina **Choose the input file or folder** (Scegliere il file o la cartella di input) passare alla cartella e al file da copiare. Selezionare la cartella o il file e selezionare **Scegli**:

    ![Scegliere il file o la cartella di input](./media/load-azure-data-lake-storage-gen2-from-gen1/choose-input-folder.png)

6. Specificare il comportamento di copia selezionando le opzioni **Copia i file in modo ricorsivo** e **Copia binaria**. Selezionare **Avanti**:

    ![Specificare la cartella di output](./media/load-azure-data-lake-storage-gen2-from-gen1/specify-binary-copy.png)
    
7. Nella pagina **Archivio dati di destinazione** fare clic su **+ Crea nuova connessione**, quindi selezionare **Data Lake Storage Gen2** e **Continua**:

    ![Pagina dell'archivio dati di destinazione](./media/load-azure-data-lake-storage-gen2-from-gen1/destination-data-storage-page.png)

8. Nella pagina delle **connessioni per Azure Data Lake Storage Gen2** seguire questa procedura:

   1. Selezionare l'account con supporto di Data Lake Storage Gen2 nell'elenco a discesa "Nome account di archiviazione".
   2. Selezionare **Fine** per creare la connessione. Quindi selezionare **Avanti**.
   
   ![Specificare un account di Azure Data Lake Storage Gen2](./media/load-azure-data-lake-storage-gen2-from-gen1/specify-adls-gen2-account.png)

9. Nel **scegliere il file di output o la cartella** pagina, immettere **copyfromadlsgen1** come nome di cartella di output, selezionare **Avanti**. Azure Data factory creerà il sistema di file di Azure Data Lake Store Gen2 corrispondente e le sottocartelle durante la copia, se non esiste.

    ![Specificare la cartella di output](./media/load-azure-data-lake-storage-gen2-from-gen1/specify-adls-gen2-path.png)

10. Nella pagina **Impostazioni** selezionare **Avanti** per usare le impostazioni predefinite.

11. Nella pagina **Riepilogo** esaminare le impostazioni e quindi selezionare **Avanti**:

    ![Pagina Riepilogo](./media/load-azure-data-lake-storage-gen2-from-gen1/copy-summary.png)
12. Nella pagina **Distribuzione** selezionare **Monitoraggio** per monitorare la pipeline:

    ![Pagina Distribuzione](./media/load-azure-data-lake-storage-gen2-from-gen1/deployment-page.png)
13. Si noti che la scheda **Monitoraggio** a sinistra è selezionata automaticamente. La colonna **Azioni** contiene collegamenti per visualizzare i dettagli delle esecuzioni dell'attività ed eseguire di nuovo la pipeline:

    ![Monitorare le esecuzioni di pipeline](./media/load-azure-data-lake-storage-gen2-from-gen1/monitor-pipeline-runs.png)

14. Per visualizzare le esecuzioni di attività associate all'esecuzione della pipeline, selezionare il collegamento **View Activity Runs** (Visualizza le esecuzioni di attività) nella colonna **Azioni**. Dato che la pipeline contiene una sola attività (attività di copia), viene visualizzata una sola voce. Per tornare alla visualizzazione delle esecuzioni di pipeline, selezionare il collegamento **Pipeline** in alto. Selezionare **Aggiorna** per aggiornare l'elenco. 

    ![Monitorare le esecuzioni delle attività](./media/load-azure-data-lake-storage-gen2-from-gen1/monitor-activity-runs.png)

15. Per monitorare i dettagli di esecuzione per ogni attività di copia, selezionare il collegamento **Dettagli** (immagine degli occhiali) in **Azioni** nella visualizzazione di monitoraggio delle attività. È possibile monitorare dettagli come il volume dei dati copiati dall'origine al sink, la velocità effettiva dei dati, i passaggi di esecuzione con la durata corrispondente e le configurazioni usate:

    ![Monitorare i dettagli di esecuzione delle attività](./media/load-azure-data-lake-storage-gen2-from-gen1/monitor-activity-run-details.png)

16. Verificare che i dati vengano copiati nell'account Data Lake Storage Gen2.

## <a name="best-practices"></a>Procedure consigliate

Quando si copia un volume considerevole di dati dall'archivio dati basato su file, è consigliabile:

- Partizionare i file in set di file da 10 TB a 30 TB l'uno.
- Non attivare troppe esecuzioni di copia simultanee per evitare la limitazione dagli archivi di dati di origine o sink. È possibile iniziare con un'esecuzione di copia e monitorare la velocità effettiva, quindi aggiungerne gradualmente altre in base alle esigenze.

## <a name="next-steps"></a>Passaggi successivi

* [Panoramica dell'attività di copia](copy-activity-overview.md)
* [Connettore di Azure Data Lake Storage Gen2](connector-azure-data-lake-storage.md)
