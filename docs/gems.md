## **Crear una Gem**
Brinda detalles sobre tus objetivos, comportamientos deseados y formato preferido para ayudar a la Gem a personalizar las respuestas de Gemini.

Las principales áreas a considerar para escribir instrucciones Gem útiles son las mismas que para escribir instrucciones generales. No es necesario que uses las cuatro, pero te servirá implementar algunas:

### Nombre
### Descripción
### Instrucciones

#### Personalidad
Indícale a tu Gem qué posición asumir y cómo responder.

#### Tarea
Dile a la Gem qué quieres que Gemini haga o cree.

#### Contexto
Brinda tanto contexto como puedas.

#### Formato
Especifica de manera clara la estructura deseada.

### Reescritura mágica
Puedes escribir una frase simple y pulsar el icono de "Usar Gemini para reescribir instrucciones" (la varita mágica).
### Herramienta predeterminada
Si empiezas una nueva conversación con el Gem, se seleccionará la herramienta predeterminada. No obstante, puedes quitarla o seleccionar otra.
### Conocimientos

Puedes añadir archivos para darle más contexto a tu Gem o para hacer referencia a documentos específicos en tus conversaciones con él. 

* Para subir un archivo de tu dispositivo: haz clic en Subir archivos
* Para añadir un archivo de tu Google Drive: haz clic en Drive .
  * Para añadir archivos de tu Drive, debes tener activado el ajuste **Actividad en las aplicaciones** de Gemini y conectar **Google Workspace** con las aplicaciones de Gemini. Si no lo has conectado, verás la opción para hacerlo. Consulta información sobre tus datos de las aplicaciones de Gemini y Google Workspace.
  * Si añades un archivo de tu Drive, Gemini utilizará la versión más reciente del archivo. Si modificas el archivo, esos cambios se reflejarán en tu Gem.

Si compartes este Gem, se mostrarán los títulos de los archivos adjuntos. Se te pedirá por separado que compartas el contenido del archivo adjunto.

## **Plantilla**

```py title="PLANTILLA"
#ROL

```

### ⚠️ Limitaciones y Avisos

* **Ventana de Contexto Compartida:** Las instrucciones de la Gema ocupan espacio en la ventana de contexto. Si las instrucciones son excesivamente largas (miles de palabras), te quedará menos espacio para la conversación activa.
* **Alucinaciones Persistentes:** Si instruyes a la Gema con información errónea en su configuración (ej: *"La capital de Francia es Lyon"*), el modelo priorizará esa instrucción sobre su conocimiento general, generando errores sistemáticos.
* **No es RAG Dinámico (por ahora):** En su versión estándar, las Gemas no se conectan automáticamente a una carpeta de Google Drive específica en tiempo real a menos que uses las extensiones o subas los archivos manualmente en cada sesión (dependiendo de la versión actual de la UI).
* **Sin "Memoria" entre sesiones:** Una Gema no recuerda lo que hablaste con ella en un chat anterior; cada vez que abres la Gema, se reinicia al estado original de sus instrucciones base.

### 🔗 Referencias Oficiales (Fuentes)

Para validar esta capacidad de RAG y el uso de Drive, consulta:

* **Google Workspace Updates (Nov 2024):** *Upload Google Docs and other file types to Gem instructions*. Confirma la capacidad de adjuntar archivos de Drive y Docs como referencia.
    * [Link a la nota oficial](https://workspaceupdates.googleblog.com/2024/11/upload-google-docs-and-other-file-types-to-gems.html)
* **Google Workspace Blog:** *New features in Gemini to deepen usage for organizations*. Detalla cómo las Gemas usan la versión más reciente de los archivos de Drive ("Gems use the most recent version of that file").
    * [Link al artículo](https://workspace.google.com/blog/product-announcements/new-gemini-gems-deeper-knowledge-and-business-context)
* **Ayuda de Google Drive:** *Use Gems with Gemini in Google Drive*.
    * [Link a Soporte](https://support.google.com/drive/answer/16684485)
* # Análisis de Archivos y Documentos (File Upload)

> **Resumen TL;DR:** Función que permite "alimentar" a Gemini con documentos externos (PDFs, hojas de cálculo, código) para que los analice, resuma o transforme. Los archivos se convierten en parte de la memoria a corto plazo (contexto) del chat.

### 📘 Explicación Técnica
Cuando subes un archivo a Gemini, no estás "guardándolo" en una nube tradicional. Técnicamente, ocurre un proceso de **Tokenización e Ingesta**:
1.  **Extracción:** Gemini lee el texto crudo (o la estructura de datos en un CSV/Excel) y lo extrae del formato original.
2.  **Inyección en Contexto:** Ese contenido extraído se cuenta como *tokens* y se inyecta directamente en la **Ventana de Contexto** (Context Window) del modelo.
3.  **Razonamiento:** El modelo procesa esa información como si tú la hubieras escrito manualmente en el chat, permitiéndole razonar sobre ella, buscar correlaciones o detectar patrones.

Gracias a la arquitectura multimodal nativa (especialmente en modelos Gemini 1.5 Pro o Flash), el sistema puede entender la estructura visual de un PDF (tablas, gráficos) y la lógica matemática de una hoja de cálculo.

### 📋 Formatos y Límites (Datos Oficiales)
Según la documentación de soporte (`answer/14903178`), estas son las especificaciones exactas:

**Formatos Admitidos:**
* **Documentos de texto:** .txt, .doc, .docx, .pdf, .rtf, .dot, .dotx, .hwp, .hwpx.
* **Datos tabulares:** .csv, .tsv, .xls, .xlsx (Hojas de cálculo).
* **Código de programación:** .js, .py, .c, .cpp, .java, .sql, .html, .css, .json, y muchos más.
* **Libros electrónicos:** .epub.

**Límites de Carga ("Hard Limits"):**
* **Cantidad:** Máximo **10 archivos** simultáneos por prompt (mensaje).
* **Peso:** Máximo **100 MB** por cada archivo.
* **Nota sobre Imágenes:** Si subes imágenes dentro de un documento, estas también consumen tokens y son procesadas por el motor de visión del modelo.

### 🛠️ Cómo usarlo (Paso a Paso)
1.  **Interfaz:** En la barra de entrada de texto, localiza el símbolo **Más (+)**.
2.  **Selección:** Elige "Subir archivo" (desde tu dispositivo) o "Google Drive" (para conectar con tus documentos en la nube).
3.  **Carga:** Espera unos segundos a que el archivo se procese (verás una barra de progreso o un icono de archivo cargado).
4.  **Prompting:** Escribe tu instrucción. *Nunca subas un archivo sin decirle qué hacer con él*.
    * *Incorrecto:* [Subir archivo] -> Enviar.
    * *Correcto:* [Subir archivo] -> "Haz un resumen ejecutivo de este reporte".

### ⚠️ Limitaciones y Avisos
* **Privacidad (Aviso Crítico):** Según la configuración de tu cuenta, los revisores humanos podrían acceder a los archivos subidos para mejorar el modelo (en versiones personales). **NO** subas documentos con información confidencial, médica o financiera (PII) a menos que uses una licencia **Enterprise** con la protección de datos activada.
* **Consumo de Contexto:** Archivos muy grandes pueden llenar la ventana de contexto. Si subes un PDF de 500 páginas, podrías tener menos espacio para que el modelo genere una respuesta larga ("output tokens").
* **Interacción con Gráficos:** Aunque Gemini es multimodal, a veces puede "alucinar" al interpretar gráficos complejos (scatter plots densos) dentro de un PDF. Siempre verifica los datos numéricos extraídos.

### 💡 Ejemplo de Prompt
> **Contexto:** Usuario sube un archivo `.csv` con datos de ventas mensuales.
>
> **Prompt:**
> "Actúa como un analista de datos senior. He adjuntado un archivo CSV con las ventas del último año.
> 1. Identifica cuál fue el mes con mayor caída (churn) de clientes.
> 2. Calcula el promedio de ventas del Q3.
> 3. Genera un gráfico de barras simple (usando código Python) que muestre la tendencia de ingresos."