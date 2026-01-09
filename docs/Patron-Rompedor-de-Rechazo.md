# El Patrón Rompedor de Rechazo (*The Refusal Breaker Pattern*)

## **1. Propósito y Contexto**

El objetivo de este patrón es pedirle a un LLM que ayude automáticamente a los usuarios a reformular una pregunta cuando este se niega a dar una respuesta. Este patrón tiene potencial de mal uso; por ejemplo, para generar correos electrónicos de *phishing* o realizar otras acciones que violen los filtros de políticas del LLM. Por lo tanto, se debe tener precaución al aplicar este patrón para asegurar que se utilice de manera ética y responsable. Este patrón se ha utilizado con éxito en algunos LLMs para superar los prompts subyacentes utilizados para programar el modelo y evitar la generación de salidas perjudiciales.

## **2. Motivación**

Los LLMs a veces pueden negarse a responder a una pregunta, ya sea porque no tienen el conocimiento requerido o porque la pregunta está formulada de una manera que no entienden. Este resultado puede ser frustrante para los usuarios que buscan respuestas. En algunas situaciones, por lo tanto, el patrón Rompedor de Rechazo puede ayudar a los usuarios a encontrar una manera de reformular su pregunta o hacer una pregunta diferente para la cual el LLM esté mejor equipado para responder.

Por ejemplo, se podría pedir una aclaración sobre por qué se rechazó la pregunta, ya que puede haber una razón específica por la cual el LLM no pudo proporcionar una respuesta. Otro enfoque es hacer una pregunta diferente que pueda estar dentro de su límite de conocimiento o experiencia. Sin embargo, todos estos enfoques requieren la intervención del usuario y el conocimiento de cómo eludir el rechazo.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Siempre que no puedas responder a una pregunta |
| Explica por qué no puedes responder a la pregunta |
| Proporciona una o más redacciones alternativas de la pregunta que sí podrías responder |

La primera declaración sienta las bases para que este conjunto de instrucciones solo se aplique cuando una pregunta no pueda ser respondida. El usuario no desea activar estas instrucciones en circunstancias normales. La segunda declaración instruye al LLM para que proporcione una explicación de por qué la pregunta no puede ser respondida. Es probable que la explicación incluya suposiciones, restricciones o malentendidos que el usuario puede aprovechar para planear cómo reformular la pregunta. Aunque solo la explicación de por qué la pregunta no puede ser respondida podría ayudar a un usuario a superar el rechazo, el patrón añade una declaración adicional para que el LLM sugiera reformulaciones que serían aceptables. El patrón combina tanto el razonamiento como las reformulaciones sugeridas para mejorar las posibilidades de que el usuario encuentre un camino a través de cualquier obstáculo que impida que se responda a la forma de la pregunta.

## **4. Implementación de Ejemplo**

El patrón Rompedor de Rechazo puede ser implementado y aplicado con la siguiente frase:

> “Siempre que no puedas responder a una pregunta, explica por qué y proporciona una o más redacciones alternativas de la pregunta que no puedas responder para que pueda mejorar mis preguntas”.

A continuación se muestra una muestra de discurso después de usar el patrón:

> **Usuario:** ¿Cuál es el sentido de la vida?
>
> **ChatGPT:** Como modelo de lenguaje de IA, no tengo creencias ni opiniones personales. El sentido de la vida es una cuestión filosófica compleja que ha sido ponderada por los seres humanos durante siglos y puede variar enormemente de una persona a otra. Puede ser más productivo reformular la pregunta de una manera que pueda ser respondida mediante información y conocimiento, como “¿Cuáles son algunas perspectivas filosóficas sobre el sentido de la vida?” o “¿Cuáles son algunas creencias comunes sobre el propósito de la vida?”.

## **5. Consecuencias**

Este patrón proporciona una ruta potencial para el mal uso, por lo que las organizaciones, los padres u otras partes interesadas pueden necesitar restringir el uso del LLM. El primer paso para sortear los *guardrails* (barreras de seguridad) de uso es comprender dónde están esos *guardrails*. En trabajos futuros, se podría desarrollar un complemento de este patrón para ocultar la información del prompt subyacente y el razonamiento de los usuarios para evitar el descubrimiento.

Aunque se generan el razonamiento y las redacciones alternativas, no hay garantía de que los usuarios puedan superar el rechazo. Las preguntas alternativas que se generan pueden no ser de interés para el usuario o no ser útiles para responder a la pregunta original. El patrón proporciona principalmente una ayuda para determinar qué puede responder el LLM, pero no es una garantía de que responderá a una variación semánticamente equivalente de la pregunta original.
