# El Patrón de Creación de Metalenguaje

## **1. Propósito y Contexto**

En una conversación con un LLM, el usuario desea redactar prompts usando un lenguaje alternativo: por ejemplo, una notación textual abreviada para grafos, una descripción de estados y transiciones de un autómata, o un conjunto de comandos para automatizar prompts. La intención de este patrón es enseñar al LLM la semántica de ese lenguaje alternativo para que, a partir de ahí, el usuario pueda usarlo en prompts posteriores.

## **2. Motivación**

Muchos problemas, estructuras e ideas se pueden expresar de manera más concisa, clara o no ambigua en un lenguaje distinto del lenguaje natural. Pero, para generar output coherente a partir de ese lenguaje alternativo, el LLM necesita comprender qué significa.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Cuando diga X, me refiero a Y (o me gustaría que hicieras Y) |

La idea central es definir el significado de uno o más símbolos, palabras o expresiones para que el modelo los interprete con esa semántica durante el resto de la conversación. A veces basta con una traducción simple como "X significa Y"; otras veces se define un conjunto de "comandos" del tipo "cuando diga X, realiza la acción Y".

## **4. Implementación de Ejemplo**

La clave para aplicar bien este patrón es crear una notación no ambigua, por ejemplo:

> “De ahora en adelante, cada vez que escriba dos identificadores separados por un “→”, estaré describiendo un grafo. Por ejemplo, “a → b” describe un grafo con los nodos “a” y “b” y una arista (*edge*) entre ellos. Si separo los identificadores por “-[w:2, z:3]→”, estaré añadiendo propiedades a la arista, como un peso o una etiqueta”.

Aquí se establece una convención para representar nodos y aristas con “→”, y se añade una sintaxis para adjuntar atributos (como pesos o etiquetas) a las aristas, manteniendo la descripción compacta y estructurada.

## **5. Consecuencias**

Aunque este patrón ofrece un medio potente para personalizar la interacción del usuario con un LLM, puede dar lugar a confusiones dentro del modelo. Si bien es crucial definir claramente la semántica del lenguaje, resulta igualmente esencial asegurar que el lenguaje en sí mismo no introduzca ambigüedades que degraden el rendimiento o la precisión del LLM. Por ejemplo, el prompt "siempre que separe dos cosas por comas, significa que la primera precede a la segunda" probablemente generará una ambigüedad significativa y producirá una semántica inesperada si se utiliza la coma como signo de puntuación en el prompt.

Para ilustrar este riesgo de confusión, ChatGPT advertirá al usuario y podría no lograr asociar un símbolo o término específico a un nuevo significado. Por ejemplo, si se proporciona el siguiente prompt a ChatGPT:

> “Cada vez que diga “a”, me estaré refiriendo a María Antonieta”.

El modelo responderá que este prompt genera excesiva confusión, dado que "a" es un artículo indefinido (en inglés) de uso muy frecuente, tal como se muestra a continuación

> "Referirse a María Antonieta usando 'a' podría causar confusión, ya que 'a' es un artículo indefinido comúnmente usado para referirse a un sustantivo que no ha sido mencionado antes. Sería más claro usar su nombre, 'María Antonieta', o un pronombre como 'ella' (she / her) para referirse a ella. Además, usar el contexto para establecer a quién te refieres también puede ayudar a evitar confusiones en la conversación."

En general, un LLM funcionará mejor con los datos con los que fue entrenado. Por lo tanto, cuando existe una notación disponible —aunque no sea el significado dominante— el patrón de Creación de Metalenguaje puede proporcionar el contexto necesario para acotar el significado del símbolo, mejorando así la precisión y utilidad de la salida. Por ejemplo, el símbolo **→** transmite información ligeramente diferente en la teoría de grafos y en la lógica proposicional. La declaración **p → q → p** podría tener sentido, pero solo si se le da al LLM el contexto apropiado a través de un prompt de Creación de Metalenguaje.

Aunque la Creación de Metalenguaje es un patrón poderoso, debe emplearse con cautela, particularmente al describir conceptos que de otro modo serían difíciles de expresar con precisión o concisión. Estos tipos de prompts funcionan mejor en sesiones de conversación completamente nuevas. Adoptar la práctica de "un solo metalenguaje por sesión" es recomendable, ya que evita el riesgo de que se apliquen semánticas conflictivas o inesperadas a la conversación a lo largo del tiempo.

## **6. Plantilla**

```py title="PLANTILLA"
[TAREA]
## NOTACIÓN ABREVIADA
- Cuando diga [X], significa [Y]
- Cuando diga [X], deseo que realices la acción [Y]
```

## **7. Ejemplo**

```py title="Planear vacaciones"
Vamos a planear unas vacaciones por Bolivia. Yo te daré el destino y el número de días que permaneceré en ese lugar y tú me darás una lista de lugares interesantes para visitar en ese sitio.

## NOTACIÓN ABREVIADA
- Cuando diga “La Paz, 3 -> Oruro, 3”, significa que viajare desde La Paz hasta Oruro y permaneceré 3 días en La Paz y 3 días en Oruro.
```
