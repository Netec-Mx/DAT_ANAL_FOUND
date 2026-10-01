---
layout: lab
title: "Práctica 4: Exploración del desempeño comercial"
permalink: /lab7/lab7/
images_base: /labs/lab7/img
duration: "33 minutos"
objective:
  - Identificar, validar y priorizar señales comerciales a partir de tendencias temporales, comparaciones por segmento y relaciones entre volumen y margen, preparando los insumos del dashboard de la Práctica 5.
prerequisites:
  - Haber completado las Prácticas 1, 2 y 3.
  - Disponer de la vista DATA_ANALYTICS_FOUNDATIONS.CURATED.VENTAS_TRANSACCIONES_CURADAS_2026_1.
  - Conservar los resultados de la Práctica 3.
  - Cuenta de Snowflake activa con permisos de lectura sobre CURATED.
  - Microsoft Excel instalado.
  - Visual Studio Code y Git Bash disponibles.
  - Acceso a Internet para descargar los archivos de la práctica.
introduction:
  - En esta práctica aplicarás el flujo preguntar, explorar, comparar, validar y concluir sobre la fuente curada. Analizarás tendencias mensuales, compararás regiones y canales, identificarás un producto de alto volumen y bajo margen y documentarás tres señales comerciales. Al final seleccionarás los KPI y visualizaciones que servirán como entrada para el dashboard de Power BI de la Práctica 5.
slug: lab7
lab_number: 7
final_result: >
  Al finalizar dispondrás de un archivo SQL reproducible y un libro Excel con definiciones
  de KPI, tendencias mensuales, comparaciones por región y canal, tres señales validadas
  y un conjunto de insumos priorizados para construir el dashboard de la Práctica 5.
notes:
  - Utiliza únicamente registros con QUALITYFLAG = 'VALID'.
  - Una señal observada no equivale a una causa confirmada.
  - El margen porcentual se calcula como SUM(GrossMargin) / SUM(NetSales).
  - El ticket promedio se calcula con TransactionID como unidad transaccional.
  - No modifiques objetos de RAW ni CURATED.
references:
  - text: Snowflake Documentation - Window functions
    url: https://docs.snowflake.com/en/sql-reference/functions-analytic
  - text: Snowflake Documentation - Workspaces
    url: https://docs.snowflake.com/en/user-guide/ui-snowsight/workspaces
prev: /lab6/lab6/
next: /lab8/lab8/
---

---

## 📁 Tarea 1. Preparar la exploración y los KPI — 5 min

Prepararás los archivos de trabajo y confirmarás las definiciones de KPI antes de explorar tendencias o segmentos.

### Tarea 1.1. Descargar y organizar los archivos

- {% include step_label.html %} Abre Git Bash y crea la carpeta `Practica_04`.

  ```bash
  mkdir -p /c/DAF/Practica_04
  ```

  > **Salida esperada:** Existe `C:\DAF\Practica_04\`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Descarga la plantilla Excel y el archivo SQL.

  1. [Descargar plantilla de la Práctica 4](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap4/Plantilla_Practica4_Exploracion_Desempeno.xlsx)
  2. [Descargar SQL de exploración](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap4/04_exploracion_desempeno.sql)

  Guarda los archivos como:

  ```text
  C:\DAF\Practica_04\Plantilla_Practica4_Exploracion_Desempeno.xlsx
  C:\DAF\Practica_04\04_exploracion_desempeno.sql
  ```

  > **Salida esperada:** Ambos archivos existen en `C:\DAF\Practica_04\`.
  {: .lab-note .output .compact}

### Tarea 1.2. Confirmar fuente y KPI

- {% include step_label.html %} Abre `https://app.snowflake.com`, inicia sesión y accede a **Projects > Workspaces**.

  > **Salida esperada:** Se muestra Snowflake Workspaces con acceso a `DATA_ANALYTICS_FOUNDATIONS.CURATED`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Crea un SQL File llamado `04_exploracion_desempeno.sql`, copia el contenido del archivo descargado y ejecuta la primera consulta.

  > **Salida esperada:** Se muestran filas válidas, transacciones, clientes, fechas, ventas netas y margen bruto.
  {: .lab-note .output .compact}

- {% include step_label.html %} Abre la plantilla Excel y revisa la hoja `KPI`.

  Confirma:

  ```text
  Margen % = SUM(GrossMargin) / SUM(NetSales)
  Ticket promedio = SUM(NetSales) / COUNT(DISTINCT TransactionID)
  ```

  > **Importante:** No promedies porcentajes de margen calculados por fila.
  {: .lab-note .important .compact}

  > **Salida esperada:** Las definiciones de KPI están validadas.
  {: .lab-note .output .compact}

{% assign results = site.data.task-results[page.slug].results %}
{% capture r1 %}{{ results[0] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r1 %}
{% include support-prompt.html task="tarea1" %}

---

## 📈 Tarea 2. Explorar la tendencia mensual — 9 min

Analizarás la evolución mensual de ventas y margen para detectar cambios que requieran revisión.

### Tarea 2.1. Calcular la tendencia

- {% include step_label.html %} Ejecuta la **consulta mensual** incluida en `04_exploracion_desempeno.sql`.

  > **Salida esperada:** Se obtienen 24 meses de resultados con ventas, margen, unidades, clientes, ticket y variaciones.
  {: .lab-note .output .compact}

- {% include step_label.html %} Copia los meses más relevantes en la hoja `Tendencia`.

  > **Nota:** Registra los meses necesarios para sustentar la señal seleccionada.
  {: .lab-note .info .compact}

  > **Salida esperada:** La hoja contiene evidencia temporal suficiente.
  {: .lab-note .output .compact}

### Tarea 2.2. Identificar la señal temporal

- {% include step_label.html %} Identifica el mes con la mayor caída de `NetSales` y el mes con el mayor crecimiento.

  > **Salida esperada:** Se registran ambos meses y sus variaciones porcentuales.
  {: .lab-note .output .compact}

- {% include step_label.html %} Compara la dirección de ventas y margen en el mes seleccionado.

  > **Advertencia:** Una caída conjunta es una señal, no una causa demostrada.
  {: .lab-note .warning .compact}

  > **Salida esperada:** Existe una interpretación breve.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra la señal `S1` en `Senales`.

  > **Salida esperada:** `S1` contiene métrica, periodo, evidencia, estado y limitación.
  {: .lab-note .output .compact}

{% capture r2 %}{{ results[1] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r2 %}
{% include support-prompt.html task="tarea2" %}

---

## 🌎 Tarea 3. Comparar segmentos y margen — 9 min

Explorarás regiones, canales y productos para localizar dónde se concentra una señal comercial.

### Tarea 3.1. Comparar región y canal

- {% include step_label.html %} Ejecuta la consulta por `Region` para 2025 y registra los segmentos más relevantes en `Segmentos`.

  > **Salida esperada:** Se dispone de una comparación consistente entre regiones.
  {: .lab-note .output .compact}

- {% include step_label.html %} Ejecuta la consulta por `Channel` para 2025 y registra los resultados principales.

  > **Salida esperada:** Se dispone de una comparación equivalente entre canales.
  {: .lab-note .output .compact}

- {% include step_label.html %} Selecciona una región o canal cuya lectura cambie al comparar ventas netas, margen % o ticket promedio y registra `S2`.

  > **Importante:** Un segmento con ventas altas puede presentar margen % o ticket inferiores.
  {: .lab-note .important .compact}

  > **Salida esperada:** `S2` contiene una desviación sustentada con al menos dos KPI.
  {: .lab-note .output .compact}

### Tarea 3.2. Identificar un producto de alto volumen y bajo margen

- {% include step_label.html %} Ejecuta la consulta `product_summary` incluida en el SQL.

  > **Salida esperada:** Se muestran productos ubicados en alto volumen y bajo margen.
  {: .lab-note .output .compact}

- {% include step_label.html %} Selecciona un producto candidato y registra `S3` en `Senales`.

  > **Advertencia:** No atribuyas el margen bajo a descuentos, costos o precio sin evidencia adicional.
  {: .lab-note .warning .compact}

  > **Salida esperada:** `S3` contiene producto, unidades, ventas, margen % y periodo.
  {: .lab-note .output .compact}

{% capture r3 %}{{ results[2] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r3 %}
{% include support-prompt.html task="tarea3" %}

---

## ✅ Tarea 4. Validar y priorizar hallazgos — 10 min

Validarás las tres señales y seleccionarás los insumos que deberán aparecer en el dashboard de la Práctica 5.

### Tarea 4.1. Validar las señales

- {% include step_label.html %} Ejecuta la consulta de **cobertura mensual** incluida al final del SQL.

  > **Salida esperada:** Se dispone de días con datos y transacciones por mes.
  {: .lab-note .output .compact}

- {% include step_label.html %} Revisa `S1`, `S2` y `S3` y marca cada una como `Validada` o `Revisar`.

  > **Importante:** Una señal solo se valida si periodo, filtros, denominadores y población son consistentes.
  {: .lab-note .important .compact}

  > **Salida esperada:** Las tres señales tienen estado y limitación.
  {: .lab-note .output .compact}

### Tarea 4.2. Priorizar para el dashboard

- {% include step_label.html %} En `Dashboard_Input`, asigna prioridad `Alta`, `Media` o `Baja` a los KPI y hallazgos.

  > **Salida esperada:** Los KPI y hallazgos tienen prioridad explícita.
  {: .lab-note .output .compact}

- {% include step_label.html %} Selecciona dos hallazgos principales y define para cada uno una visualización y segmentadores.

  > **Nota:** Cada visualización de la Práctica 5 debe responder a una pregunta o hallazgo documentado aquí.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existen al menos dos hallazgos listos para convertirse en visualizaciones.
  {: .lab-note .output .compact}

- {% include step_label.html %} Guarda una copia editable del libro como `04_exploracion_desempeno.xlsx`.

  Guarda en:

  ```text
  C:\DAF\Practica_04\04_exploracion_desempeno.xlsx
  ```

  > **Salida esperada:** El archivo final contiene KPI, tendencia, segmentos, señales y entradas para dashboard.
  {: .lab-note .output .compact}

- {% include step_label.html %} Guarda `04_exploracion_desempeno.sql` en VS Code y conserva ambos archivos para la Práctica 5.

  > **Salida esperada:** El SQL y el Excel están guardados y listos para reutilizarse.
  {: .lab-note .output .compact}

{% capture r4 %}{{ results[3] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r4 %}
{% include support-prompt.html task="tarea4" %}
