# Configuración del entorno para `entrega_final.ipynb`

Este directorio contiene la configuración mínima para ejecutar la entrega final de la asignatura Large Language Models.

El notebook principal es:

```text
entrega_final.ipynb
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


## Instalación en macOS y Linux con `make`

Esta es la ruta recomendada para macOS y Linux.

Requisitos:

- `make`.
- Conexión a internet en la primera instalación.

No hace falta instalar Python manualmente: `uv` instalará Python `3.11.9` y creará el entorno virtual.

### Instalar `make`

Comprueba si ya lo tienes:

```bash
make --version
```

Si no está instalado:

- macOS:
  ```bash
  xcode-select --install
  ```

- Ubuntu/Debian:
  ```bash
  sudo apt update
  sudo apt install make
  ```

- Fedora:
  ```bash
  sudo dnf install make
  ```

- Arch Linux:
  ```bash
  sudo pacman -S make
  ```

Configura todo con:

```bash
make setup
```

Abre el notebook con:

```bash
make notebook
```

En Jupyter, selecciona el kernel:

```text
Python 3.11 (pontia-llms-entrega-final)
```

## Instalación manual en macOS/Linux

Si no quieres usar `make`, también puedes instalar con `venv` y `pip`:

```bash
python3.11 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
python -m ipykernel install --user --name pontia-llms-entrega-final --display-name "Python 3.11 (pontia-llms-entrega-final)"
jupyter lab entrega_final.ipynb
```


## Instalación en Windows

En Windows nativo es necesario usar Python `3.11` y `requirements.txt`.

Comprueba si tienes Python 3.11:

```powershell
py -3.11 --version
```

Si no lo tienes, instala Python 3.11 de 64 bits desde:

```text
https://www.python.org/downloads/
```

Durante la instalación, marca **Add python.exe to PATH**. Después cierra y vuelve a abrir PowerShell.

Opción recomendada. Desde la carpeta del proyecto:

```powershell
uv sync
```

Alternativa con pip (requiere Python 3.11). Desde la carpeta del proyecto:

```powershell
python3.11 -m venv .venv
.\.venv\Scripts\activate
python -m pip install --upgrade pip
pip install -r requirements.txt
python -m ipykernel install --user --name pontia-llms-entrega-final --display-name "Python 3.11 (pontia-llms-entrega-final)"
jupyter lab entrega_final.ipynb
```

En Jupyter, selecciona el kernel:

```text
Python 3.11 (pontia-llms-entrega-final)
```


## Sobre `pyproject.toml`, `uv.lock`, `Makefile` y `requirements.txt`

`python -m venv .venv` solo crea un entorno virtual vacío. No instala dependencias automáticamente ni lee `pyproject.toml` por sí mismo.

El archivo `pyproject.toml` declara el proyecto, la versión de Python requerida y las dependencias directas. Herramientas como `uv` o `pip` pueden usarlo, pero hay que invocarlas explícitamente. Por ejemplo, `uv sync` crea o sincroniza el entorno a partir de `pyproject.toml` y `uv.lock`.

`uv.lock` fija las versiones exactas de dependencias directas y transitivas para que la instalación sea reproducible. Si solo existe `pyproject.toml`, las versiones pueden resolverse de forma distinta en otro momento.

`Makefile` no es obligatorio, pero simplifica la experiencia: instala `uv` si hace falta, instala Python `3.11.9`, sincroniza dependencias, registra el kernel de Jupyter y verifica imports con un solo comando.

`requirements.txt` se mantiene como ruta compatible con `pip`, especialmente útil para usuarios de Windows o para quien no quiera usar `uv`.

## Dependencias principales

El notebook usa:

- `openai`
- `numpy`
- `pandas`
- `requests`
- `jsonschema`
- `python-dotenv`
- `jupyterlab`
- `ipykernel`

`uv.lock` fija las dependencias transitivas para la ruta macOS/Linux con `make setup`. `requirements.txt` contiene una exportación fijada de dependencias para instalación manual con `pip`, especialmente útil en Windows.

## Comandos útiles

```bash
make check
```

Verifica imports y versiones principales.

```bash
make lock
```

Actualiza `uv.lock` tras cambiar dependencias.

```bash
make clean
```

Elimina `.venv`.
