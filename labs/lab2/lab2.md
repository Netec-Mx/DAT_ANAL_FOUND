---
layout: lab
title: "Reto 1: Diagnóstico de una caída de ventas"
permalink: /lab2/lab2/
images_base: /labs/lab2/img
duration: "13 minutos"
objective:
  - Formular de manera autónoma una pregunta analítica medible a partir de una solicitud comercial ambigua, identificando la decisión, la métrica, el periodo, las dimensiones y una hipótesis que deberá validarse posteriormente.
prerequisites:
  - Haber completado la Práctica 1: Convertir solicitudes operativas en preguntas analíticas.
  - Disponer de Microsoft Excel para Microsoft 365.
  - Tener acceso a Internet para descargar la plantilla del reto.
  - Conservar los recursos compartidos en C:\\DAF\\00_recursos\\.
introduction:
  - En este reto trabajarás de forma autónoma con una solicitud del liderazgo comercial relacionada con una posible caída de desempeño. Deberás transformar esa solicitud en una pregunta analítica medible y trazable al dataset artificial masivo de ventas, disponible en versiones equivalentes para Excel, Snowflake y Power BI. No consultarás todavía Snowflake ni construirás visualizaciones en Power BI; el objetivo es definir correctamente qué debe analizarse antes de trabajar con los datos.
slug: lab2
lab_number: 2
final_result: >
  Al finalizar habrás creado un archivo de Excel con la interpretación de la solicitud, las ambigüedades detectadas, la decisión que debe apoyar el análisis, una pregunta analítica medible y una hipótesis inicial claramente identificada como pendiente de validación.
notes:
  - El reto debe resolverse con mayor autonomía que la práctica. Utiliza como referencia el método aprendido, pero evita copiar literalmente la pregunta construida en la Práctica 1.
  - El dataset es artificial y representa entre 500,000 y 1,000,000 de transacciones. La pregunta formulada deberá ser compatible con un análisis posterior en Snowflake y Power BI.
references:
  - text: Microsoft Support - Crear y dar formato a tablas en Excel
    url: https://support.microsoft.com/es-es/office/crear-y-dar-formato-a-tablas-2cf0c3f0-ecfc-4f0e-99f1-a2cd4f7f7f6e
  - text: Snowflake Documentation
    url: https://docs.snowflake.com/
prev: /lab1/lab1/
next: /lab2/lab2/
---

<!-- Aquí comienzan las instrucciones paso a paso del reto -->

## 🔎 Tarea 1. Interpretar el escenario comercial — 4 min

Analizarás una solicitud del liderazgo comercial para identificar qué información falta, qué decisión se pretende apoyar y qué evidencia será necesaria antes de realizar cualquier análisis sobre el dataset.

### Tarea 1.1. Preparar el archivo del reto

Crearás la carpeta del Reto 01 dentro del directorio central y descargarás la plantilla específica sin duplicar los recursos compartidos del curso.

- {% include step_label.html %} Abre Git Bash y crea la carpeta `Reto_01` dentro del directorio central del curso.

  ```bash
  mkdir -p /c/DAF/Reto_01
  ```

  > **Nota:** Reutiliza el diccionario y la muestra existentes en `C:\DAF\00_recursos\`; no es necesario descargarlos nuevamente.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existe la carpeta `C:\DAF\Reto_01\` y los recursos compartidos continúan disponibles en `C:\DAF\00_recursos\`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Descarga la plantilla del reto desde la URL proporcionada, ábrela en Excel y guarda la copia de trabajo con el nombre indicado.

  [Descargar plantilla del Reto 1](URL_PLANTILLA_RETO_01)

  Guarda primero la descarga como:

  ```text
  C:\DAF\Reto_01\Plantilla_Reto1_Diagnostico.xlsx
  ```

  Después guarda la copia editable como:

  ```text
  C:\DAF\Reto_01\01_reto_diagnostico_caida_ventas.xlsx
  ```

  > **Importante:** No modifiques `Plantilla_Reto1_Diagnostico.xlsx`. Trabaja únicamente sobre `01_reto_diagnostico_caida_ventas.xlsx`.
  {: .lab-note .important .compact}

  > **Salida esperada:** Excel muestra la copia editable del reto y la plantilla original permanece sin modificar.
  {: .lab-note .output .compact}

### Tarea 1.2. Detectar ambigüedades y definir la decisión

Trabajarás con una solicitud distinta a la utilizada en la práctica guiada para demostrar que puedes aplicar el método a un nuevo escenario.

- {% include step_label.html %} Registra en la primera hoja la siguiente solicitud del liderazgo comercial:

  > “La dirección comercial considera que la región Norte está perdiendo desempeño y propone aumentar promociones. Antes de aprobar presupuesto, solicita evidencia que permita determinar si el problema está realmente concentrado en esa región y qué segmentos deberían investigarse.”

  > **Advertencia:** La solicitud contiene una interpretación previa. No asumas que existe una caída ni que las promociones sean la solución correcta.
  {: .lab-note .warning .compact}

  > **Salida esperada:** La solicitud aparece registrada en el archivo exactamente como fue proporcionada.
  {: .lab-note .output .compact}

- {% include step_label.html %} Identifica al menos tres ambigüedades y escribe la decisión concreta que el análisis debería apoyar.

  > **Nota:** Considera elementos como métrica, periodo, comparación, dimensiones, alcance regional y criterio para aprobar una intervención comercial.
  {: .lab-note .info .compact}

  > **Salida esperada:** El archivo contiene tres o más ambigüedades y una decisión expresada con un verbo de acción, por ejemplo evaluar, priorizar, investigar o reasignar.
  {: .lab-note .output .compact}

{% assign results = site.data.task-results[page.slug].results %}
{% capture r1 %}{{ results[0] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r1 %}

{% include support-prompt.html task="tarea1" %}

---

## 📊 Tarea 2. Formular la pregunta analítica — 6 min

Convertirás la solicitud comercial en una pregunta que pueda responderse posteriormente con el dataset masivo, definiendo los componentes mínimos para que el análisis sea medible y reproducible.

### Tarea 2.1. Definir los componentes analíticos

Selecciona los elementos que permitirán transformar la solicitud general en una pregunta concreta y verificable con los datos disponibles.

- {% include step_label.html %} Define una métrica principal que permita evaluar el desempeño comercial de la región Norte.

  > **Importante:** Utiliza únicamente una métrica que exista en el diccionario o que pueda derivarse claramente de campos documentados.
  {: .lab-note .important .compact}

  > **Salida esperada:** Existe una métrica principal documentada, por ejemplo ventas netas, acompañada del nombre del campo o de una nota de validación pendiente.
  {: .lab-note .output .compact}

- {% include step_label.html %} Define el periodo actual y un periodo de comparación equivalente.

  > **Nota:** Evita comparar periodos parciales con periodos completos. La comparación debe permitir interpretar una variación de forma consistente.
  {: .lab-note .info .compact}

  > **Salida esperada:** El archivo contiene un periodo actual y un periodo comparativo claramente identificados.
  {: .lab-note .output .compact}

- {% include step_label.html %} Selecciona al menos tres dimensiones útiles para segmentar el análisis.

  > **Nota:** Puedes considerar región, canal, categoría, producto o mes, siempre que los campos estén disponibles en el diccionario.
  {: .lab-note .info .compact}

  > **Salida esperada:** Se documentan tres o más dimensiones relacionadas con la decisión comercial.
  {: .lab-note .output .compact}

### Tarea 2.2. Redactar la pregunta y registrar una hipótesis

Construye la pregunta analítica completa y separa claramente lo que deberá medirse de las explicaciones que todavía necesitan evidencia.

- {% include step_label.html %} Redacta una pregunta analítica que incluya métrica, periodo, comparación, dimensiones y decisión.

  > **Importante:** La pregunta debe poder responderse posteriormente mediante una consulta, una tabla o una visualización reproducible.
  {: .lab-note .important .compact}

  > **Salida esperada:** Existe una pregunta analítica completa, específica y orientada a apoyar la decisión definida en la Tarea 1.
  {: .lab-note .output .compact}

- {% include step_label.html %} Revisa la pregunta y elimina cualquier afirmación que dé por comprobada una causa o una caída.

  > **Advertencia:** Expresiones como “por qué cayó”, “la región perdió ventas por” o “las promociones resolverán” introducen conclusiones que todavía no han sido demostradas.
  {: .lab-note .warning .compact}

  > **Salida esperada:** La pregunta utiliza lenguaje descriptivo y verificable, sin afirmar causalidad.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra una hipótesis inicial que pueda investigarse en prácticas posteriores.

  > **Nota:** Una formulación adecuada sería: “La variación podría concentrarse en determinadas categorías o canales de la región Norte”.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existe al menos una hipótesis marcada explícitamente como `Pendiente de validación`.
  {: .lab-note .output .compact}

{% capture r2 %}{{ results[1] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r2 %}

{% include support-prompt.html task="tarea2" %}

---

## ✅ Tarea 3. Validar y entregar el resultado — 3 min

Realizarás una revisión final para confirmar que la pregunta cumple los criterios mínimos de una pregunta analítica y que el archivo puede utilizarse como entrada para las actividades posteriores del curso.

### Tarea 3.1. Revisar el resultado final

Comprueba que tu propuesta sea medible, trazable al dataset y que mantenga una separación correcta entre evidencia, hipótesis y decisión.

- {% include step_label.html %} Comprueba que la pregunta incluya métrica, periodo, comparación, dimensiones y una decisión explícita.

  > **Importante:** Si falta alguno de estos componentes, ajusta la pregunta antes de continuar.
  {: .lab-note .important .compact}

  > **Salida esperada:** La pregunta cumple los cinco componentes mínimos de validación.
  {: .lab-note .output .compact}

- {% include step_label.html %} Verifica que la hipótesis esté separada de la pregunta y que no se presente como un hecho confirmado.

  > **Advertencia:** La hipótesis deberá contrastarse con evidencia durante las prácticas de calidad, análisis descriptivo y exploración.
  {: .lab-note .warning .compact}

  > **Salida esperada:** La hipótesis permanece identificada como explicación posible y pendiente de validación.
  {: .lab-note .output .compact}

- {% include step_label.html %} Guarda el archivo y confirma que se encuentra en `C:\DAF\Reto_01\01_reto_diagnostico_caida_ventas.xlsx`.

  > **Nota:** Conserva este archivo porque la pregunta y la hipótesis podrán reutilizarse durante el análisis del dataset en Snowflake y Power BI.
  {: .lab-note .info .compact}

  > **Salida esperada:** `C:\DAF\Reto_01\01_reto_diagnostico_caida_ventas.xlsx` está guardado y listo para utilizarse como referencia posterior.
  {: .lab-note .output .compact}

{% capture r3 %}{{ results[2] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r3 %}

{% include support-prompt.html task="tarea3" %}