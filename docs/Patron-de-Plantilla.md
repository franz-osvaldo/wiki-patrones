# El Patrón de Plantilla (*Template Pattern*)

## **1. Propósito y Contexto**

La intención de este patrón es asegurar que la salida de un LLM siga una plantilla precisa en términos estructurales. Por ejemplo, el usuario podría necesitar generar una URL con información específica dentro de la ruta de la misma. Este patrón permite instruir al LLM para que produzca su salida en un formato que, ordinariamente, no utilizaría para el tipo de contenido solicitado.

## **2. Motivación**

En algunos casos, la salida debe generarse en un formato preciso, específico de una aplicación o caso de uso, que el LLM desconoce. Dado que el modelo no es consciente de la estructura de la plantilla, se le debe instruir sobre cuál es el formato y dónde deben ubicarse las diferentes partes de su respuesta. Esto podría aplicarse a una estructura de datos de muestra que se está generando, una serie de cartas modelo que se están rellenando, etc..

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Voy a proporcionar una plantilla para tu salida |
| X es mi marcador de posición (*placeholder*) para el contenido |
| Intenta ajustar la salida en uno o más de los marcadores de posición que enumero |
| Por favor, conserva el formato y la plantilla general que proporciono |
| Esta es la plantilla: [PATRÓN con MARCADORES DE POSICIÓN] |

La primera declaración dirige al LLM a seguir una plantilla específica. Esta se usará para intentar **forzar** las respuestas del modelo hacia una estructura consistente con las necesidades de formato del usuario. Este patrón es necesario cuando el formato de destino es desconocido para el LLM . Si el modelo ya conoce el formato (ej. un tipo de archivo específico), el patrón puede omitirse especificando simplemente dicho formato. No obstante, en casos como la generación de *Javascript Object Notation* (JSON), donde existe gran variación en la representación de los datos, la plantilla sirve para asegurar que el resultado cumpla con las restricciones adicionales del usuario.

La segunda declaración advierte al LLM que la plantilla contiene un conjunto de **marcadores de posición**. Los usuarios explicarán cómo debe insertarse la salida a través de estos marcadores, los cuales permiten señalar semánticamente dónde va la información. Los marcadores pueden usar formatos como `NOMBRE`, permitiendo al LLM inferir el significado para determinar qué insertar (por ejemplo, el nombre de una persona en el marcador `NOMBRE`). Además, el uso de marcadores permite indicar qué información es innecesaria: si no hay un marcador para un componente, este puede omitirse. Idealmente, los marcadores deben usar un formato común en los datos de entrenamiento del LLM, como mayúsculas sostenidas o corchetes.

La tercera declaración intenta restringir al LLM para que no reescriba o modifique arbitrariamente la plantilla para acomodar todos los componentes. Cabe señalar que esto podría no impedir la generación de texto adicional antes o después de la plantilla. En la práctica, los LLMs suelen respetar la estructura, pero eliminar el texto excedente puede requerir experimentar con la redacción del *prompt*.

## **4. Implementación de Ejemplo**

A continuación se muestra una plantilla de ejemplo para generar URLs donde la salida se coloca en lugares específicos de la plantilla:

> “Voy a proporcionar una plantilla para tu salida. Todo lo que esté en mayúsculas sostenidas es un marcador de posición. Cada vez que generes texto, intenta ajustarlo en uno de los marcadores de posición que enumero. Por favor, conserva el formato y la plantilla general que proporciono en `https://myapi.com/NOMBRE/perfil/TRABAJO`”.

A continuación se muestra una interacción de ejemplo después de proporcionar el prompt:

> **Usuario:** “Genera un nombre y un cargo para una persona”.
> **ChatGPT:** `https://myapi.com/Emily_Parker/perfil/Software_Engineer`

## **5. Consecuencias**

Una consecuencia de aplicar el Patrón de Plantilla es que filtra la salida del LLM, lo cual puede **descartar** otras respuestas que habrían sido útiles. En muchos casos, el LLM podría proporcionar descripciones valiosas del código, justificaciones de decisiones u otros detalles que este patrón eliminará efectivamente. Por lo tanto, los usuarios deben sopesar los pros y contras de filtrar esta información adicional.

Además, el filtrado puede dificultar la combinación de este patrón con otros de la categoría de Personalización de Salida. Al restringir el formato, puede ser incompatible con otros tipos de generación. Por ejemplo, la plantilla de URL anterior difícilmente podría combinarse con el Patrón de Receta (*Recipe Pattern*), el cual requiere generar una lista secuencial de pasos.

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
