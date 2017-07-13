---
title: "Contadores de rendimiento de WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contadores de rendimiento [WCF]"
ms.assetid: f559b2bd-ed83-4988-97a1-e88f06646609
caps.latest.revision: 37
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 37
---
# Contadores de rendimiento de WCF
[!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] incluye un conjunto grande de contadores de rendimiento para ayudarle a calibrar el rendimiento de su aplicación.  
  
## Habilitación de contadores de rendimiento  
 Puede habilitar contadores de rendimiento para un servicio [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] a través del archivo de configuración app.config del servicio [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)], como se indica a continuación:  
  
```  
<configuration>  
    <system.serviceModel>  
        <diagnostics performanceCounters="All" />  
    </system.serviceModel>  
</configuration>  
```  
  
 Puede establecer el atributo `performanceCounters` para habilitar un tipo específico de contadores de rendimiento.  Los valores válidos son  
  
-   All: todos los contadores de categoría \(ServiceModelService, ServiceModelEndpoint y ServiceModelOperation\) están habilitados.  
  
-   ServiceOnly: solo se habilitan los contadores de categoría ServiceModelService.  Este es el valor predeterminado.  
  
-   Off: los contadores de rendimiento ServiceModel\* están deshabilitados.  
  
 Si desea habilitar los contadores de rendimiento para todas las aplicaciones de [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)], incluya los parámetros de configuración en el archivo Machine.config.  Para obtener más información sobre cómo configurar memoria suficiente para los contadores de rendimiento de la máquina, vea la sección **Aumento del tamaño de la memoria para los contadores de rendimiento**.  
  
 Si utiliza puntos de extensibilidad de [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)], como invocadores de operación personalizados, también debe emitir sus propios contadores de rendimiento.  Esto se debe a que, si implementa un punto de extensibilidad, [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] quizá no pueda emitir los datos de contador de rendimiento estándar en la ruta de acceso predeterminada.  Si no implementa la compatibilidad con el contador de rendimiento manual, puede que no vea los datos de contador de rendimiento que espera.  
  
 Además, puede habilitar los contadores de rendimiento en el código de la siguiente forma,  
  
```  
using System.Configuration;  
using System.ServiceModel.Configuration;  
using System.ServiceModel.Diagnostics;  
Configuration config = ConfigurationManager.OpenExeConfiguration(  
    ConfigurationUserLevel.None);  
ServiceModelSectionGroup sg = ServiceModelSectionGroup.GetSectionGroup(config);  
sg.Diagnostic.PerformanceCounters = PerformanceCounterScope.All;  
config.Save();  
```  
  
## Ver los datos de rendimiento  
 Para ver los datos capturados por los contadores de rendimiento, utilice el monitor de rendimiento \(Perfmon.exe\) incluido en Windows.  Para iniciar esta herramienta vaya a **Inicio**, haga clic en **Ejecutar** y escriba `perfmon.exe` en el cuadro de diálogo.  
  
> [!NOTE]
>  Se pueden lanzar instancias del contador de rendimiento antes de que el distribuidor del extremo haya procesado los últimos mensajes.  Esto puede dar lugar a que no se capturen los datos de rendimiento de algunos mensajes.  
  
## Aumento del tamaño de la memoria para los contadores de rendimiento  
 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] utiliza la memoria compartida independiente para sus categorías de contador de rendimiento.  
  
 De forma predeterminada, la memoria compartida independiente se establece en un cuarto del tamaño de la memoria global del contador de rendimiento.  La memoria global del contador de rendimiento predeterminada es 524.288 bytes.  Por lo tanto, las tres categorías de contador de rendimiento [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] tienen un tamaño predeterminado de aproximadamente 128KB cada una.  Dependiendo de las características del tiempo de ejecución de las aplicaciones [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] de un equipo, es posible agotar la memoria del contador de rendimiento.  Cuando esto ocurre, [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] escribe un error en el registro de eventos de la aplicación.  El contenido del error indica que no se cargó un contador de rendimiento, y la entrada contiene la excepción "System.InvalidOperationException: Memoria insuficiente para la vista personaliza del archivo de contadores". Si se habilita la traza en el nivel de error, también se sigue la traza del error.  Si se agota la memoria del contador de rendimiento y continúan ejecutándose las aplicaciones [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] con los contadores de rendimiento habilitados, podría degradarse el rendimiento.  Si es administrador de la máquina, configúrela y asigne memoria suficiente para admitir el número máximo de contadores de rendimiento que puedan existir en cualquier momento.  
  
 Puede cambiar la cantidad de memoria del contador de rendimiento para las categorías de [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] del registro.  Para cambiarla, es necesario agregar un nuevo valor DWORD, denominado `FileMappingSize`, a las tres ubicaciones siguientes y establecerlo en el valor en bytes deseado.  Reinicie su equipo para que estos cambios se hagan efectivos.  
  
-   HKLM\\System\\CurrentControlSet\\Services\\ServiceModelEndpoint 4.0.0.0\\Performance  
  
-   HKLM\\System\\CurrentControlSet\\Services\\ServiceModelOperation 4.0.0.0\\Performance  
  
-   HKLM\\System\\CurrentControlSet\\Services\\ServiceModelService 4.0.0.0\\Performance  
  
 Cuando se elimina un número importante de objetos \(por ejemplo, ServiceHost\) pero se espera recopilar los elementos no usados, el contador de rendimiento `PrivateBytes` registra un número excepcionalmente alto.  Para solucionar este problema, puede agregar sus propios contadores específicos de la aplicación, o utilizar el atributo `performanceCounters` para habilitar solo los contadores del nivel de servicio.  
  
## Tipos de contadores de rendimiento  
 Los contadores de rendimiento abarcan tres niveles diferentes: servicio, extremo y operación.  
  
 Puede utilizar WMI para recuperar el nombre de una instancia del contador de rendimiento.  Por ejemplo,  
  
-   Puede obtener el nombre de una instancia del contador de servicio a través de la propiedad “CounterInstanceName” de la instancia de WMI [Servicio](../../../../../docs/framework/wcf/diagnostics/wmi/service.md).  
  
-   Puede obtenerse el nombre de una instancia del contador de extremo a través de la propiedad “CounterInstanceName” de la instancia de WMI [Extremo](../../../../../docs/framework/wcf/diagnostics/wmi/endpoint.md).  
  
-   Puede obtener el nombre de una instancia de contador de operación a través del método “GetOperationCounterInstanceName” de la instancia de WMI [Extremo](../../../../../docs/framework/wcf/diagnostics/wmi/endpoint.md).  
  
 Para obtener más información acerca de WMI, vea [Utilización del instrumental de administración de Windows \(WMI\) para diagnósticos](../../../../../docs/framework/wcf/diagnostics/wmi/index.md).  
  
### Contadores de rendimiento del servicio  
 Los contadores de rendimiento del servicio miden el conjunto del comportamiento del servicio y se utilizan para diagnosticar el rendimiento de todo el servicio.  Pueden encontrarse en el objeto de rendimiento `ServiceModelService 4.0.0.0` al visualizarlo con el monitor de rendimiento.  Los nombres de las instancias se establecen utilizando el siguiente patrón:  
  
```  
ServiceName@ServiceBaseAddress  
```  
  
 Se agrega un contador a un ámbito del servicio desde el contador de una colección de extremos.  
  
 Los contadores de rendimiento de la creación de una instancia de servicio aumentan cuando se crea un nuevo InstanceContext.  Tenga en cuenta que también se crea un nuevo InstanceContext cuando recibe un mensaje de no activación \(con un servicio existente\), o cuando se conecta a la instancia de una sesión, finaliza la sesión y, a continuación, se vuelve a conectar desde otra sesión.  
  
### Contadores de rendimiento del extremo  
 Los contadores de rendimiento del extremo permiten examinar datos que reflejan la aceptación de los mensajes por un extremo.  Pueden encontrarse en el objeto de rendimiento `ServiceModelEndpoint 4.0.0.0` al visualizarlo mediante el monitor de rendimiento.  Los nombres de las instancias se establecen utilizando el siguiente patrón:  
  
```  
(ServiceName).(ContractName)@(endpoint listener address)  
```  
  
 Los datos son similares a los recopilados para las operaciones individuales, pero solo se agregan a lo largo del extremo.  
  
 Un contador en un ámbito de extremo se agrega desde los contadores de una colección de operaciones.  
  
> [!NOTE]
>  Si dos extremos poseen nombres y direcciones de contrato idénticos, se asignan a la misma instancia del contador.  
  
### Contadores de rendimiento de la operación  
 Los contadores de rendimiento de la operación se encuentran en el objeto de rendimiento `ServiceModelOperation 4.0.0.0` al visualizarlo con el monitor de rendimiento.  Cada operación posee una instancia individual.  Es decir, si un contrato determinado posee 10 operaciones, se asociarán 10 instancias de contador de operación a ese contrato.  Los nombres de las instancias de objeto se establecen utilizando el siguiente patrón:  
  
```  
(ServiceName).(ContractName).(OperationName)@(first endpoint listener address)  
```  
  
 Este contador permite medir la utilización de la llamada y el buen rendimiento de la operación.  
  
 Cuando los contadores son visibles en varios ámbitos, los datos recopilados de un ámbito superior se agregan a los datos de los ámbitos inferiores.  Por ejemplo, `Calls` a un extremo representa la suma de todas las llamadas de la operación en el extremo; `Calls` a un servicio representa la suma de todas las llamadas a todos los extremos del servicio.  
  
> [!NOTE]
>  Si existen nombres de la operación duplicados en un contrato, solo se obtiene una instancia de contador para ambas operaciones.  
  
## Programación de los contadores de rendimiento de WCF  
 Se instalan varios archivos en la carpeta de instalación de SDK de modo que pueda obtenerse acceso a los contadores de rendimiento [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] mediante programación.  Estos archivos se enumeran como se indica a continuación.  
  
-   \_ServiceModelEndpointPerfCounters.vrg  
  
-   \_ServiceModelOperationPerfCounters.vrg  
  
-   \_ServiceModelServicePerfCounters.vrg  
  
-   \_SMSvcHostPerfCounters.vrg  
  
-   \_TransactionBridgePerfCounters.vrg  
  
 Para obtener más información acerca de cómo obtener acceso a los contadores mediante programación, vea [Arquitectura de programación del contador de rendimiento](http://go.microsoft.com/fwlink/?LinkId=95179).  
  
## Vea también  
 [Administración y diagnóstico](../../../../../docs/framework/wcf/diagnostics/index.md)