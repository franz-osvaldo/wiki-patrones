# El Patrón de Público Objetivo (*Target Audience Pattern*)

**1. Propósito y Contexto:** El propósito de este patrón es dar instrucciones al LLM para que adapte la complejidad técnica, el tono, el vocabulario y el enfoque de la salida a un grupo específico de receptores. Este patrón permite que el mismo concepto técnico (por ejemplo, una vulnerabilidad de desbordamiento de búfer o una arquitectura de microservicios) sea explicado de manera radicalmente distinta según si el destinatario es un ejecutivo (C-level), un desarrollador senior o un estudiante principiante.

**2. Motivación:** Los LLMs, por defecto, tienden a generar respuestas con un nivel de complejidad "promedio" basado en sus datos de entrenamiento. En contextos de ingeniería de software y ciencia de datos, esto a menudo resulta en salidas que son demasiado superficiales para expertos o demasiado crípticas para las partes interesadas (*stakeholders*) no técnicas. La teoría de la comunicación aplicada al procesamiento de lenguaje natural (NLP) sugiere que la relevancia de la información es proporcional a su adecuación al conocimiento previo del receptor. Al definir el público objetivo, se activan los subconjuntos léxicos y semánticos del modelo que mejor se alinean con las expectativas y capacidades de comprensión de ese grupo específico.

**3. Estructura e Ideas Clave:** Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Explica X a la audiencia Y |
| Asume que la audiencia tiene un nivel de conocimiento Z sobre el tema |
| Ajusta el tono, el vocabulario y la profundidad técnica para que sean adecuados para Y |
| (Opcional) Evita/Utiliza jerga técnica específica de [dominio] |

La primera declaración establece el destinatario principal, lo que permite al LLM realizar una "proyección de perfil" del receptor. La segunda declaración es crucial para evitar el sesgo de asunción; al definir explícitamente el conocimiento previo (por ejemplo, "asume que conocen la sintaxis básica de Python pero no los decoradores"), el usuario previene que el LLM explique conceptos innecesarios o que omita explicaciones críticas. La tercera declaración calibra el registro lingüístico (formal, instructivo, persuasivo, etc.).

**4. Implementación de Ejemplo:** A continuación se muestra un ejemplo aplicado a la comunicación de una decisión de arquitectura de datos:

> “Explica los beneficios de migrar de una base de datos relacional a una arquitectura de malla de datos (*Data Mesh*). La audiencia son los directivos financieros (CFO) de la empresa. Asume que tienen un conocimiento profundo de los costos operativos pero un conocimiento nulo sobre ingeniería de datos. Traduce los beneficios técnicos en métricas de retorno de inversión (ROI) y agilidad de negocio, evitando tecnicismos como 'sharding' o 'puntos de enlace de API'”.

En este ejemplo, el LLM no solo filtrará la jerga técnica, sino que recontextualizará el valor de la tecnología en términos de impacto financiero, que es el "lenguaje" del público objetivo especificado.

**5. Consecuencias:** Una consecuencia positiva del patrón de Público Objetivo es el aumento significativo en la utilidad de la información para la toma de decisiones. Al alinear la salida con el receptor, se reduce la fricción en la transferencia de conocimiento dentro de organizaciones multidisciplinarias.

Sin embargo, un riesgo de este patrón es la simplificación excesiva (*dumbing down*), donde el LLM, en su intento de ser accesible, puede omitir matices técnicos críticos o recurrir a analogías que distorsionen el significado científico original. Además, el modelo puede basarse en estereotipos sobre ciertas profesiones o roles si no se le proporcionan restricciones claras sobre el nivel de conocimiento asumido. Para mitigar esto, es recomendable combinar este patrón con el patrón de **Reflexión** para asegurar que, a pesar de la simplificación, los fundamentos técnicos sigan siendo válidos.

## **6. Plantilla**

```py title="PLANTILLA"
[ TAREA / PREGUNTA ]. Asume que soy [PERFIL]
```

## **7. Ejemplos**

```py title="TikToker"
Tu tarea es comunicarme que mi puesto de trabajo ha sido eliminado por una IA. Asume que soy un Influencer de la Generación Z obsesionado con TikTok
```

```py title="El padrino"
Tu tarea es comunicarme que mi puesto de trabajo ha sido eliminado por una IA. Asume que soy un Capo de la Mafia Siciliana. Me importa el respeto y la familia
```

```py title="Villana de una Telenovela Mexicana"
Tu tarea es comunicarme que mi puesto de trabajo ha sido eliminado por una IA. Asume que soy la Villana de una Telenovela Mexicana. Soy dramática, rica buscona y malvada. Desprecia a todos y es odiada por todos.
```

```py title="Cavernícola"
Tu tarea es comunicarme que mi puesto de trabajo ha sido eliminado por una IA. Asume que soy un Cavernícola de la Edad de Piedra.
```
