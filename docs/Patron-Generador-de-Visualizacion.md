# El Patrón Generador de Visualización

## **1. Propósito y Contexto**

El propósito de este patrón es utilizar la generación de texto para crear visualizaciones. Muchos conceptos son más fáciles de asimilar en formato de diagrama o imagen. El objetivo de este patrón es crear una vía para que una herramienta produzca imágenes asociadas con otras salidas. Este patrón permite la creación de visualizaciones mediante la generación de entradas para otras herramientas de visualización bien conocidas que utilizan texto como entrada, tales como Graphviz Dot [15] o DALL-E [13]. Este patrón puede proporcionar una forma más completa y eficaz de comunicar información al combinar las fortalezas tanto de la generación de texto como de las herramientas de visualización.

## **2. Motivación**

Los LLMs generalmente producen texto y no pueden producir imágenes. Por ejemplo, un LLM no puede dibujar un diagrama para describir un grafo. El patrón Generador de Visualización supera esta limitación generando entradas textuales en el formato correcto para conectarlas (*plug into*) a otra herramienta que genere el diagrama correspondiente. La motivación detrás de este patrón es mejorar la salida del LLM y hacerla más atractiva visualmente y más fácil de entender para los usuarios. Al utilizar entradas de texto para generar visualizaciones, los usuarios pueden comprender rápidamente conceptos y relaciones complejas que podrían ser difíciles de captar únicamente a través del texto.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Genera un X que pueda proporcionar a la herramienta Y para visualizarlo |

El objetivo de las declaraciones contextuales es indicar al LLM que la salida que va a producir, “X”, se convertirá en imágenes. Dado que los LLMs no pueden generar imágenes, la aclaración “que pueda proporcionar a la herramienta Y para visualizarlo” especifica que no se espera que el LLM genere una imagen, sino que se espera que produzca una descripción de imágenes consumible por la herramienta Y para la producción de la imagen.

Muchas herramientas pueden admitir múltiples tipos de visualizaciones o formatos y, por lo tanto, la herramienta de destino en sí misma puede no ser información suficiente para producir con precisión lo que el usuario desea. Es posible que el usuario deba indicar los tipos precisos de visualizaciones (por ejemplo, gráfico de barras, grafo dirigido, diagrama de clases UML) que deben producirse. Por ejemplo, Graphviz Dot puede crear diagramas tanto para diagramas de clases UML como para grafos dirigidos. Además, como se discutirá en el siguiente ejemplo, puede ser ventajoso especificar una lista de posibles herramientas y formatos y dejar que el LLM seleccione el objetivo apropiado para la visualización.

## **4. Implementación de Ejemplo**

> “Cada vez que te pida visualizar algo, por favor crea un archivo de Graphviz Dot o un prompt de DALL-E que pueda usar para crear la visualización. Elige las herramientas apropiadas basándote en lo que necesite ser visualizado”.

Este ejemplo del patrón añade una calificación de que el tipo de salida para la visualización puede ser para Graphviz o para DALL-E. Lo interesante de este enfoque es que permite al LLM utilizar su comprensión semántica del formato de salida para seleccionar automáticamente la herramienta de destino basándose en lo que se mostrará. En este caso, Graphviz sería para visualizar grafos con necesidad de una estructura exactamente definida. DALL-E sería eficaz para visualizar imágenes realistas o artísticas que no tienen una estructura exactamente definida. El LLM puede seleccionar la herramienta basándose en las necesidades de la visualización y las capacidades de cada herramienta.

## **5. Consecuencias**

El patrón crea un pipeline de destino para que la salida renderice una visualización. El pipeline puede incluir generadores de IA, como DALL-E, que pueden producir visualizaciones ricas. El patrón permite al usuario expandir las capacidades expresivas de la salida hacia el dominio visual.
