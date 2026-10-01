---
layout: lab
title: "Práctica 3: Análisis descriptivo de ventas y clientes"
permalink: /lab5/lab5/
images_base: /labs/lab5/img
duration: "30 minutos"
objective:
  - Calcular e interpretar métricas descriptivas esenciales sobre la fuente curada de ventas, diferenciando correctamente el análisis a nivel transacción del análisis a nivel cliente.
prerequisites:
  - Haber completado la Práctica 2; Preparar y validar el dataset de ventas.
  - Disponer de la vista DATA_ANALYTICS_FOUNDATIONS.CURATED.VENTAS_TRANSACCIONES_CURADAS_2026_1.
  - Cuenta de Snowflake activa con permisos de lectura sobre el esquema CURATED.
  - Microsoft Excel instalado.
  - Visual Studio Code y Git Bash disponibles.
  - Acceso a Internet para descargar los archivos de la práctica.
introduction:
  - En esta práctica analizarás la población de transacciones válidas preparada en la Práctica 2. Utilizarás Snowflake para calcular estadísticos descriptivos, comparar regiones y canales, estimar tasas de descuento y devolución y cambiar correctamente la unidad de análisis para medir recurrencia de clientes. Finalmente, registrarás y contrastarás resultados en Excel.
slug: lab5
lab_number: 5
final_result: >
  Al finalizar dispondrás de un archivo SQL reproducible y un libro Excel con alcance,
  estadísticos descriptivos, resultados por región y canal, tasas comerciales,
  métricas de recurrencia de clientes y una validación básica de resultados.
notes:
  - Utiliza únicamente registros con QUALITYFLAG = 'VALID'.
  - La unidad de análisis principal es la transacción; para recurrencia cambia a cliente único.
  - Los resultados describen el dataset sintético disponible y no demuestran causalidad.
  - No modifiques los objetos RAW ni CURATED durante esta práctica.
references:
  - text: Snowflake Documentation - Aggregate functions
    url: https://docs.snowflake.com/en/sql-reference/functions-aggregation
  - text: Snowflake Documentation - Workspaces
    url: https://docs.snowflake.com/en/user-guide/ui-snowsight/workspaces
prev: /lab4/lab4/
next: /lab6/lab6/
---

---

<!-- Aquí comienzan las instrucciones paso a paso de la práctica -->

## 📁 Tarea 1. Preparar el análisis y validar la granularidad — 5 min

Prepararás los archivos de trabajo y confirmarás la población, periodo y granularidad antes de calcular métricas descriptivas.

### Tarea 1.1. Descargar y organizar los archivos

Crearás la carpeta de la Práctica 03 y descargarás los recursos que utilizarás durante el análisis.

- {% include step_label.html %} Abre Git Bash y crea la carpeta `Practica_03`.

  ```bash
  mkdir -p /c/DAF/Practica_03
  ```

  > **Salida esperada:** Existe `C:\DAF\Practica_03\`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Descarga la plantilla Excel y el archivo SQL desde las URL proporcionadas.

  1. [Descargar plantilla de resultados](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap3/Plantilla_Practica3_Analisis_Descriptivo.xlsx)
  2. [Descargar SQL de análisis descriptivo](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap3/03_analisis_descriptivo.sql)

  Guarda los archivos como:

  ```text
  C:\DAF\Practica_03\Plantilla_Practica3_Analisis_Descriptivo.xlsx
  C:\DAF\Practica_03\03_analisis_descriptivo.sql
  ```

  > **Salida esperada:** Los dos archivos existen en `C:\DAF\Practica_03\`.
  {: .lab-note .output .compact}

### Tarea 1.2. Validar población y granularidad

Confirmarás que el análisis se realizará sobre transacciones válidas y que los conteos tienen una unidad de análisis explícita.

- {% include step_label.html %} Abre `https://app.snowflake.com`, inicia sesión y accede a **Projects > Workspaces**. Crea un archivo de tipo sql llamado: `03_analisis_descriptivo.sql`.

  > **Nota:** Utiliza tu cuenta de Snowflake con acceso a `DATA_ANALYTICS_FOUNDATIONS.CURATED`.
  {: .lab-note .info .compact}

  > **Salida esperada:** Se muestra Snowflake Workspaces con la sesión autenticada.
  {: .lab-note .output .compact}

- {% include step_label.html %} Abre el SQL File llamado `03_analisis_descriptivo.sql`, copia el contenido del archivo descargado al archivo de snowflake y ejecuta la primera consulta.

  La consulta obtiene:

  ```text
  filas válidas
  transacciones únicas
  clientes únicos
  fecha mínima
  fecha máxima
  ```

  > **Salida esperada:** Se dispone del volumen y cobertura de los registros con `QUALITYFLAG = 'VALID'`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Abre `Plantilla_Practica3_Analisis_Descriptivo.xlsx` y registra los resultados en la hoja `Alcance`.

  > **Importante:** Si el número de filas no coincide con `TransactionID` distintos, no declares automáticamente una fila por transacción. Documenta la diferencia.
  {: .lab-note .important .compact}

  > **Salida esperada:** La hoja `Alcance` contiene población, transacciones, clientes, fechas y granularidad observada.
  {: .lab-note .output .compact}

{% assign results = site.data.task-results[page.slug].results %}
{% capture r1 %}{{ results[0] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r1 %}

{% include support-prompt.html task="tarea1" %}

---

## 📊 Tarea 2. Calcular estadísticos descriptivos — 9 min

Calcularás medidas de tendencia central, posición y extremos para `NetSales`, `Quantity` y `DiscountPct`.

### Tarea 2.1. Ejecutar los estadísticos en Snowflake

Trabajarás con la misma población válida para que las métricas sean comparables.

- {% include step_label.html %} Ejecuta la consulta de **estadísticos descriptivos** incluida en `03_analisis_descriptivo.sql`.

  Para cada variable obtendrás:

  ```text
  N
  Media
  Mediana
  Mínimo
  Máximo
  P25
  P75
  P95
  ```

  > **Salida esperada:** Snowflake devuelve una fila para `NETSALES`, una para `QUANTITY` y una para `DISCOUNTPCT`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra los resultados en la hoja `Estadisticos` de Excel.

  > **Nota:** Para `DiscountPct`, interpreta los valores como proporciones. Por ejemplo, `0.10` representa 10 %.
  {: .lab-note .info .compact}

  > **Salida esperada:** La tabla de estadísticos está completa para las tres variables.
  {: .lab-note .output .compact}

- {% include step_label.html %} Compara media y mediana de `NetSales` y escribe una interpretación breve.

  > **Importante:** Si la media es mayor que la mediana, puede existir asimetría por algunas ventas altas. Esto describe la distribución; no explica su causa.
  {: .lab-note .important .compact}

  > **Salida esperada:** La hoja `Estadisticos` contiene una interpretación basada en media y mediana.
  {: .lab-note .output .compact}

### Tarea 2.2. Interpretar percentiles

Usarás los percentiles para reconocer valores centrales y umbrales altos sin tratar el máximo como valor típico.

- {% include step_label.html %} Verifica en Excel que para cada variable se cumpla `P25 <= Mediana <= P75 <= P95`.

  > **Salida esperada:** Los percentiles tienen un orden lógico y no presentan inconsistencias evidentes.
  {: .lab-note .output .compact}

- {% include step_label.html %} Describe qué representa el P95 de `NetSales` en una frase.

  > **Nota:** Una interpretación válida es que aproximadamente 95 % de las transacciones válidas tiene una venta neta igual o inferior a ese valor.
  {: .lab-note .info .compact}

  > **Salida esperada:** El P95 se interpreta como posición dentro de la distribución y no como objetivo comercial.
  {: .lab-note .output .compact}

{% capture r2 %}{{ results[1] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r2 %}

{% include support-prompt.html task="tarea2" %}

---

## 🌎 Tarea 3. Analizar segmentos y tasas comerciales — 8 min

Compararás actividad y ventas por región y canal, y calcularás tasas globales de descuento y devolución.

### Tarea 3.1. Comparar regiones y canales

Evitarás usar una única métrica para describir todos los aspectos del desempeño comercial.

- {% include step_label.html %} Ejecuta la consulta por `Region` y copia los resultados a la hoja `Segmentos_Tasas`.

  Registra:

  ```text
  transacciones
  clientes únicos
  venta neta total
  venta neta promedio
  ```

  > **Salida esperada:** Existe una tabla comparativa por región.
  {: .lab-note .output .compact}

- {% include step_label.html %} Ejecuta la consulta por `Channel` y registra los resultados en la misma hoja.

  La consulta incluye:

  ```text
  transacciones
  venta neta total
  venta neta promedio
  devoluciones
  tasa de devolución
  ```

  > **Salida esperada:** Existe una tabla comparativa por canal con su tasa de devolución.
  {: .lab-note .output .compact}

- {% include step_label.html %} Identifica un ejemplo donde `SUM(NetSales)` y `AVG(NetSales)` podrían llevar a interpretaciones distintas.

  > **Advertencia:** El segmento con mayor venta total no necesariamente tiene la venta promedio más alta.
  {: .lab-note .warning .compact}

  > **Salida esperada:** Se documenta al menos una diferencia de interpretación entre volumen total y promedio.
  {: .lab-note .output .compact}

### Tarea 3.2. Calcular tasas globales

Calcularás proporciones observadas sobre la población válida.

- {% include step_label.html %} Ejecuta la consulta de **tasas globales** de descuento y devolución.

  > **Salida esperada:** Obtienes total de transacciones, tasa de descuento y tasa de devolución.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra las tasas como porcentajes en `Segmentos_Tasas`.

  > **Importante:** Una tasa debe interpretarse junto con el número de transacciones que forma su denominador.
  {: .lab-note .important .compact}

  > **Salida esperada:** Las tasas se encuentran entre 0 % y 100 % y están acompañadas por el volumen analizado.
  {: .lab-note .output .compact}

{% capture r3 %}{{ results[2] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r3 %}

{% include support-prompt.html task="tarea3" %}

---

## 👥 Tarea 4. Analizar recurrencia y validar resultados — 8 min

Cambiarás la unidad de análisis de transacción a cliente y documentarás una validación básica entre Snowflake y Excel.

### Tarea 4.1. Calcular recurrencia de clientes

Agruparás las transacciones por cliente antes de calcular frecuencia y recurrencia.

- {% include step_label.html %} Ejecuta la consulta `customer_frequency` incluida al final del archivo SQL.

  Obtendrás:

  ```text
  clientes
  clientes recurrentes
  proporción de clientes recurrentes
  frecuencia promedio
  frecuencia mediana
  frecuencia máxima
  ```

  > **Salida esperada:** Snowflake devuelve un resumen calculado a nivel cliente.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra los resultados en la hoja `Clientes`.

  > **Importante:** El denominador de la recurrencia es el número de clientes únicos, no el número de transacciones.
  {: .lab-note .important .compact}

  > **Salida esperada:** La hoja `Clientes` contiene todas las métricas de recurrencia.
  {: .lab-note .output .compact}

- {% include step_label.html %} Escribe una interpretación responsable de la proporción de clientes recurrentes.

  > **Advertencia:** Esta proporción describe el periodo analizado; no es una predicción de recompra futura.
  {: .lab-note .warning .compact}

  > **Salida esperada:** La interpretación diferencia claramente proporción histórica y probabilidad futura.
  {: .lab-note .output .compact}

### Tarea 4.2. Validar y guardar el entregable

Contrastarás resultados clave antes de cerrar la práctica.

- {% include step_label.html %} Completa la hoja `Validacion` con al menos cuatro métricas obtenidas en Snowflake.

  Puedes registrar:

  ```text
  transacciones válidas
  clientes únicos
  venta neta promedio
  venta neta mediana
  tasa de descuento
  tasa de devoluciones
  ```

  > **Nota:** Excel se utiliza aquí como expediente de contraste. No necesitas importar todas las transacciones.
  {: .lab-note .info .compact}

  > **Salida esperada:** La hoja `Validacion` contiene al menos cuatro métricas documentadas.
  {: .lab-note .output .compact}

- {% include step_label.html %} Guarda una copia editable del libro como `03_resultados_descriptivos.xlsx`.

  Guarda en:

  ```text
  C:\DAF\Practica_03\03_resultados_descriptivos.xlsx
  ```

  > **Salida esperada:** El libro final existe en la ruta indicada.
  {: .lab-note .output .compact}

- {% include step_label.html %} Guarda `03_analisis_descriptivo.sql` en VS Code y conserva ambos archivos para la Práctica 4.

  > **Nota:** Los resultados descriptivos serán la base para elegir comparaciones y preguntas de exploración posteriores.
  {: .lab-note .info .compact}

  > **Salida esperada:** `03_analisis_descriptivo.sql` y `03_resultados_descriptivos.xlsx` están guardados y listos para reutilizarse.
  {: .lab-note .output .compact}

{% capture r4 %}{{ results[3] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r4 %}

{% include support-prompt.html task="tarea4" %}