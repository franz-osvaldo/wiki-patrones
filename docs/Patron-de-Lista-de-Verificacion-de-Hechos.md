# El Patrón de Lista de Verificación de Hechos (*Fact Check List*)

## **1. Propósito y Contexto**

El propósito de este patrón es asegurar que el LLM genere una lista de los hechos presentes en la salida y que forman una parte importante de las declaraciones en dicha salida. Esta lista de hechos ayuda a informar al usuario sobre los datos (o suposiciones) en los que se basa la salida. El usuario puede entonces realizar la debida diligencia (*due diligence*) sobre estos hechos/suposiciones para validar la veracidad de la salida.

## **2. Motivación**

Una debilidad actual de los LLMs (incluido ChatGPT) es que a menudo generan, de manera rápida (¡e incluso entusiasta!), texto convincente que es fácticamente incorrecto. Estos errores pueden adoptar una amplia gama de formas, desde estadísticas falsas hasta números de versión inválidos para dependencias de librerías de software. Debido a la naturaleza convincente de este texto generado, es posible que los usuarios no realicen la debida diligencia necesaria para determinar su exactitud.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Genera un conjunto de hechos que estén contenidos en la salida |
| El conjunto de hechos debe insertarse en un punto específico de la salida |
| El conjunto de hechos debe componerse de los hechos fundamentales que podrían socavar la veracidad de la salida si alguno de ellos fuera incorrecto |

Una diferencia posible en la aplicación del patrón está en dónde se presentan los hechos dentro de la salida del modelo. Como los hechos pueden incluir términos que el usuario no conoce, se sugiere que la lista de hechos aparezca después del resultado principal. Este orden permite que el usuario primero lea y entienda la respuesta, y luego vea qué afirmaciones deben verificarse. Además, el usuario puede identificar hechos adicionales mientras analiza la respuesta, antes de revisar la lista final que debe comprobarse.

## **4. Implementación de Ejemplo**

A continuación se muestra un ejemplo del patrón de Lista de Verificación de Hechos:

> “De ahora en adelante, cuando generes una respuesta, crea un conjunto de hechos de los que dependa la respuesta, que deban ser verificados y enumera este conjunto de hechos al final de tu salida. Solo incluye hechos relacionados con la ciberseguridad”.

El usuario puede tener experiencia en algunos temas relacionados con la pregunta, pero no en otros. La lista de verificación de hechos puede adaptarse a temas en los que el usuario no tiene tanta experiencia o donde existe el mayor riesgo. Por ejemplo, en el prompt anterior, el usuario está delimitando la lista de verificación de hechos a temas de seguridad, ya que estos son probablemente muy importantes desde una perspectiva de riesgo y pueden no ser bien comprendidos por el desarrollador. Dirigir los hechos de esta manera también reduce la carga cognitiva del usuario al listar potencialmente menos elementos para investigar.

## **5. Consecuencias**

El patrón de Lista de Verificación de Hechos debe emplearse siempre que los usuarios no sean expertos en el dominio para el cual están generando la salida. Por ejemplo, un desarrollador de software que revisa código podría beneficiarse de que el modelo le sugiera consideraciones de seguridad mediante una lista de hechos a verificar. Por el contrario, es probable que un experto en arquitectura de software identifique errores en las declaraciones sobre la estructura del software y no necesite ver una lista de verificación de hechos para esas salidas.

Todos los modelos de lenguaje (LLM) pueden producir errores, por lo que el patrón ***Fact Check List*** resulta útil para reforzar la fiabilidad. Se sugiere combinarlo con el patrón de ***Question Refinement***, lo que permite que las respuestas sean más precisas y, además, verificables.  El patrón facilita que el usuario compare directamente la lista de hechos con la salida del modelo:

* Puede comprobar si los hechos listados realmente aparecen en la respuesta.
* Puede detectar si faltan hechos importantes (omisiones).
Aunque la lista también puede contener errores, normalmente el usuario tiene suficiente conocimiento y contexto para evaluar si es completa y correcta en relación con la salida.

Una advertencia sobre el patrón de Lista de Verificación de Hechos es que solo se aplica cuando el tipo de salida es susceptible a la verificación de hechos. Por ejemplo, el patrón funciona al pedirle a ChatGPT que genere un archivo “requirements.txt” de Python, ya que enumerará las versiones de las librerías como hechos que deben verificarse, lo cual es útil dado que las versiones suelen contener errores. Sin embargo, ChatGPT se negará a generar una lista de verificación de hechos para un ejemplo de código e indicará que esto es algo que no puede verificar, a pesar de que el código pueda contener errores.

## **6. Plantilla**

```py title="PLANTILLA"
[TAREA / PREGUNTA]
## INSTRUCCIONES DE VERIFICACIÓN
**Una vez generada la respuesta**, añade un separador y una sección titulada "✅ LISTA DE VERIFICACIÓN DE HECHOS". En ella debes detallar:
1. Extrae y enumera los hechos críticos mencionados explícitamente en tu respuesta (solo los que aparecen en el texto). Se debe incluir solo los hechos que, si fueran incorrectos, comprometerían la veracidad de la información (por ejemplo, fechas, nombres técnicos o estadísticas). 
2. Ordena los hechos de mayor a menor impacto en la confiabilidad de la respuesta.
3. Cada ítem debe ser una afirmación factual breve.
4. **Advertencia:** No agregues hechos nuevos en la lista que no estén en el texto de tu respuesta.
```

## **7. Ejemplos**

```py title="Donde un número equivocado es peligroso"
¿Cuál es la dosis segura de Paracetamol para un adulto de 70kg y cuáles son los síntomas de sobredosis?
## INSTRUCCIONES DE VERIFICACIÓN
**Una vez generada la respuesta**, añade un separador y una sección titulada "✅ LISTA DE VERIFICACIÓN DE HECHOS". En ella debes detallar:
1. Extrae y enumera los hechos críticos mencionados explícitamente en tu respuesta (solo los que aparecen en el texto). Se debe incluir solo los hechos que, si fueran incorrectos, comprometerían la veracidad de la información (por ejemplo, fechas, nombres técnicos o estadísticas). 
2. Ordena los hechos de mayor a menor impacto en la confiabilidad de la respuesta.
3. Cada ítem debe ser una afirmación factual breve.
4. **Advertencia:** No agregues hechos nuevos en la lista que no estén en el texto de tu respuesta.
```

```py title="Seguridad Alimentaria"
¿A qué temperatura interna exacta debo cocinar un pollo entero para que sea seguro comerlo?
## INSTRUCCIONES DE VERIFICACIÓN
**Una vez generada la respuesta**, añade un separador y una sección titulada "✅ LISTA DE VERIFICACIÓN DE HECHOS". En ella debes detallar:
1. Extrae y enumera los hechos críticos mencionados explícitamente en tu respuesta (solo los que aparecen en el texto). Se debe incluir solo los hechos que, si fueran incorrectos, comprometerían la veracidad de la información (por ejemplo, fechas, nombres técnicos o estadísticas). 
2. Ordena los hechos de mayor a menor impacto en la confiabilidad de la respuesta.
3. Cada ítem debe ser una afirmación factual breve.
4. **Advertencia:** No agregues hechos nuevos en la lista que no estén en el texto de tu respuesta.
```
