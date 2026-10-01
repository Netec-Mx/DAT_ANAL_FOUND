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
prev: /lab8/lab8/
next: /lab10/lab10/
---

---

> **Importante:** Esta practica esta actualizada pero la velocidad de cambios en Microsoft Power BI puede ser alta, considera que puede haber algunos textos diferentes, en cualquier momento puedes consultar al instructor.
{: .lab-note .important .compact}

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

  1. [Descargar medidas DAX](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap5/05_medidas_dashboard.dax)
  2. [Descargar SQL de validación](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap5/05_validacion_dashboard.sql)
  3. [Descargar plantilla de validación](https://d3gfd4cq9u8k8p.cloudfront.net/courses/DAT_ANAL_FOUND/cap5/Plantilla_Practica5_Validacion.xlsx)

  Guarda como:

  ```text
  C:\DAF\Practica_05\05_medidas_dashboard.dax
  C:\DAF\Practica_05\05_validacion_dashboard.sql
  C:\DAF\Practica_05\Plantilla_Practica5_Validacion.xlsx
  ```

  > **Salida esperada:** Los tres recursos están disponibles localmente.
  {: .lab-note .output .compact}

### Tarea 1.2. Crear el PBIX y conectar Snowflake

- {% include step_label.html %} Abre Power BI Desktop y selecciona **Informe en blanco > Archivo > Guardar como**.

  Guarda:

  ```text
  C:\DAF\Practica_05\05_dashboard_ventas.pbix
  ```

  > **Salida esperada:** El archivo PBIX queda creado antes de cargar datos.
  {: .lab-note .output .compact}

- {% include step_label.html %} En **Inicio**, selecciona **Obtener datos > Base de datos > Snowflake** y selecciona **Conectar**.

  Ingresa:

  - La URL de conexión entragada al curso o la de uso personal/laboral.
  - El Almacen puede ser **COMPUTE_WH** o el que estes usando para la ejecución de consultas.

  ```text
  Servidor: <SNOWFLAKE_SERVER>
  Almacén: <WAREHOUSE_ASIGNADO>
  ```

  > **Salida esperada:** Ventana de usuario y contraseña
  {: .lab-note .output .compact}

- {% include step_label.html %} Coloca el usuario y contraseña asignados al curso o de tu propia cuenta y da clic en **Conectar**

  > **Salida esperada:** Power BI muestra el Navegador de Snowflake.
  {: .lab-note .output .compact}

- {% include step_label.html %} En el Navegador lateral selecciona:

  ```text
  DATA_ANALYTICS_FOUNDATIONS
  > CURATED
  > VENTAS_TRANSACCIONES_CURADAS_2026_1
  ```

  - Selecciona **Transformar datos**.
  - Clic en **Aceptar**.

  > **Salida esperada:** Power Query Editor muestra la fuente curada.
  {: .lab-note .output .compact}

### Tarea 1.3. Preparar `Ventas Curadas`

- {% include step_label.html %} en el panel lateral derecho renombra la consulta como:

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

### Tarea 2.1. Abrir el archivo DAX y crear la tabla `Calendario`

- {% include step_label.html %} Abre **Visual Studio Code**.

- {% include step_label.html %} En VS Code selecciona:

  ```text
  File > Open File...
  ```

  Abre:

  ```text
  C:\DAF\Practica_05\05_medidas_dashboard.dax
  ```

  > **Importante:** Un archivo `.dax` es un archivo de texto con expresiones DAX. No se ejecuta desde VS Code. Solo lo usarás para copiar cada bloque y pegarlo en Power BI.
  {: .lab-note .important .compact}

- {% include step_label.html %} Dentro del archivo localiza el bloque que inicia con:

  ```DAX
  Calendario =
  ```

  y termina en el último paréntesis `)` de esa expresión.

  Debe verse similar a:

  ```DAX
  Calendario =
  ADDCOLUMNS(
      CALENDAR(DATE(2024, 1, 1), DATE(2025, 12, 31)),
      "Year", YEAR([Date]),
      "MonthNumber", MONTH([Date]),
      "Month", FORMAT([Date], "MMMM"),
      "YearMonth", FORMAT([Date], "YYYY-MM"),
      "YearMonthOrder", YEAR([Date]) * 100 + MONTH([Date])
  )
  ```

- {% include step_label.html %} Selecciona **todo el bloque `Calendario = ...`** y cópialo con `Ctrl+C`.

  > **Salida esperada:** La expresión completa de `Calendario` queda copiada al portapapeles.
  {: .lab-note .output .compact}

- {% include step_label.html %} Regresa a **Power BI Desktop**.

- {% include step_label.html %} En el panel **Datos** verifica que ya exista la tabla:

  ```text
  Ventas Curadas
  ```

  > **Importante:** No crees `Calendario` dentro de Power Query. La tabla se creará en el modelo mediante DAX.
  {: .lab-note .important .compact}

- {% include step_label.html %} En la cinta de opciones selecciona **Nueva tabla / New table**.

  Dependiendo de la versión de Power BI Desktop, la opción puede mostrarse en:

  ```text
  Inicio > Nueva tabla
  ```

  o como:

  ```text
  Modelado > Nueva tabla
  ```

- {% include step_label.html %} Se mostrará una barra de fórmulas en la parte superior del lienzo.

  Si aparece una expresión temporal, selecciónala y elimínala.

- {% include step_label.html %} Pega con `Ctrl+V` la expresión `Calendario` copiada desde VS Code.

- {% include step_label.html %} Presiona **Enter** o selecciona el icono de confirmación **✓**.

  > **Salida esperada:** En el panel **Datos** aparece una nueva tabla llamada `Calendario`.
  {: .lab-note .output .compact}

- {% include step_label.html %} Expande la tabla `Calendario` y confirma que contiene estas columnas:

  ```text
  Date
  Year
  MonthNumber
  Month
  YearMonth
  YearMonthOrder
  ```

  > **Salida esperada:** La tabla `Calendario` contiene una fila por cada fecha desde 2024-01-01 hasta 2025-12-31.
  {: .lab-note .output .compact}

### Tarea 2.2. Configurar tipos y orden de las columnas de calendario

- {% include step_label.html %} En el panel **Datos**, selecciona `Calendario[Date]`.

- {% include step_label.html %} En **Herramientas de columna / Column tools**, confirma:

  ```text
  Tipo de datos: Fecha
  ```

  Si aparece como Fecha/Hora, cambia el tipo a **Fecha**.

  > **Salida esperada:** `Calendario[Date]` y `Ventas Curadas[TRANSACTIONDATE]` usan tipo Fecha.
  {: .lab-note .output .compact}

- {% include step_label.html %} Cambia a la **Vista de informe** usando el icono de gráfico del menú izquierdo.

  > **Nota:** Power BI muestra **Ordenar por columna / Sort by column** en `Column tools` cuando seleccionas una columna desde la Vista de informe.
  {: .lab-note .important .compact}

- {% include step_label.html %} En el panel **Datos**, selecciona:

  ```text
  Calendario[Month]
  ```

- {% include step_label.html %} En **Herramientas de columna / Column tools**, selecciona:

  ```text
  Ordenar por columna > MonthNumber
  ```

  > **Salida esperada:** Los nombres de mes dejan de ordenarse alfabéticamente y usan enero, febrero, marzo, etc.
  {: .lab-note .output .compact}

- {% include step_label.html %} Selecciona ahora:

  ```text
  Calendario[YearMonth]
  ```

- {% include step_label.html %} En **Ordenar por columna / Sort by column**, selecciona:

  ```text
  YearMonthOrder
  ```

  > **Salida esperada:** `YearMonth` se ordena cronológicamente de `2024-01` a `2025-12`.
  {: .lab-note .output .compact}

### Tarea 2.3. Crear la relación entre `Calendario` y `Ventas Curadas`

- {% include step_label.html %} En el menú izquierdo selecciona **Vista de modelo / Model view**.

- {% include step_label.html %} Localiza las tablas:

  ```text
  Calendario
  Ventas Curadas
  ```

- {% include step_label.html %} Arrastra:

  ```text
  Calendario[Date]
  ```

  sobre:

  ```text
  Ventas Curadas[TRANSACTIONDATE]
  ```

- {% include step_label.html %} Si Power BI abre la ventana **Crear relación / Create relationship**, configura:

  ```text
  Tabla: Calendario
  Columna: Date

  Tabla relacionada: Ventas Curadas
  Columna relacionada: TRANSACTIONDATE

  Cardinalidad: Uno a varios (1:*)
  Dirección de filtro cruzado: Única
  Activar esta relación: Sí
  ```

- {% include step_label.html %} Selecciona **Guardar**.

- {% include step_label.html %} Revisa en la Vista de modelo que la línea muestre:

  ```text
  Calendario[Date]  1  ─────  *  Ventas Curadas[TRANSACTIONDATE]
  ```

  > **Importante:** Si Power BI muestra `*:*`, relación inactiva o una dirección distinta, no continúes hasta corregirla.
  {: .lab-note .important .compact}

  > **Salida esperada:** Existe una relación activa `1:*` desde `Calendario` hacia `Ventas Curadas`.
  {: .lab-note .output .compact}

### Tarea 2.4. Marcar `Calendario` como tabla de fechas

- {% include step_label.html %} En el panel **Datos**, selecciona la tabla completa `Calendario`.

- {% include step_label.html %} Usa una de estas rutas:

  ```text
  Herramientas de tabla > Marcar como tabla de fechas > Marcar como tabla de fechas
  ```

  o haz clic derecho sobre `Calendario` y selecciona:

  ```text
  Marcar como tabla de fechas > Marcar como tabla de fechas
  ```
  
  - **Activar**

- {% include step_label.html %} Cuando Power BI solicite la columna de fecha, selecciona:

  ```text
  Date
  ```

- {% include step_label.html %} Confirma con **Guardar**.

  > **Salida esperada:** `Calendario` queda identificada como tabla de fechas y `Date` es su columna de fecha.
  {: .lab-note .output .compact}

### Tarea 2.5. Crear las medidas DAX una por una

- {% include step_label.html %} Regresa a VS Code y mantén abierto:

  ```text
  C:\DAF\Practica_05\05_medidas_dashboard.dax
  ```

- {% include step_label.html %} En Power BI cambia a **Vista de informe**.

- {% include step_label.html %} En el panel **Datos**, haz clic una vez sobre la tabla:

  ```text
  Ventas Curadas
  ```

  Esto hace que las nuevas medidas queden almacenadas en esa tabla.

- {% include step_label.html %} Crea primero `Ventas Netas`.

  En VS Code localiza y copia únicamente:

  ```DAX
  Ventas Netas =
  SUM('Ventas Curadas'[NETSALES])
  ```

- {% include step_label.html %} En Power BI usa una de estas opciones:

  ```text
  Clic derecho en Ventas Curadas > Nueva medida
  ```

  o:

  ```text
  Inicio > Nueva medida
  ```

- {% include step_label.html %} En la barra de fórmulas pega el bloque `Ventas Netas = ...` y presiona **Enter**.

  > **Salida esperada:** Debajo de `Ventas Curadas` aparece la medida `Ventas Netas` con icono de calculadora.
  {: .lab-note .output .compact}

- {% include step_label.html %} Repite el mismo procedimiento para `Margen Bruto`.

  Copia desde VS Code:

  ```DAX
  Margen Bruto =
  SUM('Ventas Curadas'[GROSSMARGIN])
  ```

  Luego crea **Nueva medida**, pega la expresión y presiona **Enter**.

- {% include step_label.html %} Crea `Margen %`.

  Copia:

  ```DAX
  Margen % =
  DIVIDE(
      [Margen Bruto],
      [Ventas Netas],
      0
  )
  ```

  > **Importante:** `Margen %` depende de las dos medidas anteriores. Si `Ventas Netas` o `Margen Bruto` no existen, Power BI marcará error.
  {: .lab-note .important .compact}

- {% include step_label.html %} Crea `Transacciones`.

  ```DAX
  Transacciones =
  DISTINCTCOUNT('Ventas Curadas'[TRANSACTIONID])
  ```

- {% include step_label.html %} Crea `Clientes Únicos`.

  ```DAX
  Clientes Únicos =
  DISTINCTCOUNT('Ventas Curadas'[CUSTOMERID])
  ```

- {% include step_label.html %} Crea `Ticket Promedio`.

  ```DAX
  Ticket Promedio =
  DIVIDE(
      [Ventas Netas],
      [Transacciones],
      0
  )
  ```

- {% include step_label.html %} Si tu archivo `05_medidas_dashboard.dax` incluye `Unidades`, créala también como medida auxiliar:

  ```DAX
  Unidades =
  SUM('Ventas Curadas'[QUANTITY])
  ```

- {% include step_label.html %} Si el archivo incluye `Cobertura Seleccionada`, créala de la misma manera con **Nueva medida**.

  > **Salida esperada:** En `Ventas Curadas` aparecen al menos estas seis medidas con icono de calculadora:
  {: .lab-note .output .compact}

  ```text
  Ventas Netas
  Margen Bruto
  Margen %
  Transacciones
  Clientes Únicos
  Ticket Promedio
  ```

### Tarea 2.6. Formatear las medidas

- {% include step_label.html %} Selecciona la medida `Ventas Netas` en el panel **Datos**.

- {% include step_label.html %} En **Herramientas de medida / Measure tools**, configura:

  ```text
  Formato: Moneda
  Posiciones decimales: 2
  ```

- {% include step_label.html %} Repite el formato **Moneda** para:

  ```text
  Margen Bruto
  Ticket Promedio
  ```

- {% include step_label.html %} Selecciona `Margen %` y configura:

  ```text
  Formato: Porcentaje
  Posiciones decimales: 2
  ```

- {% include step_label.html %} Selecciona `Transacciones` y `Clientes Únicos` y configura:

  ```text
  Formato: Número entero
  Separador de miles: Activado
  ```

- {% include step_label.html %} Si creaste `Unidades`, configúrala como **Número entero**.

  > **Importante:** El dataset contiene varias `Currency`. El formato de moneda en Power BI solo mejora la presentación; no convierte MXN, COP, CLP y PEN a una moneda común.
  {: .lab-note .important .compact}

  > **Salida esperada:** Las medidas aparecen con formatos consistentes y están listas para usarse en visualizaciones.
  {: .lab-note .output .compact}

{% capture r2 %}{{ results[1] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r2 %}
{% include support-prompt.html task="tarea2" %}

---

## 📊 Tarea 3. Construir el dashboard — 12 min

Crearás una sola página orientada a desempeño, tendencia y segmentación.

### Tarea 3.1. Preparar la página del informe

- {% include step_label.html %} Cambia a la **Vista de informe / Report view** usando el icono de gráfico del menú izquierdo.

- {% include step_label.html %} En la parte inferior, haz doble clic sobre la pestaña de la página actual, normalmente llamada `Página 1` o `Page 1`.

- {% include step_label.html %} Renombra la página como:

  ```text
  Desempeño de ventas
  ```

- {% include step_label.html %} Haz clic en un espacio vacío del lienzo para no tener ningún visual seleccionado.

- {% include step_label.html %} En el panel **Formato / Format** de la página, localiza **Configuración del lienzo / Canvas settings**.

- {% include step_label.html %} En **Tipo / Type**, selecciona:

  ```text
  16:9
  ```

  > **Salida esperada:** La página se llama `Desempeño de ventas` y usa formato 16:9.
  {: .lab-note .output .compact}

### Tarea 3.2. Crear el slicer de fecha

- {% include step_label.html %} En el panel **Visualizaciones**, selecciona el visual **Segmentación de datos / slicer**.

- {% include step_label.html %} Con el slicer seleccionado, arrastra desde el panel **Datos**:

  ```text
  Calendario[Date]
  ```

  al campo del visual.

- {% include step_label.html %} Si Power BI muestra `Jerarquía de fechas`, abre el menú del campo dentro del visual y selecciona la columna simple:

  ```text
  Date
  ```

  > **Importante:** Para este slicer usa `Calendario[Date]`, no `Ventas Curadas[TRANSACTIONDATE]`.
  {: .lab-note .important .compact}

- {% include step_label.html %} En el slicer abre el selector de tipo y cambia a:

  ```text
  Entre / Between
  ```

  > **Salida esperada:** El participante puede elegir una fecha inicial y una fecha final.
  {: .lab-note .output .compact}

### Tarea 3.3. Crear los slicers de región y canal

- {% include step_label.html %} Inserta un segundo **slicer**.

- {% include step_label.html %} Arrastra:

  ```text
  Ventas Curadas[REGION]
  ```

  al campo del slicer.

- {% include step_label.html %} Inserta un tercer **slicer** y agrega:

  ```text
  Ventas Curadas[CHANNEL]
  ```

- {% include step_label.html %} Coloca los tres slicers en la parte superior o lateral de la página.

  > **Salida esperada:** Existen slicers independientes para fecha, región y canal.
  {: .lab-note .output .compact}

### Tarea 3.4. Crear la tarjeta `Ventas Netas`

- {% include step_label.html %} En **Visualizaciones**, selecciona **Tarjeta / Card**.

- {% include step_label.html %} Desde `Ventas Curadas`, arrastra la medida:

  ```text
  [Ventas Netas]
  ```

  al campo de datos de la tarjeta.

- {% include step_label.html %} En **Formato del visual > General > Título**, activa el título y escribe:

  ```text
  Ventas Netas
  ```

  > **Salida esperada:** La tarjeta muestra el valor de `[Ventas Netas]` para los filtros activos.
  {: .lab-note .output .compact}

### Tarea 3.5. Crear las otras tres tarjetas KPI

- {% include step_label.html %} Copia la tarjeta anterior tres veces con `Ctrl+C` y `Ctrl+V`, o inserta tres nuevas tarjetas.

- {% include step_label.html %} En la segunda tarjeta reemplaza `[Ventas Netas]` por:

  ```text
  [Margen Bruto]
  ```

- {% include step_label.html %} En la tercera tarjeta usa:

  ```text
  [Margen %]
  ```

- {% include step_label.html %} En la cuarta tarjeta usa:

  ```text
  [Ticket Promedio]
  ```

- {% include step_label.html %} Verifica que cada tarjeta tenga un título coherente con la medida mostrada.

  > **Salida esperada:** Son visibles las cuatro tarjetas `Ventas Netas`, `Margen Bruto`, `Margen %` y `Ticket Promedio`.
  {: .lab-note .output .compact}

### Tarea 3.6. Crear la tendencia mensual de ventas netas

- {% include step_label.html %} Inserta un **Gráfico de líneas / Line chart**.

- {% include step_label.html %} Arrastra:

  ```text
  Calendario[YearMonth]
  ```

  al **Eje X / X-axis**.

- {% include step_label.html %} Arrastra la medida:

  ```text
  [Ventas Netas]
  ```

  al **Eje Y / Y-axis**.

- {% include step_label.html %} Confirma que el eje muestre:

  ```text
  2024-01, 2024-02, ... 2025-12
  ```

  Si aparece desordenado, regresa a la Tarea 2.2 y verifica que `YearMonth` esté ordenado por `YearMonthOrder`.

- {% include step_label.html %} En **Formato > General > Título**, escribe:

  ```text
  Evolución mensual de ventas netas
  ```

  > **Salida esperada:** La línea muestra la evolución mensual en orden cronológico.
  {: .lab-note .output .compact}

### Tarea 3.7. Crear ventas netas por región

- {% include step_label.html %} Inserta un **Gráfico de barras agrupadas / Clustered bar chart**.

- {% include step_label.html %} Arrastra:

  ```text
  Ventas Curadas[REGION]
  ```

  al **Eje Y / Y-axis** o campo de categoría del visual.

- {% include step_label.html %} Arrastra:

  ```text
  [Ventas Netas]
  ```

  al **Eje X / X-axis** o campo de valor.

- {% include step_label.html %} En el encabezado del visual selecciona **... > Ordenar por > Ventas Netas > Descendente**.

- {% include step_label.html %} Configura el título:

  ```text
  Ventas netas por región
  ```

  > **Salida esperada:** Las regiones aparecen ordenadas de mayor a menor por `[Ventas Netas]`.
  {: .lab-note .output .compact}

### Tarea 3.8. Crear ventas netas por canal

- {% include step_label.html %} Inserta un segundo **Gráfico de barras agrupadas**.

- {% include step_label.html %} Configura:

  ```text
  Categoría / Eje: Ventas Curadas[CHANNEL]
  Valor: [Ventas Netas]
  ```

- {% include step_label.html %} Ordena por `[Ventas Netas]` de mayor a menor.

- {% include step_label.html %} Configura el título:

  ```text
  Ventas netas por canal
  ```

  > **Salida esperada:** Los canales pueden compararse por ventas netas.
  {: .lab-note .output .compact}

### Tarea 3.9. Verificar que los slicers interactúan con los visuales

- {% include step_label.html %} En el slicer `REGION`, selecciona una región.

- {% include step_label.html %} Confirma que cambien:

  ```text
  Ventas Netas
  Margen Bruto
  Margen %
  Ticket Promedio
  Evolución mensual
  Barras por región
  Barras por canal
  ```

- {% include step_label.html %} Limpia la selección usando el icono **Borrar selecciones / Clear selections** del slicer.

- {% include step_label.html %} Selecciona ahora un `CHANNEL` y repite la validación.

- {% include step_label.html %} Cambia el rango del slicer `Date` y confirma nuevamente que los KPI y gráficos respondan.

  > **Importante:** Si un visual no cambia, selecciónalo y revisa **Formato > Editar interacciones / Edit interactions** para confirmar que el slicer lo esté filtrando.
  {: .lab-note .important .compact}

  > **Salida esperada:** Todos los visuales responden de manera coherente a fecha, región y canal.
  {: .lab-note .output .compact}

{% capture r3 %}{{ results[2] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r3 %}
{% include support-prompt.html task="tarea3" %}

---

## ✅ Tarea 4. Validar y guardar — 7 min

Compararás los KPI principales contra Snowflake antes de considerar terminado el dashboard.

### Tarea 4.1. Dejar Power BI sin filtros activos

- {% include step_label.html %} En el slicer `REGION`, selecciona **Borrar selecciones / Clear selections**.

- {% include step_label.html %} Repite la acción en `CHANNEL`.

- {% include step_label.html %} En el slicer de fecha establece el rango completo:

  ```text
  2024-01-01 a 2025-12-31
  ```

- {% include step_label.html %} Confirma que las tarjetas muestran nuevamente los valores globales.

  > **Salida esperada:** El dashboard está en el mismo alcance global que la consulta de validación de Snowflake.
  {: .lab-note .output .compact}

### Tarea 4.2. Registrar los KPI de Power BI

- {% include step_label.html %} Abre en Microsoft Excel:

  ```text
  C:\DAF\Practica_05\Plantilla_Practica5_Validacion.xlsx
  ```

- {% include step_label.html %} En Power BI registra en la columna correspondiente los valores de:

  ```text
  Ventas Netas
  Margen Bruto
  Margen %
  Transacciones
  Clientes Únicos
  Ticket Promedio
  ```

- {% include step_label.html %} Para `Transacciones` y `Clientes Únicos`, si no están visibles en tarjetas, crea temporalmente una tarjeta para cada medida, registra el valor y después elimina esas tarjetas si no deseas conservarlas.

  > **Salida esperada:** La plantilla contiene los seis KPI calculados por Power BI.
  {: .lab-note .output .compact}

### Tarea 4.3. Ejecutar la validación en Snowflake

- {% include step_label.html %} Abre **Snowsight** y entra a un **SQL Worksheet**.

- {% include step_label.html %} Abre localmente en VS Code:

  ```text
  C:\DAF\Practica_05\05_validacion_dashboard.sql
  ```

  > **Nota:** Al igual que el archivo `.dax`, el `.sql` es texto. Puedes abrirlo en VS Code, copiar la consulta y ejecutarla en el Worksheet de Snowflake.
  {: .lab-note .important .compact}

- {% include step_label.html %} Localiza la consulta de validación global.

- {% include step_label.html %} Copia la consulta completa y pégala en el Worksheet de Snowflake.

- {% include step_label.html %} Ejecuta la consulta.

- {% include step_label.html %} Copia los resultados de Snowflake en la columna `Snowflake` de:

  ```text
  Plantilla_Practica5_Validacion.xlsx
  ```

  > **Salida esperada:** La plantilla contiene los KPI equivalentes de Power BI y Snowflake.
  {: .lab-note .output .compact}

### Tarea 4.4. Comparar resultados

- {% include step_label.html %} Para los conteos verifica:

  ```text
  Transacciones: diferencia = 0
  Clientes Únicos: diferencia = 0
  ```

- {% include step_label.html %} Para importes verifica una tolerancia máxima de redondeo de:

  ```text
  0.01
  ```

- {% include step_label.html %} Para `Margen %`, compara con el mismo número de decimales utilizado en la plantilla.

- {% include step_label.html %} Marca cada control como:

  ```text
  Conforme
  ```

  o:

  ```text
  Investigar
  ```

- {% include step_label.html %} Si alguna métrica no coincide, revisa en este orden:

  ```text
  1. QUALITYFLAG = VALID en Power Query
  2. rango de fecha activo
  3. filtros REGION y CHANNEL
  4. relación Calendario[Date] -> Ventas Curadas[TRANSACTIONDATE]
  5. definición de la medida DAX
  6. tipo de datos de TRANSACTIONDATE
  7. mismo filtro de Currency cuando aplique
  ```

  > **Importante:** No continúes corrigiendo cifras manualmente en Excel. La discrepancia debe resolverse en filtros, modelo, DAX o consulta SQL.
  {: .lab-note .important .compact}

  > **Salida esperada:** Los KPI principales quedan conformes o existe una causa documentada para cualquier diferencia.
  {: .lab-note .output .compact}

### Tarea 4.5. Guardar el PBIX y la evidencia

- {% include step_label.html %} Regresa a Power BI y selecciona:

  ```text
  Archivo > Guardar
  ```

  Confirma que el archivo sea:

  ```text
  C:\DAF\Practica_05\05_dashboard_ventas.pbix
  ```

- {% include step_label.html %} Regresa a Excel y selecciona:

  ```text
  Archivo > Guardar como
  ```

  Guarda una copia como:

  ```text
  C:\DAF\Practica_05\05_validacion_dashboard.xlsx
  ```

- {% include step_label.html %} Confirma en el Explorador de archivos que existan:

  ```text
  C:\DAF\Practica_05\05_dashboard_ventas.pbix
  C:\DAF\Practica_05\05_validacion_dashboard.xlsx
  C:\DAF\Practica_05\05_medidas_dashboard.dax
  C:\DAF\Practica_05\05_validacion_dashboard.sql
  ```

  > **Salida esperada:** El PBIX, la validación y los archivos auxiliares están disponibles para reutilizarse en el Reto 5.
  {: .lab-note .output .compact}

{% capture r4 %}{{ results[3] }}{% endcapture %}
{% include task-result.html title="Tarea finalizada" content=r4 %}
{% include support-prompt.html task="tarea4" %}
