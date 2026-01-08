# El Patrón de Interacción Invertida

## **1. Propósito y Contexto**
Usted desea que el LLM le haga preguntas para obtener la información que necesita para realizar algunas tareas. Por lo tanto, en lugar de que el usuario dirija la conversación, usted desea que el LLM la dirija para centrarla en el logro de un objetivo específico. Por ejemplo, puede querer que el LLM le haga un cuestionario rápido o que le haga preguntas automáticamente hasta que tenga información suficiente para generar un script de despliegue para su aplicación en un entorno de nube particular.

## **2. Motivación**
En lugar de que el usuario dirija una conversación, un LLM a menudo tiene conocimientos que puede utilizar para obtener información del usuario de forma más precisa. El objetivo del patrón de Interacción Invertida es invertir el flujo de la interacción para que el LLM le haga preguntas al usuario para alcanzar algún objetivo deseado. A menudo, el LLM puede seleccionar mejor el formato, el número y el contenido de las interacciones para garantizar que el objetivo se alcance más rápidamente, con mayor precisión y/o utilizando conocimientos que el usuario puede no poseer (inicialmente).

## **3. Estructura e Ideas Clave**
Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Me gustaría que me hicieras preguntas para lograr X |
| Debes hacer preguntas hasta que se cumpla esta condición o para lograr este objetivo (alternativamente, para siempre) |
| (Opcional) hazme las preguntas de una en una, de dos en dos, etc. |

Un prompt para una interacción invertida siempre debe especificar el objetivo de la interacción. La primera idea (es decir, que usted desea que el LLM haga preguntas para alcanzar un objetivo) comunica este propósito al LLM. Igualmente importante es que las preguntas se centren en un tema o resultado particular. Al proporcionar el objetivo, el LLM puede comprender lo que está tratando de lograr a través de la interacción y adaptar sus preguntas en consecuencia. Esta “inversión de control” permite una interacción más centrada y eficiente, ya que el LLM solo hará las preguntas que considere relevantes para alcanzar el objetivo especificado.

La segunda idea proporciona el contexto sobre cuánto tiempo debe durar la interacción. Una interacción invertida puede terminarse con una respuesta como “deja de hacer preguntas”. Sin embargo, a menudo es mejor acotar la interacción a una longitud razonable o solo hasta donde sea necesario para alcanzar el objetivo. Este objetivo puede ser sorprendentemente abierto y el LLM continuará trabajando hacia la meta haciendo preguntas, como es el caso en el ejemplo de “hasta que tengas suficiente información para generar un script de Python”.

Por defecto, es probable que el LLM genere múltiples preguntas por iteración. La tercera idea es completamente opcional, pero puede mejorar la usabilidad al limitar (o ampliar) el número de preguntas que el LLM genera por ciclo. Si no se especifica un número/formato preciso para el interrogatorio, este será semi-aleatorio y puede dar lugar a preguntas de una en una o de diez en diez. El prompt puede, por lo tanto, adaptarse para incluir el número de preguntas realizadas a la vez, el orden de las preguntas y cualquier otra consideración de formato/orden para facilitar la interacción del usuario.

## **4. Implementación de Ejemplo**
A continuación se muestra un ejemplo de prompt para una interacción invertida:

> “De ahora en adelante, me gustaría que me hicieras preguntas para desplegar una aplicación de Python en AWS. Cuando tengas suficiente información para desplegar la aplicación, crea un script de Python para automatizar el despliegue”.

En general, cuanto más específico sea el prompt respecto a las restricciones y la información a recopilar, mejor será el resultado. Por ejemplo, el prompt de ejemplo anterior podría proporcionar un menú de posibles servicios de AWS (como Lambda, EC2, etc.) con los que desplegar la aplicación. En otros casos, se puede permitir que el LLM simplemente tome decisiones apropiadas por su cuenta para cosas sobre las que el usuario no toma decisiones explícitamente. Una limitación de este prompt es que, una vez proporcionada otra información contextual sobre la tarea, puede requerir experimentación con la redacción precisa para conseguir que el LLM haga las preguntas en el número y flujo que mejor se adapte a la tarea, como pedir varias preguntas a la vez frente a una sola pregunta a la vez.

## **5. Consecuencias**
Una consideración al diseñar el prompt es cuánto dictar al LLM respecto a qué información recopilar antes de finalizar. En el ejemplo anterior, la interacción invertida es abierta y puede variar significativamente en el artefacto final generado. Esta naturaleza abierta hace que el prompt sea genérico y reutilizable, pero puede pedir potencialmente preguntas adicionales que podrían omitirse si se diera más contexto.

Si se conocen requisitos específicos de antemano, es mejor inyectarlos en el prompt en lugar de esperar que el LLM obtenga la información necesaria. De lo contrario, el LLM decidirá de forma no determinista si solicita la información al usuario o hace una suposición educada sobre el valor apropiado.

Por ejemplo, el usuario puede declarar que le gustaría desplegar una aplicación en Amazon AWS EC2, en lugar de simplemente decir “la nube” y requerir múltiples interacciones para estrechar el objetivo del despliegue. Cuanto más precisa sea la información inicial, mejor podrá el LLM utilizar las limitadas preguntas que un usuario probablemente esté dispuesto a responder para obtener información que mejore su salida.

Al desarrollar prompts para interacciones invertidas, es importante considerar el nivel de conocimiento, participación y control del usuario. Si el objetivo es cumplir la meta con la menor interacción posible del usuario (control mínimo), eso debe establecerse explícitamente. Por el contrario, si el objetivo es asegurar que el usuario sea consciente de todas las decisiones clave y las confirme (participación máxima), eso también debe establecerse explícitamente. Del mismo modo, si se espera que el usuario tenga conocimientos mínimos y las preguntas deben estar dirigidas a su nivel de experiencia, esta información debe integrarse en el prompt.
