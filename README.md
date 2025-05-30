# Modelo de Pesquisa Automatizada del Riesgo Cardiovascular mediante Inteligencia Artificial en la Red APS de Quellón, provincia de Chiloé
**Claudio Cárdenas M.**

## Introducción

La comuna de Quellón, situada en la provincia de Chiloé, enfrenta desafíos significativos en salud pública debido a la alta prevalencia de factores de riesgo cardiovascular (FRCV) en su población. Estudios realizados en diversas regiones de Chile han evidenciado tasas elevadas de hipertensión arterial, dislipidemias, obesidad y diabetes mellitus tipo 2 . Aunque no se dispone de datos específicos para Quellón, es razonable inferir que estas condiciones también afectan a su población, considerando las similitudes sociodemográficas y epidemiológicas con otras zonas del país.

## Objetivo general del estudio:

Entrenar un modelo predictivo basado en algoritmos de machine learning para la identificación temprana de personas en riesgo cardiovascular, utilizando datos clínicos de la población usuaria de la Atención Primaria de Salud en la comuna de Quellón, con el propósito de optimizar la focalización de intervenciones preventivas y mejorar la gestión del riesgo en salud cardiovascular.


## Metodologia para el proceso de *Data Science*.

ara el desarrollo de este proyecto se ha empleado, y se empleará, la metodología CRISP-DM, la cual es de libre distribución y compatible con cualquier conjunto de herramientas de minería de datos. Dicha metodología estructura el ciclo de vida de un proyecto de minería de datos en seis fases interactivas e iterativas:

- Comprensión del negocio: definición de los objetivos, evaluación de la situación actual y elaboración del plan de trabajo.

- Comprensión de los datos: identificación y recopilación de las fuentes de datos disponibles.

- Preparación de los datos: limpieza, transformación e integración de los datos para su análisis.

- Modelado: aplicación de técnicas de análisis y generación de modelos que respondan a los objetivos del negocio, produciendo información nueva y relevante.

- Evaluación: análisis de los resultados obtenidos, valoración de la calidad y validación de los modelos desarrollados.

- Despliegue: planificación de la implementación y distribución de los resultados.

Las fases de evaluación y despliegue no se abordaran en el presente estudio, dado que excede el alcance del Magíster por las limitaciones de tiempo, recursos humanos y presupuesto. No obstante, se prevé su ejecución eventual en el caso de que sea necesario implementar en producción el modelo predictivo que demuestre mejor rendimiento en este trabajo.


### Recopilación de datos iniciales:

Base de Datos de la población en control, en la Comuna de Quellón, con corte a junio 2017, con un total de 2.865 registros y 41 campos y Base de datos EMP del año 2016 y a junio 2017, extraídos del sistema RAYEN (apartada por el Subdepartamento de Tecnología de la Información del Servicio de Salud Chiloé), con un total de 2.436 registros y 68 campos. Registros totales entre ambas bases de datos fueron 5.301.


### Descripción de datos.

Se llegó a la fase de modelado con una matriz depurada que contenía nueve campos predictores. Estos fueron: edad, circunferencia de cintura (CC_CM), presión arterial sistólica, colesterol, talla, presión arterial diastólica, peso, sexo, y tabaquismo. Se dispuso de 3.586 registros, 2.006 correspondientes al grupo que presenta al menos una de las tres patologías estudiadas (Grupo SI) y 1.580 a la categoría que eventualmente no presenta patología (Grupo NO).
La **Variable Objetivo** se definió con la denominación “PVC”, compuesta por dos grupos: GRUPO SI = Grupo de pacientes en control del Programa Cardiovascular, que presenta al menos una de las tres patologías, DM HTA o DLP. GRUPO NO = Grupo de Pacientes EMPA (2016 a junio 2017) y que no están en control en Programa Cardiovascular, al corte de junio del 2017 y, eventualmente, no presenta ninguna de las tres patologías señaladas. Luego, este grupo servirá para poder discriminar y encontrar aquellos patrones en los datos que caracterizan a las personas con algunas de las tres patologías del grupo “SI” y las diferencian de aquellos en el grupo “NO”.


## Modelado

### Selección de Algoritmos

Para seleccionar el modelo más adecuado entre **regresión logística binaria** y **XGBoost** en un problema de clasificación de riesgo cardiovascular, es esencial comparar aspectos de interpretabilidad, rendimiento predictivo, robustez de los datos, requerimientos computacionales y aplicabilidad en el contexto de salud pública. La regresión logística ofrece una implementación sencilla y coeficientes directamente interpretables como odds ratio, lo cual facilita la adopción de resultados por parte de clínicos y gestores sanitarios. Por su parte, XGBoost incorpora métodos de ensamblado de árboles con regularización, que suelen superar en exactitud a los modelos lineales y manejan automáticamente valores faltantes y atípicos, aunque a costa de mayor complejidad computacional.


### Generación de Diseño de Comprobación.

Un diseño de comprobación basado en un split estratificado permite estimar la generalización de los modelos en datos no vistos, evitando sesgos de sobreajuste. Al reservar un conjunto de prueba independiente y usar una semilla fija se garantiza la reproducibilidad y la imparcialidad en la comparación entre regresión logística y XGBoost. La proporción recomendada de 80 % para entrenamiento y 20 % para prueba equilibra la variabilidad de la estimación y la cantidad de datos disponibles para ajuste de hiperparámetros mediante validación cruzada interna. Este enfoque aísla claramente la fase de evaluación final, mejorando la transparencia y confiabilidad de la selección de modelo en contextos de salud pública.



## Discusión y Conclusiones.

La comparación de ambos modelos revela un rendimiento global similar, con ventajas diferenciales según el contexto de aplicación. La regresión logística mostró una precisión de clasificación del 79,5 % (IC 95 %: 76,1–82,8), sensibilidad del 78,9 % y especificidad del 80,1 % (umbral 0,50), alcanzando un AUC de 0,7952 . En contraste, XGBoost obtuvo una exactitud de 78,6 % (IC 95 %: 75,1–81,8), sensibilidad del 77,6 %, especificidad del 79,4 %, un índice Kappa de 0,57 y un AUC de validación de 0,8791 . Aunque la diferencia en AUC favorece a XGBoost, ambos modelos presentan un balance adecuado entre tasa de verdaderos positivos y negativos, lo que garantiza su aplicabilidad en la Red Asistencial.

Desde la perspectiva de gestión en la Red APS y niveles hospitalarios del SS Chiloé, la regresión logística aporta interpretabilidad directa: sus coeficientes, transformados en odds ratios, identifican claramente a la edad, presión arterial sistólica e índice cintura–talla como predictores clave . Esto facilita la comunicación con equipos clínicos y la integración en protocolos de tamizaje prehospitalario y evaluación de riesgo cardiovascular en atención primaria. Por su parte, XGBoost, con su capacidad de ensamble y regularización automática, despliega un mayor poder discriminativo —reflejado en un AUC superior— y una robustez natural frente a valores faltantes y atípicos, destacando variables como IMC, PAS, colesterol total, ICT y edad . Sin embargo, su complejidad computacional y la necesidad de técnicas de explicación.


## Referencias:

-   Atalah, E., et al. (2003). Prevalencia de factores de riesgo de enfermedad cardiovascular en trabajadores de empresas de servicios. Revista Médica de Chile, 131(2), 123-130. <https://dx.doi.org/10.4067/S0034-98872003000200001>

-   Pedrero, V., et al. (2021). Generalidades del Machine Learning y su aplicación en la gestión sanitaria en Servicios de Urgencia. Revista Médica de Chile, 149(2), 248-254. <https://www.researchgate.net/publication/352105918_2021_Generalidades_Machine_Learning_y_su_aplicacion_en_la_gestion_sanitaria_en_SU>

-   González, C., et al. (2016). Prevalencia de factores de riesgo cardiovascular en trabajadores de salud. Revista Chilena de Nutrición, 43(1), 10-16. <https://dx.doi.org/10.4067/S0717-75182016000100005>

-   Cárdenas, Claudio, González, Sergio, Nahuel, Rosa, Herrera, Pablo, Ferrada, Luis, & Celis, Diego. (2018). Diseño de un modelo predictivo de pesquisa cardiovascular utilizando Árboles de Decisión: propensión de pacientes a presentar diabetes tipo 2, hipertensión arterial o dislipidemia: Estudio piloto, comuna de Quellón, Chiloé. Revista chilena de cardiología, 37(2), 126-133. <https://dx.doi.org/10.4067/S0718-85602018000200126>


-  Hernández Rodríguez, José, & Duchi Jimbo, Paola Narcisa. (2015). Índice cintura/talla y su utilidad para detectar riesgo cardiovascular y metabólico. Revista Cubana de Endocrinología, 26(1), 66-76. <http://scielo.sld.cu/scielo.php?script=sci_arttext&pid=S1561-29532015000100006&lng=es&tlng=es>

-  Khan, S. S., Ning, H., Wilkins, J. T., Allen, N., Carnethon, M., Berry, J. D., Sweis, R. N., & Lloyd-Jones, D. M. (2018). Association of Body Mass Index With Lifetime Risk of Cardiovascular Disease and Compression of Morbidity. JAMA cardiology, 3(4), 280–287. <https://doi.org/10.1001/jamacardio.2018.0022>

- https://www.geeksforgeeks.org/advantages-and-disadvantages-of-logistic-regression/ 

- https://xgboosting.com/xgboost-advantages-and-disadvantages-pros-vs-cons/ 

- https://builtin.com/data-science/train-test-split 

- https://machinelearningmastery.com/train-test-split-for-evaluating-machine-learning-algorithms/  

- https://realpython.com/train-test-split-python-data/ 


