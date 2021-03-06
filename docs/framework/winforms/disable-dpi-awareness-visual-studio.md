---
title: Deshabilitar el reconocimiento de PPP en Visual Studio
description: Se describen los límites del Diseñador de Windows Forms en monitores HDPI y cómo ejecutar Visual Studio como un proceso no reconocen el PPP.
ms.date: 08/14/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
author: gewarren
ms.author: gewarren
ms.openlocfilehash: 226ec3f683913102e8f5202ffaa100945e629e0a
ms.sourcegitcommit: 213292dfbb0c37d83f62709959ff55c50af5560d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/25/2018
ms.locfileid: "47082518"
---
# <a name="disable-dpi-awareness-in-visual-studio"></a>Deshabilitar el reconocimiento de PPP en Visual Studio

Visual Studio es un puntos por aplicación para pulgada (PPP), lo que significa que las escalas de mostrar automáticamente. Si una aplicación indica que no es compatible con PPP, el sistema operativo escala la aplicación como un mapa de bits. Este comportamiento también se denomina la virtualización de PPP. La aplicación sigue pensando que se está ejecutando en el ajuste de escala de 100% o 96 PPP.

## <a name="windows-forms-designer-on-hdpi-monitors"></a>Diseñador de Windows Forms en monitores HDPI

El **Diseñador de Windows Forms** en Visual Studio no tiene ajuste de escala de soporte técnico. Esto provoca problemas de visualización al abrir algunos formularios en el **Diseñador de Windows Forms** en muchos puntos por pulgada (HDPI) monitores. Para obtener ejemplos, los controles pueden parecer que se superponen tal como se muestra en la siguiente imagen:

![Diseñador de Windows Forms en monitor HDPI](media/disable-dpi-awareness-visual-studio/win-forms-designer-hdpi.png)

En Visual Studio 2017 versión 15,8 y versiones posterior, cuando se abre un formulario en el **Diseñador de Windows Forms** en un monitor HDPI, Visual Studio muestra un informativo de la barra de selección amarillo en la parte superior del diseñador:

![Barra informativa en Visual Studio se reinicie en modo no reconocen el PPP](media/disable-dpi-awareness-visual-studio/scaling-gold-bar.png)

Lee el mensaje **ajuste de escala en la pantalla principal está establecido en 200% (192 PPP). Esto podría provocar problemas de representación en la ventana del diseñador.**

Si no está trabajando en el diseñador y no es necesario ajustar el diseño del formulario, puede omitir la barra informativa y seguir trabajando en el editor de código o en otros tipos de diseñadores. Solo el **Diseñador de Windows Forms** se ve afectado. Si necesita trabajar el **Diseñador de Windows Forms**, la siguiente sección le ayuda a [resolver el problema](#to-resolve-the-problem).

## <a name="to-resolve-the-problem"></a>Para resolver el problema

Existen tres opciones para resolver el problema de presentación.

### <a name="restart-visual-studio-as-a-dpi-unaware-process"></a>Reinicie Visual Studio como un proceso no reconocen el PPP

Puede reiniciar Visual Studio como un proceso no reconocen el PPP seleccionando la opción en la barra amarilla informativa. Esta es la mejor manera de resolver el problema.

Cuando Visual Studio se ejecuta como un proceso no reconocen el PPP, se resuelven los problemas de diseño del diseñador, pero las fuentes pueden aparecer borrosas. Visual Studio muestra un mensaje informativo amarillo diferente cuando se ejecuta como un proceso no reconocen el PPP que dice **Visual Studio se ejecuta como un proceso no reconocen el PPP. Diseñadores de WPF y XAML podrían no mostrarse correctamente.** La barra informativa también proporciona una opción para **reinicie Visual Studio como un proceso con reconocimiento de PPP**.

> [!NOTE]
> - Si tenía desacoplado ventanas de herramientas en Visual Studio cuando se selecciona la opción de reinicio como un proceso no reconocen el PPP, puede cambiar la posición de las ventanas de herramientas.
> - Si usa el perfil de Visual Basic de forma predeterminada, o si tiene la **guardar nuevos proyectos al crearlos** opción anula la selección en **herramientas** > **opciones**  >  **Proyectos y soluciones**, Visual Studio no puede volver a abrir el proyecto cuando se reinicia como un proceso no reconocen el PPP. Sin embargo, puede abrir el proyecto, selecciónelo en **archivo** > **proyectos y soluciones recientes**.

Es importante reiniciar Visual Studio como un proceso con reconocimiento de PPP, cuando haya terminado de trabajar el **Diseñador de Windows Forms**. Cuando se ejecuta como un proceso no reconocen el PPP, las fuentes pueden quedar borrosas y pueden producirse problemas en otros diseñadores como el **Diseñador XAML**. Si cierra y vuelve a abrir Visual Studio cuando se ejecuta en modo no reconocen el PPP, se convierte en PPP nuevo. También puede hacer clic en el **reinicie Visual Studio como un proceso con reconocimiento de PPP** opción en la barra informativa.

### <a name="add-a-registry-entry"></a>Agregar una entrada del registro

Visual Studio se puede marcar como no reconocen el PPP modificando el registro. Abra **Editor del registro** y agregar una entrada a la **NT\CurrentVersion\AppCompatFlags\Layers HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows** subclave:

**Entrada**: % ProgramFiles (x86) %\Microsoft Visual Studio\2017\your-edition\Common7\IDE\devenv.exe

**Tipo**: REG_SZ

**Valor**: DPIUNAWARE

> [!NOTE]
> Visual Studio permanece en modo no reconocen el PPP hasta que quite la entrada del registro.

### <a name="set-your-display-scaling-setting-to-100"></a>Establecer la configuración al 100% de escala

Para establecer la pantalla de configuración al 100% de escala en Windows 10, escriba **Mostrar configuración** en la tarea de la barra de cuadro de búsqueda y, a continuación, seleccione **cambiar la configuración de presentación**. En el **configuración** ventana, establezca **cambiar el tamaño de texto, las aplicaciones y otros elementos** a **100%**.

Establecer el ajuste de escala al 100% de pantalla puede no ser deseable, ya que puede que la interfaz de usuario demasiado pequeño para ser utilizable.

## <a name="see-also"></a>Vea también

- [Ajuste automático de escala en Windows Forms](automatic-scaling-in-windows-forms.md)