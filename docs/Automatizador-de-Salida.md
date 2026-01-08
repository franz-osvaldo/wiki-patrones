# El Patrón de Automatizador de Salida

## **1. Propósito y Contexto** 
El propósito de este patrón es hacer que el LLM genere un script u otro artefacto de automatización que pueda realizar automáticamente cualquier paso que recomiende como parte de su salida. El objetivo es reducir el esfuerzo manual necesario para implementar cualquier recomendación de salida del LLM.

## **2. Motivación**
La salida de un LLM es a menudo una secuencia de pasos a seguir por el usuario. Por ejemplo, al pedirle a un LLM que genere un script de configuración de Python, este puede sugerir una serie de archivos a modificar y cambios a aplicar en cada uno. Sin embargo, el hecho de que los usuarios realicen continuamente los pasos manuales dictados por la salida del LLM es tedioso y propenso a errores.

## **3. Estructura e Ideas Clave** 
Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Siempre que produzcas una salida que tenga al menos un paso a seguir y las siguientes propiedades (alternativamente, haz esto siempre) |
| Produce un artefacto ejecutable de tipo X que automatice estos pasos |

La primera parte del patrón identifica las situaciones bajo las cuales se debe generar la automatización. Un enfoque simple es declarar que la salida incluye al menos dos pasos a seguir y que se debe producir un artefacto de automatización. El alcance queda a discreción del usuario, pero ayuda a evitar la producción de scripts de automatización de salida en casos donde ejecutar el script requeriría más esfuerzo del usuario que realizar los pasos originales producidos en la salida. El alcance puede limitarse a salidas que requieran más de un número determinado de pasos.

La siguiente parte de este patrón proporciona una declaración concreta del tipo de salida que el LLM debe producir para realizar la automatización. Por ejemplo, "produce un script de Python" le da al LLM una comprensión concreta para traducir los pasos generales en pasos equivalentes en Python. El artefacto de automatización debe ser concreto y debe ser algo que el LLM asocie con la acción de "automatizar una secuencia de pasos".

## **4. Implementación de Ejemplo** 
A continuación se muestra una muestra de este patrón de prompt aplicado a fragmentos de código (*code snippets*) generados por el LLM ChatGPT:

> “De ahora en adelante, cada vez que generes código que abarque más de un archivo, genera un script de Python que se pueda ejecutar para crear automáticamente los archivos especificados o realizar cambios en los archivos existentes para insertar el código generado”.

Este patrón es particularmente efectivo en ingeniería de software, ya que una tarea común para los ingenieros de software que utilizan LLMs es copiar y pegar las salidas en múltiples archivos. Algunas herramientas, como Copilot, insertan fragmentos limitados directamente en la sección de código en la que el programador está trabajando, pero herramientas como ChatGPT no proporcionan estas facilidades. Este truco de automatización también es eficaz para crear scripts para ejecutar comandos en una terminal, automatizar operaciones en la nube o reorganizar archivos en un sistema de archivos.

Este patrón es un complemento poderoso para cualquier sistema que pueda ser controlado por computadora. El LLM puede proporcionar un conjunto de pasos que deben tomarse en el sistema controlado por computadora y luego la salida puede traducirse en un script que permita al sistema controlar el proceso para tomar los pasos automáticamente. Este es un camino directo para permitir que los LLMs, como ChatGPT, integren calidad y controlen nuevos sistemas informáticos que tengan una interfaz de scripting conocida.

## **5. Consecuencias** 
Una consideración de uso importante de este patrón es que el artefacto de automatización debe definirse concretamente. Sin un significado concreto de cómo "automatizar" los pasos, el LLM a menudo declara que "no puede automatizar cosas", ya que eso está más allá de sus capacidades. Sin embargo, los LLMs suelen aceptar peticiones para producir código; por lo tanto, el objetivo es instruir al LLM para que genere texto/código que pueda ser ejecutado para automatizar algo. Esta sutil distinción en el significado es importante para ayudar a un LLM a desambiguar el significado del prompt.

Una advertencia del patrón Automatizador de Salida es que el LLM necesita suficiente contexto conversacional para generar un artefacto de automatización que sea funcional en el contexto de destino, como el sistema de archivos de un proyecto en una Mac frente a una computadora con Windows. Este patrón funciona mejor cuando todo el contexto necesario para la automatización está contenido dentro de la conversación, por ejemplo, cuando se genera una aplicación de software desde cero utilizando la conversación y todas las acciones en el sistema de archivos local se realizan utilizando una secuencia de artefactos de automatización generados, en lugar de acciones manuales desconocidas para el LLM. Alternativamente, las secuencias de pasos autónomas funcionan bien, como "¿cómo encuentro la lista de puertos abiertos en mi computadora Mac?".

En algunos casos, el LLM puede producir una salida larga con múltiples pasos y no incluir un artefacto de automatización. Esta omisión puede deberse a varias razones, incluyendo el exceso del límite de longitud de salida que el LLM admite. Una solución simple para esta situación es recordárselo al LLM a través de un prompt de seguimiento, como "Pero no lo automatizaste", lo que proporciona el contexto de que el artefacto de automatización fue omitido y debe ser generado.

En este punto de la evolución de los LLMs, el patrón Automatizador de Salida es mejor empleado por usuarios que puedan leer y comprender el artefacto de automatización generado. Los LLMs pueden producir (y de hecho producen) imprecisiones en su salida, por lo que aceptar y ejecutar ciegamente un artefacto de automatización conlleva un riesgo significativo. Aunque este patrón puede aliviar al usuario de realizar ciertos pasos manuales, no lo exime de su responsabilidad de comprender las acciones que realiza utilizando la salida. Cuando los usuarios ejecutan scripts de automatización, asumen la responsabilidad de los resultados.

