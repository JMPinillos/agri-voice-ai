# 🧠 Model Training

Esta carpeta contiene todos los recursos relacionados con el **entrenamiento, ajuste y evaluación de modelos** utilizados en el proyecto. Aunque el TFM se centra en un pipeline ligero y eficiente, esta carpeta está diseñada para permitir la **evolución futura** hacia modelos más avanzados y entrenamientos completos.



## 📁 Estructura

```
model_training/
├── configs/                 # Archivos de configuración (YAML/JSON)
│   └── training_config.yaml
│
├── training_scripts/        # Scripts de entrenamiento y evaluación
│   ├── train_ner.py
│   └── evaluate_ner.py
│
├── models/                  # Checkpoints o pesos de modelos entrenados (opcional)
│
└── README.md                # Este archivo
```



## 🎯 Objetivo de esta carpeta

Esta carpeta está diseñada para centralizar todo lo relacionado con **modelos entrenables**, en especial para:

- **Fine-tuning ligero** de modelos preentrenados (ej. BETO, BERT).
- Entrenamiento y evaluación de modelos de **NER**, clasificación o embeddings.
- Mantener una estructura modular que facilite extender el proyecto a entornos profesionales.
- Registrar configuraciones, experimentos y resultados.



## 🚀 Uso en el TFM (versión actual)

Para el Trabajo Fin de Máster, esta carpeta se utilizará principalmente para:

### ✔ Fine-tuning ligero de NER
- Utilizar un modelo preentrenado (BETO/BERT).
- Ajustarlo con un conjunto pequeño de ejemplos anotados.
- Obtener un modelo especializado en el dominio agronómico.

### ✔ Evaluación del modelo
- Cálculo de métricas (Precision, Recall, F1).
- Comparación de versiones del modelo si es necesario.
- Documentación de resultados reproducibles.



## 🏗 Líneas futuras (evolución profesional)

En un contexto real con más datos disponibles, esta carpeta podría ampliarse para:

- Entrenar un **NER completo** con cientos o miles de ejemplos.
- Implementar **LoRA** u otros métodos de ajuste eficiente para LLMs.
- Ajustar modelos **ASR** (SpeechBrain / Whisper Large) al dominio agrícola.
- Añadir más configuraciones avanzadas (hiperparámetros, experimentos).
- Crear un pipeline de evaluación automatizado.

Esta carpeta permite que el proyecto crezca sin comprometer la organización ni la modularidad.



## 📌 Buenas prácticas

- Mantén todos los experimentos documentados dentro de esta carpeta.
- Usa archivos YAML/JSON para separación clara entre código y configuración.
- Versiona checkpoints ligeros, pero **no subas modelos pesados** al repositorio (añadirlos a `.gitignore`).
- Registra métricas y configura logs para asegurar reproducibilidad.



