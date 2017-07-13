---
title: "Seguridad distribuida de aplicaciones | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "seguridad distribuida de aplicaciones [WCF]"
  - "seguridad [WCF], transferencia"
ms.assetid: 53928a10-e474-46d0-ab90-5f98f8d7b668
caps.latest.revision: 32
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 32
---
# Seguridad distribuida de aplicaciones
La seguridad de [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] está dividida en tres áreas funcionales principales: seguridad de transferencia, control de acceso y auditoría.La seguridad de transferencia proporciona integridad, confidencialidad y autenticación.La seguridad de transferencia la proporciona uno de los siguientes elementos: seguridad de transporte, seguridad de mensajes o `TransportWithMessageCredential`.  
  
 Para obtener información general sobre la seguridad de mensajes de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vea [Información general sobre seguridad](../../../../docs/framework/wcf/feature-details/security-overview.md).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] los otros dos fragmentos de seguridad de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] , vea [Autorización](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md) y [Auditoría](../../../../docs/framework/wcf/feature-details/auditing-security-events.md).  
  
## Escenarios de seguridad de transferencia  
 Entre los escenarios comunes que utilizan la seguridad de transferencia de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] se incluyen los siguientes:  
  
-   Transferencia segura mediante Windows.Un cliente y servicio de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] se implementan en un dominio de Windows \(o un bosque de Windows\).Los mensajes contienen datos personales, por lo que entre los requisitos se incluye la autenticación mutua de cliente y servicio, la integridad y la confidencialidad de los mensajes.Además, se requiere la prueba de que una transacción determinada se produjo, por ejemplo, el receptor del mensaje debería registrar la información de la firma.  
  
-   Transferencia segura mediante `UserName` y HTTPS.Un cliente y servicio de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] han de desarrollarse para funcionar a través de Internet.Las credenciales de clientes se autentican frente a una base de datos de pares de nombres de usuario y contraseñas.El servicio se implementa en una dirección HTTPS utilizando un certificado Secure Sockets Layer \(SSL\) de confianza.Dado que los mensajes viajan a través de Internet, el cliente y servicio deben autenticarse mutuamente y se debe preservar la confidencialidad e integridad de los mensajes durante la transferencia.  
  
-   Transferencia segura mediante el uso de certificados.Un cliente y servicio de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] han de desarrollarse para funcionar sobre la Internet pública.El cliente y el servicio tienen certificados que se pueden utilizar para proteger los mensajes.El cliente y el servicio utilizan Internet para comunicarse entre sí y realizar transacciones de valor alto que requieren integridad del mensaje, confidencialidad y autenticación mutua.  
  
## Integridad, confidencialidad y autenticación  
 Tres funciones se llaman conjuntamente seguridad de transferencia: integridad, confidencialidad y autenticación.La seguridad de transferencia proporciona funciones que ayudan a mitigar las amenazas para una aplicación distribuida.La siguiente tabla describe brevemente las tres funciones que constituyen la seguridad de transferencia.  
  
|Función|Descripción|  
|-------------|-----------------|  
|Integridad|La *integridad* es la garantía de que los datos son completos y precisos, sobre todo después de haber pasado desde un punto hasta otro, y posiblemente han sido leídos por muchos actores.La integridad debe mantenerse para evitar la modificación de los datos y normalmente se logra mediante la firma digital de un mensaje.|  
|Confidencialidad|La *confidencialidad* es la garantía de que un mensaje no ha sido leído por nadie que no sea el lector para el que estaba destinado.Por ejemplo, un número de tarjeta de crédito se debe mantener de manera confidencial al enviarse a través de Internet.La confidencialidad es a menudo proporcionada por el cifrado de datos utilizando un esquema de clave pública\/privada.|  
|Autenticación|La *autenticación* es la comprobación de una identidad reivindicada.Por ejemplo, al utilizar una cuenta bancaria, es imperativo que solo el propietario real de la cuenta pueda retirar los fondos.Diversos recursos pueden proporcionar la autenticación.Un método común es el sistema de usuario\/contraseña.Otro método consiste en el uso de un certificado X.509 proporcionado por un tercero.|  
  
## Modos de seguridad  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] tiene varios modos de seguridad de transferencia, que se describen en la siguiente tabla.  
  
|Modo|Descripción|  
|----------|-----------------|  
|Ninguno|No se proporciona ninguna seguridad en el nivel de transporte o en el nivel del mensaje.Ninguno de los enlaces predefinido utilizan este modo de forma predeterminada excepto el elemento [\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md) o, si se utiliza código, la clase <xref:System.ServiceModel.BasicHttpBinding>.|  
|Transporte|Utiliza un transporte seguro como HTTPS para la integridad, confidencialidad y autenticación mutua.|  
|Mensaje|Utiliza seguridad del mensaje SOAP para la integridad, confidencialidad y autenticación mutua.Los mensajes SOAP se protegen según los estándares de WS\-Security.|  
|Modo mixto|Utiliza la seguridad de transporte para la integridad, confidencialidad y autenticación de servidor.Utiliza la seguridad de mensajes \(WS\-Security y otros estándares\) para la autenticación del cliente.<br /><br /> \(Esta enumeración para este modo es `TransportWithMessageCredential`.\)|  
|Ambos|Lleva a cabo la protección y autenticación en ambos niveles.Este modo solo está disponible en el elemento [\<netMsmqBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/netmsmqbinding.md).|  
  
## Seguridad de transferencia y credenciales  
 Una *credencial* son datos que se presentan para establecer una identidad reivindicada o funciones.La presentación de una credencial implica la presentación de los datos y de la prueba de posesión de los datos.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] admite diversos tipos de credenciales en los niveles de seguridad de transporte y de mensaje.Puede especificar un tipo de credencial para un enlace de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 En muchos países o regiones, un permiso de conducción es un ejemplo de credencial.Un permiso contiene datos que representan la identidad y las capacidades de cada uno.Contiene prueba de posesión en forma de la imagen del poseedor.Una entidad emisora de confianza emite la licencia; normalmente, un departamento gubernamental de licencias.Se sella la licencia, que puede contener un holograma, que muestra que no se ha manipulado o falsificado.  
  
 A modo de ejemplo, considere dos tipos de credenciales admitidos en [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]: el nombre de usuario y las credenciales del certificado \(X.509\).  
  
 Para la credencial de nombre de usuario, el nombre de usuario representa la identidad reivindicada y la contraseña constituye la prueba de posesión.La autoridad de confianza en este caso es el sistema que valida el nombre de usuario y la contraseña.  
  
 En la credencial del certificado, el nombre del sujeto, el nombre alternativo del sujeto o los campos concretos dentro del certificado se puede utilizar para representar la identidad y\/o funciones reivindicadas.La prueba de posesión de los datos en la credencial se establece mediante el uso de la clave privada asociada para generar una firma.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] la programación de seguridad de transferencia y especificación de credenciales, vea [Enlaces y seguridad](../../../../docs/framework/wcf/feature-details/bindings-and-security.md) y [Comportamientos de seguridad](../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md).  
  
### Tipos de credenciales de cliente de transporte  
 La siguiente tabla muestra los posibles valores utilizados al crear una aplicación que utiliza la seguridad de transferencia.Puede utilizar estos valores en código o ajustes de enlaces.  
  
|Configuración|Descripción|  
|-------------------|-----------------|  
|None|Especifica que el cliente no necesita presentar ningún credencial.Realiza una conversión a un cliente anónimo.|  
|Básica|Especifica la autenticación básica.Para obtener información adicional, consulte RFC2617, “[Autenticación HTTP: autenticación básica e implícita](http://go.microsoft.com/fwlink/?LinkId=88313)”.|  
|Implícita|Especifica la autenticación implícita.Para obtener información adicional, consulte RFC2617, “[Autenticación HTTP: autenticación básica e implícita](http://go.microsoft.com/fwlink/?LinkId=88313)”.|  
|Ntlm|Especifica autenticación de Windows mediante negociación SSPI en un dominio de Windows.<br /><br /> La negociación SSPI resulta en el uso del protocolo Kerberos o NT LanMan \(NTLM\).|  
|Windows|Especifica autenticación de Windows utilizando SSPI en un dominio de Windows.SSPI escoge del protocolo Kerberos o NTLM como servicio de autenticación.<br /><br /> SSPI prueba primero el protocolo Kerberos; si eso falla, utiliza NTLM.|  
|Certificado|Realiza la autenticación de cliente utilizando un certificado, normalmente X.509.|  
  
### Tipos de credencial de cliente de mensaje  
 La siguiente tabla muestra los posibles valores utilizados al crear una aplicación que utiliza la seguridad de mensajes.Puede utilizar estos valores en código o ajustes de enlaces.  
  
|Configuración|Descripción|  
|-------------------|-----------------|  
|None|Permite al servicio interactuar con clientes anónimos.|  
|Windows|Permite a los intercambios de mensajes SOAP ocurrir bajo el contexto autenticado de una credencial de Windows.Utiliza el mecanismo de negociación de SSPI para escoger entre el protocolo Kerberos o NTLM como servicio de autenticación.|  
|Nombre de usuario|Permite que el servicio requiera que el cliente se autentique con una credencial del nombre de usuario.Tenga en cuenta que [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] no permite ninguna operación criptográfica con el nombre de usuario, como, por ejemplo, generar una firma o cifrar los datos.Como tal, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] garantiza que el transporte se asegure al usar credenciales de nombres de usuario.|  
|Certificado|Permite al servicio exigir la autenticación del cliente mediante un certificado.|  
|[!INCLUDE[infocard](../../../../includes/infocard-md.md)]|Permite al servicio que requiera la autenticación del cliente mediante un [!INCLUDE[infocard](../../../../includes/infocard-md.md)].|  
  
### Programación de credenciales  
 Para cada uno de los tipos de credenciales de cliente, el modelo de programación de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] le permite especificar los valores de credenciales y validadores de credenciales mediante los comportamientos de servicio y de canal.  
  
 La seguridad de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] tiene dos tipos de credenciales: comportamientos de credenciales de servicio y comportamientos de credenciales de canal.Los comportamientos de credenciales en [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] especifican los datos reales, esto es, las credenciales utilizadas para cumplir los requisitos de seguridad expresados a través de enlaces.En [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], una clase de cliente es el componente en tiempo de ejecución que convierte entre la invocación de operaciones y los mensajes.Todos los clientes heredan de la clase <xref:System.ServiceModel.ClientBase%601>.La propiedad <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> en la clase base permite especificar varios valores de credenciales del cliente.  
  
 En [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], los comportamientos de servicio son atributos aplicados a la clase que implementa un contrato de servicios \(interfaz\) para controlar mediante programación el servicio.La clase <xref:System.ServiceModel.Description.ServiceCredentials> le permite especificar certificados para la configuración de la validación de cliente y credenciales de servicio para varios tipos de credenciales de cliente.  
  
### Modelo de negociación para la seguridad de mensajes  
 El modo de seguridad de mensajes le permite realizar la seguridad de transferencia para que la credencial del servicio se configure en el cliente fuera de banda.Por ejemplo, si está utilizando un certificado almacenado en el almacén de certificados de Windows, debe utilizar una herramienta como el complemento Microsoft Management Console \(MMC\).  
  
 El modo de seguridad de mensajes también permite aplicar la seguridad de transferencia para que la credencial del servicio se intercambie con el cliente como parte de una negociación inicial.Para habilitar la negociación, establezca la propiedad <xref:System.ServiceModel.MessageSecurityOverHttp.NegotiateServiceCredential%2A> en `true`.  
  
## Vea también  
 [Información general acerca de la creación de puntos finales](../../../../docs/framework/wcf/endpoint-creation-overview.md)   
 [Enlaces proporcionados por el sistema](../../../../docs/framework/wcf/system-provided-bindings.md)   
 [Información general sobre seguridad](../../../../docs/framework/wcf/feature-details/security-overview.md)   
 [Modelo de seguridad para Windows Server App Fabric](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)