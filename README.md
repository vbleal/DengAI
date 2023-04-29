# DengAI
[DengAI](https://www.drivendata.org/competitions/44/dengai-predicting-disease-spread/)  Competition by [DrivenData](https://www.drivendata.org/) 

![](https://raw.githubusercontent.com/vbleal/DengAI/main/Imag/DrivenDataLogo.png)





# Introducción

[DengAI](https://www.drivendata.org/competitions/44/dengai-predicting-disease-spread/) es una competición organizada por la Fundación [DrivenData](https://www.drivendata.org/)  para resolver un problema crítico causado por los mosquitos utilizando datos históricos que contienen detalles sobre las condiciones ambientales para predecir la propagación de la enfermedad del dengue. 


La fiebre del ***dengue*** es una enfermedad viral mortal transmitida por mosquitos que ocurre en partes tropicales y subtropicales del mundo. Dado que esta enfermedad viral es transportada por mosquitos, la propagación del dengue está relacionada con variables climáticas como temperatura, precipitación, humedad, etc. Por lo tanto, con la ***correlación*** entre estas condiciones ambientales y los datos históricos, es posible predecir los casos de dengue. 

El presente notebook contiene detalles sobre los métodos y técnicas que hemos utilizado para predecir la propagación de la enfermedad del dengue.


# Objetivo

En este trabajo, se pretende predecir el ***número total de casos de fiebre del dengue*** informados cada semana en 2 ubicaciones:

*   San Juan, Puerto Rico 

*   Iquitos, Perú

Para ello, se usarán los datos ambientales recopilados por varias agencias del gobierno federal de los EE. UU., desde los Centros para el Control y la Prevención de Enfermedades hasta la Administración Nacional Oceánica y Atmosférica en el Departamento de Comercio de los EE. UU.


La comprensión de la relación entre el clima y la dinámica del dengue puede mejorar las iniciativas de investigación y la asignación de recursos para ayudar a combatir pandemias que amenazan la vida.


El ***objetivo*** de este proyecto es investigar y construir un modelo adecuado con un bajo ***Error Absoluto Medio (Mean Absolute Error, MAE)*** para predecir el total de casos de dengue en el conjunto de prueba proporcionado por DrivenData en la competición [DengAI](https://www.drivendata.org/competitions/44/dengai-predicting-disease-spread/).



# Dataset

## Ficheros

Hay **3 ficheros** proporcionados por DrivenData-[DengAI](https://www.drivendata.org/competitions/44/dengai-predicting-disease-spread/).

**1. `dengue_features_train.csv`**

Contiene las características y los valores relevantes de atributos del conjunto de datos de entrenamiento. Consiste en ***24 características*** y valores de atributos para 1456 semanas en las ciudades de San Juan e Iquitos.


**2. `dengue_labels_train.csv`**

Contiene el número total de casos de dengue para cada fila en el conjunto de datos de entrenamiento.


**3. `dengue_features_test.csv`**

Contiene las características y los valores relevantes de atributos del conjunto de datos de prueba. Contiene las mismas ***24 características*** que el conjunto de características de entrenamiento. Hay 416 semanas para las ciudades de San Juan e Iquitos que necesitan predecir los total_cases.

Ambos conjuntos de datos de características de entrenamiento (***train***) y prueba (***test***) proporcionados consisten en datos climáticos y no climáticos en una escala de tiempo de año y semana del año. 


## Categorías 

**1. Indicadores de ciudad y fecha**

Estos datos describen las ciudades consideradas y la fecha de inicio de los datos.

*   `city` - Abreviaturas de la ciudad: 'iq' para Iquitos y 'sj' para San Juan

*   `week_start_date` - La fecha de inicio de la semana dada en formato yyyy-mm-dd


**2. Mediciones de estación meteorológica diaria de datos climáticos de NOAA GHCN**

La ***Global Historical Climatology Network (GHCN)***  es una base de datos integrada que consiste en informes climáticos diarios de estaciones de superficie terrestre de todo el mundo. Estos datos incluyen registros de más de 100,000 estaciones en 180 países y territorios en todo el mundo. Los datos proporcionados por GHCN están sujetos a una serie común de revisiones de aseguramiento de calidad. Los siguientes atributos están disponibles en el conjunto de datos de la categoría de datos.



*  `station_max_temp_c` - Temperatura máxima

*  `station_min_temp_c` - Temperatura mínima

*  `station_avg_temp_c` - Temperatura promedio

*  `station_precip_mm` - Precipitación total

*  `station_diur_temp_rng_c` - Rango de temperatura diurna


**3. Mediciones de precipitación por satélite PERSIANN (escala de 0.25x0.25 grados)**

La ***Precipitation Estimation from Remotely Sensed Information using Artificial Neural Networks- Climate Data Record (PERSIANN-CDR)***  es la estimación de lluvia en la resolución de escala dada (escala de 0.25x0.25 grados). El siguiente atributo corresponde a esta categoría.

*  `precipitation_amt_mm` - Precipitación total



**4. Mediciones de reanálisis del Sistema de Pronóstico Climático de NOAA NCEP (escala de 0.5x0.5 grados)**

Los datos de reanálisis proporcionados por los ***National Centers for Environmental Prediction (NCEP)***  representan cómo cambia el clima y el clima con el tiempo. Estos datos son útiles para comparar las condiciones climáticas presentes y pasadas. Los siguientes atributos de esta categoría se han incluido en los conjuntos de datos proporcionados por la competencia.

*  `reanalysis_sat_precip_amt_mm` - Precipitación total

*  `reanalysis_dew_point_temp_k` - Temperatura de punto de rocío media

*  `reanalysis_air_temp_k` - Temperatura del aire media

*  `reanalysis_relative_humidity_percent` - Humedad relativa media

*  `reanalysis_specific_humidity_g_per_kg` - Humedad específica media

*  `reanalysis_precip_amt_kg_per_m2` - Precipitación total

*  `reanalysis_max_air_temp_k` - Temperatura máxima del aire

*  `reanalysis_min_air_temp_k` - Temperatura mínima del aire


**5. Vegetación por satélite - Índice de Vegetación de Diferencia Normalizada (NDVI) - NOAA CDR Índice de Vegetación de Diferencia Normalizada (escala de 0.5x0.5 grados) mediciones**

Los datos proporcionados en esta categoría representan una medida de la vegetación en un área considerada. Estos valores son útiles para determinar la disponibilidad de vegetación y agua en un área a lo largo del tiempo. Las siguientes características del conjunto de datos se incluyen en esta categoría.

*  `ndvi_se` - Píxel al sureste del centroide de la ciudad

*  `ndvi_sw` - Píxel al suroeste del centroide de la ciudad

*  `ndvi_ne` - Píxel al noreste del centroide de la ciudad

*  `ndvi_nw` - Píxel al noroeste del centroide de la ciudad


## Resultados

![](https://raw.githubusercontent.com/vbleal/DengAI/main/Supervised/SL_Results.jpg)




# Modelos

## Unsupervised Learning

***Clustering***
    
*   [Google Colab]()

*   [GitHub](https://github.com/vbleal/DengAI/tree/main/Unsupervised)


## Supervised Learning

    
*   [Google Colab]()

*   [GitHub](https://github.com/vbleal/DengAI/tree/main/Supervised)




## Aprendizaje Supervisado

***Modelo***
    
*   [Google Colab]()
    
*   [GitHub](https://github.com/vbleal/DengAI/tree/main/Supervised)


