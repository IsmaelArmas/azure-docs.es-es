---
title: Cambiar un emparejamiento público a emparejamiento de Microsoft | Microsoft Docs
description: En este artículo se detallan los pasos para cambiar un emparejamiento público a emparejamiento de Microsoft en ExpressRoute.
services: expressroute
author: cherylmc
ms.service: expressroute
ms.topic: article
ms.date: 03/12/2018
ms.author: cherylmc
ms.custom: seodec18
ms.openlocfilehash: 6b2bce6b488698db0a72c9a17f67c2555c6afa5b
ms.sourcegitcommit: 9fb6f44dbdaf9002ac4f411781bf1bd25c191e26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2018
ms.locfileid: "53100028"
---
# <a name="move-a-public-peering-to-microsoft-peering"></a>Cambiar un emparejamiento público a emparejamiento de Microsoft

Este artículo le servirá para cambiar una configuración de emparejamiento público a emparejamiento de Microsoft sin sufrir ningún tiempo de inactividad. ExpressRoute admite el uso del emparejamiento de Microsoft con filtros de ruta para los servicios de PaaS de Azure, como Azure Storage y Azure SQL Database. Ahora solo se necesita un dominio de enrutamiento para tener acceso a PaaS de Microsoft y a los servicios de SaaS. Puede usar los filtros de ruta para anunciar los prefijos del servicio de PaaS de forma selectiva en las regiones de Azure que quiere que se usen. Para más información sobre cómo enrutar emparejamientos y dominios de enrutamiento, vea [Circuitos ExpressRoute y dominios de enrutamiento](expressroute-circuit-peerings.md).

## <a name="before"></a>Antes de empezar

* Para conectarse al emparejamiento de Microsoft, necesita configurar y administrar NAT. Puede que su proveedor de conectividad haya configurado y administrado NAT como un servicio administrado. Si tiene previsto acceder a servicios de PaaS y SaaS de Azure en el emparejamiento de Microsoft, es importante cambiar correctamente el tamaño del grupo de direcciones IP de NAT. Para más información sobre NAT para ExpressRoute, vea [Requisitos NAT para el emparejamiento de Microsoft](expressroute-nat.md#nat-requirements-for-microsoft-peering).

* Si usa el emparejamiento público y actualmente tiene reglas de red IP para las direcciones IP públicas que se usan para acceder a [Azure Storage](../storage/common/storage-network-security.md) o [Azure SQL Database](../sql-database/sql-database-vnet-service-endpoint-rule-overview.md), tiene que asegurarse de que el grupo de IP de NAT configurado con el emparejamiento de Microsoft se incluye en la lista de direcciones IP públicas de la cuenta de Azure Storage o Azure SQL.

* Para cambiar a un emparejamiento de Microsoft sin sufrir tiempos de inactividad, realice los pasos de este artículo en el orden en el que aparecen.

## <a name="create"></a>1. Crear el emparejamiento de Microsoft

Si no ha creado el emparejamiento de Microsoft, use cualquiera de los siguientes artículos para crearlo. Si su proveedor de conectividad presta servicios administrados de nivel 3, puede pedirle que habilite el emparejamiento de Microsoft en su circuito.

  * [Creación del emparejamiento de Microsoft con Azure Portal](expressroute-howto-routing-portal-resource-manager.md#msft)
  * [Creación del emparejamiento de Microsoft con Azure PowerShell](expressroute-howto-routing-arm.md#msft)
  * [Creación del emparejamiento de Microsoft con la CLI de Azure](howto-routing-cli.md#msft)

## <a name="validate"></a>2. Confirmar que el emparejamiento de Microsoft está habilitado

Compruebe que el emparejamiento de Microsoft está habilitado y que los prefijos públicos anunciados están en estado configurado.

  * [Azure Portal](expressroute-howto-routing-portal-resource-manager.md#getmsft)
  * [Azure PowerShell](expressroute-howto-routing-arm.md#getmsft)
  * [CLI de Azure](howto-routing-cli.md#getmsft)

## <a name="routefilter"></a>3. Configurar un filtro de ruta y adjuntarlo al circuito

De forma predeterminada, los emparejamientos de Microsoft nuevos no publican ningún prefijo hasta que se adjunta un filtro de ruta al circuito. Cuando se crea una regla de filtro de ruta, puede especificar la lista de comunidades de servicio correspondientes a las regiones de Azure que quiere usar para los servicios de PaaS de Azure, como se muestra en la siguiente captura de pantalla:

![Combinar emparejamientos públicos](./media/how-to-move-peering/public.png)

Para configurar filtros de ruta, use cualquiera de los siguientes artículos:

  * [Configuración de filtros de ruta para el emparejamiento de Microsoft: Azure Portal](how-to-routefilter-portal.md)
  * [Configuración de filtros de ruta para el emparejamiento de Microsoft: PowerShell](how-to-routefilter-powershell.md)
  * [Configuración de filtros de ruta para el emparejamiento de Microsoft: CLI de Azure](how-to-routefilter-cli.md)

## <a name="delete"></a>4. Eliminar el emparejamiento público

Tras constatar que el emparejamiento de Microsoft está configurado y que los prefijos que se van a usar se anuncian correctamente en el emparejamiento de Microsoft, puede eliminar el emparejamiento público. Para eliminar el emparejamiento público, use cualquiera de los siguientes artículos:

  * [Eliminación del emparejamiento público de Azure con Azure Portal](expressroute-howto-routing-portal-resource-manager.md#deletepublic)
  * [Eliminación del emparejamiento público de Azure con Azure PowerShell](expressroute-howto-routing-arm.md#deletepublic)
  * [Eliminación del emparejamiento público de Azure con la CLI](howto-routing-cli.md#deletepublic)
  
## <a name="view"></a>5. Visualización de emparejamientos
  
Puede ver una lista de todos los circuitos y emparejamientos de ExpressRoute en Azure Portal. Para obtener más información, consulte [Visualización de detalles del emparejamiento de Microsoft](expressroute-howto-routing-portal-resource-manager.md#getmsft).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de ExpressRoute, consulte [P+F de ExpressRoute](expressroute-faqs.md).
