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

    Acciones Tomadas (Un Enfoque de Post-Mortem Constructivo)
En lugar de aplicar soluciones rápidas y parches, decidí abordar el problema con un enfoque sistemático, similar a un post-mortem constructivo, pero aplicado a una fase de desarrollo. No se trataba de buscar un culpable, sino de entender la causa raíz para construir una solución duradera.
  Paso 1: Identificación de la Causa Raíz (El "Post-Mortem")
Mi primer paso fue analizar a fondo la estructura de mi archivo. Revisé cómo estaban construidas las tablas dinámicas y descubrí el problema fundamental:
Algunas tablas dinámicas utilizaban rangos fijos (ej. =Hoja1!$A$1:$G$1000).
Otras, las más recientes, trabajaban sobre tablas estructuradas (ej. =TablaVentas).
La causa raíz era clara: la falta de uniformidad. Los rangos fijos no se expandían automáticamente, lo que provocaba que los gráficos y análisis basados en ellos quedaran obsoletos al agregar nuevos datos.
  Paso 2: Reestructuración de la Base de Datos (La Solución)
Con la causa identificada, procedí a estandarizar toda la base de datos:
Convertir todo en una Tabla de Excel: Seleccioné todo el rango de datos (incluyendo encabezados) y presioné Ctrl + T. Esto convirtió el rango estático en una "Tabla" dinámica. La clave de este paso es que, al añadir nuevas filas al final, la tabla se expande automáticamente, y este nuevo rango es reconocido por Excel.
  Paso 3: Actualización del Modelo de Datos
Con la tabla estructurada como base, el siguiente paso fue reconstruir el modelo analítico sobre una base sólida:
Reemplacé las tablas dinámicas antiguas: Eliminé todas las tablas dinámicas que usaban rangos fijos y las recreé desde cero, pero esta vez seleccionando como origen el nombre de la nueva Tabla de Excel (ej. TablaVentas).
Reconecté los gráficos dinámicos: Una vez que las nuevas tablas dinámicas estuvieron listas, volví a vincular cada gráfico a su tabla dinámica correspondiente.
  Paso 4: Unificación con Segmentaciones
El paso más crítico para la consistencia del dashboard fue la correcta configuración de las segmentaciones de datos.
Cada segmentación (por ejemplo, de fecha, región o producto) debía controlar todas las tablas dinámicas relevantes.
Para lograrlo, hice clic derecho sobre cada segmentación, seleccioné "Conexiones de informe..." y, en el cuadro de diálogo, marqué todas las tablas dinámicas que debían ser afectadas por ese filtro.
Esto garantizó que, al seleccionar "Región Sur", cada gráfico y cada tabla en el dashboard se actualizaran al unísono, mostrando la misma información filtrada.
  Paso 5: Validación y Documentación
Finalmente, realicé pruebas exhaustivas para asegurar la robustez de la solución:
Agregué nuevas filas de ventas.
Modifiqué categorías existentes.
Cambié fechas y eliminé registros de prueba.
En todos los casos, después de un simple clic derecho en cualquier tabla dinámica y seleccionar "Actualizar", el dashboard completo respondía correctamente y de manera uniforme.
Documenté cada uno de estos pasos en el repositorio del proyecto para que cualquier miembro del equipo pudiera comprender y replicar el flujo de trabajo en el futuro.
