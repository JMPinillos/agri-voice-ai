### Figura 1 — Arquitectura interna del pipeline de audio

**Ubicación:** 4.1.1 Organización general del notebook

Prompt:

```text
Crea un diagrama profesional y minimalista en estilo académico mostrando la arquitectura de un pipeline de procesamiento de audio para sistemas ASR. Diseño horizontal con cajas rectangulares conectadas mediante flechas. Fondo blanco, líneas limpias, colores suaves y modernos (azules y grises), tipografía profesional sans-serif.

El flujo debe contener los siguientes bloques en este orden:

Raw Audio
↓
Exploración inicial
↓
Estandarización
↓
Cálculo de métricas acústicas
↓
Generación de flags
↓
Procesamiento adaptativo

Dentro del bloque “Procesamiento adaptativo”, incluir subbloques:
- High-pass
- Denoise
- RMS normalization
- Trim + Padding
- VAD

Después:
↓
Reconstrucción final
↓
Processed Audio

Aspecto técnico, limpio y propio de una publicación científica o TFM de inteligencia artificial. Relación horizontal panorámica.
```

---

### Figura 2 — Comparación señal original vs señal procesada

**Ubicación:** 4.1.5 Evaluación de técnicas de preprocesamiento

Prompt:

```text
Crea una figura académica comparativa de procesamiento de audio para un TFM de inteligencia artificial. Mostrar dos waveforms alineados verticalmente sobre fondo blanco.

Parte superior:
Título pequeño: “Audio original”
Waveform irregular con silencios prolongados y amplitud variable.

Parte inferior:
Título pequeño: “Audio procesado”
Waveform más limpia y compacta, con silencios reducidos y señal más uniforme.

Mantener misma escala temporal en ambas señales. Estilo técnico y minimalista, similar a figuras de artículos científicos de procesamiento de señal. Colores suaves (azul oscuro y gris). Sin elementos decorativos.
```

---

### Figura 3 — Funcionamiento del VAD

**Ubicación:** 4.1.7 Implementación del VAD

Prompt:

```text
Genera una figura técnica y profesional para explicar el funcionamiento de un sistema Voice Activity Detection (VAD) en un pipeline ASR.

Mostrar una waveform horizontal sobre fondo blanco con segmentos de voz resaltados en azul y regiones de silencio en gris claro.

Añadir pequeñas etiquetas discretas:
- Voice segment
- Silence removed

Incluir debajo una segunda waveform reconstruida tras el VAD, más compacta y continua.

Estilo académico y minimalista, similar a publicaciones científicas de procesamiento de audio y machine learning. Diseño limpio, profesional y fácil de interpretar.
```

---

### Figura 4 — Lógica adaptativa del pipeline

**Ubicación:** 4.1.6 Diseño del pipeline adaptativo

Prompt:

```text
Crea un diagrama de flujo profesional y minimalista que represente la lógica adaptativa de un pipeline de procesamiento de audio para ASR.

Fondo blanco, estilo académico, cajas rectangulares limpias y flechas simples.

Flujo lógico:

Inicio
↓
Cálculo de métricas acústicas
↓
¿High silence?
→ Sí → Aplicar VAD
→ No → Continuar

¿Low energy?
→ Sí → RMS normalization

¿High ZCR?
→ Sí → Denoise

¿High silence edges?
→ Sí → Trim + Padding

¿High energy variance?
→ Sí → Skip processing

↓
Guardar audio procesado

Diseño elegante, moderno y técnico, propio de un TFM o artículo científico de inteligencia artificial y procesamiento de señal.
```


Título del Notebook 1

Análisis y procesamiento de audio para sistemas ASR
Archivo: audio_preprocessing.ipynb

⸻

Estructura real del Notebook 1


1. Carga y exploración inicial del dataset
    * Identificación de formatos de entrada
    * Verificación de integridad de archivos
    * Análisis básico de distribución (duración, frecuencia de muestreo, canales)
2. Análisis del audio original (pre-estandarización)
    * Evaluación de heterogeneidad del dataset:
        * formatos (.m4a, .mp3, etc.)
        * frecuencias de muestreo
        * número de canales
    * Identificación de problemas iniciales:
        * audios muy cortos/largos
        * posibles inconsistencias de calidad
    * Justificación de la necesidad de estandarización
3. Estandarización de audios
    * Conversión a .wav, mono, 16 kHz
    * Normalización básica de rango
    * Persistencia en disco (standardized_audio)
4. Análisis de calidad post-estandarización (baseline)
    * Cálculo sistemático de métricas acústicas:
        * RMS
        * duración
        * proporción de silencio
        * silencio en extremos
        * ZCR
        * varianza de energía
    * Análisis estadístico del conjunto:
        * distribuciones (histogramas)
        * percentiles (P10, P90, etc.)
        * detección de outliers
    * Visualización de señales representativas
    * Definición del comportamiento baseline (referencia sin procesamiento adicional)
5. Evaluación de técnicas de preprocesamiento
    * Trimming y padding
    * Filtrado paso alto
    * Reducción de ruido
    * Normalización RMS
    * VAD (energía vs modelo)
    * Evaluación:
        * cuantitativa (métricas)
        * visual (señal)
        * cualitativa (escucha)
6. Comparación de resultados
    * Análisis del impacto de cada técnica
    * Identificación de efectos negativos (artefactos, pérdida de información)
    * Selección de configuraciones óptimas
7. Implementación del pipeline final
    * Integración de técnicas seleccionadas
    * Definición de lógica adaptativa basada en métricas
8. Validación del pipeline
    * Verificación de coherencia entre flags y transformaciones
    * Comparación señal original vs procesada
    * Control de cambios y trazabilidad
    ⸻

Qué hace exactamente el pipeline

1. Conversión a formato estándar
2. Cálculo de métricas acústicas
3. Generación de flags de decisión
4. Aplicación condicional de técnicas:
    * High-pass
    * Denoise
    * RMS normalization
    * Trim + padding
    * VAD
5. Reconstrucción final (si aplica VAD)
6. Guardado de audios procesados

Orden:

Estandarización → Métricas → Flags → Procesamiento adaptativo → Guardado

⸻

Formatos de entrada y salida

Entrada: .m4a, .mp3, .wav, .flac, .ogg
Salida: .wav, mono, 16 kHz

Estructura:

* data/raw_audio/
* data/standardized_audio/
* data/processed_audio/

⸻

Métricas acústicas usadas

* Energía RMS
* Duración (segundos)
* Proporción de silencio global
* Silencio en extremos
* ZCR (Zero Crossing Rate)
* Varianza de energía
* Clipping (en análisis posteriores)

⸻

Lógica adaptativa

Se basa en percentiles + umbrales absolutos:

* Normalización RMS
    * low_energy = True
    * sin ruido alto (high_zcr = False)
* Reducción de ruido
    * high_zcr = True
    * energía suficiente
* High-pass
    * aplicado por defecto salvo alta variabilidad energética
* Trim + padding
    * high_silence_edges = True
    * no VAD
* VAD
    * high_silence = True
    * duración > 30 s
* Skip processing
    * high_energy_var = True

⸻

VAD

* Modelo final: Silero VAD (PyTorch)
* Alternativa evaluada: librosa.effects.split (descartada)

Cuándo se aplica:

* Audios largos (>30 s)
* Alta proporción de silencio

Problema que resuelve:

* Eliminación de silencios internos sin fragmentar el discurso
* Mejora frente a métodos basados en energía (menos cortes y pérdida de información)

⸻

Validaciones finales

* Comparación señal original vs procesada:
    * Igualdad de duración
    * Igualdad de señal (np.allclose)
* Verificación de coherencia con flags:
    * Audios no procesados → sin cambios
    * Audios procesados → modificados
* Muestreo aleatorio reproducible (random_state=42)
* Resumen de decisiones del pipeline

⸻

Decisión final clave

No se asume que el audio procesado sea siempre mejor.

Se comparan:

* Audios estandarizados (baseline)
* Audios procesados

Criterio final:

Se selecciona la versión (estandarizada o procesada) que proporcione mejor rendimiento en ASR (WER), evitando sobreprocesamiento cuando no aporta 
