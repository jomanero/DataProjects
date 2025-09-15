# Proyecto: Emisiones de GEI en España

Esta carpeta contiene la estructura base para analizar y modelizar las emisiones de gases de efecto invernadero (GEI) en España.
Sigue la metodología descrita en las fases de trabajo acordadas. A continuación se detalla el contenido recomendado de cada directorio.

## Estructura de carpetas

- `data/`
  - `raw/`: coloca aquí los ficheros originales descargados de las fuentes oficiales. **No los modifiques** para mantener una copia fiel.
    - Ejemplos: `ine_emisiones_gei_sector_anual.csv`, `ine_emisiones_indicadores.xlsx`.
  - `processed/`: guarda los datasets limpios y transformados listos para el análisis y la modelización.
  - `external/`: datasets de apoyo (PIB, población, consumo energético, etc.).
- `notebooks/`: cuadernos Jupyter numerados siguiendo el flujo de trabajo (ver sección *Notebooks sugeridos*).
- `src/`: scripts reutilizables.
  - `data/`: funciones para ingesta y limpieza.
  - `features/`: generación de variables derivadas y ratios.
  - `models/`: entrenamiento, evaluación y serialización de modelos.
  - `visualization/`: utilidades para gráficos.
- `reports/`
  - `figures/`: exporta aquí las imágenes y gráficos utilizados en informes.
- `models/`: archivos `.pkl` o `.joblib` con los modelos entrenados.
- `references/`: documentación, diccionarios de datos y normativa relevante.
- `docs/`: reportes intermedios, memorias y guion del vídeo final.
- `tests/`: pruebas unitarias o de integración para scripts Python.

## Notebooks sugeridos

1. `01_carga_datos.ipynb`: lectura y exploración inicial, validaciones básicas.
2. `02_limpieza_transformacion.ipynb`: tratamiento de nulos, normalizaciones y creación de ratios.
3. `03_eda_temporal_sectorial.ipynb`: análisis y visualizaciones temporales y por sector.
4. `04_eda_geografico.ipynb`: análisis territorial, mapas coropléticos.
5. `05_modelos_series_temporales.ipynb`: ARIMA, Prophet y evaluación.
6. `06_modelos_ml_supervisado.ipynb`: regresión lineal, Random Forest, XGBoost.
7. `07_escenarios_interpretacion.ipynb`: generación de escenarios y síntesis de hallazgos.

Numera los cuadernos según el orden de ejecución para facilitar la reproducción del flujo.

## Recomendaciones para el repositorio

- Mantén los datos sin versionar en Git añadiendo las rutas a `.gitignore` (ver sección siguiente).
- Documenta cada transformación en celdas Markdown dentro de los notebooks.
- Utiliza entornos virtuales gestionados con Anaconda o `conda env export` para compartir dependencias.

## Guía paso a paso en Anaconda

Sigue este itinerario como si acabaras de recibir el proyecto en tu equipo.

### 1. Descargar o clonar el repositorio

1. Abre **Anaconda Prompt** (Windows) o una terminal con Anaconda activo (macOS/Linux).
2. Sitúate en la carpeta donde guardas tus proyectos, por ejemplo:
   ```bash
   cd "C:\Users\tu_usuario\Documentos"
   ```
3. Copia la carpeta `emisiones_gei_espana` en tu equipo. Si trabajas con Git, clona el repositorio:
   ```bash
   git clone <URL_DEL_REPOSITORIO>
   cd DataProjects/emisiones_gei_espana
   ```

### 2. Crear y activar un entorno conda

1. Crea un entorno limpio para el proyecto (puedes cambiar el nombre si lo prefieres):
   ```bash
   conda create -n gei_emisiones python=3.10
   ```
2. Activa el entorno recién creado:
   ```bash
   conda activate gei_emisiones
   ```
3. Comprueba que el entorno aparece como activo con `conda info --envs`.

### 3. Instalar las dependencias principales

Instala las librerías necesarias desde `conda-forge` para garantizar versiones compatibles:

```bash
conda install -c conda-forge pandas numpy matplotlib seaborn plotly scikit-learn statsmodels
conda install -c conda-forge prophet
conda install -c conda-forge xgboost
pip install joblib
```

Si necesitas librerías adicionales (ej. `geopandas`, `folium`), instálalas ahora. Finaliza con `pip list` o `conda list` para revisar las versiones.

### 4. Registrar el kernel en Jupyter

Vincula el entorno a Jupyter para seleccionarlo fácilmente en tus notebooks:

```bash
python -m ipykernel install --user --name gei_emisiones --display-name "GEI emisiones"
```

### 5. Organizar los datos originales

1. Crea, si no existen, las carpetas `data/raw/`, `data/processed/` y `data/external/` (ya están en el repositorio como contenedores vacíos).
2. Copia tus ficheros fuente (`ine_emisiones_gei_sector_anual`, `ine_emisiones_indicadores`, etc.) dentro de `data/raw/` **sin modificarlos**.
3. Documenta en `references/` cualquier diccionario de datos o nota metodológica.

### 6. Verificar el entorno

Ejecuta una comprobación rápida para confirmar que las librerías se cargan correctamente:

```bash
python -c "import pandas as pd; import prophet; from sklearn.ensemble import RandomForestRegressor; print('Entorno configurado correctamente')"
```

Si aparece el mensaje final sin errores, el entorno está listo.

### 7. Abrir el proyecto en Jupyter

1. Desde la carpeta `emisiones_gei_espana`, lanza Jupyter:
   ```bash
   jupyter lab
   ```
   o, si prefieres, `jupyter notebook`.
2. Crea el primer cuaderno en `notebooks/` con el kernel **GEI emisiones** seleccionado y guarda como `01_carga_datos.ipynb`.
3. Sigue la numeración sugerida para mantener el flujo de trabajo ordenado.

### 8. Guardar resultados y versionar

1. Exporta gráficos a `reports/figures/` y modelos entrenados a `models/`.
2. Utiliza Git para versionar notebooks, scripts y documentación:
   ```bash
   git status
   git add notebooks/01_carga_datos.ipynb src/
   git commit -m "Analisis inicial de emisiones"
   ```
3. Si usas un repositorio remoto, realiza `git push` para sincronizar tu trabajo.

## Archivo `.gitignore`

Se proporciona un fichero `.gitignore` en la raíz del proyecto para evitar versionar datos sensibles o pesados. Si añades nuevas carpetas de datos, recuerda incluirlas allí.

## Próximos pasos recomendados

1. Completa el notebook `01_carga_datos.ipynb` cargando y describiendo los datasets.
2. Avanza al cuaderno `02_limpieza_transformacion.ipynb` para preparar los datos.
3. Continúa con el EDA (`03_` y `04_`) y, posteriormente, con la modelización (`05_` y `06_`).
4. Documenta los hallazgos y escenarios en `07_escenarios_interpretacion.ipynb` y en los informes de `docs/` y `reports/`.

¡Listo para empezar el análisis con Anaconda!
