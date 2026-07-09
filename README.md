**Blog Técnico: QA Testing en SauceDemo**

Contexto

Como parte del curso de Testing QA de Coderhouse, realicé un proceso de testing 
exploratorio y funcional sobre la aplicación de e-commerce SauceDemo, utilizando 
la técnica de caja negra (black box testing). El trabajo incluyó el diseño de 
casos de prueba, la ejecución con el usuario estándar de la plataforma, testing 
de API con Postman y un análisis de performance con Lighthouse.

Problema

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
