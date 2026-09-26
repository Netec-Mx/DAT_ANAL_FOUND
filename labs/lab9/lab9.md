---
layout: lab
title: "Práctica 5: Construir un dashboard básico de desempeño de ventas"
permalink: /lab9/lab9/
images_base: /labs/lab9/img
duration: "35 minutos"
objective:
  - Conectar Power BI Desktop a la fuente curada, crear un modelo temporal y medidas DAX esenciales, construir una página de dashboard y validar sus KPI principales contra Snowflake.
prerequisites:
  - Haber completado las Prácticas 1 a 4.
  - Power BI Desktop instalado y disponible en la VM.
  - Cuenta de Snowflake activa con acceso de lectura a DATA_ANALYTICS_FOUNDATIONS.CURATED.
  - Disponer de la vista DATA_ANALYTICS_FOUNDATIONS.CURATED.VENTAS_TRANSACCIONES_CURADAS_2026_1.
  - Conservar los hallazgos y KPI priorizados en la Práctica 4.
  - Acceso a Internet para descargar los archivos auxiliares.
introduction:
  - En esta práctica construirás la primera página de Power BI del curso. Conectarás Power BI Desktop directamente a Snowflake, filtrarás la población validada, crearás una tabla calendario, medidas DAX y visualizaciones orientadas a ventas, margen, tendencia y segmentos. Finalmente, compararás los KPI principales contra Snowflake antes de guardar el PBIX.
slug: lab9
lab_number: 9
final_result: >
  Al finalizar tendrás un archivo 05_dashboard_ventas.pbix con una página de desempeño,
  KPI, filtros, tendencia mensual y comparaciones por región y canal, además de evidencia
  de validación contra Snowflake.
notes:
  - Power BI Desktop ya debe estar instalado antes de iniciar.
  - La consulta Ventas Curadas debe filtrar QUALITYFLAG = VALID.
  - Mantén los mismos filtros cuando compares Power BI con Snowflake.
  - Si existen varias monedas sin conversión, valida importes usando una sola Currency.
  - No guardes credenciales en PBIX, SQL, Excel ni archivos de texto.
references:
  - text: Microsoft Learn - Snowflake connector for Power Query
    url: https://learn.microsoft.com/power-query/connectors/snowflake
  - text: Microsoft Learn - Set and use date tables in Power BI Desktop
    url: https://learn.microsoft.com/power-bi/transform-model/desktop-date-tables
  - text: Microsoft Learn - Create measures in Power BI Desktop
    url: https://learn.microsoft.com/power-bi/transform-model/desktop-tutorial-create-measures
  - text: Microsoft Learn - Slicer visual in Power BI
    url: https://learn.microsoft.com/power-bi/visuals/power-bi-visualization-slicer-visual
prev: /reto4/reto4/
next: /reto5/reto5/
---

---

## 🔌 Tarea 1. Conectar Power BI a Snowflake — 7 min

Crearás el archivo PBIX y conectarás Power BI Desktop a la misma fuente curada utilizada en las prácticas anteriores.

### Tarea 1.1. Preparar los archivos

- {% include step_label.html %} Abre Git Bash y crea la carpeta `Practica_05`.

  ```bash
  mkdir -p /c/DAF/Practica_05
  ```

  > **Salida esperada:** Existe `C:\DAF\Practica_05\`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Descarga los archivos auxiliares.

  1. [Descargar medidas DAX](URL_DAX_PRACTICA_05)
  2. [Descargar SQL de validación](URL_SQL_PRACTICA_05)
  3. [Descargar plantilla de validación](URL_PLANTILLA_PRACTICA_05)

  Guarda como:

  ```text
  C:\DAF\Practica_05\05_medidas_dashboard.dax
  C:\DAF\Practica_05\05_validacion_dashboard.sql
  C:\DAF\Practica_05\Plantilla_Practica5_Validacion.xlsx
  ```

  > **Salida esperada:** Los tres recursos están disponibles localmente.
  {: .lab-note .output .compact}

### Tarea 1.2. Crear el PBIX y conectar Snowflake

- {% include step_label.html %} Abre Power BI Desktop y selecciona **Archivo > Guardar como**.

  Guarda:

  ```text
  C:\DAF\Practica_05\05_dashboard_ventas.pbix
  ```

  > **Salida esperada:** El archivo PBIX queda creado antes de cargar datos.
  {: .lab-note .output .compact}

- {% include step_label.html %} En **Inicio**, selecciona **Obtener datos > Más > Base de datos > Snowflake** y selecciona **Conectar**.

  Ingresa:

  ```text
  Servidor: <SNOWFLAKE_SERVER>
  Almacén: <WAREHOUSE_ASIGNADO>
  ```

  Usa **Importar** como modo de conectividad.

  > **Nota:** Si el instructor asignó un rol específico, úsalo en las opciones avanzadas o al autenticarte según la configuración institucional.
  {: .lab-note .info .compact}

  > **Salida esperada:** Power BI muestra el Navegador de Snowflake.
  {: .lab-note .output .compact}

- {% include step_label.html %} En el Navegador selecciona:

  ```text
  DATA_ANALYTICS_FOUNDATIONS
  > CURATED
  > VENTAS_TRANSACCIONES_CURADAS_2026_1
  ```

  Selecciona **Transformar datos**.

  > **Salida esperada:** Power Query Editor muestra la fuente curada.
  {: .lab-note .output .compact}

### Tarea 1.3. Preparar `Ventas Curadas`

- {% include step_label.html %} Renombra la consulta como:

  ```text
  Ventas Curadas
  ```

- {% include step_label.html %} Filtra `QUALITYFLAG` para conservar únicamente:

  ```text
  VALID
  ```

  Revisa los tipos:

  ```text
  TRANSACTIONDATE → Fecha
  TRANSACTIONID → Texto
  CUSTOMERID → Texto
  QUANTITY → Número entero
  NETSALES → Número decimal
  GROSSMARGIN → Número decimal
  REGION / CHANNEL / CATEGORY → Texto
  ```

  > **Importante:** No elimines campos necesarios para KPI, filtros o validación.
  {: .lab-note .important .compact}

  > **Salida esperada:** La consulta contiene solo registros válidos y tipos consistentes.
  {: .lab-note .output .compact}

- {% include step_label.html %} Selecciona **Cerrar y aplicar**.

  > **Salida esperada:** El modelo contiene la tabla `Ventas Curadas`.
  {: .lab-note .output .compact}

{% assign results = site.data.task-results[page.slug].results %}
{% capture r1 %}{{ results[0] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r1 %}
{% include support-prompt.html task="tarea1" %}

---

## 🧮 Tarea 2. Crear calendario y medidas DAX — 9 min

Prepararás el modelo para filtrar fechas correctamente y centralizarás los KPI en medidas reutilizables.

### Tarea 2.1. Crear la tabla calendario

- {% include step_label.html %} En Power BI selecciona **Modelado > Nueva tabla**.

  Copia desde `05_medidas_dashboard.dax` la expresión `Calendario`.

  > **Salida esperada:** Existe una tabla `Calendario` que cubre 2024-01-01 a 2025-12-31.
  {: .lab-note .output .compact}

- {% include step_label.html %} Selecciona `Calendario[Mes]` y usa **Ordenar por columna > Mes Número**.

  Después selecciona `Calendario[Año-Mes]` y usa:

  ```text
  Ordenar por columna > Año-Mes Orden
  ```

  > **Salida esperada:** Los meses pueden ordenarse cronológicamente.
  {: .lab-note .output .compact}

- {% include step_label.html %} En la vista **Modelo**, relaciona:

  ```text
  Calendario[Date]  1  →  *  Ventas Curadas[TRANSACTIONDATE]
  ```

  Configura:

  ```text
  Cardinalidad: Uno a varios
  Dirección: Única
  Relación activa: Sí
  ```

  Marca `Calendario` como tabla de fechas usando `Date`.

  > **Salida esperada:** Existe una relación activa 1:* desde calendario hacia ventas.
  {: .lab-note .output .compact}

### Tarea 2.2. Crear las medidas

- {% include step_label.html %} Selecciona `Ventas Curadas` y usa **Modelado > Nueva medida**.

  Crea desde `05_medidas_dashboard.dax`:

  ```text
  Ventas Netas
  Margen Bruto
  Margen %
  Transacciones
  Clientes Únicos
  Ticket Promedio
  ```

  > **Salida esperada:** Las seis medidas aparecen en el panel de datos.
  {: .lab-note .output .compact}

- {% include step_label.html %} Formatea:

  ```text
  Ventas Netas → Moneda
  Margen Bruto → Moneda
  Margen % → Porcentaje
  Ticket Promedio → Moneda
  Transacciones → Entero
  Clientes Únicos → Entero
  ```

  > **Salida esperada:** Las medidas usan formatos consistentes.
  {: .lab-note .output .compact}

{% capture r2 %}{{ results[1] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r2 %}
{% include support-prompt.html task="tarea2" %}

---

## 📊 Tarea 3. Construir el dashboard — 12 min

Crearás una sola página orientada a desempeño, tendencia y segmentación.

### Tarea 3.1. Preparar la página

- {% include step_label.html %} Renombra la página como:

  ```text
  Desempeño de ventas
  ```

  Configura el lienzo en formato **16:9**.

  > **Salida esperada:** La página tiene nombre y proporción adecuados.
  {: .lab-note .output .compact}

- {% include step_label.html %} Agrega tres slicers:

  ```text
  Calendario[Date]
  Ventas Curadas[REGION]
  Ventas Curadas[CHANNEL]
  ```

  Configura `Date` como intervalo **Entre**.

  > **Salida esperada:** Los tres filtros están visibles en la parte superior o lateral.
  {: .lab-note .output .compact}

### Tarea 3.2. Crear KPI y visuales

- {% include step_label.html %} Inserta cuatro visuales de tarjeta:

  ```text
  Ventas Netas
  Margen Bruto
  Margen %
  Ticket Promedio
  ```

  > **Salida esperada:** Los cuatro KPI principales son visibles sin desplazamiento.
  {: .lab-note .output .compact}

- {% include step_label.html %} Inserta un gráfico de líneas.

  Configura:

  ```text
  Eje X: Calendario[Año-Mes]
  Eje Y: [Ventas Netas]
  Título: Evolución mensual de ventas netas
  ```

  > **Salida esperada:** La línea presenta los meses en orden cronológico.
  {: .lab-note .output .compact}

- {% include step_label.html %} Inserta un gráfico de barras horizontal.

  Configura:

  ```text
  Eje: REGION
  Valor: [Ventas Netas]
  Orden: de mayor a menor
  Título: Ventas netas por región
  ```

  > **Salida esperada:** Las regiones pueden compararse con precisión.
  {: .lab-note .output .compact}

- {% include step_label.html %} Inserta un segundo gráfico de barras para canal.

  Configura:

  ```text
  Eje: CHANNEL
  Valor: [Ventas Netas]
  Título: Ventas netas por canal
  ```

  > **Salida esperada:** El dashboard muestra composición por canal.
  {: .lab-note .output .compact}

### Tarea 3.3. Verificar los filtros

- {% include step_label.html %} Selecciona una región y confirma que las tarjetas y ambos gráficos cambian.

  Después elimina la selección.

  > **Importante:** Los KPI deben volver a los valores globales al limpiar los filtros.
  {: .lab-note .important .compact}

  > **Salida esperada:** Los visuales responden de manera coherente a los slicers.
  {: .lab-note .output .compact}

{% capture r3 %}{{ results[2] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r3 %}
{% include support-prompt.html task="tarea3" %}

---

## ✅ Tarea 4. Validar y guardar — 7 min

Compararás los KPI principales contra Snowflake antes de considerar terminado el dashboard.

### Tarea 4.1. Validar KPI

- {% include step_label.html %} Quita todos los filtros en Power BI y registra en `Plantilla_Practica5_Validacion.xlsx`:

  ```text
  Ventas Netas
  Margen Bruto
  Margen %
  Transacciones
  Clientes Únicos
  Ticket Promedio
  ```

  > **Salida esperada:** La columna Power BI contiene los KPI globales.
  {: .lab-note .output .compact}

- {% include step_label.html %} En Snowflake abre `05_validacion_dashboard.sql` y ejecuta la consulta global.

  Copia los resultados en la columna `Snowflake`.

  > **Salida esperada:** Los mismos KPI están disponibles desde la fuente curada.
  {: .lab-note .output .compact}

- {% include step_label.html %} Marca cada control como `Conforme` o `Investigar`.

  Para conteos:

  ```text
  diferencia esperada = 0
  ```

  Para importes:

  ```text
  tolerancia de redondeo = 0.01
  ```

  > **Importante:** Si una cifra no coincide, revisa filtros, tipos, relación de fechas y fórmula DAX antes de continuar.
  {: .lab-note .important .compact}

  > **Salida esperada:** Al menos cuatro controles principales están conformes.
  {: .lab-note .output .compact}

### Tarea 4.2. Guardar el entregable

- {% include step_label.html %} Guarda el PBIX.

  ```text
  C:\DAF\Practica_05\05_dashboard_ventas.pbix
  ```

- {% include step_label.html %} Guarda una copia de la plantilla como:

  ```text
  C:\DAF\Practica_05\05_validacion_dashboard.xlsx
  ```

  > **Salida esperada:** El PBIX y la evidencia de validación están listos para reutilizarse en el Reto 5.
  {: .lab-note .output .compact}

{% capture r4 %}{{ results[3] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r4 %}
{% include support-prompt.html task="tarea4" %}