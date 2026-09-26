---
layout: lab
title: "Reto 7: Recomendación al comité de operaciones"
permalink: /lab14/lab14/
images_base: /labs/lab14/img
duration: "45 minutos"
objective:
  - Transformar la evidencia del caso integral en una recomendación ejecutiva trazable, comparando alternativas, explicitando riesgos y proponiendo un próximo paso proporcional al nivel de certeza.
prerequisites:
  - Haber completado la Práctica 7: Caso integral de desempeño comercial.
  - Disponer de C:\DAF\Practica_07\07_caso_integral.xlsx.
  - Disponer de C:\DAF\Practica_07\07_caso_integral.sql.
  - Disponer de C:\DAF\Practica_07\07_caso_integral.pbix.
  - Microsoft Excel instalado.
  - Power BI Desktop y acceso a Snowflake disponibles para consultar evidencia si es necesario.
introduction:
  - El comité de operaciones necesita una recomendación concreta basada en el análisis del proyecto integrador. No debes reconstruir el análisis completo. Debes seleccionar una situación prioritaria, demostrarla con tres evidencias trazables, comparar alternativas y proponer una acción con riesgos, limitaciones y nivel de certeza explícitos.
slug: lab14
lab_number: 14
final_result: >
  Al finalizar tendrás una recomendación ejecutiva para el comité de operaciones,
  respaldada por tres evidencias, alternativas evaluadas, riesgos explícitos,
  un próximo paso verificable y un brief de una página.
notes:
  - Utiliza únicamente evidencia trazable al proyecto integrador.
  - No conviertas asociación en causalidad.
  - No elijas una alternativa solo porque fue la primera hipótesis.
  - La recomendación debe ser reversible o verificable cuando la certeza sea limitada.
references:
  - text: Caso integral de la Práctica 7
    url: URL_CASO_INTEGRAL_PRACTICA_07
prev: /lab7/lab7/
next: /
---

---

## 🎯 Tarea 1. Seleccionar la decisión prioritaria — 7 min

Elegirás una sola decisión que el comité de operaciones deba considerar.

### Tarea 1.1. Preparar el reto

- {% include step_label.html %} Abre Git Bash y crea la carpeta `Reto_07`.

  ```bash
  mkdir -p /c/DAF/Reto_07
  ```

  > **Salida esperada:** Existe `C:\DAF\Reto_07\`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Descarga la plantilla.

  [Descargar plantilla del Reto 7](URL_PLANTILLA_RETO_07)

  Guarda:

  ```text
  C:\DAF\Reto_07\Plantilla_Reto7_Comite_Operaciones.xlsx
  ```

  > **Salida esperada:** La plantilla está disponible localmente.
  {: .lab-note .output .compact}

### Tarea 1.2. Elegir la prioridad

- {% include step_label.html %} Abre `C:\DAF\Practica_07\07_caso_integral.xlsx` y revisa los tres hallazgos priorizados.

- {% include step_label.html %} En `Decision_Prioritaria`, selecciona una sola situación que requiera decisión.

  Puede relacionarse con:

  ```text
  región
  canal
  categoría
  margen
  descuentos
  devoluciones
  ```

  > **Importante:** Selecciona la prioridad por evidencia y relevancia para la decisión, no por el tamaño del gráfico.
  {: .lab-note .important .compact}

  > **Salida esperada:** Existe una decisión concreta con métrica, segmento, periodo y criterio de éxito.
  {: .lab-note .output .compact}

{% assign results = site.data.task-results[page.slug].results %}
{% capture r1 %}{{ results[0] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r1 %}
{% include support-prompt.html task="tarea1" %}

---

## 🔎 Tarea 2. Construir el caso de evidencia — 12 min

Seleccionarás las tres evidencias más sólidas que justifican que el comité revise la situación prioritaria.

### Tarea 2.1. Seleccionar tres evidencias

- {% include step_label.html %} En `Caso_Evidencia`, registra tres evidencias provenientes de SQL, Power BI o la matriz de la Práctica 7.

  Para cada una incluye:

  ```text
  fuente
  filtro
  valor o magnitud
  comparación
  qué demuestra
  limitación
  ```

  > **Salida esperada:** Existen tres evidencias trazables y comparables.
  {: .lab-note .output .compact}

- {% include step_label.html %} Si una evidencia procede de Power BI, confirma periodo y filtros antes de registrarla.

  > **Salida esperada:** Otra persona puede reproducir el mismo valor.
  {: .lab-note .output .compact}

### Tarea 2.2. Verificar el alcance de la evidencia

- {% include step_label.html %} Revisa si las tres evidencias apoyan la misma decisión o si alguna responde a una pregunta diferente.

  > **Importante:** Elimina evidencia interesante pero irrelevante para la decisión seleccionada.
  {: .lab-note .important .compact}

  > **Salida esperada:** El caso de evidencia es coherente y enfocado.
  {: .lab-note .output .compact}

{% capture r2 %}{{ results[1] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r2 %}
{% include support-prompt.html task="tarea2" %}

---

## ⚖️ Tarea 3. Evaluar alternativas — 10 min

Compararás opciones antes de formular la recomendación final.

### Tarea 3.1. Definir alternativas

- {% include step_label.html %} En `Alternativas`, define tres posibles respuestas a la situación.

  Ejemplos:

  ```text
  revisar un canal
  priorizar una categoría
  revisar política de descuentos
  profundizar devoluciones
  mantener la estrategia y recolectar evidencia adicional
  ```

  > **Salida esperada:** Existen al menos tres alternativas reales.
  {: .lab-note .output .compact}

- {% include step_label.html %} Para cada alternativa registra:

  ```text
  evidencia a favor
  riesgo
  información faltante
  factibilidad
  impacto esperado
  ```

  > **Advertencia:** No asumas que mayor impacto aparente implica mayor factibilidad o certeza.
  {: .lab-note .warning .compact}

  > **Salida esperada:** Las alternativas pueden compararse por evidencia, riesgo y factibilidad.
  {: .lab-note .output .compact}

### Tarea 3.2. Considerar no actuar todavía

- {% include step_label.html %} Evalúa también la alternativa `No actuar aún`.

  > **Salida esperada:** El participante reconoce que recolectar más evidencia también puede ser una decisión válida.
  {: .lab-note .output .compact}

{% capture r3 %}{{ results[2] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r3 %}
{% include support-prompt.html task="tarea3" %}

---

## 🧭 Tarea 4. Formular la recomendación — 10 min

Seleccionarás una alternativa y justificarás por qué es preferible frente a las demás.

### Tarea 4.1. Completar la recomendación

- {% include step_label.html %} En `Recomendacion`, redacta:

  ```text
  recomendación
  evidencia principal
  alternativa descartada
  riesgo principal
  acción inmediata
  próximo paso
  nivel de certeza
  ```

  > **Salida esperada:** Existe una recomendación completa y trazable.
  {: .lab-note .output .compact}

- {% include step_label.html %} Indica qué condición o nueva evidencia podría hacerte cambiar la decisión.

  > **Importante:** Una recomendación profesional puede cambiar cuando aparece mejor evidencia.
  {: .lab-note .important .compact}

  > **Salida esperada:** La decisión tiene una condición de revisión explícita.
  {: .lab-note .output .compact}

### Tarea 4.2. Revisar causalidad

- {% include step_label.html %} Revisa que la recomendación no afirme que un factor causó el resultado si el proyecto solo demuestra asociación.

  > **Salida esperada:** La redacción es proporcional al nivel de certeza.
  {: .lab-note .output .compact}

{% capture r4 %}{{ results[3] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r4 %}
{% include support-prompt.html task="tarea4" %}

---

## 📝 Tarea 5. Preparar el mensaje al comité — 6 min

Resumirás el caso en una sola página ejecutiva.

### Tarea 5.1. Completar el brief

- {% include step_label.html %} En `Brief_Ejecutivo`, completa:

  ```text
  decisión solicitada
  hallazgo principal
  evidencia 1
  evidencia 2
  evidencia 3
  recomendación
  riesgo / limitación
  ```

  > **Salida esperada:** El caso puede leerse sin revisar todo el libro.
  {: .lab-note .output .compact}

- {% include step_label.html %} Verifica que el brief indique claramente qué debe decidir el comité.

  > **Salida esperada:** La recomendación no se limita a describir resultados.
  {: .lab-note .output .compact}

### Tarea 5.2. Guardar el entregable

- {% include step_label.html %} Completa la hoja `Checklist`.

- {% include step_label.html %} Guarda una copia final como:

  ```text
  C:\DAF\Reto_07\07_recomendacion_comite.xlsx
  ```

  > **Salida esperada:** El archivo contiene decisión, evidencia, alternativas, recomendación y brief ejecutivo.
  {: .lab-note .output .compact}

{% capture r5 %}{{ results[4] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r5 %}
{% include support-prompt.html task="tarea5" %}
