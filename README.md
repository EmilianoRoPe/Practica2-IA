# Practica 2: EDA y preparacion de datasets

Proyecto academico de analisis exploratorio y preparacion de dos datasets de clasificacion. El flujo principal esta en `Practica2_EDA.ipynb`.

## Contenido del proyecto

- `Practica2_EDA.ipynb`: notebook principal con decisiones metodologicas, comprension del dominio, perfilado, EDA, particion de datos, imputacion, winsorizacion, balanceo, modelado y conclusiones.
- `data/adult.csv`: Adult Income; objetivo `income` (la clase positiva se define como ingreso `>50K`).
- `data/train.csv`: Titanic; objetivo `Survived` (1 = supervivencia).
- `figuras/`: graficas generadas por el notebook.
- `resultados/`: tablas CSV de perfiles, limites, estadisticas, imputacion, balanceo y comparaciones de robustez.

Abre y ejecuta el notebook de la raiz del proyecto. Hay una copia de notebook dentro de `figuras/`, pero no es la entrada recomendada: sus rutas relativas pueden no resolver los datos correctamente.

## Requisitos

- Windows 10/11.
- Python 3.11 o posterior. Se recomienda Python 3.11 para una instalacion compatible y reproducible de las bibliotecas cientificas.
- Git para clonar el repositorio.
- Para ejecutar desde VS Code: extensiones **Python** y **Jupyter** de Microsoft.

El notebook importa NumPy, pandas, Matplotlib, Seaborn, SciPy y scikit-learn. Tambien necesita Jupyter e ipykernel para ejecutarse como notebook. El balanceo SMOTE esta implementado en el notebook con NumPy/scikit-learn; `imbalanced-learn` no es un requisito declarado por el codigo.

## Inicializacion en Windows

Clona el repositorio privado (necesitas acceso a GitHub):

```powershell
git clone https://github.com/EmilianoRoPe/Practica2-IA.git
Set-Location Practica2-IA
```

Crea un entorno virtual e instala las dependencias:

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install numpy pandas matplotlib seaborn scipy scikit-learn jupyter ipykernel
```

El entorno `.venv/` es local y esta excluido de Git. Si Python 3.11 no esta instalado, instala una version compatible de Python y ajusta `-3.11` a la version disponible.

## Ejecutar en VS Code

1. Abre la carpeta `Practica2-IA` completa en VS Code, no solo el archivo del notebook.
2. Abre `Practica2_EDA.ipynb` desde la raiz.
3. En el selector de kernel, elige el interprete del proyecto: `.venv\Scripts\python.exe`.
4. Ejecuta **Run All** y espera a que terminen todas las celdas.

El notebook resuelve los datos desde `data/` y guarda las salidas con rutas relativas al directorio de trabajo. Por eso es importante abrir la raiz del repositorio como workspace. No ejecutes la copia que esta dentro de `figuras/`.

## Ejecutar desde PowerShell

Desde la raiz del repositorio:

```powershell
.\.venv\Scripts\python.exe -m jupyter notebook Practica2_EDA.ipynb
```

Se abrira Jupyter en el navegador. Selecciona el kernel `.venv` y ejecuta todas las celdas en orden.

## Salidas generadas

Las funciones del notebook crean las carpetas `figuras/` y `resultados/` si no existen. Al ejecutar las celdas se generan o actualizan imagenes PNG y archivos CSV con perfiles, estadisticas de imputacion y winsorizacion, metricas de balanceo y resultados de robustez. Una nueva ejecucion puede modificar esos archivos versionados; revisa `git status` antes de hacer commit.

El notebook contiene salidas guardadas, pero su estado de ejecucion actual aparece como no ejecutado. Para validar los resultados contra el codigo actual, ejecuta **Run All** en un kernel limpio.

## Consideraciones metodologicas

- El notebook define una particion estratificada 75/25 y la semilla `42`; los transformadores y el remuestreo se calculan sobre entrenamiento para reducir fuga de informacion.
- Se comparan estrategias de imputacion, dos criterios de winsorizacion y alternativas de balanceo, junto con regresion logistica y metricas mas alla de accuracy.
- La implementacion propia de SMOTE interpola las columnas de entrada. Si incluye columnas one-hot, puede producir valores categoricos fraccionarios; el notebook identifica esta limitacion. Interpreta esos resultados con cautela y considera SMOTENC para un tratamiento futuro de datos mixtos.
- El notebook indica que la licencia de Titanic aun debe verificarse en la fuente de Kaggle antes de la entrega academica.
- Este repositorio no incluye un archivo de dependencias con versiones fijadas; los comandos anteriores instalan las versiones disponibles al momento de la instalacion.
