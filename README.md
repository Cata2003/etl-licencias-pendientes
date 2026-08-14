# ETL de Licencias Pendientes con Python y PostgreSQL

Proyecto de procesamiento y transformación de datos enfocado en la gestión de registros de licencias médicas. Se desarrolló un proceso **ETL (Extract, Transform, Load)** utilizando Python para limpiar, transformar y generar nuevas variables relacionadas con los plazos de pronunciamiento, finalizando con la exportación de resultados y carga de los datos en PostgreSQL.

## Objetivo

Automatizar el procesamiento de una base de datos de licencias pendientes para:

* Mejorar la calidad y consistencia de los datos.
* Reducir tareas manuales de procesamiento.
* Calcular automáticamente fechas y plazos de pronunciamiento.
* Identificar casos gestionados dentro o fuera de plazo.
* Generar indicadores y tablas resumen.
* Preparar los datos para su almacenamiento y posterior análisis.

## Tecnologías utilizadas

* **Python**
* **Pandas**
* **NumPy**
* **Jupyter Notebook**
* **PostgreSQL**
* **Excel**
* **SQL**

## Flujo ETL

### 1. Extracción

Los datos son cargados desde un archivo Excel utilizando Python y Pandas.

El proceso incluye la validación de la existencia del archivo y la lectura de la hoja que contiene la base principal.

### 2. Exploración y limpieza

Se realiza una revisión inicial de la estructura del dataset, considerando:

* Dimensiones de la base.
* Tipos de datos.
* Valores nulos.
* Registros duplicados.
* Formatos de fechas.
* Nombres y consistencia de las columnas.

Posteriormente se eliminan registros duplicados y se realizan transformaciones necesarias para preparar los datos.

## Transformaciones principales

### Rango de días

Se genera una variable que clasifica la duración de las licencias en tres categorías:

* Menor o igual a 3 días.
* Entre 4 y 11 días.
* Mayor a 11 días.

### Fecha máxima de pronunciamiento

Se calcula automáticamente la fecha límite para resolver cada registro utilizando días hábiles.

El plazo depende del usuario responsable de la creación del registro:

* **4 días hábiles** cuando el usuario corresponde a `LICMED`.
* **2 días hábiles** en los demás casos.

El cálculo excluye fines de semana y feriados considerados en el proceso.

### Cumplimiento de plazo

Se compara la fecha de resolución con la fecha máxima de pronunciamiento para determinar si cada registro fue procesado dentro del plazo establecido.

### Estado de visación

Se genera una variable que permite identificar si el registro cuenta con un médico contralor asociado y, por lo tanto, si fue visado.

### Fuera de plazo

Se identifica automáticamente si un caso pendiente supera la fecha máxima establecida para su pronunciamiento.

## Generación de indicadores

A partir de los datos transformados se generan tablas resumen orientadas al análisis de la información, incluyendo:

* Distribución por cumplimiento de plazo.
* Estado de visación.
* Casos fuera de plazo.
* Distribución por rango de días.
* Distribución según días disponibles para pronunciamiento.

Estos resultados son exportados a un archivo Excel con diferentes hojas para facilitar su revisión.

## Carga en PostgreSQL

Una vez finalizada la limpieza y transformación, los datos son cargados en una base de datos PostgreSQL.

Las credenciales de conexión no se almacenan directamente en el notebook y pueden configurarse mediante variables de entorno.

Esto evita exponer credenciales sensibles dentro del repositorio.

## Estructura del repositorio

```text
etl-licencias-pendientes/
│
├── README.md
├── ETL_Licencias_Pendientes.ipynb
└── tablas_resumen_licencias.xlsx
```

## Privacidad y disponibilidad de los datos

El dataset original utilizado para el desarrollo de este proyecto fue proporcionado con fines académicos.

Debido a consideraciones de **privacidad y derechos de redistribución**, el archivo original no se encuentra incluido en este repositorio.

El repositorio contiene el código desarrollado, la metodología utilizada y resultados agregados que permiten demostrar el funcionamiento del proceso ETL sin publicar la base original.

## Resultados

El proceso desarrollado permite automatizar tareas de limpieza y transformación que originalmente podrían requerir procesamiento manual.

Como resultado, se obtiene una base estructurada y preparada para análisis, incorporando nuevas variables relacionadas con:

* Duración de las licencias.
* Fechas máximas de pronunciamiento.
* Cumplimiento de plazos.
* Estado de visación.
* Casos fuera de plazo.

Finalmente, la información puede ser utilizada tanto desde archivos Excel como desde PostgreSQL para posteriores procesos de análisis, reportería o visualización de datos.

## Habilidades aplicadas

`Python` · `Pandas` · `PostgreSQL` · `SQL` · `ETL` · `Data Cleaning` · `Data Transformation` · `Excel` · `Jupyter Notebook` · `Data Processing`

## Autor

**Catalina Jiménez Lillo**

Proyecto desarrollado con fines académicos y adaptado como parte de un portafolio de proyectos de análisis y procesamiento de datos.
