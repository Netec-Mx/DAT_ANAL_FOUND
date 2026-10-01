---
layout: lab
title: "Reto 2: Liberación o revisión de un archivo mensual"
permalink: /lab4/lab4/
images_base: /labs/lab4/img
duration: "15 minutos"
objective:
  - Evaluar de forma autónoma la calidad de un archivo mensual de ventas y emitir una decisión de liberación sustentada en evidencia.
prerequisites:
  - Haber completado la Práctica 2; Preparar y validar el dataset de ventas.
  - Cuenta de Snowflake activa con permisos para crear y consultar tablas en DATA_ANALYTICS_FOUNDATIONS.RAW.
  - Microsoft Excel instalado.
  - Acceso a Internet para descargar los archivos del reto.
  - Conservar la estructura central del curso en C:\DAF\.
introduction:
  - En este reto recibirás un archivo mensual de ventas que debe incorporarse al análisis comercial. Tu responsabilidad será cargarlo en Snowflake, ejecutar cinco controles de calidad y decidir si puede liberarse, si puede liberarse con observaciones o si debe mantenerse en revisión. No transformarás ni eliminarás registros; la decisión deberá basarse en evidencia reproducible.
slug: lab4
lab_number: 4
final_result: >
  Al finalizar habrás documentado los resultados de cinco controles de calidad y emitido una decisión
  LIBERAR, LIBERAR_CON_OBSERVACIONES o MANTENER_EN_REVISION, acompañada por evidencia y una acción recomendada.
notes:
  - El archivo contiene anomalías intencionales y no debe modificarse antes de cargarlo.
  - Un registro sospechoso no es automáticamente un registro inválido.
  - Utiliza Snowflake Workspaces para ejecutar el archivo SQL proporcionado.
references:
  - text: Snowflake Documentation - Workspaces
    url: https://docs.snowflake.com/en/user-guide/ui-snowsight/workspaces
  - text: Snowflake Documentation - Load data using Snowsight
    url: https://docs.snowflake.com/en/user-guide/data-load-web-ui
prev: /lab3/lab3/
next: /lab5/lab5/
---

---

<!-- Aquí comienzan las instrucciones paso a paso del reto -->

## 📁 Tarea 1. Preparar el archivo mensual — 4 min

Crearás el directorio del Reto 02, descargarás los archivos requeridos y cargarás el archivo mensual en Snowflake sin modificar su contenido.

### Tarea 1.1. Descargar y organizar los archivos

Prepararás la carpeta del reto y conservarás el dataset original separado de los entregables.

- {% include step_label.html %} Abre Git Bash y crea la carpeta `Reto_02`.

  ```bash
  mkdir -p /c/DAF/Reto_02
  ```

  > **Salida esperada:** Existe `C:\DAF\Reto_02\`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Descarga los tres archivos del reto desde las URL proporcionadas.

  1. [Descargar archivo mensual](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap2/Ventas_Retail_LATAM_2025_12_Mensual.csv)
  2. [Descargar plantilla del reto](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap2/Plantilla_Reto2_Liberacion.xlsx)
  3. [Descargar SQL del reto](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap2/02_reto_liberacion_archivo_mensual.sql)

  Guarda los archivos como:

  ```text
  C:\DAF\00_recursos\Ventas_Retail_LATAM_2025_12_Mensual.csv
  C:\DAF\Reto_02\Plantilla_Reto2_Liberacion.xlsx
  C:\DAF\Reto_02\02_reto_liberacion_archivo_mensual.sql
  ```

  > **Importante:** No edites el CSV. Conserva el archivo original como evidencia de entrada.
  {: .lab-note .important .compact}

  > **Salida esperada:** Los tres archivos existen en las rutas indicadas.
  {: .lab-note .output .compact}

### Tarea 1.2. Cargar el archivo en Snowflake

Crearás una tabla independiente para evaluar el lote mensual sin afectar la tabla utilizada en la Práctica 2.

- {% include step_label.html %} Abre `https://app.snowflake.com`, inicia sesión y utiliza `ACCOUNTADMIN` o el rol equivalente proporcionado.

  > **Nota:** Workspaces es el editor SQL actual de Snowsight. No necesitas utilizar los antiguos Worksheets.
  {: .lab-note .info .compact}

  > **Salida esperada:** La sesión de Snowflake está autenticada con permisos suficientes.
  {: .lab-note .output .compact}

- {% include step_label.html %} Selecciona **Create > Table > From File** y carga el archivo mensual como `VENTAS_MENSUALES_2025_12`.

  Selecciona:

  ```text
  C:\DAF\00_recursos\Ventas_Retail_LATAM_2025_12_Mensual.csv
  ```

  Configura:

  ```text
  Database: DATA_ANALYTICS_FOUNDATIONS
  Schema: RAW
  Table: VENTAS_MENSUALES_2025_12
  ```

  Revisa el esquema inferido y selecciona **Load**.

  > **Advertencia:** No corrijas manualmente valores antes de cargar el archivo.
  {: .lab-note .warning .compact}

  > **Salida esperada:** Existe `DATA_ANALYTICS_FOUNDATIONS.RAW.VENTAS_MENSUALES_2025_12`.
  {: .lab-note .output .compact}

{% assign results = site.data.task-results[page.slug].results %}
{% capture r1 %}{{ results[0] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r1 %}

{% include support-prompt.html task="tarea1" %}

---

## 🔎 Tarea 2. Ejecutar los controles de calidad — 6 min

Ejecutarás controles de volumen, fechas, campos críticos, valores y unicidad sobre el archivo mensual.

### Tarea 2.1. Abrir y ejecutar los controles básicos

Utilizarás el SQL proporcionado para obtener evidencia reproducible sin escribir las consultas desde cero.

- {% include step_label.html %} En Snowsight abre **Projects > Workspaces** y crea o abre un SQL File llamado `02_reto_liberacion_archivo_mensual.sql`.

  > **Salida esperada:** El archivo SQL está visible en Workspaces.
  {: .lab-note .output .compact}

- {% include step_label.html %} Copia el contenido del archivo descargado al SQL File y ejecuta los controles 1, 2 y 3.

  Evalúa:

  ```text
  1. Volumen y cobertura temporal.
  2. Campos críticos faltantes.
  3. Quantity y DiscountPct fuera de regla.
  ```

  > **Salida esperada:** Dispones de resultados para volumen, fechas, campos críticos y valores fuera de regla.
  {: .lab-note .output .compact}

- {% include step_label.html %} Abre `Plantilla_Reto2_Liberacion.xlsx` y registra los resultados en la hoja `Controles`.

  > **Importante:** Registra los valores observados; no escribas únicamente “bien” o “mal”.
  {: .lab-note .important .compact}

  > **Salida esperada:** Los primeros cuatro controles contienen evidencia cuantitativa.
  {: .lab-note .output .compact}

### Tarea 2.2. Revisar fechas e identificadores repetidos

Completarás la evaluación con el alcance temporal del archivo y la unicidad de las transacciones.

- {% include step_label.html %} Ejecuta el control de registros fuera de diciembre de 2025.

  > **Salida esperada:** Obtienes el número de filas cuya fecha no pertenece al periodo esperado.
  {: .lab-note .output .compact}

- {% include step_label.html %} Ejecuta la consulta de `TransactionID` repetidos y revisa el resultado.

  > **Advertencia:** Un ID repetido requiere revisión, pero no demuestra automáticamente que las filas deban eliminarse.
  {: .lab-note .warning .compact}

  > **Salida esperada:** Se identifican los IDs repetidos o se confirma que no existen.
  {: .lab-note .output .compact}

- {% include step_label.html %} Completa en Excel los controles `Cobertura temporal` y `Unicidad`, y clasifica cada control.

  Usa:

  ```text
  Cumple
  Observación
  No cumple
  ```

  > **Salida esperada:** Los cinco controles tienen resultado, evidencia y estado.
  {: .lab-note .output .compact}

{% capture r2 %}{{ results[1] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r2 %}

{% include support-prompt.html task="tarea2" %}

---

## ✅ Tarea 3. Emitir la decisión de liberación — 5 min

Interpretarás conjuntamente los controles y emitirás una decisión que pueda utilizar el equipo responsable de incorporar el archivo al análisis.

### Tarea 3.1. Documentar la decisión

Distinguirás entre una excepción controlable y un problema que requiere detener temporalmente la incorporación del archivo.

- {% include step_label.html %} Revisa los cinco controles y selecciona un estado final en la hoja `Decision`.

  Elige únicamente:

  ```text
  LIBERAR
  LIBERAR_CON_OBSERVACIONES
  MANTENER_EN_REVISION
  ```

  > **Nota:** No existe una decisión válida sin evidencia. Considera severidad, cantidad de excepciones y efecto sobre el análisis.
  {: .lab-note .info .compact}

  > **Salida esperada:** La plantilla contiene uno de los tres estados permitidos.
  {: .lab-note .output .compact}

- {% include step_label.html %} Escribe una justificación breve citando al menos tres resultados observados.

  Ejemplo de estructura:

  ```text
  Se detectaron [resultado 1], [resultado 2] y [resultado 3].
  Estos casos pueden afectar [impacto].
  ```

  > **Salida esperada:** La decisión está sustentada con al menos tres evidencias cuantitativas.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra una acción recomendada y guarda la copia final como `02_reto_liberacion.xlsx`.

  Guarda en:

  ```text
  C:\DAF\Reto_02\02_reto_liberacion.xlsx
  ```

  > **Importante:** Una acción válida puede ser corregir registros identificados, solicitar confirmación al origen o liberar con excepciones documentadas. No elimines filas durante el reto.
  {: .lab-note .important .compact}

  > **Salida esperada:** `C:\DAF\Reto_02\02_reto_liberacion.xlsx` contiene controles, evidencia, decisión y acción recomendada.
  {: .lab-note .output .compact}

{% capture r3 %}{{ results[2] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r3 %}

{% include support-prompt.html task="tarea3" %}