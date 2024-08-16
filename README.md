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
In order to propose a system that allows predicting weekly the need for buses in the Lima Metropolitan area according to the routes, it is essential to develop a predictive model based on artificial intelligence (AI). Below, I detail the key aspects of this proposal.

### General Approach
Objective: Develop a system that, using historical user data, predicts the demand for buses on different routes to optimize vehicle distribution and improve service efficiency.

### Type of AI
Soft AI: In this case, we will use soft AI techniques, since the objective is to create models that can learn from data and make predictions without needing to replicate human cognition. Soft AI focuses on automating complex processes and improving data-driven decision making, without trying to simulate full human reasoning.

### Predictive Model
For this project, an Artificial Neural Network (ANN) model will be used due to its ability to handle large volumes of data and capture complex patterns in them. In particular, a dense neural network with several hidden layers could be used to perform the weekly bus demand prediction on each route.

### Tools and Technologies
TensorFlow: This is one of the most popular libraries for building and training neural networks. It offers flexibility and efficiency to handle large amounts of data and can be easily scaled for this type of project.
Training Method
Supervised Training:

* Training Data: We will use historical user flow data, such as the origin and destination points of trips, peak demand times, days of the week, special events, etc. This data is labeled to train the model to predict future demand.
* Loss Function: A mean squared error (MSE) method could be used as the loss function, since it is common in regression problems and penalizes large deviations in predictions.
* Optimization: We will use optimization algorithms such as Adam or SGD (Stochastic Gradient Descent) to adjust the weights of the neural network and minimize the loss function.

### Neural Networks
* Architecture:
Input Layers: Input data such as user characteristics (origin, destination, time, day of the week).
Hidden Layers: Several dense layers (fully connected) with ReLU activations to capture non-linearities in the data.
Output Layer: A neuron representing the bus demand prediction for a specific route.
Validation and Testing
Cross-Validation: We will use cross-validation techniques to evaluate the model's performance and avoid overfitting. The data will be split into training, validation, and test sets to ensure that the model generalizes well to unseen data.

* Implementation and Deployment
Real-Time Predictions: Once trained, the model can be deployed in a production environment where it receives real-time data and makes weekly predictions about bus demand. These predictions can be presented to the Metro operators through an interactive dashboard.

* Maintenance and Continuous Improvement
Retraining: The model will need to be periodically retrained with new data to stay up to date and reflect changes in the Metropolitano's usage patterns.

### Summary
This approach seeks to develop a soft AI-based predictive system using artificial neural networks implemented in TensorFlow. Through the use of historical data and supervised training methods, it will be possible to anticipate bus demand and optimize their distribution efficiently. This will not only improve the user experience, but will also allow the Lima Metropolitano to operate more effectively and profitably.

## Challenges

Although the project proposes an innovative solution to predict and optimize bus demand in the Lima Metropolitan, there are several limitations and challenges that cannot be effectively addressed by this system. These challenges must be considered for a realistic and ethical implementation.

1. Unexpected User Behavior:
* The model cannot predict the unpredictable behavior or "liveliness" of users who, for example, decide to travel to the last station just to secure a seat on an empty bus. This type of behavior does not follow regular patterns and is difficult to model accurately.
2. Personal User Preferences:
* The system cannot anticipate users who prioritize convenience over speed. Some users may prefer to wait longer for an empty bus rather than take the first available bus, even if this entails a longer travel time. These decisions are subjective and not based on consistent patterns.
3. External and Unforeseen Events:
* External factors such as demonstrations, accidents, or unexpected road closures cannot be predicted by the model. These events can significantly alter bus demand and distribution, creating scenarios where prediction based on historical data becomes ineffective.
4. Limitations of Current Data:
* The project faces a major challenge related to the lack of accurate and transparent data from the current system. The absence of a detailed history of user movements and preferences means that the initial model must rely on data cross-referenced with other sources, such as censuses or mobility surveys, which might not fully reflect the reality of the system.
5. Ethical Considerations:
* When working with sensitive and personal data, such as user mobility patterns, it is crucial to ensure the privacy and security of the information. In addition, there is a risk of data bias, which could lead to suboptimal decisions that negatively affect certain groups of users, for example, if routes in less-traveled areas receive less attention.
* Furthermore, the implementation of a predictive system could have unintended consequences, such as over-reliance on predictions, which could lead to neglect of other qualitative factors that cannot be captured in a quantitative model.


## What next?

Despite initial challenges, such as lack of a team, limited expertise, bureaucracy, and political barriers, there are opportunities to advance the implementation of this project.

1. Academic Support:
* University Collaboration: Take advantage of the resources available at the university, such as laboratories, equipment, and support from professors. Integrating the project into a research program or thesis could provide access to advanced tools and specialized knowledge.
* Networking and University PR: Use the academic network and events organized by the university to present the idea to influential people. This could open doors to possible collaborations with the public or private sector.

2. Prototype Development:
* Pilot Project: With the help of professors and classmates, develop a functional prototype in a controlled environment, such as a specific route of the Metropolitano. This pilot could serve as a proof of concept to demonstrate the viability of the system and its positive impact.

3. Seek Funding and Partnerships:
* Grants and Scholarships: Research and apply for grants or scholarships for innovative projects in the area of ​​transportation and technology. Universities often have access to research and development funds that could be used for this project.
* Private Sector Partnerships: Identify technology companies or startups interested in developing solutions for public transportation and propose a collaboration to bring the project to reality.

4. Communication and Awareness Strategy:
* Awareness Campaign: Develop a communication strategy that highlights the benefits of the predictive system to improve public transportation. By engaging the community and generating public interest, you can pressure policymakers to support the implementation of the system.

5. Continuing Education:
* Professional Development: Continue to expand your knowledge in artificial intelligence, big data, and predictive analytics through additional courses, certifications, and hands-on projects. This will not only strengthen the project, but also increase your credibility and ability to lead it.

6. Navigating the Bureaucracy:
* Legal and Administrative Advice: Seek the support of law students or professors who can offer advice on how to navigate the bureaucracy and regulations related to public transport. This support could make it easier to overcome administrative and political obstacles.

