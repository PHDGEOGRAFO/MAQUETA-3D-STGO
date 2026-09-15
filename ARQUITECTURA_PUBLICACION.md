# Arquitectura de publicación de datos

## Regla general
La BBDD Maestra, cálculos, respaldos y archivos de revisión se mantienen fuera del repositorio público, en la Unidad Compartida/Drive institucional.

El visor público solo debe consumir una copia web derivada, preparada específicamente para visualización.

## Flujo estándar
1. BBDD Maestra privada en Unidad Compartida.
2. Proceso de publicación que selecciona únicamente campos autorizados.
3. Generación de archivos optimizados para web.
4. GitHub/GitHub Pages publica código y datos mínimos de visualización.

## No publicar
- BBDD maestras completas.
- Excel de cálculo o revisión.
- GeoPackage originales.
- Shapefiles originales.
- CSV completos de trabajo.
- Respaldos o archivos intermedios.
- Campos internos no visibles en el visor.

## Sí se puede publicar
- Geometría necesaria para la escena 3D.
- Identificadores públicos.
- Altura/pisos o variables derivadas necesarias para renderizar.
- Límites territoriales simplificados.
- Campos estrictamente visibles en la interfaz.

## Regla de seguridad
Todo archivo que recibe el navegador debe considerarse técnicamente descargable. Por tanto, la protección de la BBDD Maestra se logra evitando que sea enviada al navegador y publicando únicamente una versión reducida.

## Maqueta 3D Santiago
Los datos SII u otras fuentes maestras deben mantenerse privados. La publicación web debe usar una copia compacta que contenga solo geometría y atributos necesarios para representar el modelo 3D.
