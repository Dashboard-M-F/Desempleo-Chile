# Termómetro Laboral Chile

Panel interactivo del desempleo en Chile, construido sobre la Encuesta Nacional de Empleo (ENE) del Instituto Nacional de Estadísticas.

**Último período cargado:** trimestre móvil mayo–julio 2026 · boletín ENE n° 334, publicado el 28 de agosto de 2026.

---

## Archivos

| Archivo | Qué es | Cuándo se usa |
|---|---|---|
| `panel-desempleo-chile.html` | Documento HTML completo y autónomo. Se abre con doble clic en cualquier navegador; no requiere servidor ni conexión salvo para las tipografías. | Para consultar el panel sin depender de Claude, enviarlo por correo o alojarlo en un servidor propio. |
| `artifact-termometro-laboral.html` | El mismo panel, pero sin las etiquetas `<!doctype>`, `<html>`, `<head>` y `<body>`. Es el formato que exige la herramienta de artifacts de Claude, que agrega ese envoltorio al publicar. | Para republicar el panel en la URL del artifact ya existente. **No sirve para abrir directamente en un navegador.** |
| `datos-ene-may-jul-2026.json` | El conjunto de datos completo: las series nacionales, las 16 regiones y el detalle del último trimestre. | Para reutilizar las cifras en otro análisis o auditarlas contra los boletines. |

Los dos HTML son equivalentes en contenido. Al actualizar, hay que regenerar ambos.

---

## Qué contiene el panel

Siete indicadores de cabecera y seis vistas:

- **Evolución.** Serie nacional de 85 trimestres móviles (may–jul 2019 a may–jul 2026, incluida la pandemia), con selector de rango (Máx, 5 años, 3 años, 12 meses), tabla completa y un explorador que entrega, para cualquier trimestre, su tasa, la variación respecto del trimestre anterior, la variación en doce meses y su posición en el ranking histórico.
- **Regiones.** Las 16 regiones ordenadas por tasa, con la línea de referencia del promedio país, mayores alzas en doce meses y extremos del trimestre.
- **Sexo e informalidad.** Brecha de desocupación e informalidad entre mujeres y hombres, más horas trabajadas y tasas de participación y ocupación.
- **Sectores.** Variación anual del empleo por rama de actividad, en barras divergentes.
- **Series por región.** Pequeños múltiplos con la serie histórica de cada una de las 16 regiones a escala compartida, y un comparador de hasta dos regiones contra el país.
Sobre las tarjetas hay un **selector de trimestre móvil** con los 85 trimestres de la serie. Al elegir uno, la cabecera y las tarjetas muestran las cifras del INE para ese trimestre.

**El panel es de solo lectura.** Las cifras están compiladas de los boletines del INE y no pueden alterarse desde la interfaz.

La bajada del titular no es texto fijo: se calcula desde la serie cargada (variación en doce meses, desde cuándo no se registraba un nivel igual o superior, y rachas de trimestres por umbral). Lo mismo ocurre con las notas de máximo, mínimo y promedio, los conteos de regiones y el resumen de sectores.

---

## Qué dato hay para cada trimestre

El INE publica distinta profundidad según el indicador, y el panel refleja exactamente eso:

| Indicador | Cobertura en el panel |
|---|---|
| Tasa de desocupación nacional | 85 trimestres, de may–jul 2019 a may–jul 2026 |
| Desocupación de mujeres y de hombres | 61 trimestres, de may–jul 2021 a may–jul 2026 |
| Ocupación informal (total, mujeres, hombres) | 13 trimestres, de may–jul 2025 a may–jul 2026 |
| Ocupados, desocupados, participación, ocupación y horas | Solo may–jul 2026 |
| Regiones y sectores | Solo may–jul 2026 |

Cuando se selecciona un trimestre para el que un indicador no tiene serie, la tarjeta lo dice en vez de mostrar una cifra de otro período. Los paneles de regiones, sectores y sexo muestran un aviso indicando a qué trimestre corresponden.

**Nota metodológica importante:** la serie de ocupación informal **no se puede empalmar entre boletines**. El INE revisa sus valores: la edición n° 310 informa 27,6% para may–jul 2024 y la n° 322 informa 26,4% para ese mismo trimestre. Por eso el panel carga solo los trece trimestres de la edición vigente. La serie de desocupación, en cambio, sí es estable: los cuatro empalmes por sexo y los seis del total país calzaron sin una sola discrepancia.

---

## Cómo actualizar con una nueva entrega del INE

El INE publica el boletín ENE los últimos días de cada mes, y el boletín publicado a fines del mes M cubre el trimestre móvil que termina en M−1. La numeración avanza de uno en uno: la edición n° 334 corresponde a agosto de 2026, de modo que n° N = 334 + meses transcurridos desde entonces.

- Boletín nacional: `https://www.ine.gob.cl/docs/default-source/ocupacion-y-desocupacion/boletines/{AAAA}/nacional/ene-nacional-{N}.pdf`
- Boletines regionales: en `https://regiones.ine.cl/<región>/estadisticas-regionales/sociales/mercado-laboral/ocupacion-y-desocupacion`. Los nombres de archivo varían por región, así que conviene tomar la URL del listado en vez de construirla.
- Región Metropolitana: se publica en `www.ine.gob.cl`, no en el portal regional.

Cada boletín nacional trae la serie de los últimos trece trimestres móviles; cada boletín regional, la de su región. Para extender una serie basta empalmar dos ediciones separadas por doce meses, que se traslapan en un trimestre y permiten verificar el calce.

El detalle regional del trimestre no viene en el boletín nacional: hay que tomarlo de la difusión de prensa del INE del mismo día o de los boletines regionales.

---

## Fuentes de los datos cargados

- INE, boletín estadístico de empleo trimestral n° 334, 28 de agosto de 2026 (cifras nacionales del trimestre y últimos trece trimestres de la serie).
- INE, boletines n° 262, 274, 286, 298, 310 y 322 (tramos anteriores de la serie nacional, hasta completar siete años). Cada boletín publica trece trimestres móviles; las ediciones se empalman con un trimestre de traslape que permite verificar el calce, y en todos los empalmes coincidió.
- INE, difusión de prensa del 28 de agosto de 2026 (tasas regionales del trimestre).
- INE, boletines de empleo regionales del trimestre mayo–julio 2026 de las 16 regiones (series regionales de trece trimestres y detalle por sexo, informalidad y tasas complementarias).
- INE, boletines regionales de mayo–julio 2025 de Biobío y Ñuble (extensión de esas dos series a veinticinco trimestres).

Control de consistencia aplicado: las dieciséis series regionales terminan exactamente en la tasa que el INE reportó para cada región, y la diferencia entre su primer y último valor reproduce la variación en doce meses publicada.

---

## Sobre el nivel comunal

No existe en Chile una tasa de desocupación comunal oficial. El diseño muestral de la ENE está construido para dominios nacional y regional, más algunas provincias y ciudades; por debajo de ese nivel las estimaciones no son publicables. Tampoco hay un sustituto: el programa de estimaciones de área pequeña del Observatorio Social del Ministerio de Desarrollo Social cubre pobreza, no empleo, y los reportes comunales de la Biblioteca del Congreso usan registros de empresas del SII, no desempleo de personas. La región es hoy el mayor detalle territorial con calidad estadística.

---

## Advertencia

Panel elaborado con fines de análisis interno. No es una publicación del INE ni de ningún medio de prensa.
