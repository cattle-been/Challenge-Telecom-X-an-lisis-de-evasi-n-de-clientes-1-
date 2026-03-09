# 📡 TelecomX LATAM — Análisis de Evasión de Clientes (Churn)

> Proyecto de análisis exploratorio de datos para identificar los factores que impulsan la evasión de clientes en TelecomX, empresa de telecomunicaciones en América Latina.

---

## 📋 Descripción del Proyecto

TelecomX enfrenta un alto índice de **churn** (evasión de clientes): aproximadamente 1 de cada 4 suscriptores cancela su contrato. Este proyecto realiza un proceso completo de **ETL + EDA** sobre los datos de clientes para:

- Limpiar y transformar los datos brutos en un formato utilizable.
- Identificar los perfiles y comportamientos asociados al churn.
- Generar insights accionables para el equipo de negocio.
- Entregar un dataset limpio al equipo de Ciencia de Datos para modelado predictivo.

---

## 📁 Estructura del Proyecto

```
TelecomX_LATAM/
│
├── TelecomX_LATAM.ipynb       # Notebook principal (ETL + EDA + Informe)
├── TelecomX_Data.json         # Dataset original (JSON anidado, 7.267 registros)
├── TelecomX_diccionario.md    # Diccionario de variables
├── TelecomX_clean.csv         # Dataset limpio exportado (generado al ejecutar)
└── README.md                  # Este archivo
```

---

## 🗂️ Diccionario de Datos

| Variable | Descripción |
|----------|-------------|
| `customerID` | Identificador único del cliente |
| `Churn` | Si el cliente dejó (Yes) o no (No) la empresa |
| `gender` | Género del cliente |
| `SeniorCitizen` | 1 si el cliente tiene ≥ 65 años, 0 si no |
| `Partner` | Si el cliente tiene pareja |
| `Dependents` | Si el cliente tiene dependientes |
| `tenure` | Meses de contrato activo |
| `PhoneService` | Suscripción al servicio telefónico |
| `MultipleLines` | Suscripción a más de una línea telefónica |
| `InternetService` | Tipo de servicio de internet (DSL / Fiber optic / No) |
| `OnlineSecurity` | Servicio adicional de seguridad en línea |
| `OnlineBackup` | Servicio adicional de respaldo en línea |
| `DeviceProtection` | Servicio adicional de protección de dispositivo |
| `TechSupport` | Soporte técnico con menor tiempo de espera |
| `StreamingTV` | Suscripción de televisión por cable |
| `StreamingMovies` | Suscripción de streaming de películas |
| `Contract` | Tipo de contrato (Month-to-month / One year / Two year) |
| `PaperlessBilling` | Si el cliente recibe factura en línea |
| `PaymentMethod` | Método de pago |
| `Charges.Monthly` | Cargo mensual total (USD) |
| `Charges.Total` | Cargo total acumulado del cliente (USD) |

---

## ⚙️ Requisitos

```bash
Python >= 3.8

# Librerías necesarias
pandas
numpy
matplotlib
seaborn
```

Instalación rápida:

```bash
pip install pandas numpy matplotlib seaborn
```

---

## 🚀 Cómo Ejecutar

### En Google Colab (recomendado)

1. Abre [Google Colab](https://colab.research.google.com/).
2. Sube el archivo `TelecomX_LATAM.ipynb`.
3. En la primera celda de código, sube el archivo de datos:

```python
from google.colab import files
files.upload()  # Selecciona TelecomX_Data.json
```

4. Ejecuta todas las celdas en orden (`Runtime > Run all`).

### En local (Jupyter Notebook)

```bash
# Clona o descarga el repositorio
cd TelecomX_LATAM/

# Lanza Jupyter
jupyter notebook TelecomX_LATAM.ipynb
```

Asegúrate de que `TelecomX_Data.json` esté en el mismo directorio que el notebook.

---

## 🔧 Pipeline del Notebook

```
📌 EXTRACCIÓN
  └── Carga del JSON con json.load()
  └── Normalización de estructura anidada → DataFrame plano

🔧 TRANSFORMACIÓN
  └── Detección y tratamiento de cadenas vacías → NaN
  └── Conversión de tipos (Charges.Total, tenure, SeniorCitizen)
  └── Eliminación de filas sin clasificación de Churn
  └── Imputación de nulos con mediana por grupo
  └── Eliminación de duplicados por customerID
  └── Estandarización Yes/No → 1/0
  └── Creación de variables derivadas (num_addons, tenure_segment)

📊 ANÁLISIS EXPLORATORIO (10 gráficos)
  └── Distribución general de Churn
  └── Churn por género y adulto mayor
  └── Churn por tipo de contrato
  └── Churn por método de pago
  └── Distribución de antigüedad y segmentos
  └── Cargos mensuales: boxplot + KDE
  └── Churn por tipo de Internet
  └── Churn según servicios adicionales
  └── Mapa de calor de correlaciones
  └── Ranking de correlaciones con Churn

📄 INFORME FINAL
  └── Métricas clave
  └── Conclusiones e insights
  └── Recomendaciones estratégicas
  └── Exportación de TelecomX_clean.csv
```

---

## 📊 Principales Hallazgos

| Hallazgo | Detalle |
|----------|---------|
| 🔴 Tasa de Churn global | ~26% — 1 de cada 4 clientes se va |
| 🔴 Contratos mes a mes | Tasa de churn ~43%, la más alta |
| 🔴 Clientes nuevos (0-12 meses) | Tasa de churn >40% — período más crítico |
| 🟠 Fibra Óptica | Churn ~42%, mayor que DSL pese a ser premium |
| 🟠 Cheque electrónico | Método de pago con mayor tasa de evasión |
| 🟡 Adultos mayores | Churn ~41%, por encima del promedio |
| 🟢 Más servicios adicionales | A mayor número de addons, menor churn |
| 🟢 Contratos largos | Clientes con 2 años: churn < 5% |

---

## 💡 Recomendaciones Estratégicas

| Prioridad | Acción | Segmento |
|:---------:|--------|----------|
| 🔴 Alta | Incentivar contratos anuales/bianuales con descuentos | Clientes mes a mes |
| 🔴 Alta | Programa de onboarding en los primeros 12 meses | Clientes nuevos |
| 🟠 Media | Revisar pricing y calidad de Fibra Óptica | Usuarios de fibra |
| 🟠 Media | Migrar clientes a pagos automáticos con incentivos | Usuarios de cheque electrónico |
| 🟡 Media | Cross-selling de servicios adicionales | Clientes con 0-1 addons |
| 🟡 Media | Planes y soporte especial para adultos mayores | Senior Citizens |
| 🟢 Baja | Modelo predictivo de churn con dataset limpio | Todos los clientes |

---

## 🤖 Para el Equipo de Ciencia de Datos

El archivo `TelecomX_clean.csv` generado está listo para modelado predictivo:

- **Variable objetivo:** `Churn_num` (1 = evadió, 0 = permaneció)
- **Desbalance de clases:** ~74% No / 26% Yes → se recomienda usar **SMOTE** u oversampling
- **Modelos sugeridos:** Logistic Regression, Random Forest, XGBoost, LightGBM
- **Variables derivadas incluidas:** `num_addons`, `tenure_segment`
- **Variables binarias:** ya codificadas como `0/1`

---

*Este proyecto forma parte del programa de reducción de churn de TelecomX. Los datos son de uso interno.*
