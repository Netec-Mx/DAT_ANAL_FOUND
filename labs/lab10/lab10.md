---
layout: lab
title: "Reto 5: Dashboard para un supervisor regional"
permalink: /lab10/lab10/
images_base: /labs/lab10/img
duration: "30 minutos"
objective:
  - Adaptar un dashboard existente de Power BI a las necesidades de un supervisor regional, seleccionando KPI, filtros y visuales relevantes y validando la vista contra Snowflake.
prerequisites:
  - Haber completado la Práctica 5: Construir un dashboard básico de desempeño de ventas.
  - Disponer del archivo C:\DAF\Practica_05\05_dashboard_ventas.pbix.
  - Power BI Desktop instalado y disponible.
  - Cuenta de Snowflake activa con acceso de lectura a DATA_ANALYTICS_FOUNDATIONS.CURATED.
  - Acceso a Internet para descargar los archivos auxiliares del reto.
introduction:
  - Un supervisor regional necesita una vista más enfocada que el dashboard general de la Práctica 5. Debe poder revisar rápidamente el desempeño de su región, comparar canales, detectar cambios de margen e identificar categorías que requieren atención. Partirás del PBIX existente y adaptarás la página sin reconstruir el modelo desde cero.
slug: lab10
lab_number: 10
final_result: >
  Al finalizar tendrás una copia del dashboard orientada a un supervisor regional,
  con KPI, filtros y visualizaciones justificadas, una medida DAX adicional y
  una validación regional contra Snowflake.
notes:
  - Parte del PBIX creado en la Práctica 5.
  - Configura Norte como región inicial, pero conserva la posibilidad de cambiar de región.
  - Usa QUALITYFLAG = VALID como población analítica.
  - No agregues visuales solo por estética; cada elemento debe apoyar una pregunta o decisión.
  - Mantén los mismos filtros al comparar Power BI y Snowflake.
references:
  - text: Microsoft Learn - Create measures in Power BI Desktop
    url: https://learn.microsoft.com/power-bi/transform-model/desktop-tutorial-create-measures
  - text: Microsoft Learn - Slicer visual in Power BI
    url: https://learn.microsoft.com/power-bi/visuals/power-bi-visualization-slicer-visual
prev: /lab5/lab5/
next: /lab6/lab6/
---

---

## 🎯 Tarea 1. Definir las necesidades del supervisor — 5 min

Antes de modificar Power BI, relacionarás las preguntas del usuario con los KPI y visuales que realmente necesita.

### Tarea 1.1. Preparar los archivos

- {% include step_label.html %} Abre Git Bash y crea la carpeta `Reto_05`.

  ```bash
  mkdir -p /c/DAF/Reto_05
  ```

  > **Salida esperada:** Existe `C:\DAF\Reto_05\`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Descarga los archivos auxiliares.

  1. [Descargar medida DAX adicional](URL_DAX_RETO_05)
  2. [Descargar SQL de validación regional](URL_SQL_RETO_05)
  3. [Descargar plantilla del Reto 5](URL_PLANTILLA_RETO_05)

  Guarda:

  ```text
  C:\DAF\Reto_05\05_reto_medidas_regionales.dax
  C:\DAF\Reto_05\05_reto_validacion_regional.sql
  C:\DAF\Reto_05\Plantilla_Reto5_Dashboard_Regional.xlsx
  ```

  > **Salida esperada:** Los tres recursos están disponibles en `Reto_05`.
  {: .lab-note .output .compact}

### Tarea 1.2. Traducir las preguntas a requisitos

- {% include step_label.html %} Abre `Plantilla_Reto5_Dashboard_Regional.xlsx` y completa la hoja `Requisitos`.

  Trabaja con estas preguntas:

  ```text
  ¿Cómo va mi región?
  ¿Qué canal contribuye más?
  ¿Dónde está cayendo el margen?
  ¿Qué categoría requiere atención?
  ```

  > **Salida esperada:** Cada pregunta tiene KPI, visual, filtro y decisión asociada.
  {: .lab-note .output .compact}

- {% include step_label.html %} Marca cada requisito como `Definido` cuando la relación pregunta → KPI → visual sea clara.

  > **Importante:** No elijas visuales por preferencia estética; deben ayudar a responder la pregunta.
  {: .lab-note .important .compact}

  > **Salida esperada:** Los cuatro requisitos están definidos antes de editar el PBIX.
  {: .lab-note .output .compact}

{% assign results = site.data.task-results[page.slug].results %}
{% capture r1 %}{{ results[0] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r1 %}
{% include support-prompt.html task="tarea1" %}

---

## 🧮 Tarea 2. Adaptar KPI y filtros — 7 min

Crearás una copia del dashboard, agregarás una medida regional y ajustarás los filtros necesarios.

### Tarea 2.1. Crear la copia de trabajo

- {% include step_label.html %} Abre en Power BI Desktop:

  ```text
  C:\DAF\Practica_05\05_dashboard_ventas.pbix
  ```

- {% include step_label.html %} Usa **Archivo > Guardar como** y crea:

  ```text
  C:\DAF\Reto_05\05_reto_dashboard_regional.pbix
  ```

  > **Salida esperada:** Trabajas sobre una copia independiente del dashboard general.
  {: .lab-note .output .compact}

### Tarea 2.2. Agregar la medida regional

- {% include step_label.html %} Selecciona `Ventas Curadas` y crea una nueva medida desde `05_reto_medidas_regionales.dax`.

  ```dax
  Margen por Transacción =
  DIVIDE([Margen Bruto], [Transacciones], 0)
  ```

  Formatea la medida como moneda.

  > **Salida esperada:** `Margen por Transacción` está disponible para los visuales.
  {: .lab-note .output .compact}

### Tarea 2.3. Ajustar slicers

- {% include step_label.html %} Conserva o agrega estos slicers:

  ```text
  Fecha
  Región
  Canal
  Categoría
  ```

- {% include step_label.html %} En el slicer `Región`, selecciona inicialmente:

  ```text
  NORTE
  ```

  > **Nota:** No bloquees el slicer; el supervisor debe poder cambiar de región.
  {: .lab-note .info .compact}

  > **Salida esperada:** Norte aparece como vista inicial y los demás filtros siguen disponibles.
  {: .lab-note .output .compact}

{% capture r2 %}{{ results[1] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r2 %}
{% include support-prompt.html task="tarea2" %}

---

## 📊 Tarea 3. Construir la vista regional — 10 min

Simplificarás la página para responder las preguntas del supervisor con una jerarquía visual clara.

### Tarea 3.1. Ajustar las tarjetas

- {% include step_label.html %} Conserva cuatro tarjetas principales:

  ```text
  Ventas Netas
  Margen %
  Ticket Promedio
  Margen por Transacción
  ```

  > **Salida esperada:** Los cuatro KPI están visibles en la zona superior de la página.
  {: .lab-note .output .compact}

- {% include step_label.html %} Oculta o elimina tarjetas que no apoyen directamente las preguntas del supervisor.

  Registra la decisión en `Decision_Diseno`.

  > **Salida esperada:** El dashboard contiene menos elementos redundantes.
  {: .lab-note .output .compact}

### Tarea 3.2. Ajustar visualizaciones

- {% include step_label.html %} Conserva el gráfico de líneas mensual.

  Configura:

  ```text
  Eje: Calendario[Año-Mes]
  Valor: [Ventas Netas]
  ```

  > **Salida esperada:** El supervisor puede detectar cambios temporales de su región.
  {: .lab-note .output .compact}

- {% include step_label.html %} Configura un gráfico de barras por canal.

  ```text
  Eje: CHANNEL
  Valor: [Ventas Netas]
  ```

  > **Salida esperada:** Los canales pueden compararse dentro de la región seleccionada.
  {: .lab-note .output .compact}

- {% include step_label.html %} Configura un gráfico de barras por categoría.

  ```text
  Eje: CATEGORY
  Valor: [Margen %]
  ```

  Ordena de menor a mayor por `[Margen %]`.

  > **Importante:** Este visual busca categorías con margen menor; no debe interpretarse únicamente por volumen de ventas.
  {: .lab-note .important .compact}

  > **Salida esperada:** Las categorías con margen más bajo aparecen primero.
  {: .lab-note .output .compact}

### Tarea 3.3. Probar la interacción

- {% include step_label.html %} Cambia temporalmente el slicer de `Región` y confirma que tarjetas y gráficos responden.

  Después vuelve a:

  ```text
  NORTE
  ```

  > **Salida esperada:** La vista regional es reutilizable para otras regiones.
  {: .lab-note .output .compact}

{% capture r3 %}{{ results[2] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r3 %}
{% include support-prompt.html task="tarea3" %}

---

## ✅ Tarea 4. Validar y justificar el diseño — 8 min

Comprobarás que la vista regional mantiene cifras consistentes y explicarás por qué el diseño es adecuado para el supervisor.

### Tarea 4.1. Validar Norte

- {% include step_label.html %} Con `Región = NORTE`, registra en la hoja `Validacion`:

  ```text
  Ventas Netas
  Margen %
  Transacciones
  Ticket Promedio
  Margen por Transacción
  ```

  > **Salida esperada:** La columna Power BI contiene los KPI de Norte.
  {: .lab-note .output .compact}

- {% include step_label.html %} Ejecuta `05_reto_validacion_regional.sql` en Snowflake y registra los resultados equivalentes.

  > **Salida esperada:** Power BI y Snowflake usan la misma población `QUALITYFLAG = VALID`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Marca cada control como `Conforme` o `Investigar`.

  > **Importante:** Los conteos deben coincidir exactamente y los importes solo pueden diferir por redondeo.
  {: .lab-note .important .compact}

  > **Salida esperada:** Los KPI principales de Norte están validados.
  {: .lab-note .output .compact}

### Tarea 4.2. Ejecutar una prueba mensual

- {% include step_label.html %} Selecciona un mes de 2025 en Power BI y conserva `Región = NORTE`.

  Registra:

  ```text
  Ventas Netas
  Margen %
  Transacciones
  Ticket Promedio
  ```

- {% include step_label.html %} Ajusta `<FECHA_INICIAL>` y `<FECHA_FINAL>` en la consulta final del SQL y ejecútala.

  > **Salida esperada:** La prueba mensual confirma que los filtros temporales de Power BI producen los mismos resultados que Snowflake.
  {: .lab-note .output .compact}

### Tarea 4.3. Justificar el dashboard

- {% include step_label.html %} Completa la hoja `Cierre`.

  Documenta:

  ```text
  KPI más importante
  visual más útil
  filtro más importante
  elemento eliminado
  mejora obtenida
  hallazgo principal
  limitación
  ```

  > **Salida esperada:** La adaptación está justificada desde la necesidad del supervisor.
  {: .lab-note .output .compact}

- {% include step_label.html %} Guarda el archivo:

  ```text
  C:\DAF\Reto_05\05_reto_dashboard_regional.pbix
  ```

  Guarda también una copia del Excel como:

  ```text
  C:\DAF\Reto_05\05_reto_dashboard_regional.xlsx
  ```

  > **Salida esperada:** PBIX y evidencia del reto están listos para entrega.
  {: .lab-note .output .compact}

{% capture r4 %}{{ results[3] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r4 %}
{% include support-prompt.html task="tarea4" %}