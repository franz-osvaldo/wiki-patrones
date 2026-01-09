# El Patrón de Refinamiento de Pregunta

## **1. Propósito y Contexto**

Este patrón involucra al LLM en el proceso de ingeniería de prompts. El propósito es asegurar que el LLM conversacional sugiera siempre preguntas potencialmente mejores o más refinadas que el usuario podría hacer en lugar de su pregunta original. Al usar este patrón, el LLM puede ayudar al usuario a encontrar la pregunta correcta para obtener una respuesta precisa. Además, el LLM puede ayudar al usuario a encontrar la información o lograr su objetivo en menos interacciones que si el usuario empleara una técnica de prompts por ensayo y error.

## **2. Motivación**

Si un usuario hace una pregunta, es posible que no sea un experto en el dominio y que no sepa cuál es la mejor manera de formular la pregunta o no sea consciente de la información adicional que resultaría útil para plantearla. Los LLMs a menudo declararán limitaciones en la respuesta que proporcionan o solicitarán información adicional para ayudarles a producir una respuesta más precisa. Un LLM también puede declarar las suposiciones que hizo al proporcionar la respuesta. La motivación es que esta información adicional o el conjunto de suposiciones podrían usarse para generar un mejor prompt. En lugar de requerir que el usuario digiera y reformule su prompt con la información adicional, el LLM puede refinar directamente el prompt para incorporar dicha información.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Dentro del alcance X, sugiere una versión mejor de la pregunta para usar en su lugar |
| (Opcional) pregúntame si me gustaría usar la versión mejorada en su lugar |

La primera declaración contextual en el prompt pide al LLM que sugiera una mejor versión de una pregunta dentro de un alcance específico. El alcance se proporciona para asegurar que no todas las preguntas sean reformuladas automáticamente o que se refinen con un objetivo determinado. La segunda declaración contextual está pensada para la automatización y permite al usuario utilizar automáticamente la pregunta refinada sin tener que copiar/pegar o introducirla manualmente. La ingeniería de este prompt puede refinarse aún más combinándolo con el patrón de **Reflexión**, lo que permite al LLM explicar por qué cree que la pregunta refinada es una mejora.

## **4. Implementación de Ejemplo**

> “De ahora en adelante, cada vez que haga una pregunta sobre la seguridad de un artefacto de software, sugiere una versión mejor de la pregunta para usar que incorpore información específica sobre los riesgos de seguridad en el lenguaje o framework que estoy utilizando y pregúntame si me gustaría usar tu pregunta en su lugar”.

En el contexto del ejemplo anterior, el LLM utilizará el patrón de **Refinamiento de Pregunta** para mejorar las preguntas relacionadas con la seguridad solicitando o utilizando detalles específicos sobre el artefacto de software y el lenguaje o framework utilizado para construirlo. Por ejemplo, si un desarrollador de una aplicación web de Python con FastAPI le pregunta a ChatGPT: “¿Cómo manejo la autenticación de usuarios en mi aplicación web?”, el LLM refinará la pregunta teniendo en cuenta que la aplicación web está escrita en Python con FastAPI. El LLM proporciona entonces una pregunta revisada que es más específica para el lenguaje y el framework, tal como: “¿Cuáles son las mejores prácticas para manejar la autenticación de usuarios de forma segura en una aplicación web de FastAPI para mitigar riesgos de seguridad comunes, como el cross-site scripting (XSS), cross-site request forgery (CSRF) y el secuestro de sesiones?”.

Es probable que el detalle adicional en la pregunta revisada no solo haga que el usuario sea consciente de los problemas que debe considerar, sino que conduzca a una mejor respuesta por parte del LLM. Para tareas de ingeniería de software, este patrón también podría incorporar información sobre posibles errores (*bugs*), modularidad u otras consideraciones de calidad del código. Otro enfoque sería refinar automáticamente las preguntas para que el código generado separe limpiamente las responsabilidades (*concerns*) o minimice el uso de librerías externas, como por ejemplo:

> Siempre que haga una pregunta sobre cómo escribir algún código, sugiere una mejor versión de mi pregunta que pida cómo escribir el código de una manera que minimice mis dependencias de librerías externas.

## **5. Consecuencias**

El patrón de **Refinamiento de Pregunta** ayuda a cerrar la brecha entre el conocimiento del usuario y la comprensión del LLM, produciendo así interacciones más eficientes y precisas. Un riesgo de este patrón es su tendencia a estrechar rápidamente el interrogatorio por parte del usuario hacia un área específica que guía al usuario por un camino de indagación más limitado de lo necesario. La consecuencia de este estrechamiento es que el usuario puede perder información importante del “panorama general” (*bigger picture*). Una solución a este problema es proporcionar un alcance adicional al prompt del patrón, como por ejemplo “no limites mis preguntas a lenguajes de programación o frameworks específicos”.

Otro enfoque para superar el estrechamiento arbitrario o la focalización limitada de la pregunta refinada es combinar el patrón de **Refinamiento de Pregunta** con otros patrones. En particular, este patrón puede combinarse con el patrón de **Verificador Cognitivo** para que el LLM produzca automáticamente una serie de preguntas de seguimiento que puedan generar la pregunta refinada. Por ejemplo, en el siguiente prompt se aplican los patrones de **Refinamiento de Pregunta** y **Verificador Cognitivo** para asegurar que se planteen mejores preguntas al LLM:

> “De ahora en adelante, cada vez que haga una pregunta, haz cuatro preguntas adicionales que te ayuden a producir una versión mejor de mi pregunta original. Luego, usa mis respuestas para sugerir una versión mejor de mi pregunta original”.

Al igual que con muchos patrones que permiten a un LLM generar nuevas preguntas utilizando su conocimiento, el LLM puede introducir términos o conceptos desconocidos para el usuario en la pregunta. Una forma de abordar este problema es incluir una declaración que indique que el LLM debe explicar cualquier término desconocido que introduzca en la pregunta. Una mejora adicional de esta idea es combinar el patrón de **Refinamiento de Pregunta** con el patrón **Persona** para que el LLM marque los términos y genere definiciones que asuman un nivel particular de conocimiento, como en este ejemplo:

> “De ahora en adelante, cada vez que haga una pregunta, haz cuatro preguntas adicionales que te ayuden a producir una versión mejor de mi pregunta original. Luego, usa mis respuestas para sugerir una versión mejor de mi pregunta original. Después de las preguntas de seguimiento, actúa temporalmente como un usuario sin conocimientos de AWS y define cualquier término que necesite saber para responder con precisión a las preguntas”.

Un LLM siempre puede producir imprecisiones fácticas, al igual que un humano. Un riesgo de este patrón es que las imprecisiones se introduzcan en la pregunta refinada. Este riesgo puede mitigarse, sin embargo, combinando el patrón de **Lista de Verificación de Hechos** para permitir al usuario identificar posibles imprecisiones y el patrón de **Reflexión** para explicar el razonamiento detrás del refinamiento de la pregunta.

## **6. Plantilla**

```py title="PLANTILLA"
[PREGUNTA]
## PROTOCOLO DE REFINAMIENTO
Antes de responder:
1. Sugiere una mejor versión de mi pregunta.
2. Explica brevemente POR QUÉ tu versión es mejor.
3. Consúltame si quiero usar la versión que tu proporcionas.
```

## **7. Ejemplos**

```py title="Número de Huesos"
¿Cuántos huesos tiene el cuerpo humano?
## PROTOCOLO DE REFINAMIENTO
Antes de responder:
1. Sugiere una mejor versión de mi pregunta.
2. Explica brevemente POR QUÉ tu versión es mejor.
3. Consúltame si quiero usar la versión que tu proporcionas.
```

```py title="Número de Paises"
¿Cuántos países hay en el mundo?
## PROTOCOLO DE REFINAMIENTO
Antes de responder:
1. Sugiere una mejor versión de mi pregunta.
2. Explica brevemente POR QUÉ tu versión es mejor.
3. Consúltame si quiero usar la versión que tu proporcionas.
```

```py title="La montaña más alta"
¿Cuál es la montaña más alta?
## PROTOCOLO DE REFINAMIENTO
Antes de responder:
1. Sugiere una mejor versión de mi pregunta.
2. Explica brevemente POR QUÉ tu versión es mejor.
3. Consúltame si quiero usar la versión que tu proporcionas.
```

```py title="A qué temperatura"
¿A qué temperatura hierve el agua?
## PROTOCOLO DE REFINAMIENTO
Antes de responder:
1. Sugiere una mejor versión de mi pregunta.
2. Explica brevemente POR QUÉ tu versión es mejor.
3. Consúltame si quiero usar la versión que tu proporcionas.
```

```py title="A qué temperatura"
¿El tomate es una fruta o una verdura?
## PROTOCOLO DE REFINAMIENTO
Antes de responder:
1. Sugiere una mejor versión de mi pregunta.
2. Explica brevemente POR QUÉ tu versión es mejor.
3. Consúltame si quiero usar la versión que tu proporcionas.
```
