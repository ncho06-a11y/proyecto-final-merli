# Banco Río: perfiles de cartera y riesgo de crédito

Proyecto final de **Programación Analítica II** (Universidad de Montevideo, S2 2026,
docente Camila Palomeque). Propuesta A.

Autor: Ignacio Merli.

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
    ├── mora_por_trimestre.png              3.3 la cartera empeora desde 2025T3
    ├── mora_por_ratio_cuota_ingreso.png    4.1 ratio cuota / ingreso contra atraso
    └── efecto_composicion_canal.html       4.2 efecto de composición (Plotly, interactivo)
```

El notebook está ordenado según las cinco etapas de la consigna: 1. EDA y calidad de
datos, 2. creación de variables, 3. análisis de negocio, 4. visualización y
5. conclusiones. Todas las funciones del análisis están dentro del notebook (no se usa
la carpeta opcional `src/`), así cada número se puede rastrear hasta su celda.

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

Los gráficos se guardan en `salidas/`. El notebook corre completo en menos de un
minuto y no necesita conexión a internet. El gráfico interactivo
(`efecto_composicion_canal.html`) se abre con doble clic en cualquier navegador.

Si el notebook no encuentra los datos, verificar que se abrió desde la carpeta
`notebooks/`: las rutas son relativas a esa carpeta (`../datos/`).

## Qué se concluyó

1. **La cartera empeora, no mejora.** El tablero de Sistemas mide la mora "alguna vez"
   por trimestre de otorgamiento, que baja sola porque los créditos nuevos tuvieron
   menos tiempo para atrasarse (censura). Medida a 6 meses del otorgamiento, la mora
   estuvo entre 13% y 21% hasta 2025T2 y subió a 22,7% en 2025T3 y 28,4% en 2025T4.
2. **La causa es un cambio en lo que se aprueba.** Desde julio de 2025 el score de
   originación mediano cayó de alrededor de 665 a 590 y la mitad de los créditos se dio
   con score menor a 600 (antes, uno de cada cinco). Eso explica el 74% del aumento de
   la mora. El canal y el tipo de producto no cambiaron.
3. **Qué anticipa el atraso:** el score al aprobar, el sector de empleo (informales
   37,6% de mora contra 11,6% en públicos) y una cuota de más del 35% del ingreso.
4. **Problema operativo:** Comercio adherido se atrasa 7 puntos más de lo que explica
   el perfil de sus clientes. Maldonado, en cambio, tiene más mora por composición
   (más informales), no por algo propio.
5. **Recomendación:** no prestar con score menor a 550, no prestar sin ingreso
   comprobado con score menor a 650 y limitar la cuota al 35% del ingreso en créditos
   sin garantía con score menor a 700. Aplicada desde el principio, la mora habría
   bajado de 18,7% a 13,8%, resignando el 18,6% del monto prestado.
