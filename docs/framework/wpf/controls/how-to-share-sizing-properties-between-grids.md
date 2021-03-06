---
title: 'Cómo: Compartir propiedades de ajuste de tamaño entre elementos Grid'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Grid control [WPF], sharing sizing data of columns
- sizing data in Grid controls [WPF]
- Grid control [WPF], sharing sizing data of rows
ms.assetid: a0535a6f-ff04-4b25-9912-7dd856e11044
ms.openlocfilehash: a85c0c36ef99e6501afddaca7f26acd2928da1ae
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33550870"
---
# <a name="how-to-share-sizing-properties-between-grids"></a>Cómo: Compartir propiedades de ajuste de tamaño entre elementos Grid
En este ejemplo se muestra cómo compartir los datos de ajuste de tamaño de columnas y filas entre <xref:System.Windows.Controls.Grid> elementos con el fin de mantener un tamaño coherente.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se presenta dos <xref:System.Windows.Controls.Grid> elementos como elementos secundarios de un elemento primario <xref:System.Windows.Controls.DockPanel>. El <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A> adjunta la propiedad de <xref:System.Windows.Controls.Grid> se define en el registro primario <xref:System.Windows.Controls.DockPanel>.  
  
 En el ejemplo se manipula el valor de propiedad por medio de dos <xref:System.Windows.Controls.Button> elementos; cada elemento representa uno de los valores de propiedad booleana. Cuando el <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A> valor de la propiedad se establece en `true`, cada miembro de columna o fila de una <xref:System.Windows.Controls.DefinitionBase.SharedSizeGroup%2A> comparte información de ajuste de tamaño, sin tener en cuenta el contenido de una fila o columna.  
  
 [!code-xaml[gridIssharedsizescopeProp#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#1)]  
  
 ...  
  
 [!code-xaml[gridIssharedsizescopeProp#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#2)]  
  
 En el siguiente ejemplo de código subyacente controla los métodos que el botón <xref:System.Windows.Controls.Primitives.ButtonBase.Click> genera el evento. El ejemplo escribe los resultados de estas llamadas a métodos <xref:System.Windows.Controls.TextBlock> elementos que use relacionado métodos get para generar los nuevos valores de propiedad como cadenas.  
  
 [!code-csharp[gridIssharedsizescopeProp#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml.cs#3)]
 [!code-vb[gridIssharedsizescopeProp#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/gridIssharedsizescopeProp/VisualBasic/Window1.xaml.vb#3)]  
  
## <a name="see-also"></a>Vea también  
 <xref:System.Windows.Controls.Grid>  
 <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A>  
 [Información general sobre elementos Panel](../../../../docs/framework/wpf/controls/panels-overview.md)
