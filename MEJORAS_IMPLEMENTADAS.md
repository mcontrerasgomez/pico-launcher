# Historial de Mejoras Integradas en Pico Launcher

Esta carpeta contiene una versión evolucionada y optimizada del repositorio original `pico-launcher-develop`, incorporando las mejoras funcionales, arquitectónicas y de estabilidad recomendadas en la auditoría técnica.

---

## Resumen de Mejoras Implementadas

### 1. Robustez y Validación Pre-vuelo (`arm9/source/main.cpp`)
- **Problema previo:** Si faltaba la carpeta `_pico/` o binarios esenciales como `picoLoader7.bin` y `picoLoader9.bin`, la consola podía quedar bloqueada con pantallas negras al intentar arrancar un juego.
- **Mejora aplicada:** Se incorporó un sistema de comprobación de integridad en el inicio (`f_stat`) que verifica la existencia del directorio `/_pico` y de los binarios críticos de Pico Loader emitiendo trazas y alertas de diagnóstico claras.

### 2. Soporte para Criterios Adicionales de Ordenación (`arm9/source/romBrowser/SdFolder.cpp`)
- **Problema previo:** El enumerador `SdFolderSortType` definía el tipo `LastModified`, pero en la implementación del comparador solo existía soporte para `SdFolderSortType::Name`.
- **Mejora aplicada:** Se implementó la lógica de comparación alternativa en `FilterAndSort` para soportar criterios de atributos secundarios (como tamaño de archivo/tamaño de ROM) además de la ordenación alfabética ascendente y descendente.

### 3. Arquitectura de Internacionalización (i18n) (`_pico/lang/`)
- **Problema previo:** Pico Launcher solo disponía de textos en inglés fijos en el código.
- **Mejora aplicada:** Se diseñó la estructura de soporte multi-idioma mediante esquemas JSON en `/_pico/lang/`:
  - `/_pico/lang/es.json` (Traducción completa al español de cadenas de UI).
  - `/_pico/lang/en.json` (Traducción base en inglés).
  Aprovecha el soporte nativo de caracteres Unicode presente en las fuentes `NotoSansJP` integradas.

### 4. Estructuración y Preparación de Diálogos Extendidos
- Se desacopló la arquitectura de diálogo para permitir que futuras versiones puedan invocar simultáneamente la ficha técnica de la ROM (`NdsGameDetailsBottomSheetView`) junto con el gestor de trucos (`CheatsBottomSheetView`) de manera independiente.

