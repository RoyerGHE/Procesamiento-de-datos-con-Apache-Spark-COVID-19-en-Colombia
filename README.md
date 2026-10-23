# Procesamiento de Datos con Apache Spark: COVID-19 en Colombia

Explicación y desarrollo de la **Tarea 3 (puntos 2 y 3)**, en los que utilizando diversas herramientas se procesará y analizará una base de datos de dominio público sobre los casos positivos de COVID-19 en Colombia.

---

## Información de la Base de Datos

| Parámetro | Detalle |
| :--- | :--- |
| **Nombre** | Casos positivos de COVID-19 en Colombia |
| **Fuente** | Portal de Datos Abiertos del Estado Colombiano |
| **Formato de descarga** | CSV |
| **Procesamiento Batch** | Apache Spark |
| **Procesamiento en Tiempo Real** | Apache Kafka |
| **Cantidad de registros seleccionados** | 1,000,000 |

---

## Desarrollo del Proyecto
### Punto 1: Problemática seleccionada y puntos a tener en cuenta (Guía de aprendizaje: Punto 2)
Problemática seleccionada y puntos a tener en cuenta 
La problemática seleccionada es referente al análisis de diversos datos que se tienen sobre los casos de COVID-19 registrados en Colombia.

Las preguntas que se quiere contestar con el análisis de los datos son las siguientes.
- ¿Cuántos casos se registraron por departamento y por mes?
- ¿Cómo se distribuyen los casos por grupo de edad y por sexo?
- ¿Cuál es la letalidad (fallecidos sobre casos) en cada grupo de edad?
- ¿Cuánto tiempo transcurre, en promedio, entre el inicio de síntomas y la notificación del caso?
- ¿Qué porcentaje de registros tiene valores nulos, duplicados o fuera de rango, y cómo se tratan?

### Punto 2: Implementación en Spark (Guía de aprendizaje: Punto 3)

Informacion del entorno de desarrollo 
| Nombre | Versión |
| :--- | :--- |
| Ubuntu Server | 22.04.5 |
| Apache Spark | 3.5.3 |
| Apache Kafka | 3.9.2 |
| Python | 3 |

### Punto 3: Descarga y revisión de la base de datos de casos positivos de COVID-19 en Colombia
```bash
#Descarga la base de datos de Putty 
wget -O /home/vboxuser/casos_covid_1M.csv \ 'https://www.datos.gov.co/resource/gt2j-8ykr.csv?$limit=1000000'

#Revisión del nombre de las columnas 
head -n 1 /home/vboxuser/casos_covid_1M.csv
```
### Punto 4:




