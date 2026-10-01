---
layout: lab
title: "Práctica 7: Caso integral de desempeño comercial"
permalink: /lab13/lab13/
images_base: /labs/lab13/img
duration: "60 minutos"
objective:
  - Resolver un caso comercial completo utilizando Snowflake, Power BI y evidencia documentada, desde la definición de una pregunta analítica hasta una recomendación ejecutiva trazable y proporcional a la evidencia.
prerequisites:
  - Haber completado las Prácticas 1 a 6 y sus retos.
  - Disponer de C:\DAF\Practica_05\05_dashboard_ventas.pbix.
  - Disponer de C:\DAF\Practica_06\06_brief_interpretacion.xlsx.
  - Acceso de lectura a DATA_ANALYTICS_FOUNDATIONS.CURATED.VENTAS_TRANSACCIONES_CURADAS_2026_1.
  - Power BI Desktop, Microsoft Excel y acceso a Snowflake.
introduction:
  - Esta práctica es el proyecto integrador del curso. Partirás del brief de interpretación de la Práctica 6, formularás una pregunta prioritaria y dos hipótesis, verificarás que la fuente curada sea adecuada, investigarás la evidencia con SQL, contrastarás los resultados en Power BI y cerrarás con tres hallazgos y una conclusión ejecutiva.
slug: lab13
lab_number: 13
final_result: >
  Al finalizar tendrás un caso integral documentado con pregunta analítica, hipótesis,
  controles de calidad, consultas SQL, validación contra Power BI, tres hallazgos
  priorizados y una recomendación ejecutiva con nivel de certeza y limitaciones.
notes:
  - Utiliza QUALITYFLAG = 'VALID' como población principal.
  - No reconstruyas procesos ya realizados en prácticas anteriores salvo que el caso lo requiera.
  - Hipótesis no significa conclusión.
  - Una asociación observada no demuestra causalidad.
  - Mantén iguales los filtros al comparar Snowflake y Power BI.
references:
  - text: Snowflake Documentation - GROUP BY
    url: https://docs.snowflake.com/en/sql-reference/constructs/group-by
  - text: Snowflake Documentation - Aggregate functions
    url: https://docs.snowflake.com/en/sql-reference/functions-aggregation
  - text: Microsoft Learn - Filter data in Power BI reports
    url: https://learn.microsoft.com/en-us/power-bi/explore-reports/end-user-report-filter
  - text: Microsoft Learn - Power BI guidance
    url: https://learn.microsoft.com/power-bi/guidance/
prev: /lab12/lab12/
next: /lab14/lab14/
---

---

## 🎯 Tarea 1. Definir el problema y las hipótesis — 8 min

Transformarás una preocupación comercial en una pregunta medible y dos hipótesis investigables.

### Tarea 1.1. Preparar el proyecto

- {% include step_label.html %} Abre Git Bash y crea la carpeta `Practica_07`.

  Ejecuta:

  ```bash
  mkdir -p /c/DAF/Practica_07
  ```

  Presiona **Enter** y verifica que el comando termine sin errores.

  > **Nota:** La ruta `/c/DAF/Practica_07` en Git Bash corresponde a `C:\DAF\Practica_07\` en Windows.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existe `C:\DAF\Practica_07\`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Descarga los archivos auxiliares.

  Descarga:

  1. [Descargar SQL del caso integral](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap7/07_caso_integral.sql)
  2. [Descargar plantilla del caso integral](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap7/Plantilla_Practica7_Caso_Integral.xlsx)

  Guarda los archivos exactamente como:

  ```text
  C:\DAF\Practica_07\07_caso_integral.sql
  C:\DAF\Practica_07\Plantilla_Practica7_Caso_Integral.xlsx
  ```

  > **Nota:** Si el navegador guarda los archivos en `Descargas`, muévelos después a `C:\DAF\Practica_07\` sin cambiar sus nombres.
  {: .lab-note .info .compact}

  > **Salida esperada:** SQL y plantilla están disponibles localmente.
  {: .lab-note .output .compact}

### Tarea 1.2. Definir la pregunta

- {% include step_label.html %} Abre `C:\DAF\Practica_06\06_brief_interpretacion.xlsx` y revisa hallazgos, limitaciones y preguntas pendientes.

  En Excel abre:

  ```text
  C:\DAF\Practica_06\06_brief_interpretacion.xlsx
  ```

  Revisa especialmente las hojas donde registraste:

  ```text
  contexto
  evidencia
  afirmaciones
  mensajes ejecutivos
  ```

  Identifica una situación que todavía requiera validación, por ejemplo una variación temporal, una diferencia entre regiones, un canal con comportamiento distinto o una limitación pendiente.

  > **Nota:** Este archivo es el entregable generado al finalizar la Práctica 6. No es un archivo adicional de descarga.
  {: .lab-note .info .compact}

- {% include step_label.html %} En `Problema_Analitico`, define:

  Abre:

  ```text
  C:\DAF\Practica_07\Plantilla_Practica7_Caso_Integral.xlsx
  ```

  y selecciona la hoja:

  ```text
  Problema_Analitico
  ```

  Completa los siguientes campos:

  ```text
  situación observada
  audiencia
  decisión potencial
  pregunta prioritaria
  periodo
  métrica principal
  métricas complementarias
  dimensiones
  criterio de éxito
  ```

  Para cada campo usa esta guía:

  - **situación observada:** describe únicamente lo que ya viste en la evidencia;
  - **audiencia:** indica quién utilizará el análisis para decidir;
  - **decisión potencial:** explica qué decisión podría apoyarse con el análisis;
  - **pregunta prioritaria:** redacta una pregunta medible y sin asumir causas;
  - **periodo:** define exactamente el intervalo que analizarás;
  - **métrica principal:** selecciona la métrica que responderá directamente la pregunta;
  - **métricas complementarias:** agrega solo las métricas necesarias para contextualizar;
  - **dimensiones:** define cómo segmentarás el análisis, por ejemplo `Region`, `Channel` o `Category`;
  - **criterio de éxito:** indica qué evidencia permitiría considerar la pregunta suficientemente respondida.

  > **Importante:** La pregunta no debe presuponer una causa.
  {: .lab-note .important .compact}

  > **Nota:** Evita preguntas como `¿Por qué Online causó la caída?`. Prefiere formulaciones como `¿En qué canales y categorías se concentra la variación de NetSales de Norte entre 2024 y 2025?`.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existe una pregunta analítica concreta, medible y orientada a decisión.
  {: .lab-note .output .compact}

### Tarea 1.3. Formular dos hipótesis

- {% include step_label.html %} Registra `H1` y `H2` en la hoja `Hipotesis`.

  Abre la hoja:

  ```text
  Hipotesis
  ```

  Redacta dos hipótesis que puedan contrastarse con los datos.

  Cada hipótesis debe incluir:

  ```text
  hipótesis
  evidencia que la apoyaría
  evidencia que la debilitaría o descartaría
  fuente o análisis necesario
  ```

  Ejemplo de estructura:

  ```text
  H1: La variación de NetSales de Norte se concentra en determinados canales.
  Evidencia confirmatoria: uno o dos canales explican la mayor parte de la variación.
  Evidencia no confirmatoria: la variación se distribuye de forma similar entre todos los canales.
  ```

  > **Nota:** Una hipótesis es una propuesta que vas a comprobar. No la redactes como si ya fuera una conclusión demostrada.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existen dos hipótesis investigables y no redactadas como conclusiones.
  {: .lab-note .output .compact}

{% assign results = site.data.task-results[page.slug].results %}
{% capture r1 %}{{ results[0] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r1 %}
{% include support-prompt.html task="tarea1" %}

---

## ✅ Tarea 2. Validar alcance y calidad — 8 min

Confirmarás que la fuente curada sigue siendo adecuada para responder la pregunta.

### Tarea 2.1. Ejecutar controles rápidos

- {% include step_label.html %} Abre Snowflake y ejecuta la sección **A. Validación rápida de alcance y calidad** de `07_caso_integral.sql`.

  Inicia sesión en Snowflake y abre un **Worksheet**.

  Abre el archivo:

  ```text
  C:\DAF\Practica_07\07_caso_integral.sql
  ```

  Copia únicamente la sección:

  ```text
  A. Validación rápida de alcance y calidad
  ```

  pégala en el Worksheet y ejecútala.

  Revisa en los resultados:

  ```text
  número de filas
  transacciones
  clientes
  fecha mínima
  fecha máxima
  distribución de QUALITYFLAG
  ```

  Confirma que la consulta usa:

  ```text
  DATA_ANALYTICS_FOUNDATIONS.CURATED.VENTAS_TRANSACCIONES_CURADAS_2026_1
  ```

  > **Nota:** No ejecutes todavía las secciones B, C, D o E. En esta tarea solo debes validar si la fuente tiene el alcance y calidad necesarios para continuar.
  {: .lab-note .info .compact}

  > **Salida esperada:** Se obtienen filas, transacciones, clientes, fechas y distribución de `QUALITYFLAG`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra los resultados en `Control_Calidad`.

  En Excel abre la hoja:

  ```text
  Control_Calidad
  ```

  Copia los valores obtenidos en Snowflake y registra, como mínimo:

  ```text
  filas
  transacciones
  clientes
  fecha mínima
  fecha máxima
  registros VALID
  registros no VALID
  ```

  Si encuentras registros fuera del alcance de tu pregunta, anótalos como observación.

  > **Importante:** Cuantifica registros no válidos; no los ocultes ni los elimines de la evidencia.
  {: .lab-note .important .compact}

  > **Nota:** La población principal del análisis debe conservar `QUALITYFLAG = 'VALID'`, pero debes documentar si existen registros excluidos.
  {: .lab-note .info .compact}

  > **Salida esperada:** El alcance de calidad está documentado.
  {: .lab-note .output .compact}

### Tarea 2.2. Decidir si la fuente es adecuada

- {% include step_label.html %} Evalúa si periodo, volumen y calidad permiten continuar con la pregunta definida.

  Revisa los valores registrados en `Control_Calidad` y compáralos con el periodo y alcance definidos en `Problema_Analitico`.

  Selecciona:

  ```text
  Conforme
  Observación
  Revisar
  ```

  Utiliza estos criterios:

  - **Conforme:** la fuente cubre el periodo y contiene suficiente información válida;
  - **Observación:** la fuente puede utilizarse, pero existe una limitación que debe documentarse;
  - **Revisar:** existe un problema de periodo, calidad o volumen que puede impedir responder correctamente la pregunta.

  Registra junto al estado una breve justificación.

  > **Nota:** Si eliges `Observación`, no necesitas detener la práctica. Continúa dejando explícita la limitación en los siguientes análisis.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existe una conclusión explícita de calidad para el caso.
  {: .lab-note .output .compact}

{% capture r2 %}{{ results[1] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r2 %}
{% include support-prompt.html task="tarea2" %}

---

## 🔎 Tarea 3. Investigar con SQL — 17 min

Contrastarás las hipótesis mediante análisis temporal, segmentación y una profundización seleccionada.

### Tarea 3.1. Analizar el cambio temporal

- {% include step_label.html %} Ejecuta la sección **B. Análisis temporal** del SQL.

  En el mismo Worksheet de Snowflake localiza la sección:

  ```text
  B. Análisis temporal
  ```

  Ejecuta únicamente esa sección y revisa:

  ```text
  NetSales 2024 vs 2025
  NetSales YoY %
  GrossMarginPct
  AvgTicket
  Transactions
  ```

  Lee la salida identificando:

  - si `NetSales` aumenta o disminuye;
  - la magnitud de la variación `YoY %`;
  - si el margen cambia en la misma dirección;
  - si el `AvgTicket` acompaña la variación;
  - si cambia el número de transacciones.

  > **Nota:** No uses un solo indicador para explicar el resultado. La combinación de ventas, margen, ticket y transacciones ayuda a describir mejor qué cambió.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existe evidencia temporal para evaluar la pregunta principal.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra al menos una evidencia temporal en `Matriz_Evidencia`.

  En Excel abre:

  ```text
  Matriz_Evidencia
  ```

  Registra una fila con:

  ```text
  hipótesis relacionada
  análisis realizado
  métrica
  resultado
  comparación
  fuente
  nivel de certeza
  ```

  Copia la magnitud exactamente desde Snowflake e indica contra qué periodo se compara.

  > **Nota:** Evita escribir solamente `las ventas bajaron`. Registra el valor, periodo de referencia y magnitud de la variación.
  {: .lab-note .info .compact}

  > **Salida esperada:** La evidencia incluye magnitud, referencia y nivel de certeza.
  {: .lab-note .output .compact}

### Tarea 3.2. Analizar segmentos

- {% include step_label.html %} Ejecuta la sección **C. Segmentación por canal**.

  En Snowflake ejecuta únicamente:

  ```text
  C. Segmentación por canal
  ```

  Revisa cada `Channel` y compara:

  ```text
  NetSales
  variación
  GrossMarginPct
  AvgTicket
  Transactions
  ```

  Identifica qué canales concentran la mayor diferencia respecto al periodo de comparación.

  > **Nota:** Distingue entre `mayor valor actual` y `mayor contribución a la variación`. No necesariamente representan lo mismo.
  {: .lab-note .info .compact}

  > **Salida esperada:** Se identifican canales que concentran diferencias de ventas, margen o ticket.
  {: .lab-note .output .compact}

- {% include step_label.html %} Relaciona el resultado con `H1` o `H2`.

  Regresa a la hoja `Hipotesis` y compara el resultado real con la evidencia que definiste para confirmar o descartar cada hipótesis.

  Clasifica la evidencia como:

  ```text
  Confirmatoria
  No confirmatoria
  Insuficiente
  ```

  Registra también en `Matriz_Evidencia` qué dato de Snowflake justifica la clasificación.

  > **Nota:** `Confirmatoria` significa que la evidencia observada coincide con lo que la hipótesis predecía; no significa que hayas demostrado causalidad.
  {: .lab-note .info .compact}

  > **Salida esperada:** La primera hipótesis tiene un estado basado en evidencia.
  {: .lab-note .output .compact}

### Tarea 3.3. Profundizar el caso

- {% include step_label.html %} Ejecuta la sección **D. Profundización por categoría** o adapta la consulta a la dimensión que mejor responda tu pregunta.

  Si `Category` ayuda directamente a responder tu pregunta, ejecuta la sección D sin modificaciones.

  Si otra dimensión es más útil, adapta únicamente la agrupación necesaria para analizar:

  ```text
  Category
  Product
  Returned
  Customer
  ```

  Conserva:

  ```text
  QUALITYFLAG = 'VALID'
  mismo periodo
  mismo alcance regional
  mismos filtros principales
  ```

  > **Importante:** Elige la profundización por relevancia para la pregunta, no porque todas las dimensiones deban analizarse.
  {: .lab-note .important .compact}

  > **Nota:** Si modificas la consulta, cambia solo la dimensión de análisis necesaria y evita alterar simultáneamente periodo, población o métrica, porque después será difícil comparar los resultados.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existe evidencia adicional para `H2` o un hallazgo nuevo.
  {: .lab-note .output .compact}

- {% include step_label.html %} Completa al menos cinco filas de `Matriz_Evidencia`.

  Revisa la hoja y confirma que tenga al menos cinco evidencias diferentes.

  Entre las cinco filas procura incluir:

  ```text
  al menos una evidencia temporal
  al menos una evidencia por Channel
  al menos una evidencia de profundización
  evidencia relacionada con H1
  evidencia relacionada con H2
  ```

  Para cada fila registra:

  ```text
  hipótesis
  análisis
  evidencia
  comparación
  fuente
  certeza
  ```

  > **Nota:** Evita duplicar la misma evidencia con textos diferentes. Cada fila debe aportar información nueva al caso.
  {: .lab-note .info .compact}

  > **Salida esperada:** La matriz conecta hipótesis, análisis, evidencia, comparación, fuente y certeza.
  {: .lab-note .output .compact}

{% capture r3 %}{{ results[2] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r3 %}
{% include support-prompt.html task="tarea3" %}

---

## 📊 Tarea 4. Contrastar en Power BI — 12 min

Comprobarás que la evidencia obtenida con SQL sea consistente con el dashboard.

### Tarea 4.1. Crear una copia del PBIX

- {% include step_label.html %} Abre:

  En Power BI Desktop abre:

  ```text
  C:\DAF\Practica_05\05_dashboard_ventas.pbix
  ```

  Espera a que cargue completamente antes de aplicar filtros.

  > **Nota:** Utilizarás el dashboard de la Práctica 5 como punto de partida. No necesitas reconstruir el modelo.
  {: .lab-note .info .compact}

- {% include step_label.html %} Usa **Archivo > Guardar como** y crea:

  En Power BI selecciona:

  ```text
  Archivo
  → Guardar como
  ```

  Guarda la copia como:

  ```text
  C:\DAF\Practica_07\07_caso_integral.pbix
  ```

  Confirma que la barra de título de Power BI muestre el nuevo nombre.

  > **Importante:** A partir de este punto trabaja sobre `07_caso_integral.pbix`, no sobre el archivo original de la Práctica 5.
  {: .lab-note .important .compact}

  > **Salida esperada:** Existe una copia independiente para el proyecto.
  {: .lab-note .output .compact}

### Tarea 4.2. Aplicar el alcance del caso

- {% include step_label.html %} Aplica en Power BI los filtros equivalentes a tu análisis SQL.

  Revisa los filtros que utilizaste en Snowflake y aplica el mismo alcance en Power BI.

  Considera:

  ```text
  periodo
  Region
  Channel
  Category
  ```

  Si una dimensión no forma parte de tu caso, déjala sin restringir.

  Antes de comparar resultados confirma que:

  ```text
  el periodo es el mismo
  Region coincide
  Channel coincide
  Category coincide
  QUALITYFLAG corresponde a la población válida
  ```

  > **Nota:** La validación solo es útil si Snowflake y Power BI están observando exactamente la misma población.
  {: .lab-note .info .compact}

  > **Salida esperada:** El dashboard representa el mismo alcance que las consultas del caso.
  {: .lab-note .output .compact}

- {% include step_label.html %} Ejecuta la sección **E. Plantilla de validación** del SQL con los mismos filtros.

  Regresa a Snowflake y localiza:

  ```text
  E. Plantilla de validación
  ```

  Ajusta únicamente los filtros necesarios para que coincidan con los aplicados en Power BI.

  Ejecuta la consulta y conserva el resultado visible para compararlo con el dashboard.

  > **Nota:** No cambies fórmulas o definiciones de KPI durante esta validación. El objetivo es comprobar consistencia, no crear métricas nuevas.
  {: .lab-note .info .compact}

- {% include step_label.html %} Registra en `Validacion_PowerBI`:

  En Excel abre la hoja:

  ```text
  Validacion_PowerBI
  ```

  Copia desde Power BI y Snowflake:

  ```text
  Ventas netas
  Margen bruto
  Margen %
  Transacciones
  Clientes
  Ticket promedio
  ```

  Registra ambos valores en la misma fila y calcula o verifica la diferencia.

  Usa estas referencias:

  ```text
  conteos → deben coincidir exactamente
  importes → tolerancia máxima de 0.01 cuando corresponda
  porcentajes → misma definición y mismo denominador
  ```

  Si existe una diferencia, revisa primero:

  ```text
  filtros
  periodo
  relaciones
  definición de la medida
  población QUALITYFLAG
  ```

  > **Importante:** Investiga cualquier diferencia material antes de redactar la conclusión.
  {: .lab-note .important .compact}

  > **Salida esperada:** SQL y Power BI coinciden para el mismo alcance o existe una discrepancia documentada.
  {: .lab-note .output .compact}

{% capture r4 %}{{ results[3] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r4 %}
{% include support-prompt.html task="tarea4" %}

---

## 🧭 Tarea 5. Construir la conclusión ejecutiva — 15 min

Convertirás la evidencia validada en tres hallazgos y una recomendación ejecutiva.

### Tarea 5.1. Priorizar hallazgos

- {% include step_label.html %} En `Hallazgos_Cierre`, selecciona los tres hallazgos más útiles para la decisión.

  Abre la hoja:

  ```text
  Hallazgos_Cierre
  ```

  Revisa la `Matriz_Evidencia` y selecciona únicamente tres hallazgos que aporten información distinta y útil para la decisión.

  Para cada uno registra:

  ```text
  evidencia
  interpretación
  nivel de certeza
  recomendación
  limitación
  ```

  Usa estos criterios:

  - **evidencia:** incluye el valor o comparación que observaste;
  - **interpretación:** explica qué significa sin atribuir una causa no demostrada;
  - **nivel de certeza:** alto, medio o bajo según la evidencia disponible;
  - **recomendación:** propone una acción concreta y verificable;
  - **limitación:** indica qué dato o contexto falta.

  > **Nota:** No selecciones tres hallazgos que describan la misma variación. Busca complementariedad entre tiempo, segmento y profundización.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existen tres hallazgos priorizados y trazables.
  {: .lab-note .output .compact}

- {% include step_label.html %} Revisa el estado final de `H1` y `H2`.

  Regresa a la hoja `Hipotesis` y compara cada hipótesis con toda la evidencia reunida, no solo con un resultado aislado.

  Usa:

  ```text
  Confirmatoria
  No confirmatoria
  Insuficiente
  ```

  Escribe junto al estado una justificación breve indicando qué evidencia determinó el cierre.

  > **Nota:** Una hipótesis puede quedar `Insuficiente` aunque existan indicios si falta evidencia para sostenerla con seguridad.
  {: .lab-note .info .compact}

  > **Salida esperada:** Las hipótesis tienen un cierre explícito.
  {: .lab-note .output .compact}

### Tarea 5.2. Redactar la conclusión

- {% include step_label.html %} Escribe una conclusión ejecutiva de 100 a 120 palabras.

  Redacta la conclusión en la sección correspondiente de `Hallazgos_Cierre`.

  Debe responder:

  ```text
  qué ocurrió
  dónde se concentra
  qué evidencia lo sustenta
  qué significa para la decisión
  qué acción conviene tomar
  qué no puede afirmarse todavía
  ```

  Organiza el mensaje en este orden:

  ```text
  1. Hallazgo principal
  2. Segmento o periodo donde se concentra
  3. Evidencia cuantitativa
  4. Implicación para la decisión
  5. Acción recomendada
  6. Limitación o nivel de certeza
  ```

  > **Advertencia:** No conviertas asociación o concentración en causalidad.
  {: .lab-note .warning .compact}

  > **Nota:** Evita frases como `X causó Y` salvo que el análisis realmente contenga evidencia causal. En este proyecto normalmente deberás usar expresiones como `se concentra`, `se observa`, `sugiere` o `requiere validación adicional`.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existe una conclusión ejecutiva proporcional a la evidencia.
  {: .lab-note .output .compact}

- {% include step_label.html %} Define el próximo paso y el dato adicional que sería necesario para aumentar la certeza.

  En la misma hoja registra:

  ```text
  próximo paso
  dato adicional necesario
  responsable o área sugerida
  criterio para volver a evaluar
  ```

  El próximo paso debe ser concreto y verificable, por ejemplo:

  ```text
  revisar DiscountPct por Channel
  validar Currency
  analizar devoluciones por Category
  comparar clientes recurrentes
  ```

  > **Nota:** El dato adicional debe estar directamente relacionado con la principal limitación encontrada en el caso.
  {: .lab-note .info .compact}

  > **Salida esperada:** La recomendación incluye una acción verificable y una limitación.
  {: .lab-note .output .compact}

### Tarea 5.3. Guardar el proyecto

- {% include step_label.html %} Guarda una copia de la plantilla como:

  En Excel selecciona:

  ```text
  Archivo
  → Guardar como
  ```

  Guarda el archivo como:

  ```text
  C:\DAF\Practica_07\07_caso_integral.xlsx
  ```

  > **Nota:** Este archivo será la evidencia documental principal del proyecto integral y se reutilizará en el Reto 7.
  {: .lab-note .info .compact}

- {% include step_label.html %} Guarda el SQL y el PBIX.

  Confirma que existan estos archivos:

  ```text
  C:\DAF\Practica_07\07_caso_integral.sql
  C:\DAF\Practica_07\07_caso_integral.pbix
  ```

  En Power BI usa **Ctrl + S** o **Archivo > Guardar** para conservar los filtros, visuales o ajustes realizados en la copia del proyecto.

  Guarda también cualquier cambio realizado en `07_caso_integral.sql`.

  > **Importante:** No sobrescribas `C:\DAF\Practica_05\05_dashboard_ventas.pbix`.
  {: .lab-note .important .compact}

  > **Salida esperada:** SQL, Excel y PBIX quedan listos para el Reto 7.
  {: .lab-note .output .compact}

{% capture r5 %}{{ results[4] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r5 %}
{% include support-prompt.html task="tarea5" %}