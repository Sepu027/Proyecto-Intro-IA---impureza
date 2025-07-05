# Proyecto-Intro-IA---Porcentaje de impureza en el proceso de producción de concentrado mediante flotación
-- como comentario: Utilizaré ciertas funciones que no se vieron en clases pero que he utilizado en proyectos anteriores (como TimeSeriesSplit, RandomizedSearchCV, Optuna, la mayoría son de scikit Learn, además de gráficos no vistos también) --
## Definición del Problema

En la industria minera, especialmente en la producción de concentrado mediante flotación, mantener bajos niveles de impurezas como la sílice es crucial, debido a que excesos generan importantes penalizaciones económicas. El problema es que los resultados del análisis de sílice suelen obtenerse con un desfase aproximado de 60 minutos desde la toma de muestras, lo que obliga a operar "a ciegas" durante ese tiempo. Esto dificulta la toma de decisiones oportunas para controlar las condiciones del proceso y evitar costos significativos. 

El objetivo de este proyecto es predecir con anticipación (entre 30 y 60 minutos) la concentración de sílice en el concentrado, utilizando variables operacionales, permitiendo ajustes inmediatos y mejorando significativamente la eficiencia económica del proceso.

## Plan de Acción

### Descripción del Dataset:
Se utilizará el dataset público "Quality Prediction in a Mining Process" disponible en Kaggle (https://www.kaggle.com/datasets/edumagalhaes/quality-prediction-in-a-mining-process/data), que contiene 739.294 registros con variables clave del proceso de flotación, incluyendo pH, ORP, caudales, niveles de celda y dosificación de reactivos, además del contenido de sílice analizado cada hora.

### Modelo Seleccionado:
Se implementará un modelo de Random Forest Regressor debido a su efectividad comprobada en problemas tabulares complejos y no lineales, capacidad de manejar variables correlacionadas y ruido, así como por su interpretabilidad en términos prácticos.

### Estrategia de Evaluación:

División temporal del dataset (TimeSeriesSplit y utilizando la estrategia en 'cascada') para evitar filtración de información futura.

Métricas: Error Porcentual Absoluto Medio (MAPE < 8%) y Root Mean Square Error (RMSE).

Optimización del modelo mediante RandomizedSearchCV u Optuna (ajuste de hiperparámetros como número de árboles, profundidad máxima y variables por árbol).

Validación interna mediante Out-of-Bag score (OOB) para verificar estabilidad.

Análisis de importancia de variables mediante SHAP para interpretabilidad operacional.

# Justificación del Uso del Modelo Random Forest

Random Forest es especialmente adecuado para este problema por las siguientes razones:

Capacidad para manejar relaciones complejas y no lineales: Las condiciones operativas en flotación presentan interacciones y sinergias entre variables como pH, ORP y dosificación de reactivos que otros métodos más simples no capturan adecuadamente.

Robustez ante variables ruidosas y correlacionadas: El modelo Random Forest no es sensible a la presencia de valores atípicos ni requiere la eliminación estricta de variables correlacionadas, algo común en datos operacionales reales.

Interpretabilidad práctica: La identificación de variables clave mediante técnicas como SHAP permite a los operadores entender fácilmente qué parámetros están afectando la predicción, facilitando la toma de decisiones.
