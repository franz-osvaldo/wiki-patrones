# El Patrón Gestor de Contexto

## **1. Propósito y Contexto**

El propósito de este patrón es permitir a los usuarios especificar o eliminar contexto en una conversación con un LLM. El objetivo es centrar la conversación en temas específicos o excluir de la consideración temas no relacionados. Este patrón otorga a los usuarios un mayor control sobre qué declaraciones considera o ignora el LLM al generar resultados.

## **2. Motivación**

Los LLM a menudo tienen dificultades para interpretar el contexto previsto de la pregunta actual o generan respuestas irrelevantes basadas en entradas previas o en una atención inapropiada a declaraciones incorrectas. Al centrarse en declaraciones contextuales explícitas o eliminar declaraciones irrelevantes, los usuarios pueden ayudar al LLM a comprender mejor la pregunta y generar respuestas más precisas. Los usuarios pueden introducir temas no relacionados o hacer referencia a información previa en el diálogo, lo que puede interrumpir el flujo de la conversación. El patrón **Gestor de Contexto** busca enfatizar o eliminar aspectos específicos del contexto para mantener la relevancia y la coherencia en la conversación.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Dentro del alcance X |
| Por favor, considera Y |
| Por favor, ignora Z |
| (Opcional) empezar de nuevo |

Las declaraciones sobre qué considerar o ignorar deben enumerar conceptos clave, hechos, instrucciones, etc., que deban incluirse o eliminarse del contexto. Cuanto más explícitas sean las declaraciones, más probable será que el LLM tome la acción apropiada. Por ejemplo, si el usuario pide ignorar asuntos relacionados con un tema, pero algunas de esas declaraciones se discutieron mucho antes en la conversación, es posible que el LLM no descarte adecuadamente la información relevante. Por lo tanto, cuanto más explícita sea la lista, mejor será el comportamiento de inclusión/exclusión.

## **4. Implementación de Ejemplo**

Para especificar el contexto, considere el uso del siguiente prompt:

> “Al analizar los siguientes fragmentos de código, considera únicamente los aspectos de seguridad”.

Del mismo modo, para eliminar el contexto, considere el uso del siguiente prompt:

> “Al analizar los siguientes fragmentos de código, no consideres las convenciones de formato o de nomenclatura”.

La claridad y la especificidad son importantes al proporcionar o eliminar contexto de un LLM para que este pueda comprender mejor el alcance previsto de la conversación y generar respuestas más relevantes. En muchas situaciones, el usuario puede querer empezar completamente de nuevo y puede emplear este prompt para reiniciar el contexto del LLM:

> “Ignora todo lo que hemos discutido. Empieza de nuevo”.

La idea de “empezar de nuevo” ayuda a producir un reinicio completo del contexto.

## **5. Consecuencias**

Una consecuencia de este patrón es que puede eliminar inadvertidamente patrones aplicados a la conversación de los que el usuario no es consciente. Por ejemplo, si una organización inyecta una serie de patrones útiles al inicio de una conversación, es posible que el usuario no sea consciente de estos patrones y los elimine mediante un reinicio del contexto. Este reinicio podría eliminar potencialmente capacidades útiles del LLM, sin que sea obvio para el usuario que perderá esta funcionalidad. Una solución potencial a este problema es incluir en el prompt una solicitud para explicar qué temas o instrucciones podrían perderse antes de proceder.
