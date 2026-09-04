# Modelos entrenados

Esta carpeta contiene los artefactos generados durante el entrenamiento de los modelos utilizados en el proyecto.

Los modelos se incluyen con finalidad demostrativa y de revisión del trabajo. Su rendimiento está condicionado por el conjunto de datos empleado durante el desarrollo, por lo que no deben interpretarse como modelos generalizables sin un nuevo proceso de entrenamiento, validación y adaptación al dominio de aplicación.



## Contenido

- `classification_model/`: modelo de clasificación de mensajes, codificador de etiquetas y vectorizador.
- `ner_model/`: modelo NER entrenado con spaCy para la extracción de entidades agrícolas.



> [!NOTE]
>
> Estos modelos permiten documentar la estructura final del sistema y facilitar la comprensión del *pipeline*, pero su reutilización en otros contextos requiere reentrenamiento o ajuste con nuevos datos representativos.
