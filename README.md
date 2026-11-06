# SOC Analyzer

Aplicación web para **investigar un posible incidente de seguridad**: carga el Excel exportado del SIEM, detecta indicadores de compromiso, correlaciona eventos y genera un **informe técnico** y un **informe ejecutivo** en PDF, con apoyo opcional de IA.

> Proyecto del *Bootcamp Analista SOC Nivel 2 · Reto final*.

## Escenario

Consultora de ciberseguridad en Estocolmo, Suecia. El cliente reporta un posible incidente en su infraestructura y entrega un Excel con logs exportados de su SIEM. La misión: buscar indicadores de compromiso (IoC), correlacionar eventos y establecer si hubo uno o varios incidentes.

## Funcionalidades

| # | Funcionalidad | Dónde |
|---|---|---|
| 01 | Carga de archivos (.xlsx, .xls, .csv) y vista de los logs | Pestaña 1 |
| 02 | Análisis de seguridad y correlación de eventos | Pestaña 2 |
| 03 | Dashboard con estadísticas y gráficos interactivos por criticidad | Pestaña 3 |
| 04 | Clasificación de riesgos (Crítico, Alto, Medio, Bajo) con justificación | Pestaña 4 |
| 05 | Informe técnico estructurado | Pestaña 5 |
| 06 | Informe ejecutivo y exportación a PDF | Pestaña 6 |
| — | Asistente de IA (opcional) | Pestaña 7 |

## Qué detecta

- **Fuerza bruta:** intentos de acceso no autorizados y password spraying, y si hubo acceso exitoso posterior.
- **Inicios sospechosos:** sesiones anómalas por origen, horario o patrón.
- **Escalamiento:** elevación de privilegios y cambios en grupos administrativos.
- **Comandos y procesos:** ejecución sospechosa en equipos.
- **Movimiento lateral:** saltos entre sistemas de la red.
- **Otras anomalías:** cualquier comportamiento fuera de lo normal (borrado de logs, defensas desactivadas, etc.).

Cada hallazgo incluye criticidad, nivel de confianza, justificación, técnica MITRE ATT&CK y las filas del archivo que lo sustentan.

## Informes

**Informe técnico:** resumen ejecutivo, hallazgos identificados, explicación técnica de cada hallazgo, evidencias en los logs, criticidad y justificación, posible impacto en la organización, plan de acción (investigar, contener y remediar) y recomendaciones generales. Anexos: calidad de los datos, IoC y mapeo MITRE.

**Informe ejecutivo:** pensado para la dirección sin conocimientos de TI. Incluye nivel de riesgo, principales hallazgos, impacto en el negocio, avances y mitigaciones, y hoja de ruta de 3 a 6 meses. Permite comparar con el periodo anterior cargando un segundo archivo.

## Cómo usarla

1. Abra `index.html` en el navegador (doble clic) o use la versión publicada en GitHub Pages.
2. Cierre la portada con **Comenzar análisis**, o pruebe con **Probar con datos de ejemplo**.
3. Cargue el Excel del SIEM en la pestaña 1.
4. Revise el análisis, el dashboard y la clasificación de riesgos.
5. Descargue el informe técnico o ejecutivo en PDF.

No requiere instalación ni servidor. Necesita conexión a internet solo para cargar las librerías.

## Formato del archivo

Una fila por evento. La app reconoce las columnas por su nombre (español o inglés): fecha y hora, usuario, IP de origen, equipo, y evento o descripción. Si falta alguna, intenta extraerla del texto del evento. La pestaña 1 muestra qué columnas detectó y la calidad de los datos.

## Rigor analítico

- No se inventan hallazgos: cada conclusión se sustenta en filas concretas del archivo.
- Cada hallazgo muestra su nivel de confianza y el motivo de su criticidad.
- Los límites de los datos (fechas, usuarios o IP faltantes, texto redactado) se declaran en el informe.
- Las detecciones basadas en reglas son **orientativas** y deben ser validadas por un analista.

## Privacidad

- El análisis se ejecuta **en el navegador**; el Excel no se sube a ningún servidor.
- El asistente de IA es **opcional**. Solo si ingresa una API key de Anthropic, se envían a la API los hallazgos y evidencias detectados (no el archivo completo). Su respuesta se verifica automáticamente contra los registros.
- No requiere integración con Microsoft Sentinel.
- **No suba logs reales de clientes a este repositorio.** El `.gitignore` excluye `.xlsx`, `.xls`, `.csv` y `.pdf` por seguridad.

## Tecnologías

HTML, CSS y JavaScript en un solo archivo, con estas librerías cargadas desde CDN:

- [SheetJS](https://sheetjs.com/) para leer Excel
- [Chart.js](https://www.chartjs.org/) para los gráficos
- [jsPDF](https://github.com/parallax/jsPDF) para exportar PDF

## Estructura

```
soc-analyzer/
├── index.html    # Aplicación completa
├── README.md
└── .gitignore
```

## Limitaciones

Herramienta de apoyo al triaje basada en reglas y correlación. No sustituye el juicio de un analista ni una investigación forense completa.

## Autor

_Su nombre · Bootcamp Analista SOC Nivel 2_
