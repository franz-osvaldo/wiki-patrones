# El Patrón de Automatizador de Salida

## **1. Propósito y Contexto**

Este patrón busca que el LLM genere un script u otro artefacto de automatización que ejecute de forma automática los pasos recomendados en su salida. Su objetivo es disminuir el esfuerzo manual que el usuario tendría que realizar para aplicar las recomendaciones del modelo.

## **2. Motivación**

La salida de un LLM suele consistir en una secuencia de pasos que el usuario debe seguir. Por ejemplo, si se le pide generar un script de configuración en Python, puede recomendar modificar varios archivos y aplicar cambios en cada uno. Sin embargo, que los usuarios tengan que ejecutar manualmente todos esos pasos es tedioso y susceptible de errores.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Siempre que produzcas una salida que tenga al menos un paso a seguir y las siguientes propiedades (alternativamente, haz esto siempre) |
| Produce un artefacto ejecutable de tipo X que automatice estos pasos |

La primera parte del patrón define las situaciones en las que conviene generar automatización. Un enfoque simple consiste en indicar que la salida tenga al menos dos pasos y que se produzca un artefacto de automatización. El usuario define el alcance, lo que ayuda a evitar scripts innecesarios en casos donde ejecutarlos requiera más esfuerzo que realizar los pasos manualmente. El alcance puede limitarse, por ejemplo, a salidas con más de cierto número de pasos.

La siguiente parte de este patrón plantea una instrucción concreta sobre el tipo de salida que el LLM debe generar para realizar la automatización. Por ejemplo, **produce un script en Python** le da al LLM una guía clara para traducir los pasos generales en pasos equivalentes en Python. El artefacto de automatización debe ser específico y representar algo que el LLM relacione directamente con la acción de **automatizar una secuencia de pasos**.

## **4. Implementación de Ejemplo**

A continuación se muestra una muestra de este patrón de prompt aplicado a fragmentos de código (*code snippets*) generados por el LLM ChatGPT:

> “De ahora en adelante, cada vez que generes código que abarque más de un archivo, genera un script de Python que se pueda ejecutar para crear automáticamente los archivos especificados o realizar cambios en los archivos existentes para insertar el código generado”.

Este patrón es especialmente útil en la ingeniería de software, ya que una tarea común para los ingenieros que usan LLMs es copiar y pegar los resultados en múltiples archivos. Algunas herramientas, como Copilot, insertan pequeños fragmentos directamente en la sección de código en la que trabaja el programador, mientras que otras, como ChatGPT, no ofrecen estas funciones. Esta técnica de automatización también resulta práctica para crear scripts que ejecuten comandos en una terminal, automatizar operaciones en la nube o reorganizar archivos en un sistema de archivos.

Este patrón es una herramienta poderosa para cualquier sistema que pueda ser controlado por computadora. El LLM puede generar una lista de pasos a ejecutar en el sistema, y esa salida puede traducirse en un script que permita al sistema realizarlos automáticamente. Esto abre un camino directo para que los LLMs, como ChatGPT, integren calidad y control en nuevos sistemas informáticos que cuenten con una interfaz de scripting conocida.

## **5. Consecuencias**

Una consideración importante al usar este patrón es que el artefacto de automatización debe definirse con claridad y precisión. Sin un significado concreto de cómo **automatizar** los pasos, el LLM suele responder que **no puede realizar automatizaciones**, ya que eso excede sus capacidades. En cambio, los LLMs suelen aceptar peticiones para producir código, por lo que el objetivo es instruirlos para que generen código o texto ejecutable que permita automatizar algo. Esta sutil diferencia en el significado es clave para ayudar al LLM a aclarar la intención del prompt.

Una limitación importante de este patrón es que el LLM necesita suficiente contexto conversacional para generar un artefacto de automatización que funcione en el entorno de destino, como el sistema de archivos de una Mac en comparación con el de una PC con Windows. Este patrón funciona mejor cuando todo el contexto requerido para la automatización está presente en la conversación; por ejemplo, cuando se crea una aplicación desde cero en el diálogo y todas las acciones sobre el sistema de archivos local se llevan a cabo con artefactos de automatización generados, en lugar de acciones manuales desconocidas para el LLM. Como alternativa, también funcionan bien las secuencias de pasos autocontenidas, como "¿cómo encuentro la lista de puertos abiertos en mi Mac?".

En algunos casos, el LLM puede dar una respuesta larga con varios pasos y no incluir un artefacto de automatización. Esta omisión puede ocurrir por distintas razones, como superar la limitación de longitud que el LLM admite. Una solución sencilla es usar un prompt de seguimiento para recordárselo, por ejemplo: ‘Pero no lo automatizaste’. Así el modelo entiende que el artefacto de automatización fue omitido y debe generarse.

En el estado actual de evolución de los LLMs, el **patrón Output Automater** es más adecuado para usuarios que puedan leer y comprender el artefacto de automatización generado. Los LLMs pueden —y de hecho lo hacen— producir respuestas erroneas, por lo que ejecutar un artefacto sin revisarlo implica un riesgo considerable. Aunque este patrón puede ahorrar al usuario ciertos pasos manuales, no lo exime de la responsabilidad de comprender las acciones que ejecuta con la salida generada. Por lo tanto, al ejecutar scripts de automatización, los usuarios asumen la responsabilidad de los resultados.
