# Análisis de Facturación y Cobranza — Balance 2024 de una PyME

Análisis exploratorio de datos sobre el balance anual de una pequeña empresa, hecho con Python y Pandas. El objetivo fue responder preguntas concretas de negocio a partir de un Excel de facturación: si el negocio creció, quiénes son los clientes que lo sostienen, y qué tan sana está la cobranza.

Este proyecto forma parte de la serie **"Data Science desde 0"**, donde documento públicamente mi proceso de aprendizaje en análisis de datos.

> ⚠️ Los datos fueron anonimizados (nombres de clientes reemplazados por nombres ficticios). El dataset se usa exclusivamente con fines educativos y de práctica.

---

## El caso

Un amigo, dueño de una PyME, tenía el balance completo del 2024 cargado en Excel pero ningún tiempo para analizarlo. La consulta inicial fue simple: *"¿Podés decirme si el negocio creció o se estancó ese año?"*.

A partir de ahí surgieron otras preguntas que fui respondiendo una por una.

---

## Preguntas de negocio y hallazgos

### 1. ¿El negocio creció o se estancó durante el año?
Agrupé la facturación por mes y calculé la variación porcentual mes a mes.

**Hallazgo:** el año tuvo una tendencia general de crecimiento, con fuertes oscilaciones. El mes de mayor caída registró un **-20.31%** y el de mayor suba un **+90.59%** respecto al mes anterior.

### 2. ¿Quiénes son los clientes que sostienen el negocio?
Agrupé la facturación por cliente y ordené de mayor a menor para obtener el Top 5.

**Hallazgo:** los 5 principales clientes concentran más del **40% de la facturación anual**, y uno solo de ellos se lleva una porción considerablemente mayor que el resto. Es un caso claro de riesgo de concentración de cartera: la pérdida de un único cliente tendría un impacto desproporcionado en los ingresos.

### 3. ¿Los clientes pagan en fecha?
Calculé la diferencia en días entre la fecha de vencimiento y la fecha real de pago, separando las facturas cobradas de las que siguen pendientes.

**Hallazgo:** dos realidades opuestas. Las facturas ya cobradas se pagaron en promedio **medio día antes** del vencimiento. Pero las facturas pendientes llevan en promedio **más de 700 días vencidas** — no es que los clientes paguen tarde, sino que existe una porción de deuda histórica probablemente incobrable. Analizar ambos grupos por separado fue clave: un promedio general habría escondido el problema.

### 4. ¿Cómo paga cada tipo de cliente?
Crucé la forma de pago (efectivo, transferencia, cheque) contra el tipo de cliente (chico o grande).

**Hallazgo:** a nivel general predomina la transferencia, seguida del efectivo. Pero al separar por segmento, los clientes chicos casi no usan cheque, mientras que en los clientes grandes el cheque tiene un peso mucho mayor. Esto impacta directamente en el flujo de caja: los clientes que más facturan son también los que más pagan con instrumentos diferidos.

### 5. ¿Todos los clientes grandes compran igual a lo largo del año?
Crucé la evolución mensual con cada uno de los 5 clientes principales.

**Hallazgo:** el Top 5 no es un grupo homogéneo. Un cliente concentra casi toda su facturación en un único mes del año, otro muestra un pico inicial y luego se estabiliza, otro crece de forma sostenida en el segundo semestre, y dos se mantienen estables durante todo el año. Cada uno tiene una lógica de compra distinta, lo que cambia por completo cómo se planifica la caja.

---

## Stack utilizado

- **Python**
- **Pandas** — carga, limpieza y manipulación del dataset
- **NumPy** — operaciones numéricas
- **Matplotlib** y **Seaborn** — visualizaciones
- **Jupyter Notebook** — entorno de trabajo

---

## Estructura del repositorio

```
├── ANALISIS_DE_BALANCE1.ipynb    # Notebook con el análisis completo
├── data/                          # Dataset anonimizado
├── graficos/                      # Visualizaciones exportadas
└── README.md
```

---

## Proceso de limpieza

Antes de analizar, el dataset requirió varios pasos de preparación:

- Conversión de columnas de fecha al tipo `datetime`
- Normalización de nombres de clientes (espacios sobrantes y diferencias de mayúsculas/minúsculas que generaban duplicados)
- Identificación de facturas sin fecha de pago para separar la deuda pendiente
- Anonimización de los nombres reales de clientes

---

## Sobre esta serie

Comparto el proceso completo de estos análisis en LinkedIn, dentro de la serie **"Data Science desde 0"** — incluyendo los errores, las dudas y lo que voy aprendiendo en el camino.

Si te interesa seguirla o tenés feedback sobre el análisis, te leo.
