# AgriVoice AI

**Transforming Agricultural Producers’ Voice Messages into Structured Data**

AgriVoice AI is a modular artificial intelligence pipeline designed to transform unstructured agricultural voice messages into structured, traceable and reusable data records. The system focuses on field audio messages related to **coffee and cacao crops in Latin America**, integrating acoustic preprocessing, automatic speech recognition, natural language processing and semantic normalization.

The repository documents the complete workflow developed as part of a Master’s thesis project on applied artificial intelligence for agricultural data management.

---

## Overview

In many agricultural contexts, relevant field information about crops, incidents, treatments or environmental conditions is generated orally and recorded informally. This limits its later use in databases, dashboards, decision-support tools or semantic search systems.

AgriVoice AI addresses this problem through a sequential and modular pipeline:

```mermaid
flowchart LR
    A[Raw audio message] --> B[Acoustic preprocessing]
    B --> C[Automatic speech recognition]
    C --> D[Message classification]
    D --> E[Named entity recognition]
    E --> F[Semantic normalization]
    F --> G[Structured JSON output]
```

The goal is not only to transcribe audio, but to convert informal field communication into structured agricultural information that can be analyzed, validated and reused.

---

## Main Features

- Modular end-to-end AI pipeline for agricultural voice messages.
- Adaptive audio preprocessing for heterogeneous field recordings.
- Automatic speech recognition for Spanish agricultural audio messages.
- Message classification using machine learning and transformer-based approaches.
- Domain-oriented entity extraction for coffee and cacao contexts.
- Hybrid NER strategy combining model-based extraction and specialized dictionaries.
- Semantic normalization into homogeneous structured JSON records.
- Reproducible notebook-based workflow.
- HTML notebook exports for transparent methodological review.

---

## Repository Structure

```text
agri-voice-ai/
│
├── configs/
│   ├── domain/
│   ├── ner/
│   └── normalization/
│
├── data/
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
├── models/
│   ├── classification_model/
│   └── ner_model/
│
├── notebooks_html/
│   ├── 01_audio_preprocessing.html
│   ├── 02_speech_to_text_asr.html
│   ├── 03_nlp_classification_ner.html
│   └── 04_nlp_normalization.html
│
├── .gitignore
├── README.md
└── requirements.txt
```

> The executable notebooks are not included in the public repository. Instead, HTML exports are provided to document the methodology, code flow and main results while avoiding unnecessary exposure of executable notebook artifacts.

---

## Pipeline Modules

### 1. Acoustic Preprocessing

The first module standardizes and preprocesses the audio recordings before transcription. It includes operations such as format conversion, sampling rate standardization, silence handling, noise reduction and signal normalization.

The preprocessing stage is applied selectively, since not all transformations improve every input signal. This is especially relevant in real agricultural recordings, where audio quality, background noise and recording conditions may vary significantly.

### 2. Automatic Speech Recognition

The ASR module converts preprocessed audio messages into text. The output of this stage is later used by the NLP modules, so transcription quality directly affects the downstream classification, entity extraction and normalization tasks.

### 3. NLP Classification and Entity Extraction

This module classifies the transcribed messages and extracts relevant domain entities. The approach combines:

- message classification models;
- a domain-adapted NER model;
- specialized dictionaries for coffee and cacao terminology;
- evaluation on both ground-truth and ASR-generated transcriptions.

### 4. Semantic Normalization

The final module transforms the extracted information into normalized structured records. This stage maps detected entities to controlled domain values, applies normalization rules and generates a consistent JSON output.

The resulting records are suitable for later integration into databases, dashboards, semantic search systems or decision-support workflows.

---

## Notebook Documentation

The methodological workflow is documented through HTML notebook exports.

| Step | Notebook | Description |
|---:|---|---|
| 1 | [Audio preprocessing](notebooks_html/01_audio_preprocessing.html) | Audio standardization, preprocessing and signal preparation. |
| 2 | [Speech-to-text ASR](notebooks_html/02_speech_to_text_asr.html) | Automatic transcription of agricultural voice messages. |
| 3 | [NLP classification and NER](notebooks_html/03_nlp_classification_ner.html) | Message classification, entity extraction and evaluation. |
| 4 | [Semantic normalization](notebooks_html/04_nlp_normalization.html) | Entity normalization and structured JSON generation. |

### Viewing HTML notebooks on GitHub

GitHub does not always render standalone HTML files directly. If the HTML files are displayed as source code, they can be viewed through HTMLPreview using the following pattern:

```text
https://htmlpreview.github.io/?https://github.com/<USER>/<REPOSITORY>/blob/main/notebooks_html/01_audio_preprocessing.html
```

Replace `<USER>` and `<REPOSITORY>` with the corresponding GitHub account and repository name.

---

## System Requirements

The project requires Python 3.x and several Python and system-level dependencies.

### System Dependency: FFmpeg

Processing compressed audio files such as `.m4a` or `.mp3` requires `ffmpeg`. Without this dependency, the pipeline may be limited to formats supported by `libsndfile`, such as `.wav`.

#### macOS Installation

```bash
brew install ffmpeg
```

#### Ubuntu / Debian Installation

```bash
sudo apt update
sudo apt install ffmpeg
```

#### Windows Installation

Install FFmpeg from the official distribution source and ensure that the executable is available in the system `PATH`.

---

## Python Environment Setup

Create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate
```

On Windows:

```bash
python -m venv .venv
.venv\Scripts\activate
```

Install the project dependencies:

```bash
pip install -r requirements.txt
```

---

## Execution Order

The pipeline is designed to be executed sequentially:

```text
01_audio_preprocessing
        ↓
02_speech_to_text_asr
        ↓
03_nlp_classification_ner
        ↓
04_nlp_normalization
```

Each module generates intermediate outputs that are used by the next stage.

Expected output locations:

```text
data/audio/processed/
data/transcriptions/asr_output/
data/structured_data/nlp_output/
data/structured_data/normalized_output/
```

---

## Output Format

The final output is a structured JSON record containing normalized agricultural information. The exact schema depends on the detected message type and available entities, but the output is designed to preserve traceability across the pipeline.

A simplified conceptual example is shown below:

```json
{
  "audio_id": "audio_001",
  "user_id": "anonymous_user",
  "tipo": "incidencia",
  "fecha_recepcion": "YYYY-MM-DD",
  "transcripcion": "mensaje transcrito",
  "evento": {
    "cultivo": "cafe",
    "incidencia": "plaga",
    "tratamiento": "valor_normalizado"
  },
  "estado_procesamiento": "processed",
  "normalization_version": "v1.1"
}
```

---

## Compatibility Notes

During development, differences were observed between macOS environments using Intel processors and Apple Silicon, especially in dependencies related to audio processing, such as `pydub`, `ffmpeg` and `setuptools`.

These differences do not affect the pipeline design, but they may influence local execution. For this reason, it is recommended to:

- use a virtual environment;
- verify that `ffmpeg` is correctly installed;
- install dependencies from `requirements.txt`;
- avoid mixing environments or Python installations.

---

## Reproducibility

The project uses fixed random seeds where applicable to improve reproducibility across model training and evaluation steps.

However, small variations may still occur depending on:

- hardware architecture;
- operating system;
- Python and library versions;
- transformer model initialization;
- backend acceleration such as CUDA or Apple Silicon MPS.

These aspects should be considered when comparing exact training metrics across different machines.

---

## Data and Privacy

This repository is designed for methodological review and reproducibility of the pipeline structure. Depending on the public version of the repository, some real data files, raw audio recordings or executable notebooks may be excluded to protect privacy, reduce repository size and avoid unnecessary exposure of sensitive material.

The folder structure preserves the original workflow and expected locations for inputs and outputs.

---

## Academic Context

This project was developed as part of a Master’s thesis focused on the design, implementation and evaluation of a modular artificial intelligence system for transforming agricultural voice messages into structured information.

The application scope is limited to coffee and cacao crops in Latin American agricultural contexts.

---

## Limitations

- The pipeline is evaluated within a specific agricultural domain and language context.
- The system is not presented as a generic solution for all crops or regions.
- ASR errors may propagate to downstream NLP and normalization stages.
- Entity extraction performance depends on both model behavior and domain dictionary coverage.
- Semantic normalization requires curated domain mappings and may need extension for new use cases.

---

## Future Work

Potential extensions include:

- integration with a relational or vector-supported database;
- semantic search over structured agricultural records;
- dashboard-based visualization of field reports;
- retrieval-augmented generation over normalized records;
- farmer-facing alerts and recommendation systems;
- expansion to additional crops, regions or message types.

---

## License

This repository is provided for academic and demonstrative purposes. Add the appropriate license depending on the intended use and distribution policy.

---

## Author

**José Manuel Pinillos**  
Computer Engineer · Artificial Intelligence · Data and Digital Transformation
