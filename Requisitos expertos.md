# Requisitos de datos y definiciones para el desarrollo del sistema

Para avanzar en las siguientes fases del proyecto, es necesario disponer de un conjunto de datos y definiciones que permitan desarrollar, entrenar y evaluar los distintos módulos del sistema, garantizando la calidad del entrenamiento, la consistencia de los datos, la validez de la evaluación y la utilidad final de la información generada.

El sistema propuesto sigue el siguiente flujo:



<center><strong>Audio → Preprocesamiento → ASR → Texto → Clasificación → NER → Normalización → Datos estructurados</strong></center>



Este documento describe de forma detallada la información necesaria en cada una de estas etapas. Se recomienda validar los elementos definidos en este documento antes de iniciar la siguiente fase de desarrollo, con el fin de garantizar la coherencia del dataset y la validez de la evaluación experimental.



## Requisitos para el módulo ASR

El módulo de reconocimiento automático del habla (ASR) tiene como objetivo convertir los audios en texto y evaluar la calidad de dicha transcripción.

Para ello, se requiere:

- Audios reales del dominio.
- Cada audio debe estar acompañado de una **transcripción manual fiel**, imprescindible para calcular la métrica *Word Error Rate (WER)*.



### Requisitos de la transcripción:

- Debe ser **literal**, sin corregir ni resumir el contenido.
- Debe reflejar el lenguaje real utilizado por el hablante.
- Debe entregarse en un formato simple (TXT o CSV).
- Debe existir una correspondencia clara entre audio y transcripción (relación 1:1).



### Requisitos del conjunto:

- Debe ser representativo del contexto real de uso.
- Debe incluir variedad de hablantes, acentos y condiciones de grabación.

<div style="page-break-after: always; break-after: page;"></div>

## Requisitos para el módulo de clasificación

El módulo de clasificación tiene como objetivo categorizar cada mensaje en función de su contenido.



### Definición del problema

Se solicita confirmar si el problema será:

- Binario (recomendado):
  - `registro_inicial`
  - `entrada_datos`
- Multiclase (en caso de ser necesario, definir clases adicionales)



### Requisitos del dataset

- Mínimo **100 audios por clase**.
- En caso de clasificación binaria, aproximadamente **200 audios en total**.
- Se recomienda que el dataset esté balanceado entre clases.

Dado el volumen limitado de datos, se opta por un enfoque de ajuste ligero (*fine-tuning*) sobre modelos preentrenados, complementado con técnicas de *data augmentation* para mejorar la capacidad de generalización.



### Etiquetado requerido

- Cada audio debe incluir su **clase asignada por expertos**.
- No se contemplan casos ambiguos: cada audio debe pertenecer a una única clase.



### Formato recomendado

```csv
audio_id,transcripcion,clase
AUDIO_001,"Me llamo Juan y tengo una finca de café",registro_inicial
AUDIO_002,"Ayer fumigué porque vi roya en el cultivo",entrada_datos
```

> [!NOTE]
>
> - Se utiliza `,` como separador de columnas.
> - Las transcripciones deben ir entre comillas dobles `" "` para garantizar la correcta lectura del fichero.
> - El texto debe ser plano y no debe incluir comillas internas (`"`).
> - Se permite únicamente el uso de signos de puntuación básicos como `.`, `,` o `;`.
> - Evitar saltos de línea dentro de una misma transcripción.
> - Se recomienda codificación UTF-8.

<div style="page-break-after: always; break-after: page;"></div>

## Requisitos para el módulo de extracción de entidades (NER)

El módulo NER tiene como objetivo identificar información relevante dentro del texto.



### Definición de entidades

Se requiere la definición de una lista definitiva de entidades a extraer (por ejemplo, agricultor, cultivo, plaga, producto, evento, fecha, cantidad o ubicación), que deberá ser validada por expertos del dominio.



### Información requerida

- Ejemplos de textos reales con entidades identificadas y validadas por expertos.
- Criterios de anotación:
  - cómo marcar fechas
  - cómo marcar cantidades
  - cómo marcar nombres propios
  - cómo marcar ubicaciones

Las entidades deberán definirse de forma precisa, indicando qué casos se incluyen y cuáles se excluyen, con el objetivo de garantizar consistencia durante el proceso de anotación.



### Identificación de términos clave

Se solicita identificar términos relevantes del dominio, especialmente:

- plagas
- cultivos
- productos



### Formato recomendado para anotación

```json
{
  "text": "Ayer fumigué el café",
  "entities": [
    {"start": 0, "end": 4, "label": "fecha_evento"},
    {"start": 5, "end": 12, "label": "accion"},
    {"start": 16, "end": 20, "label": "cultivo"}
  ]
}
```

<div style="page-break-after: always; break-after: page;"></div>

## Requisitos para la normalización

El objetivo de esta fase es unificar distintas formas de expresar el mismo concepto.



### Información requerida

- Diccionarios de sinónimos y variantes regionales para:
  - cultivos
  - plagas
  - productos
  - eventos
- Definición de una **forma estándar (canónica)** para cada concepto.
- Inclusión de términos coloquiales o variantes locales dentro de los diccionarios, de forma que todas las expresiones equivalentes se unifiquen bajo una misma representación estándar.



### Formato recomendado

```csv
categoria,variante,forma_estandar
cultivo,elote,maiz
cultivo,choclo,maiz
cultivo,cafeto,cafe
plaga,bicho,plaga_no_especificada
producto,veneno,pesticida
evento,fumigar,aplicacion_producto
evento,echar veneno,aplicacion_producto
```

<div style="page-break-after: always; break-after: page;"></div>

## Definición funcional del sistema

Para alinear el desarrollo con las necesidades reales, se requiere definir:

- Qué datos se desean obtener como salida estructurada final del sistema.
- Qué campos son **obligatorios** y cuáles son **opcionales**.



### Formato recomendado

```csv
campo,tipo,obligatorio,descripcion
agricultor,string,si,Nombre del agricultor
cultivo,string,si,Cultivo afectado
plaga,string,no,Plaga detectada
producto,string,no,Producto aplicado
evento,string,si,Acción realizada
fecha,string,no,Fecha del evento
cantidad,string,no,Cantidad aplicada
ubicacion,string,no,Lugar dentro de la finca
```



Esta definición permitirá validar que la salida del pipeline cumple con los requisitos funcionales del sistema y facilita su posterior integración en sistemas de almacenamiento o análisis.
