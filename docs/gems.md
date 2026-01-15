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