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

El objetivo de las declaraciones contextuales es indicar al LLM que la salida que va a producir, **_X_**, se convertirá en imágenes. Dado que los LLMs no pueden generar imágenes, la aclaración "que pueda proporcionar a la herramienta **_Y_** para visualizarlo” especifica que no se espera que el LLM genere una imagen, sino que se espera que produzca una descripción de imágenes consumible por la herramienta Y para crear la imagen.

Muchas herramientas pueden admitir múltiples tipos de visualizaciones o formatos y, por lo tanto, la herramienta de destino en sí misma puede no ser información suficiente para producir con precisión lo que el usuario desea. Es posible que el usuario deba indicar los tipos precisos de visualizaciones (por ejemplo, gráfico de barras, grafo dirigido, diagrama de clases UML) que deben producirse. Por ejemplo, Graphviz Dot puede crear diagramas tanto para diagramas de clases UML como para grafos dirigidos. Además, como se discutirá en el siguiente ejemplo, puede ser ventajoso especificar una lista de posibles herramientas y formatos y dejar que el LLM seleccione el objetivo apropiado para la visualización.

## **4. Implementación de Ejemplo**

> “Cada vez que te pida visualizar algo, por favor crea un archivo de Graphviz Dot o un prompt de DALL-E que pueda usar para crear la visualización. Elige las herramientas apropiadas basándote en lo que necesite ser visualizado”.

Este enfoque permite que el LLM utilice su comprensión semántica para elegir automáticamente el formato de salida según el contexto. Graphviz se emplearía para estructuras definidas con precisión (como grafos), mientras que DALL-E sería ideal para representaciones artísticas o realistas que no requieren una estructura rígida.

## **5. Consecuencias**

El patrón establece un flujo de trabajo (_pipeline_) donde la salida del modelo se transforma en una visualización final. Este proceso puede integrar generadores de IA potentes, como DALL-E, para obtener resultados visualmente sofisticados. En última instancia, este patrón expande las capacidades expresivas del modelo hacia el terreno visual.

## **6. Plantilla**

```py title="PLANTILLA"
Genera [OBJETIVO] en formato [FORMATO] que pueda proporcionar a la herramienta [HERRAMIENTA/SITIO WEB] para visualizarlo como [NOMBRE DE LA GRÁFICA]. Por favor, no incluyas texto explicativo, dame solo solo la respuesta dentro de un bloque de código.
```

## **7. Ejemplos**

```py title="Mapa mental"
Genera un temario jerárquico sobre ASTRONOMÍA BÁSICA en formato Markdown que pueda proporcionar a la herramienta markmap.js.org para visualizarlo como mapa mental. Por favor, no incluyas texto explicativo, dame solo solo la respuesta dentro de un bloque de código.
```