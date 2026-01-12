# El Patrón de Generación Infinita

## **1. Propósito y Contexto**

La intención de este patrón es generar automáticamente una serie de resultados (que pueden parecer infinitos) sin tener que volver a introducir el prompt cada vez. El objetivo es reducir la cantidad de texto que el usuario debe escribir para obtener la siguiente salida, partiendo de la idea de que no quiere repetir constantemente la instrucción inicial. En algunas variaciones, la intención es permitir que el usuario conserve un prompt base o plantilla inicial, pero añada variaciones adicionales mediante entradas nuevas antes de cada resultado generado.

## **2. Motivación**

Muchas tareas requieren usar el mismo prompt varias veces, por ejemplo, al generar código para operaciones CRUD (crear, leer, actualizar y eliminar) de diferentes entidades, se necesita aplicar la misma instrucción repetidamente. Si el usuario tiene que escribir el prompt una y otra vez, es fácil que cometa errores. El patrón de Generación Infinita evita esto, ya que permite reutilizar el mismo prompt de manera automática, con o sin entradas adicionales, para producir múltiples resultados siguiendo ciertas reglas.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Me gustaría que generaras salidas de forma indefinida, X salida(s) a la vez |
| (Opcional) así es como debes usar la entrada que proporcione entre las salidas |
| (Opcional) detente cuando te lo pida |

La primera instrucción aclara que el usuario puede pedir al modelo (LLM) que genere resultados de manera indefinida, lo que implica que el mismo prompt se reutilizará continuamente. Para evitar que la salida sea demasiado extensa, el usuario puede indicar un límite, por ejemplo: ***genera X resultados a la vez***. Este control es crucial porque los modelos tienen restricciones de longitud en sus respuestas. Si se genera demasiado contenido de una sola vez, se corre el riesgo de superar esas limitaciones. Al establecer cuántos resultados se producen en cada ciclo, el usuario mantiene un flujo continuo de generación, pero con un ritmo manejable y seguro.

La segunda instrucción del patrón describe cómo el usuario puede dar entradas adicionales entre cada bloque de generación. Al definir cómo se incorporan esas entradas, el usuario crea una estrategia que aprovecha la retroalimentación para ajustar la siguiente salida sin perder el contexto del prompt original. El prompt inicial sigue siendo la base de la generación, pero cada nueva entrada del usuario se integra en él para refinar los resultados. La incorporación de estas entradas se hace siguiendo reglas claras, lo que asegura consistencia y control en la variación de las salidas.

La tercera declaración proporciona una forma opcional para que el usuario detenga el proceso de generación de salida. Este paso no siempre es necesario, pero puede ser útil en situaciones donde exista la posibilidad de ambigüedad sobre si la entrada proporcionada por el usuario constituye un refinamiento para la siguiente generación o un comando para detenerse. Por ejemplo si el usuario está generando datos sobre señales de tránsito y escribe “stop”, el sistema podría interpretarlo como:

* Un refinamiento (añadir una señal de “Stop” a la salida).
* O una orden para detener la generación.

Para evitar esa ambigüedad, se establece una frase clara que indique cuándo se debe detener el proceso.

## **4. Implementación de Ejemplo**

El siguiente es un ejemplo de prompt de generación infinita para producir una serie de URLs:

> “De ahora en adelante, quiero que generes un nombre y un cargo hasta que yo diga basta. Voy a proporcionar una plantilla para tu salida. Todo lo que esté en mayúsculas es un marcador de posición. Cada vez que generes texto, intenta colocarlo en uno de los marcadores de posición que enumero. Por favor, conserva el formato y la plantilla general que proporciono: `https://myapi.com/NOMBRE/perfil/TRABAJO`”.

Este prompt combina la funcionalidad del patrón de Generación Infinita con el patrón de Plantilla. El usuario pide al modelo que genere de manera continua un nombre y un cargo laboral hasta que se le indique explícitamente **basta**. Los resultados generados se formatean dentro de la plantilla proporcionada, la cual incluye espacios reservados para el nombre y el cargo. Gracias al patrón de Generación Infinita, el usuario recibe múltiples resultados sin tener que volver a introducir la plantilla cada vez. Al mismo tiempo, el patrón de Plantilla asegura que todos los resultados mantengan un formato consistente.

## **5. Consecuencias**

En cada paso, el modelo recibe la salida anterior y la nueva instrucción del usuario. Como el contexto que se conserva es limitado, con el tiempo puede perder de vista el prompt original. Esto puede hacer que el modelo se desvíe del comportamiento esperado o empiece a repetir respuestas. Por eso es importante que el usuario supervise las salidas y dé retroalimentación correctiva cuando sea necesario.
