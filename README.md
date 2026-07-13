### Logo del proyecto

```html
<img src="assets/logo/agrivoice-ai-logo.png" alt="AgriVoice AI logo" width="180"/>

```



<p align="center">
  <!-- TODO: Sustituir por el logo definitivo del proyecto -->
  <!-- Ejemplo: <img src="assets/logo/agrivoice-ai-logo.png" alt="AgriVoice AI logo" width="180"/> -->
</p>

<h1 align="center">AgriVoice AI</h1>

<p align="center">
  <strong>Transformación de mensajes de voz de productores agrícolas en información estructurada mediante inteligencia artificial</strong>
</p>

<p align="center">
  <a href="#descripción-general"><img src="https://img.shields.io/badge/Proyecto-Inteligencia%20Artificial-6f42c1?style=for-the-badge" alt="Proyecto IA"></a>
  <a href="#pipeline-del-sistema"><img src="https://img.shields.io/badge/Pipeline-Audio%20%7C%20ASR%20%7C%20NLP%20%7C%20JSON-2ea44f?style=for-the-badge" alt="Pipeline"></a>
  <a href="#ámbito-de-aplicación"><img src="https://img.shields.io/badge/Dominio-Café%20%26%20Cacao-brown?style=for-the-badge" alt="Café y cacao"></a>
  <a href="#licencia-y-propiedad-intelectual"><img src="https://img.shields.io/badge/Propiedad%20intelectual-José%20Manuel%20Pinillos%20Rubio-blue?style=for-the-badge" alt="Propiedad intelectual"></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/ASR-Faster--Whisper-111111?style=flat-square" alt="Faster Whisper">
  <img src="https://img.shields.io/badge/NLP-spaCy%20%7C%20Transformers-09A3D5?style=flat-square" alt="NLP">
  <img src="https://img.shields.io/badge/Output-Structured%20JSON-ffb000?style=flat-square" alt="JSON">
  <img src="https://img.shields.io/badge/Status-Academic%20TFM-important?style=flat-square" alt="Academic project">
</p>

---

## Índice

- [Descripción general](#descripción-general)
- [Ámbito de aplicación](#ámbito-de-aplicación)
- [Pipeline del sistema](#pipeline-del-sistema)
- [Arquitectura del repositorio](#arquitectura-del-repositorio)
- [Notebooks del pipeline](#notebooks-del-pipeline)
- [Requisitos del sistema](#requisitos-del-sistema)
- [Instalación](#instalación)
- [Ejecución del pipeline](#ejecución-del-pipeline)
- [Salida estructurada](#salida-estructurada)
- [Modelos y configuración](#modelos-y-configuración)
- [Reproducibilidad](#reproducibilidad)
- [Privacidad y datos](#privacidad-y-datos)
- [Limitaciones](#limitaciones)
- [Trabajo futuro](#trabajo-futuro)
- [Licencia y propiedad intelectual](#licencia-y-propiedad-intelectual)

---



## Descripción general

**AgriVoice AI** es un sistema modular de inteligencia artificial diseñado para transformar mensajes de audio generados en contextos agrícolas en información estructurada, trazable y reutilizable.

En entornos de campo, la información sobre cultivos, incidencias, tratamientos y condiciones ambientales se comunica con frecuencia de forma oral o mediante registros informales. Esta forma de captura reduce la fricción para el productor, pero dificulta su almacenamiento homogéneo, su consulta posterior y su integración con herramientas digitales de análisis y toma de decisiones.

El proyecto propone un *pipeline* secuencial compuesto por módulos especializados de preprocesamiento acústico, reconocimiento automático del habla, procesamiento del lenguaje natural y normalización semántica. A partir de esta arquitectura, el sistema permite convertir mensajes de voz en registros agrícolas preparados para su almacenamiento, consulta y explotación posterior.

El desarrollo se centra en los cultivos de café y cacao en Latinoamérica, con el objetivo de evaluar la viabilidad de una solución de inteligencia artificial aplicada a escenarios reales de comunicación agrícola.



## Ámbito de aplicación

AgriVoice AI está diseñado para procesar mensajes de audio generados en contextos agrícolas de campo, con un alcance centrado en los cultivos de **café y cacao en Latinoamérica**.

El sistema contempla comunicaciones orales relacionadas con observaciones sobre el estado del cultivo, incidencias fitosanitarias, tratamientos aplicados, condiciones ambientales, zonas de cultivo, cantidades, superficies, fechas y otros elementos relevantes para la gestión agrícola.

Esta delimitación permite adaptar el *pipeline* al vocabulario, las expresiones y las necesidades propias del dominio, evitando plantear el sistema como una solución agrícola generalista. El objetivo es obtener registros estructurados, coherentes y reutilizables dentro de un contexto de aplicación claramente definido.



## *Pipeline* del sistema

AgriVoice AI se estructura como un *pipeline* secuencial en el que cada módulo transforma la salida de la etapa anterior y genera artefactos intermedios reutilizables. Esta arquitectura permite evaluar cada componente de forma independiente y analizar cómo los errores pueden propagarse a lo largo del sistema.



<p align="center">
  <img src="./assets/images/Diagrama_de_flujo.png" alt="Diagrama_de_flujo" width="100%">
</p>



El flujo principal del sistema comprende una entrada inicial de audio y cinco módulos de procesamiento:

|     Tipo     |             Etapa             | Descripción                                                  |
| :----------: | :---------------------------: | ------------------------------------------------------------ |
| **Entrada**  |           **Audio**           | Mensajes de voz generados en campo por productores o técnicos agrícolas. |
| **Módulo 1** | **Preprocesamiento acústico** | Estandarización de los audios y aplicación selectiva de filtros y transformaciones acústicas para mejorar la calidad de la señal y favorecer el rendimiento del sistema ASR. |
| **Módulo 2** |            **ASR**            | Conversión de los mensajes de voz en transcripciones mediante reconocimiento automático del habla. |
| **Módulo 3** |       **Clasificación**       | Identificación de la categoría funcional del mensaje.        |
| **Módulo 4** |            **NER**            | Extracción de entidades relevantes del dominio agrícola, incluyendo cultivos, incidencias, tratamientos, magnitudes, referencias temporales, condiciones ambientales y otros elementos de interés para la estructuración de la información. |
| **Módulo 5** |       **Normalización**       | Homogeneización semántica de la información extraída y generación de registros estructurados, trazables y reutilizables. |



## Arquitectura del repositorio

El repositorio se organiza separando configuración, datos, modelos, salidas intermedias y documentación metodológica. Esta estructura facilita la trazabilidad del *pipeline*, la revisión de cada etapa y la reutilización de los distintos artefactos generados por el sistema.

```text
agri-voice-ai/
│
├── configs/                         # Configuración del dominio, NER y normalización
│   ├── domain/
│   ├── ner/
│   └── normalization/
│
├── data/                            # Datos de entrada, salidas intermedias y resultados estructurados
│   ├── audio/
│   │   ├── raw/
│   │   ├── standardized/
│   │   └── processed/
│   │
│   ├── transcriptions/
│   │   ├── asr_output/
│   │   ├── ground_truth/
│   │   └── predictions/
│   │
│   ├── structured_data/
│   │   ├── nlp_output/
│   │   └── normalized_output/
│   │
│   ├── datasets/
│   │   └── ner/
│   │
│   ├── metadata/
│   │   └── audio_metadata/
│   │
│   └── samples/
│
├── models/                          # Modelos entrenados del sistema
│   ├── classification_model/
│   └── ner_model/
│
├── notebooks_html/                  # Versiones HTML de los notebooks del pipeline
│   ├── 01_audio_preprocessing.html
│   ├── 02_speech_to_text_asr.html
│   ├── 03_nlp_classification_ner.html
│   └── 04_nlp_normalization.html
│
├── assets/                          # Imágenes y recursos visuales del repositorio
│   └── images/
│
├── requirements.txt                 # Dependencias Python del proyecto
├── .gitignore
└── README.md
```



### Recursos de configuración y modelos

Los recursos de configuración y los modelos entrenados se mantienen separados del resto de datos del proyecto para facilitar su mantenimiento, trazabilidad y reutilización.

| **Carpeta**                    | **Contenido**                                                |
| ------------------------------ | ------------------------------------------------------------ |
| `configs/domain/`              | Recursos del dominio agrícola utilizados como apoyo al procesamiento. |
| `configs/ner/`                 | Configuración, etiquetas y diccionarios empleados por el módulo de extracción de entidades. |
| `configs/normalization/`       | Mapas, reglas y recursos utilizados para la normalización semántica. |
| `models/classification_model/` | Modelo entrenado para la clasificación de mensajes agrícolas. |
| `models/ner_model/`            | Modelo entrenado para la extracción de entidades del dominio. |
| `tmp/`                         | Directorio temporal para salidas auxiliares de entrenamiento, excluido del control de versiones. |

El directorio `tmp/` se genera únicamente durante ejecuciones locales y permanece excluido del repositorio mediante `.gitignore`.



## *Notebooks* del *pipeline*

Las versiones HTML permiten revisar la metodología, el flujo de trabajo, el código utilizado y los resultados principales de cada etapa del sistema.

> [!NOTE]
>
> Los *notebooks* ejecutables originales no se incluyen en la versión pública del repositorio. Se publican versiones HTML para facilitar la revisión metodológica sin exponer innecesariamente código ejecutable, datos sensibles o artefactos de trabajo.



| Orden | *Notebook*                       | Descripción                                                  | Enlace                                                       |
| :---: | :------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
|   1   | `01_audio_preprocessing.html`    | Estandarización, limpieza y preprocesamiento acústico de los audios. | <a href="https://htmlpreview.github.io/?https://github.com/JMPinillos/agri-voice-ai/blob/main/notebooks_html/01_audio_preprocessing.html" target="_blank" rel="noopener noreferrer">  Consultar versión HTML</a> |
|   2   | `02_speech_to_text_asr.html`     | Transcripción de los audios mediante reconocimiento automático del habla. | <a href="https://htmlpreview.github.io/?https://github.com/JMPinillos/agri-voice-ai/blob/main/notebooks_html/02_speech_to_text_asr.html" target="_blank" rel="noopener noreferrer">Consultar versión HTML</a> |
|   3   | `03_nlp_classification_ner.html` | Clasificación de mensajes y extracción de entidades agrícolas. | <a href="https://htmlpreview.github.io/?https://github.com/JMPinillos/agri-voice-ai/blob/main/notebooks_html/03_nlp_classification_ner.html" target="_blank" rel="noopener noreferrer">Consultar versión HTML</a> |
|   4   | `04_nlp_normalization.html`      | Normalización semántica y generación de la salida estructurada. | <a href="https://htmlpreview.github.io/?https://github.com/JMPinillos/agri-voice-ai/blob/main/notebooks_html/04_nlp_normalization.html" target="_blank" rel="noopener noreferrer">Consultar versión HTML</a> |



## Requisitos del sistema

El proyecto requiere un entorno de ejecución con **Python 3.x**, las dependencias Python definidas en `requirements.txt` y determinadas dependencias de sistema para el procesamiento de audio.



### Dependencias del proyecto

Las dependencias Python del proyecto se definen en el archivo `requirements.txt` y se agrupan según las etapas principales del *pipeline*:

- **Procesamiento de audio:** carga, conversión, limpieza, reducción de ruido y detección de actividad de voz.
- **ASR:** transcripción automática del habla y evaluación mediante métricas WER y CER.
- **NLP:** clasificación de mensajes, extracción de entidades, uso de modelos basados en Transformers y utilidades de aprendizaje automático.
- **Normalización:** tratamiento de fechas, unidades, variantes lingüísticas y correspondencias semánticas.
- **Visualización y entorno Jupyter:** generación de gráficos, seguimiento de ejecución y soporte para *notebooks*.

Para instalar todas las dependencias del entorno Python:

```bash
pip install -r requirements.txt
```



### **Dependencias de sistema**

El procesamiento de archivos de audio como `.m4a`, `.mp3` u otros formatos comprimidos requiere la herramienta externa **ffmpeg**. Esta dependencia permite que las librerías de audio puedan leer, convertir y manipular formatos que no siempre son soportados directamente por el entorno Python.

Si `ffmpeg` no está disponible, el procesamiento puede quedar limitado a formatos compatibles de forma nativa, como `.wav`.



### Instalación de ffmpeg

A continuación se muestran opciones habituales de instalación de `ffmpeg` según el sistema operativo. Puede utilizarse cualquiera de los métodos indicados, siempre que el comando `ffmpeg` quede disponible desde la terminal.



#### macOS

```bash
brew install ffmpeg
```



#### Windows

Con Chocolatey:

```bash
choco install ffmpeg
```

Con Winget:

```bash
winget install Gyan.FFmpeg
```

También puede instalarse manualmente descargando una versión compilada de `ffmpeg` y añadiendo la carpeta `bin` al `PATH` del sistema.



#### Linux

En distribuciones basadas en Debian o Ubuntu:

```bash
sudo apt update
sudo apt install ffmpeg
```



### Verificación de instalación

Después de instalar `ffmpeg`, puede comprobarse su disponibilidad mediante:

```bash
ffmpeg -version
```



### Consideraciones de ejecución

El proyecto fue desarrollado y validado principalmente en un entorno macOS con Apple Silicon. La ejecución de los *notebooks* se verificó correctamente en dicho entorno.

Algunas librerías de aprendizaje profundo o procesamiento de audio pueden mostrar advertencias asociadas al backend de ejecución disponible, como CPU, CUDA o MPS en Apple Silicon. Estas advertencias no implican necesariamente un error en el *pipeline* y, en general, no afectan al diseño ni a la lógica funcional del sistema.

Para una ejecución local más estable, se recomienda:

- Utilizar un entorno virtual aislado.
- Instalar las dependencias desde `requirements.txt`.
- Verificar la disponibilidad de `ffmpeg`.
- Ejecutar los *notebooks* en el orden indicado.
- Revisar las versiones de librerías si se cambia de arquitectura o sistema operativo.



## Uso del repositorio

Este repositorio está orientado principalmente a la revisión metodológica del proyecto mediante documentación, estructura del *pipeline*, configuraciones, modelos y versiones HTML de los *notebooks*.

Las versiones HTML incluidas en `notebooks_html/` no requieren instalación local para ser consultadas. Pueden visualizarse directamente desde los enlaces indicados en la sección [*Notebooks* del *pipeline*](#notebooks-del-pipeline).

La instalación del entorno solo es necesaria si se desea reproducir el *pipeline* en local a partir de los *notebooks* ejecutables originales, los datos correspondientes y las dependencias del proyecto.



### Reproducibilidad

El proyecto utiliza una estructura modular, rutas relativas a la raíz del repositorio y recursos de configuración versionados para facilitar la reproducción del flujo de trabajo en distintos entornos.

Cuando corresponde, se emplean semillas fijas en los procesos de entrenamiento. No obstante, algunos componentes de aprendizaje profundo pueden presentar pequeñas variaciones entre ejecuciones debido al hardware, al backend de aceleración o a las versiones de las librerías utilizadas.

Para reproducir el *pipeline* de forma consistente se recomienda mantener la estructura de carpetas del repositorio, instalar las dependencias desde `requirements.txt`, ejecutar las etapas en el orden indicado y conservar las versiones de configuración utilizadas en cada ejecución.



## Flujo de ejecución del *pipeline*

El sistema se ejecuta de forma secuencial, de modo que cada etapa consume la salida generada por la etapa anterior. Esta organización permite mantener la trazabilidad del procesamiento y analizar el comportamiento individual de cada módulo.



<p align="center">
  <img src="https://img.shields.io/badge/1-Audio%20Preprocessing-2EA043?style=flat" alt="01 Audio Preprocessing" width="21%">
  <br><strong>⬇</strong><br>
  <img src="https://img.shields.io/badge/2-Speech%20to%20Text%20ASR-F97316?style=flat" alt="02 Speech to Text ASR" width="20%">
  <br><strong>⬇</strong><br>
  <img src="https://img.shields.io/badge/3-NLP%20Classification%20%2B%20NER-8B5CF6?style=flat" alt="03 NLP Classification and NER" width="24%">
  <br><strong>⬇</strong><br>
  <img src="https://img.shields.io/badge/4-NLP%20Normalization-14B8A6?style=flat" alt="04 NLP Normalization" width="20%">
</p>



Cada etapa consume los artefactos generados por la anterior y escribe sus resultados en una ubicación específica de `data/`:

| Etapa                | Entrada principal                  | Salida principal                          |
| :------------------- | :--------------------------------- | :---------------------------------------- |
| **Preprocesamiento** | `data/audio/raw/`                  | `data/audio/processed/`                   |
| **ASR**              | `data/audio/processed/`            | `data/transcriptions/asr_output/`         |
| **NLP**              | `data/transcriptions/asr_output/`  | `data/structured_data/nlp_output/`        |
| **Normalización**    | `data/structured_data/nlp_output/` | `data/structured_data/normalized_output/` |



## Salida estructurada

La salida final del *pipeline* se materializa en registros estructurados en formato **JSON**, donde se integra la transcripción del mensaje de audio, la clasificación del mensaje, las entidades normalizadas y los metadatos asociados al procesamiento.

Cada registro mantiene la trazabilidad entre el audio original, la transcripción utilizada y la información agrícola extraída, facilitando su posterior almacenamiento, consulta y explotación.

Ejemplo simplificado de estructura de salida:

```json
{
  "audio_id": "AUDIO_XXXXX",
  "user_id": null,
  "tipo": "evento_cultivo",
  "timestamp_recepcion": "YYYY-MM-DDTHH:MM:SSZ",
  "fecha_recepcion": "YYYY-MM-DD",
  "transcripcion": "Transcripción del mensaje de audio...",
  "evento": {
    "fecha_evento": null,
    "fecha_evento_fin": null,
    "granularidad_fecha_evento": null,
    "cultivo": "cafe",
    "variedad": null,
    "accion": null,
    "categoria_accion": null,
    "magnitudes": [
      {
        "tipo": "conteo",
        "valor": 40.0,
        "unidad": null,
        "unidad_original": "unidad_original_detectada",
        "estado": "unidad_no_mapeada"
      }
    ],
    "problemas": ["plaga", "broca", "enfermedad"],
    "tratamientos": ["cosecha", "fertilizacion", "control_maleza", "poda"],
    "partes_planta": [],
    "estado_cultivo": null,
    "espacio_agricola": null,
    "localidad": null,
    "region": null,
    "pais": null,
    "factor_climatico": ["cambio_climatico", "sequia"],
    "sistema_produccion": null,
    "especie_sombra": []
  },
  "estado_procesamiento": "ok",
  "normalization_version": "1.1"
}
```



Esta representación permite transformar comunicaciones orales de campo en registros homogéneos, trazables y preparados para su almacenamiento, consulta y explotación posterior en bases de datos, cuadros de mando, motores de búsqueda semántica, arquitecturas RAG u otros sistemas de análisis.



## Privacidad y datos

El proyecto ha sido desarrollado con audios reales y transcripciones asociadas a contextos agrícolas de campo. Este tipo de información puede contener datos personales, referencias locales, nombres propios u otros elementos potencialmente identificables.

Por este motivo, la versión pública del repositorio está orientada a la revisión metodológica y no incluye datos reales no anonimizados. La publicación del proyecto prioriza la documentación del *pipeline*, la estructura del sistema, las configuraciones generales, los modelos entrenados cuando proceda y las versiones HTML de los *notebooks*.

Antes de publicar nuevas versiones del repositorio, debe revisarse cuidadosamente el contenido de `data/`, `models/`, `notebooks_html/` y cualquier archivo generado automáticamente para evitar la exposición accidental de información sensible.

> [!IMPORTANT]
> Los datos reales del proyecto no deben publicarse sin un proceso previo de anonimización y validación.



## Licencia y propiedad intelectual

Este repositorio contiene código, documentación, configuraciones y artefactos desarrollados por **José Manuel Pinillos Rubio** en el marco del proyecto **AgriVoice AI**, un trabajo académico y técnico de inteligencia artificial aplicada.

El contenido se publica con fines de revisión, presentación académica y documentación técnica del proyecto.

Todos los derechos sobre el código, la documentación, la estructura del proyecto, los recursos de configuración, los modelos y los artefactos incluidos pertenecen a **José Manuel Pinillos Rubio**.

Este repositorio no se distribuye bajo una licencia de código abierto. Su uso, copia, modificación, redistribución, reutilización comercial, publicación derivada o incorporación total o parcial en otros proyectos requiere autorización expresa del autor.

Para más información, consultar el archivo [`LICENSE`](LICENSE).



## Autor

**José Manuel Pinillos Rubio** 

Ingeniero Informático · Máster en Inteligencia Artificial 

Proyecto: **AgriVoice AI**

<!-- Enlaces profesionales opcionales -->
<!-- GitHub: https://github.com/JMPinillos -->
<!-- LinkedIn: https://www.linkedin.com/in/USUARIO -->
<!-- Email: correo@ejemplo.com -->
