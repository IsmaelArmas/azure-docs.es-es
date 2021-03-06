---
title: Procedimientos recomendados para Azure Kubernetes Service (AKS)
description: Colección de procedimientos recomendados de operadores de clúster y desarrolladores para crear y administrar aplicaciones en Azure Kubernetes Service (AKS)
services: container-service
author: iainfoulds
ms.service: container-service
ms.topic: article
ms.date: 12/07/18
ms.author: iainfou
ms.openlocfilehash: ef7dabc8bf792893380b80458d5fb20aa15cd909
ms.sourcegitcommit: 1c1f258c6f32d6280677f899c4bb90b73eac3f2e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53256475"
---
# <a name="cluster-operator-and-developer-best-practices-to-build-and-manage-applications-on-azure-kubernetes-service-aks"></a>Procedimientos recomendados de operadores de clúster y desarrolladores para crear y administrar aplicaciones en Azure Kubernetes Service (AKS)

Para compilar y ejecutar aplicaciones correctamente en Azure Kubernetes Service (AKS), hay algunas consideraciones claves que debe comprender e implementar. Estas áreas incluyen las características de servicios multiinquilino y programador, seguridad de pod y clúster, o continuidad empresarial y recuperación ante desastres. Los siguientes procedimientos recomendados se han agrupado para ayudar a los operadores de clúster y desarrolladores a comprender las consideraciones para cada una de estas áreas e implementar las características adecuadas.

Estos procedimientos recomendados y los artículos conceptuales se han redactado junto con el grupo de productos de AKS, equipos de ingeniería y equipos de campo, incluidos cinturones negros globales (GBB).

## <a name="cluster-operator-best-practices"></a>Procedimientos recomendados para operadores de clúster

Como operador de clúster, trabaje en conjunto con los propietarios y desarrolladores de aplicaciones para conocer sus necesidades. A continuación, puede usar los siguientes procedimientos recomendados para configurar los clústeres de AKS según sea necesario.

**Servicios multiinquilino**

* [Procedimientos recomendados para el aislamiento de clústeres](operator-best-practices-cluster-isolation.md)
    * Incluye los componentes principales de los servicios multiinquilino y el aislamiento lógico con espacios de nombres.
* [Procedimientos recomendados para las características básicas del programador](operator-best-practices-scheduler.md)
    * Incluye el uso de las cuotas de recursos y los presupuestos de interrupciones de pod.
* [Procedimientos recomendados para las características avanzadas del programador](operator-best-practices-advanced-scheduler.md)
    * Incluye el uso de defectos y tolerancias, los selectores de nodo y afinidad, y la afinidad y falta de afinidad entre pods.
* [Procedimientos recomendados para autenticación y autorización](operator-best-practices-identity.md)
    * Incluye integración en Azure Active Directory, el uso de controles de acceso basado en roles (RBAC) y las identidades de pods.

**Seguridad**

* [Procedimientos recomendados para actualizaciones y seguridad de clústeres](operator-best-practices-cluster-security.md)
    * Incluye la protección del acceso al servidor de API, limitar el acceso a los contenedores y la administración de las actualizaciones y los reinicios de nodos.
* [Procedimientos recomendados para la administración y la protección de las imágenes de contenedor](operator-best-practices-container-image-management.md)
    * Incluye la protección de la imagen y los tiempos de ejecución, el uso de registros de confianza y compilaciones automatizadas en actualizaciones de la imagen base.
* [Procedimientos recomendados para la seguridad de pods](developer-best-practices-pod-security.md)
    * Incluye la protección del acceso a los recursos, la limitación de la exposición de las credenciales y el uso de identidades de pods y almacenes de claves digitales.

**Red y almacenamiento**

* [Procedimientos recomendados para la conectividad de red](operator-best-practices-network.md)
    * Incluye distintos modelos de red, el uso de firewalls de aplicaciones web (WAF) y de entrada, y la protección del acceso SSH a los nodos.
* [Procedimientos recomendados para almacenamiento y copias de seguridad](operator-best-practices-storage.md)
    * Incluye la elección del tipo de almacenamiento y el tamaño de nodo apropiados, el aprovisionamiento dinámico de volúmenes, y copias de seguridad de datos.

**Ejecución de cargas de trabajo preparadas para la empresa**

* [Procedimientos recomendados para continuidad empresarial y recuperación ante desastres](operator-best-practices-multi-region.md)
    * Incluye el uso de pares de regiones, varios clústeres con Azure Traffic Manager y la replicación geográfica de las imágenes de contenedor.

## <a name="developer-best-practices"></a>Procedimientos recomendados para desarrolladores

Como desarrollador o propietario de una aplicación, puede simplificar su experiencia de desarrollo y definir las necesidades de rendimiento de la aplicación.

* [Procedimientos recomendados para desarrolladores de aplicaciones para administrar recursos](developer-best-practices-resource-management.md)
    * Incluye la definición de las solicitudes y los límites de recursos de pod, la configuración de las herramientas de desarrollo y la comprobación de problemas de la aplicación.
* [Procedimientos recomendados para la seguridad de pods](developer-best-practices-pod-security.md)
    * Incluye la protección del acceso a los recursos, la limitación de la exposición de las credenciales y el uso de identidades de pods y almacenes de claves digitales.

## <a name="kubernetes--aks-concepts"></a>Conceptos de Kubernetes/AKS

Para ayudar a comprender algunas de las características y componentes de estos procedimientos recomendados, también puede consultar los siguientes artículos conceptuales para clústeres en Azure Kubernetes Service (AKS):

* [Conceptos básicos de Kubernetes](concepts-clusters-workloads.md)
* [Acceso e identidad](concepts-identity.md)
* [Conceptos de seguridad](concepts-security.md)
* [Conceptos de red](concepts-network.md)
* [Opciones de almacenamiento](concepts-storage.md)
* [Opciones de escalado](concepts-scale.md)

## <a name="next-steps"></a>Pasos siguientes

Si necesita empezar a trabajar con AKS, siga uno de los tutoriales de inicio rápido para implementar un clúster de Azure Kubernetes Service (AKS) con la [CLI de Azure](kubernetes-walkthrough.md) o [Azure Portal](kubernetes-walkthrough-portal.md).
