# El Patrón persona

## **1. Propósito y Contexto**
En muchos casos, los usuarios desean que la salida del LLM adopte siempre un determinado punto de vista o perspectiva. Por ejemplo, puede ser útil realizar una revisión de código como si el LLM fuera un experto en seguridad. El propósito de este patrón es darle al LLM una “persona” que le ayude a seleccionar qué tipos de salida generar y en qué detalles enfocarse.

## **2. Motivación**
Es posible que los usuarios no sepan qué tipos de resultados o detalles son importantes para que un LLM se centre en lograr una tarea determinada. Sin embargo, pueden conocer el rol o el tipo de persona a la que normalmente pedirían ayuda para esas cosas. El patrón Persona permite a los usuarios expresar lo que necesitan ayuda sin conocer los detalles exactos de las salidas que requieren.

## **3. Estructura e Ideas Clave**
Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Actúa como la persona X |
| Proporciona las salidas que la persona X crearía |

La primera declaración transmite la idea de que el LLM debe actuar como una persona específica y proporcionar las salidas que dicha persona daría. Esta persona puede expresarse de diversas maneras, que van desde una descripción de un puesto de trabajo, un título, un personaje de ficción, una figura histórica, etc. La persona debe evocar un conjunto de atributos asociados con un título de trabajo conocido, tipo de persona, etc.$^2$.

La idea secundaria —proporcionar las salidas que la persona X crearía— ofrece oportunidades de personalización. Por ejemplo, un profesor podría proporcionar una gran variedad de tipos de salida diferentes, que van desde tareas hasta listas de lectura o conferencias. Si se conoce un alcance más específico para el tipo de salida, el usuario puede proporcionarlo en esta declaración.

## **4. Implementación de Ejemplo**
A continuación se muestra una implementación de ejemplo para una revisión de código:

> “De ahora en adelante, actúa como un revisor de seguridad. Presta mucha atención a los detalles de seguridad de cualquier código que miremos. Proporciona las salidas que un revisor de seguridad daría con respecto al código”.

En este ejemplo, se instruye al LLM para que proporcione las salidas que daría un “revisor de seguridad”. El prompt establece además el escenario de que el código va a ser evaluado. Finalmente, el usuario refina la persona delimitando la persona aún más a salidas relacionadas con el código.

Las personas también pueden representar entidades inanimadas o no humanas, como una terminal de Linux, una base de datos o la perspectiva de un animal. Cuando se utiliza este patrón para representar estas entidades, puede ser útil especificar también cómo se desea que las entradas se entreguen a la entidad, como por ejemplo “asume que mi entrada es lo que el dueño le dice al perro y tu salida son los sonidos que hace el perro”. A continuación se muestra un ejemplo de prompt para una entidad no humana que utiliza una redacción de “fingir ser”:

> “Vas a fingir ser una terminal de Linux para una computadora que ha sido comprometida por un atacante. Cuando escriba un comando, vas a generar el texto correspondiente que produciría la terminal de Linux”.

Este prompt está diseñado para simular una computadora que ha sido comprometida por un atacante y que está siendo controlada a través de una terminal de Linux. El prompt especifica que el usuario introducirá comandos en la terminal y, en respuesta, la terminal simulada generará el texto correspondiente que produciría una terminal de Linux real. Este prompt es más prescriptivo en la persona y pide al LLM no solo ser una terminal de Linux, sino actuar además como una computadora que ha sido comprometida por un atacante.

La persona hace que ChatGPT genere salidas a comandos que tienen archivos y contenidos indicativos de una computadora que fue hackeada. El ejemplo ilustra cómo un LLM puede aportar su conciencia situacional a una persona, en este caso, creando evidencia de un ciberataque en las salidas que genera. Este tipo de persona puede ser muy eficaz para combinarse con el patrón de Juego (*Game Play*), donde se desea que los detalles exactos de las características de la salida se oculten al usuario (por ejemplo, no revelar lo que hizo el ciberataque describiéndolo explícitamente en el prompt).

## **5. Consecuencias**
Un aspecto interesante de adoptar personas no humanas es que el LLM puede hacer suposiciones interesantes o “alucinaciones” con respecto al contexto. Un ejemplo ampliamente difundido en Internet pide a ChatGPT que actúe como una terminal de Linux y produzca la salida esperada que se obtendría si el usuario escribiera el mismo texto en una terminal. Comandos como `ls -l` generarán un listado de archivos para un sistema de archivos UNIX imaginario, completo con archivos sobre los que se puede ejecutar `cat archivo1.txt`.

En otros ejemplos, el LLM puede pedir al usuario más contexto, como cuando se le pide a ChatGPT que actúe como una base de datos MySQL y solicita la estructura de una tabla que el usuario está fingiendo consultar. ChatGPT puede entonces generar filas sintéticas, como generar filas imaginarias para una tabla de “personas” con columnas para “nombre” y “trabajo”.

---
*Tenga en cuenta, sin embargo, que las personas relacionadas con personas vivas o personas consideradas dañinas pueden ser ignoradas debido a las reglas subyacentes de privacidad y seguridad del LLM.*
