En `DocProcessing`, hay tres tipos principales de configuraciones adaptadas para diversos interesados y sus casos de uso específicos:

1. **Configuraciones para Desarrolladores**: Estas son principalmente para la personalización básica de la aplicación, incluyendo URLs de bases de datos, configuraciones en la nube, ajustes de registro y habilitación de características. Los desarrolladores encontrarán estas configuraciones cruciales al desplegar `DocProcessing` para clientes o al crear extensiones para la misma. Estas configuraciones se definen dentro del archivo `flowsettings.py`.

2. **Configuraciones para Administradores**: Estas configuraciones son accesibles a través de la página de administración y están destinadas a usuarios administrativos. Permiten la personalización de características de bajo nivel, como credenciales de conexión a bases de datos y claves API para la integración de modelos de lenguaje (LLM).

3. **Configuraciones para Usuarios**: Estas configuraciones permiten a los usuarios finales ajustar la aplicación según sus preferencias personales. Los usuarios pueden modificar aspectos como los idiomas de salida para el chatbot y el tipo de razonamiento a utilizar. Las configuraciones detalladas para usuarios suelen encontrarse en la sección de configuración dedicada de la aplicación.
