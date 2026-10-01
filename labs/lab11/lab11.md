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
  - text: Microsoft Learn - Tips for designing a great Power BI dashboard
    url: https://learn.microsoft.com/en-us/power-bi/create-reports/service-dashboards-design-tips
  - text: Microsoft Learn - Tips and tricks for creating reports in Power BI
    url: https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-tips-and-tricks-for-creating-reports
  - text: Microsoft Learn - Interact with visuals in Power BI reports and dashboards
    url: https://learn.microsoft.com/en-us/power-bi/explore-reports/end-user-visualizations
prev: /lab10/lab10/
next: /lab12/lab12/
---

---

## 🧭 Tarea 1. Confirmar contexto y filtros — 4 min

Establecerás el alcance del dashboard antes de interpretar cualquier KPI o comparación.

### Tarea 1.1. Preparar los archivos

- {% include step_label.html %} Abre Git Bash y crea la carpeta `Practica_06`.

  Ejecuta:

  ```bash
  mkdir -p /c/DAF/Practica_06
  ```

  Presiona **Enter** y verifica que el comando termine sin errores.

  > **Nota:** La ruta `/c/DAF/Practica_06` en Git Bash corresponde a `C:\DAF\Practica_06\` en Windows.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existe `C:\DAF\Practica_06\`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Descarga la plantilla de interpretación.

  Abre el enlace:

  [Descargar plantilla de la Práctica 6](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap6/Plantilla_Practica6_Interpretacion_Ejecutiva.xlsx)

  Guarda el archivo exactamente como:

  ```text
  C:\DAF\Practica_06\Plantilla_Practica6_Interpretacion_Ejecutiva.xlsx
  ```

  > **Nota:** Si el navegador lo descarga primero en `Descargas`, mueve después el archivo a `C:\DAF\Practica_06\` y conserva el nombre indicado.
  {: .lab-note .info .compact}

  > **Salida esperada:** La plantilla está disponible localmente.
  {: .lab-note .output .compact}

- {% include step_label.html %} Abre en Power BI Desktop:

  ```text
  C:\DAF\Practica_05\05_dashboard_ventas.pbix
  ```

  Para abrirlo, usa **Archivo > Abrir > Examinar este dispositivo**, navega a `C:\DAF\Practica_05\` y selecciona `05_dashboard_ventas.pbix`.

  Espera a que el dashboard termine de cargar y confirma que se muestran las tarjetas, filtros y gráficos creados en la Práctica 5.

  > **Importante:** No modifiques el modelo, no edites medidas y no pulses **Actualizar**.
  {: .lab-note .important .compact}

  > **Nota:** Durante esta práctica solo interpretarás información existente. Si realizas selecciones en slicers para consultar valores, no necesitas guardar esos cambios.
  {: .lab-note .info .compact}

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

  Abre en Excel:

  ```text
  C:\DAF\Practica_06\Plantilla_Practica6_Interpretacion_Ejecutiva.xlsx
  ```

  y selecciona la hoja `Contexto`.

  Regresa a Power BI y revisa los slicers visibles antes de escribir cada dato:

  - **periodo:** copia la fecha inicial y final mostradas en el slicer `Date`;
  - **región:** registra el valor visible en `REGION`; si muestra `Todas`, escribe `Todas`;
  - **canal:** registra el valor visible en `CHANNEL`; si muestra `Todos`, escribe `Todos`;
  - **categoría:** registra el valor visible en `CATEGORY`; si el dashboard no tiene ese slicer, escribe `No visible`;
  - **moneda / unidad:** revisa si existe un filtro o indicación de `Currency`; si no existe, escribe `Currency no visible / no normalizada`;
  - **filtros activos:** resume únicamente las selecciones que realmente puedas confirmar.

  > **Nota:** Mantén Power BI y Excel abiertos al mismo tiempo. Consulta un elemento en Power BI y regístralo inmediatamente en Excel para evitar cambiar accidentalmente el contexto.
  {: .lab-note .info .compact}

  > **Salida esperada:** El contexto del dashboard está documentado antes de interpretar valores.
  {: .lab-note .output .compact}

- {% include step_label.html %} Si un elemento no es visible o no puede confirmarse, regístralo como limitación.

  En la misma hoja `Contexto`, utiliza el espacio de limitaciones para documentar situaciones como:

  ```text
  Currency no visible
  Category no disponible como filtro
  No se puede confirmar si los importes están normalizados
  ```

  > **Advertencia:** No asumas una moneda, periodo o filtro que no esté disponible en la evidencia.
  {: .lab-note .warning .compact}

  > **Nota:** Una limitación no invalida el análisis; indica hasta dónde puede llegar la interpretación con la información disponible.
  {: .lab-note .info .compact}

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

  Abre la hoja `Evidencia` en Excel y mantén Power BI visible.

  Para los **2 KPI**, elige dos tarjetas del dashboard, por ejemplo `Ventas Netas`, `Margen Bruto`, `Margen %` o `Ticket Promedio`, y copia el valor exactamente como aparece.

  Para los **2 valores temporales**, usa el gráfico mensual. Coloca el cursor sobre dos puntos de meses diferentes y toma el valor mostrado en el tooltip.

  Para los **2 valores por segmento**, utiliza un mismo gráfico por región, canal o categoría y registra dos segmentos distintos manteniendo los mismos filtros.

  Para cada uno incluye:

  ```text
  visual
  métrica
  valor literal
  periodo o segmento
  filtros
  ```

  > **Nota:** En `visual` escribe el nombre del objeto de Power BI, por ejemplo `Tarjeta Ventas Netas` o `Evolución mensual de ventas`. En `valor literal`, copia el dato sin recalcularlo.
  {: .lab-note .info .compact}

  > **Importante:** Los dos valores por segmento deben provenir del mismo visual y mantener el mismo contexto general; solo debe cambiar el segmento comparado.
  {: .lab-note .important .compact}

  > **Salida esperada:** Existen seis registros trazables al dashboard.
  {: .lab-note .output .compact}

- {% include step_label.html %} Conserva la unidad visible y evita interpretar la causa del valor.

  Revisa los seis registros que acabas de capturar y asegúrate de que describan únicamente lo que Power BI muestra.

  > **Ejemplo correcto:** “La tarjeta Ventas Netas muestra X bajo los filtros actuales.”
  {: .lab-note .info .compact}

  > **Advertencia:** Evita frases como `las ventas bajaron por...`, `el canal causó...` o `la región tiene problemas porque...`, ya que agregan una explicación que el dashboard puede no demostrar.
  {: .lab-note .warning .compact}

  > **Salida esperada:** Los seis registros describen evidencia y no explicaciones causales.
  {: .lab-note .output .compact}

### Tarea 2.2. Crear tres observaciones comparables

- {% include step_label.html %} Convierte la evidencia en tres observaciones usando comparaciones válidas.

  Para cada observación selecciona dos valores de la hoja `Evidencia` que puedan compararse directamente.

  Antes de aceptar cada comparación revisa:

  ```text
  periodo
  escala
  filtros
  granularidad
  denominador
  ```

  Verifica lo siguiente:

  - **periodo:** compara periodos equivalentes, por ejemplo un mes contra otro mes;
  - **escala:** compara la misma métrica y unidad;
  - **filtros:** conserva los mismos filtros generales, excepto la dimensión que estés comparando;
  - **granularidad:** no mezcles sin aclararlo una región, un cliente, una transacción o un periodo;
  - **denominador:** para tasas o promedios confirma que ambos valores usan la misma base.

  Redacta cada observación con una estructura como:

  ```text
  Bajo los mismos filtros, [segmento o periodo A] muestra [métrica] de X,
  mientras [segmento o periodo B] muestra Y.
  ```

  > **Nota:** Una observación describe una diferencia o concentración visible. Todavía no explica por qué ocurrió.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existen tres observaciones cuantificadas y contextualizadas.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra una comparación descartada si no cumple los criterios anteriores.

  Si encuentras dos valores que parecen comparables pero cambian periodo, filtros, escala, granularidad o denominador, regístralos como:

  ```text
  No comparable
  ```

  y explica brevemente el motivo.

  Ejemplo:

  ```text
  No comparable: un valor está filtrado a Norte y el otro representa todas las regiones.
  ```

  > **Importante:** Una comparación inválida también es un hallazgo metodológico útil.
  {: .lab-note .important .compact}

  > **Nota:** Si todas tus comparaciones candidatas son válidas, no inventes una comparación incorrecta. Registra este punto únicamente cuando realmente exista una diferencia de contexto.
  {: .lab-note .info .compact}

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

  Para **A1**, revisa si el dashboard permite comparar Norte con las demás regiones usando el mismo periodo, filtros y métrica.

  Para **A2**, revisa si el dashboard demuestra una relación causal entre `Online` y una caída de ventas, o si únicamente muestra concentración o asociación.

  Para **A3**, revisa si el dashboard tiene suficiente información para justificar eliminar una categoría o si solo permite identificar una categoría con menor margen.

  > **Nota:** No evalúes si las afirmaciones “suenan razonables”. Evalúa únicamente si pueden sostenerse con los visuales y métricas disponibles.
  {: .lab-note .info .compact}

- {% include step_label.html %} Para cada afirmación selecciona:

  ```text
  Sustentada
  Parcialmente sustentada
  No sustentada
  ```

  Usa:

  - `Sustentada` cuando la evidencia visible respalde directamente la afirmación;
  - `Parcialmente sustentada` cuando exista evidencia relacionada, pero falten elementos para sostener toda la conclusión;
  - `No sustentada` cuando el dashboard no aporte evidencia suficiente para demostrarla.

  En la columna de evidencia registra el visual consultado, la métrica observada, el filtro utilizado y el dato o limitación encontrada.

  > **Importante:** Clasifica según la evidencia visible, no según lo que parezca lógico.
  {: .lab-note .important .compact}

  > **Nota:** `No sustentada` no significa necesariamente `falsa`; significa que el dashboard no la demuestra.
  {: .lab-note .info .compact}

  > **Salida esperada:** Las tres afirmaciones tienen clasificación y evidencia asociada.
  {: .lab-note .output .compact}

### Tarea 3.2. Corregir el lenguaje

- {% include step_label.html %} Reescribe cada afirmación usando un lenguaje proporcional al nivel de certeza.

  Para **A1**, evita una conclusión absoluta si no has revisado todas las métricas de desempeño.

  Para **A2**, elimina lenguaje causal como `causó`, `provocó` o `generó` si el dashboard solo muestra asociación.

  Para **A3**, separa el hallazgo de la decisión: una categoría con menor margen puede justificar revisar o investigar, pero no necesariamente eliminar.

  Puedes utilizar expresiones como:

  ```text
  el dashboard muestra...
  se observa...
  los datos sugieren...
  la variación se concentra en...
  requiere validación adicional...
  ```

  Agrega también una limitación explícita para cada afirmación, por ejemplo:

  ```text
  No se observan variables causales en el dashboard.
  Se requiere validar Currency.
  El dashboard no contiene evidencia suficiente para recomendar eliminación.
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

  Usa únicamente datos que ya hayas registrado en `Contexto`, `Evidencia` y `Afirmaciones`.

  Para el **mensaje 1**, resume el desempeño general del dashboard.

  Para el **mensaje 2**, selecciona una región, canal o categoría relevante que ya hayas documentado.

  Cada mensaje debe contener:

  ```text
  Evidencia
  Implicación
  Acción
  Certeza
  ```

  Puedes organizarlo así:

  ```text
  [Evidencia observada]. Esto sugiere [implicación prudente].
  Se recomienda [acción verificable].
  Nivel de certeza: [alto / medio / bajo] porque [limitación].
  ```

  > **Nota:** No introduzcas cifras nuevas en esta etapa. Los mensajes deben poder rastrearse a información que ya registraste.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existen dos mensajes completos y trazables a la evidencia registrada.
  {: .lab-note .output .compact}

- {% include step_label.html %} Usa un mensaje para desempeño general y otro para una región, canal o categoría relevante.

  Antes de finalizar, revisa que:

  ```text
  cada mensaje tenga entre 40 y 60 palabras
  incluya al menos una evidencia verificable
  no introduzca causalidad no demostrada
  proponga una acción concreta
  declare o refleje el nivel de certeza
  ```

  > **Nota:** La acción puede ser investigar, priorizar, revisar o validar; no necesita ser una decisión irreversible.
  {: .lab-note .info .compact}

  > **Salida esperada:** Los mensajes conectan evidencia con una acción verificable.
  {: .lab-note .output .compact}

### Tarea 4.2. Guardar el brief

- {% include step_label.html %} Guarda una copia como:

  ```text
  C:\DAF\Practica_06\06_brief_interpretacion.xlsx
  ```

  En Excel usa **Archivo > Guardar como**, selecciona `C:\DAF\Practica_06\` y escribe `06_brief_interpretacion.xlsx`.

  > **Nota:** Conserva la plantilla original si deseas reutilizarla. El archivo `06_brief_interpretacion.xlsx` es el entregable de la práctica.
  {: .lab-note .info .compact}

  > **Salida esperada:** El brief contiene contexto, evidencia, afirmaciones y mensajes ejecutivos.
  {: .lab-note .output .compact}

- {% include step_label.html %} Cierra Power BI sin guardar cambios en el PBIX.

  En Power BI selecciona **Archivo > Cerrar**.

  Si aparece una pregunta para guardar cambios, selecciona **No guardar**.

  > **Importante:** No guardes las selecciones temporales de filtros realizadas durante la interpretación.
  {: .lab-note .important .compact}

  > **Salida esperada:** El dashboard original de la Práctica 5 permanece sin modificaciones.
  {: .lab-note .output .compact}

{% capture r4 %}{{ results[3] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r4 %}
{% include support-prompt.html task="tarea4" %}
