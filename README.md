# 📡 TelecomX — Análisis de Evasión de Clientes (Churn)

<div align="center">



**Oracle Next Education (ONE) · Alura Latam — Challenge 2 · Data Science**

*Autora: Daniela Andrea Puebla Mosca*

![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge&logo=python&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-4C9BE8?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
</div>

---

## 📋 Descripción

**Telecom X** enfrenta una tasa crítica de evasión de clientes (*churn*) del **≈ 26.5%**, lo que significa que 1 de cada 4 clientes, cancela el servicio mensualmente, impactando directamente los ingresos recurrentes de la empresa.

Este proyecto aplica un proceso completo de **ETL (Extracción → Transformación → Carga)** seguido de un **Análisis Exploratorio de Datos (EDA)** para identificar los factores que más influyen en la decisión de cancelar, y proponer recomendaciones estratégicas concretas para reducir el churn.

---

## 🗂️ Estructura del Proyecto

```
TelecomX-Churn-Analysis/
│
├── TelecomX_LATAM_definitivo.ipynb   # Notebook principal (ETL + EDA + Informe)
├── telecomx_limpio.csv               # Dataset procesado (generado al ejecutar)
└── README.md                         # Este archivo
```

---

## ⚙️ Arquitectura ETL

El proyecto sigue una arquitectura de tres fases:

```
┌─────────────────────────────────────────────────────────────┐
│  ⚙️  FASE 1 — EXTRACCIÓN          Carga desde API JSON      │
│  🔧  FASE 2 — TRANSFORMACIÓN      Limpieza + Estandarización│
│  📊  FASE 3 — CARGA Y ANÁLISIS    EDA + Visualizaciones     │
└─────────────────────────────────────────────────────────────┘
```

### Fase 1 — Extracción
- Carga de datos desde archivo JSON alojado en GitHub
- Lectura directa con `pd.read_json(url)`
- Normalización de JSON anidado con `pd.json_normalize()`
- Dataset crudo: **7,043 clientes · 21 variables**

### Fase 2 — Transformación

| Paso | Descripción |
|------|-------------|
| Paso 2 | Exploración inicial: tipos de datos y diccionario de variables |
| Paso 3 | Detección de nulos, duplicados e inconsistencias de formato |
| Paso 4 | Corrección: conversión numérica, imputación y limpieza de strings |
| Paso 5 | Feature engineering: `Cuentas_Diarias = Cargos_Mensuales / 30` |
| Paso 6 | Estandarización: renombrado al español, traducción de valores, codificación binaria |

### Fase 3 — Carga y Análisis

| Paso | Descripción |
|------|-------------|
| Paso 7 | Estadísticas descriptivas generales |
| Paso 8 | Distribución de la variable objetivo `Evasion` |
| Paso 9 | Evasión por variables categóricas (género, contrato, pago, internet) |
| Paso 10 | Evasión por variables numéricas: boxplots comparativos |
| Extra | Matriz de correlación + scatter Meses de Contrato vs Cuenta Diaria |

---

## 📊 Principales Hallazgos

### Tasa de Evasión General
```
Clientes activos        →  5,174  (73.5%)
Clientes que evadieron  →  1,869  (26.5%)
```
## 📈 Impacto Potencial

Si se reduce en 10 puntos porcentuales la evasión del segmento mensual (42.7%), el impacto en ingresos recurrentes podría ser significativo, especialmente considerando que este grupo concentra la mayor tasa de abandono.

El análisis permite priorizar intervenciones en los segmentos de mayor riesgo antes de invertir en adquisición de nuevos clientes.

### Factores más influyentes

| Factor | Relación con Evasión | Dato clave |
|--------|---------------------|------------|
| 🔴 **Tipo de contrato** | Alta | Mensual: ~42.7% evasión vs bianual: ~2.8% |
| 🟠 **Tiempo de permanencia** | Alta (negativa) | Evadidos: 18 meses promedio vs 37.6 de activos |
| 🟠 **Método de pago** | Alta | Cheque electrónico: ~45.3% de evasión |
| 🟡 **Tipo de internet** | Moderada | Fibra óptica: ~41.9% vs DSL: ~19% |
| 🟡 **Cargos mensuales** | Moderada | Evadidos pagan $74.4 vs $61.3 USD/mes |
| ⚪ **Género** | Nula | Sin diferencia significativa entre grupos |

### Perfil del cliente con mayor riesgo
> Nuevo cliente (< 12 meses) · Contrato mensual · Fibra óptica · Pago con cheque electrónico · Cargos > $70 USD/mes

---

## 🚀 Recomendaciones Estratégicas

1. **🎯 Migración contractual** — Incentivar el paso de contratos mensuales a anuales o bianuales mediante descuentos, upgrades o meses gratis
2. **🔔 Onboarding reforzado** — Programa de acompañamiento activo durante los primeros 6 meses de contrato
3. **💳 Pago automático** — Ofrecer descuento (~5%) a clientes que migren de cheque electrónico a débito o tarjeta
4. **💰 Revisión de precios** — Auditar la propuesta de valor en fibra óptica: alta tarifa + alta evasión indica brecha de expectativa-realidad
5. **🤖 Modelo predictivo** — Construir un clasificador de churn (Random Forest / XGBoost) con las variables identificadas

---

## 🛠️ Tecnologías Utilizadas

| Librería | Versión recomendada | Uso |
|----------|-------------------|-----|
| `pandas` | ≥ 1.5 | Manipulación y análisis de datos |
| `requests` | ≥ 2.28 | Extracción de datos desde la API |
| `matplotlib` | ≥ 3.6 | Visualizaciones base |
| `seaborn` | ≥ 0.12 | Gráficos estadísticos |

---

## ▶️ Cómo Ejecutar

### Opción 1 — Google Colab *(recomendado)*

1. Abre [Google Colab](https://colab.research.google.com/)
2. Sube el archivo `TelecomX_LATAM_definitivo.ipynb`
3. Ejecuta todas las celdas: `Runtime → Run all` o `Ctrl + F9`
4. Al finalizar, el CSV limpio se descargará automáticamente

### Opción 2 — Local con Jupyter

```bash
# 1. Clonar el repositorio
git clone https://github.com/tu-usuario/telecomx-churn-analysis.git
cd telecomx-churn-analysis

# 2. Instalar dependencias
pip install pandas requests matplotlib seaborn jupyter

# 3. Abrir el notebook
jupyter notebook TelecomX_LATAM.ipynb
```

> ⚠️ **Requisito:** conexión a internet activa para la extracción de datos en el Paso 1.

---

## 🔗 Fuente de Datos

```
https://raw.githubusercontent.com/alura-cursos/challenge2-data-science-LATAM/refs/heads/main/TelecomX_Data.json
```

Dataset público proporcionado por **Alura Latam** para el Challenge 2 de Data Science.
Contiene datos históricos de **7,043 clientes** con 21 variables sobre demografía, servicios contratados, facturación y estado de evasión.

---

## ⚠️ Solución de Problemas

| Problema | Causa probable | Solución |
|----------|---------------|----------|
| `ConnectionError` en Paso 1 | Sin conexión a internet | Verificar red e intentar de nuevo |
| `ModuleNotFoundError` | Librería no instalada | `pip install pandas requests matplotlib seaborn` |
| Gráficos sin color o error en boxplots | Celdas ejecutadas fuera de orden | `Runtime → Restart and run all` |
| `KeyError: 'Sí'` en crosstab | Celda de estandarización no ejecutada | Ejecutar celdas en secuencia desde el inicio |
| CSV no se guarda en local | Problema de permisos de escritura | Cambiar la ruta de salida en la última celda |

---

## 📄 Licencia

Proyecto desarrollado con fines educativos como parte del programa
**Oracle Next Education (ONE) + Alura Latam — Challenge 2 · Data Science**.

---

<div align="center">
  <sub>Desarrollado con 💜 por <strong>Daniela Andrea Puebla Mosca</strong></sub><br>
  <sub>Python · pandas · matplotlib · seaborn · Jupyter</sub>
</div>

