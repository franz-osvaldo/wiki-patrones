# El Patrón de Refinamiento de Pregunta

## **1. Propósito y Contexto**

Este patrón involucra al LLM en el proceso de ingeniería de *prompts*. La intención es asegurar que el modelo conversacional sugiera siempre versiones potencialmente mejores o más refinadas de la pregunta original del usuario. Al usar este patrón, el LLM ayuda a encontrar la pregunta correcta para obtener una respuesta precisa. Además, puede facilitar el acceso a la información o el logro del objetivo con menos interacciones que si se empleara un *prompting* de prueba y error.

## **2. Motivación**

Cuando un usuario hace una pregunta, es posible que no sea un experto en el dominio, que desconozca la mejor manera de formularla o que ignore información adicional útil para el planteamiento. Los LLMs a menudo declaran limitaciones sobre su respuesta o solicitan datos extra para mayor precisión, además de indicar las suposiciones realizadas. La motivación reside en usar esa información o suposiciones para generar un mejor *prompt*. En lugar de exigir al usuario que **procese** y reformule su solicitud manualmente, el LLM puede refinar el *prompt* directamente para incorporar dichos elementos .

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Dentro del alcance X, sugiere una versión mejor de la pregunta para usar en su lugar |
| (Opcional) pregúntame si me gustaría usar la versión mejorada en su lugar |

La primera declaración pide al LLM que sugiera una versión mejorada de la pregunta dentro de un ámbito específico. Se define un ámbito (*scope*) para evitar que todas las preguntas se reformulen automáticamente o para asegurar que se refinen hacia un objetivo concreto . La segunda declaración está destinada a la automatización, permitiendo al usuario aceptar la pregunta refinada sin tener que copiarla o escribirla de nuevo. La ingeniería de este *prompt* puede mejorarse combinándola con el Patrón de Reflexión (*Reflection Pattern*), permitiendo que el LLM explique por qué considera que la nueva versión es una mejora.

## **4. Implementación de Ejemplo**

> "A partir de ahora, siempre que haga una pregunta sobre la seguridad de un artefacto de software, sugiere una mejor versión de la pregunta que incorpore información específica sobre riesgos de seguridad en el lenguaje o *framework* que estoy usando, y pregúntame si me gustaría usar tu versión en su lugar".

En este contexto, el LLM utilizará el patrón para mejorar las consultas de seguridad, solicitando o integrando detalles sobre el artefacto de software y la tecnología utilizada. Por ejemplo, si un desarrollador de una aplicación web en Python con FastAPI pregunta a ChatGPT "¿Cómo manejo la autenticación de usuarios?", el modelo refinará la pregunta considerando el contexto tecnológico. Proporcionará entonces una revisión más específica, tal como: "¿Cuáles son las mejores prácticas para manejar la autenticación de usuarios de forma segura en una aplicación web FastAPI para mitigar riesgos comunes, como *cross-site scripting* (XSS), falsificación de solicitudes entre sitios (CSRF) y secuestro de sesiones?".

Es probable que el detalle adicional no solo conciencie al usuario sobre problemas a considerar, sino que conduzca a una mejor respuesta técnica. Para tareas de ingeniería de software, este patrón podría incorporar consideraciones sobre *bugs*, modularidad o calidad del código . Otro enfoque sería refinar las preguntas para que el código generado respete la **separación de responsabilidades** (*separation of concerns*) o minimice el uso de bibliotecas externas, tal como:

> "Siempre que haga una pregunta sobre cómo escribir código, sugiere una mejor versión que pida cómo hacerlo minimizando mis dependencias de bibliotecas externas."

## **5. Consecuencias**

El patrón de Refinamiento de Pregunta cierra la brecha entre el conocimiento del usuario y la comprensión del LLM, produciendo interacciones más eficientes. Un riesgo es su tendencia a **acotar** rápidamente el cuestionamiento hacia un área específica, guiando al usuario por un camino de indagación más limitado de lo necesario. Como resultado de esta **limitación**, el usuario podría perder de vista el "panorama general" (*bigger picture*). Una solución es ampliar el alcance en el *prompt*, por ejemplo: "no limites mis preguntas a lenguajes o *frameworks* específicos".

Para superar una orientación demasiado estrecha, se puede combinar este patrón con otros, como el Patrón de Verificador Cognitivo (*Cognitive Verifier*). Esto instruye al LLM a producir una serie de preguntas de seguimiento ("subpreguntas") que ayuden a construir la pregunta refinada. Por ejemplo:

> “De ahora en adelante, cada vez que haga una pregunta, haz cuatro preguntas adicionales que te ayuden a producir una versión mejor de mi pregunta original. Luego, usa mis respuestas para sugerir una versión mejor de mi pregunta original”.

Al igual que con muchos patrones que permiten a un LLM generar nuevas preguntas utilizando su conocimiento, el LLM puede introducir términos o conceptos desconocidos para el usuario en la pregunta. Una forma de abordar este problema es incluir una declaración que indique que el LLM debe explicar cualquier término desconocido que introduzca en la pregunta. Una mejora adicional de esta idea es combinar el patrón de **Refinamiento de Pregunta** con el patrón **Persona** para que el LLM marque los términos y genere definiciones que asuman un nivel particular de conocimiento, como en este ejemplo:


> “De ahora en adelante, cada vez que haga una pregunta, haz cuatro preguntas adicionales que te ayuden a producir una versión mejor de mi pregunta original. Luego, usa mis respuestas para sugerir una versión mejor de mi pregunta original. Después de las preguntas de seguimiento, actúa temporalmente como un usuario sin conocimientos de AWS y define cualquier término que necesite saber para responder con precisión a las preguntas”.

Un LLM siempre puede producir imprecisiones fácticas, al igual que un humano. Un riesgo de este patrón es que las imprecisiones se introduzcan en la pregunta refinada. Este riesgo puede mitigarse, sin embargo, combinando el patrón de **Lista de Verificación de Hechos** para permitir al usuario identificar posibles imprecisiones y el patrón de **Reflexión** para explicar el razonamiento detrás del refinamiento de la pregunta.

## **6. Plantilla**

```py title="PLANTILLA"
[PREGUNTA]
## PROTOCOLO DE REFINAMIENTO
No generes la respuesta todavía, ni des ejemplos o borradores. En su lugar:
1. Sugiere una mejor versión de mi pregunta.
2. Explica brevemente POR QUÉ tu versión es mejor.
3. Consúltame si quiero usar la versión que tu proporcionas.
```

## **7. Ejemplos**

```py title="Número de Huesos"
¿Cuántos huesos tiene el cuerpo humano?
## PROTOCOLO DE REFINAMIENTO
No generes la respuesta todavía, ni des ejemplos o borradores. En su lugar:
1. Sugiere una mejor versión de mi pregunta.
2. Explica brevemente POR QUÉ tu versión es mejor.
3. Consúltame si quiero usar la versión que tu proporcionas.
```

```py title="Número de Paises"
¿Cuántos países hay en el mundo?
## PROTOCOLO DE REFINAMIENTO
No generes la respuesta todavía, ni des ejemplos o borradores. En su lugar:
1. Sugiere una mejor versión de mi pregunta.
2. Explica brevemente POR QUÉ tu versión es mejor.
3. Consúltame si quiero usar la versión que tu proporcionas.
```

```py title="La montaña más alta"
¿Cuál es la montaña más alta?
## PROTOCOLO DE REFINAMIENTO
No generes la respuesta todavía, ni des ejemplos o borradores. En su lugar:
1. Sugiere una mejor versión de mi pregunta.
2. Explica brevemente POR QUÉ tu versión es mejor.
3. Consúltame si quiero usar la versión que tu proporcionas.
```

```py title="A qué temperatura"
¿A qué temperatura hierve el agua?
## PROTOCOLO DE REFINAMIENTO
No generes la respuesta todavía, ni des ejemplos o borradores. En su lugar:
1. Sugiere una mejor versión de mi pregunta.
2. Explica brevemente POR QUÉ tu versión es mejor.
3. Consúltame si quiero usar la versión que tu proporcionas.
```

```py title="Fruta o verdura"
¿El tomate es una fruta o una verdura?
## PROTOCOLO DE REFINAMIENTO
No generes la respuesta todavía, ni des ejemplos o borradores. En su lugar:
1. Sugiere una mejor versión de mi pregunta.
2. Explica brevemente POR QUÉ tu versión es mejor.
3. Consúltame si quiero usar la versión que tu proporcionas.
```
