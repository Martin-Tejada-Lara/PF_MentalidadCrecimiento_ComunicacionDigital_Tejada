# PF_MentalidadCrecimiento_ComunicacionDigital_Tejada
TITULO: De datos crudos a dashboards: cómo solucioné un problema con tablas dinámicas en Excel aplicando una mentalidad de crecimiento
TL;DR:Durante mi proyecto final de la Diplomatura en Ciencia de Datos, enfrenté un problema crítico: los gráficos dinámicos de mi dashboard en Excel no se actualizaban correctamente al agregar nuevos datos. Este blog detalla cómo, mediante un enfoque estructurado y la aplicación de un post-mortem constructivo, identifiqué la causa raíz (rangos fijos en las tablas dinámicas), implementé una solución robusta usando Tablas de Excel y conexiones de informe, y documenté todo el proceso. El resultado no solo fue un dashboard funcional y fiable, sino también una valiosa lección sobre la importancia de las bases de datos bien estructuradas y la cultura de mejora continua.
Contexto
Durante el desarrollo del proyecto final de la Diplomatura en Ciencia de Datos, trabajé en la construcción de un dashboard interactivo en Microsoft Excel. El objetivo era transformar un conjunto de datos de ventas (aproximadamente 10,000 registros con campos como fecha, producto, región, vendedor y monto) en un tablero dinámico y profesional que permitiera a los stakeholders visualizar tendencias y tomar decisiones.
Para lograrlo, decidí utilizar un stack de herramientas nativas de Excel:
1) Power Query: Para la limpieza y transformación inicial de los datos.
2) Tablas Dinámicas y Gráficos Dinámicos: Como el núcleo del análisis y la visualización.
3) Segmentaciones de datos: Para ofrecer filtros interactivos y fáciles de usar.
4) Validaciones de datos: Para garantizar la integridad de la información ingresada.
  El requisito fundamental del proyecto era que el dashboard debía actualizarse automáticamente cada vez que se incorporaran nuevos registros a la base de datos, sin necesidad de intervención manual por parte del usuario final.

Problema
Al comenzar a ensamblar el dashboard, me topé con un inconveniente importante que amenazaba con descarrilar el proyecto. Los gráficos dinámicos no reflejaban correctamente los cambios realizados en la base de datos.
Cada vez que agregaba nuevos registros para probar la funcionalidad, me encontraba con que:
Algunos gráficos se quedaban con el rango de datos anterior.
Las tablas dinámicas no incluían las nuevas filas.
Debía actualizar manualmente el origen de datos de cada elemento, un proceso tedioso y propenso a errores.
Lo más crítico: Las segmentaciones no controlaban todos los gráficos. Esto provocaba que, al seleccionar un filtro (ej. "Región Norte"), algunos indicadores mostraran datos correctos mientras que otros seguían mostrando información sin filtrar, generando inconsistencias y una gran confusión.
En esencia, el dashboard, que debía ser una fuente de verdad única, se estaba convirtiendo en una fuente de desinformación.
