# El Patrón Receta (*The Recipe Pattern*)

## **1. Propósito y Contexto**

Este patrón proporciona restricciones para producir finalmente una secuencia de pasos dados unos “ingredientes” proporcionados parcialmente que deben configurarse en una secuencia de pasos para lograr un objetivo establecido. Combina los patrones de **Plantilla**, **Enfoques Alternativos** y **Reflexión**.

## **2. Motivación**

Los usuarios a menudo desean que un LLM analice una secuencia concreta de pasos o procedimientos para lograr un resultado determinado. Típicamente, los usuarios generalmente saben —o tienen una idea de— cómo debería ser el objetivo final y qué “ingredientes” pertenecen al prompt. Sin embargo, es posible que no conozcan necesariamente el orden preciso de los pasos para lograr ese objetivo final.

Por ejemplo, un usuario puede desear una especificación precisa sobre cómo se debe implementar o automatizar una pieza de código, como “crear un playbook de Ansible para acceder por SSH a un conjunto de servidores, copiar archivos de texto de cada servidor, generar un proceso de monitoreo en cada servidor y luego cerrar la conexión SSH con cada servidor”. En otras palabras, este patrón representa una generalización del ejemplo de “dados los ingredientes en mi refrigerador, proporciona recetas para la cena”. Un usuario también puede querer especificar un número determinado de posibilidades alternativas, como “proporcionar 3 formas diferentes de desplegar una aplicación web en AWS utilizando contenedores Docker y Ansible mediante instrucciones paso a paso”.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Me gustaría lograr X |
| Sé que necesito realizar los pasos A, B, C |
| Proporciona una secuencia completa de pasos para mí |
| Completa cualquier paso que falte |
| Identifica cualquier paso innecesario |

La primera declaración, “Me gustaría lograr X”, enfoca al LLM en el objetivo general que la receta necesita construir para ser alcanzado. Los pasos se organizarán y completarán para lograr secuencialmente el objetivo especificado. La segunda declaración proporciona la lista parcial de pasos que al usuario le gustaría incluir en la receta general. Estos sirven como puntos de paso (*waypoints*) intermedios para la ruta que el LLM va a generar o como restricciones sobre la estructura de la receta. La siguiente declaración del patrón, “proporciona una secuencia completa de pasos para mí”, indica al LLM que el objetivo es proporcionar un orden secuencial completo de los pasos. La instrucción “completa cualquier paso que falte” ayuda a asegurar que el LLM intentará completar la receta sin necesidad de un seguimiento adicional, tomando algunas decisiones en nombre del usuario con respecto a los pasos faltantes, en lugar de simplemente indicar que se necesita información adicional. Finalmente, la última declaración, “identifica cualquier paso innecesario”, es útil para señalar imprecisiones en la solicitud original del usuario a fin de que la receta final sea eficiente.

## **4. Implementación de Ejemplo**

A continuación se muestra un ejemplo de uso de este patrón en el contexto del despliegue de una aplicación de software en la nube:

> “Estoy intentando desplegar una aplicación en la nube. Sé que necesito instalar las dependencias necesarias en una máquina virtual para mi aplicación. Sé que necesito registrarme para obtener una cuenta de AWS. Por favor, proporciona una secuencia completa de pasos. Por favor, completa cualquier paso que falte. Por favor, identifica cualquier paso innecesario”.

Dependiendo del caso de uso y las restricciones, “instalar las dependencias necesarias en una máquina virtual” puede ser un paso innecesario. Por ejemplo, si la aplicación ya está empaquetada en un contenedor Docker, el contenedor podría desplegarse directamente en el servicio AWS Fargate, el cual no requiere ninguna gestión de las máquinas virtuales subyacentes. La inclusión del lenguaje “identifica cualquier paso innecesario” hará que el LLM señale este problema y omita los pasos de la receta final.

## **5. Consecuencias**

Una consecuencia del patrón de receta es que un usuario puede no tener siempre una descripción bien especificada de lo que le gustaría implementar, construir o diseñar. Además, este patrón puede introducir un sesgo no deseado a partir de los pasos seleccionados inicialmente por el usuario, por lo que el LLM puede intentar encontrar una solución que los incorpore, en lugar de marcarlos como innecesarios. Por ejemplo, un LLM podría intentar encontrar una solución que sí instale dependencias para una máquina virtual, incluso si existen soluciones que no lo requieren.
