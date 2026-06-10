Lo replantearía así, porque durante la conversación hemos separado claramente qué pertenece al **Notebook 3 (NER y dominio)** y qué pertenece al **Notebook 4 (normalización y estructuración)**.

# **Notebook 3 – NER y conocimiento de dominio**

## **Objetivo**

Identificar entidades relevantes dentro de los mensajes agrícolas mediante una combinación de:

- Fine-tuning de spaCy.
- Refuerzo mediante diccionario de dominio.
- Detección de sinónimos y expresiones propias del sector agrícola.



## **Aspectos a validar con expertos**

### **Cultivos**

Determinar los nombres y sinónimos utilizados habitualmente para cada cultivo.

Ejemplos:

- café
- cafeto
- cafetal
- grano
- cereza
- cacao
- cacaotero
- cacaotal
- pepa



### **Plagas y enfermedades**

Identificar las principales enfermedades y formas coloquiales de referirse a ellas.

Ejemplos:

- roya
- broca
- monilia
- escoba de bruja
- ojo de gallo
- antracnosis
- phytophthora



### **Productos fitosanitarios**

Validar nombres técnicos y nombres coloquiales.

Ejemplos:

- fungicida
- insecticida
- herbicida
- fertilizante
- abono
- remedio
- medicina



### **Eventos agrícolas**

Determinar acciones habituales reportadas por los agricultores.

Ejemplos:

- siembra
- cosecha
- riego
- fumigación
- poda
- deshierbe
- abonado



### **Estados del cultivo**

Ejemplos:

- floración
- llenado
- maduración
- marchitez
- amarillamiento



### **Espacios agrícolas**

Ejemplos:

- finca
- lote
- parcela
- hacienda
- vivero



### **Condiciones climáticas**

Ejemplos:

- lluvia
- sequía
- humedad
- viento



### **Otras entidades de interés**

Preguntar explícitamente a los expertos si consideran relevante detectar:

- partes de la planta
- tipos de suelo
- herramientas o maquinaria
- variedades específicas de café o cacao



## **Entidades NER propuestas**

```json
{
  "entities": [
    "cultivo",
    "plaga_enfermedad",
    "producto_fitosanitario",
    "evento_agricola",
    "estado_cultivo",
    "espacio_agricola",
    "condicion_climatica",
    "fecha_evento"
  ]
}
```

Estas entidades serán las utilizadas durante el entrenamiento de spaCy y reforzadas mediante el diccionario de dominio.



# **Notebook 4 – Normalización y estructuración**

## **Objetivo**

Transformar la información detectada por el NER en datos estructurados y normalizados.



## **Aspectos a validar con expertos**

### **Fechas relativas**

Ejemplos:

- ayer
- anteayer
- hace tres días
- la semana pasada
- el otro día

Preguntar:

- ¿Cómo tratar expresiones ambiguas?
- ¿Debe utilizarse la fecha de la nota de voz como referencia?

Recomendación:

Convertir a fecha absoluta cuando sea posible.



### **Volumen**

Ejemplos:

- litros
- mililitros
- galones

Recomendación:

Normalizar a litros.



### **Superficie**

Ejemplos:

- hectáreas
- metros cuadrados
- manzanas
- cuadras

Recomendación:

Normalizar a hectáreas.



### **Masa**

Ejemplos:

- kilos
- gramos
- libras
- toneladas

Recomendación:

Normalizar a kilogramos.



### **Duración**

Ejemplos:

- días
- semanas
- meses

Recomendación:

Normalizar a días.



### **Cantidades ausentes**

Ejemplo:

```text
Apliqué fungicida en el café
```

No aparece la cantidad aplicada.

Recomendación:

```json
{
  "producto_fitosanitario": "fungicida",
  "cantidad": null
}
```

Sin inferir valores.



## **Extracción cantidad-unidad**

Validar cómo interpretar expresiones como:

```text
15 litros
2 hectáreas
500 kilos
3 meses
```

Generando estructuras del tipo:

```json
{
  "tipo": "volumen",
  "valor": 15,
  "unidad_original": "litros"
}
{
  "tipo": "superficie",
  "valor": 2,
  "unidad_original": "hectáreas"
}
```



## **Diccionario de normalización propuesto**

```json
{
  "temporal": {
    "fecha_relativa": [
      "ayer",
      "anteayer",
      "hace tres días",
      "la semana pasada",
      "el otro día"
    ],
    "unidad_duracion": [
      "día",
      "días",
      "semana",
      "semanas",
      "mes",
      "meses"
    ]
  },
  "unidades": {
    "volumen": {
      "terminos": [
        "litro",
        "litros",
        "mililitro",
        "mililitros",
        "galón",
        "galones"
      ],
      "unidad_normalizada": "litros"
    },
    "superficie": {
      "terminos": [
        "hectárea",
        "hectáreas",
        "ha",
        "metro cuadrado",
        "metros cuadrados"
      ],
      "unidad_normalizada": "hectareas"
    },
    "masa": {
      "terminos": [
        "kilo",
        "kilos",
        "kg",
        "gramo",
        "gramos",
        "libra",
        "libras",
        "tonelada",
        "toneladas"
      ],
      "unidad_normalizada": "kilogramos"
    }
  }
}
```



## **Resultado esperado**

A partir de una frase como:

```text
Ayer apliqué 15 litros de fungicida en 2 hectáreas de café porque encontré roya.
```

obtener:

```json
{
  "fecha_evento": "2026-06-02",
  "evento_agricola": "fumigacion",
  "producto_fitosanitario": "fungicida",
  "volumen": 15,
  "superficie": 2,
  "cultivo": "cafe",
  "plaga_enfermedad": "roya"
}
```

Ese es el punto donde termina el Notebook 3 (detección de entidades) y comienza el Notebook 4 (normalización y estructuración).