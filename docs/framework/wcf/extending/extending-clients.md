---
title: Extensión de clientes
ms.date: 03/30/2017
helpviewer_keywords:
- proxy extensions [WCF]
ms.assetid: 1328c61c-06e5-455f-9ebd-ceefb59d3867
ms.openlocfilehash: 95340a9ae6ac5a3face81d5fe6f61ea134fb6ad2
ms.sourcegitcommit: 15109844229ade1c6449f48f3834db1b26907824
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2018
ms.locfileid: "33806661"
---
# <a name="extending-clients"></a>Extensión de clientes
En una aplicación que realiza la llamada, el nivel de modelo de servicio es responsable de traducir invocaciones de método en el código de la aplicación a mensajes salientes, insertarlos en los canales subyacentes, traducir los resultados en valores devueltos y los parámetros de salida en el código de la aplicación, y devolver los resultados al autor de la llamada. Las extensiones de modelo de servicio modifican o implementan el comportamiento de la comunicación o la ejecución y características implicadas en la funcionalidad de distribuidor o cliente, comportamientos personalizados, interceptación de mensajes y parámetros, y otra funcionalidad de extensibilidad.  
  
 Este tema describe cómo utilizar el <xref:System.ServiceModel.Dispatcher.ClientRuntime> y <xref:System.ServiceModel.Dispatcher.ClientOperation> clases en una aplicación de cliente de Windows Communication Foundation (WCF) para modificar el comportamiento de ejecución predeterminado de un cliente WCF o para interceptar o modificar mensajes, parámetros o valores devueltos antes o después de enviar o recuperarlos desde la capa del canal. Para obtener más información acerca de cómo ampliar el tiempo de ejecución de servicio, consulte [extender distribuidores](../../../../docs/framework/wcf/extending/extending-dispatchers.md). Para obtener más información acerca de los comportamientos que modificar e insertar los objetos de personalización en el tiempo de ejecución de cliente, consulte [configuración y al ampliar el tiempo de ejecución con comportamientos](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md).  
  
## <a name="clients"></a>Clientes  
 En un cliente, un canal de cliente o el objeto de cliente WCF convierte las invocaciones de método en mensajes salientes y los mensajes entrantes a los resultados de la operación que se devuelven a la aplicación que realiza la llamada. (Para obtener más información acerca de los tipos de cliente, consulte [arquitectura de cliente de WCF](../../../../docs/framework/wcf/feature-details/client-architecture.md).)  
  
 Tipos de cliente WCF tienen tipos de tiempo de ejecución que gestionan esta funcionalidad en el nivel de punto de conexión y operación. Cuando una aplicación llama a una operación, <xref:System.ServiceModel.Dispatcher.ClientOperation> traduce los objetos salientes en un mensaje, procesa los interceptores, confirma que la llamada saliente cumple con el contrato de destino y entrega el mensaje saliente a <xref:System.ServiceModel.Dispatcher.ClientRuntime>, que es responsable de crear y administrar los canales salientes (y canales entrantes en el caso de los servicios dúplex), administrar el procesamiento de mensajes salientes adicionales (como la modificación del encabezado), procesar los interceptores de mensajes en ambas direcciones y enrutar las llamadas dúplex entrantes hacia el objeto <xref:System.ServiceModel.Dispatcher.DispatchRuntime> en el lado del cliente adecuado. <xref:System.ServiceModel.Dispatcher.ClientOperation> y <xref:System.ServiceModel.Dispatcher.ClientRuntime> proporcionan servicios similares cuando los mensajes (incluidos los errores) se devuelven al cliente.  
  
 Estas dos clases en tiempo de ejecución son la extensión principal para personalizar el procesamiento de objetos de cliente WCF y canales. La clase <xref:System.ServiceModel.Dispatcher.ClientRuntime> permite a los usuarios interceptar y extender la ejecución del cliente por todos los mensajes en el contrato. La clase <xref:System.ServiceModel.Dispatcher.ClientOperation> permite a los usuarios interceptar y extender la ejecución del cliente para todos los mensajes en una operación determinada.  
  
 La modificación de las propiedades o la inserción de personalizaciones se realiza mediante los comportamientos del contrato, del punto de conexión y de la operación. Para obtener más información acerca de cómo usar estos tipos de comportamientos para realizar las personalizaciones en tiempo de ejecución de cliente, consulte [configuración y al ampliar el tiempo de ejecución con comportamientos](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md).  
  
## <a name="scenarios"></a>Escenarios  
 Hay varias razones para extender el sistema cliente, incluidas:  
  
-   Validación personalizada del mensaje. Un usuario puede querer exigir que un mensaje sea válido para un determinado esquema. Esto se puede hacer implementando la interfaz <xref:System.ServiceModel.Dispatcher.IClientMessageInspector> y asignando la implementación en la propiedad <xref:System.ServiceModel.Dispatcher.DispatchRuntime.MessageInspectors%2A>. Para obtener ejemplos, vea [Cómo: inspeccionar o modificar mensajes en el cliente](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-messages-on-the-client.md) y [Cómo: inspeccionar o modificar mensajes en el cliente](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-messages-on-the-client.md).  
  
-   Registro personalizado de mensajes. Un usuario puede desear inspeccionar y registrar un conjunto de mensajes de la aplicación que fluyen a través de un punto de conexión. Esto también se puede lograr con las interfaces del interceptor de mensajes.  
  
-   Transformaciones personalizadas del mensaje. En lugar de modificar el código de aplicación, el usuario puede querer aplicar ciertas transformaciones al mensaje en el tiempo de ejecución (por ejemplo, para controlar las versiones). Esto también se puede lograr, de nuevo, con las interfaces del interceptor de mensajes.  
  
-   Modelo de datos personalizado. Un usuario puede desear tener un modelo de datos o de serialización distinto de aquellos admitidos de forma predeterminada en WCF (es decir, <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>, <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>, y <xref:System.ServiceModel.Channels.Message?displayProperty=nameWithType> objetos). Esto se puede hacer implementando las interfaces del formateador de mensajes. Para obtener más información, vea <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter?displayProperty=nameWithType> y la propiedad <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A?displayProperty=nameWithType>.  
  
-   Validación personalizada de parámetros. Un usuario puede querer exigir que los parámetros con tipo sean válidos (por oposición a XML). Esto puede hacerse mediante las interfaces del inspector de parámetros. Para obtener un ejemplo, vea [Cómo: inspeccionar o modificar parámetros](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-parameters.md) o [validación del cliente](../../../../docs/framework/wcf/samples/client-validation.md).  
  
### <a name="using-the-clientruntime-class"></a>Uso de la clase ClientRuntime  
 La clase <xref:System.ServiceModel.Dispatcher.ClientRuntime> es un punto de extensibilidad al que puede agregar objetos de extensión que interceptan los mensajes y extienden el comportamiento del cliente. Los objetos de interceptación pueden procesar todos los mensajes de un contrato determinado, procesar solo los mensajes para operaciones determinadas, realizar la inicialización personalizada de canales e implementar otro comportamiento de aplicación cliente personalizado.  
  
-   La propiedad <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackDispatchRuntime%2A> devuelve el objeto en tiempo de ejecución de envío para los clientes de devolución de llamada iniciados por el servicio.  
  
-   La propiedad <xref:System.ServiceModel.Dispatcher.ClientRuntime.OperationSelector%2A> acepta un objeto de selector de operación personalizado.  
  
-   La propiedad <xref:System.ServiceModel.Dispatcher.ClientRuntime.ChannelInitializers%2A> habilita la adición de un inicializador de canales que puede inspeccionar o modificar el canal del cliente.  
  
-   La propiedad <xref:System.ServiceModel.Dispatcher.ClientRuntime.Operations%2A> obtiene una colección de objetos <xref:System.ServiceModel.Dispatcher.ClientOperation> a la que puede agregar interceptores de mensajes personalizados que proporcionan funcionalidad específica a los mensajes de esa operación.  
  
-   La propiedad <xref:System.ServiceModel.Dispatcher.ClientRuntime.ManualAddressing%2A> permite a una aplicación desactivar algunos encabezados de direccionamiento automáticos para controlar directamente el direccionamiento.  
  
-   La propiedad <xref:System.ServiceModel.Dispatcher.ClientRuntime.Via%2A> establece el valor del destino del mensaje en el nivel de transporte para admitir intermediarios y otros escenarios.  
  
-   El <xref:System.ServiceModel.Dispatcher.ClientRuntime.MessageInspectors%2A> propiedad obtiene una colección de <xref:System.ServiceModel.Dispatcher.IClientMessageInspector> objetos a los que puede agregar interceptores de mensajes personalizados para todos los mensajes que se transmiten a través de un cliente de WCF.  
  
 Además, hay varias propiedades que recuperan la información del contrato:  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractName%2A>  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractNamespace%2A>  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractClientType%2A>  
  
 Si el cliente WCF es un cliente WCF dúplex, las propiedades siguientes también recuperan la información de cliente WCF de devolución de llamada:  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackClientType%2A>  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackDispatchRuntime%2A>  
  
 Para extender la ejecución del cliente WCF a través de un cliente WCF todo, revise las propiedades disponibles en la <xref:System.ServiceModel.Dispatcher.ClientRuntime> clase para ver si modificando una propiedad o implementando una interfaz y agregándola a una propiedad crean la funcionalidad que está buscando. Una vez que haya elegido una extensión determinada que desea crear, inserte su extensión en la propiedad <xref:System.ServiceModel.Dispatcher.ClientRuntime> adecuada implementando un comportamiento de cliente que proporciona el acceso a la clase <xref:System.ServiceModel.Dispatcher.ClientRuntime> cuando se invoca.  
  
 Puede insertar los objetos de extensión personalizados en una colección utilizando un comportamiento de la operación (un objeto que implementa <xref:System.ServiceModel.Description.IOperationBehavior>), un comportamiento del contrato (un objeto que implementa <xref:System.ServiceModel.Description.IContractBehavior>) o un comportamiento del extremo (un objeto que implementa <xref:System.ServiceModel.Description.IEndpointBehavior>). El objeto de comportamiento de instalación se agrega mediante programación a la colección adecuada de comportamientos, mediante declaración (implementando un atributo personalizado) o implementando un objeto <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> personalizado para permitir insertar el comportamiento con un archivo de configuración de la aplicación. Para obtener más información, consulte [configuración y al ampliar el tiempo de ejecución con comportamientos](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md).  
  
 Para obtener ejemplos que muestran la interceptación a través de un cliente de WCF, vea [Cómo: inspeccionar o modificar mensajes en el cliente](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-messages-on-the-client.md).  
  
### <a name="using-the-clientoperation-class"></a>Uso de la clase ClientOperation  
 La clase <xref:System.ServiceModel.Dispatcher.ClientOperation> es la ubicación para las modificaciones del cliente en tiempo de ejecución y el punto de inserción para las extensiones personalizadas cuyo ámbito es solo una operación de servicio. (Para modificar el comportamiento del tiempo de ejecución del cliente para todos los mensajes de un contrato, use la clase <xref:System.ServiceModel.Dispatcher.ClientRuntime>.)  
  
 Use la propiedad <xref:System.ServiceModel.Dispatcher.ClientRuntime.Operations%2A> para buscar el objeto <xref:System.ServiceModel.Dispatcher.ClientOperation> que representa una operación de servicio determinada. Las propiedades siguientes le permiten insertar objetos personalizados en el sistema de cliente WCF:  
  
-   Use la propiedad <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A> para insertar una implementación personalizada de <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> para una operación o modificar el formateador actual.  
  
-   Use la propiedad <xref:System.ServiceModel.Dispatcher.ClientOperation.ParameterInspectors%2A> para insertar una implementación personalizada de <xref:System.ServiceModel.Dispatcher.IParameterInspector> o modificar la actual.  
  
 Las propiedades siguientes le permiten modificar el sistema interactuando con el formateador y los inspectores de parámetro personalizados:  
  
-   Use la propiedad <xref:System.ServiceModel.Dispatcher.ClientOperation.SerializeRequest%2A> para controlar la serialización de un mensaje saliente.  
  
-   Use la propiedad <xref:System.ServiceModel.Dispatcher.ClientOperation.DeserializeReply%2A> para controlar la deserialización de un mensaje entrante.  
  
-   Utilice la propiedad <xref:System.ServiceModel.Dispatcher.ClientOperation.Action%2A> para controlar la acción de WS-Addressing del mensaje de solicitud.  
  
-   Use la <xref:System.ServiceModel.Dispatcher.ClientOperation.BeginMethod%2A> y <xref:System.ServiceModel.Dispatcher.ClientOperation.EndMethod%2A> para especificar qué métodos de cliente WCF están asociados con una operación asincrónica.  
  
-   Use la propiedad <xref:System.ServiceModel.Dispatcher.ClientOperation.FaultContractInfos%2A> para obtener una colección que contiene los tipos que pueden aparecer en errores de SOAP como tipo de detalle.  
  
-   Use las propiedades <xref:System.ServiceModel.Dispatcher.ClientOperation.IsInitiating%2A> y <xref:System.ServiceModel.Dispatcher.ClientOperation.IsTerminating%2A> para controlar si una sesión se inicia o se anula, respectivamente, cuando se llama a la operación.  
  
-   Utilice la propiedad <xref:System.ServiceModel.Dispatcher.ClientOperation.IsOneWay%2A> para controlar si la operación es unidireccional.  
  
-   Use la propiedad <xref:System.ServiceModel.Dispatcher.ClientOperation.Parent%2A> para obtener el objeto <xref:System.ServiceModel.Dispatcher.ClientRuntime> contenedor.  
  
-   Use la propiedad <xref:System.ServiceModel.Dispatcher.ClientOperation.Name%2A> para obtener el nombre de la operación.  
  
-   Use la propiedad <xref:System.ServiceModel.Dispatcher.ClientOperation.SyncMethod%2A> para controlar qué método se asigna a la operación.  
  
 Para extender la ejecución de cliente WCF a través de solo una operación de servicio, revise las propiedades disponibles en la <xref:System.ServiceModel.Dispatcher.ClientOperation> clase para ver si modificando una propiedad o implementando una interfaz y agregándola a una propiedad crean la funcionalidad que está buscando. Una vez que haya elegido una extensión determinada que desea crear, inserte su extensión en la propiedad <xref:System.ServiceModel.Dispatcher.ClientOperation> adecuada implementando un comportamiento de cliente que proporciona el acceso a la clase <xref:System.ServiceModel.Dispatcher.ClientOperation> cuando se invoca. Dentro de ese comportamiento, podrá modificar a continuación la propiedad <xref:System.ServiceModel.Dispatcher.ClientRuntime> para ajustarse a sus requisitos.  
  
 Normalmente, implementar un comportamiento de la operación (un objeto que implementa la interfaz <xref:System.ServiceModel.Description.IOperationBehavior>) es suficiente, pero también puede utilizar comportamientos del extremo y del contrato para lograr lo mismo buscando <xref:System.ServiceModel.Description.OperationDescription> para una operación determinada y adjuntando allí el comportamiento. Para obtener más información, consulte [configuración y al ampliar el tiempo de ejecución con comportamientos](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md).  
  
 Para utilizar su comportamiento personalizado de la configuración, instale el comportamiento mediante un controlador de la sección de configuración de comportamiento personalizado. También puede instalar su comportamiento creando un atributo personalizado.  
  
 Para obtener ejemplos que muestran la interceptación a través de un cliente de WCF, vea [Cómo: inspeccionar o modificar parámetros](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-parameters.md).  
  
## <a name="see-also"></a>Vea también  
 <xref:System.ServiceModel.Dispatcher.ClientRuntime>  
 <xref:System.ServiceModel.Dispatcher.ClientOperation>  
 [Inspección o modificación de mensajes en el cliente](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-messages-on-the-client.md)  
 [Inspección o modificación de parámetros](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-parameters.md)
