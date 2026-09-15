# Límites Oficiales GIS STGO

La Maqueta 3D utiliza la referencia territorial común definida por GIS STGO.

Fuente canónica de publicación:
- Comuna: `PHDGEOGRAFO/GEOINDICADORES/data/comuna.geojson`
- Barrios: `PHDGEOGRAFO/GEOINDICADORES/data/barrios.geojson`
- Territorios PLADECO: `PHDGEOGRAFO/GEOINDICADORES/data/limite_territorios_pladeco.geojson`
- Manzana Censal 2024: `PHDGEOGRAFO/GEOINDICADORES/data/manzanas/*.geojson`

CRS web: EPSG:4326.

Jerarquía territorial oficial: `COMUNA → TERRITORIO → BARRIO → MANZANA CENSAL 2024`.

La llave oficial de manzana es `COD_MZN`.

Los antiguos archivos locales de límites quedan como respaldo/compatibilidad y no deben editarse como fuente independiente. Las correcciones territoriales se hacen primero en la fuente canónica y luego se consumen desde los visores.
