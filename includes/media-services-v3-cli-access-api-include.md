---
title: File di inclusione
description: File di inclusione
services: media-services
author: WenJason
ms.service: media-services
ms.topic: include
origin.date: 05/29/2018
ms.date: 06/25/2018
ms.author: v-nany
ms.custom: include file
ms.openlocfilehash: 4dde0a47f0452da2dd951df86ccb6e02a44521ed
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60309082"
---
## <a name="access-the-media-services-api"></a>Accedere all'API di Servizi multimediali

Per connettersi alle API di Servizi multimediali di Azure, si usa l'autenticazione dell'entità servizio di Azure AD. Il comando seguente consente di creare un'applicazione Azure AD e di collegare un'entità servizio all'account. È consigliabile usare i valori restituiti per configurare l'applicazione.

Prima di eseguire lo script, è possibile sostituire `amsaccount` e `amsResourceGroup` con i nomi scelti durante la creazione di queste risorse. `amsaccount` è il nome dell'account di Servizi multimediali di Azure al quale collegare l'entità servizio.

Il comando seguente restituisce un output `json`:

```cli
az ams account sp create --account-name amsaccount --resource-group amsResourceGroup
```

Con questo comando viene generata una risposta simile alla seguente:

```json
{
  "AadClientId": "00000000-4cdd-418a-8a72-0755ace03de5",
  "AadEndpoint": "https://login.partner.microsoftonline.cn",
  "AadSecret": "00000000-02f5-4bf2-9057-1c4f7baff155",
  "AadTenantId": "00000000-86f1-41af-91ab-2d7cd011db47",
  "AccountName": "amsaccount22",
  "ArmAadAudience": "https://management.core.chinacloudapi.cn/",
  "ArmEndpoint": "https://management.chinacloudapi.cn/",
  "Region": "chinaeast",
  "ResourceGroup": "amsResourceGroup2",
  "SubscriptionId": "00000000-6753-4ca2-b1ae-193798e2c9d8"
}
```

Se si vuole ottenere un output `xml` nella risposta, usare il comando seguente:

```cli
az ams account sp create --account-name amsaccount --resource-group amsResourceGroup --xml
```
