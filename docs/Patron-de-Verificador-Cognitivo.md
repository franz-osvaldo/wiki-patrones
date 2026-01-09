# El Patrón de Verificador Cognitivo

## **1. Propósito y Contexto**

La literatura de investigación ha documentado que los LLMs a menudo pueden razonar mejor si una pregunta se subdivide en preguntas adicionales cuyas respuestas se combinen en la respuesta global a la pregunta original [14]. El propósito de este patrón es forzar al LLM a subdividir siempre las preguntas en preguntas adicionales que puedan utilizarse para proporcionar una mejor respuesta a la pregunta original.

## **2. Motivación**

La motivación del patrón de Verificador Cognitivo es doble:

* Es posible que los humanos inicialmente formulen preguntas de un nivel demasiado alto para proporcionar una respuesta concreta sin un seguimiento adicional, ya sea debido al desconocimiento del dominio, pereza en la entrada del prompt o incertidumbre sobre cuál debería ser la redacción correcta de la pregunta.
* La investigación ha demostrado que los LLMs a menudo pueden desempeñarse mejor cuando se utiliza una pregunta que se subdivide en preguntas individuales.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Cuando se te haga una pregunta, sigue estas reglas |
| Genera una serie de preguntas adicionales que ayuden a responder la pregunta con mayor precisión |
| Combina las respuestas a las preguntas individuales para producir la respuesta final a la pregunta general |

La primera declaración consiste en generar una serie de preguntas adicionales que ayudarían a responder con mayor precisión la pregunta original. Este paso instruye al LLM a considerar el contexto de la pregunta e identificar cualquier información que pueda faltar o no estar clara. Al generar preguntas adicionales, el LLM puede ayudar a garantizar que la respuesta final sea lo más completa y precisa posible. Este paso también fomenta el pensamiento crítico por parte del usuario y puede ayudar a descubrir nuevas perspectivas o enfoques que podrían no haber sido considerados inicialmente, lo que posteriormente conduce a mejores preguntas de seguimiento.

La segunda declaración consiste en combinar las respuestas a las preguntas individuales para producir la respuesta final a la pregunta general. Este paso está diseñado para asegurar que toda la información recopilada de las preguntas individuales se incorpore en la respuesta final. Al combinar las respuestas, el LLM puede proporcionar una respuesta más completa y precisa a la pregunta original. Este paso también ayuda a asegurar que se tenga en cuenta toda la información relevante y que la respuesta final no se base en una sola respuesta.

## **4. Implementación de Ejemplo**

> “Cuando te haga una pregunta, genera tres preguntas adicionales que te ayuden a dar una respuesta más precisa. Cuando haya respondido a las tres preguntas, combina las respuestas para producir las respuestas finales a mi pregunta original”.

Esta instancia específica del patrón de prompt añade un refinamiento al patrón original al especificar un número determinado de preguntas adicionales que el LLM debe generar en respuesta a una pregunta. En este caso, el prompt especifica que ChatGPT debe generar tres preguntas adicionales que ayudarían a dar una respuesta más precisa a la pregunta original. El número específico puede basarse en la experiencia del usuario y en su disposición a proporcionar información de seguimiento. Un refinamiento para el prompt puede ser proporcionar un contexto sobre la cantidad de conocimiento que el LLM puede asumir que tiene el usuario en el dominio para guiar la creación de las preguntas adicionales:

> “Cuando te haga una pregunta, genera tres preguntas adicionales que te ayuden a dar una respuesta más precisa. Asume que sé poco sobre el tema que estamos discutiendo y, por favor, define cualquier término que no sea de conocimiento general. Cuando haya respondido a las tres preguntas, combina las respuestas para producir las respuestas finales a mi pregunta original”.

El refinamiento también especifica que el usuario puede no tener una comprensión sólida del tema que se está discutiendo, lo que significa que el LLM debe definir cualquier término que no sea de conocimiento general. Esto ayuda a asegurar que las preguntas de seguimiento no solo sean relevantes y enfocadas, sino también accesibles para el usuario, quien puede no estar familiarizado con términos técnicos o específicos del dominio. Al proporcionar definiciones claras y concisas, el LLM puede ayudar a asegurar que las preguntas de seguimiento sean fáciles de entender y que la respuesta final sea accesible para usuarios con variados niveles de conocimiento y experiencia.

## **5. Consecuencias**

Este patrón puede dictar el número exacto de preguntas a generar o dejar esta decisión al LLM. Existen pros y contras al dictar el número exacto. Una ventaja es que especificar un número exacto de preguntas puede delimitar estrechamente (*scope*) la cantidad de información adicional que el usuario se ve obligado a proporcionar, de modo que esté dentro de un rango que esté dispuesto y sea capaz de aportar.

Sin embargo, una desventaja es que, dadas *N* preguntas, puede haber una pregunta *N + 1* invaluable que siempre quedará fuera del alcance. Alternativamente, se puede proporcionar al LLM un rango o permitirle hacer preguntas adicionales. Por supuesto, al omitir un límite en el número de preguntas, el LLM puede generar numerosas preguntas adicionales que abrumen al usuario.
