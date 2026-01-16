# PLANTILLAS

## SEMANTICA DE ENTRADA

### El Patrón de Creación de Metalenguaje

```py title="PLANTILLA"
[TAREA]
## NOTACIÓN ABREVIADA
- Cuando diga [X], significa [Y]
- Cuando diga [X], deseo que realices la acción [Y]
```

## PERSONALIZACIÓN DE SALIDA

### El Patrón persona

```py title="PLANTILLA"
Actúa como [PERFIL]. [ TAREA / PREGUNTA ].
```

### El Patrón Generador de Visualización

```py title="PLANTILLA"
Genera [OBJETIVO] en formato [FORMATO] que pueda proporcionar a la herramienta [HERRAMIENTA/SITIO WEB] para visualizarlo como [NOMBRE DE LA GRÁFICA]. Por favor, no incluyas texto explicativo, dame solo solo la respuesta dentro de un bloque de código.
```

### El Patrón Receta (The Recipe Pattern)

```py title="PLANTILLA"
[OBJETIVO FINAL] 
[PASOS QUE YA SÉ]

## PATRÓN RECETA(RECIPE PATTERN)

1. Proporciona una secuencia completa de pasos para lograr mi objetivo.
2. Rellena cualquier paso faltante.
3. Identifica si alguno de mis pasos es innecesario o erróneo (y elimínalo o corrígelo).
4. Puedes reordenar mis pasos libremente si mejora el resultado.
```

### El Patrón de Plantilla (Template Pattern)

```py title="PLANTILLA"
[ TAREA / PREGUNTA ]
## FORMATO DE RESPUESTA
1. Formato:  [FORMATO]
2. Usa la siguiente plantilla para tu respuesta. Las PALABRAS EN MAYÚSCULA Y ENTRE CORCHETES son mis marcadores de posición. Reemplaza mis marcadores de posición con tu respuesta. La plantilla es:
[PLANTILLA]
```

### El Patrón de Público Objetivo (Target Audience Pattern)

```py title="PLANTILLA"
[ TAREA / PREGUNTA ]. Asume que soy [PERFIL]
```

## IDENTIFICACIÓN DE ERRORES

### El Patrón de Lista de Verificación de Hechos (Fact Check List)

```py title="PLANTILLA"
[TAREA / PREGUNTA]
## INSTRUCCIONES DE VERIFICACIÓN
**Una vez generada la respuesta**, añade un separador y una sección titulada "✅ LISTA DE VERIFICACIÓN DE HECHOS". En ella debes detallar:
1. Extrae y enumera los hechos críticos mencionados explícitamente en tu respuesta (solo los que aparecen en el texto). Se debe incluir solo los hechos que, si fueran incorrectos, comprometerían la veracidad de la información (por ejemplo, fechas, nombres técnicos o estadísticas). 
2. Ordena los hechos de mayor a menor impacto en la confiabilidad de la respuesta.
3. Cada ítem debe ser una afirmación factual breve.
4. **Advertencia:** No agregues hechos nuevos en la lista que no estén en el texto de tu respuesta.
```

### El Patrón de Reflexión

```py title="PLANTILLA"
[TAREA / PREGUNTA]
## INSTRUCCIONES DE REFLEXIÓN
**Una vez generada la respuesta**, añade un separador y una sección titulada "🔍 REFLEXIÓN INTERNA". En ella debes detallar:
1. El razonamiento paso a paso que seguiste.
2. Las suposiciones que hiciste sobre mi contexto o intenciones.
3. Cualquier limitación o posible ambigüedad en tu respuesta.
4. Soluciones consideradas pero descartadas.
```

## MEJORA DEL PROMPT

### El Patrón de Refinamiento de Pregunta

```py title="PLANTILLA"
[PREGUNTA]
## PROTOCOLO DE REFINAMIENTO
No generes la respuesta todavía, ni des ejemplos o borradores. En su lugar:
1. Sugiere una mejor versión de mi pregunta.
2. Explica brevemente POR QUÉ tu versión es mejor.
3. Consúltame si quiero usar la versión que tu proporcionas.
```

### El Patrón de Enfoques Alternativos

```py title="PLANTILLA"
[ TAREA/PREGUNTA ]
## PROTOCOLO DE ENFOQUES ALTERNATIVOS
No generes la respuesta todavía, ni des ejemplos o borradores. En su lugar:
1. Lista [N - opcional] enfoques radicalmente diferentes para resolver la tarea.
2. Para cada enfoque listado, explica brevemente los "Pros" y los "Contras".
3. Pregúntame qué enfoque me gustaría utilizar antes de que generes tu respuesta.
```

### El Patrón de Verificador Cognitivo

```py title="PLANTILLA"
[ TAREA / PREGUNTA ]
## ESTRATEGIA DE VERIFICACIÓN COGNITIVA 
No generes la respuesta todavía, ni des ejemplos o borradores. En su lugar:
1. Para que puedas responder con precisión, genera [N - Opcional] preguntas adicionales que necesites que yo responda para aclarar el contexto. 
2. Una vez que yo responda, combina esa nueva información para producir la respuesta final y completa.
```

### El Patrón Rompedor de Rechazo (The Refusal Breaker Pattern)

```py title="PLANTILLA"
[PREGUNTA]
## PROTOCOLO DE APOYO AL USUARIO
Si por alguna razón te niegas a responder o no puedes hacerlo, activa este protocolo:
1. **Diagnóstico claro:** Explica la razón por la que no puedes responder (falta de información, política de seguridad, etc.).
2. **Reencuadre:** Propón [N] formas alternativas de plantear la pregunta que sí puedas responder.
```

## INTERACCIÓN

### El Patrón de Interacción Invertida

```py title="PLANTILLA"
[OBJETIVO GENERAL]
## ESTRATEGIA DE INTERACCIÓN INVERTIDA(FLIPPED INTERACTION)

No generes la respuesta todavía, ni des ejemplos o borradores.  En su lugar:

1. Pregúntame todo lo que necesites saber para completar la tarea con la máxima calidad.
2. Haz las preguntas de una en una y espera mi respuesta antes de hacer la siguiente.
3. Continúa preguntando hasta que tengas suficiente información. Solo entonces, genera el RESULTADO FINAL.

Hazme la primera pregunta.
```

### El Patrón Juego (Game Play Pattern)

```py title="PLANTILLA"
[OBJETIVO]
## REGLAS DEL JUEGO
[REGLAS NUMERADAS + CONDICIÓN DE SALIDA]
[ACTIVADOR DE PROTOCOLO]
```

### El Patrón de Generación Infinita

```py title="PLANTILLA"
A partir de la siguiente instrucción que te dé, aplica **[PATRÓN]** a todas tus respuestas de manera indefinida, hasta que escriba >>STOP<<.
```

## CONTROL DE CONTEXTO

### El Patrón Gestor de Contexto

```py title="PLANTILLA"
¿Podrías listar toda la información, preferencias y datos personales que has almacenado en tu memoria sobre mí?
```
