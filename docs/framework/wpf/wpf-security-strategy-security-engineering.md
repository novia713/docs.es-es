---
title: 'Estrategia de seguridad de WPF: Ingeniería de seguridad'
ms.date: 03/30/2017
helpviewer_keywords:
- security [WPF], testing techniques
- Security Development Lifecycle (SDL), security analysis [WPF]
- Security Development Lifecycle (SDL), threat modeling
- Security Development Lifecycle (SDL), testing techniques
- Security Development Lifecycle (SDL), source analysis tools
- Security Development Lifecycle (SDL), critical code management
- threat modeling [WPF]
ms.assetid: 0fc04394-4e47-49ca-b0cf-8cd1161d95b9
ms.openlocfilehash: fd29696d88eba5c1363464334b63cb2ab0df4a0e
ms.sourcegitcommit: 5bbfe34a9a14e4ccb22367e57b57585c208cf757
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2018
ms.locfileid: "45698554"
---
# <a name="wpf-security-strategy---security-engineering"></a>Estrategia de seguridad de WPF: Ingeniería de seguridad
Trustworthy Computing es una iniciativa de Microsoft para garantizar la producción de código seguro. Un elemento clave de la iniciativa Trustworthy Computing es [!INCLUDE[TLA#tla_sdl](../../../includes/tlasharptla-sdl-md.md)]. [!INCLUDE[TLA2#tla_sdl](../../../includes/tla2sharptla-sdl-md.md)] es un procedimiento de ingeniería que se usa junto con procesos de ingeniería estándar para facilitar la distribución de código seguro. [!INCLUDE[TLA2#tla_sdl](../../../includes/tla2sharptla-sdl-md.md)] consta de diez fases en las que se combinan prácticas recomendadas con formalización, mensurabilidad y una estructura adicional, que incluye:  
  
-   Análisis del diseño de seguridad  
  
-   Comprobaciones de calidad basadas en herramientas  
  
-   Pruebas de penetración  
  
-   Revisión final de la seguridad  
  
-   Administración de la seguridad del producto después de su lanzamiento  
  
## <a name="wpf-specifics"></a>Especificaciones de WPF  
 El equipo de ingenieros de [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] aplica y extiende [!INCLUDE[TLA2#tla_sdl](../../../includes/tla2sharptla-sdl-md.md)], y esta combinación incluye los siguientes aspectos claves:  
  
 [Modelo de amenazas](#threat_modeling)  
  
 [Herramientas de edición y análisis de la seguridad](#tools)  
  
 [Técnicas de pruebas](#techniques)  
  
 [Administración de código crítico](#critical_code)  
  
<a name="threat_modeling"></a>   
### <a name="threat-modeling"></a>Modelo de amenazas  
 El modelado de amenazas es un componente básico de [!INCLUDE[TLA2#tla_sdl](../../../includes/tla2sharptla-sdl-md.md)], y se usa para generar perfiles de un sistema con el fin de determinar las posibles vulnerabilidades de seguridad. Una vez identificadas las vulnerabilidades, el modelado de amenazas también garantiza que se tomen las medidas oportunas.  
  
 De forma general, el modelado de amenazas conlleva los siguientes pasos principales, usando una tienda de comestibles como ejemplo:  
  
1.  **Identificar los activos**. Entre los activos de una tienda de comestibles se pueden incluir los empleados, una caja de seguridad, las cajas registradoras y el inventario.  
  
2.  **Enumerar los puntos de entrada**. Los puntos de entrada de una tienda de comestibles podrían ser las puertas delantera y trasera, las ventanas, el muelle de carga y el sistema de aire acondicionado.  
  
3.  **Investigar ataques contra activos mediante los puntos de entrada**. Un posible ataque podría dirigirse al activo *caja de seguridad* de la tienda de comestibles a través del punto de entrada *aire acondicionado*; el sistema de aire acondicionado puede desatornillarse para poder sacar la caja de seguridad a través de él.  
  
 El modelado de amenazas se aplica en todo [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] e incluye lo siguiente:  
  
-   Cómo el analizador de [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] lee los archivos, asigna el texto a las clases de modelo de objetos correspondiente y crea el código real.  
  
-   Cómo se crea un identificador de ventana (hWnd), cómo envía los mensajes y cómo se usa para representar el contenido de una ventana.  
  
-   Cómo el enlace de datos obtiene los recursos e interactúa con el sistema.  
  
 Estos modelos de amenazas son importantes para identificar los requisitos de diseño de seguridad y reducir las amenazas durante el proceso de desarrollo.  
  
<a name="tools"></a>   
### <a name="source-analysis-and-editing-tools"></a>Análisis de código fuente y herramientas de edición  
 Además de los elementos manuales de revisión del código de seguridad de [!INCLUDE[TLA2#tla_sdl](../../../includes/tla2sharptla-sdl-md.md)], el equipo de [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] usa varias herramientas para realizar análisis del código fuente y las modificaciones asociadas para reducir las vulnerabilidades de seguridad. Se usa una amplia variedad de herramientas de código fuente, entre ellas:  
  
-   **FXCop**: busca problemas de seguridad comunes en código administrado, que van desde reglas de herencia hasta el uso de la seguridad de acceso del código para interoperar de forma segura con código no administrado. Consulte [FXCop](http://www.gotdotnet.com/team/fxcop/).  
  
-   **Prefix/Prefast**: busca vulnerabilidades de seguridad y problemas de seguridad comunes en código no administrado, como la saturación de búferes, los problemas de cadenas de formato y la comprobación de errores.  
  
-   **API prohibidas**: busca código fuente para identificar el uso accidental de funciones que se sabe que producen problemas de seguridad, como `strcpy`. Una vez identificadas, estas funciones se reemplazan por alternativas más seguras.  
  
<a name="techniques"></a>   
### <a name="testing-techniques"></a>Técnicas de pruebas  
 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] usa diferentes técnicas de pruebas de seguridad, entre las que se incluyen:  
  
-   **Pruebas de caja blanca**: los evaluadores ven el código fuente y, a continuación, generan pruebas de explotación.  
  
-   **Pruebas de caja negra**: los evaluadores intentan encontrar vulnerabilidades de seguridad examinando la API y las características y, después, intentan atacar el producto.  
  
-   **Regresiones de problemas de seguridad de otros productos**: cuando procede, se prueban problemas de seguridad de productos relacionados. Por ejemplo, se han identificado variantes de unos sesenta problemas de seguridad para [!INCLUDE[TLA2#tla_ie](../../../includes/tla2sharptla-ie-md.md)] y se ha probado su aplicabilidad a [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)].  
  
-   **Pruebas de penetración basadas en herramientas mediante datos aleatorios**: las pruebas de exploración de vulnerabilidades mediante datos aleatorios consisten en explotar el intervalo de entrada de un lector de archivos mediante diferentes entradas. Un ejemplo del uso de esta técnica en [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] es la comprobación de errores en código de descodificación de imágenes.  
  
<a name="critical_code"></a>   
### <a name="critical-code-management"></a>Administración de código crítico  
 Para [!INCLUDE[TLA#tla_xbap#plural](../../../includes/tlasharptla-xbapsharpplural-md.md)], [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] crea un recinto de seguridad usando la compatibilidad de .NET Framework para marcar y seguimiento del código crítico para la seguridad que eleva los privilegios (consulte **metodología crítica para la seguridad** en [WPF Estrategia de seguridad: seguridad de la plataforma](../../../docs/framework/wpf/wpf-security-strategy-platform-security.md)). Dados los requisitos de calidad de alta seguridad del código crítico para la seguridad, este código recibe un nivel adicional de auditoría de seguridad y control de administración de código fuente. Aproximadamente del 5% al 10% de [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] se compone de código crítico para la seguridad, que es revisado por un equipo de revisión específico. Para administrar el código fuente y el proceso de inserción en el repositorio, se realiza el seguimiento del código crítico para la seguridad y se asigna cada entidad crítica (es decir, un método que contiene código crítico) a su estado de autorización. El estado de autorización incluye los nombres de uno o varios revisores. Cada compilación diaria de [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] compara el código crítico con el de compilaciones anteriores para comprobar si hay cambios no aprobados. Si un ingeniero modifica código crítico sin la aprobación del equipo de revisión, se identifica y se corrige inmediatamente. Este proceso permite la aplicación y el mantenimiento de un nivel especialmente alto de control sobre el código en espacio aislado de [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Seguridad](../../../docs/framework/wpf/security-wpf.md)  
 [Seguridad de confianza parcial de WPF](../../../docs/framework/wpf/wpf-partial-trust-security.md)  
 [Estrategia de seguridad de WPF: Seguridad de plataforma](../../../docs/framework/wpf/wpf-security-strategy-platform-security.md)  
 [Informática de confianza](https://www.microsoft.com/mscorp/twc/default.mspx)  
 [Modelado de amenazas de aplicación](https://msdn.microsoft.com/security/securecode/threatmodeling/acetm/)  
 [Directrices de seguridad: .NET Framework 2.0](https://msdn.microsoft.com/library/default.asp?url=/library/dnpag2/html/PAGGuidelines0003.asp)
