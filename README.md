# Banco Río: perfiles de cartera y riesgo de crédito

Proyecto final de **Programación Analítica II** (Universidad de Montevideo, S2 2026,
docente Camila Palomeque). Propuesta A.

Autor: NOMBRE Merli.

## Qué hace el proyecto

La Gerencia de Riesgos del Banco Río quiere saber:

1. Qué perfiles de cliente tiene la cartera de crédito al consumo.
2. Cuáles se atrasan y por qué.
3. Si la cartera está mejorando o empeorando, porque el tablero de Sistemas dice
   que mejora hace dos años y al Directorio eso ya no le cierra.

El notebook audita y limpia los tres archivos que entregó el banco, construye las
variables que faltan (definición de mora, montos en pesos y ratio cuota / ingreso),
responde las tres preguntas y termina con una recomendación de política de crédito.

## Estructura

```
proyecto-final-merli/
├── README.md            este archivo
├── requirements.txt     librerías necesarias, con versión
├── .gitignore           lo que no se sube al repositorio
├── datos/               los tres archivos del banco (corte al 30/06/2026)
│   ├── clientes.csv
│   ├── productos.csv
│   ├── tipo_cambio_mensual.csv
│   └── Info.txt         descripción original de los archivos
├── notebooks/
│   └── analisis_riesgo_credito.ipynb   todo el análisis
└── salidas/             gráficos que genera el notebook
```

## Datos

Los archivos de `datos/` son los que entregó la docente en el Moodle (carpeta
`A_riesgo_de_credito`). Son datos sintéticos de uso docente, por eso se incluyen en el
repositorio: el notebook los lee directamente de esa carpeta y no hay que descargar
nada aparte.

## Cómo crear el entorno

Requiere Python 3.11 o superior. Desde una terminal abierta en la carpeta del proyecto:

```bash
python -m venv .venv
```

Activar el entorno:

```bash
# Windows
.venv\Scripts\activate

# macOS / Linux
source .venv/bin/activate
```

Instalar las librerías:

```bash
pip install -r requirements.txt
```

## Cómo correrlo y en qué orden

Hay un solo notebook y se corre completo, de arriba hacia abajo:

1. Abrir `notebooks/analisis_riesgo_credito.ipynb` en VS Code o Jupyter.
2. Elegir como kernel el entorno `.venv` creado en el paso anterior.
3. Ejecutar todas las celdas en orden (*Run All*).

Los gráficos se guardan en `salidas/`.
