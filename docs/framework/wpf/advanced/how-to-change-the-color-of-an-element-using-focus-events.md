---
title: 'Cómo: Cambiar el color de un elemento mediante eventos de foco'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- focus events [WPF], changing element color for
- colors of elements [WPF], changing
- elements [WPF], changing color of
ms.assetid: 7e246802-3625-47a7-ae9d-c8a2a40fd040
ms.openlocfilehash: d8d8a3e8b24021cf8a5f916ce3f291a3b66d9411
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33543119"
---
# <a name="how-to-change-the-color-of-an-element-using-focus-events"></a>Cómo: Cambiar el color de un elemento mediante eventos de foco
Este ejemplo muestra cómo cambiar el color de un elemento cuando recibe y pierde el foco mediante el uso de la <xref:System.Windows.UIElement.GotFocus> y <xref:System.Windows.UIElement.LostFocus> eventos.  
  
 Este ejemplo consta de un [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] archivo y un archivo de código subyacente.  
  
## <a name="example"></a>Ejemplo  
 El siguiente [!INCLUDE[TLA2#tla_titlexaml](../../../../includes/tla2sharptla-titlexaml-md.md)] crea la interfaz de usuario, que consta de dos <xref:System.Windows.Controls.Button> objetos y asocia los controladores de eventos para el <xref:System.Windows.UIElement.GotFocus> y <xref:System.Windows.UIElement.LostFocus> eventos para el <xref:System.Windows.Controls.Button> objetos.  
  
 [!code-xaml[gotfocusLostfocusEffectUsingEvent#GotLostFocusSampleXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gotfocusLostfocusEffectUsingEvent/CSharp/Window1.xaml#gotlostfocussamplexaml)]  
  
 Crea el código siguiente detrás de la <xref:System.Windows.UIElement.GotFocus> y <xref:System.Windows.UIElement.LostFocus> controladores de eventos.  Cuando el <xref:System.Windows.Controls.Button> mejoras en el foco de teclado del <xref:System.Windows.Controls.Control.Background%2A> de la <xref:System.Windows.Controls.Button> se cambia a rojo.  Cuando el <xref:System.Windows.Controls.Button> pierde el foco de teclado, el <xref:System.Windows.Controls.Control.Background%2A> de la <xref:System.Windows.Controls.Button> vuelve a establecerse en blanco.  
  
 [!code-csharp[gotfocusLostfocusEffectUsingEvent#GotLostFocusSampleEventHandlers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gotfocusLostfocusEffectUsingEvent/CSharp/Window1.xaml.cs#gotlostfocussampleeventhandlers)]
 [!code-vb[gotfocusLostfocusEffectUsingEvent#GotLostFocusSampleEventHandlers](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/gotfocusLostfocusEffectUsingEvent/VisualBasic/Window1.xaml.vb#gotlostfocussampleeventhandlers)]  
  
## <a name="see-also"></a>Vea también  
 [Información general sobre acciones del usuario](../../../../docs/framework/wpf/advanced/input-overview.md)
