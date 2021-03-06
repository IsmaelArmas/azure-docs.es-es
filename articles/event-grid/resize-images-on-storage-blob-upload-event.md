---
title: Usar Azure Event Grid para automatizar el cambio de tamaño de imágenes cargadas | Microsoft Docs
description: Azure Event Grid puede desencadenarse en cargas de blob de Azure Storage. Puede usarlo para enviar archivos de imagen cargados en Azure Storage a otros servicios, como Azure Functions, a fin de cambiar el tamaño y otras mejoras.
services: event-grid, functions
author: spelluru
manager: jpconnoc
editor: ''
ms.service: event-grid
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/29/2019
ms.author: spelluru
ms.custom: mvc
ms.openlocfilehash: b3ddaf7667baf98d9d5daa93a3106e457d0aeacb
ms.sourcegitcommit: 039263ff6271f318b471c4bf3dbc4b72659658ec
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/06/2019
ms.locfileid: "55756876"
---
# <a name="tutorial-automate-resizing-uploaded-images-using-event-grid"></a>Tutorial: Automatizar el cambio de tamaño de imágenes cargadas mediante Event Grid

[Azure Event Grid](overview.md) es un servicio de eventos para la nube. Event Grid permite crear suscripciones a eventos producidos por servicios de Azure o recursos de terceros.  

Este tutorial es la segunda parte de una serie de tutoriales sobre almacenamiento. Amplía el [tutorial anterior sobre almacenamiento][previous-tutorial] para agregar la generación de vistas en miniatura automática sin servidor con Azure Event Grid y Azure Functions. Event Grid permite que [Azure Functions](../azure-functions/functions-overview.md) responda a eventos de [Azure Blob Storage](../storage/blobs/storage-blobs-introduction.md) y genere vistas en miniatura de imágenes cargadas. Se crea una suscripción de eventos en el evento de creación de Blob Storage. Cuando se agrega un blob a un contenedor de Blob Storage determinado, se llama a un punto de conexión de función. Los datos pasados al enlace de función desde Event Grid se usan para acceder al blob y generar la imagen en miniatura.

Use la CLI de Azure y Azure Portal para agregar la funcionalidad de cambio de tamaño a una aplicación existente de carga de imágenes.

![Aplicación web publicada en el explorador Microsoft Edge](./media/resize-images-on-storage-blob-upload-event/tutorial-completed.png)

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear una cuenta general de Azure Storage
> * Implementar código sin servidor con Azure Functions
> * Crear una suscripción de eventos de Blob Storage en Event Grid

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial:

Debes haber completado el tutorial anterior sobre el almacenamiento de blobs: [Carga de datos de imagen en la nube con Azure Storage][previous-tutorial].

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

Si anteriormente no ha registrado el proveedor de recursos de Event Grid en su suscripción, asegúrese de que está registrado.

```azurepowershell-interactive
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.EventGrid
```

```azurecli-interactive
az provider register --namespace Microsoft.EventGrid
```

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si decide instalar y usar la CLI de forma local, en este tutorial se necesita la CLI de Azure versión 2.0.14 o posterior. Ejecute `az --version` para encontrar la versión. Si necesita instalarla o actualizarla, vea [Instalación de la CLI de Azure]( /cli/azure/install-azure-cli). 

Si no usa Cloud Shell, primero debe iniciar sesión con `az login`.

## <a name="create-an-azure-storage-account"></a>Creación de una cuenta de Azure Storage

Azure Functions necesita una cuenta de almacenamiento general. Cree una cuenta de almacenamiento general independiente en el grupo de recursos con el comando [az storage account create](/cli/azure/storage/account#az-storage-account-create).

Los nombres de las cuentas de almacenamiento deben tener entre 3 y 24 caracteres y solo pueden incluir números y letras en minúscula. 

En el siguiente comando, sustituya su propio nombre único global por la cuenta de almacenamiento general donde vea el marcador de posición `<general_storage_account>`. 

1. Establezca una variable para almacenar el nombre del grupo de recursos que creó en el tutorial anterior. 

    ```azurecli-interactive
    resourceGroupName=<Name of the resource group that you created in the previous tutorial>
    ```
2. Establezca una variable para el nombre de la cuenta de almacenamiento que requiere la función de Azure. 

    ```azurecli-interactive
    functionstorage=<name of the storage account to be used by function>
    ```
3. Cree la cuenta de almacenamiento para la función de Azure. Esto es diferente del almacenamiento que contiene las imágenes. 

    ```azurecli-interactive
    az storage account create --name $functionstorage --location eastus --resource-group $resourceGroupName --sku Standard_LRS --kind storage
    ```

## <a name="create-a-function-app"></a>Creación de una aplicación de función  

Debe tener una Function App para hospedar la ejecución de la función. La Function App proporciona un entorno para la ejecución sin servidor de su código de función. Cree una Function App con el comando [az functionapp create](/cli/azure/functionapp#az-functionapp-create). 

En el siguiente comando, sustituya su propio nombre único de Function App donde vea el marcador de posición `<function_app>`. El nombre de la aplicación de función se usa como dominio DNS predeterminado para la aplicación de función y, por ello, el nombre debe ser único en todas las aplicaciones de Azure. En `<general_storage_account>`, sustituya el nombre de la cuenta de almacenamiento general que ha creado.

1. Especifique un nombre para la aplicación de función que se va a crear. 

    ```azurecli-interactive
    functionapp=<name of the function app>
    ```
2. Cree la función de Azure. 

    ```azurecli-interactive
    az functionapp create --name $functionapp --storage-account  $functionstorage --resource-group $resourceGroupName --consumption-plan-location eastus
    ```

Ahora debe configurar la aplicación de función para conectarse a la cuenta de Blob Storage que creó en el [tutorial anterior][previous-tutorial].

## <a name="configure-the-function-app"></a>Configuración de la Function App

La función necesita la cadena de conexión para conectarse a la cuenta de Blob Storage. El código de función que se implementa en Azure en el siguiente paso busca la cadena de conexión en la configuración de aplicación myblobstorage_STORAGE y busca el nombre del contenedor de imágenes en miniatura en la configuración de aplicación myContainerName. Obtenga la cadena de conexión con el comando [az storage account show-connection-string](/cli/azure/storage/account). Establezca la configuración de aplicación con el comando [az functionapp config appsettings set](/cli/azure/functionapp/config/appsettings).

En este caso, `<blob_storage_account>` es el nombre de la cuenta de Blob Storage creada en el tutorial anterior.

1. Obtenga la cadena de conexión de la cuenta de almacenamiento que contiene las imágenes. 

    ```azurecli-interactive
    storageConnectionString=$(az storage account show-connection-string --resource-group $resourceGroupName --name $blobStorageAccount --query connectionString --output tsv)
    ```
2. Configure la aplicación de función. 

    ```azurecli-interactive
    az functionapp config appsettings set --name $functionapp --resource-group $resourceGroupName --settings AzureWebJobsStorage=$storageConnectionString THUMBNAIL_CONTAINER_NAME=thumbnails THUMBNAIL_WIDTH=100 FUNCTIONS_EXTENSION_VERSION=~2
    ```

    El valor `FUNCTIONS_EXTENSION_VERSION=~2` hace que la aplicación de función se ejecute en la versión 2.x del entorno de ejecución de Azure Functions.

Ahora puede implementar un proyecto de código de función en esta Function App.

## <a name="deploy-the-function-code"></a>Implementación del código de función 

# <a name="nettabdotnet"></a>[\.NET](#tab/dotnet)

El cambio de tamaño del script C# de ejemplo (.csx) está disponible en [GitHub](https://github.com/Azure-Samples/function-image-upload-resize). Implemente este proyecto de código de Functions en la Function App mediante el comando [az functionapp deployment source config](/cli/azure/functionapp/deployment/source). 

En el siguiente comando, `<function_app>` es el nombre de la aplicación de función que creó anteriormente.

```azurecli-interactive
az functionapp deployment source config --name $functionapp --resource-group $resourceGroupName --branch master --manual-integration --repo-url https://github.com/Azure-Samples/function-image-upload-resize
```

# <a name="nodejstabnodejs"></a>[Node.js](#tab/nodejs)
La función de cambio de tamaño de Node.js de ejemplo está disponible en [GitHub](https://github.com/Azure-Samples/storage-blob-resize-function-node). Implemente este proyecto de código de Functions en la Function App mediante el comando [az functionapp deployment source config](/cli/azure/functionapp/deployment/source).

En el siguiente comando, `<function_app>` es el nombre de la aplicación de función que creó anteriormente.

```azurecli-interactive
az functionapp deployment source config --name <function_app> \
--resource-group myResourceGroup --branch master --manual-integration \
--repo-url https://github.com/Azure-Samples/storage-blob-resize-function-node
```
---

La función de cambio de tamaño de imagen se desencadena mediante solicitudes HTTP que se le envían desde el servicio Event Grid. Indicará a Event Grid que quiere obtener estas notificaciones en la dirección URL de su función mediante la creación de una suscripción a evento. En este tutorial se suscribirá a eventos creados por blob.

Los datos pasados a la función desde la notificación de Event Grid incluyen la dirección URL del blob. A su vez, la dirección URL se pasa al enlace de entrada para obtener la imagen cargada desde Blob Storage. La función genera una imagen en miniatura y escribe el flujo resultante en un contenedor independiente de Blob Storage. 

Este proyecto usa `EventGridTrigger` para el tipo de desencadenador. Es recomendable usar el desencadenador de Event Grid antes que desencadenadores HTTP genéricos. Event Grid valida automáticamente los desencadenadores de Event Grid Function. Con desencadenadores HTTP genéricos, debe implementar la [respuesta de validación](security-authentication.md#webhook-event-delivery).

Para saber más sobre esta función, consulte los archivos [function.json y run.csx](https://github.com/Azure-Samples/function-image-upload-resize/tree/master/imageresizerfunc).
 
El código de proyecto de función se implementa directamente desde el repositorio público de ejemplo. Para más información sobre las opciones de implementación de Azure Functions, vea [Implementación continua para Azure Functions](../azure-functions/functions-continuous-deployment.md).

## <a name="create-an-event-subscription"></a>Creación de una suscripción a evento

Una suscripción de eventos indica los eventos generados por el proveedor que se quieren enviar a un punto de conexión determinado. En este caso, el punto de conexión se expone mediante la función. Use los pasos siguientes para crear una suscripción a evento que envíe notificaciones a su función en Azure Portal: 

1. En [Azure Portal](https://portal.azure.com), seleccione **Todos los servicios** en el menú izquierdo y, a continuación, seleccione **Instancias de Function App**. 

    ![Function Apps en Azure Portal](./media/resize-images-on-storage-blob-upload-event/portal-find-functions.png)

2. Expanda la aplicación de función, elija la función **Thumbnail** y luego seleccione **Agregar suscripción a Event Grid**.

    ![Function Apps en Azure Portal](./media/resize-images-on-storage-blob-upload-event/add-event-subscription.png)

3. Use la configuración de suscripción de eventos que se especifica en la tabla.
    
    ![Creación de suscripción de eventos a partir de la función en Azure Portal](./media/resize-images-on-storage-blob-upload-event/event-subscription-create.png)

    | Configuración      | Valor sugerido  | Descripción                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nombre** | imageresizersub | Nombre que identifica a la nueva suscripción de eventos. | 
    | **Tipo de tema** |  Cuentas de almacenamiento | Elija el proveedor de eventos de las cuentas de almacenamiento. | 
    | **Suscripción** | Su suscripción de Azure | De forma predeterminada, se selecciona la suscripción de Azure actual.   |
    | **Grupos de recursos** | myResourceGroup | Seleccione **Usar existente** y elija el grupo de recursos que se ha venido usando en este tutorial.  |
    | **Recurso** |  La cuenta de Blob Storage |  Elija la cuenta de Blob Storage que ha creado. |
    | **Tipos de evento** | Blob creado | Desactive todos los tipos que no sean **Blob creado**. Solo los tipos de evento de `Microsoft.Storage.BlobCreated` se pasan a la función.| 
    | **Tipo de suscriptor** |  generado automáticamente |  Predefinidos como Webhook. |
    | **Punto de conexión de suscriptor** | generado automáticamente | Use la dirección URL del punto de conexión generado automáticamente. | 
4. Cambie a la pestaña **Filtro** y realice las siguientes acciones:     
    1. Seleccione la opción **Habilitar el filtrado del asunto**.
    2. En **El asunto comienza por**, escriba el siguiente valor: **/blobServices/default/containers/images/blobs/**.

        ![Especificación del filtro para la suscripción a eventos](./media/resize-images-on-storage-blob-upload-event/event-subscription-filter.png) 
2. Seleccione **Crear** para agregar la suscripción de eventos. Se crea una suscripción a evento que desencadena la función `Thumbnail` cuando se agrega un blob al contenedor `images`. La función cambia el tamaño de las imágenes y las agrega al contenedor `thumbnails`.

Ahora que se han configurado los servicios back-end, pruebe la funcionalidad de cambio de tamaño de imagen en la aplicación web de ejemplo. 

## <a name="test-the-sample-app"></a>Prueba de la aplicación de ejemplo

Para probar el cambio de tamaño de imagen en la aplicación web, vaya a la dirección URL de la aplicación publicada. La dirección URL predeterminada de la aplicación web es `https://<web_app>.azurewebsites.net`.

Haga clic en la región **Cargar fotos** para seleccionar y cargar un archivo. También puede arrastrar una foto a esta región. 

Observe que después de que la imagen cargada desaparezca, se muestra una copia de ella en el carrusel **Miniaturas generadas**. La función ha cambiado el tamaño de la imagen, la imagen se ha agregado al contenedor *thumbnails* y el cliente web la ha descargado.

![Aplicación web publicada en el explorador Microsoft Edge](./media/resize-images-on-storage-blob-upload-event/tutorial-completed.png) 

## <a name="next-steps"></a>Pasos siguientes

En este tutorial aprendió lo siguiente:

> [!div class="checklist"]
> * Crear una cuenta general de Azure Storage
> * Implementar código sin servidor con Azure Functions
> * Crear una suscripción de eventos de Blob Storage en Event Grid

Vaya a la tercera parte de la serie de tutoriales sobre almacenamiento para aprender a proteger el acceso a la cuenta de almacenamiento.

> [!div class="nextstepaction"]
> [Proteger el acceso a los datos de una aplicación en la nube](../storage/blobs/storage-secure-access-application.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

+ Para más información sobre Event Grid, vea [Una introducción a Event Grid](overview.md). 
+ Para probar otro tutorial sobre Azure Functions, vea [Creación de una función que se integre con Azure Logic Apps](../azure-functions/functions-twitter-email.md). 

[previous-tutorial]: ../storage/blobs/storage-upload-process-images.md
