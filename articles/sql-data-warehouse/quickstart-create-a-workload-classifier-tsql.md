---
title: 'Guida introduttiva: Creare un classificatore di carico di lavoro - T-SQL | Microsoft Docs'
description: Usare T-SQL per creare un classificatore di carico di lavoro con priorità alta
services: sql-data-warehouse
author: ronortloff
manager: craigg
ms.service: sql-data-warehouse
ms.topic: quickstart
ms.subservice: workload management
ms.date: 03/13/2019
ms.author: rortloff
ms.reviewer: jrasnick
ms.openlocfilehash: 198faf6791a4a2caa2cefee2181a13ed8185310e
ms.sourcegitcommit: fec96500757e55e7716892ddff9a187f61ae81f7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2019
ms.locfileid: "59617338"
---
# <a name="quickstart-create-a-workload-classifier-using-t-sql-preview"></a>Guida introduttiva: Creare un classificatore di carico di lavoro con T-SQL (anteprima)

In questa Guida introduttiva si creerà rapidamente un classificatore di carico di lavoro con priorità alta per il direttore generale dell'organizzazione. Il classificatore di carico di lavoro consentirà alle query del direttore generale di avere la precedenza su quelle con priorità inferiore nella coda.

> [!Note]
> La classificazione del carico di lavoro è disponibile in anteprima in SQL Data Warehouse Gen2. L'anteprima delle funzionalità di classificazione e priorità della gestione del carico di lavoro è disponibile per le build con data di rilascio 9 aprile 2019 o successiva.  Gli utenti dovrebbero evitare di usare le build precedenti a questa data per i test di gestione del carico di lavoro.  Per determinare se la build è in grado di gestire il carico di lavoro, eseguire select @@version quando si è connessi all'istanza di SQL Data Warehouse.

Se non si ha una sottoscrizione di Azure, creare un account [gratuito](https://azure.microsoft.com/free/) prima di iniziare.

> [!NOTE]
> La creazione di un'istanza di SQL Data Warehouse può dare luogo a un nuovo servizio fatturabile.  Per altre informazioni, vedere [SQL Data Warehouse Prezzi](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).
>
>

## <a name="prerequisites"></a>Prerequisiti

Questa guida introduttiva presuppone che l'utente abbia già un data warehouse SQL con autorizzazioni CONTROL DATABASE. Se è necessario crearne uno, fare riferimento a [Creare e connettere - portale](create-data-warehouse-portal.md) per creare un data warehouse denominato **mySampleDataWarehouse**.

## <a name="sign-in-to-the-azure-portal"></a>Accedere al portale di Azure

Accedere al [portale di Azure](https://portal.azure.com/).

## <a name="create-login-for-theceo"></a>Creare un accesso per IlCEO

Creare un account di accesso con autenticazione di SQL Server nel database `master` con l’istruzione [CREATE LOGIN](/sql/t-sql/statements/create-login-transact-sql) per “IlCEO”.

```sql
IF NOT EXISTS (SELECT * FROM sys.sql_logins WHERE name = 'TheCEO')
BEGIN
CREATE LOGIN [TheCEO] WITH PASSWORD='<strongpassword>'
END
;
```

## <a name="create-user"></a>Create user

[Creare l'utente](/sql/t-sql/statements/create-user-transact-sql?view=azure-sqldw-latest) "TheCEO" in mySampleDataWarehouse

```sql
IF NOT EXISTS (SELECT * FROM sys.database_principals WHERE name = 'THECEO')
BEGIN
CREATE USER [TheCEO] FOR LOGIN [TheCEO]
END
;
```

## <a name="create-a-workload-classifier"></a>Creare un classificatore del carico di lavoro

Creare un [classificatore di carico di lavoro](/sql/t-sql/statements/create-workload-classifier-transact-sql?view=azure-sqldw-latest) per "TheCEO" con priorità alta.

```sql
DROP WORKLOAD CLASSIFIER [wgcTheCEO];
CREATE WORKLOAD CLASSIFIER [wgcTheCEO]
WITH (WORKLOAD_GROUP = 'xlargerc'
      ,MEMBERNAME = 'TheCEO'
      ,IMPORTANCE = HIGH);
```

## <a name="view-existing-classifiers"></a>Visualizzare i classificatori esistenti

```sql
SELECT * FROM sys.workload_management_workload_classifiers
```

## <a name="clean-up-resources"></a>Pulire le risorse

```sql
DROP WORKLOAD CLASSIFIER [wgcTheCEO]
DROP USER [TheCEO]
;
```

Per le unità del data warehouse e i dati archiviati vengono addebitati costi. Le risorse di calcolo e archiviazione vengono fatturate separatamente.

- Se si vogliono mantenere i dati nelle risorse di archiviazione, è possibile sospendere il calcolo quando il data warehouse non è in uso. In questo modo, vengono addebitati solo i costi per l'archiviazione dei dati. Quando si è pronti a lavorare con i dati, riprendere il calcolo.
- Per evitare di ricevere addebiti in futuro, è possibile eliminare il data warehouse.

Seguire questa procedura per pulire le risorse.

1. Accedere al [portale di Azure](https://portal.azure.com) e selezionare il proprio data warehouse.

    ![Pulire le risorse](media/load-data-from-azure-blob-storage-using-polybase/clean-up-resources.png)

2. Per sospendere il calcolo, selezionare il pulsante **Pausa**. Quando si sospende il data warehouse, viene visualizzato il pulsante **Avvia**.  Per riprendere il calcolo, selezionare **Avvia**.

3. Per rimuovere il data warehouse in modo da non ricevere addebiti per operazioni di calcolo o archiviazione, selezionare **Elimina**.

4. Per rimuovere il server SQL creato, selezionare **mynewserver-20180430.database.windows.net** nell'immagine precedente e quindi selezionare **Elimina**.  Fare attenzione quando si esegue questa operazione perché l'eliminazione del server comporta anche quella di tutti i database assegnati al server.

5. Per rimuovere il gruppo di risorse, selezionare **myResourceGroup** e quindi **Elimina gruppo di risorse**.

## <a name="next-steps"></a>Passaggi successivi

È stato creato un classificatore di carico di lavoro. Eseguire alcune query come IlCEO per verificarne le prestazioni. Consultare [sys.dm_pdw_exec_requests](/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql) per visualizzare le query e la loro priorità.

Per ulteriori informazioni sulla gestione del carico di lavoro di SQL Data Warehouse, vedere [Priorità del carico di lavoro di SQL Data Warehouse](sql-data-warehouse-workload-importance.md) e [Classificazione del carico di lavoro di SQL Data Warehouse](sql-data-warehouse-workload-classification.md).
