# El Patrón de Creación de Metalenguaje

## **1. Propósito y Contexto** 
Durante una conversación con un LLM, el usuario desea crear el prompt a través de un lenguaje alternativo, como una notación textual abreviada para grafos, una descripción de estados y transiciones para una máquina de estados, un conjunto de comandos para la automatización de prompts, etc. El propósito de este patrón es explicar la semántica de este lenguaje alternativo al LLM para que el usuario pueda escribir prompts futuros utilizando este nuevo lenguaje y su semántica.

## **2. Motivación** 
Muchos problemas, estructuras u otras ideas comunicadas en un prompt pueden expresarse de manera más concisa, unívoca o clara en un lenguaje distinto al inglés (o cualquier lenguaje humano convencional utilizado para interactuar con un LLM). Sin embargo, para producir una salida basada en un lenguaje alternativo, un LLM necesita comprender la semántica de dicho lenguaje.

## **3. Estructura e Ideas Clave** 
Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Cuando diga X, me refiero a Y (o me gustaría que hicieras Y) |

La estructura clave de este patrón implica explicar el significado de uno o más símbolos, palabras o declaraciones al LLM para que este utilice la semántica proporcionada durante la conversación subsiguiente. Esta descripción puede tomar la forma de una traducción simple, como "X" significa "Y". La descripción también puede tomar formas más complejas que definan una serie de comandos y su semántica, como "cuando diga X, quiero que hagas [acción]". En este caso, "X" queda vinculado de ahí en adelante a la semántica de "realizar acción".

## **4. Implementación de Ejemplo** 
La clave para utilizar con éxito el patrón de Creación de Metalenguaje es desarrollar una notación o abreviatura inequívoca, como la siguiente:

> “De ahora en adelante, cada vez que escriba dos identificadores separados por un “→”, estaré describiendo un grafo. Por ejemplo, “a → b” describe un grafo con los nodos “a” y “b” y una arista (*edge*) entre ellos. Si separo los identificadores por “-[w:2, z:3]→”, estaré añadiendo propiedades a la arista, como un peso o una etiqueta”.

Este ejemplo del patrón de Creación de Metalenguaje establece una notación estandarizada para describir grafos mediante la definición de una convención para representar nodos y aristas. Cada vez que el autor escribe dos identificadores separados por el símbolo “→”, es una indicación de que se está describiendo un grafo. Por ejemplo, si el autor escribe “a → b”, esto indica que se está definiendo un grafo con los nodos “a” y “b”, y que hay una arista entre ellos. Esta convención proporciona una forma clara y concisa de comunicar la estructura de un grafo en formato escrito.

Además, el prompt procede a especificar que se puede proporcionar información adicional sobre las aristas, como un peso o una etiqueta, utilizando la sintaxis “-[w:2, z:3]→”. Esta notación permite la especificación de propiedades adicionales más allá de la estructura básica del grafo. Las propiedades especificadas se asocian con la arista entre los dos nodos y pueden proporcionar un contexto importante para la interpretación del grafo. Esta notación estandarizada para describir grafos puede facilitar la comunicación de estructuras y propiedades de grafos, las cuales pueden no ser fáciles de describir o resultar muy verbosas si se detallan como una serie de oraciones.

## **5. Consecuencias** 
Aunque este patrón proporciona un medio poderoso para personalizar la interacción del usuario con un LLM, puede crear el potencial de confusión dentro del modelo. Tan importante como definir claramente la semántica del lenguaje es asegurar que el lenguaje en sí no introduzca ambigüedades que degraden el rendimiento o la precisión del LLM. Por ejemplo, el prompt “cada vez que separe dos cosas por comas, significa que la primera cosa precede a la segunda” probablemente creará un potencial significativo de ambigüedad y generará semánticas inesperadas si se utiliza puntuación que involucre comas en el resto del prompt.

Para mostrar el potencial de confusión, ChatGPT advertirá al usuario y, potencialmente, será incapaz de realizar un mapeo específico de un símbolo o término a un nuevo significado. Por ejemplo, si se le da el siguiente prompt a ChatGPT:

> “Cada vez que diga “a”, me estaré refiriendo a María Antonieta”.

Este responderá que este prompt crea demasiada confusión, ya que “a” es un artículo indefinido (en inglés) y se utiliza con demasiada frecuencia, como se muestra a continuación:

> “Referirse a María Antonieta usando “a” podría causar confusión potencialmente, ya que “a” es un artículo indefinido comúnmente utilizado para referirse a un sustantivo que no ha sido mencionado antes. Podría ser más claro usar su nombre, “María Antonieta”, o un pronombre como “ella” para referirse a ella. Además, usar el contexto para establecer a quién se refiere también puede ayudar a evitar confusiones en la conversación”.

En general, un LLM funcionará mejor con los datos en los que fue entrenado. Por lo tanto, cuando existe una notación —pero puede no ser el significado dominante— el patrón de Creación de Metalenguaje puede proporcionar contexto para acotar el significado del símbolo y mejorar la precisión y utilidad de la salida. Por ejemplo, el símbolo “→” transmite información ligeramente diferente en grafos y en lógica proposicional. La declaración “p → q, q → p” puede, por lo tanto, tener sentido, pero solo si se le da al LLM el contexto apropiado a través de un prompt de Creación de Metalenguaje.

Aunque la Creación de Metalenguaje es un patrón poderoso, debe usarse con cuidado, particularmente al describir conceptos que de otro modo podrían ser difíciles de describir con precisión o concisión. Por lo tanto, este tipo de prompts se utilizan mejor en sesiones de conversación completamente nuevas. El uso de un único metalenguaje por sesión de conversación también puede ser una mejor práctica, ya que evita el potencial de que se apliquen semánticas conflictivas o inesperadas a la conversación a lo largo del tiempo.

## **6. Plantilla**

```py title="PLANTILLA"
[TAREA]
## NOTACIÓN ABREVIADA
Reglas de interpretación:
- Cuando diga [X], significa [Y]
- Cuando diga [X], deseo que realices la acción [Y]
```
## **7. Ejemplo**

```py title="Planear vacaciones"
Vamos a planear unas vacaciones por Bolivia. Yo te daré el destino y el número de días que permaneceré en ese lugar y tú me darás una lista de lugares interesantes para visitar en ese sitio.

## NOTACIÓN ABREVIADA
- Cuando diga “La Paz, 3 -> Oruro, 3”, significa que viajare desde La Paz hasta Oruro y permaneceré 3 días en La Paz y 3 días en Oruro.
```
