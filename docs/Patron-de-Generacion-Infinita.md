# El Patrón de Generación Infinita

## **1. Propósito y Contexto**

El propósito de este patrón es generar automáticamente una serie de salidas (que pueden parecer infinitas) sin tener que volver a introducir el prompt generador cada vez. El objetivo es limitar la cantidad de texto que el usuario debe escribir para producir la siguiente salida, partiendo del supuesto de que el usuario no desea reintroducir continuamente el prompt. En algunas variaciones, la intención es permitir que el usuario mantenga una plantilla de prompt inicial, pero añadiendo una variación adicional a través de entradas complementarias antes de cada salida generada.

## **2. Motivación**

Muchas tareas requieren la aplicación repetitiva de un mismo prompt a múltiples conceptos. Por ejemplo, la generación de código para operaciones de creación, lectura, actualización y eliminación (CRUD) para un tipo específico de entidad puede requerir la aplicación del mismo prompt a múltiples tipos de entidades. Si se obliga al usuario a volver a escribir el prompt una y otra vez, este podría cometer errores. El patrón de Generación Infinita permite al usuario aplicar repetidamente un prompt, ya sea con o sin entrada adicional, para automatizar la generación de múltiples salidas utilizando un conjunto predefinido de restricciones.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Me gustaría que generaras salidas de forma indefinida, X salida(s) a la vez |
| (Opcional) así es como debes usar la entrada que proporcione entre las salidas |
| (Opcional) detente cuando te lo pida |

La primera declaración especifica que el usuario desea que el LLM genere salidas de forma indefinida, lo que comunica de manera efectiva la información de que el mismo prompt se va a reutilizar una y otra vez. Al especificar el número de salidas que deben generarse a la vez (es decir, “X salidas a la vez”), el usuario puede limitar la tasa de generación (*rate limit*), lo que puede ser particularmente importante si existe el riesgo de que la salida exceda las limitaciones de longitud del LLM para una sola respuesta.

La segunda declaración proporciona instrucciones opcionales sobre cómo utilizar la entrada proporcionada por el usuario entre las salidas. Al especificar cómo se pueden proporcionar y aprovechar las entradas adicionales del usuario entre los prompts, el usuario puede crear una estrategia de prompts que aproveche la retroalimentación en el contexto del prompt original. El prompt original sigue estando en el contexto de la generación, pero cada entrada del usuario entre los pasos de generación se incorpora al prompt original para refinar la salida utilizando reglas prescritas.

La tercera declaración proporciona una forma opcional para que el usuario detenga el proceso de generación de salida. Este paso no siempre es necesario, pero puede ser útil en situaciones donde exista la posibilidad de ambigüedad sobre si la entrada proporcionada por el usuario constituye un refinamiento para la siguiente generación o un comando para detenerse. Por ejemplo, se podría crear una frase de detención explícita si el usuario estuviera generando datos relacionados con señales de tráfico, donde el usuario podría querer introducir un refinamiento como “stop” (alto) para indicar que se debe añadir una señal de alto a la salida.

## **4. Implementación de Ejemplo**

El siguiente es un ejemplo de prompt de generación infinita para producir una serie de URLs:

> “De ahora en adelante, quiero que generes un nombre y un cargo hasta que yo diga basta. Voy a proporcionar una plantilla para tu salida. Todo lo que esté en mayúsculas sostenidas es un marcador de posición. Cada vez que generes texto, intenta ajustarlo en uno de los marcadores de posición que enumero. Por favor, conserva el formato y la plantilla general que proporciono: `https://myapi.com/NOMBRE/perfil/TRABAJO`”.

Este prompt combina la funcionalidad de los patrones de Generación Infinita y de Plantilla. El usuario solicita que el LLM genere continuamente un nombre y un cargo hasta que se le indique explícitamente “basta”. Las salidas generadas se formatean entonces en la plantilla proporcionada, que incluye marcadores de posición para el nombre y el cargo. Al utilizar el patrón de Generación Infinita, el usuario recibe múltiples salidas sin tener que volver a introducir la plantilla continuamente. Del mismo modo, se aplica el patrón de Plantilla para proporcionar un formato consistente para las salidas.

## **5. Consecuencias**

En los LLM conversacionales, la entrada al modelo en cada paso temporal es la salida anterior y la nueva entrada del usuario. Aunque los detalles de qué se conserva y se reintroduce en el siguiente ciclo de salida dependen del modelo y de la implementación, a menudo tienen un alcance limitado. Por lo tanto, el modelo recibe constantemente las salidas anteriores y el prompt, lo que puede dar lugar a que el modelo pierda el hilo de las instrucciones del prompt original con el tiempo si estas exceden el alcance de lo que se le proporciona como entrada.

A medida que se generan salidas adicionales, el contexto que rodea al prompt puede desvanecerse, lo que provoca que el modelo se desvíe del comportamiento previsto. Es importante supervisar las salidas producidas por el modelo para (1) asegurar que sigue cumpliendo con el comportamiento deseado y (2) proporcionar retroalimentación correctiva si es necesario. Otro problema a considerar es que el LLM puede generar salidas repetitivas, lo cual puede no ser deseado ya que los usuarios encuentran esta repetición tediosa y propensa a errores durante el procesamiento.
