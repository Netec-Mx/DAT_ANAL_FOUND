---
layout: lab
title: "Práctica 2: Preparar y validar el dataset de ventas"
permalink: /lab3/lab3/
images_base: /labs/lab3/img
duration: "33 minutos"
objective:
  - Perfilar un dataset de ventas, detectar problemas de calidad y crear en Snowflake una vista curada mínima y trazable para las prácticas posteriores.
prerequisites:
  - Haber completado la Práctica 1: Convertir solicitudes operativas en preguntas analíticas.
  - Máquina virtual de Windows disponible.
  - Microsoft Excel, Visual Studio Code y Git Bash disponibles.
  - Cuenta de Snowflake activa con permisos de administrador o permisos equivalentes para crear base de datos, esquemas, tablas y vistas.
  - Acceso a Internet para descargar los archivos requeridos desde las URL proporcionadas.
introduction:
  - En esta práctica prepararás una fuente de ventas utilizable para análisis. Descargarás un archivo con miles de transacciones y anomalías controladas, lo cargarás en Snowflake mediante Snowsight, ejecutarás consultas de perfilado y crearás una vista curada con una bandera de calidad. El objetivo no es eliminar automáticamente registros sospechosos, sino identificarlos, normalizar campos básicos y conservar trazabilidad.
slug: lab3
lab_number: 3
final_result: >
  Al finalizar dispondrás de un archivo SQL reproducible, evidencia de perfilado y una vista DATA_ANALYTICS_FOUNDATIONS.CURATED.VENTAS_TRANSACCIONES_CURADAS_2026_1 que normaliza región, canal y categoría, identifica condiciones de revisión y conserva la fuente RAW sin modificar.
notes:
  - La fuente RAW se considera inmutable. No ejecutes UPDATE, DELETE, TRUNCATE, DROP ni ALTER sobre la tabla de datos cargada.
  - La práctica utiliza Snowsight y Workspaces, el editor SQL actual de Snowflake.
  - El archivo CSV contiene anomalías intencionales para fines didácticos.
references:
  - text: Snowflake Documentation - Load data using Snowsight
    url: https://docs.snowflake.com/en/user-guide/data-load-web-ui
  - text: Snowflake Documentation - Workspaces
    url: https://docs.snowflake.com/en/user-guide/ui-snowsight/workspaces
prev: /lab1/lab1/
next: /lab3/lab3/
---

---

## 📁 Tarea 1. Preparar archivos y cargar la fuente en Snowflake — 8 min

Crearás la carpeta de la Práctica 02, descargarás el dataset y prepararás en Snowflake una tabla RAW que conservará los datos originales para el perfilado.

### Tarea 1.1. Descargar y organizar los recursos

Prepararás el directorio de trabajo y descargarás el archivo de datos que contiene las anomalías necesarias para esta práctica.

- {% include step_label.html %} Abre Git Bash y crea la carpeta `Practica_02` dentro del directorio central del curso.

  ```bash
  mkdir -p /c/DAF/Practica_02
  ```

  > **Salida esperada:** Existe la carpeta `C:\DAF\Practica_02\`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Descarga el dataset de calidad desde la URL proporcionada y guárdalo en `00_recursos`.

  [Descargar dataset de calidad](URL_DATASET_CALIDAD_PRACTICA_02)

  ```text
  C:\DAF\00_recursos\Ventas_Retail_LATAM_2026_1_Calidad.csv
  ```

  > **Importante:** No edites este CSV. Funcionará como fuente original para la Práctica 2.
  {: .lab-note .important .compact}

  > **Salida esperada:** El archivo existe en `C:\DAF\00_recursos\Ventas_Retail_LATAM_2026_1_Calidad.csv`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Abre Visual Studio Code y crea `02_preparacion_ventas.sql` dentro de `C:\DAF\Practica_02\`.

  > **Nota:** Mantén abierto este archivo. Copiarás en él todas las consultas antes de ejecutarlas en Snowflake.
  {: .lab-note .info .compact}

  > **Salida esperada:** VS Code muestra `C:\DAF\Practica_02\02_preparacion_ventas.sql`.
  {: .lab-note .output .compact}

### Tarea 1.2. Acceder a Snowflake y cargar el CSV

Iniciarás sesión en Snowsight con tu cuenta y cargarás el archivo local como una tabla RAW sin aplicar transformaciones.

- {% include step_label.html %} Abre `https://app.snowflake.com`, selecciona tu cuenta e inicia sesión con las credenciales proporcionadas.

  > **Importante:** Usa tu cuenta de Snowflake con permisos de administrador. No guardes contraseñas ni tokens dentro de archivos SQL, Excel o Markdown.
  {: .lab-note .important .compact}

  > **Salida esperada:** Se muestra Snowsight con la sesión autenticada.
  {: .lab-note .output .compact}

- {% include step_label.html %} Cambia el rol activo a `ACCOUNTADMIN` o al rol administrativo proporcionado por el instructor.

  > **Salida esperada:** La sesión utiliza un rol con permisos para crear base de datos, esquemas, tablas y vistas.
  {: .lab-note .output .compact}

- {% include step_label.html %} Abre **Projects > Workspaces**, crea un archivo SQL temporal y ejecuta la preparación de objetos.

  ```sql
  CREATE DATABASE IF NOT EXISTS DATA_ANALYTICS_FOUNDATIONS;
  CREATE SCHEMA IF NOT EXISTS DATA_ANALYTICS_FOUNDATIONS.RAW;
  CREATE SCHEMA IF NOT EXISTS DATA_ANALYTICS_FOUNDATIONS.CURATED;
  ```

  Después selecciona **Create > Table > From File**, carga:

  ```text
  C:\DAF\00_recursos\Ventas_Retail_LATAM_2026_1_Calidad.csv
  ```

  y crea:

  ```text
  Database: DATA_ANALYTICS_FOUNDATIONS
  Schema: RAW
  Table: VENTAS_TRANSACCIONES_2026_1
  ```

  Revisa el esquema inferido y selecciona **Load**.

  > **Advertencia:** No corrijas los datos durante la carga. Las anomalías forman parte intencional de la práctica.
  {: .lab-note .warning .compact}

  > **Salida esperada:** Existe `DATA_ANALYTICS_FOUNDATIONS.RAW.VENTAS_TRANSACCIONES_2026_1` con aproximadamente 6,000 filas.
  {: .lab-note .output .compact}

{% assign results = site.data.task-results[page.slug].results %}
{% capture r1 %}{{ results[0] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r1 %}

{% include support-prompt.html task="tarea1" %}

---

## 🔎 Tarea 2. Perfilar la estructura y el contenido — 9 min

Abrirás el archivo SQL en Snowflake Workspaces y ejecutarás consultas breves para conocer volumen, cobertura temporal, completitud y granularidad antes de transformar los datos.

### Tarea 2.1. Abrir el SQL en Workspaces

Crearás un archivo SQL en el editor actual de Snowflake y establecerás el contexto de ejecución.

- {% include step_label.html %} En Snowsight abre **Projects > Workspaces**, selecciona **+** y crea un **SQL File** llamado `02_preparacion_ventas.sql`.

  > **Nota:** Workspaces reemplaza a los antiguos Worksheets. Utiliza este editor para ejecutar todas las consultas de la práctica.
  {: .lab-note .info .compact}

  > **Salida esperada:** Se muestra un archivo SQL llamado `02_preparacion_ventas.sql` dentro de Workspaces.
  {: .lab-note .output .compact}

- {% include step_label.html %} Copia al inicio del archivo SQL local y del archivo en Workspaces el contexto de trabajo.

  ```sql
  USE ROLE ACCOUNTADMIN;
  USE DATABASE DATA_ANALYTICS_FOUNDATIONS;
  USE SCHEMA RAW;
  ```

  > **Salida esperada:** El contexto activo apunta a `DATA_ANALYTICS_FOUNDATIONS.RAW`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Ejecuta una muestra de 10 filas para verificar que la carga sea legible.

  ```sql
  SELECT *
  FROM VENTAS_TRANSACCIONES_2026_1
  LIMIT 10;
  ```

  > **Salida esperada:** Se muestran 10 registros y columnas como `TRANSACTIONID`, `TRANSACTIONDATE`, `REGION`, `CHANNEL`, `CATEGORY` y `NETSALES`.
  {: .lab-note .output .compact}

### Tarea 2.2. Ejecutar el perfil inicial

Medirás filas, transacciones distintas, cobertura temporal y valores faltantes en campos críticos.

- {% include step_label.html %} Ejecuta el perfil de volumen y cobertura temporal.

  ```sql
  SELECT
      COUNT(*) AS TOTAL_ROWS,
      COUNT(DISTINCT TRANSACTIONID) AS UNIQUE_TRANSACTIONS,
      MIN(TRY_TO_DATE(TRANSACTIONDATE)) AS MIN_DATE,
      MAX(TRY_TO_DATE(TRANSACTIONDATE)) AS MAX_DATE
  FROM VENTAS_TRANSACCIONES_2026_1;
  ```

  > **Salida esperada:** El total ronda 6,000 filas y la cobertura incluye registros fuera del periodo esperado 2024-01-01 a 2025-12-31.
  {: .lab-note .output .compact}

- {% include step_label.html %} Ejecuta el perfil de campos críticos.

  ```sql
  SELECT
      COUNT_IF(TRANSACTIONID IS NULL OR TRIM(TRANSACTIONID) = '') AS MISSING_TRANSACTION_ID,
      COUNT_IF(REGION IS NULL OR TRIM(REGION) IN ('', 'N/A')) AS MISSING_REGION,
      COUNT_IF(CHANNEL IS NULL OR TRIM(CHANNEL) IN ('', 'N/A')) AS MISSING_CHANNEL,
      COUNT_IF(CATEGORY IS NULL OR TRIM(CATEGORY) IN ('', 'N/A')) AS MISSING_CATEGORY,
      COUNT_IF(QUANTITY <= 0) AS INVALID_QUANTITY,
      COUNT_IF(DISCOUNTPCT < 0 OR DISCOUNTPCT > 0.60) AS INVALID_DISCOUNT
  FROM VENTAS_TRANSACCIONES_2026_1;
  ```

  > **Salida esperada:** Al menos uno de los controles devuelve un valor mayor que cero.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra en `02_preparacion_ventas.sql` un comentario con tres hallazgos observados.

  ```sql
  -- Hallazgo 1:
  -- Hallazgo 2:
  -- Hallazgo 3:
  ```

  > **Advertencia:** Describe hechos observados. No conviertas todavía una anomalía en una causa o en una decisión de eliminación.
  {: .lab-note .warning .compact}

  > **Salida esperada:** El archivo SQL contiene tres hallazgos basados en resultados ejecutados.
  {: .lab-note .output .compact}

{% capture r2 %}{{ results[1] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r2 %}

{% include support-prompt.html task="tarea2" %}

---

## 🧪 Tarea 3. Detectar duplicados y variantes de calidad — 8 min

Examinarás identificadores repetidos y categorías inconsistentes para distinguir problemas técnicos de condiciones que requieren revisión antes del análisis.

### Tarea 3.1. Detectar identificadores repetidos

Comprobarás si `TransactionID` puede utilizarse directamente como identificador único.

- {% include step_label.html %} Ejecuta la consulta de identificadores repetidos.

  ```sql
  SELECT TRANSACTIONID, COUNT(*) AS REPETITIONS
  FROM VENTAS_TRANSACCIONES_2026_1
  GROUP BY TRANSACTIONID
  HAVING COUNT(*) > 1
  ORDER BY REPETITIONS DESC, TRANSACTIONID;
  ```

  > **Salida esperada:** Se muestran identificadores con más de una fila asociada.
  {: .lab-note .output .compact}

- {% include step_label.html %} Revisa una muestra de las filas asociadas a IDs repetidos.

  ```sql
  SELECT *
  FROM VENTAS_TRANSACCIONES_2026_1
  WHERE TRANSACTIONID IN (
      SELECT TRANSACTIONID
      FROM VENTAS_TRANSACCIONES_2026_1
      GROUP BY TRANSACTIONID
      HAVING COUNT(*) > 1
  )
  ORDER BY TRANSACTIONID
  LIMIT 40;
  ```

  > **Importante:** Una repetición del identificador no demuestra por sí sola que ambas filas sean duplicados exactos.
  {: .lab-note .important .compact}

  > **Salida esperada:** La muestra permite observar repeticiones exactas y repeticiones con diferencias entre campos.
  {: .lab-note .output .compact}

- {% include step_label.html %} Documenta en el SQL que los IDs repetidos deberán marcarse para revisión y no eliminarse automáticamente.

  > **Salida esperada:** El criterio de tratamiento queda registrado como comentario en el archivo SQL.
  {: .lab-note .output .compact}

### Tarea 3.2. Identificar variantes de región, canal y categoría

Examinarás valores que podrían fragmentar una misma categoría lógica durante el análisis.

- {% include step_label.html %} Ejecuta un perfil normalizado de `Region`.

  ```sql
  SELECT REGION, UPPER(TRIM(REGION)) AS REGION_NORMALIZED, COUNT(*) AS ROWS_COUNT
  FROM VENTAS_TRANSACCIONES_2026_1
  GROUP BY REGION, UPPER(TRIM(REGION))
  ORDER BY ROWS_COUNT DESC;
  ```

  > **Salida esperada:** Se observan valores equivalentes con diferencias de espacios, mayúsculas o etiquetas.
  {: .lab-note .output .compact}

- {% include step_label.html %} Ejecuta el mismo control sobre `Channel`.

  ```sql
  SELECT CHANNEL, UPPER(TRIM(CHANNEL)) AS CHANNEL_NORMALIZED, COUNT(*) AS ROWS_COUNT
  FROM VENTAS_TRANSACCIONES_2026_1
  GROUP BY CHANNEL, UPPER(TRIM(CHANNEL))
  ORDER BY ROWS_COUNT DESC;
  ```

  > **Salida esperada:** Se observan variantes como `ONLINE`, `WEB`, `E-COMMERCE` o diferencias de formato.
  {: .lab-note .output .compact}

- {% include step_label.html %} Revisa `Category` y registra qué valores requieren normalización o revisión.

  ```sql
  SELECT CATEGORY, UPPER(TRIM(CATEGORY)) AS CATEGORY_NORMALIZED, COUNT(*) AS ROWS_COUNT
  FROM VENTAS_TRANSACCIONES_2026_1
  GROUP BY CATEGORY, UPPER(TRIM(CATEGORY))
  ORDER BY ROWS_COUNT DESC;
  ```

  > **Salida esperada:** Se dispone de evidencia para definir reglas básicas de normalización de categoría.
  {: .lab-note .output .compact}

{% capture r3 %}{{ results[2] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r3 %}

{% include support-prompt.html task="tarea3" %}

---

## ✅ Tarea 4. Crear y validar la vista curada — 8 min

Crearás una vista de trabajo que normaliza los campos de segmentación y marca los registros sospechosos sin modificar ni eliminar información de la fuente RAW.

### Tarea 4.1. Crear la vista curada

Aplicarás reglas mínimas de estandarización y una bandera de calidad reutilizable por las prácticas siguientes.

- {% include step_label.html %} Agrega al archivo SQL la creación de la vista `CURATED`.

  ```sql
  CREATE OR REPLACE VIEW DATA_ANALYTICS_FOUNDATIONS.CURATED.VENTAS_TRANSACCIONES_CURADAS_2026_1 AS
  SELECT
      TRANSACTIONID,
      TRY_TO_DATE(TRANSACTIONDATE) AS TRANSACTIONDATE,
      CUSTOMERID,
      COUNTRY,
      CASE
          WHEN REGION IS NULL OR TRIM(REGION) IN ('', 'N/A') THEN 'SIN_REGION'
          WHEN UPPER(TRIM(REGION)) IN ('NORTE', 'ZONA NORTE') THEN 'NORTE'
          WHEN UPPER(TRIM(REGION)) = 'CENTRO' THEN 'CENTRO'
          WHEN UPPER(TRIM(REGION)) = 'OCCIDENTE' THEN 'OCCIDENTE'
          WHEN UPPER(TRIM(REGION)) = 'SUR' THEN 'SUR'
          WHEN UPPER(TRIM(REGION)) = 'ANDINA' THEN 'ANDINA'
          ELSE UPPER(TRIM(REGION))
      END AS REGION,
      CITY,
      CASE
          WHEN CHANNEL IS NULL OR TRIM(CHANNEL) IN ('', 'N/A') THEN 'SIN_CANAL'
          WHEN UPPER(TRIM(CHANNEL)) IN ('ONLINE', 'WEB', 'E-COMMERCE') THEN 'ONLINE'
          WHEN UPPER(TRIM(CHANNEL)) IN ('TIENDA', 'TIENDA FISICA') THEN 'TIENDA'
          WHEN UPPER(TRIM(CHANNEL)) IN ('MARKETPLACE', 'MARKET PLACE') THEN 'MARKETPLACE'
          ELSE UPPER(TRIM(CHANNEL))
      END AS CHANNEL,
      PRODUCTID,
      PRODUCTNAME,
      CASE
          WHEN CATEGORY IS NULL OR TRIM(CATEGORY) IN ('', 'N/A') THEN 'SIN_CATEGORIA'
          ELSE UPPER(TRIM(CATEGORY))
      END AS CATEGORY,
      QUANTITY,
      UNITPRICE,
      DISCOUNTPCT,
      NETSALES,
      GROSSMARGIN,
      RETURNED,
      RETURNAMOUNT,
      TRANSACTIONSTATUS,
      CASE
          WHEN TRANSACTIONID IS NULL OR TRIM(TRANSACTIONID) = '' THEN 'REVIEW'
          WHEN TRY_TO_DATE(TRANSACTIONDATE) IS NULL THEN 'REVIEW'
          WHEN TRY_TO_DATE(TRANSACTIONDATE) < '2024-01-01'::DATE OR TRY_TO_DATE(TRANSACTIONDATE) > '2025-12-31'::DATE THEN 'REVIEW'
          WHEN REGION IS NULL OR TRIM(REGION) IN ('', 'N/A') THEN 'REVIEW'
          WHEN CHANNEL IS NULL OR TRIM(CHANNEL) IN ('', 'N/A') THEN 'REVIEW'
          WHEN CATEGORY IS NULL OR TRIM(CATEGORY) IN ('', 'N/A') THEN 'REVIEW'
          WHEN QUANTITY <= 0 THEN 'REVIEW'
          WHEN DISCOUNTPCT < 0 OR DISCOUNTPCT > 0.60 THEN 'REVIEW'
          WHEN COUNT(*) OVER (PARTITION BY TRANSACTIONID) > 1 THEN 'REVIEW'
          ELSE 'VALID'
      END AS QUALITYFLAG
  FROM DATA_ANALYTICS_FOUNDATIONS.RAW.VENTAS_TRANSACCIONES_2026_1;
  ```

  > **Importante:** La vista transforma la lectura de los datos; no modifica la tabla RAW.
  {: .lab-note .important .compact}

  > **Salida esperada:** Se crea `DATA_ANALYTICS_FOUNDATIONS.CURATED.VENTAS_TRANSACCIONES_CURADAS_2026_1`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Ejecuta un resumen de la bandera de calidad.

  ```sql
  SELECT QUALITYFLAG, COUNT(*) AS ROWS_COUNT,
         ROUND(COUNT(*) * 100.0 / SUM(COUNT(*)) OVER (), 2) AS PERCENTAGE
  FROM DATA_ANALYTICS_FOUNDATIONS.CURATED.VENTAS_TRANSACCIONES_CURADAS_2026_1
  GROUP BY QUALITYFLAG
  ORDER BY QUALITYFLAG;
  ```

  > **Salida esperada:** El resultado contiene registros `VALID` y registros `REVIEW`.
  {: .lab-note .output .compact}

### Tarea 4.2. Validar y guardar el entregable

Confirmarás que la fuente curada conserva las filas y que el SQL queda disponible para reproducir la preparación.

- {% include step_label.html %} Compara el número de filas entre RAW y CURATED.

  ```sql
  SELECT
      (SELECT COUNT(*) FROM DATA_ANALYTICS_FOUNDATIONS.RAW.VENTAS_TRANSACCIONES_2026_1) AS RAW_ROWS,
      (SELECT COUNT(*) FROM DATA_ANALYTICS_FOUNDATIONS.CURATED.VENTAS_TRANSACCIONES_CURADAS_2026_1) AS CURATED_ROWS;
  ```

  > **Salida esperada:** `RAW_ROWS` y `CURATED_ROWS` tienen el mismo valor.
  {: .lab-note .output .compact}

- {% include step_label.html %} Ejecuta una muestra de registros marcados para revisión.

  ```sql
  SELECT *
  FROM DATA_ANALYTICS_FOUNDATIONS.CURATED.VENTAS_TRANSACCIONES_CURADAS_2026_1
  WHERE QUALITYFLAG = 'REVIEW'
  LIMIT 20;
  ```

  > **Salida esperada:** Se muestran registros asociados con alguna de las condiciones de calidad evaluadas.
  {: .lab-note .output .compact}

- {% include step_label.html %} Guarda en VS Code la versión final del SQL en `C:\DAF\Practica_02\02_preparacion_ventas.sql`.

  > **Nota:** Conserva la vista curada y el archivo SQL. Ambos serán utilizados como base en las prácticas posteriores.
  {: .lab-note .info .compact}

  > **Salida esperada:** El archivo SQL está guardado localmente y la vista curada permanece disponible en Snowflake.
  {: .lab-note .output .compact}

{% capture r4 %}{{ results[3] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r4 %}

{% include support-prompt.html task="tarea4" %}
