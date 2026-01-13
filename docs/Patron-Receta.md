# El Patrón Receta (*The Recipe Pattern*)

## **1. Propósito y Contexto**

Este patrón establece restricciones para producir una secuencia de pasos, partiendo de unos "ingredientes" parciales que deben configurarse en un orden específico para lograr un objetivo declarado. Combina los patrones de **Plantilla**, **Enfoques Alternativos** y **Reflexión**.

## **2. Motivación**

Los usuarios suelen querer que un LLM analice una secuencia concreta de pasos o procedimientos para alcanzar un resultado concreto. Normalmente los usuarios saben, o al menos tienen una idea, de cómo debería verse el objetivo final y qué "ingredientes" deberían formar parte del prompt. Sin embargo, a menudo no saben con exactitud el orden de los pasos necesarios para llegar a ese objetivo.

Por ejemplo, un usuario podría querer una especificación precisa sobre cómo implementar o automatizar un fragmento de código, tal como: "crea un playbook de Ansible para conectarse por SSH a un conjunto de servidores, copiar archivos de texto de cada servidor, lanzar un proceso de monitoreo en cada uno y luego cerrar la conexión SSH". En otras palabras, este patrón representa una generalización del ejemplo "dados los ingredientes en mi refrigerador, dame recetas para la cena". Un usuario también podría querer especificar un número determinado de posibilidades, como "proporciona 3 formas diferentes de desplegar una aplicación web en AWS usando contenedores Docker y Ansible con instrucciones paso a paso"

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Deseo lograr X |
| Sé que necesito realizar los pasos A, B, C |
| Proporciona una secuencia completa de pasos |
| Completa los pasos que falten |
| Identifica cualquier paso innecesario |

La primera declaración, "Deseo lograr X", centra al LLM en el objetivo general para el cual se debe construir la receta. Los pasos se organizarán y completarán para lograr secuencialmente el objetivo especificado.

La segunda declaración proporciona la lista parcial de pasos que al usuario le gustaría incluir en la receta global. Estos sirven como puntos de control intermedios para el camino que el LLM va a generar, o como restricciones en la estructura de la receta.

La siguiente declaración, "proporciona una secuencia completa de pasos", indica al LLM que el objetivo es entregar un ordenamiento secuencial exhaustivo. La frase "completa los pasos que falten" ayuda a garantizar que el LLM intente finalizar la receta sin necesidad de seguimiento adicional, tomando decisiones en nombre del usuario respecto a los pasos ausentes, en lugar de limitarse a indicar que se necesita más información.

Finalmente, la última declaración, “identifica cualquier paso innecesario”, es útil para señalar imprecisiones en la solicitud original del usuario a fin de que la receta final sea eficiente.

## **4. Implementación de Ejemplo**

A continuación se muestra un ejemplo de uso de este patrón en el contexto del despliegue de una aplicación de software en la nube:

> “Estoy intentando desplegar una aplicación en la nube. Sé que necesito instalar las dependencias necesarias en una máquina virtual para mi aplicación. Sé que necesito registrarme para obtener una cuenta de AWS. Por favor, proporciona una secuencia completa de pasos. Por favor, completa cualquier paso que falte. Por favor, identifica cualquier paso innecesario”.

Dependiendo del caso de uso y las restricciones, "instalar las dependencias necesarias en una máquina virtual" podría ser un paso superfluo. Por ejemplo, si la aplicación ya está empaquetada en un contenedor Docker, el contenedor podría desplegarse directamente en el servicio AWS Fargate, el cual no requiere ninguna gestión de las máquinas virtuales subyacentes. La inclusión de la instrucción "Identifica cualquier paso innecesario" hará que el LLM señale este problema y omita dichos pasos de la receta final.

## **5. Consecuencias**

Una consecuencia del patrón de Receta es que el usuario puede no tener siempre una descripción bien definida de lo que le gustaría implementar, construir o diseñar. Además, este patrón puede introducir un sesgo no deseado a partir de los pasos seleccionados inicialmente por el usuario, provocando que el LLM intente encontrar una solución que los incorpore a toda costa, en lugar de marcarlos como innecesarios. Por ejemplo, un LLM podría intentar forzar una solución que instale dependencias en una máquina virtual, incluso si existen alternativas que no lo requieren.

## **6. Plantilla**

```py title="PLANTILLA"
[OBJETIVO FINAL] 
[PASOS QUE YA SÉ]

## PATRÓN RECETA(RECIPE PATTERN)

1. Proporciona una secuencia completa de pasos para lograr mi objetivo.
2. Rellena cualquier paso faltante.
3. Identifica si alguno de mis pasos es innecesario o erróneo (y elimínalo o corrígelo).
4. Puedes reordenar mis pasos libremente si mejora el resultado.
```

## **7. Ejemplos**

```py title="Rocky Balboa"
Ayúdame a ponerme en forma y ganar músculo rápido. Se que tengo que ir al gimnasio, beber huevos crudos como Rocky Balboa, comprar la ropa deportiva más cara.

## PATRÓN RECETA(RECIPE PATTERN)

1. Proporciona una secuencia completa de pasos para lograr mi objetivo.
2. Rellena cualquier paso faltante.
3. Identifica si alguno de mis pasos es innecesario o erróneo (y elimínalo o corrígelo).
4. Puedes reordenar mis pasos libremente si mejora el resultado.
```
