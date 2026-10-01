---
layout: lab
title: "Reto 6: Cuestionar una conclusión engañosa"
permalink: /lab12/lab12/
images_base: /labs/lab12/img
duration: "25 minutos"
objective:
  - Evaluar críticamente una conclusión ejecutiva, separar hechos, inferencias y causalidad, clasificar el nivel de sustento de cada afirmación y reescribirla de forma proporcional a la evidencia disponible.
prerequisites:
  - Haber completado la Práctica 6; Interpretación ejecutiva de un dashboard.
  - Disponer del archivo C:\DAF\Practica_05\05_dashboard_ventas.pbix.
  - Disponer de C:\DAF\Practica_06\06_brief_interpretacion.xlsx.
  - Power BI Desktop y Microsoft Excel instalados.
  - Acceso a Internet para descargar la plantilla del reto.
introduction:
  - Un gerente afirma que la región Norte está perdiendo ventas porque el canal Online tiene demasiado descuento y propone reducir promociones inmediatamente. Tu objetivo será comprobar qué partes de esa conclusión están respaldadas por el dashboard, qué partes son inferencias o causalidad no demostrada y cómo debería reescribirse la conclusión antes de tomar una decisión.
slug: lab12
lab_number: 12
final_result: >
  Al finalizar tendrás una evaluación trazable de cuatro afirmaciones, evidencia registrada
  desde el dashboard, una clasificación de su nivel de sustento y una conclusión ejecutiva
  revisada con una acción prudente y un nivel de certeza explícito.
notes:
  - No modifiques el modelo ni las medidas del dashboard.
  - No pulses Actualizar salvo instrucción del instructor.
  - No sustentada significa no demostrada con la evidencia disponible; no significa necesariamente falsa.
  - Una correlación o concentración visible no demuestra causalidad.
references:
  - text: Dashboard construido en la Práctica 5
    url: URL_DASHBOARD_PRACTICA_05
prev: /lab11/lab11/
next: /lab13/lab13/
---

---

## 🧩 Tarea 1. Descomponer la conclusión — 5 min

Separarás una conclusión compleja en afirmaciones independientes que puedan evaluarse por evidencia.

### Tarea 1.1. Preparar el reto

- {% include step_label.html %} Abre Git Bash y crea la carpeta `Reto_06`.

  ```bash
  mkdir -p /c/DAF/Reto_06
  ```

  > **Salida esperada:** Existe `C:\DAF\Reto_06\`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Descarga la plantilla del reto.

  [Descargar plantilla del Reto 6](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap6/Plantilla_Reto6_Conclusion_Enganosa.xlsx)

  Guarda:

  ```text
  C:\DAF\Reto_06\Plantilla_Reto6_Conclusion_Enganosa.xlsx
  ```

  > **Salida esperada:** La plantilla está disponible localmente.
  {: .lab-note .output .compact}

- {% include step_label.html %} Abre en Power BI Desktop:

  ```text
  C:\DAF\Practica_05\05_dashboard_ventas.pbix
  ```

  > **Importante:** Trabaja con el dashboard como evidencia. No modifiques el modelo.
  {: .lab-note .important .compact}

### Tarea 1.2. Separar la afirmación

- {% include step_label.html %} Abre el archivo descargado `Plantilla_Reto6_Conclusion_Enganosa.xlsx`y lee la conclusión propuesta:

  > “La región Norte está perdiendo ventas porque el canal Online tiene demasiado descuento. Debemos reducir las promociones inmediatamente.”

- {% include step_label.html %} En `Descomposicion`, revisa estas cuatro partes:

  ```text
  C1. Norte está perdiendo ventas.
  C2. Online concentra la caída.
  C3. El descuento causó la caída.
  C4. Reducir promociones resolverá el problema.
  ```

  > **Salida esperada:** La conclusión está separada en hechos potenciales, inferencias causales y recomendación.
  {: .lab-note .output .compact}

- {% include step_label.html %} Para cada parte escribe qué evidencia tendría que existir para demostrarla.

  > **Salida esperada:** Cada afirmación tiene un criterio explícito de evidencia.
  {: .lab-note .output .compact}

{% assign results = site.data.task-results[page.slug].results %}
{% capture r1 %}{{ results[0] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r1 %}
{% include support-prompt.html task="tarea1" %}

---

## 🔎 Tarea 2. Buscar evidencia en el dashboard — 7 min

Revisarás el dashboard para identificar qué partes de la conclusión pueden comprobarse directamente.

### Tarea 2.1. Revisar Norte y Online

- {% include step_label.html %} Usa los slicers para seleccionar `Región = NORTE` y revisa la tendencia mensual de `Ventas Netas`.

  > **Salida esperada:** Existe evidencia para evaluar si Norte presenta una caída en el periodo visible.
  {: .lab-note .output .compact}

- {% include step_label.html %} Revisa el visual por `Channel` y compara `Online` con los demás canales.

  > **Salida esperada:** Puedes determinar si Online concentra o no una parte relevante de la variación visible.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra en `Evidencia` los valores o patrones que respaldan o contradicen C1 y C2.

  > **Importante:** Registra periodo y filtros junto con cada evidencia.
  {: .lab-note .important .compact}

  > **Salida esperada:** C1 y C2 tienen evidencia trazable al dashboard.
  {: .lab-note .output .compact}

### Tarea 2.2. Examinar causalidad y acción

- {% include step_label.html %} Busca si el dashboard contiene información suficiente sobre descuentos, promociones y su relación temporal con ventas.

  > **Salida esperada:** Se documenta qué información existe y qué información falta para C3.
  {: .lab-note .output .compact}

- {% include step_label.html %} Determina si el dashboard demuestra que reducir promociones mejoraría ventas o margen.

  > **Advertencia:** Una recomendación de intervención requiere evidencia adicional si el dashboard es descriptivo.
  {: .lab-note .warning .compact}

  > **Salida esperada:** Se documenta la evidencia faltante para C4.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra al menos seis evidencias o ausencias relevantes en la hoja `Evidencia`.

  > **Salida esperada:** El reto cuenta con evidencia suficiente para clasificar las cuatro afirmaciones.
  {: .lab-note .output .compact}

{% capture r2 %}{{ results[1] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r2 %}
{% include support-prompt.html task="tarea2" %}

---

## ⚖️ Tarea 3. Clasificar el nivel de sustento — 6 min

Determinarás qué partes de la conclusión pueden mantenerse y cuáles deben reducir su nivel de certeza.

### Tarea 3.1. Clasificar las cuatro afirmaciones

- {% include step_label.html %} En `Clasificacion`, asigna a C1–C4 una categoría:

  ```text
  Sustentada
  Parcialmente sustentada
  No sustentada
  ```

  > **Importante:** Clasifica según la evidencia encontrada, no según lo que esperabas encontrar.
  {: .lab-note .important .compact}

  > **Salida esperada:** Las cuatro afirmaciones tienen nivel de sustento explícito.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra la evidencia disponible y la evidencia faltante para cada afirmación.

  > **Salida esperada:** La clasificación puede justificarse sin depender de opinión personal.
  {: .lab-note .output .compact}

### Tarea 3.2. Corregir cada afirmación

- {% include step_label.html %} Reescribe cada parte usando lenguaje responsable.

  Puedes usar:

  ```text
  el dashboard muestra...
  la variación se concentra en...
  se observa una asociación...
  los datos sugieren...
  no puede determinarse con la evidencia disponible...
  requiere validación adicional...
  ```

  > **Advertencia:** No uses “causó”, “demuestra” o “resolverá” cuando la evidencia no permita sostener causalidad.
  {: .lab-note .warning .compact}

  > **Salida esperada:** C1–C4 tienen una redacción prudente y una acción de validación.
  {: .lab-note .output .compact}

{% capture r3 %}{{ results[2] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r3 %}
{% include support-prompt.html task="tarea3" %}

---

## 📝 Tarea 4. Reescribir la conclusión ejecutiva — 7 min

Integrarás las partes sustentadas en una conclusión útil para la decisión sin exceder lo que los datos permiten afirmar.

### Tarea 4.1. Construir la versión revisada

- {% include step_label.html %} En `Reescritura`, documenta qué sí muestra la evidencia, qué solo sugiere, qué no puede concluirse y qué evidencia adicional falta.

  > **Salida esperada:** Se distingue evidencia directa, inferencia y necesidad de validación.
  {: .lab-note .output .compact}

- {% include step_label.html %} Redacta una conclusión ejecutiva final de 60 a 90 palabras.

  Debe incluir:

  ```text
  Evidencia
  Interpretación prudente
  Acción reversible
  Nivel de certeza
  ```

  > **Importante:** Prioriza revisar o validar antes de modificar políticas de forma irreversible.
  {: .lab-note .important .compact}

  > **Salida esperada:** Existe una conclusión ejecutiva corregida y accionable.
  {: .lab-note .output .compact}

### Tarea 4.2. Cerrar el reto

- {% include step_label.html %} Completa la hoja `Checklist`.

  > **Salida esperada:** Los criterios están conformes o tienen una observación pendiente.
  {: .lab-note .output .compact}

- {% include step_label.html %} Guarda una copia final como:

  ```text
  C:\DAF\Reto_06\06_reto_conclusion_enganosa.xlsx
  ```

  > **Salida esperada:** El archivo contiene descomposición, evidencia, clasificación y conclusión revisada.
  {: .lab-note .output .compact}

- {% include step_label.html %} Cierra Power BI sin guardar cambios sobre el PBIX.

  > **Salida esperada:** El dashboard permanece sin modificaciones.
  {: .lab-note .output .compact}

{% capture r4 %}{{ results[3] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r4 %}
{% include support-prompt.html task="tarea4" %}