# El Patrón de Lista de Verificación de Hechos (*Fact Check List*)

## **1. Propósito y Contexto**

El propósito de este patrón es asegurar que el LLM genere una lista de los hechos presentes en la salida que forman una parte importante de las declaraciones emitidas. Esta lista de hechos ayuda a informar al usuario sobre los datos (o suposiciones) en los que se basa la salida. El usuario puede entonces realizar la debida diligencia (*due diligence*) sobre estos hechos/suposiciones para validar la veracidad de la salida.

## **2. Motivación**

Una debilidad actual de los LLMs (incluido ChatGPT) es que a menudo generan, de manera rápida (¡e incluso entusiasta!), texto convincente que es fácticamente incorrecto. Estos errores pueden adoptar una amplia gama de formas, desde estadísticas falsas hasta números de versión inválidos para dependencias de librerías de software. Debido a la naturaleza convincente de este texto generado, es posible que los usuarios no realicen la debida diligencia necesaria para determinar su exactitud.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Genera un conjunto de hechos que estén contenidos en la salida |
| El conjunto de hechos debe insertarse en un punto específico de la salida |
| El conjunto de hechos debe ser de los hechos fundamentales que podrían socavar la veracidad de la salida si alguno de ellos fuera incorrecto |

Un punto de variación en este patrón es dónde se presentan los hechos. Dado que los hechos pueden ser términos con los que el usuario no está familiarizado, es preferible que la lista de hechos aparezca después de la salida. Este orden de presentación posterior a la salida permite al usuario leer y comprender las declaraciones antes de ver qué afirmaciones deben verificarse. El usuario también puede determinar hechos adicionales antes de darse cuenta de que la lista de hechos al final debe ser verificada.

## **4. Implementación de Ejemplo**

A continuación se muestra una redacción de ejemplo del patrón de Lista de Verificación de Hechos:

> “De ahora en adelante, cuando generes una respuesta, crea un conjunto de hechos de los que dependa la respuesta que deban ser verificados y enumera este conjunto de hechos al final de tu salida. Solo incluye hechos relacionados con la ciberseguridad”.

El usuario puede tener experiencia en algunos temas relacionados con la pregunta, pero no en otros. La lista de verificación de hechos puede adaptarse a temas en los que el usuario no tiene tanta experiencia o donde existe el mayor riesgo. Por ejemplo, en el prompt anterior, el usuario está delimitando la lista de verificación de hechos a temas de seguridad, ya que estos son probablemente muy importantes desde una perspectiva de riesgo y pueden no ser bien comprendidos por el desarrollador. Dirigir los hechos de esta manera también reduce la carga cognitiva del usuario al listar potencialmente menos elementos para investigar.

## **5. Consecuencias**

El patrón de Lista de Verificación de Hechos debe emplearse siempre que los usuarios no sean expertos en el dominio para el cual están generando la salida. Por ejemplo, un desarrollador de software que revisa código podría beneficiarse del patrón que sugiere consideraciones de seguridad. Por el contrario, es probable que un experto en arquitectura de software identifique errores en las declaraciones sobre la estructura del software y no necesite ver una lista de verificación de hechos para esas salidas.

Los errores son potenciales en todas las salidas de los LLMs, por lo que la Lista de Verificación de Hechos es un patrón eficaz para combinar con otros patrones, como el de **Refinamiento de Pregunta**. Un aspecto clave de este patrón es que los usuarios pueden verificarlo inherentemente contra la salida. En particular, los usuarios pueden comparar directamente la lista de hechos con la salida para verificar si los hechos enumerados en la lista de verificación realmente aparecen en la salida. Los usuarios también pueden identificar cualquier omisión en la lista. Aunque la propia lista de verificación de hechos también puede contener errores, los usuarios suelen tener suficiente conocimiento y contexto para determinar su integridad y precisión en relación con la salida.

Una advertencia del patrón de Lista de Verificación de Hechos es que solo se aplica cuando el tipo de salida es propenso a la verificación de hechos. Por ejemplo, el patrón funciona al pedirle a ChatGPT que genere un archivo “requirements.txt” de Python, ya que enumerará las versiones de las librerías como hechos que deben verificarse, lo cual es útil dado que las versiones suelen contener errores. Sin embargo, ChatGPT se negará a generar una lista de verificación de hechos para un ejemplo de código e indicará que esto es algo que no puede verificar, a pesar de que el código pueda contener errores.
