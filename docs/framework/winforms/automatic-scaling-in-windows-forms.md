---
title: "Automatic Scaling in Windows Forms | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "scalability, automatic in Windows Forms"
  - "Windows Forms, automatic scaling"
ms.assetid: 68fad25b-afbc-44bd-8e1b-966fc43507a4
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Automatic Scaling in Windows Forms
El escalado automático permite que un formulario y sus respectivos controles, diseñados en una máquina con una determinada resolución de pantalla o fuente del sistema, se muestren correctamente en otra máquina con una resolución de pantalla o una fuente de sistema diferentes.  El escalado automático garantiza que el formulario y sus controles cambien de tamaño para mantener la coherencia con las ventanas nativas y otras aplicaciones tanto en máquinas de los usuarios como en las de otros desarrolladores.  La compatibilidad de [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] con el escalado automático y los estilos visuales permite que las aplicaciones de [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] mantengan una apariencia coherente en comparación con aplicaciones Windows nativas en cada equipo de usuario.  
  
## Necesidad de escalado automático  
 Sin escalado automático, una aplicación diseñada para una fuente o una resolución de pantalla aparecerá demasiado pequeña o demasiado grande cuando se cambie la fuente o la resolución.  Por ejemplo, si la aplicación está diseñada con Tahoma de 9 puntos como línea base, sin el ajuste aparecerá demasiado pequeña si se ejecuta en una máquina donde la fuente de sistema sea Tahoma de 12 puntos.  Los elementos de texto, como títulos, menús, el contenido de cuadros de texto, etc. se representarán más pequeños que en otras aplicaciones.  Además, el tamaño de los elementos de interfaz de usuario \(UI\) que contienen texto —como la barra de título, los menús y muchos controles— depende de la fuente usada.  En este ejemplo, estos elementos también aparecerán relativamente más pequeños.  
  
 Una situación análoga se produce cuando se diseña una aplicación para una determinada resolución de pantalla.  La resolución de pantalla más común es 96 puntos por pulgada \(PPP\), pero cada vez son más comunes las pantallas de resolución superior que admiten 120, 133, 170 y otras mayores.  Si no se ajusta la escala de una aplicación diseñada para una resolución —especialmente si se trata de una aplicación basada en gráficos—, dicha aplicación se verá demasiado grande o demasiado pequeña cuando se ejecute a otra resolución.  
  
 El escalado automático busca mejorar estos problemas con un cambio automático el tamaño del formulario y de sus controles secundarios, de acuerdo con el tamaño de fuente o la resolución de pantalla relativos.  El sistema operativo Windows admite el escalado automático de cuadros de diálogo mediante una unidad relativa de medida denominada unidades de cuadro de diálogo.  Una unidad de cuadro de diálogo se basa en la fuente del sistema y su relación con los píxeles se puede determinar mediante la función del SDK de Win32 `GetDialogBaseUnits`.  Cuando un usuario cambia el tema usado por Windows, todos los cuadros de diálogo se ajustan automáticamente según corresponda.  Además:  
  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] admite el escalado automático en función de los valores predeterminados de fuente de sistema o resolución de pantalla.  Opcionalmente, el escalado automático se puede deshabilitar en una aplicación.  
  
## Compatibilidad original con escalado automático  
 Las versiones 1.0 y 1.1 de [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] admitían el escalado automático de una manera sencilla que dependía de la fuente predeterminada de Windows usada para la interfaz de usuario, representada por el valor del SDK de Win32 **DEFAULT\_GUI\_FONT**.  Por lo general, esta fuente solo se cambia cuando se modifica la resolución de pantalla.  El mecanismo siguiente se usó para implementar el escalado automático:  
  
1.  En tiempo de diseño, la propiedad <xref:System.Windows.Forms.Form.AutoScaleBaseSize%2A> \(que ahora está en desuso\) se estableció en el alto y ancho de la fuente predeterminada del sistema en la máquina del desarrollador.  
  
2.  En runtime, la fuente predeterminada del sistema de la máquina del usuario se usaba para inicializar la propiedad <xref:System.Windows.Forms.Control.Font%2A> de la clase <xref:System.Windows.Forms.Form>.  
  
3.  Antes de mostrar el formulario, se llamaba al método <xref:System.Windows.Forms.Form.ApplyAutoScaling%2A> para escalar el formulario.  Este método calculaba los tamaños de escala relativa de <xref:System.Windows.Forms.Form.AutoScaleBaseSize%2A> y <xref:System.Windows.Forms.Control.Font%2A> y, a continuación, se llamaba al método <xref:System.Windows.Forms.Control.Scale%2A> para escalar el formulario y sus elementos secundarios.  
  
4.  El valor de <xref:System.Windows.Forms.Form.AutoScaleBaseSize%2A> se actualizaba para que las siguientes llamadas a <xref:System.Windows.Forms.Form.ApplyAutoScaling%2A> no cambiaran progresivamente el tamaño del formulario.  
  
 Aunque este mecanismo era suficiente para la mayoría de los propósitos, sufría las limitaciones siguientes:  
  
-   Puesto que la propiedad <xref:System.Windows.Forms.Form.AutoScaleBaseSize%2A> representaba el tamaño de fuente básico como valores enteros, se producían errores de redondeo que se hacían evidentes cuando un formulario recorría varias resoluciones.  
  
-   El escalado automático se implementó solo en la clase <xref:System.Windows.Forms.Form>, no en la clase <xref:System.Windows.Forms.ContainerControl>.  Como resultado, los controles de usuario solo se escalaban correctamente si el control de usuario estaba diseñado con la misma resolución que el formulario y se colocaba en el formulario en tiempo de diseño.  
  
-   Los formularios y sus controles secundarios solo podían diseñarse de manera simultánea por varios desarrolladores si las resoluciones de sus máquinas eran iguales.  Igualmente, hacía que la herencia de un formulario dependiese de la resolución asociada con el formulario principal.  
  
-   No es compatible con los administradores de diseño más recientes introducidos con [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] versión 2.0, como <xref:System.Windows.Forms.FlowLayoutPanel> y <xref:System.Windows.Forms.TableLayoutPanel>.  
  
-   No admitía el escalado automático basado directamente en la resolución de pantalla necesaria para ser compatible con [!INCLUDE[compact](../../../includes/compact-md.md)].  
  
 Aunque este mecanismo se conserva en [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] versión 2.0 para mantener la compatibilidad con versiones anteriores, se ha sustituido por el mecanismo de escalado más sólido que se describe a continuación.  En consecuencia, <xref:System.Windows.Forms.Form.AutoScale%2A>, <xref:System.Windows.Forms.Form.ApplyAutoScaling%2A>, <xref:System.Windows.Forms.Form.AutoScaleBaseSize%2A> y determinadas sobrecargas <xref:System.Windows.Forms.Control.Scale%2A> están marcadas como obsoletas.  
  
> [!NOTE]
>  Puede eliminar las referencias a estos miembros cuando actualice su código heredado a [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] versión 2.0.  
  
## Compatibilidad actual con escalado automático  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] versión 2.0 supera las limitaciones anteriores gracias a la introducción de los cambios siguientes en el escalado automático de Windows Forms:  
  
-   El soporte básico para el escalado se ha movido a la clase <xref:System.Windows.Forms.ContainerControl> para que los formularios, los controles compuestos nativos y los controles de usuario reciban soporte de escalado uniforme.  Se han agregado los nuevos miembros <xref:System.Windows.Forms.ContainerControl.AutoScaleFactor%2A>, <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A>, <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A> y <xref:System.Windows.Forms.ContainerControl.PerformAutoScale%2A>.  
  
-   La clase <xref:System.Windows.Forms.Control> también tiene varios miembros nuevos que le permiten participar en el escalado y admitir escalado mixto en el mismo formulario.  Concretamente, los miembros <xref:System.Windows.Forms.Control.Scale%2A>, <xref:System.Windows.Forms.Control.ScaleChildren%2A> y <xref:System.Windows.Forms.Control.GetScaledBounds%2A> admiten el escalado.  
  
-   Se ha agregado soporte de escalado basado en la resolución de pantalla para complementar el soporte de fuentes del sistema, tal como se define en la enumeración <xref:System.Windows.Forms.AutoScaleMode>.  Este modo es compatible con el escalado automático admitido por el [!INCLUDE[compact](../../../includes/compact-md.md)], lo que permite una migración de aplicaciones más sencilla.  
  
-   Se ha agregado compatibilidad con administradores de diseño como <xref:System.Windows.Forms.FlowLayoutPanel> y <xref:System.Windows.Forms.TableLayoutPanel> a la implementación del escalado automático.  
  
-   Los factores de escalado se representan ahora como valores de número de punto flotante, normalmente mediante la estructura <xref:System.Drawing.SizeF>, con lo que prácticamente se han eliminado los errores de redondeo.  
  
> [!CAUTION]
>  No se admiten combinaciones arbitrarias de los modos de escalado de DPI y fuente.  Aunque puede escalar sin ningún problema un control de usuario usando un modo \(por ejemplo, DPI\) y colocarlo en un formulario usando otro modo \(Font\), la combinación de un formulario base en un modo y un formulario derivado en otro puede provocar resultados inesperados.  
  
### Escalado automático en acción  
 Windows Forms ahora usa la lógica siguiente para escalar automáticamente los formularios y su contenido:  
  
1.  En tiempo de diseño, cada <xref:System.Windows.Forms.ContainerControl> registra el modo de escalado y su resolución actual en <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A> y <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A>, respectivamente.  
  
2.  En tiempo de ejecución, la resolución real se almacena en la propiedad <xref:System.Windows.Forms.ContainerControl.CurrentAutoScaleDimensions%2A>.  La propiedad <xref:System.Windows.Forms.ContainerControl.AutoScaleFactor%2A> calcula dinámicamente la proporción entre la resolución de escalado en tiempo de ejecución y tiempo de diseño.  
  
3.  Si al cargar el formulario los valores de <xref:System.Windows.Forms.ContainerControl.CurrentAutoScaleDimensions%2A> y <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A> son diferentes, se llamará al método <xref:System.Windows.Forms.ContainerControl.PerformAutoScale%2A> para escalar el control y sus elementos secundarios.  Este método suspende el diseño y llama al método <xref:System.Windows.Forms.Control.Scale%2A> para realizar el escalado real.  Después, el valor de <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A> se actualiza para evitar el escalado progresivo.  
  
4.  <xref:System.Windows.Forms.ContainerControl.PerformAutoScale%2A> también se invoca automáticamente en las situaciones siguientes:  
  
    -   En respuesta al evento <xref:System.Windows.Forms.Control.OnFontChanged%2A> si el modo de escalado es <xref:System.Windows.Forms.AutoScaleMode>.  
  
    -   Cuando el diseño del contenedor se reanuda y se detecta un cambio en las propiedades <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A> o <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A>.  
  
    -   Como se insinúa anteriormente, cuando se escala un elemento primario <xref:System.Windows.Forms.ContainerControl>.  Cada control contenedor es responsable de realizar el escalado de sus elementos secundarios mediante sus propios factores de escala, no los del contenedor primario.  
  
5.  Los controles secundarios pueden modificar su comportamiento de escalado a través de varios medios:  
  
    -   La propiedad <xref:System.Windows.Forms.Control.ScaleChildren%2A> se puede invalidar para determinar si se deben escalar sus controles secundarios o no.  
  
    -   El método <xref:System.Windows.Forms.Control.GetScaledBounds%2A> se puede invalidar para ajustar los límites a los que se escala el control, pero no la lógica de escalado.  
  
    -   El método <xref:System.Windows.Forms.Control.ScaleControl%2A> se puede invalidar para cambiar la lógica de escalado del control actual.  
  
## Vea también  
 <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A>   
 <xref:System.Windows.Forms.Control.Scale%2A>   
 <xref:System.Windows.Forms.ContainerControl.PerformAutoScale%2A>   
 <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A>   
 [Representar controles con estilos visuales](../../../docs/framework/winforms/controls/rendering-controls-with-visual-styles.md)   
 [Cómo: Mejorar el rendimiento evitando el ajuste de tamaño automático](../../../docs/framework/winforms/advanced/how-to-improve-performance-by-avoiding-automatic-scaling.md)