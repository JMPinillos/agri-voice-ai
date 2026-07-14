# *Notebooks* del *pipeline*

Esta carpeta contiene las versiones HTML de los *notebooks* desarrollados para <strong style="color:#0098cd">AgriVoice AI</strong>.

Los archivos permiten revisar la metodología, el flujo de trabajo, el código utilizado y los resultados principales de cada etapa del *pipeline* sin necesidad de disponer de un entorno local de ejecución.

> [!NOTE]
> Los *notebooks* ejecutables originales (`.ipynb`) no se incluyen en la versión pública del repositorio. Las versiones HTML se publican con fines de revisión metodológica y documentación técnica, evitando exponer datos sensibles, artefactos temporales o código ejecutable no necesario para la presentación del proyecto.



## Orden de revisión

Los *notebooks* deben consultarse en el siguiente orden:

| Orden | *Notebook*                       | Descripción                                                  | Enlace                                                       |
| :---: | :------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
|   1   | `01_audio_preprocessing.html`    | Estandarización, limpieza y preprocesamiento acústico de los audios. | <a href="https://htmlpreview.github.io/?https://github.com/JMPinillos/agri-voice-ai/blob/main/notebooks_html/01_audio_preprocessing.html" target="_blank" rel="noopener noreferrer">Consultar versión HTML</a> |
|   2   | `02_speech_to_text_asr.html`     | Transcripción de los audios mediante reconocimiento automático del habla. | <a href="https://htmlpreview.github.io/?https://github.com/JMPinillos/agri-voice-ai/blob/main/notebooks_html/02_speech_to_text_asr.html" target="_blank" rel="noopener noreferrer">Consultar versión HTML</a> |
|   3   | `03_nlp_classification_ner.html` | Clasificación de mensajes y extracción de entidades agrícolas. | <a href="https://htmlpreview.github.io/?https://github.com/JMPinillos/agri-voice-ai/blob/main/notebooks_html/03_nlp_classification_ner.html" target="_blank" rel="noopener noreferrer">Consultar versión HTML</a> |
|   4   | `04_nlp_normalization.html`      | Normalización semántica y generación de la salida estructurada. | <a href="https://htmlpreview.github.io/?https://github.com/JMPinillos/agri-voice-ai/blob/main/notebooks_html/04_nlp_normalization.html" target="_blank" rel="noopener noreferrer">Consultar versión HTML</a> |



## Flujo del *pipeline*

<p align="center">
  <img src="https://img.shields.io/badge/1-Audio%20Preprocessing-2EA043?style=flat" alt="1 Audio Preprocessing" width="21%">
  <br><strong>⬇</strong><br>
  <img src="https://img.shields.io/badge/2-Speech%20to%20Text%20ASR-F97316?style=flat" alt="2 Speech to Text ASR" width="20%">
  <br><strong>⬇</strong><br>
  <img src="https://img.shields.io/badge/3-NLP%20Classification%20%2B%20NER-8B5CF6?style=flat" alt="3 NLP Classification and NER" width="24%">
  <br><strong>⬇</strong><br>
  <img src="https://img.shields.io/badge/4-NLP%20Normalization-14B8A6?style=flat" alt="4 NLP Normalization" width="19%">
</p>



Cada *notebook* documenta una etapa específica del *pipeline* y utiliza como entrada los artefactos generados por la etapa anterior.

> [!IMPORTANT]
>
> Los archivos HTML no están diseñados para su ejecución directa. Para conocer la arquitectura completa, los requisitos del sistema y las condiciones de uso del repositorio, consulte el [README principal](../README.md).

