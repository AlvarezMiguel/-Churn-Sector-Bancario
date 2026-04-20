# Análisis Predictivo de Abandono de Clientes (Bank Churn)
Este proyecto desarrolla un sistema de clasificación para predecir la probabilidad de que un cliente cancele su cuenta bancaria. 
Utilizando técnicas de Machine Learning se busca identificar a los clientes en riesgo de abandono, lo cual permitiría a las instituciones financieras tomar medidas preventivas de retención.

## Desafíos Técnicos
**Desbalance de Clientes: La base original presentaba un 80% de permanencia vs. un 20% de abandono. Se solucionó utilizando SMOTE-NC para equilibrar las clases y evitar sesgos en el entrenamiento.

## Herramientas Utilizadas
* **Lenguaje:** R
* **Librerías principales:** `tidymodels`, `themis` (para SMOTENC), `psych`, `ggplot2` (visualización).

## Variables predictoras : 
Score Crediticio, Ciudad, Sexo, Edad, Antigüedad, Balance, Número de Productos, Tarjeta de Crédito, Actividad y Salario Estimado

## Hallazgos del Análisis Exploratorio (EDA)
Edad: Factor determinante; se observa una distribución distinta entre quienes se van y quienes se quedan.
No existen correlación lienal evidente entre las variables predictoras.
Las variables predictoras manifiestan una distrubución normal o uniforme(Antigüedad y Salario Estimado). 
 
 `img/pair_plot.png` 


## Modelado: Entrenamiento y optimización de hiperparámetros mediante validación cruzada para los siguientes algoritmos:
   - K-Nearest Neighbors (KNN)
   - Naive Bayes
   - Support Vector Machines (Lineal, Radial, Polinomial)
   - Random Forest
   - Redes Neuronales
   - Modelo de Ensamble

##  Resultados Destacados

Los modelos demostraron una **alta capacidad** para identificar a los clientes que no abandonan el banco, siendo el desafío principal la predicción precisa de la clase positiva (abandono).

* [cite_start]**Random Forest:** Alcanzó un Accuracy de **0.866** y un área bajo la curva (AUC) de **0.869**[cite: 1866]. [cite_start]Se identificó que la Edad, el Número de Productos y el Saldo (Balance) son las variables más determinantes[cite: 2166, 2174].
* [cite_start]**Redes Neuronales:** Logró un Accuracy de **0.818** y un AUC de **0.868**[cite: 1995].
* [cite_start]**Ensamble:** Combinando los modelos, se obtuvo un AUC de **0.868** con una excelente especificidad (96.1%), demostrando gran eficacia para distinguir las clases[cite: 2045, 2047, 2049].

*(Agrega aquí imágenes de `img/curva_roc_random_forest.png` y `img/importancia_variables.png` usando sintaxis Markdown: `![Curva ROC](ruta_a_la_imagen)`)*

## 🧪 Experimentos Adicionales
Para evaluar la robustez de los modelos, se replicó el análisis bajo dos escenarios:
1.  [cite_start]**Transformación PCA:** Modelado sobre el subespacio de dimensión reducida (7 componentes)[cite: 2068, 2069].
2.  **Muestreo Reducido:** Entrenamiento con una muestra aleatoria del 20% de los datos. [cite_start]Se comprobó que, aunque los modelos mantienen cierto poder predictivo, la calidad general (Accuracy, Sensibilidad, AUC) disminuye, subrayando la importancia de volúmenes de datos adecuados para la estabilidad predictiva[cite: 2132, 2367, 2368].

