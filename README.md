# **Blog Técnico: QA Testing en SauceDemo**

## Contexto

Como parte del curso de Testing QA de Coderhouse, realicé un proceso de testing 
exploratorio y funcional sobre la aplicación de e-commerce SauceDemo, utilizando 
la técnica de caja negra (black box testing). El trabajo incluyó el diseño de 
casos de prueba, la ejecución con el usuario estándar de la plataforma, testing 
de API con Postman y un análisis de performance con Lighthouse.

## Problema

Durante la ejecución de los casos de prueba con el usuario `standard_user`, 
identifiqué varios comportamientos inesperados en el flujo de compra de la 
aplicación. Entre los más relevantes:

- El carrito de compras **conserva los productos agregados incluso después 
  de cerrar sesión**, cuando lo esperable sería que se vacíe o al menos se 
  advierta al usuario.
- Al aplicar un filtro de ordenamiento de productos (por precio, por nombre) 
  y luego navegar a otra sección, **el filtro se pierde** y vuelve al estado 
  por defecto.
- Al eliminar un producto del carrito, **no hay ninguna confirmación visual** 
  de que la acción se realizó correctamente.
- El **impuesto (tax) recién se muestra en el paso final del checkout**, sin 
  que el usuario pueda anticipar el costo total antes de llegar a esa instancia.

Estos hallazgos plantearon la necesidad de documentar cada uno como bug 
report formal, priorizando su impacto en la experiencia del usuario.


## Acciones

Para abordar estos hallazgos, seguí el siguiente proceso:

1. **Diseño de casos de prueba:** elaboré 10 casos de prueba (positivos y 
   negativos) cubriendo login, búsqueda, filtrado, carrito y checkout.
2. **Ejecución y reporte de bugs:** de la ejecución surgieron 3 reportes de 
   bugs formales, cada uno con pasos de reproducción, resultado esperado vs. 
   obtenido, y evidencia.
3. **Testing de API con Postman:** complementé el testing funcional con 
   pruebas a nivel de API, verificando respuestas y códigos de estado.
4. **Análisis de performance con Lighthouse:** generé un reporte de 
   performance para identificar oportunidades de mejora en tiempos de carga 
   y accesibilidad.

### Post-mortem constructivo

Al cerrar el ciclo de testing, hice una revisión del proceso identificando 
qué funcionó bien y qué podía mejorarse:

**Qué funcionó bien:**
- La combinación de testing funcional (UI) con testing de API permitió 
  detectar problemas que solo aparecían al cruzar ambas capas, como bugs 
  de experiencia de usuario que no eran evidentes solo mirando las 
  respuestas del backend.
- Diseñar casos de prueba negativos (no solo positivos) ayudó a encontrar 
  el bug de persistencia del carrito, que no hubiera aparecido probando 
  únicamente el flujo "feliz".

**Qué se podía mejorar:**
- En los primeros bugs reportados, la evidencia (capturas, pasos) se agregó 
  después de la ejecución, en lugar de capturarla en el momento. Esto generó 
  retrabajo para reconstruir el contexto exacto de cada fallo.
- No prioricé los bugs por severidad/impacto desde el principio, lo cual 
  hubiera ayudado a comunicar mejor cuáles requerían atención más urgente 
  (por ejemplo, el bug del carrito persistente tiene mayor impacto que la 
  falta de confirmación visual al eliminar un producto).

**Mejora implementada:**
- A partir de esa revisión, adopté la práctica de documentar cada bug 
  inmediatamente después de detectarlo (captura + pasos + severidad), en 
  lugar de dejarlo para el final del ciclo de testing.

## Aprendizajes

Este proceso me dejó varios aprendizajes concretos:

- La importancia de **separar claramente lo funcional de lo no funcional**: 
  un bug de UX (como la falta de confirmación al eliminar un producto) es 
  tan válido de reportar como uno que rompe una funcionalidad.
- Un buen reporte de bug no solo dice "qué está mal", sino que **facilita 
  el trabajo de quien lo va a solucionar**, con pasos claros y reproducibles.
- El testing de API mostró que muchos problemas de UX no vienen del backend, 
  sino de decisiones de diseño en el frontend — algo que solo se detecta 
  combinando ambos enfoques de testing.
- Documentar la evidencia en el momento (y no después) ahorra tiempo y 
  mejora la calidad del reporte final.
