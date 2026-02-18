# Tarea de Aprendizaje No Supervisado Semana 3

Este notebook realiza una segmentación de países basada en sus métricas de conectividad digital y penetración de internet utilizando técnicas de Aprendizaje No Supervisado.

## 🛠️ Herramientas

**Lenguaje:** Python 3.14

## 📊 Dataset

El dataset utilizado es el archivo `data.csv` que contiene las métricas de conectividad digital y penetración de internet para diferentes países.

**Fuente:** [Internet Users Dataset](https://www.kaggle.com/datasets/ashishraut64/internet-users)

## 📚 Librerías Utilizadas

- `pandas` (v3.0.0) - Manipulación y análisis de datos
- `numpy` (v2.4.2) - Cálculos numéricos avanzados
- `matplotlib` (v3.10.8) - Visualización de datos estática
- `seaborn` (v0.13.2) - Visualización estadística de datos
- `scikit-learn` (v1.8.0) - Implementación de modelos (K-Means, DBSCAN, PCA, StandardScaler)

## 🚀 Instalación y Uso

1. Clonar el repositorio
2. Crear un entorno virtual:
   ```
   python -m venv .venv
   ```
3. Activar el entorno e instalar dependencias:
   ```
   .\.venv\Scripts\activate
   pip install pandas numpy matplotlib seaborn scikit-learn
   ```
4. Ejecutar el notebook `no_supervisado.ipynb` seleccionando el kernel del entorno virtual

## 🧠 Justificación del Enfoque

Se busca entender la brecha digital a través de la historia en los diferentes países. Se utilizaron las siguientes técnicas:
- **Estandarización (StandardScaler):** Crucial para que variables con diferentes escalas tengan el mismo peso en el clustering.
- **K-Means:** Elegido por su eficiencia en la identificación de perfiles de desarrollo (Bajo, Medio, Alto).
- **DBSCAN:** Utilizado para detectar anomalías o entidades con comportamientos atípicos de conectividad.
- **PCA:** Utilizado para la visualización global, validando que los grupos identificados en 5 dimensiones tengan una separación física clara en 2D.
- **t-SNE:** Herramienta para visualizar estructuras locales y complejas, permitiendo verificar la cohesión interna de los clusters.

## 📊 Análisis de Resultados

### Perfiles Identificados
1. **Alta Conectividad:** Países con alta penetración de banda ancha e internet.
2. **Conectividad en crecimiento:** Países con alto uso de celulares pero internet en crecimiento.
3. **Baja Conectividad:** Regiones con infraestructura digital mínima.

### Diferencias entre Modelos
- **K-Means:** Generó una segmentación estructurada por niveles de progreso.
- **DBSCAN:** Mostró que existen datos "ruido" que no pertenecen a la norma global, posiblemente países con crecimientos desproporcionados en métricas específicas.
- **PCA:** Permitió visualizar la separación global de los grupos, facilitando la interpretación técnica de los componentes principales.
- **t-SNE:** Reveló que los grupos son más densos de lo que PCA sugiere, lo que indica que el clustering es robusto.

## ⚠️ Limitaciones y Mejoras
- **Sesgo Temporal:** Los datos históricos mezclados pueden confundir el estado actual. Se recomienda filtrar por años recientes (2020+).
- **Sesgo de Población:** Las métricas absolutas favorecen a países grandes. Se sugiere normalizar todas las variables a tasas "per cápita" o porcentajes.

# Respuestas a las preguntas planteadas

### 1. ¿Qué tipo de perfiles se pueden identificar?
A través del modelo **K-Means**, se identificaron tres perfiles claros de desarrollo tecnológico:
- **Cluster de Alta Conectividad**: Entidades con los niveles más altos en todas las variables, destacando en penetración de internet y suscripciones de banda ancha fija.
- **Cluster en Desarrollo/Transición**: Países con una adopción sólida de telefonía móvil pero con una infraestructura de internet y banda ancha aún en crecimiento.
- **Cluster de Baja Conectividad**: Regiones con acceso limitado o nulo, caracterizados por valores cercanos a cero en todas las métricas.

### 2. ¿Qué diferencias clave surgieron entre los modelos?
- **K-Means**: Fue el más efectivo para segmentar la población en niveles socio-tecnológicos definidos, creando grupos basados en la distancia a los centroides.
- **DBSCAN**: Se centró en la densidad de los datos. Su principal diferencia fue la capacidad de identificar **ruido**, aunque es más difícil de configurar para datasets con densidades muy variadas.
- **PCA**: PCA mostró una separación lineal clara que facilitó la interpretación global
- **t-SNE**: t-SNE reveló estructuras locales más complejas y la cohesión interna de los clusters.

### 3. ¿Qué limitaciones encontraron y cómo las abordarían?
- **Limitación de Serie Temporal**: El dataset mezcla datos de 1980 con datos de 2020. Un país puede estar en el "Cluster de Baja Conectividad" en 1990 y en "Líderes" en 2020, lo que complica el perfilamiento estático. 
  - *Solución*: Filtrar el análisis para el año 2020 exclusivamente para entender la brecha digital actual.
- **Escala de Población**: La cantidad ed usuarios de internet beneficia a países muy poblados.
  - *Solución*: Utilizar únicamente variables relativas porcentajes o tasas por cada 100 habitantes para que el tamaño de la población no distorsione el perfil tecnológico.