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
  - text: Dashboard construido en la Práctica 5
    url: URL_DASHBOARD_PRACTICA_05
  - text: Brief de interpretación de la Práctica 6
    url: URL_BRIEF_PRACTICA_06
prev: /reto6/reto6/
next: /reto7/reto7/
---

---

## 🎯 Tarea 1. Definir el problema y las hipótesis — 8 min

Transformarás una preocupación comercial en una pregunta medible y dos hipótesis investigables.

### Tarea 1.1. Preparar el proyecto

- {% include step_label.html %} Abre Git Bash y crea la carpeta `Practica_07`.

  ```bash
  mkdir -p /c/DAF/Practica_07
  ```

  > **Salida esperada:** Existe `C:\DAF\Practica_07\`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Descarga los archivos auxiliares.

  1. [Descargar SQL del caso integral](URL_SQL_PRACTICA_07)
  2. [Descargar plantilla del caso integral](URL_PLANTILLA_PRACTICA_07)

  Guarda:

  ```text
  C:\DAF\Practica_07\07_caso_integral.sql
  C:\DAF\Practica_07\Plantilla_Practica7_Caso_Integral.xlsx
  ```

  > **Salida esperada:** SQL y plantilla están disponibles localmente.
  {: .lab-note .output .compact}

### Tarea 1.2. Definir la pregunta

- {% include step_label.html %} Abre `C:\DAF\Practica_06\06_brief_interpretacion.xlsx` y revisa hallazgos, limitaciones y preguntas pendientes.

- {% include step_label.html %} En `Problema_Analitico`, define:

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

  > **Importante:** La pregunta no debe presuponer una causa.
  {: .lab-note .important .compact}

  > **Salida esperada:** Existe una pregunta analítica concreta, medible y orientada a decisión.
  {: .lab-note .output .compact}

### Tarea 1.3. Formular dos hipótesis

- {% include step_label.html %} Registra `H1` y `H2` en la hoja `Hipotesis`.

  Cada una debe indicar qué evidencia permitiría confirmarla o descartarla.

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

  > **Salida esperada:** Se obtienen filas, transacciones, clientes, fechas y distribución de `QUALITYFLAG`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra los resultados en `Control_Calidad`.

  > **Importante:** Cuantifica registros no válidos; no los ocultes ni los elimines de la evidencia.
  {: .lab-note .important .compact}

  > **Salida esperada:** El alcance de calidad está documentado.
  {: .lab-note .output .compact}

### Tarea 2.2. Decidir si la fuente es adecuada

- {% include step_label.html %} Evalúa si periodo, volumen y calidad permiten continuar con la pregunta definida.

  Selecciona:

  ```text
  Conforme
  Observación
  Revisar
  ```

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

  Revisa:

  ```text
  NetSales 2024 vs 2025
  NetSales YoY %
  GrossMarginPct
  AvgTicket
  Transactions
  ```

  > **Salida esperada:** Existe evidencia temporal para evaluar la pregunta principal.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra al menos una evidencia temporal en `Matriz_Evidencia`.

  > **Salida esperada:** La evidencia incluye magnitud, referencia y nivel de certeza.
  {: .lab-note .output .compact}

### Tarea 3.2. Analizar segmentos

- {% include step_label.html %} Ejecuta la sección **C. Segmentación por canal**.

  > **Salida esperada:** Se identifican canales que concentran diferencias de ventas, margen o ticket.
  {: .lab-note .output .compact}

- {% include step_label.html %} Relaciona el resultado con `H1` o `H2`.

  Clasifica la evidencia como:

  ```text
  Confirmatoria
  No confirmatoria
  Insuficiente
  ```

  > **Salida esperada:** La primera hipótesis tiene un estado basado en evidencia.
  {: .lab-note .output .compact}

### Tarea 3.3. Profundizar el caso

- {% include step_label.html %} Ejecuta la sección **D. Profundización por categoría** o adapta la consulta a la dimensión que mejor responda tu pregunta.

  Puedes profundizar en:

  ```text
  Category
  Product
  Returned
  Customer
  ```

  > **Importante:** Elige la profundización por relevancia para la pregunta, no porque todas las dimensiones deban analizarse.
  {: .lab-note .important .compact}

  > **Salida esperada:** Existe evidencia adicional para `H2` o un hallazgo nuevo.
  {: .lab-note .output .compact}

- {% include step_label.html %} Completa al menos cinco filas de `Matriz_Evidencia`.

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

  ```text
  C:\DAF\Practica_05\05_dashboard_ventas.pbix
  ```

- {% include step_label.html %} Usa **Archivo > Guardar como** y crea:

  ```text
  C:\DAF\Practica_07\07_caso_integral.pbix
  ```

  > **Salida esperada:** Existe una copia independiente para el proyecto.
  {: .lab-note .output .compact}

### Tarea 4.2. Aplicar el alcance del caso

- {% include step_label.html %} Aplica en Power BI los filtros equivalentes a tu análisis SQL.

  Considera:

  ```text
  periodo
  Region
  Channel
  Category
  ```

  > **Salida esperada:** El dashboard representa el mismo alcance que las consultas del caso.
  {: .lab-note .output .compact}

- {% include step_label.html %} Ejecuta la sección **E. Plantilla de validación** del SQL con los mismos filtros.

- {% include step_label.html %} Registra en `Validacion_PowerBI`:

  ```text
  Ventas netas
  Margen bruto
  Margen %
  Transacciones
  Clientes
  Ticket promedio
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

  Para cada uno registra:

  ```text
  evidencia
  interpretación
  nivel de certeza
  recomendación
  limitación
  ```

  > **Salida esperada:** Existen tres hallazgos priorizados y trazables.
  {: .lab-note .output .compact}

- {% include step_label.html %} Revisa el estado final de `H1` y `H2`.

  Usa:

  ```text
  Confirmatoria
  No confirmatoria
  Insuficiente
  ```

  > **Salida esperada:** Las hipótesis tienen un cierre explícito.
  {: .lab-note .output .compact}

### Tarea 5.2. Redactar la conclusión

- {% include step_label.html %} Escribe una conclusión ejecutiva de 100 a 120 palabras.

  Debe responder:

  ```text
  qué ocurrió
  dónde se concentra
  qué evidencia lo sustenta
  qué significa para la decisión
  qué acción conviene tomar
  qué no puede afirmarse todavía
  ```

  > **Advertencia:** No conviertas asociación o concentración en causalidad.
  {: .lab-note .warning .compact}

  > **Salida esperada:** Existe una conclusión ejecutiva proporcional a la evidencia.
  {: .lab-note .output .compact}

- {% include step_label.html %} Define el próximo paso y el dato adicional que sería necesario para aumentar la certeza.

  > **Salida esperada:** La recomendación incluye una acción verificable y una limitación.
  {: .lab-note .output .compact}

### Tarea 5.3. Guardar el proyecto

- {% include step_label.html %} Guarda una copia de la plantilla como:

  ```text
  C:\DAF\Practica_07\07_caso_integral.xlsx
  ```

- {% include step_label.html %} Guarda el SQL y el PBIX.

  ```text
  C:\DAF\Practica_07\07_caso_integral.sql
  C:\DAF\Practica_07\07_caso_integral.pbix
  ```

  > **Salida esperada:** SQL, Excel y PBIX quedan listos para el Reto 7.
  {: .lab-note .output .compact}

{% capture r5 %}{{ results[4] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r5 %}
{% include support-prompt.html task="tarea5" %}