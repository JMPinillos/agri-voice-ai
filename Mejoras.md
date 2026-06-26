### **Revisión del esquema de anotación NER – Mejora de categorías semánticas**

Durante el desarrollo del sistema de extracción de entidades se ha identificado una limitación en el esquema de anotación utilizado para el entrenamiento del modelo NER.

#### **Problema detectado**

Actualmente, la categoría **“tratamiento”** agrupa tanto:

- Intervenciones agronómicas específicas (por ejemplo: *aplicar fungicida*, *fertilizar*)
- Acciones generales realizadas en el cultivo (por ejemplo: *recoger*, *deshierbar*, *limpiar*)

Esta agrupación introduce ambigüedad semántica, ya que ambas tipologías de acciones representan conceptos diferentes desde el punto de vista agronómico.

Como consecuencia, el modelo NER aprende a clasificar acciones generales como si fueran tratamientos, afectando a la precisión semántica de las entidades extraídas.

#### **Propuesta de mejora**

Se propone revisar el esquema de anotación y separar la categoría actual en al menos dos clases diferenciadas:

- **tratamiento**: acciones orientadas a la aplicación de productos o intervenciones técnicas (fungicidas, fertilizantes, etc.)
- **acción_agricola** (o denominación equivalente): acciones generales de manejo del cultivo (recolección, deshierbe, limpieza, etc.)

#### **Impacto esperado**

- Mejora en la precisión semántica de las entidades
- Reducción de ambigüedades en la interpretación de resultados
- Mayor calidad de los datos estructurados generados

#### **Plan de actuación**

1. Revisión del esquema de etiquetas por parte de expertos en dominio agrícola
2. Actualización del dataset de entrenamiento con la nueva categorización
3. Reentrenamiento del modelo NER con las nuevas etiquetas
4. Reevaluación del sistema para medir la mejora obtenida

#### **Observaciones**

Este ajuste no requiere modificaciones en la arquitectura del sistema ni en el pipeline implementado, sino únicamente en la definición y anotación de las entidades, lo que facilita su integración en futuras iteraciones del proyecto.
