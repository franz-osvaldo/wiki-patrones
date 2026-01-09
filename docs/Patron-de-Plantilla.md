# El Patrón de Plantilla (*Template Pattern*)

## **1. Propósito y Contexto**

El propósito de este patrón es asegurar que la salida de un LLM siga una plantilla precisa en términos de estructura. Por ejemplo, el usuario podría necesitar generar una URL que inserte información generada en posiciones específicas dentro de la ruta de la URL. Este patrón permite al usuario instruir al LLM para que produzca su salida en un formato que normalmente no utilizaría para el tipo de contenido específico que se está generando.

## **2. Motivación**

En algunos casos, la salida debe producirse en un formato preciso que es específico de la aplicación o del caso de uso y que el LLM desconoce. Dado que el LLM no es consciente de la estructura de la plantilla, se le debe instruir sobre cuál es el formato y dónde deben ir las diferentes partes de su salida. Esto podría tomar la forma de una estructura de datos de muestra que se está generando, una serie de cartas modelo que se están completando, etc.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Voy a proporcionar una plantilla para tu salida |
| X es mi marcador de posición (*placeholder*) para el contenido |
| Intenta ajustar la salida en uno o más de los marcadores de posición que enumero |
| Por favor, conserva el formato y la plantilla general que proporciono |
| Esta es la plantilla: [PATRÓN con MARCADORES DE POSICIÓN] |

La primera declaración ordena al LLM que siga una plantilla específica para su salida. La plantilla se utilizará para intentar forzar las respuestas del LLM hacia una estructura que sea consistente con las necesidades de formato del usuario. Este patrón es necesario cuando el formato de destino es desconocido para el LLM. Si el LLM ya tiene conocimiento del formato, como un tipo de archivo específico, entonces el patrón de plantilla puede omitirse y el usuario puede simplemente especificar el formato conocido. Sin embargo, puede haber casos, como la generación de *Javascript Object Notation* (JSON), donde exista una gran cantidad de variaciones en cómo podrían representarse los datos dentro de ese formato, y la plantilla puede usarse para asegurar que la representación dentro del formato de destino cumpla con las restricciones adicionales del usuario.

La segunda declaración hace que el LLM sea consciente de que la plantilla contendrá un conjunto de marcadores de posición. Los usuarios explicarán cómo debe insertarse la salida en la plantilla a través de estos marcadores. Los marcadores de posición permiten al usuario dirigir semánticamente dónde debe insertarse la información. Los marcadores de posición pueden usar formatos, como NOMBRE, que permitan al LLM inferir el significado semántico para determinar dónde debe insertarse la salida (por ejemplo, insertar el nombre de la persona en el marcador NOMBRE). Además, al usar marcadores de posición, el usuario puede indicar qué no es necesario en la salida: si no existe un marcador de posición para un componente de la salida generada, entonces ese componente puede omitirse. Idealmente, los marcadores de posición deberían usar un formato que se emplee comúnmente en el texto con el que se entrenó al LLM, como mayúsculas sostenidas, encerrado entre corchetes, etc.

La tercera declaración intenta restringir al LLM para que no reescriba arbitrariamente la plantilla ni intente modificarla de modo que no se puedan insertar todos los componentes de la salida. Cabe señalar que esta declaración puede no excluir la generación de texto adicional antes o después. En la práctica, los LLM suelen seguir la plantilla, pero es más difícil eliminar cualquier texto adicional generado más allá de la plantilla sin experimentar con la redacción del prompt.

## **4. Implementación de Ejemplo**

A continuación se muestra una plantilla de ejemplo para generar URLs donde la salida se coloca en lugares específicos de la plantilla:

> “Voy a proporcionar una plantilla para tu salida. Todo lo que esté en mayúsculas sostenidas es un marcador de posición. Cada vez que generes texto, intenta ajustarlo en uno de los marcadores de posición que enumero. Por favor, conserva el formato y la plantilla general que proporciono en `https://myapi.com/NOMBRE/perfil/TRABAJO`”.

A continuación se muestra una interacción de ejemplo después de proporcionar el prompt:

> **Usuario:** “Genera un nombre y un cargo para una persona”.
> **ChatGPT:** `https://myapi.com/Emily_Parker/perfil/Software_Engineer`

## **5. Consecuencias**

Una consecuencia de aplicar el patrón de Plantilla es que filtra la salida del LLM, lo que puede eliminar otras salidas que el LLM habría proporcionado y que podrían ser útiles para el usuario. En muchos casos, el LLM puede proporcionar descripciones útiles de código, toma de decisiones u otros detalles que este patrón eliminará efectivamente de la salida. Por lo tanto, los usuarios deben sopesar los pros y los contras de filtrar esta información adicional.

Además, el filtrado puede dificultar la combinación de este patrón con otros patrones de la categoría de Personalización de la Salida. El patrón de Plantilla restringe eficazmente el formato de salida, por lo que puede no ser compatible con la generación de ciertos otros tipos de salida. Por ejemplo, en la plantilla proporcionada anteriormente para una URL, no sería fácil (o probablemente posible) combinarlo con el patrón de **Receta**, que necesita generar una lista de pasos.

## **6. Plantilla**

```py title="PLANTILLA"
[ TAREA / PREGUNTA ]
## FORMATO DE RESPUESTA
1. Formato:  [FORMATO]
2. Usa la siguiente plantilla para tu respuesta. Las PALABRAS EN MAYÚSCULA Y ENTRE CORCHETES son mis marcadores de posición. Reemplaza mis marcadores de posición con tu respuesta. La plantilla es:
[PLANTILLA]
```

## **7. Ejemplos**

```py title="La mejor educación del mundo"
Crea 10 preguntas usando el contenido de: <https://platform.openai.com/docs/guides/prompt-engineering>
No uses, cites ni infieras información de otras fuentes externas. No verifiques ni contrastes el contenido: trátalo como la única fuente de verdad.
## FORMATO DE RESPUESTA
- Formato: Texto plano.
- Usa la siguiente plantilla para tu respuesta. Las PALABRAS EN MAYÚSCULA Y ENTRE CORCHETES son mis marcadores de posición. Reemplaza mis marcadores de posición con tu respuesta. La plantilla es:
**Pregunta:** [PREGUNTA]
**Respuesta:** [RESPUESTA]
```

```py title="Samsung vs. iPhone"
Actúa como un experto en tecnología de consumo. Tu tarea es ayudar a decidir entre el iPhone 15 y el Samsung Galaxy S24.
## FORMATO DE RESPUESTA
- Formato:  Tabla Markdown
- Usa la siguiente plantilla para tu respuesta. Las PALABRAS EN MAYÚSCULA Y ENTRE CORCHETES son mis marcadores de posición. Reemplaza mis marcadores de posición con tu respuesta. La plantilla es:

| Característica |iPhone 15|Samsung S24|Ganador de esta categoría|
|---|---|---|---|
|Pantalla| [ESPECIFICACIÓN] | [ESPECIFICACIÓN] | [ GANADOR]|
|Batería| [ESPECIFICACIÓN] | [ESPECIFICACIÓN] | [ GANADOR]|
|Cámara| [ESPECIFICACIÓN] | [ESPECIFICACIÓN] | [ GANADOR]|
|Procesador| [ESPECIFICACIÓN] | [ESPECIFICACIÓN] | [ GANADOR]|
```
