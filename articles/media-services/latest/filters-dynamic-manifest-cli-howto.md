---
title: Uso dell'interfaccia della riga di comando per la creazione di filtri con Servizi multimediali di Azure | Microsoft Docs
description: In questo argomento illustra come usare l'interfaccia della riga di comando per creare filtri con Servizi multimediali.
services: media-services
documentationcenter: ''
author: juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/26/2018
ms.author: juliako
ms.custom: seodec18
ms.openlocfilehash: 2ba3de32f4ec3b9f6faf1d5a51da9c1c91e4a2e4
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60732434"
---
# <a name="creating-filters-with-cli"></a>Creazione di filtri con l'interfaccia della riga di comando 

Quando si distribuiscono contenuti ai clienti (flusso di eventi dal vivo o di video on demand), il client potrebbe avere bisogno di una maggiore flessibilità rispetto a quanto descritto nel file manifesto dell'asset predefinito. Servizi multimediali di Azure consente di definire i filtri account e i filtri asset per i propri contenuti. Per altre informazioni, vedere [Filtri e manifesti dinamici](filters-dynamic-manifest-overview.md).

Questo argomento illustra come configurare un filtro per un asset Video on demand e usare l'interfaccia della riga di comando per Servizi multimediali v3 per creare [filtri account](https://docs.microsoft.com/cli/azure/ams/account-filter?view=azure-cli-latest) e [filtri asset](https://docs.microsoft.com/cli/azure/ams/asset-filter?view=azure-cli-latest). 

## <a name="prerequisites"></a>Prerequisiti 

- [Creare un account di Servizi multimediali di Azure](create-account-cli-how-to.md). Assicurarsi di ricordare il nome del gruppo di risorse e il nome dell'account di Servizi multimediali. 
- Leggere [Filtri e manifesti dinamici](filters-dynamic-manifest-overview.md).

[!INCLUDE [media-services-cli-instructions](../../../includes/media-services-cli-instructions.md)]

## <a name="define-a-filter"></a>Definire un filtro 

Di seguito è riportato l'esempio che definisce le condizioni di selezione di traccia che vengono aggiunte al manifesto finale. Questo filtro include tracce audio EC-3 e tracce video con velocità in bit nell'intervallo 0-1000000.

I filtri definiti in REST includono l'oggetto JSON wrapper "Properties".  

```json
[
    {
        "trackSelections": [
            {
                "property": "Type",
                "value": "Audio",
                "operation": "Equal"
            },
            {
                "property": "FourCC",
                "value": "EC-3",
                "operation": "NotEqual"
            }
        ]
    },
    {
        "trackSelections": [
            {
                "property": "Type",
                "value": "Video",
                "operation": "Equal"
            },
            {
                "property": "Bitrate",
                "value": "0-1000000",
                "operation": "Equal"
            }
        ]
    }
]
```

## <a name="create-account-filters"></a>Creare filtri account

Il comando [az ams account-filter](https://docs.microsoft.com/cli/azure/ams/account-filter?view=azure-cli-latest) seguente crea un filtro account con le selezioni di traccia del filtro [definite in precedenza](#define-a-filter). 

Questo comando consente di superare il parametro `--tracks` facoltativo che include JSON per le selezioni di traccia.  Usare @{file} per caricare JSON da un file. Se si usa l’interfaccia della riga di comando di Azure in locale, specificare il percorso completo del file:

```azurecli
az ams account-filter create -a amsAccount -g resourceGroup -n filterName --tracks @tracks.json
```

Vedere anche [Esempi JSON per i filtri](https://docs.microsoft.com/rest/api/media/accountfilters/createorupdate#create_an_account_filter).

## <a name="create-asset-filters"></a>Creare filtri asset

Il comando [az ams asset-filter](https://docs.microsoft.com/cli/azure/ams/asset-filter?view=azure-cli-latest) seguente crea un filtro asset con le selezioni di traccia del filtro [definite in precedenza](#define-a-filter). 

```azurecli
az ams asset-filter create -a amsAccount -g resourceGroup -n filterName --asset-name assetName --tracks @tracks.json
```

Vedere anche [Esempi JSON per i filtri](https://docs.microsoft.com/rest/api/media/assetfilters/createorupdate#create_an_asset_filter).

## <a name="next-step"></a>Passaggio successivo

[Video in streaming](stream-files-tutorial-with-api.md) 

## <a name="see-also"></a>Vedere anche 

[Interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/ams?view=azure-cli-latest)
