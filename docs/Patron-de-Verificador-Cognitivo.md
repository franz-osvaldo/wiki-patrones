# El Patrón de Verificador Cognitivo

## **1. Propósito y Contexto**

La literatura de investigación ha documentado que los LLMs suelen razonar mejor si una pregunta compleja se subdivide en interrogantes adicionales, cuyas respuestas se combinan para formar la respuesta general a la pregunta original. La intención del patrón es forzar al LLM a **desglosar** siempre las consultas en preguntas subsidiarias que permitan construir una mejor respuesta final.

## **2. Motivación**

La motivación del patrón de Verificador Cognitivo es doble:

1. Los humanos pueden formular inicialmente preguntas de demasiado alto nivel para obtener una respuesta concreta sin seguimiento adicional. Esto puede deberse a la falta de familiaridad con el dominio, **falta de esfuerzo en la redacción del _prompt_** o inseguridad sobre el fraseo correcto.

2. La investigación demuestra que los LLMs a menudo se desempeñan mejor cuando abordan una consulta subdividida en preguntas individuales.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Cuando se te haga una pregunta, sigue estas reglas |
| Genera una serie de preguntas adicionales que ayudarían a responder con mayor precisión a la pregunta. |
| Combina las respuestas de las preguntas individuales para producir la respuesta final a la pregunta general. |

La primera declaración instruye generar **una serie de preguntas adicionales** que ayuden a responder con mayor precisión a la original. Este paso obliga al LLM a considerar el contexto e identificar información faltante o ambigua. Al generar estas preguntas, el LLM asegura que la respuesta final sea lo más completa y precisa posible. Esto también fomenta el pensamiento crítico del usuario, descubriendo nuevas perspectivas que tal vez no se consideraron inicialmente, lo que conduce a mejores preguntas de seguimiento.

La segunda declaración ordena **integrar** las respuestas individuales para producir la respuesta final. Este paso asegura que toda la información recopilada se incorpore en la conclusión. Al combinar las respuestas, el LLM proporciona una solución más robusta y evita basarse en un único punto de datos.

## **4. Implementación de Ejemplo**

> "Cuando te haga una pregunta, genera tres preguntas adicionales que te ayudarían a dar una respuesta más precisa. Cuando haya respondido a las tres preguntas, combina las respuestas para producir la respuesta final a mi pregunta original."

Esta instancia añade un refinamiento al especificar un número fijo de preguntas adicionales. En este caso, el _prompt_ estipula que ChatGPT debe generar **tres** preguntas auxiliares. Este número puede ajustarse según la experiencia del usuario y su disposición a colaborar.

Un refinamiento adicional puede proporcionar contexto sobre el nivel de conocimiento del usuario:

> "Cuando te haga una pregunta, genera tres preguntas adicionales que te ayudarían a dar una respuesta más precisa. Asume que sé poco sobre el tema y, por favor, define cualquier término que no sea de conocimiento general. Cuando haya respondido a las tres preguntas, combina las respuestas para producir la respuesta final".

Este refinamiento especifica que el usuario carece de una comprensión sólida del tema, instruyendo al LLM a definir términos técnicos. Esto asegura que las preguntas de seguimiento sean accesibles y fáciles de entender para usuarios con distintos niveles de experiencia.

## **5. Consecuencias**

Este patrón puede **estipular** el número exacto de preguntas o dejar la decisión al LLM. Existen ventajas y desventajas en fijar un número exacto. Una ventaja es que acota estrictamente la cantidad de información adicional que el usuario debe aportar, manteniéndola dentro de un rango manejable.

Sin embargo, una desventaja es que, dadas _N_ preguntas, podría existir una pregunta _N+1_ valiosa que siempre quedará **fuera del alcance**. Alternativamente, se puede dar un rango o libertad total al LLM. No obstante, sin un límite, el LLM podría generar una cantidad excesiva de preguntas que abrume al usuario.

## **6. Plantilla**

```py title="PLANTILLA"
[ TAREA / PREGUNTA ]
## ESTRATEGIA DE VERIFICACIÓN COGNITIVA 
No generes la respuesta todavía, ni des ejemplos o borradores. En su lugar:
1. Para que puedas responder con precisión, genera [N - Opcional] preguntas adicionales que necesites que yo responda para aclarar el contexto. 
2. Una vez que yo responda, combina esa nueva información para producir la respuesta final y completa.
```

## **7. Ejemplos**

```py title="La Excusa Perfecta"
Genera una excusa creíble para no ir a la fiesta de cumpleaños de mi jefe este sábado.
## ESTRATEGIA DE VERIFICACIÓN COGNITIVA 
No generes la respuesta todavía, ni des ejemplos o borradores. En su lugar:
1. Para que puedas responder con precisión, genera 4 preguntas adicionales que necesites que yo responda para aclarar el contexto. 
2. Una vez que yo responda, combina esa nueva información para producir la respuesta final y completa.

```

```py title="El Pánico del Aniversario"
Olvidé que mañana mi esposa y yo estamos de aniversario. Dime qué comprar rápido.
## ESTRATEGIA DE VERIFICACIÓN COGNITIVA 
No generes la respuesta todavía, ni des ejemplos o borradores. En su lugar:
1. Para que puedas responder con precisión, genera 4 preguntas adicionales que necesites que yo responda para aclarar el contexto. 
2. Una vez que yo responda, combina esa nueva información para producir la respuesta final y completa.
```

```py title="Diplomacia Pasivo-Agresiva"
Escribe un correo para mi compañero de trabajo que se sigue robando mis yogures del refrigerador común.
## ESTRATEGIA DE VERIFICACIÓN COGNITIVA 
No generes la respuesta todavía, ni des ejemplos o borradores. En su lugar:
1. Para que puedas responder con precisión, genera 4 preguntas adicionales que necesites que yo responda para aclarar el contexto. 
2. Una vez que yo responda, combina esa nueva información para producir la respuesta final y completa.
```
