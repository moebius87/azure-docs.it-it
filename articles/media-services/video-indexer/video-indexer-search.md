---
title: Trovare momenti esatti nei video - Video Indexer
titlesuffix: Azure Media Services
description: Questo argomento illustra come trovare momenti esatti nei video con Video Indexer.
services: media-services
author: Juliako
manager: femila
ms.service: media-services
ms.topic: article
ms.date: 02/25/2019
ms.author: juliako
ms.openlocfilehash: 07b3c806dc5df5f93bee3206cbca53485675e7dd
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60560356"
---
# <a name="find-exact-moments-within-videos"></a>Trovare momenti esatti nei video

Questo argomento illustra le opzioni di ricerca disponibili per trovare momenti esatti nei video.

1. Passare al sito Web di [Video Indexer](https://www.videoindexer.ai/) ed eseguire l'accesso.
2. Eseguire una ricerca tra tutti i video nel proprio account.

    Nell'esempio seguente, vengono cercati tutti i video che comunicano con i fondamenti della protezione e in cui compare Satya,

    ![Ricerca](./media/video-indexer-search/video-indexer-search01.png)
3. Cercare le informazioni dettagliate riepilogate del video.

    È poi possibile eseguire ricerche all'interno di un video facendo clic su **Riproduci** sul video. Si può quindi cercare all'interno del video selezionando la scheda **Ricerca**. 

    Nell'esempio riportato di seguito è cercare "sicuro" all'interno del video selezionato.

    ![Ricerca](./media/video-indexer-search/video-indexer-search02.png)

    Se si fa clic su uno dei risultati, il lettore si posiziona in quel momento nel video. È possibile implementare la visualizzazione e la sincronizzazione del lettore e delle informazioni dettagliate nella propria applicazione. Per altre informazioni, vedere [Incorporare i widget di Video Indexer nelle applicazioni](video-indexer-embed-widgets.md). 
4. Cercare la suddivisione dettagliata del video.
    
    Se si desidera creare il proprio clip basato sul video a cui è stato individuato, premere il **modifica** pulsante. Questa pagina illustra video insieme ai relativi insights come filtri. Per altre informazioni, vedere [Visualizzare e modificare le informazioni dettagliate di Video Indexer](video-indexer-view-edit.md). 

    È possibile cercare all'interno del video per mostrare solo le righe si è interessati e usano le informazioni dettagliate sul lato per filtrare le parti che si desidera visualizzare. Al termine, è possibile visualizzare in anteprima il ritaglio e premere **pubblica** per creare la nuova clip che viene visualizzato nella raccolta.
    
    Nell'esempio seguente viene cercato il testo "realtà mista". Sono stati anche applicati filtri aggiuntivi, come illustrato nello screenshot di seguito.
    
    ![Ricerca](./media/video-indexer-search/video-indexer-search03.png)

## <a name="next-steps"></a>Passaggi successivi 

Dopo aver individuato il video che si vuole usare, è possibile continuare a elaborarlo come descritto in uno degli argomenti seguenti: 

- [Creare informazioni dettagliate video da video esistenti](video-indexer-create-new.md)
- [Elaborare contenuti con l'API REST Video Indexer](video-indexer-use-apis.md)
- [Embed visual widgets in your application](video-indexer-embed-widgets.md) (Incorporare i widget visivi nell'applicazione)

## <a name="see-also"></a>Vedere anche 

[Panoramica di Video Indexer](video-indexer-overview.md)
