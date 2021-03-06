---
title: Come connettere le origini dati in Azure Data Catalog
description: Articolo sulle procedure di connessione alle origini dati individuate con il catalogo dati di Azure.
services: data-catalog
author: JasonWHowell
ms.author: jasonh
ms.assetid: 4e6b27a5-cf75-4012-b88c-333c1fe638e8
ms.service: data-catalog
ms.topic: conceptual
ms.date: 01/18/2018
ms.openlocfilehash: c64340491dba11870364610a6c2ff62e25c1328a
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "61001832"
---
# <a name="how-to-connect-to-data-sources"></a>Come connettersi a origini dati
## <a name="introduction"></a>Introduzione
**Microsoft Azure Data Catalog** è un servizio cloud completamente gestito che funge da sistema di registrazione e di individuazione per origini dati aziendali. In altre parole, il **Catalogo dati di Azure** consente agli utenti di individuare, comprendere e usare origini dati e aiuta le organizzazioni a ottenere maggior valore dai dati esistenti. Un aspetto fondamentale di questo scenario è l’utilizzo dei dati: una volta che un utente individua un'origine dati e ne comprende lo scopo, il passaggio successivo consiste nella connessione all'origine dati per utilizzarne i dati.

## <a name="data-source-locations"></a>Percorsi di origine dati
Durante la registrazione dell’origine dati, **Catalogo dati Azure** riceve i metadati relativi alla stessa origine dati. Tali metadati includono i dettagli del percorso dell'origine dati. I dettagli del percorso variano da origine dati a origine dati, ma conterranno sempre le informazioni necessarie per la connessione. Ad esempio, il percorso per una tabella di SQL Server include il nome del server, il nome del database, il nome dello schema e il nome della tabella, mentre il percorso per un report di SQL Server Reporting Services include il nome del server e il percorso del report. Gli altri tipi di origine dati disporranno di percorsi che riflettono la struttura e la funzionalità del sistema di origine.

## <a name="integrated-client-tools"></a>Strumenti client integrato
Il modo più semplice per connettersi a un'origine dati consiste nell'usare il menu "Apri in..." nel portale di **Azure Data Catalog**. Questo menu consente di visualizzare un elenco di opzioni per la connessione all’asset di dati selezionato.
Quando si utilizza la visualizzazione affiancata predefinita, questo menu è disponibile in ogni sezione.

 ![Apertura di una tabella di SQL Server in Excel dal riquadro asset di dati](./media/data-catalog-how-to-connect/data-catalog-how-to-connect1.png)

Quando si utilizza la visualizzazione elenco, il menu è disponibile nella barra di ricerca nella parte superiore della finestra del portale.

 ![Apertura di un report di SQL Server Reporting Services in Gestione Report dalla barra di ricerca](./media/data-catalog-how-to-connect/data-catalog-how-to-connect2.png)

## <a name="supported-client-applications"></a>Applicazioni client supportate
Quando si usa il menu "Apri in...." per le origini dati nel portale di Azure Data Catalog, è necessario che nel computer client sia installata l'applicazione client corretta.

| Apri in applicazione | Estensione file/protocollo | Versioni applicazione supportate |
| --- | --- | --- |
| Excel |odc |Excel 2010 o versioni successive |
| Excel (prime 1000) |odc |Excel 2010 o versioni successive |
| Power Query |xlsx |Excel 2016, Excel 2010 o Excel 2013 con componente aggiuntivo Power Query per Excel installato |
| Power BI Desktop |pbix |Power BI Desktop luglio 2016 o versioni successive |
| SQL Server Data Tools |vsweb:// |Visual Studio 2013 Update 4 o versioni successive con strumenti di SQL Server installati |
| Gestione report |http:// |Vedere i [requisiti del browser per SQL Server Reporting Services](https://technet.microsoft.com/library/ms156511.aspx) |

## <a name="your-data-your-tools"></a>Dati e strumenti
Le opzioni disponibili nel menu dipendono dal tipo di asset di dati selezionato. Naturalmente, non tutti gli strumenti possibili saranno inclusi nel menu "Apri in....", ma è comunque semplice connettersi all'origine dati tramite qualsiasi strumento client. Quando viene selezionato un asset di dati nel portale **Azure Data Catalog**, il percorso completo viene visualizzato nel riquadro proprietà.

 ![Informazioni sulla connessione per una tabella SQL Server](./media/data-catalog-how-to-connect/data-catalog-how-to-connect3.png)

Le informazioni di connessione saranno diverse per ogni tipo di origine dati, ma le informazioni incluse nel portale forniranno tutto il necessario per connettersi all'origine dati in qualsiasi strumento client. Gli utenti possono copiare i dettagli della connessione per le origini dati che si sono individuate utilizzando **Catalogo dati Azure**, in modo da poter lavorare con i dati nello strumento scelto.

## <a name="connecting-and-data-source-permissions"></a>Autorizzazioni dell'origine dati e di connessione
Sebbene il **Catalogo dei dati di Azure** rende le origini dati individuabili, l’accesso ai dati stessi rimane sotto il controllo del proprietario dell'origine dati o dell’amministratore. L’individuazione di un'origine dati nel **Catalogo dati Azure** non fornisce agli utenti alcuna autorizzazione per accedere all'origine dati.

Per rendere il tutto più semplice per gli utenti che individuano un'origine dati ma che non dispongono dell'autorizzazione per accedervi, gli utenti possono fornire informazioni nella proprietà Richiesta di accesso durante l'annotazione di un'origine dati. Le informazioni riportate di seguito, inclusi i collegamenti al processo o al punto di contatto per ottenere l'accesso all'origine dati, vengono presentate nel portale con le informazioni sul percorso di origine dati.

 ![Informazioni sulla connessione con istruzioni fornite per la richiesta di accesso](./media/data-catalog-how-to-connect/data-catalog-how-to-connect4.png)

## <a name="summary"></a>Riepilogo
La registrazione di un'origine dati con il **Azure Data Catalog** rende più semplice individuare e comprendere l'origine dati, copiando i metadati strutturali e descrittivi dall'origine dati nel servizio Catalogo. Una volta che un'origine dati è stata registrata e individuata, gli utenti possono connettersi all'origine dati dal menu "Apri in..." del portale **Azure Data Catalog** o usando gli strumenti dati preferiti.

## <a name="see-also"></a>Vedere anche 
* [Introduzione ad Azure Data Catalog](data-catalog-get-started.md) .
