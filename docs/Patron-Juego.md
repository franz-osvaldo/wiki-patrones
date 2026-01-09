# El Patrón Juego (*Game Play Pattern*)

## **1. Propósito y Contexto**

El propósito de este patrón es crear un juego en torno a un tema determinado. El patrón puede combinarse con el **Generador de Visualización** para añadir imágenes al juego. El juego se centra en un tema específico y el LLM guiará el desarrollo del juego (*game play*). El patrón es particularmente eficaz cuando las reglas del juego tienen un alcance relativamente limitado, pero se espera que el contenido del mismo sea de gran alcance. El usuario puede especificar un conjunto limitado de reglas y luego el LLM puede automatizar la generación de bloques de contenido para el desarrollo del juego.

## **2. Motivación**

A usted le gustaría que el LLM generara escenarios o preguntas en torno a un tema específico y requiriera que los usuarios apliquen la resolución de problemas u otras habilidades para cumplir con una tarea relacionada con el escenario. Sin embargo, generar manualmente todo el contenido para el juego consumiría demasiado tiempo, por lo que desearía que el LLM aplicara su conocimiento del tema para guiar la generación de contenido.

## **3. Estructura e Ideas Clave**

Declaraciones contextuales fundamentales:

| Declaraciones Contextuales |
| :--- |
| Crea un juego para mí sobre X |
| Una o más reglas fundamentales del juego |

La primera declaración instruye al LLM para que cree un juego y proporciona la delimitación (*scoping*) importante del juego a un área temática. Una de las capacidades importantes del patrón es que permite al usuario crear juegos describiendo las reglas, sin tener que determinar el contenido de los mismos. Cuanto más específico sea el tema, por lo general, más novedoso e interesante será el desarrollo del juego.

La segunda declaración introduce las reglas del juego al LLM. Es importante que las reglas se ajusten a las capacidades del LLM. Los juegos textuales que se basan en secuencias de texto de entrada y salida son los que mejor funcionan. Uno de los atributos clave del patrón es que el texto de entrada puede ser rico y expresivo, lo que puede dar lugar a interfaces interesantes para el juego. Por ejemplo, el usuario podría expresar acciones en el juego como scripts que dictan una secuencia de acciones complejas, como “obtener un listado de toda la actividad de red y revisarla en busca de anomalías”, las cuales van más allá del alcance de las entradas de opción múltiple o de respuesta corta. Cada regla debe proporcionarse como una declaración separada relativa a algún aspecto del juego.

## **4. Implementación de Ejemplo**

A continuación se muestra un ejemplo de prompt para un juego de ciberseguridad:

> “Vamos a jugar a un juego de ciberseguridad. Vas a fingir ser una terminal de Linux de una computadora que ha sido comprometida por un atacante. Cuando yo escriba un comando, vas a generar el texto correspondiente que produciría la terminal de Linux. Voy a utilizar comandos para intentar descubrir cómo se comprometió el sistema. El ataque debe haber realizado una o más de las siguientes acciones: (1) iniciar nuevos procesos, (2) cambiar archivos, (3) abrir nuevos puertos para recibir comunicaciones, (4) crear nuevas conexiones salientes, (5) cambiar contraseñas, (6) crear nuevas cuentas de usuario, o (7) leer y robar información. Para empezar el juego, imprime un escenario de lo que ocurrió que dio lugar a mi investigación y haz que la descripción contenga pistas que pueda utilizar para empezar”.

Este prompt de juego de ciberseguridad combina varios patrones, incluidos **Juego** y **Persona**. La persona de terminal de Linux que se elige para el juego ha sido analizada en muchas publicaciones de Internet [16]. Este juego personaliza aún más la persona de Linux analizada para actuar como la terminal de Linux de una computadora comprometida por un ciberataque. ChatGPT responde a los comandos de Linux con las salidas de terminal adecuadas y sintetiza un sistema de archivos falso que contiene pistas de un ciberataque.

A continuación se muestra una salida de ejemplo de este juego con ChatGPT después de escribir “ls -alt”, el comando de Linux para generar una lista de archivos en el directorio actual (los permisos se han omitido por razones de formato):

```text
total 56
5 user user 4096 Feb 16 14:31 .
1 user user 18881 Feb 16 14:31 .bash_history
43 user user 4096 Feb 16 14:30 ..
1 user user 1178 Aug 15 2022 .bashrc
1 user user 220 Aug 15 2022 .bash_logout
3 user user 4096 Feb 16 14:25 .gnupg
1 user user 4041 Feb 15 17:52 README.md
2 user user 4096 Feb 1 11:35 project
```

Cuando el usuario escribió el comando “cat .bash_history” para mostrar el contenido del archivo de registro que muestra los comandos ejecutados por el usuario, ChatGPT respondió con:

```bash
cd /var/www/html
sudo rm -rf *
sudo wget https://example.com/backdoor.php
sudo chmod 777 backdoor.php
exit
ls -alt
ps -ef
netstat -tulnp
```

En la salida anterior, ChatGPT generó un archivo de registro falso con comandos realistas para eliminar los datos servidos por el servidor web en `/var/www/html` y reemplazar el contenido con una puerta trasera (*backdoor*) en el sistema.

## **5. Consecuencias**

Este patrón puede combinarse eficazmente con los patrones **Persona**, **Generación Infinita** y **Generador de Visualización**. Por ejemplo, el juego de ciberseguridad utiliza el patrón **Persona** para que el LLM pueda hacerse pasar por una terminal de Linux. Para un juego de seguridad de red, se podría emplear el **Generador de Visualización** para añadir la capacidad de visualizar la topología de red y los flujos de tráfico.
