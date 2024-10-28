El archivo index almacena archivos en una carpeta local y los indexa para su recuperación. Este archivo de índice proporciona la siguiente infraestructura para respaldar la indexación:

- **Tabla SQL Source**: almacena la lista de archivos que son indexados por el sistema.
- **Almacenamiento vectorial**: contiene las representaciones en vectores de segmentos de los archivos.
- **Almacenamiento de documentos**: contiene el texto de segmentos de los archivos. Cada texto almacenado en este almacenamiento de documentos está asociado con un vector en el almacenamiento vectorial.
- **Tabla SQL Index**: almacena la relación entre (1) el source y el docstore, y (2) el source y el vector store.

Se recomienda que los pipelines de indexación y recuperación utilicen la infraestructura de software mencionada.

## Pipeline de indexación

DocProcessing tiene un pipeline de indexación por defecto: `DocProcessing.index.file.pipelines.IndexDocumentPipeline`.

Este pipeline funciona de la siguiente manera:

- **Entrada**: lista de rutas de archivos.
- **Salida**: lista de nodos que son indexados en la base de datos.
- **Proceso**:
  - Leer archivos y convertirlos en textos. Diferentes tipos de archivos tienen diferentes formas de leer textos.
  - Dividir archivos de texto en segmentos más pequeños.
  - Ejecutar cada segmento para obtener sus embeddings.
  - Almacenar los embeddings en el vector store. Almacenar los textos de cada segmento en el docstore. Almacenar la lista de archivos en Source. Almacenar el vínculo entre Sources y el docstore + vectorstore en la tabla Index.

Puedes personalizar este pipeline por defecto si tu proceso de indexación es similar al pipeline predeterminado. Si hay demasiada lógica diferente, puedes crear tu propio pipeline de indexación.

### Personaliza el pipeline por defecto

El pipeline por defecto proporciona los puntos de contacto en `flowsettings.py`.

1. `FILE_INDEX_PIPELINE_FILE_EXTRACTORS`: Proporciona extractores de archivo que sobrescriben, basados en la extensión del archivo. Ejemplo: `{".pdf": "ruta.a.PDFReader", ".xlsx": "ruta.a.ExcelReader"}`
2. `FILE_INDEX_PIPELINE_SPLITTER_CHUNK_SIZE`: Número esperado de caracteres de cada segmento de texto. Ejemplo: 1024.
3. `FILE_INDEX_PIPELINE_SPLITTER_CHUNK_OVERLAP`: Número esperado de caracteres que los segmentos de texto consecutivos deben superponerse entre sí. Ejemplo: 256.

### Crea tu propio pipeline de indexación

Tu pipeline de indexación debe heredar de `BaseFileIndexIndexing`.

Deberías definir los siguientes métodos:

- `run(self, file_paths)`: ejecuta la indexación dado el pipeline.
- `get_pipeline(cls, user_settings, index_settings)`: devuelve el pipeline completamente inicializado, listo para ser utilizado por DocProcessing.
  - `user_settings`: es un diccionario que contiene configuraciones del usuario (por ejemplo, `{"pdf_mode": True, "num_retrieval": 5}`). Puedes declarar estas configuraciones en el método de clase `get_user_settings`. DocProcessing recolectará estas configuraciones en la página de Configuración de la aplicación y proporcionará estas configuraciones de usuario a tu método `get_pipeline`.
  - `index_settings`: es un diccionario. Actualmente está vacío para el índice de archivos.
- `get_user_settings`: para declarar configuraciones de usuario, devuelve un diccionario.

Al heredar de `BaseFileIndexIndexing`, tendrás acceso a los siguientes recursos:

- `self._Source`: la tabla de fuentes.
- `self._Index`: la tabla de índices.
- `self._VS`: el almacenamiento vectorial.
- `self._DS`: el almacenamiento de documentos.

Una vez que hayas preparado tu pipeline, regístralo en `flowsettings.py`: `FILE_INDEX_PIPELINE = "<ruta.python.a.tu.pipeline>"`.

## Pipeline de recuperación

DocProcessing tiene un pipeline de recuperación por defecto: `DocProcessing.index.file.pipelines.DocumentRetrievalPipeline`. Este pipeline funciona de la siguiente manera:

- **Entrada**: consulta de texto del usuario y opcionalmente una lista de identificaciones de archivos fuente.
- **Salida**: segmentos de salida que coinciden con la consulta de texto del usuario.
- **Proceso**:
  - Si se proporciona una lista de identificaciones de archivos fuente, obtiene la lista de identificaciones de vectores asociadas a esos archivos.
  - Embebe la consulta de texto del usuario.
  - Consulta el almacenamiento vectorial. Proporciona una lista de identificaciones de vectores para limitar el alcance de la consulta si el usuario restringe.
  - Devuelve los segmentos de texto coincidentes.

### Crea tu propio pipeline de recuperación

Tu pipeline de recuperación debe heredar de `BaseFileIndexRetriever`. El recuperador tiene el mismo acceso a la base de datos, al almacenamiento vectorial y al almacenamiento de documentos que el pipeline de indexación.

Deberías definir los siguientes métodos:

- `run(self, query, file_ids)`: recupera documentos relevantes relacionados con la consulta. Si se proporcionan `file_ids`, deberías restringir tu búsqueda dentro de esos `file_ids`.
- `get_pipeline(cls, user_settings, index_settings, selected)`: devuelve el pipeline completamente inicializado, listo para ser utilizado por DocProcessing.
  - `user_settings`: es un diccionario que contiene configuraciones del usuario (por ejemplo, `{"pdf_mode": True, "num_retrieval": 5}`). Puedes declarar estas configuraciones en el método de clase `get_user_settings`. DocProcessing recolectará estas configuraciones en la página de Configuración de la aplicación y proporcionará estas configuraciones de usuario a tu método `get_pipeline`.
  - `index_settings`: es un diccionario. Actualmente está vacío para el índice de archivos.
  - `selected`: una lista de identificaciones de archivos seleccionadas por el usuario. Si el usuario no selecciona nada, esta variable será None.
- `get_user_settings`: para declarar configuraciones de usuario, devuelve un diccionario.

Una vez que hayas construido la clase del pipeline de recuperación, puedes registrarla en `flowsettings.py`: `FILE_INDEXING_RETRIEVER_PIPELIENS = ["ruta.a.recuperacion.pipeline"]`. Dado que puede haber múltiples pipelines paralelos dentro de un índice, esta variable toma una lista de cadenas en lugar de una sola cadena.

## Infraestructura de software

| Infra             | Acceso        | Esquema                                                                                                                                                                                                                                                                                      | Referencia                                                    |
| ----------------- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| Tabla SQL Source  | self.\_Source | - id (int): id de la fuente (auto)<br>- nombre (str): el nombre del archivo<br>- ruta (str): la ruta del archivo<br>- tamaño (int): el tamaño del archivo en bytes<br>- nota (dict): permite información adicional opcional sobre el archivo<br>- fecha_creacion (datetime): la fecha en que se creó el archivo (auto) | Esta es una clase ORM de SQLAlchemy. Se puede consultar      |
| Tabla SQL Index   | self.\_Index  | - id (int): id de la entrada del índice (auto)<br>- source_id (int): el id de un archivo en la tabla Source<br>- target_id: el id del segmento en el docstore o el vector store<br>- relation_type (str): si el vínculo es "documento" o "vector"                                        | Esta es una clase ORM de SQLAlchemy                          |
| Almacenamiento vectorial | self.\_VS     | - self.\_VS.add: agregar la lista de embeddings al vector store (opcionalmente asociar metadatos e ids)<br>- self.\_VS.delete: eliminar entradas de vectores basadas en ids<br>- self.\_VS.query: obtener embeddings basados en embeddings.                                                                | DocChatUI > storages > vectorstores > BaseVectorStore      |
| Almacenamiento de documentos | self.\_DS     | - self.\_DS.add: agregar los segmentos a los almacenes de documentos<br>- self.\_DS.get: obtener los segmentos basados en id<br>- self.\_DS.get_all: obtener todos los segmentos<br>- self.\_DS.delete: eliminar segmentos basados en id                                                             | DocChatUI > storages > docstores > base > BaseDocumentStore |