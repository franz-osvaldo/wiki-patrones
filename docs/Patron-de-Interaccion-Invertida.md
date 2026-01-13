# El Patrón de Interacción Invertida

## **1. Propósito y Contexto**

Se desea que el LLM formule preguntas para obtener la información necesaria para realizar una tarea. En lugar de que el usuario conduzca la conversación, se busca que el LLM la dirija para enfocarse en lograr un objetivo específico. Por ejemplo, es posible que desee que el LLM le haga una prueba rápida o que le formule preguntas automáticamente hasta reunir suficiente información para generar un script de despliegue para su aplicación en un entorno de nube particular.

## **2. Motivación**

En lugar de que el usuario dirija la conversación, un LLM a menudo posee conocimientos que puede aprovechar para obtener información del usuario con mayor precisión. El objetivo del patrón de Interacción Invertida es **invertir** el flujo de la interacción para que sea el LLM quien haga preguntas al usuario con el fin de alcanzar una meta deseada. A menudo, el LLM puede seleccionar mejor el formato, la cantidad y el contenido de las interacciones para garantizar que el objetivo se alcance más rápido, con mayor precisión y/o utilizando conocimientos que el usuario podría no poseer inicialmente.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Me gustaría que me hicieras preguntas para lograr X |
| Debes hacer preguntas hasta que se cumpla esta condición o para lograr este objetivo (alternativamente, indefinidamente) |
| (Opcional) hazme las preguntas de una en una, de dos en dos, etc. |

Un *prompt* para una interacción invertida siempre debe especificar el objetivo de la interacción. La primera idea (que el LLM haga preguntas para lograr un objetivo) comunica esta meta al modelo. Igualmente importante es que las preguntas se centren en un tema o resultado particular. Al proporcionar el objetivo, el LLM puede entender qué se intenta lograr y adaptar sus preguntas en consecuencia. Esta "inversión de control" permite una interacción más enfocada y eficiente, ya que el LLM solo formulará las preguntas que considere relevantes para lograr el objetivo especificado.

La segunda idea proporciona el contexto sobre la duración de la interacción. Una interacción invertida puede terminarse con una respuesta como "deja de hacer preguntas". Sin embargo, a menudo es mejor acotar la interacción a una longitud razonable o hasta alcanzar la meta. Este objetivo puede ser sorprendentemente **abierto** (*open-ended*), y el LLM continuará trabajando hacia la meta haciendo preguntas, como ocurre en el ejemplo de "hasta que tengas suficiente información para generar un script de Python" .

Por defecto, es probable que el LLM genere múltiples preguntas por iteración. La tercera idea es opcional, pero puede mejorar la usabilidad al limitar (o expandir) el número de preguntas que el LLM genera por ciclo. Si no se especifica un número o formato preciso para la **secuencia de preguntas**, este será semi-aleatorio (ej. de una en una o de diez en diez). Por lo tanto, el *prompt* puede adaptarse para incluir el número de preguntas formuladas a la vez y su orden para facilitar la interacción .

## **4. Implementación de Ejemplo**

A continuación se muestra un ejemplo de prompt para una interacción invertida:

> “De ahora en adelante, me gustaría que me hicieras preguntas para desplegar una aplicación de Python en AWS. Cuando tengas suficiente información para desplegar la aplicación, crea un script de Python para automatizar el despliegue”.

En general, cuanto más específico sea el *prompt* respecto a las restricciones e información a recopilar, mejor será el resultado. Por ejemplo, el *prompt* anterior podría proporcionar un menú de servicios de AWS posibles (como Lambda, EC2, etc.). En otros casos, se puede permitir que el LLM simplemente tome decisiones apropiadas por su cuenta sobre aspectos que el usuario no decida explícitamente.

Una limitación de este *prompt* es que, una vez proporcionada otra información contextual, puede requerir experimentación con el fraseo preciso para lograr que el LLM haga las preguntas en el número y flujo adecuados (ej. múltiples preguntas a la vez frente a una por turno).

## **5. Consecuencias**

Una consideración al diseñar el *prompt* es cuánto dictar al LLM sobre la información a recopilar antes de finalizar. En el ejemplo anterior, la interacción es abierta, lo que hace al *prompt* genérico y reutilizable, pero podría derivar en preguntas innecesarias si se omite contexto clave.

Si se conocen requisitos específicos de antemano, es mejor inyectarlos en el *prompt* en lugar de esperar que el LLM los deduzca. De lo contrario, el LLM decidirá de manera no determinista si solicitar la información o realizar una **conjetura fundamentada** sobre un valor apropiado. Por ejemplo, especificar "desplegar en Amazon AWS EC2" evita múltiples rondas de preguntas para acotar el objetivo "la nube". Cuanto más precisa sea la información inicial, mejor podrá usar el LLM las preguntas limitadas para mejorar su salida.

Al desarrollar *prompts* para interacciones invertidas, es importante considerar el nivel de conocimiento, compromiso y control del usuario. Si el objetivo es minimizar la interacción del usuario (control mínimo) o maximizar su confirmación de decisiones (compromiso máximo), esto debe indicarse explícitamente. Asimismo, si se espera que el usuario tenga un conocimiento mínimo, esta restricción debe **incorporarse explícitamente en el diseño** del *prompt* para ajustar el nivel de las preguntas .

## **6. Plantilla**

```py title="PLANTILLA"
[OBJETIVO GENERAL]
## ESTRATEGIA DE INTERACCIÓN INVERTIDA(FLIPPED INTERACTION)

No generes la respuesta todavía, ni des ejemplos o borradores.  En su lugar:

1. Pregúntame todo lo que necesites saber para completar la tarea con la máxima calidad.
2. Haz las preguntas de una en una y espera mi respuesta antes de hacer la siguiente.
3. Continúa preguntando hasta que tengas suficiente información. Solo entonces, genera el RESULTADO FINAL.

Hazme la primera pregunta.
```

## **7. Ejemplos**

```py title="Haz lo que quieras"
Ayúdame a interpretar qué quiso decir mi novia con su último mensaje: "Haz lo que quieras 👍"

## ESTRATEGIA DE INTERACCIÓN INVERTIDA(FLIPPED INTERACTION)

No generes la respuesta todavía, ni des ejemplos o borradores.  En su lugar:

1. Pregúntame todo lo que necesites saber para completar la tarea con la máxima calidad.
2. Haz las preguntas de una en una y espera mi respuesta antes de hacer la siguiente.
3. Continúa preguntando hasta que tengas suficiente información. Solo entonces, genera el RESULTADO FINAL.

Hazme la primera pregunta. 
```

```py title="Crítica artística profunda"
Generar una crítica artística profunda, filosófica y exageradamente compleja (al estilo de un curador de museo snob) sobre un dibujo objetivamente feo que acaba de hacer un niño de 4 años.

## ESTRATEGIA DE INTERACCIÓN INVERTIDA(FLIPPED INTERACTION)

No generes la respuesta todavía, ni des ejemplos o borradores.  En su lugar:

1. Pregúntame todo lo que necesites saber para completar la tarea con la máxima calidad.
2. Haz las preguntas de una en una y espera mi respuesta antes de hacer la siguiente.
3. Continúa preguntando hasta que tengas suficiente información. Solo entonces, genera el RESULTADO FINAL.

Hazme la primera pregunta. 
```
