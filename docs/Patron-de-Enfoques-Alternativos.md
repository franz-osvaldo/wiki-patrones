# El Patrón de Enfoques Alternativos

## **1. Propósito y Contexto**

El propósito de este patrón es asegurar que un LLM siempre ofrezca formas alternativas de realizar una tarea, de modo que el usuario no se limite a seguir únicamente los enfoques con los que está familiarizado. El LLM puede proporcionar enfoques alternativos que obliguen al usuario a reflexionar sobre lo que está haciendo y a determinar si ese es el mejor camino para alcanzar su objetivo. Además, la resolución de la tarea puede informar al usuario o enseñarle conceptos alternativos para seguimientos posteriores.

## **2. Motivación**

Los seres humanos a menudo sufren de sesgos cognitivos que los llevan a elegir un enfoque particular para resolver un problema, incluso cuando no es el enfoque correcto o el "mejor". Además, es posible que las personas desconozcan enfoques alternativos a los que han recurrido en el pasado. La motivación del patrón de **Enfoques Alternativos** es asegurar que el usuario sea consciente de otras opciones para seleccionar un mejor enfoque mediante la disolución de sus sesgos cognitivos.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Dentro del alcance X, si existen formas alternativas de lograr lo mismo, enumera los mejores enfoques alternativos |
| (Opcional) compara/contrasta los pros y contras de cada enfoque |
| (Opcional) incluye la forma original que pregunté |
| (Opcional) pregúntame qué enfoque me gustaría usar |

La primera instrucción, *dentro del alcance X*, fija el tema o los límites de la interacción. Ese alcance son las restricciones que el usuario establece, por ejemplo ***para decisiones de implementación*** o ***para el despliegue de la aplicación***. Así se asegura que cualquier alternativa propuesta respete esas condiciones.

La segunda instrucción, ***si existen formas alternativas de lograr lo mismo, enumera los mejores enfoques alternativos***,  instruye al LLM para que sugiera alternativas. Estas instrucciones pueden hacerse más específicas o incluir contexto del área en la que se trabaja. Por ejemplo, se puede indicar ***si hay formas alternativas de lograr lo mismo con el framework que uso***, para evitar que el modelo proponga alternativas inviables que requieran demasiados cambios en otras partes de la aplicación.

Dado que es posible que el usuario no conozca los enfoques alternativos, también es posible que no sepa por qué debería elegir uno de ellos. La declaración opcional ***compara/contrasta los pros y contras de cada enfoque*** añade criterios de decisión al análisis. Esta instrucción garantiza que el modelo proporcione al usuario la justificación necesaria para las alternativas. La declaración final, ***pregúntame qué enfoque me gustaría usar***, ayuda a eliminar la necesidad de que el usuario tenga que copiar/pegar o introducir manualmente un enfoque alternativo si se selecciona uno.

## **4. Implementación de Ejemplo**

Implementación de un prompt de ejemplo para generar, comparar y permitir que el usuario seleccione uno o más enfoques alternativos:

> Cada vez que te pida desplegar una aplicación en un servicio específico de la nube, si existen servicios alternativos dentro del mismo proveedor que permitan lograr lo mismo, enumera las mejores opciones y luego compara y contrasta las ventajas y desventajas de cada enfoque en términos de costo, disponibilidad y esfuerzo de mantenimiento, incluyendo también la forma original en que lo pedí. Finalmente, pregúntame con cuál opción quiero continuar.

Esta implementación del patrón de **Enfoques Alternativos** se está adaptando específicamente al contexto de la ingeniería de software y se centra en el despliegue de aplicaciones en servicios en la nube. El prompt está diseñado para interceptar momentos en los que el desarrollador podría haber realizado una selección de servicio en la nube sin tener pleno conocimiento de servicios alternativos que podrían tener un precio más competitivo o ser más fáciles de mantener. El prompt dirige a ChatGPT para que enumere los mejores servicios alternativos que pueden realizar la misma tarea con el mismo proveedor de servicios en la nube (proporcionando restricciones a las alternativas) y para comparar y contrastar los pros y contras de cada enfoque.

## **5. Consecuencias**

Este patrón es efectivo en su forma genérica y puede aplicarse a una amplia gama de tareas de manera eficaz. Los refinamientos podrían incluir tener un catálogo estandarizado de alternativas aceptables en un dominio específico del cual el usuario deba seleccionar. El patrón de **Enfoques Alternativos** también puede utilizarse para incentivar a los usuarios a seleccionar uno de un conjunto aprobado de enfoques mientras se les informa de los pros y contras de las opciones aprobadas.

## **6. Plantilla**

```py title="PLANTILLA"
[ TAREA/PREGUNTA ]
## ENFOQUES ALTERNATIVOS
No generes la respuesta todavía, ni des ejemplos o borradores. En su lugar:
1. Lista [N - opcional] enfoques radicalmente diferentes para resolver la tarea.
2. Para cada enfoque listado, explica brevemente los "Pros" y los "Contras".
3. Pregúntame qué enfoque me gustaría utilizar antes de que generes tu respuesta.
```

## **7. Ejemplos**

```py title="El aprendiz de violín"
Mi vecino de arriba está aprendiendo a tocar el violín a las 11 de la noche. Necesito que pare.
## ENFOQUES ALTERNATIVOS
No generes la respuesta todavía, ni des ejemplos o borradores. En su lugar:
1. Lista enfoques radicalmente diferentes para resolver la tarea.
2. Para cada enfoque listado, explica brevemente los "Pros" y los "Contras".
3. Pregúntame qué enfoque me gustaría utilizar antes de que generes tu respuesta.
```

!!! success "Pros y contras"
    El patrón asegura que el usuario evalúe racionalmente las opciones al contrastar los "pros y contras" de cada enfoque antes de comprometerse con una solución.

---

```py title="Estudiante de primer año de psicología"
Explica el concepto de "Inteligencia Artificial Generativa". Asume que soy estudiante de primer año de psicología.
## ENFOQUES ALTERNATIVOS
No generes la respuesta todavía, ni des ejemplos o borradores. En su lugar:
1. Lista enfoques radicalmente diferentes para resolver la tarea.
2. Para cada enfoque listado, explica brevemente los "Pros" y los "Contras".
3. Pregúntame qué enfoque me gustaría utilizar antes de que generes tu respuesta.
```

!!! success "Definir el alcance"
    El “scope” (estudiante de primer año de psicología) es el marco de restricciones dentro del cual el LLM debe proponer alternativas.

---
