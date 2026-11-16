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
3. **Estacionariedad de la serie** — ADF y KPSS en nivel y primera diferencia, con lectura conjunta impresa.
4. **Estrategia de evaluación** — seis bloques cronológicos de validación y seis meses finales reservados como prueba.
5. **Modelos candidatos** — regresiones (lineal, cuadrática, cúbica, con/sin estacionalidad), promedios móviles simples y ponderados, y configuraciones ETS.
6. **Evaluación y comparación** — todos los modelos en una única tabla; selección por RMSE promedio de validación y evaluación única en la prueba final.
7. **Diagnóstico de residuos** — batería de pruebas de clase sobre la mejor regresión y sobre el modelo ETS ganador.
8. **Pronóstico de seis meses** — valores puntuales con intervalos de predicción del 95 %.
9. **Conclusión y limitaciones**.
