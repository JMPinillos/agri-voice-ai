<!--
README profesional para AgriVoice AI
Autor: José Manuel Pinillos Rubio
Sustituye los marcadores TODO por tus enlaces, imágenes y datos finales antes de publicar.
-->

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

El repositorio se organiza separando configuración, datos, modelos, salidas intermedias y documentación metodológica. Esta estructura facilita la trazabilidad del pipeline, la revisión de cada etapa y la reutilización de los distintos artefactos generados por el sistema.

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



## *Notebooks* del *pipeline*

Las versiones HTML permiten revisar la metodología, el flujo de trabajo, el código utilizado y los resultados principales de cada etapa del sistema.

> [!NOTE]
>
> Los *notebooks* ejecutables originales no se incluyen en la versión pública del repositorio. Se publican versiones HTML para facilitar la revisión metodológica sin exponer innecesariamente código ejecutable, datos sensibles o artefactos de trabajo.





| Orden | Notebook                         | Descripción                                                  | Enlace                                                       |
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
- **Visualización y entorno Jupyter:** generación de gráficos, seguimiento de ejecución y soporte para notebooks.

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

El proyecto fue desarrollado y validado principalmente en un entorno macOS con Apple Silicon. La ejecución de los notebooks se verificó correctamente en dicho entorno.

Algunas librerías de aprendizaje profundo o procesamiento de audio pueden mostrar advertencias asociadas al backend de ejecución disponible, como CPU, CUDA o MPS en Apple Silicon. Estas advertencias no implican necesariamente un error en el pipeline y, en general, no afectan al diseño ni a la lógica funcional del sistema.

Para una ejecución local más estable, se recomienda:

- Utilizar un entorno virtual aislado.
- Instalar las dependencias desde `requirements.txt`.
- Verificar la disponibilidad de `ffmpeg`.
- Ejecutar los notebooks en el orden indicado.
- Revisar las versiones de librerías si se cambia de arquitectura o sistema operativo.



## Uso del repositorio

Este repositorio está orientado principalmente a la revisión metodológica del proyecto mediante documentación, estructura del pipeline, configuraciones, modelos y versiones HTML de los notebooks.

Las versiones HTML incluidas en `notebooks_html/` no requieren instalación local para ser consultadas. Pueden visualizarse directamente desde los enlaces indicados en la sección [Notebooks del pipeline](#notebooks-del-pipeline).

La instalación del entorno solo es necesaria si se desea reproducir el pipeline en local a partir de los notebooks ejecutables originales, los datos correspondientes y las dependencias del proyecto.



## Flujo de ejecución del pipeline

El sistema se ejecuta de forma secuencial, de modo que cada etapa consume la salida generada por la etapa anterior. Esta organización permite mantener la trazabilidad del procesamiento y analizar el comportamiento individual de cada módulo.



<p align="center">
  <img src="https://img.shields.io/badge/01-Audio%20Preprocessing-2EA043?style=for-the-badge" alt="01 Audio Preprocessing">
  <br><strong>⬇</strong><br>
  <img src="https://img.shields.io/badge/02-Speech%20to%20Text%20ASR-F97316?style=for-the-badge" alt="02 Speech to Text ASR">
  <br><strong>⬇</strong><br>
  <img src="https://img.shields.io/badge/03-NLP%20Classification%20%2B%20NER-8B5CF6?style=for-the-badge" alt="03 NLP Classification and NER">
  <br><strong>⬇</strong><br>
  <img src="https://img.shields.io/badge/04-NLP%20Normalization-14B8A6?style=for-the-badge" alt="04 NLP Normalization">
</p>







Cada módulo genera artefactos intermedios o finales dentro de la estructura `data/`:

| Etapa            | Entrada principal                  | Salida principal                          |
| ---------------- | ---------------------------------- | ----------------------------------------- |
| Preprocesamiento | `data/audio/raw/`                  | `data/audio/processed/`                   |
| ASR              | `data/audio/processed/`            | `data/transcriptions/asr_output/`         |
| NLP              | `data/transcriptions/asr_output/`  | `data/structured_data/nlp_output/`        |
| Normalización    | `data/structured_data/nlp_output/` | `data/structured_data/normalized_output/` |















## Flujo de ejecución del pipeline

El sistema se ejecuta de forma secuencial, de modo que cada etapa consume la salida generada por la etapa anterior. Esta organización permite mantener la trazabilidad del procesamiento y analizar el comportamiento individual de cada módulo.

```text
01_audio_preprocessing
        ↓
02_speech_to_text_asr
        ↓
03_nlp_classification_ner
        ↓
04_nlp_normalization
```



Cada módulo consume la salida generada por la etapa anterior y produce artefactos intermedios o finales dentro de la estructura `data/`.

| Etapa | Entrada principal | Salida principal |
|---|---|---|
| Preprocesamiento | `data/audio/raw/` | `data/audio/processed/` |
| ASR | `data/audio/processed/` | `data/transcriptions/asr_output/` |
| NLP | `data/transcriptions/asr_output/` | `data/structured_data/nlp_output/` |
| Normalización | `data/structured_data/nlp_output/` | `data/structured_data/normalized_output/` |

---

## Salida estructurada

La salida final del pipeline se genera en formato **JSON estructurado**, permitiendo representar de forma homogénea la información extraída de cada mensaje de voz.

Ejemplo conceptual:

```json
{
  "audio_id": "AUDIO_001",
  "user_id": "USER_001",
  "tipo": "incidencia",
  "fecha_recepcion": "2026-01-01",
  "transcripcion": "Texto procesado del mensaje...",
  "evento": {
    "cultivo": "cafe",
    "problema": "plaga",
    "tratamiento": "control biologico"
  },
  "estado_procesamiento": "procesado",
  "normalization_version": "v1.1"
}
```

Esta estructura facilita su posterior integración en:

- bases de datos;
- cuadros de mando;
- sistemas de búsqueda semántica;
- herramientas de soporte a la decisión;
- pipelines RAG;
- sistemas de alertas o monitorización agrícola.

---

## Modelos y configuración

El repositorio separa explícitamente código, datos, configuración y modelos.

| Carpeta | Contenido |
|---|---|
| `configs/domain/` | Recursos del dominio agrícola |
| `configs/ner/` | Configuración y diccionarios utilizados por el módulo NER |
| `configs/normalization/` | Mapas y reglas de normalización semántica |
| `models/classification_model/` | Modelo entrenado para clasificación de mensajes |
| `models/ner_model/` | Modelo entrenado para extracción de entidades |
| `tmp/` | Salidas temporales de entrenamiento ignoradas por Git |

Las salidas temporales de entrenamiento no forman parte del repositorio y deben mantenerse excluidas mediante `.gitignore`.

---

## Reproducibilidad

El proyecto ha sido desarrollado con una estructura modular y rutas relativas a la raíz del repositorio para facilitar la ejecución en distintos entornos.

Se utilizan semillas fijas en los procesos de entrenamiento cuando corresponde. Aun así, algunos componentes de aprendizaje profundo pueden presentar pequeñas variaciones entre ejecuciones debido a diferencias de hardware, backend de aceleración o versiones de librerías.

Para mejorar la reproducibilidad se recomienda:

- ejecutar los notebooks en el orden indicado;
- utilizar el entorno definido en `requirements.txt`;
- mantener la estructura de carpetas del repositorio;
- evitar modificar manualmente los artefactos intermedios;
- conservar las versiones de configuración utilizadas en cada ejecución.

---

## Privacidad y datos

Los audios originales, transcripciones completas y salidas asociadas pueden contener información sensible o identificable. Por este motivo, la versión pública del repositorio debe evitar incluir datos reales no anonimizados.

La estructura del proyecto permite publicar únicamente:

- muestras anonimizadas;
- configuraciones generales;
- modelos entrenados si no exponen información sensible;
- notebooks exportados a HTML;
- documentación metodológica.

> Antes de publicar el repositorio, revisar cuidadosamente el contenido de `data/`, `models/`, `notebooks_html/` y cualquier archivo generado automáticamente.

---

## Limitaciones

El sistema debe interpretarse dentro de su ámbito de aplicación y evaluación.

Principales limitaciones:

- el dominio se restringe a café y cacao;
- el rendimiento depende de la calidad de los audios de entrada;
- los errores de ASR pueden propagarse a las etapas de NLP y normalización;
- la normalización semántica depende de los mapas, reglas y diccionarios definidos;
- el sistema no sustituye la validación experta en decisiones agronómicas críticas.

---

## Trabajo futuro

Líneas potenciales de evolución:

- ampliación del dominio a otros cultivos;
- integración con bases de datos relacionales o vectoriales;
- explotación mediante dashboards;
- búsqueda semántica sobre registros agrícolas;
- integración con sistemas RAG;
- generación de alertas para incidencias relevantes;
- evaluación con un mayor volumen de audios y escenarios de campo;
- despliegue como servicio en la nube.

---

## Capturas e imágenes del proyecto

Puedes añadir aquí imágenes, esquemas o capturas del sistema.

### Logo del proyecto

```html
<img src="assets/logo/agrivoice-ai-logo.png" alt="AgriVoice AI logo" width="180"/>
```

### Esquema visual del pipeline

```markdown
![Pipeline AgriVoice AI](assets/images/pipeline-overview.png)
```

### Ejemplo de salida estructurada

```markdown
![Ejemplo JSON estructurado](assets/images/json-output-example.png)
```

Estructura recomendada para imágenes:

```text
assets/
├── logo/
│   └── agrivoice-ai-logo.png
└── images/
    ├── pipeline-overview.png
    └── json-output-example.png
```

---

## Licencia y propiedad intelectual

Este repositorio contiene código, documentación, configuraciones y artefactos desarrollados por:

**José Manuel Pinillos Rubio**

El contenido de este repositorio forma parte de un trabajo académico y técnico desarrollado en el marco de un proyecto de inteligencia artificial aplicada.

Salvo que se indique expresamente lo contrario mediante una licencia específica, todos los derechos de autor y propiedad intelectual sobre el código, documentación y estructura del proyecto pertenecen a **José Manuel Pinillos Rubio**.

No se autoriza la copia, redistribución, reutilización comercial, publicación derivada o incorporación total o parcial de este trabajo en otros proyectos sin autorización expresa del autor.

> Si deseas permitir determinados usos, añade una licencia formal en un archivo `LICENSE`. Si no añades licencia, por defecto el repositorio queda protegido por derechos de autor, pero otros usuarios no tendrán permisos explícitos de uso, copia o modificación.

---

## Autor

**José Manuel Pinillos Rubio**  
Ingeniero Informático · Máster en Inteligencia Artificial  
Proyecto: **AgriVoice AI**

<!-- TODO: Añadir enlaces profesionales si procede -->
<!-- GitHub: https://github.com/USUARIO -->
<!-- LinkedIn: https://www.linkedin.com/in/USUARIO -->
<!-- Email: correo@ejemplo.com -->

---

<p align="center">
  <strong>AgriVoice AI</strong><br>
  Transformando mensajes de voz agrícolas en datos estructurados mediante inteligencia artificial.
</p>
