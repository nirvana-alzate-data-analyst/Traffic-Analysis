# 🚦 Análisis de Movilidad Urbana y Productividad Económica en Latinoamérica (2024)

Evaluación de la relación entre la congestión vehicular y los indicadores económicos en las principales ciudades de América Latina, desarrollada como estudio de caso para orientar decisiones de inversión en infraestructura de transporte (contexto: *Latin American Development Bank - LADB*).

---

## 🎯 Objetivo del Proyecto
Analizar cómo impacta la movilidad urbana en la productividad económica de 15 ciudades pertenecientes a 7 países de Latinoamérica durante el año **2024**, cruzando métricas de tráfico en tiempo real con variables macroeconómicas y demográficas para identificar prioridades de inversión vial y de transporte público.

---

## 📂 Estructura del Repositorio

* `S5 ladb_mobility_economy_project_student.ipynb`: Notebook principal con todo el flujo de trabajo (carga, limpieza, transformación, agregación, visualización y análisis).
* `ladb_mobility_economy_2024_clean.csv`: Dataset final consolidado y limpio resultante del cruce de fuentes para el año 2024.
* `README.md`: Documentación general del proyecto, metodología y hallazgos.

*(Nota: Los datasets crudos de origen utilizados en el análisis son `/datasets/tomtom_traffic.csv` y `/datasets/oecd_city_economy.csv`).*

---

## 🛠️ Tecnologías y Librerías Utilizadas
* **Lenguaje:** Python 3.9
* **Manipulación y Análisis de Datos:** `pandas`, `numpy`
* **Visualización de Datos:** `matplotlib`, `seaborn`

---

## 🔄 Metodología y Flujo de Trabajo

1. **Exploración Inicial:** Inspección de estructura y tipos de datos en dos fuentes: *TomTom Traffic Index* (>1 millón de registros diarios/horarios) y *OECD Cities* (30 registros macroeconómicos).
2. **Limpieza y Estandarización:**
   * Renombramiento de todas las columnas al estándar `snake_case`.
   * Conversión de marcas de tiempo (`update_time_utc` y `update_time_utc_week_ago`) a formato `datetime64`.
   * Limpieza de caracteres especiales (`.`, `,`, `%`) y transformación a tipo numérico (`float`) de variables económicas (`city_gdp_per_capita`, `unemployment_pct`, `population_million`), además del cálculo de la población absoluta (`population`).
3. **Filtrado Temporal y Agregación:**
   * Extracción del año a partir de las fechas de tráfico y filtrado exclusivo para **2024**.
   * Agrupación por `city`, `country` y `year` calculando los promedios anuales de los principales indicadores de congestión (`jams_delay`, `traffic_index_live`, `jams_length_in_kms`, `jams_count`, `mins_delay` y tiempos de viaje por cada 10 km).
4. **Integración de Datos (Merge):** Unión de tipo `inner` entre los indicadores de movilidad y economía utilizando `city` y `year` como llaves primarias, consolidando una tabla única de 15 ciudades latinoamericanas.
5. **Análisis Exploratorio Visual (EDA):**
   * *Boxplot* para identificar la dispersión, mediana, promedio y valores atípicos (*outliers*) de los minutos de congestión (`jams_delay`).
   * *Histograma* para evaluar la distribución del PIB per cápita (`city_gdp_per_capita`).
   * *Gráfico de barras comparativo* para contrastar el nivel de congestión frente al ingreso per cápita por ciudad.

---

## 📊 Principales Hallazgos

* **Relación inversa general:** En la mayoría de las ciudades analizadas se observa una tendencia inversa entre el PIB per cápita y los niveles de congestión vehicular. Ciudades con mayor PIB per cápita como **Montevideo** y **Brasilia** presentan menores tiempos de retraso por tráfico.
* **Alta congestión con menor PIB:** Ciudades como **Bogotá**, **Lima** y **Santiago** registran altos niveles de congestión acompañados de un PIB per cápita relativamente bajo en comparación con el resto de la muestra.
* **Caso atípico (Outlier):** **Ciudad de México** encabeza el ranking global y regional de retrasos por tráfico (`jams_delay` promedio de ~2,833), pero mantiene al mismo tiempo un PIB per cápita elevado, rompiendo la tendencia general del grupo.

---

## 💡 Recomendaciones Estratégicas

1. **Priorización de Inversión (Santiago):** Se recomienda priorizar a **Santiago** para proyectos de inversión en infraestructura vial, desarrollo de vías alternas y expansión de sistemas de transporte masivo sostenible con el fin de reducir los tiempos de traslado y desbloquear productividad económica.
2. **Análisis Multivariable (Ciudad de México):** Debido a su comportamiento atípico, se sugiere incorporar nuevas variables en una segunda fase de estudio —como extensión geográfica, densidad poblacional y tasa de motorización— para aislar los factores estructurales detrás de sus altos niveles de congestión.

---

## 🚀 Cómo ejecutar este proyecto

1. Clona este repositorio en tu máquina local:
   ```bash
   git clone [https://github.com/nirvana-alzate-data-analyst/Traffic-Analysis.git](https://github.com/nirvana-alzate-data-analyst/Traffic-Analysis.git)
