# PDF Merger + Compresor — Courier Docs

Herramienta web para fusionar, ordenar y comprimir los PDFs de envíos de courier. Todo el procesamiento ocurre en el navegador: ningún archivo se sube a ningún servidor.

## Qué hace

- Carga carpetas de envíos (cada carpeta = un envío con 4 documentos).
- Detecta automáticamente el tipo de cada PDF y los ordena: **1) Guía Aérea → 2) DSI → 3) Factura Courier → 4) Invoice**.
- Agrupa los archivos por carpeta de origen y avisa si a un envío le falta alguno de los 4 documentos.
- Fusiona todo en un único PDF respetando ese orden, envío por envío.
- Comprime el resultado en 4 niveles seleccionables (Sin comprimir / Equilibrado / Alta calidad / Máxima compresión).
- Permite descargar el PDF final y muestra cuánto se redujo el peso.

## Dónde está alojada

- **Repositorio GitHub:** `dgbelgrano-del/PDFMerged`
- **Link de uso (desde cualquier equipo):** `https://dgbelgrano-del.github.io/PDFMerged/`
- El archivo en el repo se llama `index.html` (nombre obligatorio para que GitHub Pages lo muestre).

## Cómo usarla

1. Abrir el link en el navegador.
2. Cargar los envíos de alguna de estas 3 formas:
   - Arrastrar una o varias carpetas juntas a la zona de carga.
   - Clic en "Agregar carpeta" las veces que haga falta (se van sumando).
   - Seleccionar una carpeta madre que contenga todas las subcarpetas de envíos.
3. Revisar que cada envío figure como "Completo". Si algún archivo quedó sin categoría, asignarla con el selector de esa fila.
4. Elegir el nivel de compresión (por defecto "Equilibrado", ideal para documentos escaneados).
5. Clic en "Fusionar PDFs" y luego en "Descargar PDF".

## Cómo actualizarla en el futuro

1. Editar el archivo HTML con los cambios.
2. En el repo de GitHub: "Add file" → "Upload files".
3. Subir el nuevo archivo manteniendo el nombre `index.html` y confirmar el reemplazo.
4. "Commit changes". En 1-2 minutos el link queda actualizado.

## Notas técnicas

- **Detección de tipo de documento:** combina palabras clave (guia, dsi, factura, invoice) con patrones de nombres codificados (ej. `CAF721757` → Guía, `AF721757_30716891603` → DSI, `FAA-4-188098` → Factura).
- **Compresión:** rasteriza cada página y la reencoda como JPEG con calidad controlada. Es lo más efectivo para documentos escaneados. Contrapartida: el texto digital deja de ser seleccionable, por eso existe la opción "Sin comprimir".
- **Privacidad:** se usó este enfoque (en vez de servicios como iLovePDF) justamente para que los archivos nunca salgan del equipo.

## Aprendizajes clave del proceso

- **Los artefactos de Claude corren en un sandbox** que bloquea la descarga de archivos. Por eso la herramienta funciona como archivo HTML alojado, no como artefacto.
- **El protocolo `file://`** (abrir el HTML localmente) rompe la lectura de carpetas arrastradas. Servir el archivo por `https` (GitHub Pages) resuelve esto y habilita todas las funciones.
- La solución final —hospedar en GitHub Pages— da lo mejor de ambos mundos: link accesible desde cualquier lado + todas las funciones operativas.

## Librerías utilizadas

- **pdf-lib** — fusión de PDFs y armado del documento final.
- **pdf.js** — rasterizado de páginas para la compresión.
- **Tailwind / CSS propio** — interfaz.
