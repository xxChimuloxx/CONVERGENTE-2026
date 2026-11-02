# Subte / Una estación. Toda una red.

Versión 2. Página estática del proyecto de Metodología de la Investigación, Licenciatura en Ciencia de Datos, Universidad del Gran Rosario.

Autores: Sebastián Fuentes, Solange Galaz y Mattias Peralta Fernández.
Contacto: sf85@hotmail.com

## Abrir la página en tu computadora

1. Descomprimí TODO el ZIP en una carpeta.
2. Abrí `index.html` en tu navegador.
3. Conservá las carpetas `data`, `assets` y `descargas` junto al HTML.

Esta versión carga los datos mediante archivos JavaScript clásicos, sin `fetch`, módulos, llamadas a servicios externos ni lectura de JSON mediante solicitudes del navegador. Se eliminó la dependencia que impedía la carga habitual al abrir el HTML con `file://`.

La revisión de interfaz se realizó en la vista previa HTTP. El navegador remoto usado para revisar no permite navegar a `file://`; esa apertura directa no pudo comprobarse allí. Si un navegador o una política de tu computadora restringe los archivos locales, podés servir esta carpeta con `python -m http.server 8000` y abrir http://localhost:8000, o publicarla en GitHub Pages.

## Publicar en GitHub Pages

1. Creá un repositorio y subí el contenido descomprimido: `index.html`, `app.js`, `config.js`, `styles.css`, `assets`, `data`, `descargas` y `.nojekyll` deben quedar en la raíz.
2. En el repositorio, entrá a **Settings > Pages**.
3. En **Build and deployment**, elegí **Deploy from a branch**, tu rama (habitualmente `main`) y **/(root)**.
4. Guardá y esperá a que GitHub muestre la dirección publicada.

No subas el ZIP como un único archivo: subí su contenido. Todos los archivos individuales de esta versión están por debajo de 25 MiB, por lo que se puede usar la carga web de GitHub. No necesita npm ni compilación. Las rutas relativas permiten alojarla también dentro de un repositorio de proyecto.

## Qué cambió

- Datos de inicio y detalle horario empaquetados como JavaScript local, sin `fetch`.
- Explicación ampliada de demanda, grafos, centralidades, modelos gravitatorios, asignación de recorridos, criticidad y organización de tablas.
- Ejemplo interactivo de sensibilidad gravitatoria con las alternativas de Bulnes D a las 17:00. β = 1,50 reproduce el reparto base; otros valores son ejercicios de sensibilidad claramente identificados.
- Se conserva el explorador de resultados originales por estación y hora.
- Se dejan únicamente el informe completo PDF y el vínculo externo de materiales. El ZIP no incluye PBIX, Word, póster ni descarga CSV.

## Cambiar el vínculo de Drive

Editá `config.js` y reemplazá el valor de `materialsUrl` por el enlace compartido de tu carpeta de Drive. Está cargado el enlace `https://qrto.org/h0Vmlj`, extraído del QR que proporcionaron los autores. No es una URL directa de Drive y no se pudo verificar su redirección desde el entorno de revisión. Verificá su destino o reemplazalo por el enlace directo antes de publicar.

El informe se encuentra en `descargas/informe.pdf`. Reemplazá ese archivo conservando el nombre cuando tengas una nueva versión.

## Procedencia y unidades

Los resultados del explorador se extrajeron de `Subtes_Grupo6.pbix`; el archivo original no se publica con esta página. La web consulta sus resultados precalculados: no ejecuta Power BI ni DAX. El histórico comprende 83.948.107 registros de 2014–2021 y los perfiles usan 30 miércoles de junio a diciembre de 2019.

Los destinos, recorridos y redistribución son estimaciones bajo supuestos explícitos. La tasa base de traslado es 0,7. El p95 de demanda no es capacidad física. Una estación-hora con 0 días observados no tiene observaciones de ingreso disponibles.

- Porcentajes: los valores del modelo ya están en escala 0–100.
- Índice de impacto: escala comparativa 0–100, no porcentaje de pasajeros.
- Distancia de cierre: distancia compuesta ponderada, en kilómetros.
- Demanda habitual: promedio de ingresos por estación y hora.
- Variación de flujo: diferencia entre flujo estimado posterior y base.

### Datos del navegador

`data/catalog.js` contiene `window.SUBTE_DATA`: red, perfiles horarios y caso gravitatorio. La red tiene 90 estaciones–línea y 97 conexiones.

Los perfiles contienen arrays alineados con las 90 estaciones:

- `demand`: [ingresos medios, p95, días observados].
- `impact`: [flujo afectado %, flujo desconectado %, pérdida de eficiencia %, pares desconectados %, índice, ranking de impacto, ranking de demanda, nivel].
- `closure`: [demanda afectada, reasignados, no reasignados, distancia ponderada km, cantidad de alternativas, tasa].
- `alternatives`: [índice de alternativa, ingresos recibidos estimados, distancia compuesta km, proporción local].

`data/routes-H.js`, H=0…23, carga el detalle de interrupciones de una hora en `window.SUBTE_ROUTES[H]`. Cada escenario incluye nodos y aristas alineados con la red: [flujo base, flujo posterior, variación, estado]. Se cargan a demanda para evitar leer las 24 horas de detalle al inicio.

Cada selección representa una estación por separado. No se suman incidentes simultáneos.

## Documentación de publicación

- https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
- https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository
