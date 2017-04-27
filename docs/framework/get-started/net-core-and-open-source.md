---
title: ".NET Core y código abierto | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e6bd4655-ce37-4003-8462-468a6fe2c40f
caps.latest.revision: 8
author: mairaw
ms.author: mairaw
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 54bade1b6e310db37537102a1625a76e11e136a7
ms.lasthandoff: 04/18/2017

---
# <a name="net-core-and-open-source"></a>.NET Core y código abierto
En este tema se proporciona una breve descripción de .NET Core y se muestra cómo encontrar más información. Para encontrar la lista completa de temas de .NET Core, visite el [sitio de documentación de .NET Core](https://docs.microsoft.com/en-us/dotnet/articles/core/index).  
  
<a name="BKMK_WhatisNETCore"></a>   
## <a name="what-is-net-core"></a>¿Qué es .NET Core?  
 .NET Core es una implementación de .NET Platform para uso general, modular, multiplataforma y de código abierto. Contiene muchas de las API de .NET Framework (aunque .NET Core es un conjunto más pequeño), e incluye componentes de entorno en tiempo de ejecución, framework, compilador y herramientas que admiten una variedad de sistemas operativos y destinos de chip. La implementación de .NET Core se debe principalmente a las cargas de trabajo de ASP.NET Core, pero también a la necesidad y la intención de tener un entorno en tiempo de ejecución más moderno. Se puede utilizar en escenarios de dispositivos, nube e incrustados/IoT.  
  
 Para empezar a conocer .NET Core, visite la [página principal de .NET Core](https://www.microsoft.com/net/core).  
  
 Estas son las principales características de .NET Core:  
  
-   **Multiplataforma**: .NET Core proporciona una funcionalidad clave para implementar las características de la aplicación que necesita y reutilizar este código independientemente del destino de la plataforma. En estos momentos, es compatible con los principales sistemas operativos (SO): Windows, Linux y macOS. Puede escribir aplicaciones y bibliotecas que se ejecutan sin modificaciones en todos los sistemas operativos compatibles. Para ver una lista de todos los sistemas operativos compatibles, visite [.NET Core roadmap](https://github.com/dotnet/core/blob/master/roadmap.md) (Mapa de ruta de .NET Core).  
  
-   **Código abierto**: .NET Core es uno de los muchos proyectos que administra [.NET Foundation](http://www.dotnetfoundation.org/) y está disponible en [GitHub](https://github.com/).  Al tratarse de un proyecto de código abierto, .NET Core favorece que el proceso de desarrollo sea más transparente y que exista una comunidad activa y comprometida.  
  
-   **Desarrollo flexible**: hay dos modos principalmente para desarrollar una aplicación, implementación basada en marco e implementación autocontenida. Con la implementación basada en marco, solo se instalan su aplicación y las dependencias de terceros, y la aplicación requiere la presencia de una versión de .NET Core en todo el sistema.  Con la implementación autocontenida, la versión de .NET Core que se utiliza para compilar su aplicación también se implementa junto con la aplicación y las dependencias de terceros, y se puede ejecutar paralelamente con otras versiones.    Para obtener más información, consulte el tema [Implementación de aplicaciones .NET Core](https://docs.microsoft.com/en-us/dotnet/articles/core/deploying/index).  
  
-   **Modular**: .NET Core es modular, ya que se publica a través de NuGet en paquetes de ensamblado más reducidos. En lugar de un ensamblado grande que contiene la mayor parte de la funcionalidad básica, .NET Core está disponible como paquetes más pequeños centrados en las características. Esta característica nos permite un modelo de desarrollo más ágil y le permite optimizar su aplicación para incluir solo los paquetes de NuGet que necesita. Entre las ventajas de una menor superficie de aplicación se incluyen una mayor seguridad, mantenimiento reducido, rendimiento mejorado y menores costes en un modelo de suscripción ajustado a sus necesidades.  
  
## <a name="the-net-core-platform"></a>Plataforma .NET Core  
 La plataforma .NET Core está formada por varios componentes, entre los que se incluyen los compiladores administrados, el entorno en tiempo de ejecución, las bibliotecas de clases base y numerosos modelos de aplicaciones, como ASP.NET Core. Puede obtener más información sobre los diferentes componentes y colaborar visitando los siguientes repositorios de [GitHub](https://github.com/):  
  
-   [Núcleo de .NET](https://github.com/dotnet/core)  
  
-   [CoreFX: bibliotecas fundamentales de .NET Core](https://github.com/dotnet/corefx)  
  
-   [CoreCLR: .NET Core runtime](https://github.com/dotnet/coreclr)  
  
-   [CLI: Herramientas de la interfaz de la línea de comandos de .NET Core](https://github.com/dotnet/cli)  
  
-   [Roslyn: SDK de .NET Compiler Platform](https://github.com/dotnet/roslyn)  
  
-   [ASP.NET Core](https://github.com/aspnet/home)  
  
## <a name="see-also"></a>Vea también  
 [Página principal de .NET Core](https://www.microsoft.com/net/core)   
 [Sitio de documentación de .NET Core](https://docs.microsoft.com/en-us/dotnet/articles/core/index)   
 [Documentación de ASP.NET Core](https://docs.asp.net/)