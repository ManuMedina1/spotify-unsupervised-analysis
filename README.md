# 🎵 Spotify Audio Clustering: Unsupervised Learning Analysis

![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python)
![Scikit-Learn](https://img.shields.io/badge/Library-Scikit--Learn-orange?logo=scikit-learn)
![Status](https://img.shields.io/badge/Status-Completed-success)

> **Análisis de patrones musicales y agrupación automática de géneros utilizando algoritmos de Clustering Jerárquico, K-Means y DBSCAN.**

---

## 📖 Descripción del Proyecto
Este proyecto aplica técnicas de **Aprendizaje No Supervisado** sobre un dataset de **Spotify** (aprox. 5,000 canciones) para identificar estructuras latentes y géneros musicales sin utilizar etiquetas predefinidas.

El objetivo es responder a la pregunta: *¿Podemos agrupar canciones automáticamente basándonos únicamente en sus características acústicas (energía, bailabilidad, tempo, etc.)?*

### 🎯 Objetivos
* **Preprocesar datos de audio** reales, tratando outliers y distribuciones no gaussianas.
* **Implementar y comparar** tres familias de algoritmos: Jerárquicos, Particionales y de Densidad.
* **Interpretar semánticamente** los clústeres resultantes para mapearlos a géneros musicales reales (Pop, Rock, EDM, etc.).

---

## 🛠️ Tecnologías y Herramientas
* **Lenguaje:** Python
* **Análisis de Datos:** Pandas, NumPy
* **Machine Learning:** Scikit-Learn (KMeans, AgglomerativeClustering, DBSCAN)
* **Visualización:** Matplotlib, Seaborn

---

## 📊 Metodología y Flujo de Trabajo

### 1. Preprocesamiento de Datos (`ETL`)
Antes de aplicar los modelos, realizamos un análisis exploratorio exhaustivo:
* **Limpieza:** Eliminación de nulos y columnas irrelevantes (IDs).
* **Transformación:**
    * *Logaritmo* a `duration_ms` (corregir skewness de 21.8).
    * *Raíz Cúbica* a `loudness`.
* **Escalado:** `MinMaxScaler` para normalizar todas las características al rango [0, 1].

### 2. Modelado y Comparativa

| Enfoque | Algoritmo Seleccionado | Configuración Óptima | Hallazgos Clave |
| :--- | :--- | :--- | :--- |
| **Jerárquico** | Agglomerative Clustering | **Euclídea + Ward (K=8)** | Mejor balance estructural. Identificó subgéneros por "Mood" (Alegre vs Triste). |
| **Particional** | K-Means | **K=8** | **Modelo Ganador.** Mejor equilibrio entre métricas matemáticas y utilidad de negocio. |
| **Densidad** | DBSCAN | **Eps=0.22, MinPts=8** | Encontró 7 clústeres "puros" y detectó mucho ruido. Útil para nichos, difícil para generalizar. |

---

## 📈 Resultados Destacados

### 🏆 El Modelo Ganador: K-Means (K=8)
Tras evaluar métricas como el **Coeficiente de Silueta**, **Calinski-Harabasz** y la interpretación de negocio, seleccionamos K-Means con 8 clústeres.

**Identificación de Géneros:**
El algoritmo logró separar con éxito los siguientes estilos musicales basándose solo en matemáticas:

1.  🎹 **Classical:** Alta instrumentalidad, baja energía.
2.  🎤 **Hip-Hop/Rap:** Alto `speechiness`.
3.  💃 **Pop Comercial:** Alta bailabilidad y energía, modo Mayor.
4.  🎸 **Rock / Indie:** Sonido de banda, energía media-alta.
5.  🎻 **Acoustic / Folk:** Acústico extremo, melódico.
6.  ⚡ **EDM / Electronic:** Máxima energía, sintético.
7.  ☁️ **Ambient:** Instrumental y tranquilo.
8.  🌚 **Urban / Dark Pop:** Similar al pop pero en tonalidad Menor.

*(Puedes ver los heatmaps detallados en el notebook `2_particional.ipynb`)*

![Heatmap de Clústeres](ruta/a/tu/imagen_heatmap.png)

---

## 📂 Estructura del Repositorio

```bash
├── data/                   # Dataset original y procesado
├── notebooks/
│   ├── 1_jerarquico.ipynb  # Clustering Aglomerativo y Dendrogramas
│   ├── 2_particional.ipynb # K-Means, Método del Codo y Siluetas
│   └── 3_densidad.ipynb    # DBSCAN y análisis de ruido
├── reports/
│   └── memoria_final.pdf   # Documentación detallada del proyecto
└── README.md
