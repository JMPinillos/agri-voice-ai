# AgriVoice AI

Transforming Agricultural Producers’ Voice Messages into Structured Data

## **Requisitos del sistema**

El proyecto requiere un entorno de ejecución con Python 3.x y la instalación de dependencias tanto a nivel de Python como de sistema.

### **Dependencias de sistema**

El procesamiento de archivos de audio comprimido (por ejemplo, `.m4a` o `.mp3`) requiere la disponibilidad de la herramienta externa `ffmpeg`. En ausencia de esta dependencia, el sistema limita su funcionamiento a formatos compatibles con `libsndfile` (como `.wav`).

#### Instalación en macOS

```bash
brew install ffmpeg
```

---

### **Consideraciones de compatibilidad**

Durante el desarrollo se observaron diferencias de comportamiento entre entornos macOS con distinta arquitectura (Intel vs Apple Silicon), especialmente en la gestión de dependencias relacionadas con el procesamiento de audio (como `pydub`, `ffmpeg` o `setuptools`).

Estas diferencias no afectan al diseño del pipeline, pero pueden influir en su ejecución local. Por este motivo, se recomienda:

* el uso de entornos virtuales (`venv`) para aislar dependencias
* la validación previa de la instalación de `ffmpeg`
* comprobar la correcta instalación de las librerías indicadas en `requirements.txt`

---

### **Instalación del entorno Python**

Una vez cumplidos los requisitos anteriores, se debe instalar el entorno de dependencias del proyecto mediante:

```bash
pip install -r requirements.txt
```

---

### Ajuste importante (crítica)

Hacer esto en el README global es correcto porque:

* afecta a todo el pipeline, no solo al notebook 1
* es una dependencia de sistema, no de código

---

Si lo dejas dentro de un notebook, el tribunal lo ignora. Aquí sí queda profesional.
