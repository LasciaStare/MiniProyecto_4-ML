# Proyecto Bayesiano: Predicción de Enfermedades Cardíacas

## Descripción

Este proyecto utiliza un modelo de Naive Bayes Gaussiano para predecir la presencia de enfermedades cardíacas a partir de un conjunto de datos clínicos. El objetivo principal es construir un clasificador robusto y analizar su rendimiento en comparación con otros modelos como Regresión Logística y Naive Bayes de Bernoulli.

El flujo de trabajo abarca desde la carga y limpieza de datos, pasando por un análisis exploratorio (EDA) para entender las variables, hasta el preprocesamiento, modelado y la interpretación de los resultados.

## Características del Dataset

El proyecto utiliza el [dataset de Heart Disease de la UCI](https://archive.ics.uci.edu/dataset/45/heart+disease), que contiene 14 atributos, entre ellos:

*   **age**: Edad del paciente.
*   **sex**: Sexo del paciente.
*   **cp**: Tipo de dolor torácico.
*   **trestbps**: Presión arterial en reposo.
*   **chol**: Colesterol sérico.
*   **thalach**: Frecuencia cardíaca máxima alcanzada.
*   **exang**: Angina inducida por el ejercicio.
*   **oldpeak**: Depresión del segmento ST inducida por el ejercicio.
*   **ca**: Número de vasos principales visibles por fluoroscopia.
*   **target (num)**: Diagnóstico de enfermedad cardíaca (variable objetivo).

## Flujo del Proyecto

### 1. Carga e Identificación de Datos

Se cargó el dataset y se realizó una inspección inicial para identificar tipos de datos y valores faltantes. Se encontraron valores nulos en las columnas `ca` y `thal`, que fueron imputados utilizando la moda debido a su bajo porcentaje (menos del 1.5%).

### 2. Análisis Exploratorio de Datos (EDA)

Inicialmente, la variable objetivo tenía 5 niveles de gravedad. Para simplificar el problema a una clasificación binaria, se agruparon todos los niveles de enfermedad (1, 2, 3, 4) en una sola categoría (1), mientras que los pacientes sanos se mantuvieron como (0).

El análisis reveló que:
*   Las personas diagnosticadas con cardiopatía tienden a tener una edad más avanzada.
*   La depresión del segmento ST (`oldpeak`) es notablemente mayor en pacientes enfermos.
*   El tipo de dolor torácico (`cp`) y la presencia de angina inducida por ejercicio (`exang`) son fuertes indicadores de la enfermedad.

### 3. Preprocesamiento

Se seleccionaron las variables categóricas y numéricas más relevantes. Se aplicó `OneHotEncoder` a las variables categóricas y `StandardScaler` a las numéricas para prepararlas para el modelado.

### 4. Modelado y Evaluación

Se implementó un pipeline que integra el preprocesamiento y el modelo **Gaussian Naive Bayes**. El modelo alcanzó una **precisión (accuracy) del 88.5%** en el conjunto de prueba y un **AUC de 0.97**. Un punto destacable es su alto **recall (96%)** para la clase "enfermo", lo que indica una excelente capacidad para minimizar falsos negativos.

### 5. Comparación de Modelos

El rendimiento del modelo Gaussiano se comparó con:
*   **Regresión Logística**: Obtuvo una precisión del 91.8% y un AUC de 0.97.
*   **Bernoulli Naive Bayes**: Logró una precisión del 90.1% y un AUC de 0.98.

Todos los modelos mostraron un rendimiento excelente, destacando el Bernoulli Naive Bayes por su alto valor de AUC.

## Análisis de Relevancia de Variables

*   **Gaussian Naive Bayes**: Priorizó métricas de rendimiento dinámico como `thalach` (frecuencia cardíaca máxima) y `oldpeak` (depresión ST), sugiriendo que la capacidad funcional del corazón es un indicador clave.
*   **Regresión Logística**: Se centró en hallazgos diagnósticos categóricos, asignando la mayor importancia a `ca` (vasos obstruidos), `thal` (resultado de la prueba de esfuerzo con talio) y `cp` (tipo de dolor torácico).

## Conclusiones

El modelo Bayesiano demostró ser una herramienta de diagnóstico robusta y simple, especialmente valiosa por su alta sensibilidad para detectar pacientes enfermos. Aunque el supuesto de independencia entre variables es una limitación teórica, en la práctica el modelo ofrece un gran valor como sistema de alerta temprana en un entorno clínico.

Ambos enfoques de modelado (Naive Bayes y Regresión Logística) convergen al identificar los mismos factores de riesgo clave, aunque desde perspectivas diferentes (fisiológica vs. diagnóstica).

## Tecnologías Utilizadas

*   **Python**
*   **Pandas**
*   **NumPy**
*   **Scikit-learn**
*   **Matplotlib**
*   **Seaborn**

## Autores

*   José Menco
*   Camilo Vargas
*   Iván Ramirez
