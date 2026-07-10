# Online Retail Analytics

Análisis exploratorio y segmentación de clientes sobre un dataset de transacciones de una tienda de retail online del Reino Unido (2009–2011).

---

## Objetivo

Responder preguntas clave de negocio a partir de datos transaccionales:

- ¿Cómo evolucionó el revenue a lo largo del tiempo?
- ¿Qué productos y mercados generan más valor?
- ¿Cómo se pueden segmentar los clientes según su comportamiento de compra?

---

## Dataset

**Fuente:** [Online Retail II — UCI Machine Learning Repository](https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci) via Kaggle

**Descripción:** Dataset de transacciones reales de una tienda de retail online del Reino Unido entre diciembre de 2009 y diciembre de 2011. Incluye ventas a clientes minoristas y mayoristas, principalmente en Europa.

| Columna | Descripción |
|---|---|
| Invoice | Número de factura (prefijo 'C' indica cancelación) |
| StockCode | Código de producto |
| Description | Nombre del producto |
| Quantity | Cantidad por transacción (negativo = devolución) |
| InvoiceDate | Fecha y hora de la transacción |
| Price | Precio unitario en libras esterlinas (£) |
| Customer ID | Identificador único del cliente |
| Country | País del cliente |

---

## Tecnologías utilizadas

- Python 3
- pandas
- numpy
- matplotlib
- seaborn
- Google Colab

---

## Estructura del proyecto

El análisis está organizado en un único notebook con las siguientes etapas:

**1. Carga y exploración inicial**
Carga del dataset, inspección de estructura, tipos de datos, nulos y estadísticas descriptivas.

**2. Limpieza de datos**
- Eliminación de cancelaciones (Invoice con prefijo 'C') y ajustes contables (prefijo 'A')
- Eliminación de filas con Quantity o Price negativos o iguales a cero
- Conversión de InvoiceDate a formato datetime
- Creación de la columna Revenue (Quantity × Price)
- Los nulos de Customer ID se conservan para el análisis general y se filtran únicamente para la segmentación RFM

**3. Análisis de métricas de negocio**
- Revenue total y evolución mensual
- Top 10 productos por revenue
- Top 10 países por revenue (excluyendo Reino Unido)

**4. Visualizaciones**
- Línea de tendencia de revenue mensual (2009–2011)
- Gráfico de barras: top 10 productos por revenue
- Gráfico de barras: top 10 países por revenue

**5. Segmentación RFM**
Segmentación de 5.862 clientes identificados en cinco grupos según comportamiento de compra: VIP, Leal, Nuevo o prometedor, En riesgo y Perdido.

---

## Principales hallazgos

- **Revenue total:** £20,9 millones en dos años de operación
- **Estacionalidad marcada:** octubre, noviembre y diciembre concentran los picos de revenue en ambos años, con noviembre 2011 como mes récord (£1,5M). Esto sugiere una fuerte dependencia de la temporada navideña
- **Producto estrella:** REGENCY CAKESTAND 3 TIER generó £344.563 en el período, casi el doble que el segundo producto
- **Mercado concentrado:** Reino Unido domina las ventas. Entre los mercados internacionales, Irlanda (EIRE) y Netherlands lideran con £640k y £550k respectivamente
- **Segmentación de clientes:**

| Segmento | Clientes | % |
|---|---|---|
| Perdido | 2.043 | 35% |
| Leal | 1.381 | 24% |
| En riesgo | 888 | 15% |
| Nuevo o prometedor | 888 | 15% |
| VIP | 662 | 11% |

El segmento "En riesgo" representa una oportunidad de retención inmediata: son clientes con alta frecuencia histórica que dejaron de comprar recientemente.

---

## Cómo reproducir el análisis

1. Clonar el repositorio
2. Descargar el dataset desde [Kaggle](https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci) y colocarlo en la carpeta raíz
3. Abrir el notebook en Google Colab o Jupyter
4. Ejecutar las celdas en orden

---

## Decisiones analíticas

- **Exclusión de UK en el análisis por país:** Reino Unido concentra más del 90% de las transacciones. Se excluye para permitir visualizar la distribución entre mercados internacionales.
- **Criterios de segmentación RFM:** los segmentos se definen a partir de los puntajes R (Recency) y F (Frequency) como dimensiones principales. M (Monetary) se incorpora únicamente para la clasificación VIP, donde el valor económico es un criterio diferenciador clave.
- **Customer ID nulos:** representan el 23% del dataset (compras anónimas). Se conservan para el análisis de revenue y productos, y se excluyen únicamente para la segmentación RFM donde la identificación del cliente es necesaria.