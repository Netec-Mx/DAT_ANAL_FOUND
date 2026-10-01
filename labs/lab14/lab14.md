---
layout: lab
title: "Reto 7: Recomendación al comité de operaciones"
permalink: /lab14/lab14/
images_base: /labs/lab14/img
duration: "45 minutos"
objective:
  - Transformar la evidencia del caso integral en una recomendación ejecutiva trazable, comparando alternativas, explicitando riesgos y proponiendo un próximo paso proporcional al nivel de certeza.
prerequisites:
  - Haber completado la Práctica 7; Caso integral de desempeño comercial.
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
  - text: Microsoft Learn - Tips for designing a great Power BI dashboard
    url: https://learn.microsoft.com/en-us/power-bi/create-reports/service-dashboards-design-tips
  - text: Microsoft Learn - Create report bookmarks in Power BI
    url: https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-bookmarks
  - text: Microsoft Learn - Drillthrough in Power BI reports
    url: https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-drillthrough
prev: /lab13/lab13/
next: /
---

---

## 🎯 Tarea 1. Seleccionar la decisión prioritaria — 7 min

Elegirás una sola decisión que el comité de operaciones deba considerar.

### Tarea 1.1. Preparar el reto

- {% include step_label.html %} Abre Git Bash y crea la carpeta `Reto_07`.

  Ejecuta:

  ```bash
  mkdir -p /c/DAF/Reto_07
  ```

  Presiona **Enter** y verifica que el comando termine sin errores.

  > **Nota:** La ruta `/c/DAF/Reto_07` en Git Bash corresponde a `C:\DAF\Reto_07\` en Windows.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existe `C:\DAF\Reto_07\`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Descarga la plantilla.

  Abre el enlace:

  [Descargar plantilla del Reto 7](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap7/Plantilla_Reto7_Comite_Operaciones.xlsx)

  Guarda el archivo exactamente como:

  ```text
  C:\DAF\Reto_07\Plantilla_Reto7_Comite_Operaciones.xlsx
  ```

  > **Nota:** Si el navegador descarga el archivo en `Descargas`, muévelo después a `C:\DAF\Reto_07\` sin cambiar el nombre.
  {: .lab-note .info .compact}

  > **Salida esperada:** La plantilla está disponible localmente.
  {: .lab-note .output .compact}

### Tarea 1.2. Elegir la prioridad

- {% include step_label.html %} Abre `C:\DAF\Practica_07\07_caso_integral.xlsx` y revisa los tres hallazgos priorizados.

  Abre el archivo en Excel y consulta la hoja:

  ```text
  Hallazgos_Cierre
  ```

  Revisa los tres hallazgos, su evidencia, nivel de certeza, recomendación y limitación.

  Identifica cuál de ellos requiere una decisión concreta del comité.

  > **Nota:** No selecciones todavía una acción. En este paso solo debes identificar qué situación merece prioridad para el comité.
  {: .lab-note .info .compact}

- {% include step_label.html %} En `Decision_Prioritaria`, selecciona una sola situación que requiera decisión.

  Abre en Excel:

  ```text
  C:\DAF\Reto_07\Plantilla_Reto7_Comite_Operaciones.xlsx
  ```

  y selecciona la hoja:

  ```text
  Decision_Prioritaria
  ```

  Puede relacionarse con:

  ```text
  región
  canal
  categoría
  margen
  descuentos
  devoluciones
  ```

  Registra como mínimo:

  ```text
  situación prioritaria
  métrica principal
  segmento
  periodo
  decisión requerida
  criterio de éxito
  ```

  La decisión debe ser específica. Evita expresiones generales como:

  ```text
  mejorar ventas
  revisar resultados
  ```

  Prefiere formulaciones como:

  ```text
  decidir si conviene priorizar la revisión de Online y Marketplace en Norte
  decidir si se requiere profundizar Tecnología antes de modificar promociones
  ```

  > **Importante:** Selecciona la prioridad por evidencia y relevancia para la decisión, no por el tamaño del gráfico.
  {: .lab-note .important .compact}

  > **Nota:** La prioridad debe poder vincularse directamente con al menos uno de los hallazgos de la Práctica 7.
  {: .lab-note .info .compact}

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

  Abre la hoja:

  ```text
  Caso_Evidencia
  ```

  Consulta, según sea necesario:

  ```text
  C:\DAF\Practica_07\07_caso_integral.xlsx
  C:\DAF\Practica_07\07_caso_integral.sql
  C:\DAF\Practica_07\07_caso_integral.pbix
  ```

  Selecciona tres evidencias que apoyen directamente la decisión prioritaria.

  Para cada una incluye:

  ```text
  fuente
  filtro
  valor o magnitud
  comparación
  qué demuestra
  limitación
  ```

  Usa estos criterios:

  - **fuente:** indica si proviene de SQL, Power BI o la matriz;
  - **filtro:** registra periodo, región, canal o categoría aplicados;
  - **valor o magnitud:** copia el dato exacto;
  - **comparación:** especifica contra qué periodo o segmento se compara;
  - **qué demuestra:** describe solo lo que la evidencia permite afirmar;
  - **limitación:** indica qué no puede concluirse con ese dato.

  > **Nota:** Una evidencia útil para el comité debe ser comprensible sin reconstruir todo el análisis.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existen tres evidencias trazables y comparables.
  {: .lab-note .output .compact}

- {% include step_label.html %} Si una evidencia procede de Power BI, confirma periodo y filtros antes de registrarla.

  Abre `07_caso_integral.pbix` y revisa los slicers o filtros activos.

  Confirma que coincidan con el dato que estás documentando:

  ```text
  periodo
  Region
  Channel
  Category
  ```

  Registra esos filtros junto con la evidencia.

  Si el valor también está disponible en Snowflake, verifica que ambos coincidan para el mismo alcance.

  > **Nota:** No registres un valor de Power BI sin indicar el contexto en el que fue obtenido.
  {: .lab-note .info .compact}

  > **Salida esperada:** Otra persona puede reproducir el mismo valor.
  {: .lab-note .output .compact}

### Tarea 2.2. Verificar el alcance de la evidencia

- {% include step_label.html %} Revisa si las tres evidencias apoyan la misma decisión o si alguna responde a una pregunta diferente.

  Lee las tres filas de `Caso_Evidencia` como si fueras un miembro del comité.

  Para cada evidencia pregúntate:

  ```text
  ¿apoya directamente la decisión prioritaria?
  ¿usa el mismo periodo o un periodo comparable?
  ¿el segmento es relevante para la decisión?
  ¿la métrica ayuda a justificar la recomendación?
  ```

  Si alguna evidencia responde a otro problema, reemplázala por una más pertinente.

  > **Importante:** Elimina evidencia interesante pero irrelevante para la decisión seleccionada.
  {: .lab-note .important .compact}

  > **Nota:** Tres evidencias coherentes son más útiles que muchas evidencias desconectadas.
  {: .lab-note .info .compact}

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

  Abre la hoja:

  ```text
  Alternativas
  ```

  Formula tres opciones distintas que el comité podría considerar.

  Ejemplos:

  ```text
  revisar un canal
  priorizar una categoría
  revisar política de descuentos
  profundizar devoluciones
  mantener la estrategia y recolectar evidencia adicional
  ```

  Procura que las alternativas representen decisiones diferentes, no variaciones menores de la misma acción.

  > **Nota:** Incluye al menos una alternativa de análisis o validación cuando la certeza del caso sea limitada.
  {: .lab-note .info .compact}

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

  Completa cada campo usando la evidencia de la Práctica 7.

  Interpreta los campos así:

  - **evidencia a favor:** dato que justifica considerar la alternativa;
  - **riesgo:** consecuencia posible si la alternativa resulta incorrecta;
  - **información faltante:** dato necesario para reducir incertidumbre;
  - **factibilidad:** qué tan viable es aplicarla con los recursos y datos disponibles;
  - **impacto esperado:** qué resultado se espera observar si la alternativa funciona.

  Usa una escala consistente para factibilidad e impacto, por ejemplo:

  ```text
  Alta
  Media
  Baja
  ```

  > **Advertencia:** No asumas que mayor impacto aparente implica mayor factibilidad o certeza.
  {: .lab-note .warning .compact}

  > **Nota:** No conviertas `impacto esperado` en una promesa. Exprésalo como resultado esperado o hipótesis de trabajo.
  {: .lab-note .info .compact}

  > **Salida esperada:** Las alternativas pueden compararse por evidencia, riesgo y factibilidad.
  {: .lab-note .output .compact}

### Tarea 3.2. Considerar no actuar todavía

- {% include step_label.html %} Evalúa también la alternativa `No actuar aún`.

  Considera esta opción cuando la evidencia sea insuficiente para justificar una intervención inmediata.

  Registra:

  ```text
  qué evidencia falta
  qué riesgo evita esperar
  qué riesgo genera esperar
  qué dato debería recopilarse
  cuánto permitiría mejorar la certeza
  ```

  > **Nota:** `No actuar aún` no significa ignorar el problema. Puede implicar ejecutar una validación, recopilar datos o realizar una prueba antes de una decisión mayor.
  {: .lab-note .info .compact}

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

  Abre la hoja:

  ```text
  Recomendacion
  ```

  Completa:

  ```text
  recomendación
  evidencia principal
  alternativa descartada
  riesgo principal
  acción inmediata
  próximo paso
  nivel de certeza
  ```

  Para redactar cada campo:

  - **recomendación:** indica qué debería aprobar o priorizar el comité;
  - **evidencia principal:** utiliza uno o dos datos que expliquen por qué;
  - **alternativa descartada:** menciona la opción más relevante que no elegiste y por qué;
  - **riesgo principal:** identifica qué podría salir mal;
  - **acción inmediata:** define una acción concreta que pueda ejecutarse ahora;
  - **próximo paso:** explica qué debe ocurrir después de la acción inicial;
  - **nivel de certeza:** usa `Alta`, `Media` o `Baja` y relaciónalo con la evidencia disponible.

  > **Nota:** La recomendación debe poder leerse de forma independiente sin revisar toda la hoja `Alternativas`.
  {: .lab-note .info .compact}

  > **Salida esperada:** Existe una recomendación completa y trazable.
  {: .lab-note .output .compact}

- {% include step_label.html %} Indica qué condición o nueva evidencia podría hacerte cambiar la decisión.

  Registra una condición de revisión concreta.

  Ejemplos:

  ```text
  si DiscountPct no presenta relación con la variación observada
  si Marketplace explica una proporción mayor de la caída que Online
  si la validación por Currency cambia la magnitud del hallazgo
  ```

  Escribe también qué dato o análisis permitiría evaluar esa condición.

  > **Importante:** Una recomendación profesional puede cambiar cuando aparece mejor evidencia.
  {: .lab-note .important .compact}

  > **Salida esperada:** La decisión tiene una condición de revisión explícita.
  {: .lab-note .output .compact}

### Tarea 4.2. Revisar causalidad

- {% include step_label.html %} Revisa que la recomendación no afirme que un factor causó el resultado si el proyecto solo demuestra asociación.

  Lee nuevamente la recomendación y busca verbos como:

  ```text
  causó
  provocó
  generó
  demuestra
  garantiza
  ```

  Si la evidencia no es causal, sustituye esas expresiones por:

  ```text
  se concentra en
  se observa en
  está asociado con
  sugiere
  requiere validación adicional
  ```

  > **Nota:** Una recomendación puede ser útil aunque el análisis no identifique una causa definitiva, siempre que la acción propuesta sea proporcional a la certeza disponible.
  {: .lab-note .info .compact}

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

  Abre la hoja:

  ```text
  Brief_Ejecutivo
  ```

  Completa:

  ```text
  decisión solicitada
  hallazgo principal
  evidencia 1
  evidencia 2
  evidencia 3
  recomendación
  riesgo / limitación
  ```

  Utiliza esta lógica:

  - **decisión solicitada:** qué debe aprobar, priorizar o revisar el comité;
  - **hallazgo principal:** resumen del problema en una sola idea;
  - **evidencia 1–3:** datos concretos y trazables;
  - **recomendación:** acción propuesta;
  - **riesgo / limitación:** principal incertidumbre que el comité debe conocer.

  > **Nota:** Evita copiar párrafos completos de otras hojas. Resume únicamente la información necesaria para tomar la decisión.
  {: .lab-note .info .compact}

  > **Salida esperada:** El caso puede leerse sin revisar todo el libro.
  {: .lab-note .output .compact}

- {% include step_label.html %} Verifica que el brief indique claramente qué debe decidir el comité.

  Lee únicamente la hoja `Brief_Ejecutivo` y comprueba que puedas responder:

  ```text
  ¿qué problema requiere atención?
  ¿qué evidencia lo demuestra?
  ¿qué alternativas se consideraron?
  ¿qué se recomienda?
  ¿qué riesgo o limitación existe?
  ¿qué debe decidir el comité?
  ```

  Si alguna respuesta no es clara, ajusta el brief antes de continuar.

  > **Nota:** El brief debe orientar una decisión, no limitarse a resumir resultados.
  {: .lab-note .info .compact}

  > **Salida esperada:** La recomendación no se limita a describir resultados.
  {: .lab-note .output .compact}

### Tarea 5.2. Guardar el entregable

- {% include step_label.html %} Completa la hoja `Checklist`.

  Revisa cada criterio y marca el estado únicamente cuando exista evidencia en el libro.

  Confirma como mínimo:

  ```text
  decisión prioritaria definida
  tres evidencias trazables
  alternativas comparadas
  riesgos documentados
  recomendación redactada
  condición de revisión
  brief ejecutivo completo
  ```

  > **Nota:** Si un criterio no está completo, regresa a la hoja correspondiente antes de guardar la versión final.
  {: .lab-note .info .compact}

- {% include step_label.html %} Guarda una copia final como:

  En Excel selecciona:

  ```text
  Archivo
  → Guardar como
  ```

  guarda en:

  ```text
  C:\DAF\Reto_07\07_recomendacion_comite.xlsx
  ```

  Verifica que el archivo se encuentre en `C:\DAF\Reto_07\` y que puedas abrirlo nuevamente.

  > **Importante:** Conserva `Plantilla_Reto7_Comite_Operaciones.xlsx` como archivo base y utiliza `07_recomendacion_comite.xlsx` como entregable final.
  {: .lab-note .important .compact}

  > **Salida esperada:** El archivo contiene decisión, evidencia, alternativas, recomendación y brief ejecutivo.
  {: .lab-note .output .compact}

{% capture r5 %}{{ results[4] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r5 %}
{% include support-prompt.html task="tarea5" %}
