# EDA
# EDA — Notas de Estudiantes (Matemáticas y Portugués)

**Curso:** (completar)  
**Autores:** (completar)  
**Fecha:** (completar)

Este trabajo presenta un **análisis exploratorio de datos (EDA)** con **variable respuesta numérica**. Tomamos como guía el ejemplo de Walmart (ventas semanales) y lo adaptamos al contexto académico: aquí la respuesta es la **nota final `G3` (0–20)**. Los datos provienen de dos archivos: `student-mat.csv` (Matemáticas) y `student-por.csv` (Portugués).

---

## 3.4 Análisis exploratorio con variable respuesta numérica

Para el desarrollo de las visualizaciones y resúmenes seguimos el mismo flujo del ejemplo (ETL → variable objetivo → variables independientes → bivariado). En lugar de `weekly_sales`, nuestra variable objetivo es **`G3`** y usaremos características demográficas, hábitos de estudio, contexto familiar y antecedentes académicos como explicativas.

---

## 3.4.1 Contexto de los datos (estudiantes)

**Archivos de origen**
- `student-mat.csv` → estudiantes de **Matemáticas**
- `student-por.csv` → estudiantes de **Portugués**

Tras unificar ambas bases y estandarizar nombres, trabajamos con **1.044** observaciones y **34** variables. Algunas variables relevantes:

- **Demográficas:** `sex` (F/M), `age`, `address` (U/R), `famsize` (LE3/GT3).  
- **Familia y tutoría:** `Pstatus` (T/A), `Medu`, `Fedu`, `Mjob`, `Fjob`, `guardian`.  
- **Escolares:** `studytime` (1–4), `failures`, `absences`, `traveltime` (1–4).  
- **Apoyos y recursos:** `schoolsup`, `famsup`, `paid`, `activities`, `higher`, `internet`, `romantic`.  
- **Escalas (1–5):** `famrel`, `freetime`, `goout`, `Dalc`, `Walc`, `health`.  
- **Notas:** `G1`, `G2`, **`G3`** (0–20).

**Objetivo**  
Comprender patrones y relaciones alrededor de **`G3`** y dejar artefactos listos para modelado posterior.

---

## 3.4.2 Extracción, transformación y carga (ETL)

- Se cargaron ambos CSV desde `data/`, se limpiaron nombres y se unificaron en un solo conjunto, agregando la etiqueta `subject` (Math/Portuguese).
- Se eliminaron algunas columnas no utilizadas en el análisis inicial (p. ej., `school`, `address`).

**Calidad de datos**
- **Conteo de NAs por variable:** `tables/na_table.csv`  
- **Mapa de valores perdidos:** `images/missmap.png`  

**Lectura:** No se observaron valores faltantes en las variables clave, por lo que el conjunto es **apto para análisis**.

---

## 3.4.3 Análisis de la variable objetivo: `G3`

**Resumen (`n = 1.044`)**  
- **Media:** **11.34** (DS = **3.86**)  
- **Mediana:** **11.00**  
- **Mínimo–Máximo:** **0.00** – **20.00**  
- **Q1–Q3:** **10.00** – **14.00** (IQR = **4.00**)

**Interpretación (en el estilo del ejemplo)**  
La variable `G3` fue analizada a partir de **1.044** observaciones. Se obtuvo un **promedio** de **11.34** puntos (DS = **3.86**), donde el **50%** de las notas se encuentra **por debajo de 11.00**. El **mínimo** observado fue **0.00**, lo que indica casos de pérdida total, y el **máximo** alcanzó **20.00**, es decir, calificación perfecta. El rango intercuartílico (IQR = **4.00**) refleja una **dispersión moderada** entre el primer y tercer cuartil. La distribución muestra **asimetría hacia la izquierda** (concentración en valores medios y cola hacia los bajos), consistente con la presencia de **outliers** en **0** y **20**.

**Artefactos**  
- Resumen numérico: `tables/resumen_g3.csv`  
- Histograma + densidad: `images/hist_g3.png`  
- Boxplot: `images/boxplot_g3.png`

---

## 3.4.4 Análisis de las variables características (independientes)

### 3.4.4.1 Variables numéricas

Se analizaron **`age`**, **`absences`** y **`studytime`**:

- **Edad (`age`)**  
  n = 1.044; **media = 16.73**, DS = **1.24**; mediana = **17.00**; min–max = **15.00–22.00**; Q1–Q3 = **16.00–18.00** (IQR = **2.00**).  
  Conjunto **homogéneo** en edad escolar: la mayoría se concentra entre 16 y 18 años.

- **Ausencias (`absences`)**  
  n = 1.044; **media = 4.43**, DS = **6.21**; mediana = **2.00**; min–max = **0.00–75.00**; Q1–Q3 = **0.00–6.00** (IQR = **6.00**).  
  Predominan **pocas ausencias**, pero existen **casos extremos** (p99 ≈ **25.57**), lo que genera **alta asimetría**.

- **Tiempo de estudio (`studytime`, 1–4)**  
  n = 1.044; **media = 1.97**, DS = **0.83**; mediana = **2.00**; min–max = **1.00–4.00**; Q1–Q3 = **1.00–2.00** (IQR = **1.00**).  
  Distribución **concentrada** en niveles bajos/medios: 1 (**317**), 2 (**503**), 3 (**162**), 4 (**62**).

**Artefactos**  
- Resumen numérico: `tables/resumen_variables_numericas.csv`  
- Boxplots combinados: `images/boxplots_variables_numericas.png`

---

### 3.4.4.2 Variables categóricas

A modo de ejemplo, se presentan **`sex`**, **`schoolsup`** y **`activities`**.

- **Sexo (`sex`)**  
  F = **56.61%** (n=591); M = **43.39%** (n=453).  
- **Apoyo escolar (`schoolsup`)**  
  **no = 88.60%** (n=925); **yes = 11.40%** (n=119).  
- **Actividades (`activities`)**  
  **no = 50.57%** (n=528); **yes = 49.43%** (n=516).

**Artefactos**  
- Tabla de frecuencias: `tables/frecuencias_categoricas.csv`  
- Gráfico de ejemplo (`sex`): `images/frecuencia_sex.png`

**Lectura (al estilo del ejemplo)**  
`schoolsup` muestra **baja cobertura** del apoyo, lo que sugiere focalización en casos específicos. `activities` está **casi equilibrada**, permitiendo comparaciones razonables entre grupos. `sex` es **ligeramente desbalanceada** a favor de F.

---

## 3.4.5 Análisis exploratorio bivariado

### 3.4.5.1 Comparación de `G3` con variables numéricas

- **Dispersión `G3` vs `age`**  
  Los puntos se distribuyen entre 15 y 22 años sin una tendencia pronunciada. La correlación es **débil y negativa** (**r = -0.125**): la **edad explica poco** la variación en `G3`.

- **Dispersión `G3` vs `absences`**  
  Se observa **alta dispersión** (ausencias de 0 a 75) y una tendencia **ligeramente negativa** (**r = -0.046**): a mayor número de ausencias, **menor `G3`** en promedio, aunque el efecto es **pequeño**.

- **Dispersión `G3` vs `studytime`**  
  Se aprecia una **relación débil y positiva** (**r = 0.162**): más tiempo de estudio suele asociarse con **mejor `G3`**, con **solapamientos** entre niveles.

> Nota: Los **scatterplots con recta LM** se visualizan en ejecución; no se guardan por defecto en disco.

### 3.4.5.2 Comparación de `G3` con variables categóricas

Se calcularon estadísticas por nivel (n, media, DS, mediana, min, max, Q1, Q3, IQR):

- **`sex`**  
  F: **media = 11.45**, mediana = **12.00**, IQR = **4.00** (n=591)  
  M: **media = 11.20**, mediana = **11.00**, IQR = **4.00** (n=453)  
  → **Medianas muy similares**; no se evidencia una brecha marcada por género.

- **`schoolsup`**  
  no: **media = 11.45**, mediana = **12.00**, IQR = **4.00** (n=925)  
  yes: **media = 10.49**, mediana = **11.00**, IQR = **3.00** (n=119)  
  → El grupo “yes” muestra **media menor**, coherente con **asignación del apoyo a estudiantes con mayor rezago** (no implica efecto causal del apoyo).

- **`activities`**  
  no: **media = 11.21**, mediana = **11.00**, IQR = **4.00** (n=528)  
  yes: **media = 11.47**, mediana = **12.00**, IQR = **4.00** (n=516)  
  → Participar en actividades se asocia con **ligera mejora** promedio, con **solapamientos** importantes.

**Artefacto**  
- Tabla consolidada: `tables/analisis_bivariado.csv`  

> Nota: Los **boxplots** de esta sección se muestran en pantalla; no se guardan por defecto.

### 3.4.5.3 Vistazo multivariado (GGally)

Una inspección con `ggpairs()` confirma patrones:  
- **`G2` vs `G3`** presenta una **correlación fuerte y positiva** (**r = 0.911**), como era esperable (continuidad evaluativa).  
- Señales **débiles** con `age`, `absences` y `studytime`, en las direcciones descritas arriba.

---

## Conclusiones

1. **`G3`** muestra **heterogeneidad** con concentración en valores medios (Mediana = **11.00**) y presencia de **outliers** (0 y 20).  
2. **`G2`** es el **mejor predictor inmediato** de `G3` (**r = 0.911**).  
3. Entre las numéricas simples, **`studytime`** se asocia **positivamente** y **`absences`** **negativamente** con `G3` (ambas con efectos **débiles**).  
4. **`schoolsup`** (apoyo) exhibe **media inferior**, coherente con un **efecto de selección** (no causal). **`sex`** no muestra brechas relevantes; **`activities`** se asocia a **mejoras modestas**.  
5. El dataset está **limpio (sin NAs)** y documentado con tablas y figuras para su posterior uso en modelado.

---

## Archivos generados

**Tablas**  
- `tables/na_table.csv`  
- `tables/resumen_g3.csv`  
- `tables/resumen_variables_numericas.csv`  
- `tables/frecuencias_categoricas.csv`  
- `tables/analisis_bivariado.csv`

**Imágenes**  
- `images/missmap.png`  
- `images/hist_g3.png`  
- `images/boxplot_g3.png`  
- `images/boxplots_variables_numericas.png`  
- `images/frecuencia_sex.png`
