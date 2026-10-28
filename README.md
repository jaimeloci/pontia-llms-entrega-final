# Configuración del entorno

Este directorio contiene la configuración mínima para ejecutar la entrega final de la asignatura Large Language Models.

El notebook principal se encuentra en:

```text
.\notebooks\finales\notebook-llms-entrega-final.ipynb
```

## API Key

El notebook usa la API de OpenAI.

Antes de ejecutarlo en local, crea un archivo `.env` a partir de `.env.template`:

En macOS/Linux:

```bash
cp .env.template .env
```

En Windows PowerShell:

```powershell
Copy-Item .env.template .env
```

Rellena:

```text
OPENAI_API_KEY="..."
```

------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------

## Requisitos previos

Es necesario tener ``Python 3.11.x`` instalado y actualizado. También será necesario tener la librería ``pip`` y ``uv``.

## Crear y activar entorno virtual

Ejecutar en un terminal:

```bash
# Mac/Linux
uv venv --python 3.11
source .venv/bin/activate

# Windows
uv venv --python 3.11
.\.venv\Scripts\activate
```

## Instalar dependencias

Ejecutar en un terminal:

```bash
uv sync
```

## Crear kernell

Ejecutar en un terminal situado en la raíz del proyecto:

```bash
# Mac/Linux/Windows
python -m ipykernel install --user --name pontia-llms-entrega-final --display-name "Python 3.11 (pontia-llms-entrega-final)"
```


## Cargar notebook en Jupyter

Ejecutar en un terminal situado en la raíz del proyecto:

```bash
# Mac/Linux
jupyter lab ./notebooks/finales/notebook-llms-entrega-final.ipynb

# Windows
jupyter lab .\notebooks\finales\notebook-llms-entrega-final.ipynb
```

## Desactivar entorno virtual

Ejecutar en un terminal situado en la raíz del proyecto o en alguno de sus subdirectorios:

```bash
deactivate
```




## Sobre `pyproject.toml`, `uv.lock` y `requirements.txt`

`python -m venv .venv` solo crea un entorno virtual vacío. No instala dependencias automáticamente ni lee `pyproject.toml` por sí mismo.

El archivo `pyproject.toml` declara el proyecto, la versión de Python requerida y las dependencias directas. Herramientas como `uv` o `pip` pueden usarlo, pero hay que invocarlas explícitamente. Por ejemplo, `uv sync` crea o sincroniza el entorno a partir de `pyproject.toml` y `uv.lock`.

`uv.lock` fija las versiones exactas de dependencias directas y transitivas para que la instalación sea reproducible. Si solo existe `pyproject.toml`, las versiones pueden resolverse de forma distinta en otro momento.

`requirements.txt` se mantiene como ruta compatible con `pip`, especialmente útil para usuarios de Windows o para quien no quiera usar `uv`.

## Dependencias principales

El notebook principal usa:

* Entorno interactivo Jupyter
  * `ipykernel`
  * `jupyterlab`

* Ecosistema LangChain, LangGraph y OpenAI
  * `langchain`
  * `langchain-core`
  * `langchain-openai`
  * `langchain-text-splitters`
  * `langgraph`
  * `openai`
  * `tiktoken`

* Procesamiento de datos, PDF y visualización
  * `matplotlib`
  * `numpy`
  * `pandas`
  * `pypdf`

* Red, validación de esquemas y configuración
  * `jsonschema`
  * `pydantic`
  * `python-dotenv`
  * `requests`

