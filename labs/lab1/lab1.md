---
layout: lab
title: "Práctica 1: Convertir solicitudes operativas en preguntas analíticas"
permalink: /lab1/lab1/
images_base: /labs/lab1/img
duration: "25 minutos"
objective:
  - Transformar una solicitud operativa del liderazgo comercial en una pregunta analítica medible, trazable y orientada a una decisión.
prerequisites:
  - Máquina virtual de Windows disponible.
  - Microsoft Excel instalado y operativo.
  - Git Bash disponible para crear la estructura de carpetas.
  - Acceso a Internet para descargar los archivos desde las URL proporcionadas.
  - Conocimientos básicos de métricas, dimensiones, periodos y comparaciones.
introduction:
  - En esta práctica trabajarás con el contexto de un dataset artificial masivo de ventas, disponible en versiones equivalentes para Excel, Snowflake y Power BI, con entre 500,000 y 1,000,000 de transacciones. A partir de una solicitud del liderazgo comercial, identificarás ambigüedades, definirás los componentes analíticos necesarios y redactarás una pregunta medible que pueda guiar las prácticas posteriores del curso.
slug: lab1
lab_number: 1
final_result: >
  Al finalizar dispondrás de una ficha analítica en Excel con una solicitud de negocio desambiguada, una pregunta analítica medible, sus métricas, periodos, dimensiones, decisión asociada, campos confirmados en el diccionario y una hipótesis inicial marcada como pendiente de validación.
notes:
  - En esta práctica no consultarás Snowflake ni construirás visualizaciones en Power BI; ambos se utilizarán en prácticas posteriores.
  - No inventes nombres de campos. Utiliza únicamente los nombres confirmados en el diccionario de datos.
  - Una hipótesis expresa una explicación posible; no debe redactarse como una causa confirmada.
references:
  - text: Microsoft Support - Crear y dar formato a tablas en Excel
    url: https://support.microsoft.com/es-es/office/crear-tablas-y-darles-formato-e81aa349-b006-4f8a-9806-5af9df0ac664
  - text: Microsoft Learn - Introducción a Power BI
    url: https://learn.microsoft.com/es-es/power-bi/fundamentals/power-bi-overview
prev: /
next: /lab2/lab2/
---

---

<!-- Aquí comienzan las instrucciones paso a paso de la práctica -->

## 🔎 Tarea 1. Analizar la solicitud del negocio — 8 min

Prepararás el espacio de trabajo y revisarás una solicitud del liderazgo comercial para identificar qué información falta antes de convertirla en una pregunta analítica medible.

### Tarea 1.1. Preparar los recursos de análisis

Crearás la estructura central del curso, descargarás los archivos requeridos desde las URL externas y abrirás los recursos que utilizarás en la práctica.

- {% include step_label.html %} Abre Git Bash y crea la estructura central de trabajo para el curso y la Práctica 01.

  ```bash
  mkdir -p /c/DAF/00_recursos /c/DAF/Practica_01
  ```

  > **Nota:** `C:\DAF\` será el directorio central del curso. Las prácticas posteriores utilizarán carpetas como `Practica_02`, `Practica_03` y así sucesivamente.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existen las carpetas `C:\DAF\00_recursos\` y `C:\DAF\Practica_01\`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Descarga los tres archivos requeridos desde las URL proporcionadas y guárdalos en las rutas indicadas.

  1. [Descargar diccionario de datos](URL_DICCIONARIO_DATOS)
  2. [Descargar plantilla de la Práctica 1](URL_PLANTILLA_PRACTICA_01)
  3. [Descargar muestra de ventas](URL_MUESTRA_VENTAS)

  Guarda los archivos exactamente en:

  ```text
  C:\DAF\00_recursos\Diccionario_Datos_Ventas_Retail_LATAM_2026_1.xlsx
  C:\DAF\00_recursos\Muestra_Ventas_Retail_LATAM_2026_1.csv
  C:\DAF\Practica_01\Plantilla_Pregunta_Analitica.xlsx
  ```

  > **Importante:** El diccionario y la muestra son recursos compartidos del curso. No los edites ni cambies su nombre.
  {: .lab-note .important .compact}

  > **Salida esperada:** Los tres archivos descargados existen en las rutas indicadas y conservan sus nombres originales.
  {: .lab-note .output .compact}

- {% include step_label.html %} Abre la plantilla y el diccionario en Excel, y guarda una copia editable de la plantilla como `01_pregunta_analitica.xlsx`.

  Guarda la copia en:

  ```text
  C:\DAF\Practica_01\01_pregunta_analitica.xlsx
  ```

  > **Nota:** La muestra CSV se conservará en `00_recursos` para consulta y para prácticas posteriores; no necesitas abrirla todavía.
  {: .lab-note .info .compact}

  > **Salida esperada:** Están abiertos el diccionario y `01_pregunta_analitica.xlsx`, mientras los archivos originales permanecen sin modificar.
  {: .lab-note .output .compact}

### Tarea 1.2. Detectar ambigüedades de la solicitud

Analizarás la solicitud del liderazgo para separar la necesidad de negocio de los elementos que todavía deben definirse antes de medirla.

- {% include step_label.html %} Registra en la plantilla la solicitud: “Necesitamos entender si realmente existe una caída en las ventas y dónde se concentra antes de decidir dónde intervenir”.

  > **Nota:** El dataset del caso contiene entre 500,000 y 1,000,000 de transacciones y dispone de versiones equivalentes para Excel, Snowflake y Power BI.
  {: .lab-note .info .compact}

  > **Salida esperada:** La solicitud original está registrada sin modificar su intención de negocio.
  {: .lab-note .output .compact}

- {% include step_label.html %} Identifica al menos cuatro elementos faltantes o ambiguos de la solicitud.

  > **Importante:** Considera como mínimo métrica, periodo, comparación, dimensiones y decisión que se pretende apoyar.
  {: .lab-note .important .compact}

  > **Salida esperada:** La plantilla contiene al menos cuatro ambigüedades claramente documentadas.
  {: .lab-note .output .compact}

- {% include step_label.html %} Define en una frase la decisión comercial que debería apoyar el análisis.

  > **Advertencia:** No redactes una conclusión. La decisión debe indicar qué podría hacerse después de revisar la evidencia.
  {: .lab-note .warning .compact}

  > **Salida esperada:** Existe una decisión concreta, por ejemplo determinar qué segmentos requieren una revisión comercial prioritaria.
  {: .lab-note .output .compact}

{% assign results = site.data.task-results[page.slug].results %}
{% capture r1 %}{{ results[0] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r1 %}

{% include support-prompt.html task="tarea1" %}

---

## 🧩 Tarea 2. Construir la pregunta analítica — 9 min

Definirás los componentes necesarios para convertir la solicitud original en una pregunta medible que pueda responderse posteriormente con Excel, Snowflake o Power BI.

### Tarea 2.1. Definir los componentes analíticos

Seleccionarás la métrica, los periodos y las dimensiones que permitirán medir el comportamiento solicitado por el liderazgo comercial.

- {% include step_label.html %} Selecciona una métrica principal y regístrala en la plantilla.

  > **Nota:** Para este caso puedes utilizar ventas netas si el diccionario confirma que el campo existe o que puede calcularse de forma reproducible.
  {: .lab-note .info .compact}

  > **Salida esperada:** La plantilla contiene una métrica principal claramente definida.
  {: .lab-note .output .compact}

- {% include step_label.html %} Define el periodo actual y el periodo de comparación que utilizarás.

  > **Importante:** Los periodos deben ser comparables. Evita contrastar meses parciales contra meses completos.
  {: .lab-note .important .compact}

  > **Salida esperada:** El periodo actual y el comparativo están documentados con un criterio temporal claro.
  {: .lab-note .output .compact}

- {% include step_label.html %} Selecciona las dimensiones necesarias para localizar dónde se concentra la variación.

  > **Nota:** Región, canal y categoría de producto son ejemplos válidos solo si existen en el diccionario.
  {: .lab-note .info .compact}

  > **Salida esperada:** La plantilla contiene las dimensiones que segmentarán el análisis.
  {: .lab-note .output .compact}

### Tarea 2.2. Formular la pregunta analítica

Integrarás los componentes definidos en una sola pregunta orientada a una decisión y sin afirmar causalidad que todavía no ha sido demostrada.

- {% include step_label.html %} Redacta una primera versión de la pregunta incluyendo métrica, periodo, comparación y dimensiones.

  > **Salida esperada:** Existe una pregunta inicial que puede responderse mediante datos y no contiene expresiones ambiguas como “mejor” o “peor”.
  {: .lab-note .output .compact}

- {% include step_label.html %} Agrega a la pregunta la decisión que pretende apoyar el análisis.

  > **Nota:** Una estructura útil es: “¿Cuál fue la variación de [métrica] en [periodo] frente a [comparativo], por [dimensiones], para apoyar [decisión]?”.
  {: .lab-note .info .compact}

  > **Salida esperada:** La pregunta relaciona explícitamente la evidencia requerida con una decisión comercial.
  {: .lab-note .output .compact}

- {% include step_label.html %} Revisa la redacción y elimina cualquier afirmación causal no sustentada.

  > **Advertencia:** Evita preguntas como “¿qué causó la caída?”. El dataset puede mostrar variaciones, concentraciones y asociaciones, pero no demuestra causalidad por sí solo.
  {: .lab-note .warning .compact}

  > **Salida esperada:** La pregunta final es medible, neutral y no presupone una causa.
  {: .lab-note .output .compact}

{% capture r2 %}{{ results[1] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r2 %}

{% include support-prompt.html task="tarea2" %}

---

## ✅ Tarea 3. Validar y documentar la pregunta — 8 min

Comprobarás que la pregunta pueda responderse con el dataset disponible, registrarás una hipótesis inicial y completarás la ficha que servirá como entrada para las siguientes prácticas.

### Tarea 3.1. Validar la trazabilidad con el dataset

Confirmarás que las métricas y dimensiones seleccionadas tienen respaldo en el diccionario y que la pregunta puede trasladarse a las distintas versiones del dataset.

- {% include step_label.html %} Busca en el diccionario los campos necesarios para responder la pregunta analítica.

  > **Importante:** Copia los nombres exactos de los campos. Si alguno no existe, marca “No disponible / requiere validación”.
  {: .lab-note .important .compact}

  > **Salida esperada:** Cada componente principal de la pregunta tiene un campo confirmado o una observación de validación pendiente.
  {: .lab-note .output .compact}

- {% include step_label.html %} Verifica que la pregunta pueda responderse mediante una tabla, consulta o visualización definida.

  > **Nota:** No es necesario construir todavía la consulta o el dashboard; solo comprobar que la pregunta sea técnicamente medible.
  {: .lab-note .info .compact}

  > **Salida esperada:** La pregunta puede traducirse posteriormente a cálculos en Excel, SQL en Snowflake o visualizaciones en Power BI.
  {: .lab-note .output .compact}

- {% include step_label.html %} Registra una hipótesis inicial relacionada con la variación de ventas y márcala como pendiente de validación.

  > **Advertencia:** Una hipótesis es una explicación posible. No la presentes como un hallazgo ni como una causa confirmada.
  {: .lab-note .warning .compact}

  > **Salida esperada:** Existe al menos una hipótesis verificable y su estado indica que requiere evidencia adicional.
  {: .lab-note .output .compact}

### Tarea 3.2. Finalizar el entregable

Completarás una revisión breve para asegurar que la ficha analítica sea consistente, reutilizable y adecuada como entrada para las prácticas posteriores.

- {% include step_label.html %} Completa la ficha con solicitud, decisión, métrica, periodos, dimensiones, pregunta, campos e hipótesis.

  > **Salida esperada:** Todos los apartados esenciales de la ficha analítica están completos.
  {: .lab-note .output .compact}

- {% include step_label.html %} Revisa que la pregunta especifique qué se medirá, cuándo, contra qué referencia y por cuáles dimensiones.

  > **Importante:** Si cualquiera de estos componentes falta, corrige la pregunta antes de continuar.
  {: .lab-note .important .compact}

  > **Salida esperada:** La pregunta cumple los criterios mínimos de medición, comparación y segmentación.
  {: .lab-note .output .compact}

- {% include step_label.html %} Guarda el archivo final de la práctica en `C:\DAF\Practica_01\01_pregunta_analitica.xlsx`.

  > **Nota:** Conserva este archivo. Se reutilizará para validar calidad de datos y mantener trazabilidad en las prácticas posteriores.
  {: .lab-note .info .compact}

  > **Salida esperada:** `C:\DAF\Practica_01\01_pregunta_analitica.xlsx` existe y contiene la ficha analítica validada.
  {: .lab-note .output .compact}

{% capture r3 %}{{ results[2] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r3 %}

{% include support-prompt.html task="tarea3" %}