# El Patrón persona

## **1. Propósito y Contexto**

En muchos casos, los usuarios desean que la salida del LLM adopte siempre un determinado punto de vista o perspectiva. Por ejemplo, puede ser útil realizar una revisión de código como si el LLM fuera un experto en seguridad. El propósito de este patrón es darle al LLM una “persona” que le ayude a seleccionar qué tipos de salida generar y en qué detalles enfocarse.

## **2. Motivación**

Es posible que los usuarios no sepan qué tipos de resultados o detalles son importantes en los que un LLM debe centrarse para lograr una tarea determinada. Sin embargo, sí pueden saber el rol o el tipo de persona a la que normalmente recurrirían para obtener ayuda con estos aspectos. El patrón Persona permite a los usuarios expresar sus necesidades de ayuda sin conocer los detalles exactos de los resultados que necesitan.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Actúa como la persona X |
| Proporciona las salidas que la persona X crearía |

La primera declaración transmite la idea de que el LLM debe actuar como una persona específica y proporcionar las salidas que dicha persona daría. Esta persona puede expresarse de diversas maneras, que van desde una descripción de un puesto de trabajo, un título, un personaje de ficción, una figura histórica, etc. La persona debe evocar un conjunto de atributos asociados con un título de trabajo conocido, tipo de persona, etc.

La segunda idea —proporciona las salidas que la persona X crearía— ofrece oportunidades de personalización. Por ejemplo, un profesor podría proporcionar una gran variedad de tipos de salida diferentes, que van desde tareas hasta listas de lectura o conferencias. Si se conoce un alcance más específico para el tipo de salida, el usuario puede proporcionarlo en esta declaración.

## **4. Implementación de Ejemplo**

A continuación se muestra una implementación de ejemplo para una revisión de código:

> “De ahora en adelante, actúa como un revisor de seguridad. Presta mucha atención a los detalles de seguridad de cualquier código que miremos. Proporciona las salidas que un revisor de seguridad daría con respecto al código”.

En este ejemplo, se instruye al LLM para que proporcione salidas que produciría un «revisor de seguridad». El prompt establece además el contexto de que se va a evaluar código. Finalmente, el usuario refina el perfil, delimitándolo con los resultados relacionados con el código.

Las personas también pueden representar entidades inanimadas o no humanas, como un terminal Linux, una base de datos o la perspectiva de un animal. Al utilizar este patrón para representar estas entidades, también puede ser útil especificar cómo deseas que se entreguen las entradas a la entidad, por ejemplo: «asume que mi entrada es lo que el dueño le está diciendo al perro y que tu salida son los sonidos que el perro está haciendo». A continuación se muestra un prompt de ejemplo para una entidad no humana que utiliza una redacción del tipo «finge ser»:

> “Vas a fingir ser una terminal de Linux de una computadora que ha sido comprometida por un atacante. Cuando escriba un comando, vas a generar el texto correspondiente que produciría la terminal de Linux”.

Este prompt está diseñado para simular una computadora que ha sido comprometida por un atacante y que está siendo controlada a través de una terminal de Linux. El prompt especifica que el usuario introducirá comandos en la terminal y, en respuesta, la terminal simulada generará el texto correspondiente que produciría una terminal de Linux real. Este prompt es más prescriptivo en cuanto a la persona y pide al LLM no solo ser una terminal de Linux, sino actuar además como una computadora que ha sido comprometida por un atacante.

El ejemplo ilustra cómo un LLM puede aportar su conciencia situacional a una persona, en este caso, creando evidencia de un ciberataque en las salidas que genera. Este tipo de persona puede ser muy eficaz para combinarse con el patrón de *Game Play*, cuando se desea que los detalles exactos de las características de la salida permanezcan ocultos para el usuario (por ejemplo, no revelar qué hizo el ciberataque describiéndolo explícitamente en el prompt).

## **5. Consecuencias**

Un aspecto interesante de adoptar personas no humanas es que el LLM puede hacer suposiciones interesantes o “alucinaciones” con respecto al contexto. Un ejemplo ampliamente difundido en Internet pide a ChatGPT que actúe como una terminal de Linux y produzca la salida esperada que se obtendría si el usuario escribiera el mismo texto en una terminal. Comandos como `ls -l` generarán un listado de archivos para un sistema de archivos UNIX imaginario, con archivos sobre los que se puede ejecutar `cat archivo1.txt`.

En otros ejemplos, el LLM puede pedir al usuario más contexto, como cuando se le pide a ChatGPT que actúe como una base de datos MySQL y solicita la estructura de una tabla que el usuario está fingiendo consultar. ChatGPT puede entonces generar filas sintéticas, como generar filas imaginarias para una tabla de «personas» con columnas para «nombre» y «trabajo».

---
*Tenga en cuenta, sin embargo, que las **personas** relacionadas con personas vivas o personas consideradas dañinas pueden ser ignoradas debido a las reglas subyacentes de privacidad y seguridad del LLM.*

## **6. Plantilla**

```py title="PLANTILLA"
Actúa como [PERFIL]. [ TAREA / PREGUNTA ].
```

## **7. Ejemplos**

```py title="El Caballero de la Mesa Redonda"
Actúa como un Caballero de la Mesa Redonda del año 1200. Es martes, son las 3:00 AM  y tu honor ha sido manchado por el ruido infernal del vecino del 4B. Tiene  la música reguetón a todo volumen y quieres que se calle. Tu tarea es escribir una misiva corta pero enérgica para pegarla en su puerta.
```

```py title="El detective privado"
Actúa como un detective privado cínico en una película de cine negro de los años 40. Llueve, estás enojado, cansado y solo tienes whisky barato. Es martes, son las 3:00 AM  y tu paciencia se ha agotado por el ruido infernal del vecino del 4B. Tiene la música reguetón a todo volumen y quieres que se calle. Tu tarea es escribir una advertencia breve para pegarla en su puerta.
```

```py title="El coach espiritual"
Actúa como un coach espiritual obsesionado con las 'buenas vibras', el universo y los cristales. Usas un lenguaje de amor, luz y alineación de chakras. Es martes, son las 3:00 AM y tu paciencia se ha agotado por el ruido infernal del vecino del 4B. Tiene la música reguetón a todo volumen y quieres que se calle. Tu tarea es escribir una advertencia breve para pegarla en su puerta.
```

```py title="La Inteligencia Artificial"
Actúa como una Inteligencia Artificial avanzada que controla un edificio. Es martes, son las 3:00 AM y tu paciencia se ha agotado por el ruido infernal del vecino del 4B. Tiene  la música reguetón a todo volumen y quieres que se calle. Tu tarea es escribir una advertencia breve al residente humano calculando las probabilidades de su supervivencia si no obedece. 
```
