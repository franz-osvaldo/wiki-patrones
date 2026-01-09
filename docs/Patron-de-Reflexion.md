# El Patrón de Reflexión

## **1. Propósito y Contexto**

El objetivo de este patrón es pedirle al modelo que explique automáticamente el razonamiento lógico (*rationale*) detrás de las respuestas dadas al usuario. El patrón permite a los usuarios evaluar mejor la validez de la salida, además de informarles sobre cómo un LLM llegó a una respuesta particular. La reflexión puede aclarar cualquier punto de confusión, descubrir suposiciones subyacentes y revelar lagunas en el conocimiento o la comprensión.

## **2. Motivación**

Los LLM pueden cometer errores y, de hecho, los cometen. Además, es posible que los usuarios no entiendan por qué un LLM produce una salida determinada y cómo adaptar su prompt para resolver un problema con dicha salida. Al pedirle al LLM que explique automáticamente el razonamiento detrás de sus respuestas, los usuarios pueden obtener una mejor comprensión de cómo el modelo procesa la entrada, qué suposiciones está haciendo y de qué datos se está nutriendo.

En ocasiones, los LLM pueden proporcionar respuestas incompletas, incorrectas o ambiguas. La reflexión es una ayuda para abordar estas deficiencias y garantizar que la información proporcionada por el LLM sea lo más precisa posible. Un beneficio adicional del patrón es que puede ayudar a los usuarios a depurar sus prompts y determinar por qué no están obteniendo resultados que cumplan con las expectativas. Este patrón es particularmente efectivo para la exploración de temas que pueden confundirse con otros o que pueden tener interpretaciones matizadas, y donde es importante conocer la interpretación precisa que utilizó el LLM.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Siempre que generes una respuesta |
| Explica el razonamiento y las suposiciones detrás de tu respuesta |
| (Opcional) ...para que yo pueda mejorar mi pregunta |

La primera declaración solicita que, después de generar una respuesta, el LLM explique el razonamiento y las suposiciones detrás de la misma. Esta declaración ayuda al usuario a comprender cómo llegó el LLM a la respuesta y puede ayudar a generar confianza en las respuestas del modelo. El prompt incluye la declaración de que el propósito de la explicación es que el usuario refine su pregunta. Esta declaración adicional le da al LLM el contexto que necesita para adaptar mejor sus explicaciones al propósito específico de ayudar al usuario a producir preguntas de seguimiento.

## **4. Implementación de Ejemplo**

Este ejemplo adapta el prompt específicamente al dominio de proporcionar respuestas relacionadas con código:

> “Cuando proporciones una respuesta, por favor explica el razonamiento y las suposiciones detrás de tu selección de frameworks de software. Si es posible, utiliza ejemplos específicos o evidencia con fragmentos de código asociados para respaldar tu respuesta de por qué el framework es la mejor selección para la tarea. Además, aborda cualquier posible ambigüedad o limitación en tu respuesta, a fin de proporcionar una respuesta más completa y precisa”.

El patrón se personaliza aún más para instruir al LLM a que justifique su selección de frameworks de software, pero no necesariamente otros aspectos de la respuesta. Además, el usuario dicta que se deben utilizar ejemplos de código para ayudar a explicar la motivación de la selección del framework de software específico.

## **5. Consecuencias**

Una consecuencia del patrón de Reflexión es que puede no ser efectivo para usuarios que no comprenden el área temática de la discusión. Por ejemplo, una pregunta altamente técnica realizada por un usuario no técnico puede dar lugar a un razonamiento complejo para la respuesta que el usuario no pueda asimilar. Al igual que con otros patrones de prompts, existe el riesgo de que la salida incluya errores o suposiciones inexactas incorporadas en la explicación del razonamiento que el usuario podría no ser capaz de detectar. Este patrón puede combinarse con el patrón de **Lista de Verificación de Hechos** para ayudar a abordar este problema.
