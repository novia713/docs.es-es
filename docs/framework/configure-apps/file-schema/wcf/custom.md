---
title: '&lt;Personalizado&gt;'
ms.date: 03/30/2017
ms.assetid: a6f65a00-bd1a-4d4a-955a-fe009ec02ab8
ms.openlocfilehash: 7d558be66b8a1e46d9743c5f8bf0bb9a8b4c349e
ms.sourcegitcommit: fb78d8abbdb87144a3872cf154930157090dd933
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47207817"
---
# <a name="ltcustomgt"></a>&lt;Personalizado&gt;
Especifica la configuración concreta para un servicio de resolución del mismo nivel personalizado.  
  
\<system.serviceModel>  
\<enlaces >  
\<netPeerBinding >  
\<enlace >  
\<resolución >  
\<personalizado >  
  
## <a name="syntax"></a>Sintaxis  
  
```xml
<custom address="Uri" 
        resolverType="String">  
  <headers/>  
  <identity/>  
</custom>  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|`address`|Un URI que especifica la dirección de extremo del nodo de iguales que hospeda el servicio de resolución del mismo nivel personalizado.|  
|`resolverType`|Una cadena que especifica el tipo de servicio de resolución del mismo nivel personalizado.|  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<identidad >](../../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)|Especifica la identidad para las resoluciones del mismo nivel personalizadas configuradas con este elemento. Este elemento es del tipo <xref:System.ServiceModel.Configuration.IdentityElement>.|  
|[\<encabezados >](../../../../../docs/framework/configure-apps/file-schema/wcf/headers-element.md)|Una colección de encabezado de dirección usada para mensajes SOAP administrados por la resolución del mismo nivel personalizada.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<resolución >](../../../../../docs/framework/configure-apps/file-schema/wcf/resolver.md)|Una resolución del mismo nivel que se usa para resolver un Id. de malla del mismo nivel como un conjunto de direcciones del nodo del mismo nivel que representa varios nodos que participan en la malla.|  
  
## <a name="remarks"></a>Comentarios  
 Este elemento define la configuración básica para un servicio de la resolución del mismo nivel personalizado, incluso la dirección de punto de conexión del igual que hospeda el servicio y cualquier configuración de enlace concreta. Para obtener más información sobre la creación de un solucionador personalizado, consulte [agregando un solucionador personalizado a una aplicación PeerChannel](https://msdn.microsoft.com/library/12aa3787-2962-439c-ad27-46523c8b0419).  
  
## <a name="see-also"></a>Vea también  
 <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService>  
 <xref:System.ServiceModel.PeerResolvers.PeerCustomResolverSettings>  
 <xref:System.ServiceModel.Configuration.PeerResolverElement.Custom%2A>  
 <xref:System.ServiceModel.Configuration.PeerCustomResolverElement>  
 [Resoluciones del mismo nivel](../../../../../docs/framework/wcf/feature-details/peer-resolvers.md)  
 [Adición de un solucionador personalizado a una aplicación PeerChannel](https://msdn.microsoft.com/library/12aa3787-2962-439c-ad27-46523c8b0419)
