# Módulo 4: Datos no relacionales en Azure

## Clase 8

## **Parte 1: Exploración de analítica de datos con Azure Synapse, Data Lake, HD Insighty Databricks**
  - Se transmitió el: miércoles 30 de Octubre a las 20:00
  - [Ver grabación](https://codigofacilito.com/videos/introduccion-exploracion-de-analitica-de-datos-con-azure-synapse-data-lake-hd-insighty-databricks-parte-1)
  

  
# Objetivos de la clase/Intro

Hoy nos adentraremos de forma práctica en el servicio **Azure Synapse Analytics**.  
Realizaremos algunos ejercicios que te permitirán:  
- Explorar este servicio.  
- Crear nuestra base de datos y tablas.  
- Realizar **ingesta de datos** (carga).  
- Hacer análisis con **SQL (serverless)** y **Spark**.


# /01 Prácticas

- **1 – Crear un espacio de trabajo Synapse (Synapse workspace)**  
  [Enlace a la guía](https://learn.microsoft.com/en-us/azure/synapse-analytics/get-startedcreate-workspace)

- **2 – Analizar datos con un pool SQL serverless**  
  [Enlace a la guía](https://learn.microsoft.com/en-us/azure/synapse-analytics/get-startedanalyze-sql-on-demand)

- **3 – Analizar con Apache Spark**  
  [Enlace a la guía](https://learn.microsoft.com/en-us/azure/synapse-analytics/get-startedanalyze-spark)

- **4 – Explorar Azure Synapse Analytics**  
  [Enlace a la guía](https://microsoftlearning.github.io/dp-203-azure-dataengineer/Instructions/Labs/01-Explore-Azure-Synapse.html)

- **5 – Analizar datos en una base de datos Lake**  
  [Enlace a la guía](https://microsoftlearning.github.io/dp-203-azure-dataengineer/Instructions/Labs/04-Create-a-Lake-Database.html)




# Comprendiendo Azure Synapse, Data Lake, HD Insight y Databricks

## **Azure Synapse Analytics**
Azure Synapse es una plataforma integral SasS que combina **almacenamiento y análisis de datos masivos**  
### Características:
- Ejecuta consultas SQL y Apache Spark para datos estructurados y no estructurados.
- Permite integrar servicios como Power BI y Azure Machine Learning.
- Modelos de uso escalables: dedicado y sin servidor.
### Casos de uso:
Ideal para análisis masivo, integración de datos y soluciones de inteligencia artificial.

---

## **Azure Data Lake**
Azure Data Lake es un repositorio centralizado para almacenar grandes volúmenes de datos en su formato original.  
### Características:
- Maneja datos estructurados, semiestructurados y no estructurados.
- Totalmente escalable, diseñado para Big Data.
- Integración con herramientas como Hadoop y Databricks.
### Casos de uso:
Análisis interactivo y procesos de datos masivos.

---

## **Azure HD Insight**
Azure HD Insight es un servicio administrado para **ejecutar tecnologías de macrodatos** como Hadoop y Spark.  
### Características:
- Clústeres configurables y escalables.
- Compatible con Kafka, Hive y otras herramientas de análisis de datos.
### Casos de uso:
**Procesamiento en tiempo real** y canalizaciones de datos avanzadas.

---

## **Azure Databricks**
Azure Databricks es una plataforma de análisis de datos e inteligencia artificial.  
### Características:
- Optimizado para integrar Data Lake y Blob Storage.
- Facilita ETL, análisis avanzado y machine learning.
### Casos de uso:
Modelado predictivo, generación de paneles y soluciones basadas en IA.
---

## **Relación entre Gen1 y Gen2**
- Aunque ambos comparten el mismo propósito general (almacenar y procesar datos masivos), Gen2 representa la versión más moderna, con mejoras significativas en flexibilidad, rendimiento, seguridad e integración.

- Si alguien menciona "Data Lake" sin especificar, generalmente se refiere a **Data Lake Gen2**, que es el estándar actual en el ecosistema de Azure.

---

# Almacenamiento de Azure Synapse Analytics

## **Data Warehouse Propio**
Azure Synapse tiene su propio almacenamiento dedicado que funciona como su **Data Warehouse**, diseñado específicamente para **datos estructurados**.

### **Características del Data Warehouse en Synapse**
1. **SQL Dedicado (Dedicated SQL Pool):**
   - Motor principal del Data Warehouse.
   - Proporciona recursos exclusivos para almacenar y procesar datos estructurados.
   - Optimizado para análisis empresariales y consultas rápidas.

2. **Sin Servidor (Serverless SQL Pool):**
   - Permite ejecutar consultas SQL directamente sobre datos en un **Data Lake**.
   - No requiere cargar datos al almacenamiento dedicado.
   - Ideal para análisis ad-hoc y datos no estructurados.

3. **Escalabilidad:**
   - El almacenamiento dedicado se adapta a grandes volúmenes de datos empresariales según las necesidades.

---

## **Relación con Data Lake**
Aunque Azure Synapse tiene un Data Warehouse dedicado, también se complementa con **Azure Data Lake**:
- El Data Lake sirve como repositorio para almacenar datos en su formato original (raw data).
- Los datos pueden transformarse en el Data Lake y luego cargarse al Data Warehouse para análisis estructurado.

---

## **Conclusión**
El Data Warehouse en Synapse es un componente exclusivo para datos estructurados y análisis empresarial, mientras que el Data Lake complementa esta funcionalidad al manejar datos no estructurados y masivos.


---


# Ejecución de Consultas en Azure Synapse Analytics

## **Azure Synapse Analytics: SQL y Apache Spark**
Azure Synapse Analytics tiene su propio motor de consultas SQL, diseñado para trabajar con datos tanto almacenados en:
- **Data Warehouse dedicado:** Datos estructurados organizados en tablas.
- **Azure Data Lake:** Datos no estructurados o semiestructurados.

## **Contexto**
- El motor SQL de Synapse permite realizar consultas directamente dentro del ecosistema de Synapse.
- Aunque puede interactuar con **Azure SQL Database** como origen o destino de datos, no se limita exclusivamente a esta base de datos.
- Synapse también integra Apache Spark para manejar datos no estructurados y realizar análisis avanzados o transformaciones.

---

### Contexto:
1. **Consultas SQL en Synapse:**
   - Puedes realizar consultas T-SQL directamente sobre datos almacenados en Synapse (almacenamiento dedicado o sin servidor).
   - También permite analizar datos almacenados en **Azure Data Lake**, Blob Storage u otras fuentes, sin necesidad de cargarlos previamente en una base de datos.

2. **Relación con Azure SQL Database:**
   - Aunque Synapse y Azure SQL Database utilizan sintaxis SQL, no es obligatorio usar Azure SQL Database como fuente o destino.
   - Sin embargo, puedes integrar **Azure SQL Database** como origen o destino de datos en Synapse para mover o procesar datos entre ambos servicios.

3. **Apache Spark:**
   - Spark en Synapse **permite procesar datos no estructurados** y **realizar análisis avanzados** o transformaciones masivas, usando lenguajes como Python, Scala o SQL.

En resumen, el motor SQL de Synapse está diseñado para manejar consultas directamente dentro del ecosistema de Synapse y puede interactuar con Azure SQL Database, pero no se limita a esta base de datos.

---

# Azure Synapse Analytics y su Data Warehouse

**Azure Synapse Analytics** tiene su propio almacenamiento dedicado que funciona como su **Data Warehouse**. Este almacenamiento es diferente de un **Data Lake** y está específicamente diseñado para trabajar con datos estructurados que se organizan en tablas, filas y columnas.

### **Características del Data Warehouse de Synapse**
1. **SQL Dedicado (Dedicated SQL Pool):**
   - Este es el motor principal del *Data Warehouse* en Synapse.
   - Proporciona recursos exclusivos para almacenar y procesar datos estructurados.
   - Optimizado para consultas rápidas y análisis de datos empresariales.

2. **Sin Servidor (Serverless SQL Pool):**
   - Permite ejecutar consultas SQL directamente sobre datos en un **Data Lake** sin necesidad de cargarlos en el almacenamiento dedicado.
   - Útil para análisis ad-hoc o cuando los datos no necesitan estar estructurados completamente.

3. **Escalabilidad:**
   - El almacenamiento dedicado puede crecer en capacidad para manejar grandes volúmenes de datos empresariales.

---

## **Resumen**
El **Data Warehouse** de Synapse es un componente propio dentro de la plataforma, optimizado para datos estructurados y análisis empresariales. Sin embargo, también puede complementar un **Data Lake** para aprovechar ambas capacidades según las necesidades de procesamiento de datos.

---


# Definición: Apache Spark

**Apache Spark** es una plataforma de análisis de datos de código abierto diseñada para el procesamiento de datos masivos en tiempo real y en lotes (*batch processing*). Ofrece un motor rápido y de propósito general, altamente escalable, que permite realizar tareas complejas de análisis y procesamiento distribuido.

### **Características principales:**
1. **Procesamiento distribuido:**
   - Divide las tareas en múltiples nodos dentro de un clúster, lo que permite manejar grandes volúmenes de datos.
   
2. **Velocidad:**
   - Es mucho más rápido que otras tecnologías como Hadoop MapReduce debido a su capacidad de mantener datos en memoria durante las operaciones.

3. **API versátil:**
   - Proporciona soporte para varios lenguajes de programación como Python, Scala, Java y R, además de una interfaz SQL.

4. **Soporte de datos estructurados y no estructurados:**
   - Trabaja con múltiples formatos de datos, como archivos CSV, JSON, Parquet, bases de datos relacionales y datos no estructurados.

5. **Casos de uso:**
   - Análisis en tiempo real.
   - Aprendizaje automático.
   - Transformación y limpieza de datos.
   - Consultas SQL sobre datos distribuidos.

Spark se utiliza ampliamente en sistemas de Big Data y análisis avanzado, integrándose con herramientas como Hadoop, Databricks y Azure Synapse Analytics.


# Disponibilidad de Apache Spark en Azure

## **Azure Synapse Analytics**
- Incluye la integración de **Apache Spark** para procesar y transformar grandes volúmenes de datos.
- Permite realizar análisis avanzados sobre datos no estructurados dentro del ecosistema de Synapse.

## **Azure Databricks**
- Implementación altamente optimizada de Apache Spark.
- Diseñada para un rendimiento superior y fácil integración con otros servicios de Azure.
- Ofrece capacidades avanzadas para análisis, ETL y machine learning, aprovechando Spark como núcleo.

---


# Definición: Apache Hadoop

**Apache Hadoop** es un marco de software de código abierto diseñado para el **almacenamiento distribuido** y el procesamiento de grandes volúmenes de datos (Big Data). Es ampliamente utilizado en sistemas de análisis y procesamiento de datos en clústeres de hardware.

## **Características principales:**
1. **Almacenamiento distribuido:**
   - Utiliza un sistema de archivos llamado **HDFS (Hadoop Distributed File System)** para almacenar datos distribuidos en múltiples nodos.

2. **Procesamiento distribuido:**
   - Emplea el modelo **MapReduce** para dividir las tareas en partes más pequeñas y ejecutarlas en paralelo en un clúster.

3. **Escalabilidad:**
   - Diseñado para crecer fácilmente añadiendo más nodos a un clúster.

4. **Compatibilidad:**
   - Integración con múltiples herramientas y frameworks como Apache Hive, Apache Spark, y otros.

## **Casos de uso:**
- Procesamiento masivo de datos.
- Análisis de datos no estructurados.
- Arquitecturas de Big Data.

Hadoop ha sido uno de los principales pilares en el mundo de Big Data debido a su capacidad de manejar grandes volúmenes de datos con eficiencia.

# Hadoop en Azure

## **Azure HDInsight**
- **Azure HDInsight** es el servicio principal en Azure que soporta **Apache Hadoop**.
- Permite aprovisionar clústeres de Hadoop en la nube para procesamiento distribuido y análisis de datos masivos.
- Compatible con otros marcos de Big Data como Apache Spark, Hive, Kafka y HBase.
- Ofrece integración con servicios de Azure como **Azure Data Lake Storage**, **Azure Blob Storage** y **Azure Synapse Analytics**.

## **Características de Hadoop en HDInsight**
1. **Procesamiento distribuido:**
   - Utiliza el sistema de archivos distribuido de Hadoop (HDFS) para manejar grandes volúmenes de datos.
2. **Escalabilidad:**
   - Escalado automático para ajustar los recursos según la carga de trabajo.
3. **Gestión simplificada:**
   - Azure se encarga de la infraestructura, lo que elimina la necesidad de gestionar hardware o configuraciones complejas.

## **Casos de uso**
- Procesamiento de datos en lotes y en tiempo real.
- Análisis de datos masivos.
- Integración con herramientas de análisis y visualización como Power BI.

---




Data Factory se usa para ejecutar canalizaciones ETL. 
Data Factory permite organizar el flujo de datos sin codificar mediante canalizaciones.

Azure Synapse permite realizar análisis casi en tiempo real en los datos operativos.Azure Synapse Analytics es un servicio nativo de Azure basado en Apache Spark. 

Databricks se usa para procesar grandes cantidades de datos que son compatibles con varios proveedores de nube.
Databricks ejecuta tareas de procesamiento de datos.


HDInsight se usa para procesar grandes cantidades de datos mediante Apache Hadoop.
HDInsight ejecuta tareas de procesamiento de datos.

 
 

Data Lake es un repositorio de almacenamiento. 
Data Lake Storage es una categoría de almacén de datos analíticos.
Data Lake Storage, Event Hubs e IoT Hub son orígenes que se usan habitualmente para ingerir datos para el procesamiento de flujos.


 Primero se debe crear un servicio vinculado. 
 Las canalizaciones usan servicios vinculados existentes para cargar y procesar datos. 
 Los conjuntos de datos son la entrada y salida, y las actividades se pueden definir como el flujo de datos.

¿Cuál es una característica del procesamiento de flujos?La latencia se mide en segundos o milisegundos.


 El procesamiento de flujos es rápido. 
 Procesa los datos a medida que llegan. 
 El procesamiento de flujos ejecuta análisis simples o simplemente escribe datos en un receptor. 
 El procesamiento de flujos controla pequeños fragmentos de datos.
¿Cuál es una característica del procesamiento por lotes?
Se puede realizar un análisis complejo.
 El procesamiento por lotes se usa para ejecutar análisis complejos. El procesamiento por lotes controla una gran cantidad de datos a la vez. El procesamiento por lotes se mide normalmente en minutos y horas.
 Azure SQL Database y Azure Function son salidas.
 Azure SQL Database se usa para conservar los resultados procesados en una tabla de base de datos para realizar consultas y análisis.

 Azure Function son salidas.

 Stream Analytics permite agregar datos de un período específico antes de escribirlos en un lago de datos. 
 Event Hubs se usa como origen o receptor para el procesamiento de flujos. 

 Los gráficos de dispersión se usan para determinar una relación o correlación entre dos valores numéricos. Los gráficos circulares comparan visualmente valores diferentes como una proporción de un total. Los gráficos de líneas se usan para examinar las tendencias, normalmente en el tiempo. Los gráficos de barras se usan para comparar valores diferentes para categorías discretas.

 Una jerarquía permite explorar en profundidad una dimensión. Una dimensión permite la navegación, pero la jerarquía se usa para explorar en profundidad en una dimensión. Las tablas de hechos tienen valores. Los cubos no se crean en Microsoft PowerBI.


 RowKey es único dentro de una partición, no dentro de una tabla. Los elementos de una misma partición se almacenan en el orden de las claves de fila. Las tablas no pueden tener índices para acelerar las consultas.

 La API de MongoDB almacena datos en el formato BSON. 
 La API de Table se usa para pares clave-valor. 
 La API de Cassandra se usa para datos tabulares en un almacenamiento de familia de columnas. 
 Gremlin API se usa para las bases de datos de grafos.

 La API de Cassandra se consulta mediante SQL. 
 La API de MongoDB se consulta mediante el Lenguaje de consulta MongoDB (MQL). 
 La API de Gremlin se consulta mediante Graph. 
 La API de Table se consulta mediante consultas OData y LINQ.


 Las bases de datos de familia de columnas se usan para almacenar datos tabulares y no estructurados que comprenden filas y columnas. 
 Los grupos de Spark de Azure Synapse Analytics no admiten directamente bases de datos relacionales o de grafos.

 SQL es la API nativa en Cosmos DB. Administra los datos en formato JSON. 
 La API de Cassandra usa una estructura de almacenamiento de familia de columnas.
  La API de Table se usa para trabajar con datos en tablas clave-valor.
   La API de Gremlin se usa con datos en una estructura de grafos.

 Cada fila de una tabla de una base de datos relacional tiene el mismo número de columnas, puede tener una clave principal basada en varias columnas y debe tener un tipo de datos. Las tablas de las bases de datos relacionales no necesitan todas las columnas para contener valores o pueden requerir que solo haya una clave externa.

 Un procedimiento almacenado puede encapsular cualquier tipo de lógica de negocios que se pueda reutilizar en la aplicación. Un procedimiento almacenado puede modificar los datos existentes, así como agregar nuevas entradas a las tablas. Un procedimiento almacenado se puede ejecutar desde una aplicación, así como desde el servidor.

No se puede usar una función insertada para completar la tarea porque no puede modificar ni crear objetos. Se puede usar para consultar una base de datos. No se puede usar una vista para completar la tarea porque no puede modificar ni crear objetos. Se puede usar para consultar una base de datos. No se puede usar una función con valores de tabla para completar la tarea porque no puede modificar ni crear objetos. Se puede usar para consultar una base de datos.

Azure Synapse Analytics y Data Factory permiten crear una canalización en respuesta a un evento. Databricks y HDInsight ejecutan tareas de procesamiento de datos.

Databricks y el grupo de Spark en Azure Synapse Analytics ejecutan el procesamiento de datos para grandes cantidades de datos mediante Scala.



Delta Lake es una capa de almacenamiento de código abierto que agrega compatibilidad a Data Lake Storage para la coherencia transaccional.

Las dimensiones se usan para agregar datos. Las tablas de hechos contienen medidas agregadas, no valores para agregar. Una relación se usa para vincular datos a dimensiones. Las claves se usan para establecer relaciones.Data Lake Storage Gen2 se puede usar para almacenar archivos. Azure Synapse Analytics y Databricks se pueden usar para conservar los datos en una base de datos para realizar más consultas y análisis. Event Hubs es un servicio de ingesta de datos.



Debe compartir un informe que creó en Microsoft Power BI Desktop con otros usuarios.

¿Qué debe hacer primero?

Para compartir modelos de datos e informes creados en Power BI Desktop, primero se publican en el servicio Power BI.


Las bases de datos de serie temporal se usan para almacenar datos secuenciales. Table Storage no es adecuado para series temporales. Las bases de datos de Graph se usan para almacenar datos jerárquicos, como los gráficos organizativos que tienen nodos y bordes. Azure SQL Database es la mejor opción para las operaciones de creación, lectura, actualización y eliminación (CRUD), usa la menor cantidad de espacio de almacenamiento y no está optimizado para series temporales.

Las bases de datos OLAP se usan para esquemas de copo de nieve con datos históricos. Table Storage no es adecuado para este tipo de datos. Las bases de datos de Graph se usan para almacenar datos jerárquicos, como los gráficos organizativos que tienen nodos y bordes. Las bases de datos OLTP se usan para las operaciones de creación, lectura, actualización y eliminación (CRUD), usan la menor cantidad de espacio de almacenamiento y no son para los datos históricos en un esquema de copo de nieve.


Las bases de datos de familia de columnas se usan para almacenar datos tabulares y no estructurados que comprenden filas y columnas. Los grupos de Spark de Azure Synapse Analytics no admiten directamente bases de datos relacionales o de grafos.


¿Qué característica del procesamiento de datos transaccional garantiza que los procesos simultáneos no puedan ver los datos en un estado incoherente?

El aislamiento en el procesamiento de datos transaccionales garantiza que las transacciones simultáneas no puedan interferir entre sí y deben dar lugar a un estado de base de datos coherente.