---
title: File di inclusione
description: File di inclusione
services: virtual-machines
author: axayjo
ms.service: virtual-machines
ms.topic: include
ms.date: 04/30/2019
ms.author: akjosh; cynthn
ms.custom: include file
ms.openlocfilehash: 9647cdd584b53f581f46f728ca2d08f9a113ce92
ms.sourcegitcommit: 0568c7aefd67185fd8e1400aed84c5af4f1597f9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65199196"
---
## <a name="before-you-begin"></a>Prima di iniziare

Per completare l'esempio in questo articolo, è necessario disporre di un'immagine gestita esistente di una macchina virtuale generalizzata. Per altre informazioni, vedere [Esercitazione: Creare un'immagine personalizzata di una macchina virtuale di Azure con l'interfaccia della riga di comando di Azure versione 2.0](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-custom-images). Se l'immagine gestita contiene un disco dati, le dimensioni del disco dati non possono essere più di 1 TB.

## <a name="launch-azure-cloud-shell"></a>Avviare Azure Cloud Shell

Azure Cloud Shell è una shell interattiva gratuita che può essere usata per eseguire la procedura di questo articolo. Include strumenti comuni di Azure preinstallati e configurati per l'uso con l'account. 

Per aprire Cloud Shell, basta selezionare **Prova** nell'angolo superiore destro di un blocco di codice. È anche possibile avviare Cloud Shell in una scheda separata del browser visitando [https://shell.azure.com/bash](https://shell.azure.com/bash). Selezionare **Copia** per copiare i blocchi di codice, incollarli in Cloud Shell e premere INVIO per eseguirli.

## <a name="create-an-image-gallery"></a>Creare un raccolta di immagini 

Una raccolta di immagini è la risorsa principale usata per l'abilitazione della condivisione di immagini. I caratteri consentiti per i nomi delle raccolte sono lettere maiuscole o minuscole, numeri e punti. Il nome della raccolta non può contenere trattini.   I nomi di raccolta devono essere univoci all'interno della sottoscrizione. 

Creare una raccolta di immagini usando [sig az create](/cli/azure/sig#az-sig-create). L'esempio seguente crea una raccolta denominata *myGallery* nelle *myGalleryRG*.

```azurecli-interactive
az group create --name myGalleryRG --location WestCentralUS
az sig create -g myGalleryRG --gallery-name myGallery
```

## <a name="create-an-image-definition"></a>Creare una definizione dell'immagine

Le definizioni di immagini crea un raggruppamento logico per le immagini. Vengono utilizzati per gestire le informazioni sulle versioni di immagini che vengono creati in esse contenute. I nomi definizione di immagine possono essere costituiti da periodi, cifre, punti, trattini e lettere maiuscole o minuscole. Per altre informazioni sui valori è possibile specificare per una definizione dell'immagine, vedere [le definizioni di immagine](https://docs.microsoft.com/azure/virtual-machines/linux/shared-image-galleries#image-definitions).

Creare una definizione dell'immagine iniziale nella raccolta usando [az sig image-definition create](/cli/azure/sig/image-definition#az-sig-image-definition-create).

```azurecli-interactive 
az sig image-definition create \
   -g myGalleryRG \
   --gallery-name myGallery \
   --gallery-image-definition myImageDefinition \
   --publisher myPublisher \
   --offer myOffer \
   --sku 16.04-LTS \
   --os-type Linux 
```


## <a name="create-an-image-version"></a>Creare una versione di immagine 

Creare versioni dell'immagine in base alle esigenze usando [az image gallery create-image-version](/cli/azure/sig/image-version#az-sig-image-version-create). È necessario passare l'ID dell'immagine gestita da usare come baseline per creare la versione dell'immagine. È possibile usare [elenco di immagini di az](/cli/azure/image?view#az-image-list) per ottenere informazioni sulle immagini in un gruppo di risorse. 

I caratteri consentiti per le versioni delle immagini sono numeri e punti. I numeri devono essere compresi nell'intervallo di un valore Integer a 32 bit. Formato: *MajorVersion*.*MinorVersion*.*Patch*.

In questo esempio è la versione dell'immagine del nostro *1.0.0* e andremo a creare 2 repliche nel *East US* area, 1 replica nel *South Central US* 1 e area replica all'interno di *Stati Uniti orientali 2* area.


```azurecli-interactive 
az sig image-version create \
   -g myGalleryRG \
   --gallery-name myGallery \
   --gallery-image-definition myImageDefinition \
   --gallery-image-version 1.0.0 \
   --target-regions "WestCentralUS" "SouthCentralUS=1" "EastUS2=1" \
   --replica-count 2 \
   --managed-image "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/images/myImage"
```

> [!NOTE]
> È necessario attendere che la versione dell'immagine terminare completamente corso di compilazione e replicati prima di poter usare la stessa immagine gestita per creare un'altra versione dell'immagine.
>
> È anche possibile archiviare la versione dell'immagine nel [archiviazione con ridondanza della zona](https://docs.microsoft.com/azure/storage/common/storage-redundancy-zrs) aggiungendo `--storage-account-type standard_zrs` quando si crea la versione dell'immagine.
>
