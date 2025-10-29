# 🧠 Laboratorio: Estimación de edad a partir de imágenes faciales

---

## 🎯 Descripción general

En este proyecto, deberán diseñar un modelo de **inteligencia artificial** capaz de **predecir el rango etario** de una persona a partir de una imagen de su rostro.

El trabajo combina conceptos de **computer vision**, **deep learning** y **transfer learning**, utilizando un dataset público y herramientas de código abierto.

El modelo deberá clasificar las imágenes en **cuatro categorías** de edad:

- 👶 **Niño:** 0–12 años  
- 🧒 **Joven:** 13–25 años  
- 🧑 **Adulto:** 26–59 años  
- 👴 **Mayor:** 60+ años

---

## ⚙️ Requisitos técnicos

- **Lenguaje:** Python 3.10+   
- **Librerías recomendadas:**  
  `tensorflow`, `keras`, `opencv-python`, `numpy`, `pandas`, `matplotlib`, `scikit-learn`   
- **Dataset sugerido:** [UTKFace Dataset](https://susanqq.github.io/UTKFace/) (público y de uso académico)  

---

## 🧠 Actividades

### 1. Cargar el dataset

Cada archivo del dataset tiene un formato similar a:  
`age_gender_race_date.jpg`

Ejemplo:
```python
import os
import cv2
import pandas as pd

images, ages = [], []

for filename in os.listdir('UTKFace'):
    age = int(filename.split('_')[0])
    img = cv2.imread(os.path.join('UTKFace', filename))
    if img is not None:
        img = cv2.resize(img, (128, 128))
        images.append(img)
        ages.append(age)

df = pd.DataFrame({'age': ages})
```

### 1. Crear categorías de edad

```python
def categorize_age(age):
    if age <= 12:
        return 'child'
    elif age <= 25:
        return 'young'
    elif age <= 50:
        return 'adult'
    else:
        return 'senior'

df['age_group'] = df['age'].apply(categorize_age)

```
### 3. Preparar datos para entrenamiento

```python
from sklearn.model_selection import train_test_split
from tensorflow.keras.utils import to_categorical
import numpy as np

X = np.array(images) / 255.0
y = pd.get_dummies(df['age_group']).values

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, stratify=y)

```

### 4. Modelo base (transfer learning)

```python

import tensorflow as tf
from tensorflow.keras.applications import MobileNetV2
from tensorflow.keras import layers, models

base_model = MobileNetV2(weights='imagenet', include_top=False, input_shape=(128,128,3))
base_model.trainable = False  # Congelar capas base

model = models.Sequential([
    base_model,
    layers.GlobalAveragePooling2D(),
    layers.Dense(128, activation='relu'),
    layers.Dropout(0.3),
    layers.Dense(4, activation='softmax')
])

model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])
history = model.fit(X_train, y_train, validation_data=(X_test, y_test), epochs=5)


```

### 5. Evaluación y visualización

```python

import matplotlib.pyplot as plt

plt.plot(history.history['accuracy'], label='train acc')
plt.plot(history.history['val_accuracy'], label='val acc')
plt.legend()
plt.title('Evolución de la precisión')
plt.show()

# Ejemplo de predicción
pred = model.predict(X_test[:5])

```
## 💡 Extensiones opcionales

- Agregar predicción de género además de edad.
- Crear una demo interactiva en Streamlit o en Colab que permita subir una imagen.
