---
title: '&lt;quitar&gt; (elemento) para &lt;los agentes de escucha&gt; para &lt;seguimiento&gt;'
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/remove
helpviewer_keywords:
- remove element
- <remove> element
ms.assetid: 9a5cd1b5-be1a-485f-8f0c-2890ad3ef3e0
author: mcleblanc
ms.author: markl
ms.openlocfilehash: 54fd529c571c8e8cf43c5dabe2398ae4a6cf4f11
ms.sourcegitcommit: fb78d8abbdb87144a3872cf154930157090dd933
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47230987"
---
# <a name="ltremovegt-element-for-ltlistenersgt-for-lttracegt"></a>&lt;quitar&gt; (elemento) para &lt;los agentes de escucha&gt; para &lt;seguimiento&gt;
Quita un agente de escucha el **los agentes de escucha** colección.  
  
 \<configuration>  
\<System.Diagnostics >  
\<seguimiento >  
\<los agentes de escucha >  
\<Quitar >  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<remove name="listener name" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|**name**|Atributo necesario.<br /><br /> El nombre del agente de escucha que se va a quitar de la **los agentes de escucha** colección.|  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguno.  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|`configuration`|Elemento raíz de cada archivo de configuración usado por las aplicaciones de Common Language Runtime y .NET Framework.|  
|`listeners`|Especifica un agente de escucha que recopila, almacena y enruta los mensajes. Los agentes de escucha dirigen los resultados de seguimiento a un destino apropiado.|  
|`system.diagnostics`|Especifica los agentes de escucha de seguimiento que recopilan, almacenan y enrutan mensajes, así como el nivel en el que está establecido un modificador de seguimiento.|  
|`trace`|Configura el servicio de seguimiento ASP.NET.|  
  
## <a name="remarks"></a>Comentarios  
  
> [!NOTE]
>  Quitar el <xref:System.Diagnostics.DefaultTraceListener> desde el `Listeners` colección modifica el comportamiento de la <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType>, <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=nameWithType>, <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=nameWithType>, y <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=nameWithType> métodos. Una llamada a un `Assert` o `Fail` método normalmente da como resultado la presentación de un cuadro de mensaje, pero no se muestra el cuadro de mensaje si el <xref:System.Diagnostics.DefaultTraceListener> no está en el `Listeners` colección.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra cómo quitar el agente de escucha de seguimiento predeterminado de la traza **los agentes de escucha** colección.  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <trace autoflush="true" indentsize="0">  
         <listeners>  
            <remove name="Default" />  
         </listeners>  
      </trace>  
   </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>Vea también  
 <xref:System.Diagnostics.TraceListener>  
 <xref:System.Diagnostics.DefaultTraceListener>  
 <xref:System.Diagnostics.TextWriterTraceListener>  
 <xref:System.Diagnostics.EventLogTraceListener>  
 [Esquema de la configuración de seguimiento y depuración](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)
