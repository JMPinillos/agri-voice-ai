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


### **Nota sobre la evolución del catálogo de entidades y reglas de normalización**

El esquema de entidades y las reglas de normalización definidos en esta fase deben entenderse como una versión inicial y extensible del módulo. Aunque permiten estructurar la información principal extraída de los mensajes agrícolas, su despliegue en un entorno productivo requerirá una revisión progresiva junto con expertos de dominio.

En particular, será necesario validar y ampliar el catálogo de términos relacionados con cultivos, variedades, plagas, enfermedades, tratamientos, productos fitosanitarios, unidades de medida, espacios agrícolas y estados del cultivo. Esta revisión permitirá incorporar variantes regionales, expresiones propias de los productores y términos técnicos específicos que puedan no estar suficientemente representados en el conjunto de datos inicial.

Asimismo, las entidades asociadas a magnitudes deberán refinarse de forma progresiva. En esta versión, valores como cantidades, superficies, masas, volúmenes, distancias o duraciones pueden tratarse mediante reglas de normalización basadas en unidades detectadas en el texto. Sin embargo, en fases posteriores será conveniente revisar si estas categorías deben mantenerse como entidades independientes del modelo NER o si resulta más robusto detectarlas mediante reglas específicas dentro del módulo de normalización.

También será necesario ajustar el mapeo semántico de acciones agrícolas. Expresiones como “recoger”, “cosechar”, “fumigar”, “aplicar producto”, “limpiar el lote”, “hacer deshierbe” o “revisar plantas” pueden presentar variabilidad lingüística y diferencias de uso según el país o el contexto técnico. Por ello, el catálogo de acciones canónicas deberá validarse con expertos para evitar agrupaciones incorrectas o pérdidas de significado.

Finalmente, la evolución del sistema deberá contemplar mecanismos de revisión de casos no resueltos, entidades no normalizadas y valores ambiguos. Estos casos permitirán retroalimentar el catálogo de dominio, mejorar las reglas de normalización y, si fuera necesario, ampliar el esquema de anotación del modelo NER en futuras iteraciones.