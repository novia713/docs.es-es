---
title: Agregar elementos, atributos y nodos a un árbol XML (Visual Basic)
ms.date: 07/20/2015
ms.assetid: e243e694-c987-43aa-8b22-1e33dace582c
ms.openlocfilehash: 86d28f5974e30a9b7f1a1e830cd40c3cd916e8ae
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33643018"
---
# <a name="adding-elements-attributes-and-nodes-to-an-xml-tree-visual-basic"></a>Agregar elementos, atributos y nodos a un árbol XML (Visual Basic)
Puede agregar contenidos (elementos, atributos, comentarios, instrucciones de procesamiento, texto y bloques CDATA) a un árbol XML existente.  
  
## <a name="methods-for-adding-content"></a>Métodos para agregar contenidos  
 Los métodos siguientes agregan contenidos secundarios a un <xref:System.Xml.Linq.XElement> o a un <xref:System.Xml.Linq.XDocument>:  
  
|Método|Descripción|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XContainer.Add%2A>|Agrega un contenido al final de los contenidos secundarios del <xref:System.Xml.Linq.XContainer>.|  
|<xref:System.Xml.Linq.XContainer.AddFirst%2A>|Agrega un contenido al comienzo de los contenidos secundarios del <xref:System.Xml.Linq.XContainer>.|  
  
 Los métodos siguientes agregan contenidos como nodos relacionados de un <xref:System.Xml.Linq.XNode>. El nodo al que se agregan habitualmente contenidos relacionados es <xref:System.Xml.Linq.XElement>, aunque es posible agregar contenidos relacionados válidos a otros tipos de nodos, como por ejemplo, al nodo <xref:System.Xml.Linq.XText> o al nodo <xref:System.Xml.Linq.XComment>.  
  
|Método|Descripción|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XNode.AddAfterSelf%2A>|Añade un contenido detrás de <xref:System.Xml.Linq.XNode>.|  
|<xref:System.Xml.Linq.XNode.AddBeforeSelf%2A>|Agrega contenido antes de <xref:System.Xml.Linq.XNode>.|  
  
## <a name="example"></a>Ejemplo  
  
### <a name="description"></a>Descripción  
 El siguiente ejemplo crear dos árboles XML y, a continuación, modifica uno de ellos.  
  
### <a name="code"></a>Código  
  
```vb  
Dim srcTree As XElement = _  
    <Root>  
        <Element1>1</Element1>  
        <Element2>2</Element2>  
        <Element3>3</Element3>  
        <Element4>4</Element4>  
        <Element5>5</Element5>  
    </Root>  
Dim xmlTree As XElement = _  
    <Root>  
        <Child1>1</Child1>  
        <Child2>2</Child2>  
        <Child3>3</Child3>  
        <Child4>4</Child4>  
        <Child5>5</Child5>  
    </Root>  
  
xmlTree.Add(<NewChild>new content</NewChild>)  
xmlTree.Add( _  
    From el In srcTree.Elements() _  
    Where CInt(el) > 3 _  
    Select el)  
  
' Even though Child9 does not exist in srcTree, the following statement  
' will not throw an exception, and nothing will be added to xmlTree.  
xmlTree.Add(srcTree.Element("Child9"))  
Console.WriteLine(xmlTree)  
```  
  
### <a name="comments"></a>Comentarios  
 Este código genera el siguiente resultado:  
  
```xml  
<Root>  
  <Child1>1</Child1>  
  <Child2>2</Child2>  
  <Child3>3</Child3>  
  <Child4>4</Child4>  
  <Child5>5</Child5>  
  <NewChild>new content</NewChild>  
  <Element4>4</Element4>  
  <Element5>5</Element5>  
</Root>  
```  
  
## <a name="see-also"></a>Vea también  
 [Modificar árboles XML (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)
