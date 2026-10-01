---
layout: lab
title: "Reto 4: Investigar una región de bajo desempeño"
permalink: /lab8/lab8/
images_base: /labs/lab8/img
duration: "35 minutos"
objective:
  - Investigar de forma autónoma si una región presenta bajo desempeño, localizar dónde se concentra la desviación y formular una recomendación sustentada en evidencia.
prerequisites:
  - Haber completado la Práctica 4; Exploración del desempeño comercial.
  - Disponer de la vista DATA_ANALYTICS_FOUNDATIONS.CURATED.VENTAS_TRANSACCIONES_CURADAS_2026_1.
  - Cuenta de Snowflake activa con permisos de lectura sobre CURATED.
  - Microsoft Excel instalado.
  - Acceso a Internet para descargar los archivos del reto.
introduction:
  - La dirección comercial considera que la región Norte podría estar presentando un desempeño inferior durante 2025. Tu responsabilidad será verificar si la señal existe, decidir con qué métricas debe evaluarse, identificar los meses y segmentos donde se concentra y redactar una conclusión prudente. No debes asumir que Norte está deteriorándose antes de revisar la evidencia.
slug: lab8
lab_number: 8
final_result: >
  Al finalizar habrás documentado si la región Norte presenta o no una desviación relevante,
  qué métricas la sustentan, en qué meses, canales o categorías se concentra, qué controles
  validan la señal y qué acción comercial o analítica conviene priorizar.
notes:
  - Utiliza registros con QUALITYFLAG = 'VALID' para las comparaciones principales.
  - Bajo desempeño debe definirse mediante métricas; no es una categoría automática.
  - Compara 2025 frente a 2024 con criterios equivalentes.
  - Una asociación o concentración observada no demuestra causalidad.
references:
  - text: Snowflake Documentation - Window functions
    url: https://docs.snowflake.com/en/sql-reference/functions-analytic
  - text: Snowflake Documentation - Workspaces
    url: https://docs.snowflake.com/en/user-guide/ui-snowsight/workspaces
prev: /lab7/lab7/
next: /lab9/lab9/
---

---

<!-- Aquí comienzan las instrucciones paso a paso del reto -->

## 🎯 Tarea 1. Definir la investigación — 5 min

Prepararás los archivos y definirás qué significa bajo desempeño antes de consultar los datos.

### Tarea 1.1. Preparar los recursos

- {% include step_label.html %} Abre Git Bash y crea la carpeta `Reto_04`.

  ```bash
  mkdir -p /c/DAF/Reto_04
  ```

  > **Salida esperada:** Existe `C:\DAF\Reto_04\`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Descarga la plantilla y el SQL del reto.

  1. [Descargar plantilla del Reto 4](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap4/Plantilla_Reto4_Region_Bajo_Desempeno.xlsx)
  2. [Descargar SQL del Reto 4](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap4/04_reto_region_bajo_desempeno.sql)

  Guarda los archivos como:

  ```text
  C:\DAF\Reto_04\Plantilla_Reto4_Region_Bajo_Desempeno.xlsx
  C:\DAF\Reto_04\04_reto_region_bajo_desempeno.sql
  ```

  > **Salida esperada:** Ambos archivos existen en la carpeta del reto.
  {: .lab-note .output .compact}

### Tarea 1.2. Definir hipótesis y métricas

- {% include step_label.html %} Abre la plantilla Excel y registra una hipótesis inicial sobre Norte.

  > **Advertencia:** Formula la hipótesis como posibilidad, no como conclusión confirmada.
  {: .lab-note .warning .compact}

  > **Salida esperada:** Existe una hipótesis inicial pendiente de validación.
  {: .lab-note .output .compact}

- {% include step_label.html %} Define qué considerarás `bajo desempeño` usando al menos tres métricas.

  Puedes considerar:

  ```text
  variación de NetSales
  GrossMarginPct
  AvgTicket
  Transaction count
  Customer count
  ```

  > **Importante:** No uses una sola métrica como sinónimo universal de desempeño.
  {: .lab-note .important .compact}

  > **Salida esperada:** La hoja `Hipotesis_Metricas` contiene tres métricas y su comparativo.
  {: .lab-note .output .compact}

{% assign results = site.data.task-results[page.slug].results %}
{% capture r1 %}{{ results[0] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r1 %}
{% include support-prompt.html task="tarea1" %}

---

## 📊 Tarea 2. Confirmar si existe la desviación — 9 min

Compararás Norte frente al resto de regiones y frente a su propio resultado de 2024.

### Tarea 2.1. Comparar regiones

- {% include step_label.html %} Abre `https://app.snowflake.com`, entra a **Projects > Workspaces** y crea el archivo `04_reto_region_bajo_desempeno.sql`.

  > **Salida esperada:** El archivo SQL está listo para ejecutarse en Snowflake.
  {: .lab-note .output .compact}

- {% include step_label.html %} Abre el archivo descargado `04_reto_region_bajo_desempeno.sql` y copia el contenido al archivo de snowflake. 

- {% include step_label.html %} Ejecuta la consulta regional 2024 vs 2025.

  Revisa:

  ```text
  NetSales YoY %
  GrossMarginPct
  Transaction count
  Customer count
  AvgTicket
  ```

  > **Salida esperada:** Se dispone de una comparación anual por región.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra los resultados principales en `Comparacion_Regional`.

  > **Importante:** Comprueba si Norte realmente presenta una desviación y si depende de la métrica elegida.
  {: .lab-note .important .compact}

  > **Salida esperada:** La hoja permite comparar Norte con las demás regiones.
  {: .lab-note .output .compact}

### Tarea 2.2. Localizar el periodo

- {% include step_label.html %} Ejecuta la consulta mensual de Norte 2024 vs 2025.

  > **Salida esperada:** Se obtienen variaciones YoY por mes.
  {: .lab-note .output .compact}

- {% include step_label.html %} Identifica los meses donde la diferencia de `NetSales` es más negativa o más relevante.

  > **Salida esperada:** Se documenta el periodo donde se concentra la señal.
  {: .lab-note .output .compact}

- {% include step_label.html %} Revisa si la caída de ventas coincide con cambios en margen, ticket o transacciones.

  > **Advertencia:** Si las métricas se mueven de forma distinta, evita resumir el caso únicamente como “caída de ventas”.
  {: .lab-note .warning .compact}

  > **Salida esperada:** La interpretación distingue volumen, margen, ticket y actividad.
  {: .lab-note .output .compact}

{% capture r2 %}{{ results[1] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r2 %}
{% include support-prompt.html task="tarea2" %}

---

## 🔎 Tarea 3. Descomponer Norte por canal y categoría — 10 min

Buscarás qué segmentos contribuyen en mayor medida a la desviación observada.

### Tarea 3.1. Analizar canales

- {% include step_label.html %} Ejecuta la consulta de Norte 2025 por `Channel`.

  Compara:

  ```text
  NetSales
  GrossMarginPct
  AvgTicket
  Transactions
  ReturnRate
  ```

  > **Salida esperada:** Se dispone de una comparación entre canales de Norte.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra en `Descomposicion_Norte` los canales con resultados más relevantes.

  > **Salida esperada:** La hoja muestra qué canal concentra la señal o si está distribuida.
  {: .lab-note .output .compact}

- {% include step_label.html %} Determina si el canal con menor venta también presenta menor margen, ticket o mayor devolución.

  > **Importante:** No confundas bajo volumen con bajo desempeño relativo.
  {: .lab-note .important .compact}

  > **Salida esperada:** Existe una interpretación basada en más de un KPI.
  {: .lab-note .output .compact}

### Tarea 3.2. Analizar categorías

- {% include step_label.html %} Ejecuta la consulta de Norte 2025 por `Category`.

  > **Salida esperada:** Se dispone de ventas, unidades, margen y ticket por categoría.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra las categorías con menor desempeño según las métricas definidas en la Tarea 1.

  > **Salida esperada:** La hoja contiene las categorías que explican o concentran parte de la señal.
  {: .lab-note .output .compact}

- {% include step_label.html %} Selecciona el canal o categoría que merece mayor investigación adicional.

  > **Salida esperada:** Se identifica un segmento prioritario con evidencia cuantitativa.
  {: .lab-note .output .compact}

{% capture r3 %}{{ results[2] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r3 %}
{% include support-prompt.html task="tarea3" %}

---

## ✅ Tarea 4. Validar la señal — 6 min

Comprobarás que la conclusión no dependa de cobertura incompleta, registros en revisión o denominadores inconsistentes.

### Tarea 4.1. Ejecutar controles

- {% include step_label.html %} Ejecuta la consulta de validación de Norte incluida al final del SQL.

  Revisa:

  ```text
  filas
  transacciones únicas
  clientes únicos
  cobertura temporal
  devoluciones
  registros REVIEW
  ```

  > **Salida esperada:** Se dispone de evidencia para evaluar la confiabilidad de la señal.
  {: .lab-note .output .compact}

- {% include step_label.html %} Completa la hoja `Validacion` y clasifica cada control.

  Usa:

  ```text
  Cumple
  Observación
  No cumple
  ```

  > **Salida esperada:** Todos los controles tienen estado e impacto documentado.
  {: .lab-note .output .compact}

- {% include step_label.html %} Decide si la señal puede considerarse validada, parcial o requiere revisión adicional.

  > **Importante:** Una señal con problemas de cobertura o comparabilidad no debe presentarse como conclusión definitiva.
  {: .lab-note .important .compact}

  > **Salida esperada:** Existe una conclusión de validación explícita.
  {: .lab-note .output .compact}

{% capture r4 %}{{ results[3] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r4 %}
{% include support-prompt.html task="tarea4" %}

---

## 🧭 Tarea 5. Redactar conclusión y recomendación — 5 min

Transformarás la evidencia en un hallazgo útil para el negocio sin exceder lo que los datos permiten afirmar.

### Tarea 5.1. Cerrar la investigación

- {% include step_label.html %} En la hoja `Conclusion`, indica si existe bajo desempeño en Norte.

  Selecciona:

  ```text
  Sí
  No
  Parcial / depende de la métrica
  ```

  > **Salida esperada:** Existe una respuesta explícita sustentada en los controles anteriores.
  {: .lab-note .output .compact}

- {% include step_label.html %} Escribe la evidencia principal incluyendo métrica, magnitud, periodo y segmento.

  > **Salida esperada:** La conclusión contiene evidencia cuantitativa trazable.
  {: .lab-note .output .compact}

- {% include step_label.html %} Redacta una interpretación prudente y una acción recomendada.

  > **Advertencia:** No atribuyas la desviación a promociones, inventario, precio u otras variables que no hayan sido medidas.
  {: .lab-note .warning .compact}

  > **Salida esperada:** Existe una recomendación orientada a revisar, priorizar o investigar el segmento identificado.
  {: .lab-note .output .compact}

- {% include step_label.html %} Guarda una copia final como `04_reto_region_bajo_desempeno.xlsx`.

  Guarda en:

  ```text
  C:\DAF\Reto_04\04_reto_region_bajo_desempeno.xlsx
  ```

  > **Salida esperada:** El archivo contiene hipótesis, evidencia, validación, conclusión y recomendación.
  {: .lab-note .output .compact}

{% capture r5 %}{{ results[4] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r5 %}
{% include support-prompt.html task="tarea5" %}