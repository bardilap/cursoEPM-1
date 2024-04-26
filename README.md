# cursoEPM-1
# Proyecto de Predicción ENSA
#Brayan Ardila y Jhonatan Escobar
## Descripción
Este repositorio contiene el código y el análisis para un proyecto de modelado de series temporales cuyo objetivo es predecir la variable ENSA. El modelo se basa en datos históricos y utiliza técnicas de aprendizaje automático para proyectar valores futuros.

## Cambios Realizados
A lo largo del desarrollo del proyecto, se han realizado varios cambios significativos para mejorar la precisión del modelo y su capacidad para capturar patrones dentro de los datos. Estos cambios incluyen:

1. Característica Combinada
Se introdujo una nueva característica que combina dos de las variables más correlacionadas con ENSA, Panama y PIB__corriente. La razón detrás de esto es aprovechar la relación entre estas dos variables para mejorar las predicciones del modelo.

Código Añadido:

datos_Maestro['combined_feature'] = datos_Maestro['Panama'] / datos_Maestro['PIB__corriente']

2. Ajuste del Tamaño de Ventana
El tamaño de la ventana para la creación de secuencias temporales se incrementó de 6 a 24 para abarcar un ciclo estacional completo y mejorar la capacidad del modelo para aprender patrones estacionales.

Código Modificado:

window_size = 24
X, y = create_sequences(features_selected_scaled_df, datos_Maestro['ENSA'], window_size=24)

3. Cambio en la División de Datos
Se modificó la proporción de división de datos de entrenamiento y validación para proporcionar más datos al modelo durante la fase de entrenamiento, buscando una mejora en el aprendizaje y la generalización.

Código Modificado:

X_train, X_val, y_train, y_val = train_test_split(X, y, test_size=0.05, random_state=42)
4. Incremento en las Neuronas de las Capas
Se aumentó el número de neuronas en las capas GRU y la capa densa para dar al modelo más capacidad para capturar la complejidad de los datos.

Código Modificado:
GRU(150, activation='relu', return_sequences=True),
GRU(150, activation='relu'),
Dense(50, activation='relu'),

5. Aumento de Epochs y Batch Size
Se incrementaron las épocas de entrenamiento y el tamaño del batch para proporcionar un entrenamiento más exhaustivo y robusto al modelo.

Código Modificado:
history = model.fit(X_train, y_train, epochs=50, batch_size=64, validation_data=(X_val, y_val))

6. Mejora en la Visualización de Predicciones
Se realizaron ajustes en la visualización final para conectar de manera fluida los datos históricos con la predicción, facilitando la interpretación de la transición de los datos conocidos a los valores proyectados.

Código Añadido:
# Extraer el último punto de los datos históricos para conectarlo con las predicciones
last_historical_value = datos_Maestro['ENSA'].iloc[-1]
last_historical_index = datos_Maestro.index[-1]
# Conectar el último punto de los datos históricos con el primer punto de la predicción
plt.plot([last_historical_index, predicted_data.index[0]], [last_historical_value, predi
