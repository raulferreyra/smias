<!-- This is the markdown template for the final project of the Building AI course, 
created by Reaktor Innovations and University of Helsinki. 
Copy the template, paste it to your GitHub README and edit! -->

# smias
Super Metropolitano IA System

Final project for the Building AI course

## Summary

This project will develop an artificial intelligence predictive system to optimize the distribution of Metropolitano units in Lima, Peru, using cross-data on passenger flow on different routes and key stops. 


## Background

The Lima Metropolitano faces significant challenges due to the lack of units at strategic points, which causes an inefficient service. This problem is common and affects thousands of users daily. My personal motivation arises from the need to improve public transportation in my city, providing a solution that optimizes the distribution of buses based on the actual flow of passengers. This issue is crucial to improve the quality of life of citizens and make an essential transportation system more efficient. In this way and with the collection of new data, routes could be improved by adding stops that are created possible and/or completely changing a route that benefits users.


## How is it used?

The predictive system is designed to be used by operators of the Lima Metropolitano. The solution is implemented in real time, allowing operators to monitor and adjust the distribution of transport units based on passenger demand on different routes and stations. Operators can quickly identify the need for additional units at critical points, prioritize emergencies such as broken buses, and optimize routes to improve overall service efficiency. In addition, a review and modification of station entrances and exits is required to obtain accurate data on the flow of pedestrian passengers, which is essential to identify and address the real needs of users.

### El Metropolitano
![Metropolitano](https://scontent.flim2-1.fna.fbcdn.net/v/t31.18172-8/27021867_1059219784219736_4647830421122505517_o.jpg?_nc_cat=108&ccb=1-7&_nc_sid=13d280&_nc_ohc=cX_llKdVoZYQ7kNvgH6OSOB&_nc_ht=scontent.flim2-1.fna&oh=00_AYC48s4VsTN48NVEmq9jEOBF5yqtKYahI-7jy5f81At_hA&oe=66E613A4)

This is only Example:
```
import numpy as np
import pandas as pd

# Definir estaciones y rutas
estaciones = [f'Estación {i}' for i in range(1, 11)]
rutas = ['Ruta 1', 'Ruta 2', 'Ruta 3']

# Generar datos de usuarios
np.random.seed(42)
datos_usuarios = []

for i in range(100):  # Generar datos para 100 usuarios
    estacion_origen = np.random.choice(estaciones[:-3])  # No pueden subir en las últimas 3 estaciones
    estacion_destino = np.random.choice(estaciones[estaciones.index(estacion_origen)+3:])  # Destino a mínimo 3 estaciones de distancia
    ruta = np.random.choice(rutas)
    datos_usuarios.append([estacion_origen, estacion_destino, ruta])

# Crear DataFrame
df_usuarios = pd.DataFrame(datos_usuarios, columns=['Origen', 'Destino', 'Ruta'])

# Mostrar datos generados de usuarios
print("Datos generados de usuarios:\n", df_usuarios.head(), "\n")

# Contar la demanda por ruta
demanda_ruta = df_usuarios['Ruta'].value_counts()

# Distribución inicial (15 vehículos distribuidos uniformemente)
vehiculos_por_ruta = {'Ruta 1': 5, 'Ruta 2': 5, 'Ruta 3': 5}

# Ajustar la distribución de vehículos según la demanda
total_vehiculos = 15
nueva_distribucion = (demanda_ruta / demanda_ruta.sum() * total_vehiculos).round().astype(int)

# Asegurar que la suma total de vehículos sea igual a 15
diferencia = total_vehiculos - nueva_distribucion.sum()
if diferencia != 0:
    # Ajustar la ruta con mayor demanda o menor número de vehículos
    index = nueva_distribucion.idxmax() if diferencia > 0 else nueva_distribucion.idxmin()
    nueva_distribucion[index] += diferencia

# Imprimir resultados
print("Demanda por ruta:\n", demanda_ruta)
print("\nDistribución inicial de vehículos por ruta:\n", vehiculos_por_ruta)
print("\nNueva distribución de vehículos basada en la demanda:\n", nueva_distribucion.to_dict())
```


## Data sources and AI methods
Where does your data come from? Do you collect it yourself or do you use data collected by someone else?
If you need to use links, here's an example:
[Twitter API](https://developer.twitter.com/en/docs)

| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |

## Challenges

What does your project _not_ solve? Which limitations and ethical considerations should be taken into account when deploying a solution like this?

## What next?

How could your project grow and become something even more? What kind of skills, what kind of assistance would you  need to move on? 


## Acknowledgments

* list here the sources of inspiration 
* do not use code, images, data etc. from others without permission
* when you have permission to use other people's materials, always mention the original creator and the open source / Creative Commons licence they've used
  <br>For example: [Sleeping Cat on Her Back by Umberto Salvagnin](https://commons.wikimedia.org/wiki/File:Sleeping_cat_on_her_back.jpg#filelinks) / [CC BY 2.0](https://creativecommons.org/licenses/by/2.0)
* etc
