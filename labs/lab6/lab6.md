---
layout: lab
title: "Reto 3: Elegir la métrica correcta"
permalink: /lab6/lab6/
images_base: /labs/lab6/img
duration: "30 minutos"
objective:
  - Seleccionar, calcular y justificar la métrica adecuada para responder preguntas comerciales distintas sin confundir volumen, promedio, tasa o granularidad.
prerequisites:
  - Haber completado la Práctica 3; Análisis descriptivo de ventas y clientes.
  - Disponer de la vista DATA_ANALYTICS_FOUNDATIONS.CURATED.VENTAS_TRANSACCIONES_CURADAS_2026_1.
  - Cuenta de Snowflake activa con permisos de lectura sobre CURATED.
  - Microsoft Excel instalado.
  - Acceso a Internet para descargar los archivos del reto.
introduction:
  - En este reto trabajarás con cuatro preguntas comerciales que pueden producir conclusiones diferentes dependiendo de la métrica seleccionada. Tu objetivo será identificar la métrica que responde a cada pregunta, ejecutar las consultas, comparar resultados y justificar por qué una métrica puede cambiar la interpretación sin que los datos sean contradictorios.
slug: lab6
lab_number: 6
final_result: >
  Al finalizar habrás documentado una matriz de selección de métricas, ejecutado comparaciones
  por región y canal, calculado recurrencia a nivel cliente y redactado una conclusión sobre
  cómo cambia la interpretación cuando se usa venta total, promedio, tasa o métricas por cliente.
notes:
  - Utiliza únicamente registros con QUALITYFLAG = 'VALID'.
  - Una métrica técnicamente correcta puede responder una pregunta distinta.
  - No interpretes una tasa sin revisar su denominador.
  - No uses transacciones como denominador cuando la unidad de análisis sea cliente.
references:
  - text: Snowflake Documentation - Aggregate functions
    url: https://docs.snowflake.com/en/sql-reference/functions-aggregation
  - text: Snowflake Documentation - Workspaces
    url: https://docs.snowflake.com/en/user-guide/ui-snowsight/workspaces
prev: /lab5/lab5/
next: /lab7/lab7/
---

---

<!-- Aquí comienzan las instrucciones paso a paso del reto -->

## 📁 Tarea 1. Preparar el reto y seleccionar métricas — 5 min

Prepararás los archivos y definirás qué métrica responde mejor a cada pregunta antes de ejecutar consultas.

### Tarea 1.1. Descargar y organizar los archivos

Crearás la carpeta del Reto 03 y conservarás los archivos de trabajo separados de la Práctica 3.

- {% include step_label.html %} Abre Git Bash y crea la carpeta `Reto_03`.

  ```bash
  mkdir -p /c/DAF/Reto_03
  ```

  > **Salida esperada:** Existe `C:\DAF\Reto_03\`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Descarga la plantilla y el SQL del reto desde las URL proporcionadas.

  1. [Descargar plantilla del Reto 3](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap3/Plantilla_Reto3_Metrica_Correcta.xlsx)
  2. [Descargar SQL del Reto 3](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap3/03_reto_metricas_correctas.sql)

  Guarda los archivos como:

  ```text
  C:\DAF\Reto_03\Plantilla_Reto3_Metrica_Correcta.xlsx
  C:\DAF\Reto_03\03_reto_metricas_correctas.sql
  ```

  > **Salida esperada:** Ambos archivos existen en `C:\DAF\Reto_03\`.
  {: .lab-note .output .compact}

### Tarea 1.2. Seleccionar la métrica antes de consultar

Definirás la métrica que mejor responde a cada pregunta y registrarás su granularidad.

- {% include step_label.html %} Abre `Plantilla_Reto3_Metrica_Correcta.xlsx` y revisa los cuatro casos de la hoja `Seleccion_Metricas`.

  > **Salida esperada:** Se muestran cuatro preguntas de negocio distintas.
  {: .lab-note .output .compact}

- {% include step_label.html %} Para cada caso, selecciona una métrica principal y registra la granularidad correcta.

  Considera métricas como:

  ```text
  SUM(NetSales)
  AVG(NetSales)
  COUNT(TransactionID)
  COUNT(DISTINCT CustomerID)
  tasa de devolución
  frecuencia por cliente
  venta neta por cliente
  ```

  > **Importante:** No ejecutes todavía las consultas. Primero documenta qué métrica usarías y por qué.
  {: .lab-note .important .compact}

  > **Salida esperada:** Los cuatro casos tienen una métrica y una granularidad propuestas.
  {: .lab-note .output .compact}

{% assign results = site.data.task-results[page.slug].results %}
{% capture r1 %}{{ results[0] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r1 %}

{% include support-prompt.html task="tarea1" %}

---

## 📊 Tarea 2. Comparar volumen, promedio y tasa — 10 min

Ejecutarás consultas por región y canal para observar cómo cambia la lectura al utilizar métricas diferentes.

### Tarea 2.1. Comparar métricas por región

Validarás si “vender más” significa mayor venta total, mayor promedio o mayor actividad.

- {% include step_label.html %} Abre `https://app.snowflake.com`, accede a **Projects > Workspaces** y crea un SQL File llamado `03_reto_metricas_correctas.sql`.

  > **Salida esperada:** El archivo SQL está abierto en Workspaces.
  {: .lab-note .output .compact}

- {% include step_label.html %} Copia el contenido del SQL descargado y ejecuta la consulta del **Caso 1** por `Region`.

  Compara:

  ```text
  transacciones
  clientes únicos
  venta neta total
  venta neta promedio
  ```

  > **Salida esperada:** Se dispone de varias métricas para cada región.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra en `Resultados` la región con mayor `SUM(NetSales)` y la región con mayor `AVG(NetSales)`.

  > **Advertencia:** Si son regiones distintas, no existe contradicción. Las métricas responden preguntas diferentes.
  {: .lab-note .warning .compact}

  > **Salida esperada:** Se documenta si la venta total y la venta promedio producen la misma o distinta lectura.
  {: .lab-note .output .compact}

### Tarea 2.2. Evaluar devolución por canal

Distinguirás entre conteo bruto de devoluciones y tasa de devolución.

- {% include step_label.html %} Ejecuta la consulta del **Caso 2** por `Channel`.

  Compara:

  ```text
  transacciones
  devoluciones
  tasa de devolución
  ```

  > **Salida esperada:** Cada canal muestra su volumen y su tasa de devolución.
  {: .lab-note .output .compact}

- {% include step_label.html %} Identifica el canal con mayor número de devoluciones y el canal con mayor tasa de devolución.

  > **Importante:** Una tasa requiere un denominador. El canal con más devoluciones no necesariamente tiene el mayor riesgo relativo.
  {: .lab-note .important .compact}

  > **Salida esperada:** Se documenta la diferencia entre conteo y tasa cuando exista.
  {: .lab-note .output .compact}

- {% include step_label.html %} Actualiza en `Seleccion_Metricas` la justificación del **Caso 2** según la evidencia observada.

  > **Salida esperada:** La selección de métrica está sustentada por los resultados ejecutados.
  {: .lab-note .output .compact}

{% capture r2 %}{{ results[1] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r2 %}

{% include support-prompt.html task="tarea2" %}

---

## 👥 Tarea 3. Cambiar la granularidad a cliente — 8 min

Comprobarás que una pregunta sobre frecuencia o desempeño por cliente no debe responderse únicamente con métricas transaccionales.

### Tarea 3.1. Medir recurrencia

Agruparás primero a nivel cliente para responder correctamente una pregunta de recurrencia.

- {% include step_label.html %} Ejecuta la consulta del **Caso 3** con `customer_frequency`.

  Obtendrás:

  ```text
  clientes
  frecuencia promedio
  frecuencia mediana
  clientes recurrentes
  tasa de clientes recurrentes
  ```

  > **Salida esperada:** Se dispone de métricas calculadas a nivel cliente.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra los resultados del **Caso 3** en la hoja `Resultados`.

  > **Importante:** La tasa de recurrencia usa clientes únicos como denominador.
  {: .lab-note .important .compact}

  > **Salida esperada:** El **Caso 3** muestra claramente la granularidad cliente.
  {: .lab-note .output .compact}

- {% include step_label.html %} Explica por qué `COUNT(TransactionID)` no responde por sí solo a la pregunta “¿los clientes compran más veces?”.

  > **Salida esperada:** La explicación menciona la necesidad de agrupar transacciones por `CustomerID`.
  {: .lab-note .output .compact}

### Tarea 3.2. Comparar desempeño por cliente

Calcularás una métrica que incorpora explícitamente el número de clientes del canal.

- {% include step_label.html %} Ejecuta la consulta del **Caso 4** y compara `TOTAL_NET_SALES`, `AVG_NET_SALES` y `NET_SALES_PER_CUSTOMER`.

  > **Salida esperada:** Cada canal dispone de tres lecturas distintas del desempeño.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra qué canal ocupa la primera posición en cada una de las tres métricas.

  > **Nota:** No asumas que el mismo canal debe liderar todos los indicadores.
  {: .lab-note .info .compact}

  > **Salida esperada:** La hoja `Resultados` permite contrastar volumen, promedio transaccional y resultado por cliente.
  {: .lab-note .output .compact}

{% capture r3 %}{{ results[2] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r3 %}

{% include support-prompt.html task="tarea3" %}

---

## ✅ Tarea 4. Justificar la métrica y cerrar el reto — 7 min

Consolidarás la evidencia y formularás una regla de decisión que pueda reutilizarse en análisis posteriores.

### Tarea 4.1. Validar las cuatro selecciones

Revisarás si la métrica elegida inicialmente sigue siendo adecuada después de observar los resultados.

- {% include step_label.html %} Regresa a `Seleccion_Metricas` y marca cada caso como `Justificado` o `Revisar`.

  > **Salida esperada:** Los cuatro casos tienen un estado final.
  {: .lab-note .output .compact}

- {% include step_label.html %} Corrige cualquier selección cuya métrica no responda exactamente a la pregunta de negocio.

  > **Importante:** Cambiar una métrica después de revisar la evidencia no es un error; es parte del razonamiento analítico.
  {: .lab-note .important .compact}

  > **Salida esperada:** Cada pregunta tiene una métrica, granularidad y justificación coherentes.
  {: .lab-note .output .compact}

### Tarea 4.2. Redactar la conclusión

Documentarás qué aprendiste sobre la relación entre pregunta, métrica y granularidad.

- {% include step_label.html %} Completa la hoja `Decision` identificando el caso donde más cambió la interpretación.

  > **Salida esperada:** Se identifica una comparación concreta entre dos métricas.
  {: .lab-note .output .compact}

- {% include step_label.html %} Escribe una regla aprendida en una sola frase.

  Puedes utilizar una estructura como:

  ```text
  Antes de comparar segmentos, debo definir si la pregunta busca volumen,
  valor promedio, proporción o comportamiento por cliente.
  ```

  > **Salida esperada:** La regla relaciona pregunta de negocio, métrica y granularidad.
  {: .lab-note .output .compact}

- {% include step_label.html %} Guarda una copia final como `03_reto_metricas_correctas.xlsx`.

  Guarda en:

  ```text
  C:\DAF\Reto_03\03_reto_metricas_correctas.xlsx
  ```

  > **Salida esperada:** El archivo final contiene selección, resultados, justificaciones y conclusión.
  {: .lab-note .output .compact}

{% capture r4 %}{{ results[3] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r4 %}

{% include support-prompt.html task="tarea4" %}