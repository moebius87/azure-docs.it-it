---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Calcolare le dimensioni del contenitore BLOB | Microsoft Docs
description: Calcolare le dimensioni di un contenitore dell'Archiviazione BLOB di Azure sommando le dimensioni dei BLOB del contenitore.
services: storage
documentationcenter: na
author: tamram
manager: timlt
editor: tysonn
ms.assetid: ''
ms.custom: mvc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: sample
ms.date: 06/28/2017
ms.author: tamram
ms.openlocfilehash: 3cb1e35617a58fcde7968ab45d437d865c91f983
ms.sourcegitcommit: a65b424bdfa019a42f36f1ce7eee9844e493f293
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/04/2019
ms.locfileid: "55696933"
---
# <a name="calculate-the-size-of-a-blob-storage-container"></a>Calcolare le dimensioni di un contenitore di archiviazione BLOB

Lo script consente di calcolare le dimensioni di un contenitore dell'Archiviazione BLOB di Azure sommando le dimensioni dei BLOB del contenitore.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

> [!IMPORTANT]
> Questo script dell'interfaccia della riga di comando offre una dimensione stimata per il contenitore e non deve essere usato per calcoli di fatturazione.

## <a name="sample-script"></a>Script di esempio

[!code-azurecli[main](../../../cli_scripts/storage/calculate-container-size/calculate-container-size.sh?highlight=2-3 "Calculate container size")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Eseguire il comando seguente per rimuovere il gruppo di risorse, il contenitore e tutte le risorse correlate.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Spiegazione dello script

Lo script usa i comandi seguenti per calcolare le dimensioni del contenitore dell'archiviazione BLOB. Ogni elemento della tabella include collegamenti alla documentazione specifica del comando.

| Comando | Note |
|---|---|
| [az group create](/cli/azure/group) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az storage blob upload](/cli/azure/storage/account) | Carica file locali in un contenitore dell'Archiviazione BLOB di Azure. |
| [az storage blob list](/cli/azure/storage/account/keys) | Elenca i BLOB in un contenitore dell'Archiviazione BLOB di Azure. |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](/cli/azure).

Altri esempi di script dell'interfaccia della riga di comando sono disponibili in [Azure CLI samples for Azure Blob storage](../blobs/storage-samples-blobs-cli.md) (Esempi dell'interfaccia della riga di comando di Azure per l'Archiviazione BLOB di Azure).
