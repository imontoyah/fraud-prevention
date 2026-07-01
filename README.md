# Prevención de Fraude — Mercado Libre

Solución de Machine Learning end to end para predecir si una transacción es
fraudulenta, con el objetivo de **maximizar la ganancia** de la empresa dada la asimetría de
costos del problema, donde se gana el 25 % del monto por cada transacción legítima aprobada y se
pierde el 100 % por cada fraude aprobado.

El trabajo cubre análisis exploratorio, feature engineering, selección y ajuste de modelos y selección del umbral de decisión por ganancia.

## Estructura del proyecto

```
fraud-prevention/
├── data/
│   ├── fraud_meli_dataset.csv       # dataset de entrada (ver sección "Datos")
│   └── processed/
│       └── fraud_fe.parquet         # dataset procesado (lo genera el notebook 02)
├── notebooks/
│   ├── 01_fraud_eda.ipynb           # análisis exploratorio (EDA)
│   ├── 02_feature_engineering.ipynb # transformaciones + baseline de importancia
│   └── 03_modeling.ipynb            # modelos, umbral y evaluación
├── pyproject.toml                   # dependencias del proyecto
├── uv.lock                          # versiones exactas (lock)
└── README.md
```

## Requisitos

- Python 3.12 o superior.
- [uv](https://docs.astral.sh/uv/) como gestor de entorno y dependencias.

## Instalación

1. Clonar el repositorio:

   ```bash
   git clone <URL-DEL-REPOSITORIO>
   cd fraud-prevention
   ```

2. Crear el entorno e instalar las dependencias (uv lee `pyproject.toml` y `uv.lock`):

   ```bash
   uv sync
   ```

   > Alternativa sin uv: crear un entorno virtual con Python 3.12 e instalar las dependencias
   > listadas en `pyproject.toml` con `pip` (`pandas`, `numpy`, `matplotlib`, `seaborn`,
   > `jupyter`, `scikit-learn`, `pyarrow`, `lightgbm`).

## Datos

El notebook espera el dataset de entrada en la ruta `data/fraud_meli_dataset.csv`. Dado que no se incluye en
el repositorio, se debe descargar desde la URL indicada en el enunciado y colocarlo en esa ruta con el nombre especificado.

## Ejecución

Ejecutar los notebooks **en orden**, ya que cada uno depende del anterior:

1. **`01_fraud_eda.ipynb`** — Análisis exploratorio y validación de las hipótesis iniciales.
2. **`02_feature_engineering.ipynb`** — Aplica las transformaciones y guarda el dataset procesado
   en `data/processed/fraud_fe.parquet`.
3. **`03_modeling.ipynb`** — Entrena y compara los modelos, selecciona el umbral de decisión por ganancia y evalúa
   el resultado final sobre el conjunto de prueba.


## Reproducibilidad

Todos los procesos con componente aleatorio (entrenamiento de modelos, búsqueda de
hiperparámetros y permutation importance) usan una semilla fija (`SEED = 42`), por lo que los
resultados son reproducibles entre ejecuciones.

