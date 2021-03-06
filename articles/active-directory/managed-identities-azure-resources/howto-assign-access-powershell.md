---
title: Asignación de un acceso de identidad administrada a un recurso de Azure mediante PowerShell
description: Instrucciones paso a paso para asignar una identidad administrada en un recurso y acceso a otro recurso, mediante PowerShell.
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: daveba
editor: ''
ms.service: active-directory
ms.subservice: msi
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/06/2018
ms.author: priyamo
ms.collection: M365-identity-device-management
ms.openlocfilehash: fc910ad51984204c8fc072ce49ebdfe4695be4a0
ms.sourcegitcommit: f715dcc29873aeae40110a1803294a122dfb4c6a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56268023"
---
# <a name="assign-a-managed-identity-access-to-a-resource-using-powershell"></a>Asignación de un acceso de identidad administrada a un recurso mediante PowerShell

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

Una vez que haya configurado un recurso de Azure con una identidad administrada, puede dar acceso de identidad administrada a otro recurso, al igual que cualquier entidad de seguridad. En este ejemplo se muestra cómo otorgar acceso de identidad administrada a una máquina virtual de Azure para una cuenta de almacenamiento de Azure, mediante PowerShell.

[!INCLUDE [az-powershell-update](../../../includes/updated-for-az.md)]

## <a name="prerequisites"></a>Requisitos previos

- Si no está familiarizado con las identidades administradas de los recursos de Azure, consulte la [sección de introducción](overview.md). **No olvide revisar la [diferencia entre una identidad administrada asignada por el sistema y una identidad administrada asignada por el usuario](overview.md#how-does-it-work)**.
- Si aún no tiene una cuenta de Azure, [regístrese para una cuenta gratuita](https://azure.microsoft.com/free/) antes de continuar.
- Instale [la versión más reciente de Azure PowerShell](/powershell/azure/install-az-ps) si aún no lo ha hecho.

## <a name="use-rbac-to-assign-a-managed-identity-access-to-another-resource"></a>Uso de RBAC para asignar el acceso de una identidad administrada a otro recurso

Después de habilitar la identidad administrada en un recurso de Azure, [como una máquina virtual de Azure](qs-configure-powershell-windows-vm.md):

1. Inicie sesión en Azure mediante el cmdlet `Connect-AzAccount`. Use una cuenta asociada a la suscripción de Azure en la que haya configurado la identidad administrada:

   ```powershell
   Connect-AzAccount
   ```
2. En este ejemplo, vamos a dar a una máquina virtual de Azure acceso a una cuenta de almacenamiento. En primer lugar, se usa [Get-AzVM](/powershell/module/az.compute/get-azvm) para obtener la entidad de servicio para la máquina virtual denominada `myVM`, que se creó cuando se habilitó la identidad administrada. A continuación, usamos [New-AzRoleAssignment](/powershell/module/Az.Resources/New-AzRoleAssignment) para conceder a la máquina virtual acceso de **lectura** a una cuenta de almacenamiento denominada `myStorageAcct`:

    ```powershell
    $spID = (Get-AzVM -ResourceGroupName myRG -Name myVM).identity.principalid
    New-AzRoleAssignment -ObjectId $spID -RoleDefinitionName "Reader" -Scope "/subscriptions/<mySubscriptionID>/resourceGroups/<myResourceGroup>/providers/Microsoft.Storage/storageAccounts/<myStorageAcct>"
    ```

## <a name="next-steps"></a>Pasos siguientes

- [Identidades administradas de recursos de Azure](overview.md)
- Para habilitar la identidad administrada de una máquina virtual de Azure, consulte [Configuración de identidades administradas de recursos de Azure en una VM de Azure mediante PowerShell](qs-configure-powershell-windows-vm.md).
