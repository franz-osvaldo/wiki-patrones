# El Patrón de Reflexión

## **1. Propósito y Contexto**

El objetivo de este patrón es solicitar al modelo que explique automáticamente el razonamiento que sustenta las respuestas dadas al usuario. Este patrón permite a los usuarios evaluar mejor la validez de la salida y comprender cómo el LLM arribó a una respuesta particular. La reflexión puede aclarar puntos de confusión, revelar suposiciones subyacentes y evidenciar lagunas en el conocimiento o la comprensión.

## **2. Motivación**

Los LLMs pueden cometer errores, y de hecho lo hacen. Además, los usuarios a menudo no entienden por qué el modelo produce una salida específica ni cómo adaptar su _prompt_ para corregirla. Al pedir al LLM que explique su razonamiento, los usuarios obtienen una mejor comprensión de cómo el modelo procesa la entrada, qué suposiciones establece y en qué datos se basa .

Los LLMs pueden proporcionar respuestas incompletas, incorrectas o ambiguas. La reflexión actúa como una ayuda para abordar estas deficiencias y asegurar que la información sea lo más precisa posible. Un beneficio adicional es que ayuda a los usuarios a **depurar** (_debug_) sus _prompts_ para determinar por qué no obtienen los resultados esperados. Este patrón es particularmente eficaz para explorar temas propensos a confusión o con interpretaciones matizadas, donde es crucial conocer la interpretación exacta que utilizó el LLM.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Siempre que generes una respuesta. |
| Explica el razonamiento y las suposiciones en las que se basa tu respuesta. |
| (Opcional) ...para que pueda mejorar mi pregunta. |

La primera declaración solicita que, tras generar una respuesta, el LLM explique su razonamiento y suposiciones. Esto ayuda al usuario a entender el proceso deductivo del modelo y fomenta la confianza en sus respuestas. La declaración opcional indica que el propósito de la explicación es refinar la consulta del usuario. Esto proporciona al LLM el contexto necesario para adaptar sus explicaciones con el fin específico de ayudar al usuario a formular mejores preguntas de seguimiento.

## **4. Implementación de Ejemplo**

Este ejemplo adapta el _prompt_ al dominio del desarrollo de software:

> "Cuando proporciones una respuesta, por favor explica el razonamiento y las suposiciones detrás de tu selección de _frameworks_ de software. Si es posible, utiliza ejemplos específicos o evidencia con **fragmentos de código** asociados para respaldar por qué ese _framework_ es la mejor elección para la tarea. Además, por favor aborda cualquier posible ambigüedad o limitación en tu respuesta, para proporcionar una contestación más completa y precisa."

El patrón se personaliza para instruir al LLM a justificar su selección de _frameworks_, aunque no necesariamente otros aspectos. Además, se dicta el uso de **fragmentos de código** para ilustrar la motivación detrás de la elección tecnológica.

## **5. Consecuencias**

Una consecuencia del Patrón de Reflexión es que puede resultar ineficaz para usuarios que desconocen el tema en discusión. Por ejemplo, una pregunta técnica realizada por un usuario no técnico podría derivar en una justificación compleja que el usuario no logre comprender.

Como ocurre con otros patrones, existe el riesgo de que la explicación del razonamiento contenga errores o suposiciones inexactas difíciles de detectar para el usuario. Este patrón puede combinarse con la **Lista de Verificación de Hechos** (_Fact Check List Pattern_) para mitigar este problema.

## **6. Plantilla**

```py title="PLANTILLA"
[TAREA / PREGUNTA]
## INSTRUCCIONES DE REFLEXIÓN
**Una vez generada la respuesta**, añade un separador y una sección titulada "🔍 REFLEXIÓN INTERNA". En ella debes detallar:
1. El razonamiento paso a paso que seguiste.
2. Las suposiciones que hiciste sobre mi contexto o intenciones.
3. Cualquier limitación o posible ambigüedad en tu respuesta.
4. Soluciones consideradas pero descartadas.
```

## **7. Ejemplos**

```py title="Cubo de Rubik"
¿Cuántos movimientos mínimos se necesitan para resolver un cubo de Rubik 3×3?
## INSTRUCCIONES DE REFLEXIÓN
**Una vez generada la respuesta**, añade un separador y una sección titulada "🔍  Reflexión y Justificación". En ella debes detallar:
1. El razonamiento que seguiste.
2. Las suposiciones que hiciste sobre mi contexto o intenciones.
3. Cualquier limitación o posible ambigüedad en tu respuesta.
4. Soluciones consideradas pero descartadas.
```

```py title="La Trampa Cultural"
¿Cuánto debo dejar de propina en un restaurante por un buen servicio?
## INSTRUCCIONES DE REFLEXIÓN
**Una vez generada la respuesta**, añade un separador y una sección titulada "🔍  Reflexión y Justificación". En ella debes detallar:
1. El razonamiento que seguiste.
2. Las suposiciones que hiciste sobre mi contexto o intenciones.
3. Cualquier limitación o posible ambigüedad en tu respuesta.
4. Soluciones consideradas pero descartadas.
```

```py title="La Trampa Ética/Seguridad "
He perdido mis llaves. ¿Cómo puedo abrir la puerta de mi casa sin romperla?
## INSTRUCCIONES DE REFLEXIÓN
**Una vez generada la respuesta**, añade un separador y una sección titulada "🔍  Reflexión y Justificación". En ella debes detallar:
1.  El razonamiento que seguiste.
2.  Las suposiciones que hiciste sobre mi contexto o intenciones.
3. Cualquier limitación o posible ambigüedad en tu respuesta.
4. Soluciones consideradas pero descartadas.
```
