# Análisis Predictivo de Abandono de Clientes (Bank Churn)
Este proyecto desarrolla un sistema de clasificación para predecir la probabilidad de abandono de clientes en el sector bancario. El objetivo además de pronosticar la fuga es hallar los factores subyacentes que impulsan la decisión de abandono. Esto permite al banco diseñar estrategias de retención más efectivas.

## Desafíos Técnicos
El problema presenta un marcado desbalance de clases, donde los clientes que abandonan representan una minoría. Este sesgo puede afectar la capacidad del modelo para detectar correctamente los casos de abandono.Para mitigar este efecto, se aplicó la técnica SMOTE (Synthetic Minority Oversampling Technique), siguiendo las recomendaciones de la literatura (Rahman & Kumar, 2020), que permite mejorar la sensibilidad del modelo.

## Herramientas Utilizadas
* **Lenguaje:** R
* **Modelado y Preprocesamiento:** Framework `tidymodels`, `themis` (para el balanceo de clases mediante SMOTENC)[cite: 63].
* **Explicabilidad (Explainable AI - XAI):** `DALEX` (análisis de importancia, dependencia parcial y explicaciones locales).
* **Visualización:** `ggplot2`

## Hallazgos del Análisis Exploratorio (EDA)
Durante la exploración inicial, se identificaron los siguientes patrones clave:
* **Desbalance de clases:** Aproximadamente el 80% de los clientes permanecen en el banco frente a un 20% que lo abandonan.
* **Factores de riesgo iniciales:** Variables como la Edad presentan una diferencia notable en las distribuciones de los clientes que abandonan frente a los que se quedan. Asimismo, a mayor número de productos, el número de casos de abandono parece aumentar.
  
![Distribucion de las variables num](img/pairplot.png)

![Distribucion de las variables cat](img/evento_en_cat.png)

## Entrenamiento y optimización de hiperparámetros mediante validación cruzada para los siguientes algoritmos:
Se realizó el entrenamiento y la optimización de hiperparámetros mediante validación cruzada. Tomando como caso de evaluación el algoritmo K-Nearest Neighbors (KNN) (optimizado en el número de vecinos y funciones de peso):
- Fase de Entrenamiento: El modelo reportó un ROC AUC de 0.826, lo cual indica una capacidad sólida para distinguir entre los dos eventos de interés.
- Fase de Prueba: El modelo logró un ROC AUC de 0.811, lo que demuestra una capacidad predictiva consistente ante datos no vistos.

| Métrica       | Valor | Interpretación |
| ------------- | ------|----------------|
| Precisión     | 0.74 | El modelo clasifica correctamente al 74% del total de clientes.|
| Sensibilidad  | 0.71 | Logra detectar correctamente al 71% de los clientes que sí abandonaron (foco principal del negocio).|
| Especificidad | 0.75 | Detecta correctamente al 75% de los clientes que decidieron quedarse|
| ROC AUC       | 0.81 | Muestra una buena capacidad de discriminación general.|

![Curva de ROC y Matrz de confusión](img/curva_y_mat.png)
  

## Análisis de variables de mayor impacto. 
### Importancia de las variables (Nivel Global)
Una de las ventajas competitivas de este proyecto es que permite analizar el impacto global de cada variable y examinar a clientes específicos para comprender a detalle por qué toman la decisión de irse o quedarse.

Las variables críticas identificadas para la decisión de abandono, son las siguientes :

![Importancia de variables](img/importancia_var.png)

- La Edad es el factor determinante principal, seguido por el Número de productos contratados.
- La baja Actividad y el Balance (saldo) también contribuyen de manera significativa.
- Un hallazgo demográfico importante fue la identificación de Alemania como un factor geográfico de riesgo de abandono frente a otros países.
  
### Perfiles de Dependencia Parcial (PDP)
A continuación, se presentan las gráficas de dependencia parcial. Estas permiten visualizar cómo cambia la probabilidad de abandono al variar específicamente las características críticas identificadas, aislando el efecto del resto de las variables. Este análisis detalla la compleja relación no lineal entre el perfil del cliente y su riesgo de fuga.

![pdp_importantes](img/cinco_variables_pdp.png)  
  

## Análisis de casos específicos (Nivel Local)
Este procedimiento responde a una pregunta de negocio fundamental: ¿Por qué un cliente en particular decidió abandonar o no el banco?

Los resultados se lograron mediante el método SHAP (SHapley Additive exPlanations). Esta técnica analítica permite estimar la contribución matemática exacta de cada característica a una predicción individual, descomponiendo una decisión compleja del modelo en aportes individuales y comprensibles. 

![SHap](img/cleintes_20_y_3.png)  


