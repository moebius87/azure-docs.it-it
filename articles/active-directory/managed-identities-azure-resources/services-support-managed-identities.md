---
title: Servizi di Azure che supportano le identità gestite per le risorse di Azure
description: Elenco di servizi che supportano le identità gestite per le risorse di Azure e l'autenticazione di Azure AD
services: active-directory
author: MarkusVi
ms.author: priyamo
ms.date: 04/15/2019
ms.topic: conceptual
ms.service: active-directory
ms.subservice: msi
manager: markvi
ms.collection: M365-identity-device-management
ms.openlocfilehash: 79c3f8ae183c78b19f7f520f8154bf9484a1f795
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60289787"
---
# <a name="services-that-support-managed-identities-for-azure-resources"></a>Servizi che supportano le identità gestite per le risorse di Azure

Le identità gestite per le risorse di Azure offrono ai servizi di Azure un'identità gestita automaticamente in Azure Active Directory. Con un'identità gestita è possibile eseguire l'autenticazione a qualsiasi servizio che supporti l'autenticazione di Azure AD senza dover inserire le credenziali nel codice. È in corso l'integrazione dell'autenticazione di Azure AD e delle identità gestite per le risorse di Azure in Azure. Controllare spesso gli aggiornamenti.

> [!NOTE]
> Identità gestite per le risorse di Azure è il nuovo nome per il servizio precedentemente noto come identità del servizio gestita.

## <a name="azure-services-that-support-managed-identities-for-azure-resources"></a>Servizi di Azure che supportano le identità gestite per le risorse di Azure

I servizi di Azure seguenti supportano le identità gestite per le risorse di Azure:

### <a name="azure-virtual-machines"></a>Macchine virtuali di Azure

| Tipo di identità gestita | Disponibile a livello generale<br>Aree globali di Azure | Azure Government | Azure Germania | 21Vianet per Azure Cina |
| --- | --- | --- | --- | --- |
| Assegnata dal sistema | Disponibile | Anteprima | Anteprima | Anteprima | 
| Assegnata dall'utente | Anteprima | Anteprima | Anteprima | Anteprima |

Vedere l'elenco seguente per configurare l'identità gestita per le macchine virtuali di Azure (nelle aree in cui è disponibile):

- [Portale di Azure](qs-configure-portal-windows-vm.md)
- [PowerShell](qs-configure-powershell-windows-vm.md)
- [Interfaccia della riga di comando di Azure](qs-configure-cli-windows-vm.md)
- [Modelli di Gestione risorse di Azure](qs-configure-template-windows-vm.md)
- [REST](qs-configure-rest-vm.md)

### <a name="azure-virtual-machine-scale-sets"></a>Set di scalabilità delle macchine virtuali di Azure

|Tipo di identità gestita | Disponibile a livello generale<br>Aree globali di Azure | Azure Government | Azure Germania | 21Vianet per Azure Cina |
| --- | --- | --- | --- | --- |
| Assegnata dal sistema | Disponibile | Anteprima | Anteprima | Anteprima |
| Assegnata dall'utente | Anteprima | Anteprima | Anteprima | Anteprima |

Vedere l'elenco seguente per configurare l'identità gestita per il set di scalabilità di macchine virtuali di Azure (nelle aree in cui è disponibile):

- [Portale di Azure](qs-configure-portal-windows-vm.md)
- [PowerShell](qs-configure-powershell-windows-vm.md)
- [Interfaccia della riga di comando di Azure](qs-configure-cli-windows-vm.md)
- [Modelli di Gestione risorse di Azure](qs-configure-template-windows-vm.md)
- [REST](qs-configure-rest-vm.md)

### <a name="azure-app-service"></a>Servizio app di Azure

| Tipo di identità gestita | Disponibile a livello generale<br>Aree globali di Azure | Azure Government | Azure Germania | 21Vianet per Azure Cina |
| --- | --- | --- | --- | --- |
| Assegnata dal sistema | Disponibile | Disponibile | Disponibile | Disponibile |
| Assegnata dall'utente | Anteprima | Non disponibile | Non disponibile | Non disponibile |

Vedere l'elenco seguente per configurare l'identità gestita per il Servizio app di Azure (nelle aree in cui è disponibile):

- [Portale di Azure](/azure/app-service/overview-managed-identity#using-the-azure-portal)
- [Interfaccia della riga di comando di Azure](/azure/app-service/overview-managed-identity#using-the-azure-cli)
- [Azure PowerShell](/azure/app-service/overview-managed-identity#using-azure-powershell)
- [Modello di Azure Resource Manager](/azure/app-service/overview-managed-identity#using-an-azure-resource-manager-template)

### <a name="azure-blueprints"></a>Azure Blueprint

|Tipo di identità gestita | Disponibile a livello generale<br>Aree globali di Azure | Azure Government | Azure Germania | 21Vianet per Azure Cina |
| --- | --- | --- | --- | --- |
| Assegnata dal sistema | Anteprima | Non disponibile | Non disponibile | Non disponibile |
| Assegnata dall'utente | Anteprima | Non disponibile | Non disponibile | Non disponibile |

Vedere l'elenco seguente per usare un'identità gestita con [progetti Azure](../../governance/blueprints/overview.md):

- [Portale di Azure - assegnazione progetto](../../governance/blueprints/create-blueprint-portal.md#assign-a-blueprint)
- [API REST - assegnazione progetto](../../governance/blueprints/create-blueprint-rest-api.md#assign-a-blueprint)

### <a name="azure-functions"></a>Funzioni di Azure

Tipo di identità gestita |Disponibile a livello generale<br>Aree globali di Azure | Azure Government | Azure Germania | 21Vianet per Azure Cina |
| --- | --- | --- | --- | --- |
| Assegnata dal sistema | Disponibile | Disponibile | Disponibile | Disponibile |
| Assegnata dall'utente | Anteprima | Non disponibile | Non disponibile | Non disponibile |

Vedere l'elenco seguente per configurare l'identità gestita per Funzioni di Azure (nelle aree in cui è disponibile):

- [Portale di Azure](/azure/app-service/overview-managed-identity#using-the-azure-portal)
- [Interfaccia della riga di comando di Azure](/azure/app-service/overview-managed-identity#using-the-azure-cli)
- [Azure PowerShell](/azure/app-service/overview-managed-identity#using-azure-powershell)
- [Modello di Azure Resource Manager](/azure/app-service/overview-managed-identity#using-an-azure-resource-manager-template)

### <a name="azure-logic-apps"></a>App per la logica di Azure

Tipo di identità gestita | Disponibile a livello generale<br>Aree globali di Azure | Azure Government | Azure Germania | 21Vianet per Azure Cina |
| --- | --- | --- | --- | --- |
| Assegnata dal sistema | Anteprima | Anteprima | Non disponibile | Anteprima |
| Assegnata dall'utente | Non disponibile | Non disponibile | Non disponibile | Non disponibile |

Vedere l'elenco seguente per configurare l'identità gestita per le App per la logica di Azure (nelle aree in cui è disponibile):

- [Portale di Azure](/azure/logic-apps/create-managed-service-identity#azure-portal)
- [Modello di Azure Resource Manager](/azure/app-service/overview-managed-identity)

### <a name="azure-data-factory-v2"></a>Azure Data Factory V2

Tipo di identità gestita | Disponibile a livello generale<br>Aree globali di Azure | Azure Government | Azure Germania | 21Vianet per Azure Cina |
| --- | --- | --- | --- | --- |
| Assegnata dal sistema | Disponibile | Non disponibile | Non disponibile | Non disponibile |
| Assegnata dall'utente | Non disponibile | Non disponibile | Non disponibile | Non disponibile |

Vedere l'elenco seguente per configurare l'identità gestita per Azure Data Factory V2 (nelle aree in cui è disponibile):

- [Portale di Azure](~/articles/data-factory/data-factory-service-identity.md#generate-managed-identity)
- [PowerShell](~/articles/data-factory/data-factory-service-identity.md#generate-managed-identity-using-powershell)
- [REST](~/articles/data-factory/data-factory-service-identity.md#generate-managed-identity-using-rest-api)
- [SDK](~/articles/data-factory/data-factory-service-identity.md#generate-managed-identity-using-sdk)

### <a name="azure-api-management"></a>Gestione API di Azure

Tipo di identità gestita | Disponibile a livello generale<br>Aree globali di Azure | Azure Government | Azure Germania | 21Vianet per Azure Cina |
| --- | --- | --- | --- | --- |
| Assegnata dal sistema | Disponibile | Disponibile | Non disponibile | Non disponibile |
| Assegnata dall'utente | Non disponibile | Non disponibile | Non disponibile | Non disponibile |

Vedere l'elenco seguente per configurare l'identità gestita per Gestione API di Azure (nelle aree in cui è disponibile):

- [Modello di Azure Resource Manager](/azure/api-management/api-management-howto-use-managed-service-identity)

### <a name="azure-container-instances"></a>Istanze di Azure Container

Tipo di identità gestita | Disponibile a livello generale<br>Aree globali di Azure | Azure Government | Azure Germania | 21Vianet per Azure Cina |
| --- | --- | --- | --- | --- |
| Assegnata dal sistema | Linux: Anteprima<br>Windows: Non disponibile | Non disponibile | Non disponibile | Non disponibile |
| Assegnata dall'utente | Linux: Anteprima<br>Windows: Non disponibile | Non disponibile | Non disponibile | Non disponibile |

Vedere l'elenco seguente per configurare l'identità gestita per Istanze di Azure Container (nelle aree in cui è disponibile):

- [Interfaccia della riga di comando di Azure](~/articles/container-instances/container-instances-managed-identity.md)
- [Modello di Azure Resource Manager](~/articles/container-instances/container-instances-managed-identity.md#enable-managed-identity-using-resource-manager-template)
- [YAML](~/articles/container-instances/container-instances-managed-identity.md#enable-managed-identity-using-yaml-file)

## <a name="azure-services-that-support-azure-ad-authentication"></a>Servizi di Azure che supportano l'autenticazione di Azure AD

I servizi seguenti supportano l'autenticazione di Azure AD e sono stati testati con i servizi client che usano le identità gestite per le risorse di Azure.

### <a name="azure-resource-manager"></a>Azure Resource Manager

Vedere l'elenco seguente per configurare l'accesso ad Azure Resource Manager:

- [Assegnare l'accesso tramite il portale di Azure](howto-assign-access-portal.md)
- [Assegnare l'accesso tramite Powershell](howto-assign-access-powershell.md)
- [Assegnare l'accesso tramite comando di Azure](howto-assign-access-CLI.md)
- [Assegnare l'accesso tramite il modello di Azure Resource Manager](../../role-based-access-control/role-assignments-template.md)

| Cloud | ID risorsa | Stato |
|--------|------------|--------|
| Azure Global | `https://management.azure.com/`| Disponibile |
| Azure Government | `https://management.usgovcloudapi.net/` | Disponibile |
| Azure Germania | `https://management.microsoftazure.de/` | Disponibile |
| 21Vianet per Azure Cina | `https://management.chinacloudapi.cn` | Disponibile |

### <a name="azure-key-vault"></a>Azure Key Vault

| Cloud | ID risorsa | Stato |
|--------|------------|--------|
| Azure Global | `https://vault.azure.net`| Disponibile |
| Azure Government | `https://vault.usgovcloudapi.net` | Disponibile |
| Azure Germania |  `https://vault.microsoftazure.de` | Disponibile |
| 21Vianet per Azure Cina | `https://vault.azure.cn` | Disponibile |

### <a name="azure-data-lake"></a>Azure Data Lake 

| Cloud | ID risorsa | Stato |
|--------|------------|--------|
| Azure Global | `https://datalake.azure.net/` | Disponibile |
| Azure Government |  | Non disponibile |
| Azure Germania |   | Non disponibile |
| 21Vianet per Azure Cina |  | Non disponibile |

### <a name="azure-sql"></a>SQL di Azure 

| Cloud | ID risorsa | Stato |
|--------|------------|--------|
| Azure Global | `https://database.windows.net/` | Disponibile |
| Azure Government | `https://database.usgovcloudapi.net/` | Disponibile |
| Azure Germania | `https://database.cloudapi.de/` | Disponibile |
| 21Vianet per Azure Cina | `https://database.chinacloudapi.cn/` | Disponibile |

### <a name="azure-event-hubs"></a>Hub eventi di Azure

| Cloud | ID risorsa | Stato |
|--------|------------|--------|
| Azure Global | `https://eventhubs.azure.net` | Anteprima |
| Azure Government |  | Non disponibile |
| Azure Germania |   | Non disponibile |
| 21Vianet per Azure Cina |  | Non disponibile |

### <a name="azure-service-bus"></a>Bus di servizio di Azure

| Cloud | ID risorsa | Stato |
|--------|------------|--------|
| Azure Global | `https://servicebus.azure.net`  | Anteprima |
| Azure Government |  | Non disponibile |
| Azure Germania |   | Non disponibile |
| 21Vianet per Azure Cina |  | Non disponibile |

### <a name="azure-storage-blobs-and-queues"></a>Le code e BLOB di archiviazione di azure

| Cloud | ID risorsa | Stato |
|--------|------------|--------|
| Azure Global | `https://storage.azure.com/` | Disponibile |
| Azure Government | `https://storage.azure.com/` | Disponibile |
| Azure Germania | `https://storage.azure.com/` | Disponibile |
| 21Vianet per Azure Cina | `https://storage.azure.com/` | Disponibile |
