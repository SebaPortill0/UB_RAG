<div align="center">

# RAG Project

Una interfaz de usuario de RAG (Recuperación Aumentada por Generación) de código abierto, limpia y personalizable para conversar con tus documentos. Diseñada pensando tanto en usuarios finales como en desarrolladores.

</div>

## Introduction

Este proyecto funciona como una interfaz RAG para usuarios finales que desean realizar preguntas y respuestas sobre sus documentos, así como para desarrolladores que buscan construir su propio pipeline de RAG.

<br>

### Para Usuarios Finales

- **Interfaz Limpia y Minimalista**: Una interfaz fácil de usar para preguntas y respuestas (QA) basadas en RAG.
- **Soporte para diferentes LLMs**: Compatible con proveedores de API de LLM (OpenAI, AzureOpenAI, Cohere, etc.) y con LLMs locales (via `ollama` y `llama-cpp-python`).
- **Fácil Instalación**: Conlleva una instalación simple e intuitiva.

### PAra Desarrolladores

- **Framework para RAG Pipelines**: Herramientas para construir tu propio pipeline de preguntas y respuestas (QA) basado en RAG para documentos.
- **UI Personalizable**: Observa tu pipeline de RAG en acción con la interfaz de usuario proporcionada, construida con <a href='https://github.com/gradio-app/gradio'>Gradio <img src='https://img.shields.io/github/stars/gradio-app/gradio'></a>.

## Características Principales

- **Aloja tu propia interfaz web de preguntas y respuestas de documentos (RAG)**: Admite inicio de sesión para múltiples usuarios, organiza tus archivos en colecciones privadas/públicas, colabora y comparte tus conversaciones favoritas con otros.

- **Organiza tus modelos LLM y de Embedding**: Compatible tanto con LLMs locales como con los principales proveedores de API (OpenAI, Azure, Ollama, Groq).

- **Pipeline RAG híbrido**: Pipeline RAG con valores predeterminados sensatos, utilizando un recuperador híbrido (texto completo y vectorial) y reordenamiento para asegurar la mejor calidad en la recuperación.

- **Soporte de QA multimodal**: Realiza preguntas y respuestas en múltiples documentos que incluyan figuras y tablas, con opciones de análisis de documentos multimodales seleccionables en la interfaz.

- **Citas avanzadas con vista previa de documentos**: Por defecto, el sistema proporciona citas detalladas para asegurar la precisión de las respuestas de los LLM. Visualiza tus citas (incluyendo el puntaje de relevancia) directamente en el visor de PDF en el navegador, con resaltados. Advertencia cuando la recuperación devuelve artículos de baja relevancia.

- **Compatibilidad con métodos de razonamiento complejos**: Usa la descomposición de preguntas para responder preguntas complejas o de múltiples pasos. Compatible con razonamiento basado en agentes, como `ReAct`, `ReWOO` y otros agentes.

- **Interfaz de configuración ajustable**: Puedes modificar los aspectos más importantes del proceso de recuperación y generación en la interfaz (incluyendo prompts).

- **Extensible**: Al estar construido en Gradio, puedes personalizar o añadir elementos de la interfaz como desees. Además, buscamos soportar múltiples estrategias para la indexación y recuperación de documentos. El pipeline de indexación `GraphRAG` se proporciona como ejemplo.


## Instalación

### Requerimientos del Sistema

1. [Python](https://www.python.org/downloads/) >= 3.10

### Sin Docker

1. Clona e instala los paquetes necesarios en un nuevo entorno de Python.

   ```shell
   # optional (setup env)
   conda create -n DocChatUI python=3.10
   conda activate DocChatUI

   # clone this repo
   git clone https://github.com/this_repo/DocChatUI
   cd DocChatUI

   pip install -e "libs/DocChatUI[all]"
   pip install -e "libs/DocProcessing"
   ```

2. Crea un archivo `.env` en la raíz de este proyecto. Usa `.env.example` como plantilla.

   El archivo `.env` está diseñado para casos en los que los usuarios desean preconfigurar los modelos antes de iniciar la aplicación (por ejemplo, desplegar la aplicación en el hub de Hugging Face). Este archivo solo se utilizará para poblar la base de datos una vez durante la primera ejecución y no se utilizará en ejecuciones subsiguientes.


3. Inicia el servidor web:

   ```shell
   python app.py
   ```

   - La aplicación se lanzará automáticamente en tu navegador.
   - El nombre de usuario y la contraseña predeterminados son ambos `admin`. Puedes configurar usuarios adicionales directamente a través de la interfaz de usuario.


4. Verifica la pestaña `Recursos` y `LLMs y Embeddings` y asegúrate de que el valor de tu `api_key` esté configurado correctamente en tu archivo `.env`. Si no está configurado, puedes establecerlo allí.

### Setup GraphRAG

> [!NOTE]
> Actualmente la función de GraphRAG no se encuentra implementada.

  ```shell
  pip install graphrag future
  ```

- **Configuración de la CLAVE API**: Para utilizar la función de recuperación de GraphRAG, asegúrese de configurar la variable de entorno `GRAPHRAG_API_KEY`. Puede hacerlo directamente en su entorno o agregándola a un archivo `.env`.
- **Uso de modelos locales y configuraciones personalizadas**: Si desea utilizar GraphRAG con modelos locales (como `Ollama`) o personalizar el LLM predeterminado y otras configuraciones, configure la variable de entorno `USE_CUSTOMIZED_GRAPHRAG_SETTING` en verdadero. Luego, ajuste su configuración en el archivo `settings.yaml.example`.