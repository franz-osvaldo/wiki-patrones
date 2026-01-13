# El Patrón Gestor de Contexto

## **1. Propósito y Contexto**

El Context Manager Pattern busca dar al usuario la capacidad de definir o eliminar el contexto dentro de una conversación con un modelo de lenguaje (LLM). El Objetivo principal es permitir que la interacción se centre en temas específicos y que se excluyan los temas irrelevantes. Con este patrón, el usuario decide qué información el modelo debe considerar y qué debe ignorar al generar sus respuestas. Se logra una conversación más enfocada y precisa, evitando que el modelo se desvíe hacia contenidos que no son relevantes para la tarea o el tema en cuestión.

## **2. Motivación**

 Los LLM suelen confundirse con el contexto real de la pregunta actual, porque arrastran información de entradas anteriores o prestan atención a frases irrelevantes. Esto puede llevar a respuestas fuera de tema, incoherentes o poco útiles, especialmente cuando el usuario introduce tópicos no relacionados o menciona información de diálogos pasados. El **Context Manager Pattern** permite al usuario resaltar el contexto importante o eliminar el irrelevante, para que el modelo se concentre en lo que realmente importa. El objetivo es mantener la conversación relevante y coherente, evitando que el flujo se interrumpa por distracciones o desvíos.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Dentro del alcance X |
| Por favor, considera Y |
| Por favor, ignora Z |
| (Opcional) empezar de nuevo |

Las declaraciones sobre qué considerar o ignorar deben enumerar conceptos clave, hechos o instrucciones que se incluyan o eliminen del contexto. Cuanto más explícitas sean, mayor será la probabilidad de que el modelo las aplique correctamente. Por ejemplo, si se pide ignorar un tema mencionado mucho antes en la conversación, el modelo podría no omitirlo de forma adecuada. Por eso, cuanto más clara y detallada sea la lista, mejor será el manejo de inclusión y exclusión.

## **4. Implementación de Ejemplo**

Para especificar el contexto, considere el uso del siguiente prompt:

> “Al analizar los siguientes fragmentos de código, considera únicamente los aspectos de seguridad”.

Del mismo modo, para eliminar el contexto, considere el uso del siguiente prompt:

> “Al analizar los siguientes fragmentos de código, no consideres las convenciones de formato o de nomenclatura”.

La claridad y la especificidad son esenciales al dar o quitar contexto a un LLM. Esto le permite entender mejor el alcance de la conversación y generar respuestas más relevantes. En muchos casos, el usuario puede querer empezar desde cero

> “Ignora todo lo que hemos discutido. Empieza de nuevo”.

La idea de “empezar de nuevo” ayuda a producir un reinicio completo del contexto.

## **5. Consecuencias**

Una consecuencia de este patrón es que puede eliminar sin querer patrones añadidos a la conversación de los que el usuario no es consciente. Por ejemplo, si una organización introduce patrones útiles al inicio de la conversación, el usuario podría no saberlo y borrarlos al reiniciar el contexto. Ese reinicio podría quitar capacidades valiosas del LLM sin que el usuario se dé cuenta de que las perderá. Una solución posible es añadir al prompt una instrucción que explique qué temas o indicaciones podrían perderse antes de continuar.

## **6. Plantillas**

```py title="PLANTILLA"
¿Podrías listar toda la información, preferencias y datos personales que has almacenado en tu memoria sobre mí?
```
