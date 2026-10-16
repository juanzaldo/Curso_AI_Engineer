# 00 · Memoria de instalación y preparación del entorno

[Volver al índice](README.md)

**Curso:** Bootcamp AI Engineer con Python — Código Facilito, segunda generación.  
**Sesión documentada:** 6–7 de octubre de 2026, zona horaria de Ciudad de México.  
**Entorno:** Windows x64 y PowerShell.  
**Rama de la práctica:** `practica/clase-1`.  
**Commit del ejercicio de Groq:** `fde2bf5` — `Implementa adaptador de Groq para clase 1`.  
**Estado:** entorno preparado, primera práctica de Groq publicada y memorias creadas localmente. Los pendientes se detallan al final.

Esta guía combina instrucciones para otro alumno con evidencia de la sesión original. Los apartados **Resultado observado** describen lo que se comprobó; los resultados esperados y los pasos opcionales no se presentan como pruebas realizadas.

## Contenido

1. [Objetivo y alcance](#1-objetivo-y-alcance)
2. [Criterios de éxito](#2-criterios-de-éxito)
3. [Requisitos previos](#3-requisitos-previos)
4. [Herramientas y decisiones](#4-herramientas-y-decisiones)
5. [Organización de carpetas](#5-organización-de-carpetas)
6. [Procedimiento de instalación](#6-procedimiento-de-instalación)
7. [Proveedores y primera práctica](#7-proveedores-y-primera-práctica)
8. [GitHub y publicación de la entrega](#8-github-y-publicación-de-la-entrega)
9. [Problemas y soluciones](#9-problemas-y-soluciones)
10. [Evidencias de validación](#10-evidencias-de-validación)
11. [Uso diario, respaldos y limpieza](#11-uso-diario-respaldos-y-limpieza)
12. [Pendientes, referencias y cambios](#12-pendientes-referencias-y-cambios)

## 1. Objetivo y alcance

Preparar un equipo para ejecutar el proyecto **Agente Operador**, comprender sus herramientas y entregar ejercicios en un repositorio propio de GitHub.

El proyecto del profesor es [Bootcamp_AI_Engineer_Codigofacilito_2nd_Gen](https://github.com/RamsesCamas/Bootcamp_AI_Engineer_Codigofacilito_2nd_Gen). Su asistente de operaciones procesa tickets y va incorporando capacidades durante el curso.

Se prepararon Python con uv, Git, el entorno virtual, VS Code, Ollama con un modelo local y las claves de Google Gemini y Groq. Se completó el adaptador de Groq y se publicó una rama de práctica.

**Decisiones de alcance:**

- Guardar código, herramientas principales, caché de uv y modelos locales en la carpeta `Codigo`.
- Usar PowerShell y los comandos del curso, sin introducir Docker ni otro gestor de entornos.
- Mantener Ollama como proveedor predeterminado y probar Gemini/Groq explícitamente.
- No integrar la API de OpenAI: el alumno descartó una facturación adicional por API. El uso con API key tiene una facturación separada de la suscripción de ChatGPT/Codex; esta decisión no altera la suscripción existente. [Referencia de OpenAI](https://learn.chatgpt.com/docs/pricing).
- Aprender haciendo: el alumno edita el código; la asistencia guía y revisa.

La organización en `Codigo` no convierte toda la instalación en portable: Windows, VS Code, los instaladores y la autenticación pueden guardar configuraciones, temporales o credenciales en el perfil de usuario.

## 2. Criterios de éxito

| Criterio | Cómo se verifica | Estado de esta sesión |
|---|---|---|
| uv ejecuta Python 3.11 | `uv run --no-project --python 3.11 python --version` | Confirmado |
| El proyecto tiene su propio entorno | `sys.executable` apunta a `bootcamp\.venv\Scripts\python.exe` | Confirmado |
| Las dependencias funcionan | Imports y pruebas con pytest | 17 pruebas aprobadas |
| Ollama puede ejecutar un modelo | Pregunta con `ollama run llama3.2` | Confirmado en la CLI |
| Gemini responde desde el proyecto | `uv run main.py --provider gemini ...` | Confirmado |
| Groq responde desde el proyecto | `uv run main.py --provider groq ...` | Confirmado después del ejercicio |
| Las claves están excluidas de Git | `git check-ignore .env` | Confirmado |
| La práctica está publicada | Rama remota y `git status` sincronizado | Confirmado antes de crear esta memoria |

La llamada real a Ollama **desde `main.py`** quedó propuesta, pero no se aportó su resultado. No se considera confirmada por el hecho de que la CLI de Ollama haya respondido.

## 3. Requisitos previos

- Un equipo Windows x64, acceso a PowerShell e Internet.
- Permiso para instalar aplicaciones en la cuenta del usuario.
- Una cuenta de GitHub. Google AI Studio y Groq requieren sus propias cuentas para obtener claves.
- Espacio para programas, descargas y modelos. Ollama es una de las piezas más grandes; hay que revisar el espacio libre antes de instalar.

**Equipo observado:** 16 GB de RAM y gráficos Intel Iris Xe. El modelo terminó ejecutándose con `100% CPU`; no se confirmó aceleración por GPU.

Para consultar RAM:

```powershell
Get-CimInstance Win32_ComputerSystem | Select-Object @{Name="RAM_GB";Expression={[math]::Round($_.TotalPhysicalMemory / 1GB)}}
```

Si el comando no tiene permiso, consultar **Administrador de tareas → Rendimiento → Memoria**. El hardware observado es una referencia de esta sesión, no una garantía de velocidad para otros equipos.

## 4. Herramientas y decisiones

| Elemento | Función | Decisión y resultado |
|---|---|---|
| PowerShell | Terminal para ejecutar comandos | Se usó durante toda la instalación y dentro de VS Code |
| uv | Instala Python y gestiona dependencias y entornos | Se instaló en `herramientas\uv`; versión verificada: **0.12.23** |
| Python | Intérprete que ejecuta el código | Se eligió 3.11 porque el proyecto acepta `>=3.11`; versión instalada: **3.11.17** |
| Git for Windows Portable | Historial, ramas y comunicación con GitHub | Extraído en `herramientas\git`; versión **2.56.0.windows.2** |
| GitHub | Alojamiento remoto de las entregas | Repositorio propio, conservando una conexión al del profesor |
| Git Credential Manager | Autenticación de Git con GitHub | Se seleccionó `manager` y se autorizó la cuenta en el navegador |
| VS Code | Editor y terminal integrados | Se abrió `bootcamp` y se seleccionó el intérprete de `.venv`; versión no registrada |
| Extensión Python de Microsoft | Integra Python con VS Code | Se configuró siguiendo la guía; el alumno confirmó los pasos |
| Ollama | Ejecuta modelos abiertos en el equipo | Instalado en `herramientas\ollama`; versión informada: **0.40.0** |
| Llama 3.2 | Modelo local para las prácticas | `llama3.2:latest`, ID `a80c4f17acd5`; respuesta real confirmada |
| Gemini / Groq | Ejecutan modelos mediante APIs remotas | Se configuraron claves privadas y se probaron ambos proveedores |

No se instaló Python mediante un instalador independiente: lo descargó uv. Tampoco se instalaron SDKs de Gemini, Groq u OpenAI; el proyecto ya realiza solicitudes HTTP con `httpx`.

Las versiones son las observadas en esta sesión. Para reconstruir las dependencias se conserva `uv.lock`; el instalador actual de una herramienta puede ofrecer una versión más reciente.

## 5. Organización de carpetas

```text
Codigo/
├── herramientas/
│   ├── uv/
│   ├── python/
│   ├── uv-tools/
│   ├── git/
│   │   └── cmd/git.exe
│   ├── ollama/
│   └── OllamaSetup.exe          # Instalador; puede retirarse después
├── cache/
│   ├── uv/
│   └── pytest-.../              # Temporales de pruebas
├── modelos/                    # Modelos de Ollama
└── bootcamp/                   # Raíz del repositorio Git
    ├── .git/
    ├── .venv/
    ├── .env                    # Privado; ignorado por Git
    ├── .env.example
    ├── .gitignore
    ├── pyproject.toml
    ├── uv.lock
    ├── main.py
    ├── core/
    ├── tests/
    ├── scripts/
    ├── logs/
    └── memoria/
        ├── README.md
        └── 00_memoria_de_Instalacion.md
```

`Codigo` contiene el espacio de trabajo completo; **solo `bootcamp` es el repositorio del curso**. Por eso `memoria` está dentro de `bootcamp`: podrá publicarse en GitHub sin subir herramientas o modelos.

## 6. Procedimiento de instalación

### 6.1 Elegir la ruta y abrir PowerShell

**Objetivo:** tener una raíz conocida para todas las instrucciones. Cada alumno puede cambiar la primera línea.

```powershell
$carpetaCurso = "C:\_juan\cursos\2026\AI Engineer con Python\Codigo"
New-Item -ItemType Directory -Path $carpetaCurso -Force | Out-Null
Set-Location $carpetaCurso
```

Las comillas son necesarias porque la ruta contiene espacios. Ejecutar solo el contenido de los bloques, sin copiar el prefijo `PS C:\...` de la terminal.

**Regla para toda la guía:** `$carpetaCurso` es una variable de la ventana actual. Si se abre otra terminal, repetir su asignación. Los pasos que requieren otra ubicación incluyen `Set-Location`.

### 6.2 Configurar ubicaciones de uv

**Motivo:** cambiar únicamente la ubicación de `uv.exe` no mueve sus descargas o instalaciones de Python. Por eso configuramos también esas rutas. [Opciones del instalador](https://docs.astral.sh/uv/reference/installer/) y [almacenamiento de uv](https://docs.astral.sh/uv/reference/storage/).

```powershell
$rutasUv = @{
    UV_INSTALL_DIR        = "$carpetaCurso\herramientas\uv"
    UV_PYTHON_INSTALL_DIR = "$carpetaCurso\herramientas\python"
    UV_PYTHON_BIN_DIR     = "$carpetaCurso\herramientas\uv"
    UV_CACHE_DIR          = "$carpetaCurso\cache\uv"
    UV_TOOL_DIR           = "$carpetaCurso\herramientas\uv-tools"
    UV_TOOL_BIN_DIR       = "$carpetaCurso\herramientas\uv"
}

foreach ($nombre in $rutasUv.Keys) {
    $ruta = $rutasUv[$nombre]
    New-Item -ItemType Directory -Path $ruta -Force | Out-Null
    [Environment]::SetEnvironmentVariable($nombre, $ruta, "User")
    [Environment]::SetEnvironmentVariable($nombre, $ruta, "Process")
}
```

`User` conserva la configuración para futuras sesiones del usuario; `Process` la aplica a esta ventana. El bloque puede terminar sin imprimir nada. Estas variables también afectan otros proyectos de uv ejecutados por esa cuenta. [Variables de entorno de uv](https://docs.astral.sh/uv/reference/environment/).

### 6.3 Instalar uv

```powershell
powershell -ExecutionPolicy Bypass -c "irm https://astral.sh/uv/install.ps1 | iex"
$env:Path = "$env:UV_INSTALL_DIR;$env:Path"
uv --version
```

**Qué significa el instalador:** `irm` abrevia `Invoke-RestMethod`, que obtiene el script; `|` entrega el resultado al siguiente comando; `iex` abrevia `Invoke-Expression`, que ejecuta ese texto. Se utiliza la dirección oficial. `Bypass` aplica al proceso de PowerShell lanzado para instalar.

`PATH` es la lista de carpetas donde la terminal busca ejecutables. La segunda línea permite encontrar uv inmediatamente en esta sesión.

**Resultado observado:** `uv 0.12.23`.

### 6.4 Instalar y comprobar Python

```powershell
uv python install 3.11
uv python find --managed-python 3.11
uv run --no-project --python 3.11 python -c "import sys; print('Python listo:', sys.version); print('Ubicacion:', sys.executable)"
```

**Motivo:** utilizar una versión compatible con el proyecto y administrarla con la misma herramienta. `--no-project` comprueba Python antes de tener un proyecto. [Python con uv](https://docs.astral.sh/uv/guides/install-python/).

**Resultado observado:** Python 3.11.17 y un ejecutable bajo:

```text
Codigo\herramientas\python\cpython-3.11-windows-x86_64-none\python.exe
```

### 6.5 Descargar y extraer Git Portable

**Motivo:** una cuenta de GitHub no instala Git en Windows. Hace falta Git para clonar y publicar.

1. Abrir la [descarga oficial de Git para Windows](https://git-scm.com/install/windows).
2. Elegir **Git for Windows/x64 Portable**.
3. Ejecutar el archivo descargado, en esta sesión `PortableGit-2.56.0.2-64-bit.7z.exe`.
4. En el destino de extracción, escribir la ruta completa equivalente a `$carpetaCurso\herramientas\git`.

El campo gráfico de extracción requiere la ruta escrita, no el nombre literal de la variable PowerShell.

**Verificar y agregar al PATH:**

```powershell
$rutaGit = "$carpetaCurso\herramientas\git\cmd"

if (Test-Path "$rutaGit\git.exe") {
    $pathUsuario = [Environment]::GetEnvironmentVariable("Path", "User")
    if (($pathUsuario -split ";") -notcontains $rutaGit) {
        [Environment]::SetEnvironmentVariable("Path", "$rutaGit;$pathUsuario", "User")
    }
    $env:Path = "$rutaGit;$env:Path"
    git --version
} else {
    Write-Host "No se encontro git.exe. Revisa la carpeta donde lo extrajiste."
}
```

**Resultado observado:** `git version 2.56.0.windows.2`.

Guardar el archivo autoextraíble en una carpeta llamada `git` no equivale a extraerlo. La subcarpeta `cmd` apareció después de ejecutar la extracción.

### 6.6 Clonar el proyecto del profesor

Ejecutar una sola vez, cuando `bootcamp` todavía no exista:

```powershell
Set-Location $carpetaCurso
git clone https://github.com/RamsesCamas/Bootcamp_AI_Engineer_Codigofacilito_2nd_Gen.git bootcamp
Set-Location "$carpetaCurso\bootcamp"
git status
Get-ChildItem
```

**Motivo:** clonar descarga archivos e historial. El nombre local `bootcamp` acorta la ruta.

**Resultado observado:** rama `main`, sin cambios pendientes, con `main.py`, `pyproject.toml` y `uv.lock`. En este momento `origin` apunta al profesor.

Esta guía parte de la base del profesor. Quien solo quiera consultar la solución puede abrir la rama publicada del alumno; no debe reemplazar con ella el ejercicio que quiera resolver por su cuenta.

### 6.7 Crear el entorno e instalar dependencias

```powershell
Set-Location "$carpetaCurso\bootcamp"
uv sync --python 3.11 --locked
if (!(Test-Path .env)) {
    Copy-Item .env.example .env
}
uv run python -c "import sys, httpx, pydantic; print('Entorno listo'); print(sys.executable)"
```

**Motivo:** `.venv` separa las librerías de esta práctica de otros proyectos. `pyproject.toml` declara requisitos; `uv.lock` fija la resolución de versiones. `--locked` evita actualizar silenciosamente ese archivo: si no coincide con la configuración, hay que investigar el error. [Proyectos con uv](https://docs.astral.sh/uv/guides/projects/).

La copia de `.env` solo se realiza si no existe; no se sobrescriben claves ya guardadas.

**Dependencias principales observadas:**

| Paquete | Versión instalada | Para qué se usa |
|---|---|---|
| `httpx` | 0.28.1 | Solicitudes HTTP a los proveedores |
| `pydantic` | 2.13.5 | Validación de datos |
| `pydantic-settings` | 2.15.0 | Lectura y validación de configuración |
| `pytest` | 9.1.1 | Pruebas automatizadas |
| `ruff` | 0.16.10 | Análisis y formato del código |

Se instalaron **20 paquetes**, incluyendo dependencias auxiliares. No se instalan manualmente uno por uno: los resuelve uv. La lista completa de versiones y dependencias se conserva en [uv.lock](../uv.lock).

**Resultado observado:** `Entorno listo` y ruta `bootcamp\.venv\Scripts\python.exe`. El entorno virtual utiliza el Python administrado instalado antes; ambos tienen funciones distintas.

### 6.8 Ejecutar las pruebas

```powershell
uv run pytest -q
```

Las pruebas incluidas usan simulaciones; no prueban tus claves ni requieren llamadas reales a los proveedores.

**Incidente observado:** 9 pruebas pasaron y 8 fallaron al preparar archivos temporales por acceso denegado en `AppData\Local\Temp\pytest-of-janzaldo`.

**Solución aplicada desde `bootcamp`:**

```powershell
$temporalPruebas = Join-Path (Split-Path $PWD.Path -Parent) ("cache\pytest-" + [guid]::NewGuid().ToString("N"))
uv run pytest -q --basetemp "$temporalPruebas"
```

Se asigna una carpeta nueva y única dentro de `Codigo\cache`. `--basetemp` es un directorio de trabajo que pytest puede limpiar; no se le entrega una carpeta con documentos propios. [Temporales de pytest](https://docs.pytest.org/en/stable/how-to/tmp_path.html).

**Resultado observado del alumno:** `17 passed in 0.27s`. No fue necesario reinstalar Python ni modificar los permisos de Windows.

### 6.9 Configurar Visual Studio Code

**Motivo:** editar archivos y ejecutar comandos en el mismo lugar.

1. Abrir VS Code. Si otro alumno no lo tiene, puede obtenerlo en la [descarga oficial](https://code.visualstudio.com/Download). En esta sesión no se registró la instalación del editor ni su versión.
2. Elegir **Archivo → Abrir carpeta** y seleccionar `Codigo\bootcamp`.
3. Revisar la confianza del espacio de trabajo al abrir el repositorio conocido del curso.
4. Abrir **Extensiones** con `Ctrl + Shift + X` e instalar **Python**, publicada por Microsoft.
5. Usar `Ctrl + Shift + P` → **Python: Select Interpreter**.
6. Seleccionar `bootcamp\.venv\Scripts\python.exe`; si no aparece, usar **Enter interpreter path**.
7. Abrir **Terminal → Nueva terminal** y elegir PowerShell.

**Comprobación:**

```powershell
uv run python -c "import sys; print(sys.executable)"
```

Debe apuntar a `.venv`. VS Code puede mostrar `(agente-operador)` al activar el entorno. Usar `uv run` permite ejecutar con las dependencias del proyecto sin depender de activar manualmente el entorno. [Entornos Python en VS Code](https://code.visualstudio.com/docs/python/environments).

**Distinción aprendida:** el intérprete ejecuta Python; el adaptador de un proveedor conecta con su API. Seleccionar el intérprete no implementa el adaptador de Groq.

### 6.10 Instalar Ollama en la ubicación elegida

En la nueva terminal, volver a definir la ruta base:

```powershell
$carpetaCurso = "C:\_juan\cursos\2026\AI Engineer con Python\Codigo"
$rutaModelos = "$carpetaCurso\modelos"
New-Item -ItemType Directory -Path $rutaModelos -Force | Out-Null
[Environment]::SetEnvironmentVariable("OLLAMA_MODELS", $rutaModelos, "User")
$env:OLLAMA_MODELS = $rutaModelos
```

Descargar manualmente `OllamaSetup.exe` desde [Ollama para Windows](https://ollama.com/download/windows) y guardarlo en `Codigo\herramientas`. Desde esa misma terminal, iniciar el instalador así:

```powershell
& "$carpetaCurso\herramientas\OllamaSetup.exe" "/DIR=`"$carpetaCurso\herramientas\ollama`""
```

Completar la ventana del instalador. `&` ejecuta un archivo cuya ruta está entre comillas; `/DIR` fija el destino. Las comillas internas preservan los espacios de la ruta.

Si Ollama ya estaba abierto cuando se cambió `OLLAMA_MODELS`, cerrarlo desde el icono junto al reloj y volver a abrirlo para que lea la configuración.

```powershell
$env:Path = "$carpetaCurso\herramientas\ollama;$env:Path"
ollama --version
[Environment]::GetEnvironmentVariable("OLLAMA_MODELS", "User")
ollama list
```

**Resultado observado:** versión `0.40.0`, ruta de modelos bajo `Codigo\modelos` y lista inicialmente vacía.

El programa requiere varios GB y los modelos agregan espacio. Ollama documenta al menos 4 GB para la instalación binaria. La personalización del destino y de `OLLAMA_MODELS` está descrita en [Ollama para Windows](https://docs.ollama.com/windows).

**Incidente de esta sesión:** al hacer doble clic primero, Ollama se instaló en el perfil de usuario. Se desinstaló desde **Configuración → Aplicaciones → Aplicaciones instaladas** y luego se instaló indicando la ruta. No se corrigió borrando manualmente la carpeta del programa.

### 6.11 Descargar y probar el modelo local

```powershell
ollama pull llama3.2
ollama run llama3.2 "Responde en español en una sola frase: ¿qué es Python?"
ollama ps
```

**Motivo:** usar el modelo indicado por el curso y medir el resultado real. El modelo predeterminado de esta familia es de 3B parámetros y su descarga ronda 2 GB. [Ficha de Llama 3.2](https://ollama.com/library/llama3.2:3b).

**Resultado observado:** una respuesta correcta en español. `ollama ps` mostró:

```text
NAME              ID             SIZE     PROCESSOR  CONTEXT  RUNNER
llama3.2:latest    a80c4f17acd5   2.6 GB   100% CPU   4096     llamacpp
```

El tamaño mostrado durante la ejecución no es necesariamente igual al archivo descargado. No se midió la latencia de esta prueba; no hay una comparación válida de velocidad con las APIs.

Para liberar la memoria del modelo al terminar:

```powershell
ollama stop llama3.2
```

Esto detiene su ejecución, no borra el modelo del disco.

## 7. Proveedores y primera práctica

### 7.1 Configurar el proyecto para Ollama

Desde `bootcamp`, abrir `.env` en VS Code. También se puede abrir con:

```powershell
Set-Location "$carpetaCurso\bootcamp"
notepad .env
```

Editar las líneas existentes, sin duplicarlas. Esta es una plantilla **sin claves reales**:

```dotenv
GEMINI_API_KEY=
GROQ_API_KEY=

GEMINI_MODEL=gemini-3.8-flash
GROQ_MODEL=openai/gpt-oss-20b
OLLAMA_MODEL=llama3.2
OLLAMA_BASE_URL=http://localhost:11434/v1

PRIMARY=ollama
FALLBACKS=[]
TIMEOUT_S=120
MAX_RETRIES=3
LOG_PATH=logs/llm_calls.jsonl
```

| Variable | Significado y decisión |
|---|---|
| `PRIMARY` | Proveedor usado cuando no se indica otro en el comando |
| `FALLBACKS` | Proveedores de respaldo; `[]` evita activar respaldos antes de probarlos |
| `TIMEOUT_S` | Máxima espera por solicitud; se amplió a 120 segundos para la ejecución local |
| `MAX_RETRIES` | Reintentos ante errores transitorios; se conservó el valor del curso |
| `LOG_PATH` | Archivo local con registros de las llamadas |
| `*_MODEL` | Identificador del modelo de cada proveedor |
| `OLLAMA_BASE_URL` | API local que el adaptador del proyecto utiliza |

El archivo original traía Gemini como principal y Groq como respaldo. Se cambió esa configuración para poder comenzar con Ollama sin necesitar claves.

**Prueba propuesta para completar la comprobación local desde Python:**

```powershell
uv run main.py --provider ollama "Resume este ticket: el portal de proveedores no carga desde las 9:00 y hay tres facturas pendientes de registrar."
```

Resultado esperado: respuesta y línea de estadísticas con proveedor `ollama`. Este comando quedó pendiente de evidencia en la sesión; la prueba confirmada de Ollama fue la de su CLI.

### 7.2 Obtener y guardar las claves

Una API key identifica y autoriza a la cuenta que hace una solicitud. Cada alumno obtiene las suyas y las guarda en su propio `.env`.

1. **Google:** abrir [Google AI Studio — API Keys](https://aistudio.google.com/apikey), iniciar sesión y crear o seleccionar una clave del proyecto.
2. **Groq:** abrir [Groq — API Keys](https://console.groq.com/keys), iniciar sesión y crear una clave para el curso.
3. En `.env`, pegar cada clave justo después del `=`, en una sola línea, sin reemplazar otros ajustes:

```dotenv
GEMINI_API_KEY=TU_CLAVE_REAL_DE_GEMINI
GROQ_API_KEY=TU_CLAVE_REAL_DE_GROQ
```

Los textos anteriores son marcadores, no credenciales válidas. Guardar con **Ctrl + S**. No editar `.env.example` para guardar secretos ni compartir capturas de las claves.

Google explica la relación entre claves y proyectos en su [guía de API keys](https://ai.google.dev/gemini-api/docs/api-key); Groq documenta el alta en su [inicio rápido](https://console.groq.com/docs/quickstart).

**Estado observado:** el alumno guardó ambas claves y confirmó **Free Tier** en Google AI Studio. El nivel de facturación de Groq no se verificó en la conversación. Antes de replicar llamadas, cada alumno debe comprobar su propio plan y límites.

### 7.3 Probar Gemini

```powershell
uv run main.py --provider gemini "Responde en español en una frase: ¿qué es una API?"
```

El argumento `--provider gemini` selecciona ese proveedor para esta ejecución y desactiva respaldos en esa llamada. No reescribe `PRIMARY` en `.env`.

**Resultado observado:**

```text
gemini · gemini-3.8-flash · 43/27 tokens · 8806 ms · $0.000133
```

La respuesta describió una API como un puente para comunicar sistemas. El identificador del modelo funcionó en esa cuenta durante la sesión; no garantiza disponibilidad futura en todos los proyectos.

### 7.4 Completar GroqProvider en VS Code

**Objetivo:** resolver la parte de la clase 1 que conecta el proyecto a Groq.

**Cómo se identificó el ejercicio:** [providers.py](../core/providers.py) contenía un comentario `TODO(clase-1)` y un constructor que lanzaba `NotImplementedError`. Las instrucciones pedían consultar el endpoint, definir el nombre y quitar el bloqueo.

Antes:

```python
class GroqProvider(OpenAICompatibleProvider):
    def __init__(self, *args, **kwargs) -> None:
        raise NotImplementedError(
            "TODO(clase-1): implementa el adaptador de Groq. Pista: mira GeminiProvider."
        )
```

Pasos de aprendizaje:

1. Observar `GeminiProvider` y distinguir `name` de `base_url`.
2. Consultar el endpoint en la [documentación de Groq](https://console.groq.com/docs/openai).
3. Definir esos atributos en `GroqProvider`.
4. Eliminar el `__init__` que lanza el error y los comentarios del pendiente ya resuelto.
5. Conservar la función `build_provider` que aparece a continuación.
6. Guardar el archivo.

Después:

```python
class GroqProvider(OpenAICompatibleProvider):
    name = "groq"
    base_url = "https://api.groq.com/openai/v1"
```

**Por qué funciona:** la clase hereda el constructor y el método `generate()` de `OpenAICompatibleProvider`. La clase base ya prepara los encabezados, envía mensajes a `/chat/completions`, procesa respuestas y transforma errores. `build_provider` le entrega el modelo, la clave y el tiempo máximo configurados.

Quitar el constructor de bloqueo permite que se use el heredado. Agregar solo los atributos y conservar el `raise NotImplementedError` no habría resuelto el ejercicio.

**Prueba real realizada:**

```powershell
uv run main.py --provider groq "hola"
```

```text
groq · openai/gpt-oss-20b · 107/64 tokens · 615 ms · $0.000027
```

La respuesta saludó y ofreció asistencia. El prefijo `openai/` es parte del nombre del modelo servido por Groq; esta llamada utiliza el endpoint y la clave de Groq, no una clave de la API de OpenAI.

### 7.5 Interpretar tokens, tiempos y costo

La línea de estadísticas tiene este formato:

```text
proveedor · modelo · tokens_entrada/tokens_salida · latencia_ms · costo_estimado_USD
```

- Los tokens son unidades de texto procesadas, no equivalen necesariamente a palabras.
- La latencia es el tiempo medido de la solicitud.
- El costo se calcula en [core/pricing.py](../core/pricing.py), con una tabla local marcada como **ilustrativa**.

Por ejemplo, para la llamada registrada a Gemini, el código calculó:

```text
(43 × 0.75 + 27 × 3.75) / 1,000,000 = 0.0001335 USD
```

El programa no consulta si el proyecto de Google está en Free Tier y su estimación no es una factura. La facturación real se consulta en el proveedor. Google distingue niveles gratuitos y de pago en su [guía de facturación](https://ai.google.dev/gemini-api/docs/billing).

Ollama local registra 0 en esa función porque no hay una tarifa por llamada del proveedor remoto; sigue consumiendo recursos y electricidad del equipo.

### 7.6 Revisar el ejercicio

Desde la raíz del proyecto:

```powershell
uv run ruff check core/providers.py
$temporalPruebas = Join-Path (Split-Path $PWD.Path -Parent) ("cache\pytest-" + [guid]::NewGuid().ToString("N"))
uv run pytest -q --basetemp "$temporalPruebas"
git diff -- core/providers.py
```

Las comprobaciones offline realizadas sobre el adaptador dieron 17 pruebas aprobadas y Ruff sin errores. La revisión final del alumno mostró exactamente el reemplazo del constructor de bloqueo por los dos atributos; después se confirmó la llamada real a Groq.

No se completaron todos los ejercicios de la clase 1: siguen pendientes el reporte y la práctica de fallback, entre otros indicados en la sección 12.

## 8. GitHub y publicación de la entrega

### 8.1 Crear un repositorio propio vacío

En GitHub se creó:

[juanzaldo/Curso_AI_Engineer](https://github.com/juanzaldo/Curso_AI_Engineer)

Otro alumno debe crear el suyo bajo su propia cuenta. En esta sesión se eligió:

- Visibilidad **Public**, para permitir la revisión del profesor.
- **Add README:** desactivado.
- **Add .gitignore:** ninguno.
- **Add license:** ninguna en ese momento.

**Motivo:** el repositorio local ya contiene archivos e historial. Un repositorio remoto vacío evita introducir un historial adicional antes del primer push. Se creó un repositorio nuevo; no se utilizó el botón de fork.

### 8.2 Distinguir las dos conexiones remotas

| Nombre local | Destino | Uso |
|---|---|---|
| `origin` | Repositorio del alumno | Publicar prácticas |
| `upstream` | Repositorio del profesor | Consultar o incorporar futuras actualizaciones |

Estos nombres son alias de direcciones, no carpetas ni ramas. Que `git remote -v` muestre una URL de push para el profesor no concede permiso para escribir allí.

Desde `bootcamp`, con el `origin` original todavía apuntando al profesor:

```powershell
git remote -v
git remote rename origin upstream
```

Adaptar el usuario y repositorio antes de ejecutar el siguiente bloque:

```powershell
$usuarioGitHub = "TU_USUARIO"
$nombreRepo = "Curso_AI_Engineer"
git remote add origin "https://github.com/$usuarioGitHub/$nombreRepo.git"
git remote -v
```

**Resultado observado en esta sesión:**

```text
origin    https://github.com/juanzaldo/Curso_AI_Engineer.git
upstream  https://github.com/RamsesCamas/Bootcamp_AI_Engineer_Codigofacilito_2nd_Gen.git
```

La configuración de remotos no publica archivos. No hay que repetir `remote add` si el remoto ya existe; primero se revisa el estado. [Gestión de remotos en GitHub](https://docs.github.com/en/get-started/git-basics/managing-remote-repositories).

### 8.3 Subir main y autenticar Git

```powershell
git push -u origin main
```

**Motivo:** publicar la base del curso. Los cambios de Groq que todavía no tenían commit no se incluyeron en este push.

En la primera autenticación apareció **CredentialHelperSelector**:

1. Seleccionar **manager**.
2. Marcar **Always use this from now on**.
3. Continuar; en esta ventana podía usarse Enter.
4. Abrir la autenticación del navegador con la cuenta propia.
5. Revisar que la página esté en `github.com` y autorizar **Git Credential Manager / git-ecosystem**.
6. Regresar a la terminal.

La pantalla mostró permisos amplios sobre repositorios, gists y workflows. El alumno completó la autorización de su propia cuenta. El retorno a `127.0.0.1` devolvió el resultado a la aplicación local. No se copiaron tokens a los documentos. [Git Credential Manager y GitHub](https://docs.github.com/en/get-started/git-basics/caching-your-github-credentials-in-git).

**Resultado observado:**

```text
* [new branch] main -> main
branch 'main' set up to track 'origin/main'.
```

`-u` configura el seguimiento de la rama remota. Este uso de seguimiento no debe confundirse con el remoto al que dimos el nombre `upstream`.

### 8.4 Crear la rama y revisar la entrega

```powershell
git switch -c practica/clase-1
git status --short
git diff -- core/providers.py
git check-ignore .env
```

**Motivo:** separar el trabajo de la práctica de la rama base. Los cambios pendientes del archivo permanecieron al crear la rama.

**Resultado observado:** únicamente `core/providers.py` aparecía modificado y `git check-ignore .env` devolvió `.env`.

Este chequeo confirma la regla de exclusión del archivo en esta instalación; no equivale a una auditoría de todo el historial de cualquier repositorio.

### 8.5 Guardar y publicar el ejercicio

Ejecutar los comandos por separado y revisar el diff antes del commit:

```powershell
git add core/providers.py
git diff --cached
git commit -m "Implementa adaptador de Groq para clase 1"
git push -u origin practica/clase-1
git status
```

| Comando | Qué hace |
|---|---|
| `git add` | Prepara el archivo que formará parte del próximo commit |
| `git diff --cached` | Muestra lo preparado |
| `git commit` | Registra una versión local con un mensaje |
| `git push` | Publica los commits en GitHub |
| `git status` | Informa rama, sincronización y cambios pendientes |

Si otro alumno recibe `Author identity unknown`, debe configurar su identidad antes de repetir el commit. Dentro de ese repositorio puede usar:

```powershell
git config user.name "Tu nombre"
git config user.email "TU_CORREO_DE_GIT"
```

Usar el correo elegido para GitHub, o el correo de privacidad que muestra GitHub en la configuración de la cuenta. Este error no se reportó en la sesión original; se incluye como ayuda de reproducción.

**Resultado final informado por el alumno:**

```text
On branch practica/clase-1
Your branch is up to date with 'origin/practica/clase-1'.

nothing to commit, working tree clean
```

La comprobación local previa a redactar esta memoria identificó el commit `fde2bf5`.

**Entrega:** [rama practica/clase-1](https://github.com/juanzaldo/Curso_AI_Engineer/tree/practica/clase-1).

No se creó un pull request ni se mezcló la práctica a `main`. El estado limpio anterior corresponde al código publicado, antes de añadir estos Markdown.

### 8.6 Publicar estas memorias después de revisarlas

La memoria y el índice se crean localmente por autorización del alumno. Su publicación se realiza como un paso separado:

```powershell
git status
git add memoria/README.md memoria/00_memoria_de_Instalacion.md
git diff --cached
git commit -m "Documenta instalacion y preparacion del entorno"
git push
```

Esta publicación de documentos todavía no forma parte de la evidencia de la sesión.

## 9. Problemas y soluciones

| Síntoma | Causa identificada o límite de la comprobación | Solución aplicada |
|---|---|---|
| `git` no se reconocía en PowerShell | El Git detectado por la asistencia pertenecía a su propio entorno; no estaba disponible en la terminal del alumno | Extraer Git Portable y añadir su carpeta `cmd` al PATH |
| No existía `git\cmd\git.exe` | Solo estaba descargado el autoextraíble dentro de `git` | Ejecutar el archivo y extraerlo en la ruta elegida |
| 9 pruebas aprobadas y 8 errores | Pytest no podía acceder a una carpeta temporal de Windows | Utilizar una carpeta nueva con `--basetemp` bajo `Codigo\cache` |
| Aviso de caché durante una comprobación de la asistencia | La cuenta de la asistencia no pudo escribir en `.pytest_cache`; las pruebas sí pasaron | Se registró como aviso, sin cambiar permisos ni tratarlo como fallo del código |
| Ollama se instaló bajo `Users` | Se abrió con doble clic, sin el argumento de destino | Desinstalar desde Aplicaciones y reinstalar con `/DIR` |
| Duda entre el instalador y el programa | `OllamaSetup.exe` instala; la carpeta `ollama` contiene el programa en uso | Se aclaró qué se puede retirar y qué debe conservarse |
| `ollama list` no mostraba modelos | Ollama estaba instalado, pero aún no había un modelo descargado | Ejecutar `ollama pull llama3.2` |
| Groq estaba bloqueado por un pendiente | Su `__init__` lanzaba `NotImplementedError` | Resolver el adaptador y eliminar ese constructor |
| Gemini mostró un importe pese a Free Tier | El código calcula precios ilustrativos sin consultar el nivel de cuenta | Revisar `core/pricing.py` y confirmar el nivel en AI Studio |
| Ventanas de credenciales durante el push | Git necesitaba autenticar la cuenta del alumno | Elegir `manager` y completar la autorización en GitHub |

Si una terminal nueva de VS Code no reconoce un programa recién agregado al PATH, cerrar y volver a abrir VS Code para que herede el entorno actualizado. Verificar después `uv --version`, `git --version` u `ollama --version`, según corresponda.

No se debe repetir una instalación ni borrar carpetas por un error de comando sin comprobar primero la ruta y el mensaje.

## 10. Evidencias de validación

| Elemento | Evidencia | Alcance |
|---|---|---|
| uv | 0.12.23, comprobado al preparar la memoria | Ejecutable instalado |
| Python | 3.11.17 y ruta bajo `herramientas\python` | Instalación administrada |
| Entorno virtual | `Entorno listo` y ruta bajo `bootcamp\.venv` | Imports y entorno del proyecto |
| Dependencias | 20 paquetes instalados con uv | Resolución del curso |
| Pruebas | `17 passed in 0.27s`, informado por el alumno | Pruebas offline después de cambiar temporales |
| Adaptador Groq | 17 pruebas y Ruff correctos durante la comprobación de la asistencia; un aviso de caché | Validación offline, distinta de la autenticación real |
| Ollama | Versión 0.40.0; Llama 3.2 respondió y mostró 100% CPU | CLI local; llamada desde el proyecto no confirmada |
| Gemini | 43/27 tokens, 8806 ms, estimación USD 0.000133 | Una llamada real desde el proyecto |
| Cuenta de Google | El alumno confirmó Free Tier | Nivel informado, no una auditoría de facturación |
| Groq | 107/64 tokens, 615 ms, estimación USD 0.000027 | Una llamada real desde el proyecto |
| Secretos | `git check-ignore .env` devolvió `.env` | Exclusión local confirmada |
| Publicación | `main` y `practica/clase-1` publicados; estado limpio y sincronizado | Código del ejercicio, previo a los documentos nuevos |

Estas dos latencias de APIs corresponden a solicitudes diferentes; no son un benchmark entre modelos. No se conservaron claves en esta memoria ni fue necesario leer el `.env` privado para redactarla.

## 11. Uso diario, respaldos y limpieza

### 11.1 Retomar la práctica

1. Abrir la carpeta `bootcamp` en VS Code.
2. Abrir una terminal PowerShell.
3. Confirmar ubicación, rama e intérprete:

```powershell
Get-Location
git status
uv run python -c "import sys; print(sys.executable)"
```

4. Elegir el proveedor de la práctica:

```powershell
uv run main.py --provider gemini "Explica una API en una frase."
uv run main.py --provider groq "Explica una API en una frase."
```

Los comandos anteriores son alternativas, no una obligación de ejecutar ambos. Revisar cuotas y plan antes de utilizar APIs.

Para trabajar localmente, abrir Ollama y comprobar su disponibilidad:

```powershell
ollama list
uv run main.py --provider ollama "Explica una API en una frase."
```

Este último comando también sirve para completar la comprobación que quedó pendiente.

Si cambian las dependencias del curso o se reconstruye `.venv`, usar `uv sync --python 3.11 --locked`. No hay que reinstalar todo en cada sesión.

### 11.2 Terminar la sesión

```powershell
git status
ollama stop llama3.2
```

Revisar los archivos modificados antes de preparar el siguiente commit. No subir `.env`, modelos, programas ni el entorno virtual.

### 11.3 Qué se puede respaldar en una SD y qué se conserva

| Elemento | Qué hacer | Consecuencia |
|---|---|---|
| `OllamaSetup.exe` | Copiar a la SD o borrar cuando la instalación funciona | No desinstala Ollama; habría que descargarlo otra vez para reinstalar |
| `PortableGit-...7z.exe` | Copiar o borrar después de extraer Git correctamente | El Git extraído sigue funcionando |
| `bootcamp`, código y memorias | Respaldar y conservar la copia de trabajo | Una copia completa puede contener `.env`; no distribuirla sin revisar |
| `pyproject.toml` y `uv.lock` | Conservar en Git y en respaldos | Permiten reconstruir las dependencias |
| `herramientas\uv`, `python`, `git`, `ollama` | Mantener mientras se usen | Moverlas puede romper PATH, accesos directos y referencias de `.venv` |
| `.venv` | No necesita distribuirse a otros alumnos | Cada equipo la reconstruye con uv; no es un entorno portable |
| `cache\uv` | Se puede limpiar con `uv cache clean` si hace falta espacio | Futuras operaciones pueden volver a descargar paquetes |
| Temporales `cache\pytest-...` | Se pueden retirar al terminar las pruebas | Confirmar que son temporales de pruebas, no otros archivos |
| `modelos` | Conservar para seguir trabajando sin descargarlos otra vez | Moverlos exige reconfigurar Ollama y puede afectar la velocidad de carga |
| `.env` | Conservar de forma privada | No incluirlo en materiales compartidos o en GitHub |

Los instaladores almacenados consumen disco, no RAM o CPU por el hecho de existir. Ejecutar un modelo sí utiliza memoria y procesamiento. Una SD puede servir como respaldo, pero no se verificó su velocidad para ejecutar modelos; se mantuvieron las instalaciones activas en el disco interno.

Para distribuir el curso a compañeros, compartir el repositorio y estas memorias. Cada persona instala su entorno y crea sus propias claves. No hace falta copiar toda la carpeta `Codigo`.

## 12. Pendientes, referencias y cambios

### Pendientes explícitos

- Obtener evidencia de una respuesta de Ollama desde `uv run main.py --provider ollama ...`.
- Confirmar el nivel de facturación y los límites de Groq si se van a hacer más llamadas.
- Practicar el fallback y revisar su registro.
- Completar `scripts/report.py`, que mantiene un `TODO(clase-1)`.
- Evaluar el ejercicio opcional `--temperature` cuando corresponda.
- Revisar y publicar estos dos documentos con un commit separado.
- Crear las siguientes memorias por clase, añadiendo sus enlaces al [índice](README.md).

La instalación y la publicación del adaptador de Groq no significan que todos los ejercicios de la clase 1 estén terminados.

### Referencias para consultar durante la réplica

| Tema | Fuente |
|---|---|
| Requisitos y ejercicios del curso | [README del proyecto](../README.md) |
| uv: instalación | [Instalador](https://docs.astral.sh/uv/reference/installer/) |
| uv: directorios y variables | [Almacenamiento](https://docs.astral.sh/uv/reference/storage/) · [Variables](https://docs.astral.sh/uv/reference/environment/) |
| uv: Python y proyectos | [Python](https://docs.astral.sh/uv/guides/install-python/) · [Proyectos](https://docs.astral.sh/uv/guides/projects/) |
| Git para Windows | [Descarga oficial](https://git-scm.com/install/windows) |
| Entornos en VS Code | [Documentación de Python](https://code.visualstudio.com/docs/python/environments) |
| Ollama | [Windows](https://docs.ollama.com/windows) · [Hardware](https://docs.ollama.com/gpu) · [Inicio rápido](https://docs.ollama.com/quickstart) |
| Modelo local | [Llama 3.2](https://ollama.com/library/llama3.2:3b) |
| Gemini | [Claves](https://ai.google.dev/gemini-api/docs/api-key) · [Facturación](https://ai.google.dev/gemini-api/docs/billing) |
| Groq | [Inicio rápido](https://console.groq.com/docs/quickstart) · [Compatibilidad de API](https://console.groq.com/docs/openai) |
| GitHub | [Remotos](https://docs.github.com/en/get-started/git-basics/managing-remote-repositories) · [Credenciales](https://docs.github.com/en/get-started/git-basics/caching-your-github-credentials-in-git) |
| pytest | [Directorios temporales](https://docs.pytest.org/en/stable/how-to/tmp_path.html) |

Los enlaces apuntan a documentación que puede cambiar. Para las evidencias históricas de esta instalación se conservan aquí la fecha, las versiones y los resultados concretos.

### Registro de cambios

| Fecha | Cambio |
|---|---|
| 2026-10-07 | Primera memoria: instalación, configuración, práctica de Groq, publicación en GitHub, incidencias y pendientes de la sesión del 6–7 de octubre |
