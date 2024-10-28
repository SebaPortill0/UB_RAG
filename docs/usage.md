## 1. Agrega tus modelos de IA

- La herramienta utiliza modelos de lenguaje grandes (LLM) para realizar varias tareas en un proceso de control de calidad.
Por lo tanto, debe proporcionar a la aplicación acceso a los LLM que desea.
Para utilizar.
- Solo es necesario que incluyas al menos uno. Sin embargo, se recomienda que incluyas todos los LLM.
a los que tienes acceso, podrás cambiar entre ellos mientras usas el solicitud.

Para agregar un modelo:

1. Vaya a la pestaña "Recursos".
2. Seleccione la subpestaña “LLMs”.
3. Seleccione la subpestaña "Agregar".
4. Configure el modelo para agregar:
-Dale un nombre.
- Elija un proveedor (por ejemplo, « ChatOpenAI «).
- Proporcionar las especificaciones.
- (Opcional) Establecer el modelo como predeterminado.
5. Haga clic en "Agregar" para agregar el modelo.
6. Seleccione la subpestaña «Modelos de incorporación» y repita los pasos 3 a 5 para agregar un modelo de incorporación.

<detalles rebajados>

<summary>(Opcional) Configurar el modelo a través del archivo .env</summary>

Alternativamente, puede configurar los modelos a través del archivo `.env` con la información necesaria para conectarse a los LLM. Este archivo se encuentra en
La carpeta de la aplicación. Si no la ves, puedes crear una.

Actualmente, se admiten los siguientes proveedores:

### IA abierta

En el archivo `.env`, configure la variable `OPENAI_API_KEY` con su clave API de OpenAI para
para permitir el acceso a los modelos de OpenAI. Hay otras variables que se pueden modificar,
No dude en editarlos para que se ajusten a su caso. De lo contrario, el parámetro predeterminado debería
Funciona para la mayoría de la gente.

``concha
OPENAI_API_BASE=https://api.openai.com/v1
OPENAI_API_KEY=<su clave API de OpenAI aquí>
OPENAI_CHAT_MODEL=gpt-3.5-turbo
OPENAI_EMBEDDINGS_MODEL=incrustación-de-texto-ada-002
```

###Azure OpenAI

Para los modelos OpenAI a través de la plataforma Azure, debe proporcionar su punto de conexión y API de Azure
clave. Es posible que también deba proporcionar el nombre de sus desarrollos para el modelo de chat y el
modelo de incrustación dependiendo de cómo configure el desarrollo de Azure.

``concha
PUNTO FINAL DE AZURE_OPENAI=
CLAVE DE API DE AZURE OPENAI=
OPENAI_API_VERSION=2024-02-15-preview # podría ser diferente para usted
AZURE_OPENAI_CHAT_DEPLOYMENT=gpt-35-turbo # cambia el nombre de tu implementación
AZURE_OPENAI_EMBEDDINGS_DEPLOYMENT=text-embedding-ada-002 # cambie el nombre de su implementación
```

### Modelos locales

Ventajas:

- Privacidad. Sus documentos se almacenarán y procesarán localmente.
- Opciones. Existe una amplia gama de LLM en términos de tamaño, dominio e idioma para elegir.
de.
- Costo. Es gratis.

Contras:

- Calidad. Los modelos locales son mucho más pequeños y, por lo tanto, tienen una calidad generativa menor que
API pagadas.
- Velocidad. Los modelos locales se implementan utilizando su máquina, por lo que la velocidad de procesamiento es
limitado por su hardware.

#### Busque y descargue un LLM

Puede buscar y descargar un LLM para ejecutarlo localmente desde [Hugging Face
Hub](https://huggingface.co/models). Actualmente, se admiten los siguientes formatos de modelos:

- UGGF

Debes elegir un modelo cuyo tamaño sea menor que la memoria de tu dispositivo y dejarlo
Aproximadamente 2 GB. Por ejemplo, si tienes 16 GB de RAM en total, de los cuales 12 GB están disponibles,
Entonces deberías elegir un modelo que ocupe como máximo 10 GB de RAM. Los modelos más grandes tienden a ocupar
Proporciona una mejor generación pero también requiere más tiempo de procesamiento.

A continuación se muestran algunas recomendaciones y su tamaño en memoria:

- [Qwen1.5-1.8B-Chat-GGUF]( https://huggingface.co/Qwen/Qwen1.5-1.8B-Chat-GGUF/resolve/main/qwen1_5-1_8b-chat-q8_0.gguf?download=true ):
alrededor de 2 GB

#### Habilitar modelos locales (PENDIENTE)

Para agregar un modelo local al grupo de modelos, configure la variable `LOCAL_MODEL` en `.env`
archivo a la ruta del archivo del modelo.

``concha
LOCAL_MODEL=<ruta completa a su archivo de modelo>
```

Aquí se explica cómo obtener la ruta completa del archivo de su modelo:

- En Windows 11: haga clic derecho en el archivo y seleccione "Copiar como ruta".
</detalles>

## 2. Sube tus documentos

Para poder realizar el control de calidad de sus documentos, primero debe cargarlos en la aplicación.
Vaya a la pestaña «Índice de archivos» y verá 2 secciones:

1. Subida de archivos:
- Arrastre y suelte su archivo en la interfaz de usuario o selecciónelo desde su sistema de archivos.
Luego haga clic en "Cargar e indexar".
- La aplicación tardará un tiempo en procesar el archivo y mostrará un mensaje una vez que haya terminado.
2. Lista de archivos:
- Esta sección muestra la lista de archivos que se han cargado a la aplicación y permite a los usuarios eliminarlos.

## 3. Chatea con tus documentos

Ahora, vuelva a la pestaña "Chat". La pestaña de chat se divide en tres partes:

1. Panel de configuración de conversaciones
- Aquí puedes seleccionar, crear, renombrar y eliminar conversaciones.
- De forma predeterminada, se crea automáticamente una nueva conversación si no se selecciona ninguna conversación.
- Debajo tienes el índice de archivos, donde puedes elegir si deseas deshabilitar, seleccionar todos los archivos o seleccionar de qué archivos recuperar referencias.
- Si elige "Deshabilitado", ningún archivo se considerará como contexto durante el chat.
- Si elige "Buscar todo", se considerarán todos los archivos durante el chat.
- Si eliges "Seleccionar", aparecerá un menú desplegable para que selecciones la
archivos a tener en cuenta durante el chat. Si no se selecciona ningún archivo, no se mostrarán los archivos.
Los archivos se considerarán durante el chat.
2. Panel de chat
- Aquí es donde puedes chatear con el chatbot.
3. Panel informativo

- Se proporcionará información de apoyo, como la evidencia recuperada y la referencia.
se muestra aquí.
- Se resalta la cita directa de la respuesta producida por el LLM.
- Se muestran el puntaje de confianza de la respuesta y los puntajes relevantes de las evidencias para evaluar rápidamente la calidad de la respuesta y el contenido recuperado.

- Significado de la puntuación mostrada:
- **Confianza en la respuesta** : nivel de confianza en la respuesta del modelo LLM.
- **Puntuación de relevancia** : puntuación de relevancia general entre la evidencia y la pregunta del usuario.
- ** Puntuación de Vectorstore ** : puntuación relevante del cálculo de similitud de incrustación de vectores (muestra `búsqueda de texto completo` si se recupera de la base de datos de búsqueda de texto completo).
- **Puntaje relevante de LLM** : puntaje relevante del modelo LLM (que juzga la relevancia entre la pregunta y la evidencia utilizando una indicación específica).
- **Puntuación de reranking** : puntuación relevante de Cohere [modelo de reranking]( https://cohere.com/rerank ).

Generalmente, la calidad de la puntuación es “Puntuación relevante de LLM” > “Puntuación de reranking” > “ Vectorscore ”.
De manera predeterminada, la puntuación de relevancia general se toma directamente de la puntuación de relevancia de LLM. Las evidencias se ordenan en función de su puntuación de relevancia general y de si tienen citas o no.
