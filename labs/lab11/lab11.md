---
layout: lab
title: "Práctica 6: Interpretación ejecutiva de un dashboard"
permalink: /lab11/lab11/
images_base: /labs/lab11/img
duration: "20 minutos"
objective:
  - Interpretar un dashboard comercial distinguiendo evidencia, observación, hallazgo e inferencia, evaluando el nivel de sustento de afirmaciones y redactando mensajes ejecutivos proporcionales a la evidencia disponible.
prerequisites:
  - Haber completado la Práctica 5 y el Reto 5.
  - Disponer del archivo C:\DAF\Practica_05\05_dashboard_ventas.pbix.
  - Power BI Desktop instalado y disponible.
  - Microsoft Excel instalado.
  - Acceso a Internet para descargar la plantilla de la práctica.
introduction:
  - En esta práctica no construirás visualizaciones ni medidas. El objetivo es leer críticamente el dashboard creado en la Práctica 5, registrar evidencia literal, convertirla en observaciones comparables, evaluar afirmaciones y redactar dos mensajes ejecutivos sin atribuir causalidad cuando los datos solo muestran asociación o concentración.
slug: lab11
lab_number: 11
final_result: >
  Al finalizar dispondrás de un brief ejecutivo en Excel con contexto del dashboard,
  seis evidencias literales, tres observaciones comparables, tres afirmaciones evaluadas
  y dos mensajes ejecutivos con acción y nivel de certeza.
notes:
  - No modifiques el modelo ni las medidas del PBIX.
  - No pulses Actualizar salvo que el instructor lo indique.
  - Una afirmación no sustentada no necesariamente es falsa; significa que el dashboard no la demuestra.
  - Registra siempre periodo, filtros y unidad antes de interpretar un valor.
references:
  - text: Dashboard construido en la Práctica 5
    url: URL_DASHBOARD_PRACTICA_05
prev: /reto5/reto5/
next: /reto6/reto6/
---

---

## 🧭 Tarea 1. Confirmar contexto y filtros — 4 min

Establecerás el alcance del dashboard antes de interpretar cualquier KPI o comparación.

### Tarea 1.1. Preparar los archivos

- {% include step_label.html %} Abre Git Bash y crea la carpeta `Practica_06`.

  ```bash
  mkdir -p /c/DAF/Practica_06
  ```

  > **Salida esperada:** Existe `C:\DAF\Practica_06\`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Descarga la plantilla de interpretación.

  [Descargar plantilla de la Práctica 6](URL_PLANTILLA_PRACTICA_06)

  Guarda:

  ```text
  C:\DAF\Practica_06\Plantilla_Practica6_Interpretacion_Ejecutiva.xlsx
  ```

  > **Salida esperada:** La plantilla está disponible localmente.
  {: .lab-note .output .compact}

- {% include step_label.html %} Abre en Power BI Desktop:

  ```text
  C:\DAF\Practica_05\05_dashboard_ventas.pbix
  ```

  > **Importante:** No modifiques el modelo ni pulses **Actualizar**.
  {: .lab-note .important .compact}

  > **Salida esperada:** Se muestra el dashboard de desempeño creado en la Práctica 5.
  {: .lab-note .output .compact}

### Tarea 1.2. Registrar el contexto

- {% include step_label.html %} Abre la hoja `Contexto` y registra:

  ```text
  periodo
  región
  canal
  categoría
  moneda / unidad
  filtros activos
  ```

  > **Salida esperada:** El contexto del dashboard está documentado antes de interpretar valores.
  {: .lab-note .output .compact}

- {% include step_label.html %} Si un elemento no es visible o no puede confirmarse, regístralo como limitación.

  > **Advertencia:** No asumas una moneda, periodo o filtro que no esté disponible en la evidencia.
  {: .lab-note .warning .compact}

  > **Salida esperada:** Las limitaciones de contexto están explícitas.
  {: .lab-note .output .compact}

{% assign results = site.data.task-results[page.slug].results %}
{% capture r1 %}{{ results[0] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r1 %}
{% include support-prompt.html task="tarea1" %}

---

## 🔎 Tarea 2. Registrar evidencia y observaciones — 6 min

Separarás valores visibles del dashboard de cualquier explicación o recomendación.

### Tarea 2.1. Registrar seis datos literales

- {% include step_label.html %} En la hoja `Evidencia`, registra seis valores visibles:

  ```text
  2 KPI
  2 valores temporales
  2 valores por segmento
  ```

  Para cada uno incluye:

  ```text
  visual
  métrica
  valor literal
  periodo o segmento
  filtros
  ```

  > **Salida esperada:** Existen seis registros trazables al dashboard.
  {: .lab-note .output .compact}

- {% include step_label.html %} Conserva la unidad visible y evita interpretar la causa del valor.

  > **Ejemplo correcto:** “La tarjeta Ventas Netas muestra X bajo los filtros actuales.”
  {: .lab-note .info .compact}

  > **Salida esperada:** Los seis registros describen evidencia y no explicaciones causales.
  {: .lab-note .output .compact}

### Tarea 2.2. Crear tres observaciones comparables

- {% include step_label.html %} Convierte la evidencia en tres observaciones usando comparaciones válidas.

  Antes de aceptar cada comparación revisa:

  ```text
  periodo
  escala
  filtros
  granularidad
  denominador
  ```

  > **Salida esperada:** Existen tres observaciones cuantificadas y contextualizadas.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra una comparación descartada si no cumple los criterios anteriores.

  > **Importante:** Una comparación inválida también es un hallazgo metodológico útil.
  {: .lab-note .important .compact}

  > **Salida esperada:** Existe al menos una comparación marcada como no comparable cuando corresponda.
  {: .lab-note .output .compact}

{% capture r2 %}{{ results[1] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r2 %}
{% include support-prompt.html task="tarea2" %}

---

## ⚖️ Tarea 3. Evaluar afirmaciones — 5 min

Clasificarás conclusiones que podrían parecer razonables, pero que requieren distintos niveles de evidencia.

### Tarea 3.1. Clasificar el nivel de sustento

- {% include step_label.html %} Abre la hoja `Afirmaciones` y evalúa:

  ```text
  A1. La región Norte tiene el peor desempeño.
  A2. El canal Online causó la caída de ventas.
  A3. La categoría con menor margen debería eliminarse.
  ```

- {% include step_label.html %} Para cada afirmación selecciona:

  ```text
  Sustentada
  Parcialmente sustentada
  No sustentada
  ```

  > **Importante:** Clasifica según la evidencia visible, no según lo que parezca lógico.
  {: .lab-note .important .compact}

  > **Salida esperada:** Las tres afirmaciones tienen clasificación y evidencia asociada.
  {: .lab-note .output .compact}

### Tarea 3.2. Corregir el lenguaje

- {% include step_label.html %} Reescribe cada afirmación usando un lenguaje proporcional al nivel de certeza.

  Puedes utilizar expresiones como:

  ```text
  el dashboard muestra...
  se observa...
  los datos sugieren...
  la variación se concentra en...
  requiere validación adicional...
  ```

  > **Advertencia:** No utilices “causó”, “demuestra” o “garantiza” si la evidencia solo muestra asociación.
  {: .lab-note .warning .compact}

  > **Salida esperada:** Cada afirmación tiene una versión responsable y una limitación explícita.
  {: .lab-note .output .compact}

{% capture r3 %}{{ results[2] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r3 %}
{% include support-prompt.html task="tarea3" %}

---

## 📝 Tarea 4. Redactar mensajes ejecutivos — 5 min

Convertirás la evidencia en dos mensajes breves orientados a decisión.

### Tarea 4.1. Construir dos mensajes

- {% include step_label.html %} En la hoja `Mensajes`, redacta dos mensajes de 40 a 60 palabras.

  Cada mensaje debe contener:

  ```text
  Evidencia
  Implicación
  Acción
  Certeza
  ```

  > **Salida esperada:** Existen dos mensajes completos y trazables a la evidencia registrada.
  {: .lab-note .output .compact}

- {% include step_label.html %} Usa un mensaje para desempeño general y otro para una región, canal o categoría relevante.

  > **Nota:** La acción puede ser investigar, priorizar, revisar o validar; no necesita ser una decisión irreversible.
  {: .lab-note .info .compact}

  > **Salida esperada:** Los mensajes conectan evidencia con una acción verificable.
  {: .lab-note .output .compact}

### Tarea 4.2. Guardar el brief

- {% include step_label.html %} Guarda una copia como:

  ```text
  C:\DAF\Practica_06\06_brief_interpretacion.xlsx
  ```

  > **Salida esperada:** El brief contiene contexto, evidencia, afirmaciones y mensajes ejecutivos.
  {: .lab-note .output .compact}

- {% include step_label.html %} Cierra Power BI sin guardar cambios en el PBIX.

  > **Salida esperada:** El dashboard original de la Práctica 5 permanece sin modificaciones.
  {: .lab-note .output .compact}

{% capture r4 %}{{ results[3] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r4 %}
{% include support-prompt.html task="tarea4" %}
