# data-web

Carpeta estándar para datos derivados destinados al visor público.

## Regla
Todo archivo aquí debe poder ser descargado públicamente sin exponer la BBDD Maestra ni información de trabajo.

## Origen
Unidad Compartida / BBDD Maestra -> proceso de publicación -> `data-web/`.

## Contenido permitido
- Geometría derivada necesaria para la escena 3D.
- Altura/pisos u otras variables derivadas requeridas para renderizar.
- Límites territoriales simplificados.
- Identificadores públicos y campos visibles.

## Contenido prohibido
- BBDD SII maestra u otras bases fuente.
- Archivos de cálculo o respaldo.
- Excel, GeoPackage, Shapefile, SQLite.
- Campos fuente no utilizados por la maqueta.

## Estado de migración
TRANSICIÓN. La maqueta aún consume archivos desde rutas históricas. Los archivos actuales no se moverán hasta validar la equivalencia y evitar romper GitHub Pages.
