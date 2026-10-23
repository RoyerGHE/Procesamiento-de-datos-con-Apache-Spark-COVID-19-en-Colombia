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
Descarga la base de datos de Putty 
```bash
wget -O /home/vboxuser/casos_covid_1M.csv \ 'https://www.datos.gov.co/resource/gt2j-8ykr.csv?$limit=1000000'
```
Revisión del nombre de las columnas para ver información relevante de la información 
```bash
head -n 1 /home/vboxuser/casos_covid_1M.csv
```
### Punto 3.2: Implementación desde Putty 
Se utiliza la terminal nano para ingresar el código Python que limpiara y analizara los datos
```bash
nano /home/vboxuser/analisis_batch_covid.py
```
Ejecucion de la depuración y análisis batch
```bash
spark-submit --driver-memory 2g /home/vboxuser/analisis_batch_covid.py --input /home/vboxuser/casos_covid_1M.csv --output /home/vboxuser/resultados_1M
```
### Punto 3.3: Resultados y consultas de datos 
Resultados obtenidos tras el análisis realizado
1) ¿Cuántos casos se registraron por departamento y por mes?, también la cantidad de casos por departamento 

<img width="331" height="587" alt="2" src="https://github.com/user-attachments/assets/1764577a-b325-4a61-9631-42b342d4e98d" />

<img width="279" height="583" alt="3" src="https://github.com/user-attachments/assets/e6f2ac5e-cfb6-4dc2-8c15-4de1e9319e6d" />

2)¿Cómo se distribuyen los casos por grupo de edad y por sexo?

<img width="349" height="368" alt="4" src="https://github.com/user-attachments/assets/7273f2db-428b-40c0-a998-80dff5618692" />

3)¿Cuál es la letalidad (fallecidos sobre casos) en cada grupo de edad?

<img width="426" height="241" alt="5" src="https://github.com/user-attachments/assets/be0c0116-95d4-41c8-a5d7-f6e279508b77" />

4)¿Cuánto tiempo transcurre, en promedio, entre el inicio de síntomas y la notificación del caso?

<img width="425" height="589" alt="6" src="https://github.com/user-attachments/assets/b97762c2-fbd6-4be3-97b4-ad32fe677b92" />

5)¿Qué porcentaje de registros tiene valores nulos, duplicados o fuera de rango, y cómo se tratan?

<img width="540" height="258" alt="7" src="https://github.com/user-attachments/assets/73635888-69b8-401d-91f3-25d154af4884" />

### Punto 3.4: Datos almacenados en formato CSV para facilitar su consulta 
Cuando se termina de ejecutar el análisis y depuración de los archivos al final de todo se puede observar las siguientes líneas de código

<img width="581" height="106" alt="8" src="https://github.com/user-attachments/assets/8a24fd7b-b591-4594-ac38-cc64763373e3" />

Esto nos muestra que la información obtenida se almacena en un archivo CSV, esto es útil ya que permite realizar consultas especificas mas rápidamente ya que solo será realizar la consulta de la información para poder verla sin la necesidad de realizar la consulta completa.
| Nombre carpeta | información almacenada |
| :--- | :--- |
| 01_casos_departamento_mes | Numero de casos en un mes determinado por departamento |
| 01b_total_por_departamento | Total de casos por departamento |
| 02_casos_edad_sexo | Total de casos por edad y sexo |
| 03_letalidad_edad | Calculo en porcentajes de la letalidad del Covid-19 por edad |
| 04_tiempo_notificacion | Tiempo entre inicio de los síntomas y la notificación |
| 05_calidad_datos | Información sobre la calidad de los datos usados | 

Código de consulta de cada uno de los datos almacenados 
```bash
#Departamento y mes
cat /home/vboxuser/resultados_1M/01_casos_departamento_mes/part-*.csv

#Total de casos departamento 
cat /home/vboxuser/resultados_1M/01b_total_por_departamento/part-*.csv

#Grupo de edad y sexo
cat /home/vboxuser/resultados_1M/02_casos_edad_sexo/part-*.csv

#Letalidad dependiendo de la edad
cat /home/vboxuser/resultados_1M/03_letalidad_edad/part-*.csv

#Tiempos síntomas y notificación
cat /home/vboxuser/resultados_1M/04_tiempo_notificacion/part-*.csv

#Calidad de los datos
cat /home/vboxuser/resultados_1M/05_calidad_datos/part-*.csv
```
### Punto 3.5: Visualización web en tiempo real
Permite visualizar en la interfaz web Spark información sobre la ejecución de la aplicación, los trabajos realizados y por realizarse, las etapas y el estado del procesamiento.
```bash
#Visualisar en web
spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.5.3 /home/vboxuser/spark_streaming_consumer.py
```

Para acceder a la pagina se debe usar la dirección http://Ip_usada:4040 





