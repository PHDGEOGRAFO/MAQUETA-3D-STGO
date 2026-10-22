# STGO 3D — Plan de integración ambiental y gemelo digital
Fecha: 2026-10-22
Estado: hoja de ruta técnica, sin cambios a producción.

## Principio rector
Preservar `maqueta-general/`, `ambiental/`, `urbano/` y `subsuelo/` como módulos independientes. GIS CORE / DATA CORE como capa común de datos y servicios. El módulo Ambiental sigue siendo la prioridad de desarrollo; no duplicar pilotos ni sustituir metodologías existentes.

## Estado verificado del módulo `ambiental/index.html`
- Piloto Av. República: escenarios A (arborización), B (vegetación + desealado), C (intervención integrada).
- Índice de criticidad (ICT) con siete componentes y pesos explícitos; calcular solo con valores válidos y misma unidad/normalización.
- Referencia meteorológica Open-Meteo (modelo, no estación) y reporte SINCA Parque O'Higgins (estación, no medición de calle).
- Referencias DMC, Windy, CR2, ARClim; exportación/importación JSON; cartografía MapLibre 2D/3D.
- Pendientes: geometría definitiva corredor, StgoHot y sus fechas, sombra edificios/copas, impermeabilidad, ventilación, Censo 2024 por COD_MZN y vinculación Plan IV/PLADECO.
- El punto NDVI 0,09765 es referencia barrial provisional, no el corredor. Mantener visibles estas restricciones.

## Matriz de asignación
| Función | Módulo responsable | Compartir con |
|---|---|---|
| Geometría edificaciones SII, alturas estimadas, fachadas brutas | Maqueta General | Ambiental, Urbano |
| Sombra de edificios, radiación, sombra vegetal, viento, aire, calor, arbolado, ruido | Ambiental | Urbano |
| Escenarios de construcción, accesibilidad, isócronas, cartera de proyectos | Urbano | Ambiental |
| Redes e infraestructura subterránea | Subsuelo | Urbano |

## Integración de fuentes (registro inicial en `ambiental/fuentes-dinamicas.json`)
- Open-Meteo: modelo/pronóstico, conexión ya programada; lectura horaria cuando proveedor disponible.
- SINCA: observaciones estación, conexión ya programada; registrar período de promedio y estado.
- DMC: observación para calibración; credenciales solo servidor, autorización y estación por validar.
- SENAPRED: puntos críticos históricos y vigentes; verificar disponibilidad y licencia de servicio/exportación antes de automatizar.
- CR2MET: grillas históricas; procesamiento espacial y temporal, no 'tiempo real'.
- ARClim: escenarios climáticos, no monitoreo actual; elegir variable, período y escenario.
- Windy: visualización contextual, no sustituye datos del modelo ni implica derecho de extracción.
- StgoHot: temperatura superficial y fecha pendiente de fuente geoespacial validada.

## Requisitos del conector
1. Ingesta servidor o GitHub Actions para datos públicos permitidos; no incrustar llaves secretas en GitHub Pages.
2. Para cada fuente: identificador, URL oficial de documentación, licencia, método de acceso, frecuencia esperada, último intento, último dato válido, marca temporal del dato, zona horaria, unidad, resolución espacial, calidad, estado y error.
3. Normalizar WGS84 para publicación, EPSG:32719 para cálculos métricos; conservar fuente original y códigos de unión (COD_MZN, barrio, territorio, comuna). Evitar publicar personas, RUT, domicilio sensible y datos privados.
4. Conservar series históricas; nunca sobrescribir datos sin fecha. Si falla fuente, mantener último registro válido con advertencia de antigüedad.
5. Estados: observado, modelado, histórico, proyectado, simulado; no mezclar sin advertencia explícita.
6. Validación de rango, unidad, geometría y duplicados; registro reproducible del cálculo y versión del conjunto.
7. Respetar límites de solicitudes, CORS, atribuciones y políticas de reutilización.

## Fases y criterios de aceptación
**Fase 0 — Proteger lo existente**: respaldar y comprobar visores, enlaces, pilotos y cálculos de ICT. Pruebas de humo de fuentes actuales. No modificar producción con datos no validados.
**Fase 1 — Inventario / trazabilidad**: registro de fuentes y panel con actualización, fecha, estado y calidad; separar observado de pronóstico. Mostrar fallas sin datos inventados.
**Fase 2 — Territorializar riesgos**: serie de puntos críticos SENAPRED; identificar nuevos, persistentes y resueltos; cruces por COD_MZN/barrio solo con georreferenciación validada.
**Fase 3 — Sombras / fachadas**: superficie bruta por orientación; muros medianeros y alturas diferenciadas; sombra solar por fecha/hora con incertidumbre SII. Reutilizar geometría desde Maqueta General.
**Fase 4 — Arbolado / intervenciones**: copa y sombra con alturas verificadas; contraste de escenarios A/B/C, área efectivamente intervenida y temperatura/radiación cuando haya insumos.
**Fase 5 — Evaluación territorial**: indicadores auditables, escenarios vs línea base; integración con Plan de Infraestructura Verde, PLADECO y PDT; fichas descargables.
**Fase 6 — Transferencia**: pilotos adicionales a Av. República solo después de validación y criterios comparables.

## Condiciones técnicas
- No confundir 2,30 m de altura libre normativa con altura piso-a-piso construida; estimaciones desde pisos SII requieren espesor de losa e incertidumbre.
- No calcular UTCI con variables faltantes; no transformar NDVI directamente en grados; no presentar pronóstico regional como medida local.
- Las bandas paramétricas de referencia no constituyen resultados observados del piloto.
- Registrar fecha, escala y fuentes de cada indicador; exportar GeoPackage/CSV desde proceso validado.
- Desarrollo incremental en rama, revisión y pruebas antes de desplegar producción.

## Fuentes de inspiración
- HabitEntorno: funcionalidades referenciales de gemelo digital; no asumir acceso al código privado.
- Proyectos de Pablo Sarricolea: integración territorial de datos públicos y seguimiento entre años; verificación de mecanismo exacto de actualización pendiente.
