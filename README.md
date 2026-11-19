# Análisis de uso de clientes – ConnectaTel

Análisis exploratorio del comportamiento de uso (llamadas y mensajes) de los clientes de **ConnectaTel**, empresa de telecomunicaciones con operación en México y Colombia. Datos registrados hasta 2024.

## Objetivo

Identificar patrones de uso, detectar comportamientos atípicos y segmentar a los clientes por edad y nivel de consumo, para proponer mejoras en la oferta de planes y estrategias de retención.

**Preguntas de negocio**
- ¿Qué segmentos usan más o menos llamadas y mensajes?
- ¿Qué usuarios tienen valores atípicos (posible fraude o error de registro)?
- ¿Cómo varía el uso según la edad y el plan contratado?
- ¿Qué patrones ayudan a diseñar mejores planes?

## Datasets

| Archivo | Contenido |
|---|---|
| `plans.csv` | Catálogo de planes: precio, minutos y GB incluidos, costo por extra |
| `users_latam.csv` | Clientes: edad, ciudad, fecha de registro, plan, churn |
| `usage.csv` | Eventos de uso: tipo (`call` / `text`), fecha, duración y longitud |

## Etapas del análisis

1. **Carga y exploración** – estructura, tipos de dato y tamaño de cada dataset.
2. **Calidad de datos** – nulos, sentinels (`age = -999`, `city = "?"`) y fechas fuera de rango.
3. **Limpieza** – imputación de edad con la mediana, sentinels a nulo, fechas futuras a `NaT`; los nulos de `duration`/`length` se dejan por ser MAR (dependen de `type`).
4. **Estadísticas por usuario** – agregación de mensajes, llamadas y minutos por `user_id` y unión con `users`.
5. **Distribuciones y outliers** – histogramas por plan, boxplots y límites con método IQR.
6. **Segmentación** – grupos de uso (Bajo / Medio / Alto) y de edad (Joven / Adulto / Adulto Mayor).
7. **Insight ejecutivo** – conclusiones y recomendaciones comerciales.

## Estructura del repositorio

```
.
├── ConnectaTel_Analisis.ipynb
├── README.md
└── datasets/            # (opcional) plans.csv, users_latam.csv, usage.csv
```

## Cómo ejecutarlo

**Google Colab**
1. Abre el notebook desde GitHub en Colab (`File → Open notebook → GitHub`).
2. Sube los tres CSV a la sesión y ajusta las rutas de la celda de carga si no están en `/datasets/`.
3. Ejecuta `Runtime → Run all`.

**Local**
```bash
git clone https://github.com/VictoriaLasso/DataAnalitic.git
cd connectatel-analysis
pip install pandas numpy seaborn matplotlib jupyter
jupyter notebook ConnectaTel_Analisis.ipynb
```
Coloca los CSV en `datasets/` y cambia las rutas de `'/datasets/...'` a `'datasets/...'`.

## Herramientas

Python 3 · pandas · numpy · seaborn · matplotlib · Jupyter Notebook
