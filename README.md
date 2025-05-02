# API-ProteinFolder

**API-ProteinFolder** es una API REST desarrollada en **Flask** que proporciona funcionalidades para el análisis y gestión de archivos relacionados con estructuras de proteínas. Esta API actúa como el backend del proyecto [Protein-folder](https://github.com/ramaffei/ProteinFolder-WEB).

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/) 
[![Flask](https://img.shields.io/badge/Flask-3.0.2-green.svg)](https://flask.palletsprojects.com/) 
[![Biopython](https://img.shields.io/badge/Biopython-1.83-yellow.svg)](https://biopython.org/)

## Características Principales

- **Carga y extracción de archivos ZIP** con archivos PDB y JSON.
- **Análisis de archivos PDB** para obtener ángulos phi-psi.
- **Generación de gráficos de Ramachandran** a partir de archivos PDB.
- **Cálculo y visualización de Z-scores** para comparación estructural.
- **Integración con ESM Atlas** para predicción de estructuras de proteínas.
- **Procesamiento de archivos FASTA** para obtener estructuras similares.

## Requisitos

- Python 3.8+
- Flask 3.0+
- Biopython 1.83+
- Matplotlib
- NumPy
- SciPy
- Requests

## Instalación

### 1. Clonar el Repositorio

```bash
git clone https://github.com/ramaffei/api-protein-folder.git
cd api-protein-folder
```

### 2. Crear y Activar un Entorno Virtual (Recomendado)

```bash
python -m venv venv
```

Activar el entorno virtual:

- **En Windows**:
  ```bash
  venv\Scriptsctivate
  ```
- **En macOS y Linux**:
  ```bash
  source venv/bin/activate
  ```

### 3. Instalar Dependencias

```bash
pip install -r requirements.txt
```

### 4. Ejecutar la Aplicación

```bash
flask --app app run --debug
```

La API estará disponible en `http://localhost:5000/`.

## Estructura del Proyecto

```
api-protein-folder/
├── app.py                  # Aplicación principal Flask
├── prodconfig.py           # Configuración de producción
├── requirements.txt        # Dependencias del proyecto
├── results/                # Directorio para archivos generados
└── src/
    ├── AlphaRamachan.py    # Generación de diagramas de Ramachandran
    ├── esm_api.py          # Integración con ESM Atlas
    ├── fetch_pdb.py        # Obtención de ángulos phi-psi
    ├── functions.py        # Funciones auxiliares
    └── z_scores.py         # Cálculo y visualización de Z-scores
```

## Endpoints de la API

### Status del Servidor

#### `GET /`
- **Descripción**: Verifica si el servidor está en funcionamiento.
- **Respuesta**: `{'msg':'SERVER UP'}`

### Carga y Extracción de Archivos

#### `POST /upload/`
- **Descripción**: Recibe un archivo ZIP y extrae su contenido, organizando los archivos por extensión.
- **Parámetros**:
  - `zipFile`: Archivo ZIP a procesar
- **Respuesta**: JSON con rutas relativas de los archivos extraídos, organizados por extensión.

### Análisis de Archivos PDB

#### `POST /pdb/`
- **Descripción**: Procesa archivos PDB para obtener ángulos phi-psi.
- **Parámetros**:
  - `filenames`: Array de rutas relativas a los archivos PDB
  - `ignored_residues` (opcional): Booleano para incluir residuos ignorados
- **Respuesta**: JSON con ángulos phi-psi calculados.

### Generación de Gráficos

#### `POST /pdb/plots/`
- **Descripción**: Genera un gráfico de Ramachandran para los archivos PDB especificados.
- **Parámetros**:
  - `filenames`: Array de rutas relativas a los archivos PDB
- **Respuesta**: Imagen en formato base64.

#### `POST /pdb/plot/ramachandran/`
- **Descripción**: Genera un gráfico de Ramachandran para un solo archivo PDB.
- **Parámetros**:
  - `filename`: Ruta relativa al archivo PDB
- **Respuesta**: Imagen en formato base64.

#### `POST /json/plot/zscores/`
- **Descripción**: Genera un gráfico de Z-scores a partir de un archivo JSON.
- **Parámetros**:
  - `filename`: Ruta relativa al archivo JSON
- **Respuesta**: Imagen en formato base64.

#### `POST /pdb/plot/zscores/`
- **Descripción**: Compara dos archivos PDB y genera un gráfico de Z-scores.
- **Parámetros**:
  - `filenames`: Array con exactamente 2 rutas relativas a archivos PDB
- **Respuesta**: Imagen en formato base64.

### Integración con ESM Atlas

#### `POST /pdb/esm/fasta/`
- **Descripción**: Procesa un archivo FASTA para obtener estructuras de proteínas.
- **Parámetros**:
  - `fastaFile`: Archivo FASTA con secuencias de proteínas
- **Respuesta**: JSON con información sobre las estructuras obtenidas.

## Integración con Protein-folder Frontend

Esta API está diseñada para funcionar como backend del proyecto **Protein-folder**, proporcionando todas las funcionalidades necesarias para:

- Procesar archivos de proteínas cargados por el usuario.
- Realizar análisis estructurales.
- Generar visualizaciones relevantes.
- Obtener predicciones de estructura mediante ESM Atlas.

## Manejo de Errores

La API proporciona mensajes de error claros en formato JSON, incluyendo:

- Código de estado HTTP apropiado
- Mensaje descriptivo del error
- Datos adicionales cuando sea relevante

## Contacto

[Linkedin](https://www.linkedin.com/in/ramaffei)
