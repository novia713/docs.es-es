---
title: Uso de extremos estándar
ms.date: 03/30/2017
ms.assetid: ecd6a62f-9619-4778-a497-6f888087a9ea
ms.openlocfilehash: b3e8cb32832763c7182f86f68c5c80d80ce8c3af
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43518231"
---
# <a name="usage-of-standard-endpoints"></a>Uso de extremos estándar

Este ejemplo muestra cómo utilizar los puntos de conexión estándar en archivos de configuración de servicio. Un extremo estándar permite al usuario simplificar las definiciones de extremo utilizando una sola propiedad para describir una dirección, enlace y combinación de contratos con propiedades adicionales asocias. En este ejemplo se muestra cómo definir e implementar un extremo estándar personalizado y cómo definir propiedades concretas en él.

## <a name="sample-details"></a>Detalles del ejemplo

Los extremos de servicio se pueden especificar proporcionando tres parámetros: dirección, enlace y contrato. Otros parámetros que se pueden proporcionar son la configuración de comportamiento, los encabezados, el URI de escucha, etc. En algunos casos, con una dirección o con todas, los enlaces y contratos tienen valores que no pueden cambiar. Por esta razón, es posible utilizar extremos estándar. Algunos ejemplos de tales extremos incluyen los de intercambio de metadatos y los de detección. Los extremos estándar también mejoran la capacidad de uso al permitir la configuración de los extremos de servicio sin tener que proporcionar información de naturaleza fija o crear sus propios extremos estándar, por ejemplo proporcionando un conjunto razonable de valores predeterminados y, por tanto, reduciendo el nivel de detalle de los archivos de configuración.

Este ejemplo está compuesto de dos proyectos: el servicio que define dos extremos estándar y el cliente que comunica con el servicio. La manera en que los extremos estándar se definen para el servicio en el archivo de configuración se muestra en el siguiente ejemplo.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <extensions>
      <endpointExtensions>
        <add name="customEndpoint" type="Microsoft.Samples.StandardEndpoints.CustomEndpointCollectionElement, service" />
      </endpointExtensions>
    </extensions>
    <services>
      <service name="Microsoft.Samples.StandardEndpoints.CalculatorService">
        <endpoint address="http://localhost:8000/Samples/Service.svc/customEndpoint" contract="Microsoft.Samples.StandardEndpoints.ICalculator" kind="customEndpoint" />
        <endpoint kind="mexEndpoint" />
      </service>
    </services>
    <behaviors>
      <serviceBehaviors>
        <behavior>
          <serviceMetadata httpGetEnabled="True"/>
        </behavior>
      </serviceBehaviors>
    </behaviors>
    <standardEndpoints>
      <customEndpoint>
        <standardEndpoint property="True" />
      </customEndpoint>
    </standardEndpoints>
  </system.serviceModel>
</configuration>
```

El primer extremo definido para el servicio es de tipo `customEndpoint`, cuya definición se puede ver en la sección `<standardEndpoints>`, en la que la propiedad `property` recibe el valor `true`. Este es el caso de un extremo personalizado con una nueva propiedad. El segundo extremo corresponde a un extremo de metadatos en el que los valores de la dirección, el enlace y el contrato son fijos.

Para definir el elemento de extremo estándar, se debe crear una clase que se derive de `StandardEndpointElement`. En el caso de este ejemplo, la clase `CustomEndpointElement` se ha definido como se muestra en el siguiente ejemplo.

```csharp
public class CustomEndpointElement : StandardEndpointElement
{
    public bool Property
    {
        get { return (bool)base["property"]; }
        set { base["property"] = value; }
    }

    protected override ConfigurationPropertyCollection Properties
    {
        get
        {
            ConfigurationPropertyCollection properties = base.Properties;
            properties.Add(new ConfigurationProperty("property", typeof(bool), false, ConfigurationPropertyOptions.None));
            return properties;
        }
    }

    protected override Type EndpointType
    {
        get { return typeof(CustomEndpoint); }
    }

    protected override ServiceEndpoint CreateServiceEndpoint(ContractDescription contract)
    {
        return new CustomEndpoint();
    }

    protected override void OnApplyConfiguration(ServiceEndpoint endpoint, ServiceEndpointElement serviceEndpointElement)
    {
        CustomEndpoint customEndpoint = (CustomEndpoint)endpoint;
        customEndpoint.Property = this.Property;
    }

    protected override void OnApplyConfiguration(ServiceEndpoint endpoint, ChannelEndpointElement channelEndpointElement)
    {
        CustomEndpoint customEndpoint = (CustomEndpoint)endpoint;
        customEndpoint.Property = this.Property;
    }

    protected override void OnInitializeAndValidate(ServiceEndpointElement serviceEndpointElement)
    {
    }

    protected override void OnInitializeAndValidate(ChannelEndpointElement channelEndpointElement)
    {
    }
}
```

En la función `CreateServiceEndpoint`, se crea un objeto `CustomEndpoint`. Su definición se muestra en el ejemplo siguiente:

```csharp
public class CustomEndpoint : ServiceEndpoint
{
    public CustomEndpoint() 
        : this(string.Empty)
    {
    }

    public CustomEndpoint(string address)
        : this(address, ContractDescription.GetContract(typeof(ICalculator)))
    {
    }

    public CustomEndpoint(string address, ContractDescription contract)
        : base(contract)
    {
        this.Binding = new BasicHttpBinding();
        this.IsSystemEndpoint = false;
    }

    public bool Property
    {
        get;
        set;
    }
}
```

 Para realizar la comunicación entre el servicio y el cliente, se crea una referencia del servicio en el cliente para el servicio. Cuando el ejemplo se compila y ejecuta, el servicio se ejecuta y el cliente se comunica con él. Observe que la referencia del servicio debería actualizarse cada vez que hay algún cambio en el servicio.

#### <a name="to-use-this-sample"></a>Para utilizar este ejemplo

1.  Mediante [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)], abra el archivo StandardEndpoints.sln.

2.  Habilite varios proyectos para iniciarse.

    1.  En **el Explorador de soluciones**, haga clic en la solución de puntos de conexión estándar y, a continuación, seleccione **propiedades**.

    2.  En **propiedades comunes**, seleccione **proyecto de inicio**y, a continuación, haga clic en **varios proyectos de inicio**.

    3.  Mueva el proyecto de servicio al principio de la lista, con el **acción** establecido en **iniciar**.

    4.  Mueva el proyecto cliente después del proyecto de servicio, también con la **acción** establecido en **iniciar**.

         De esta forma se especifica que el proyecto Cliente se ejecute después del proyecto Servicio.

3.  Presione F5 para ejecutar la solución.

> [!NOTE]
> Si estos pasos no funcionan, asegúrese de que el entorno ha se ha establecido correctamente, mediante los siguientes pasos:
>
> 1. Asegúrese de que ha realizado la [procedimiento de instalación de un solo uso para los ejemplos de Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).
> 2. Para compilar la solución, siga las instrucciones de [compilar los ejemplos de Windows Communication Foundation](building-the-samples.md).
> 3. Para ejecutar el ejemplo en una o varias configuraciones de equipo, siga las instrucciones de [ejecutando los ejemplos de Windows Communication Foundation](running-the-samples.md).

> [!IMPORTANT]
> Puede que los ejemplos ya estén instalados en su equipo. Compruebe el siguiente directorio (predeterminado) antes de continuar.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Si no existe este directorio, vaya a [Windows Communication Foundation (WCF) y Windows Workflow Foundation (WF) Samples para .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los Windows Communication Foundation (WCF) y [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ejemplos. Este ejemplo se encuentra en el siguiente directorio.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\StandardEndpoints`
