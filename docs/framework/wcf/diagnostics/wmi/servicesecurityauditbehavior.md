---
title: ServiceSecurityAuditBehavior
ms.date: 03/30/2017
ms.assetid: 2c5809e7-5364-44ce-bc71-848be4672e2a
author: BrucePerlerMS
ms.openlocfilehash: 8f43ee752830d95db6bbbdbe311b6d77735e31b5
ms.sourcegitcommit: fb78d8abbdb87144a3872cf154930157090dd933
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47196897"
---
# <a name="servicesecurityauditbehavior"></a>ServiceSecurityAuditBehavior
ServiceSecurityAuditBehavior  
  
## <a name="syntax"></a>Sintaxis  
  
```  
class ServiceSecurityAuditBehavior : Behavior  
{  
  string AuditLogLocation;  
  string MessageAuthenticationAuditLevel;  
  string ServiceAuthorizationAuditLevel;  
  boolean SuppressAuditFailure;  
};  
```  
  
## <a name="methods"></a>Métodos  
 La clase ServiceSecurityAuditBehavior no define ningún método.  
  
## <a name="properties"></a>Propiedades  
 La clase ServiceSecurityAuditBehavior tiene las propiedades siguientes:  
  
### <a name="auditloglocation"></a>AuditLogLocation  
 Tipo de datos: cadena  
  
 Tipo de acceso: solo lectura  
  
 La ubicación del registro de auditoría.  
  
### <a name="messageauthenticationauditlevel"></a>MessageAuthenticationAuditLevel  
 Tipo de datos: cadena  
  
 Tipo de acceso: solo lectura  
  
 El tipo de nivel de autenticación de mensajes que se usa para registrar eventos de auditoría.  
  
### <a name="serviceauthorizationauditlevel"></a>ServiceAuthorizationAuditLevel  
 Tipo de datos: cadena  
  
 Tipo de acceso: solo lectura  
  
 Los tipos de eventos de autorización que se graban en el registro de auditoría.  
  
### <a name="suppressauditfailure"></a>SuppressAuditFailure  
 Tipo de datos: booleano  
  
 Tipo de acceso: solo lectura  
  
 Un valor booleano que especifica el comportamiento para suprimir errores al escribir en el registro de auditoría.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Se declara en Servicemodel.mof.|  
|---------|-----------------------------------|  
|Espacio de nombres|Se define en root\ServiceModel|  
  
## <a name="see-also"></a>Vea también  
 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>
