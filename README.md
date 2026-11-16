# Pronóstico de ocupados en las 13 ciudades principales

Cuaderno de Jupyter que compara modelos de pronóstico (regresiones lineales con tendencia y estacionalidad, promedios móviles y suavización exponencial ETS) para la serie mensual de **ocupados** (en miles de personas), usando validación cronológica por bloques y una prueba final reservada.

> **Nota sobre las fechas:** el archivo de datos disponible termina en **junio de 2019**, por lo que el pronóstico de seis meses que genera el cuaderno corresponde a **julio–diciembre de 2019**.

## Contenido del repositorio

| Archivo | Descripción |
| --- | --- |
| `pronostico_ocupados_13_ciudades.ipynb` | Cuaderno principal con el análisis completo |
| `datosEmpleo.xlsx` | Fuente de datos (hoja `Hoja1`, columnas `mes` y `Ocupados`) |
| `requirements.txt` | Dependencias de Python |

## Requisitos

- Python 3.10 o superior
- Las dependencias listadas en `requirements.txt`

## Instalación

Se recomienda usar un entorno virtual:

```bash
# Crear y activar el entorno virtual
python -m venv .venv

# Windows
.venv\Scripts\activate

# macOS / Linux
source .venv/bin/activate

# Instalar dependencias
pip install -r requirements.txt
```

## Uso

1. Clona el repositorio y entra a la carpeta:

   ```bash
   git clone https://github.com/veroserna/Aprendizaje_Autom_3.git
   cd Aprendizaje_Autom_3
   ```

2. Deja `datosEmpleo.xlsx` junto al cuaderno (ya viene en el repo). También puedes:
   - ponerlo en una subcarpeta `data/`, o
   - indicar otra ubicación con la variable de entorno `DATOS_EMPLEO_PATH`:

     ```bash
     # Windows (cmd)
     set DATOS_EMPLEO_PATH=C:\ruta\a\datosEmpleo.xlsx

     # macOS / Linux
     export DATOS_EMPLEO_PATH=/ruta/a/datosEmpleo.xlsx
     ```

3. Abre y ejecuta el cuaderno:

   ```bash
   jupyter notebook pronostico_ocupados_13_ciudades.ipynb
   ```

   o con JupyterLab / VS Code. Ejecuta las celdas en orden (*Run All*): no requiere ningún ajuste de rutas.

## Estructura del análisis

1. **Carga y validación de datos** — verifica columnas, duplicados y faltantes; no imputa valores en silencio.
2. **Exploración básica** — descriptivos y trayectoria de la serie.
3. **Estrategia de evaluación** — seis bloques cronológicos de validación y seis meses finales reservados como prueba.
4. **Modelos candidatos** — regresiones (lineal, cuadrática, cúbica, con/sin estacionalidad), promedios móviles simples y ponderados, y configuraciones ETS.
5. **Evaluación y comparación** — selección por RMSE promedio de validación; MAE y sMAPE como complemento.
6. **Diagnóstico y pronóstico** — pruebas de residuos de la mejor regresión y del modelo ETS ganador, y pronóstico de seis meses con intervalos de predicción del 95 %.
7. **Conclusión y limitaciones**.
