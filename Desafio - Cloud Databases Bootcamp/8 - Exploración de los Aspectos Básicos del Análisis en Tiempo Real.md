# 8) Exploración de los Aspectos Básicos del Análisis en Tiempo Real


## Objetivos de Aprendizaje
En este módulo aprenderás a:
- Comprender el **procesamiento por lotes** y **flujos**.
- Describir los **elementos comunes** de las soluciones de datos de streaming.
- Describir las **características y funcionalidades** de la inteligencia en tiempo real en **Microsoft Fabric**.
- Describir las **características y funcionalidades** de streaming de **Apache Spark Structured** en Azure.
- Explorar el **análisis en tiempo real** en **Microsoft Fabric**.

## Requisitos Previos
Antes de iniciar este módulo, debes tener conocimientos conceptuales sobre el **almacenamiento y análisis de datos modernos**. Debes estar familiarizado con los servicios de Azure para cargas de trabajo de datos, como:
- **Azure Storage**
- **Azure SQL Database**
- **Azure Synapse Analytics**


# RESUMEN

## 1. Procesamiento por Lotes y Flujos

### Ejemplo Práctico
Imagina que tienes un sitio web de comercio electrónico y necesitas procesar los datos de ventas diarios. El **procesamiento por lotes** implica recopilar todos los datos del día y procesarlos juntos en un solo trabajo nocturno. Por otro lado, el **procesamiento de flujos** manejaría cada transacción en tiempo real a medida que ocurre.

### Resumen
- **Procesamiento por Lotes**: Procesa grandes volúmenes de datos en intervalos regulares.
- **Procesamiento de Flujos**: Maneja datos en tiempo real a medida que se generan.

## 2. Elementos Comunes de las Soluciones de Datos de Streaming

### Ejemplo Práctico
Imagina un sistema de monitorización de redes que detecta anomalías en tiempo real. Este sistema necesita componentes como **fuentes de datos**, **procesadores de streaming**, y **destinos de datos** para manejar el flujo continuo de información.

### Resumen
- **Fuentes de Datos**: Orígenes de datos en tiempo real.
- **Procesadores de Streaming**: Analizan y transforman datos en tiempo real.
- **Destinos de Datos**: Almacenan los datos procesados para su análisis posterior.

## 3. Inteligencia en Tiempo Real en Microsoft Fabric

### Ejemplo Práctico
Supongamos que utilizas **Microsoft Fabric** para analizar las interacciones de los usuarios en tu aplicación móvil en tiempo real. Esto te permite ajustar las campañas de marketing basadas en el comportamiento del usuario casi instantáneamente.

### Resumen
**Microsoft Fabric** ofrece herramientas y funcionalidades para análisis de datos en tiempo real, permitiendo tomar decisiones rápidas basadas en datos actualizados al instante.

## 4. Streaming de Apache Spark Structured en Azure

### Ejemplo Práctico
Imagina que usas **Apache Spark Structured Streaming** en Azure para procesar logs de servidores en tiempo real, identificando patrones y anomalías mientras se generan.

### Resumen
**Apache Spark Structured Streaming** en Azure permite el procesamiento en tiempo real de datos estructurados, ideal para análisis continuo y en tiempo real.

## 5. Análisis en Tiempo Real en Microsoft Fabric

### Ejemplo Práctico
Considera una empresa que utiliza **Microsoft Fabric** para análisis de datos de sensores IoT en una fábrica. Esto les permite optimizar la producción y detectar problemas operativos inmediatamente.

### Resumen
El análisis en tiempo real en **Microsoft Fabric** permite a las empresas monitorear y reaccionar a los datos a medida que se generan, mejorando la eficiencia y la toma de decisiones.



---


# Introducción al Análisis en Tiempo Real

## Contexto
El uso masivo de la tecnología por parte de personas, empresas y organizaciones, junto con la proliferación de dispositivos inteligentes y el acceso a Internet, ha generado un crecimiento masivo en el volumen de datos que se pueden generar, capturar y analizar.

### Procesamiento en Tiempo Real
Gran parte de estos datos se pueden procesar en tiempo real (o casi en tiempo real) como un flujo perpetuo de datos. Esto permite la creación de sistemas que:
- Revelan conclusiones y tendencias instantáneas.
- Toman medidas inmediatas en respuesta a los eventos a medida que se producen.

## Objetivo del Módulo
Este módulo está diseñado para:
- Presentar una **introducción conceptual** del procesamiento en tiempo real.
- Describir los **servicios de Azure** que se pueden usar para crear soluciones de análisis en tiempo real.

### Nota Importante
Este módulo **no** está diseñado para enseñar los detalles de implementación para crear una solución de procesamiento de flujos.


---

# Comprensión del Procesamiento de Flujos y por Lotes

## Introducción
El procesamiento de datos convierte datos sin procesar en información significativa. Existen dos métodos generales para procesar los datos:
- **Procesamiento por Lotes**: Se recopilan y almacenan varios registros de datos antes de procesarse juntos en una sola operación.
- **Procesamiento de Flujos (Streaming)**: Un origen de datos se supervisa y procesa constantemente en tiempo real a medida que se producen nuevos eventos de datos.

## 1. Procesamiento por Lotes

### Definición
Los datos recién llegados se recopilan y almacenan. Todo el grupo se procesa de forma conjunta, como un lote.

### Ejemplo Práctico
Un ejemplo real de procesamiento por lotes es la forma en que las empresas de tarjetas de crédito controlan la facturación. El cliente no recibe una factura por cada compra que hace con su tarjeta de crédito, sino una factura mensual que agrupa todas las compras del mes.

### Ventajas
- Procesa grandes volúmenes de datos en un momento especificado.
- Puede programarse para ejecutarse en horas de poca actividad.

### Desventajas
- Tiempo de retardo entre la ingesta de los datos y la obtención de resultados.
- Los problemas con los datos pueden detener todo el proceso hasta que se resuelvan.

## 2. Procesamiento de Flujos (Streaming)

### Definición
Cada nuevo fragmento de datos se procesa cuando llega. No hay tiempo de espera hasta el siguiente intervalo de procesamiento por lotes.

### Ejemplo Práctico
Contar automóviles en tiempo real a medida que pasan por un tramo de carretera.

### Ventajas
- Ideal para datos dinámicos nuevos generados de forma continua.
- Proporciona resultados instantáneos en tiempo real.

### Ejemplos Reales
- Seguimiento de cambios en el mercado de valores en tiempo real.
- Recomendaciones en tiempo real basadas en la ubicación geográfica en un sitio web inmobiliario.

## Diferencias entre el Procesamiento por Lotes y de Flujos

### Ámbito de los Datos
- **Lotes**: Procesa todos los datos del conjunto de datos.
- **Flujos**: Procesa solo los datos recibidos más recientemente o dentro de un período de tiempo cambiante.

### Tamaño de los Datos
- **Lotes**: Adecuado para grandes conjuntos de datos.
- **Flujos**: Diseñado para registros individuales o microlotes.

### Rendimiento
- **Lotes**: Latencia de unas horas.
- **Flujos**: Latencia en segundos o milisegundos.

### Análisis
- **Lotes**: Usado para análisis complejos.
- **Flujos**: Usado para funciones de respuesta simples y cálculos rápidos.

## Combinación del Procesamiento por Lotes y de Flujos

### Ejemplo Práctico
Un sistema de monitorización de tráfico que usa procesamiento de flujos para contar automóviles en tiempo real y almacenamiento por lotes para análisis histórico.

### Métodos Combinados
- Captura de datos de flujos en tiempo real.
- Ingesta de datos de otros orígenes en un almacén de datos.
- Procesamiento por lotes y almacenamiento para análisis históricos.
- Uso de herramientas analíticas y de visualización para explorar datos históricos y en tiempo real.

### Nota
Las arquitecturas **lambda** y **delta** combinan tecnologías para el procesamiento de datos por lotes y en tiempo real, creando una solución analítica integral.


---


# Exploración de Elementos Comunes de la Arquitectura de Procesamiento de Flujos

## Introducción
Existen muchas tecnologías para implementar una solución de procesamiento de flujos. Aunque los detalles de implementación pueden variar, hay elementos comunes en la mayoría de las arquitecturas de flujos.

### Arquitectura General para el Procesamiento de Flujos
En su forma más simple, una arquitectura de alto nivel para el procesamiento de flujos tiene el siguiente aspecto:

1. **Generación de Datos**:
   - **Ejemplo**: Una señal de un sensor, un mensaje de redes sociales, una entrada de archivo de registro.
   
2. **Captura de Datos**:
   - Los datos generados se capturan en un origen de streaming para su procesamiento.
   - **Ejemplo**: Carpeta de un almacén de datos en la nube o una tabla de base de datos.

3. **Procesamiento de Datos**:
   - Los datos se procesan mediante una consulta perpetua que selecciona y suma datos en periodos de tiempo.
   - **Ejemplo**: Recuento del número de emisiones de sensores por minuto.

4. **Salida de Datos**:
   - Los resultados del procesamiento de flujos se escriben en una salida (archivo, tabla de base de datos, panel visual en tiempo real).


## Servicios de Análisis en Tiempo Real

### 1. Azure Stream Analytics
- **Descripción**: Solución de plataforma como servicio (PaaS) para definir trabajos de streaming.
- **Funcionalidad**: Ingiere datos de un origen de streaming, aplica una consulta perpetua y escribe los resultados en una salida.

### 2. Spark Structured Streaming
- **Descripción**: Biblioteca de código abierto para soluciones de streaming complejas.
- **Funcionalidad**: Utilizada en servicios basados en Apache Spark, incluyendo Microsoft Fabric y Azure Databricks.

### 3. Microsoft Fabric
- **Descripción**: Plataforma de bases de datos y análisis de alto rendimiento.
- **Funcionalidad**: Incluye ingeniería de datos, factoría de datos, ciencia de datos, análisis en tiempo real, almacenamiento de datos y bases de datos.



## Orígenes para el Procesamiento de Flujos

### 1. Azure Event Hubs
- **Funcionalidad**: Servicio de ingesta de datos para administrar colas de datos de eventos, garantizando que cada evento se procese en orden, solo una vez.

### 2. Azure IoT Hub
- **Funcionalidad**: Similar a Azure Event Hubs, pero optimizado para administrar datos de eventos de dispositivos de Internet de las Cosas (IoT).

### 3. Azure Data Lake Store Gen 2
- **Funcionalidad**: Servicio de almacenamiento altamente escalable, usado tanto en escenarios de procesamiento por lotes como de streaming.

### 4. Apache Kafka
- **Funcionalidad**: Solución de ingesta de datos de código abierto, a menudo utilizada junto con Apache Spark.



## Receptores para el Procesamiento de Flujos

### 1. Azure Event Hubs
- **Funcionalidad**: Utilizado para poner en cola los datos procesados para su posterior procesamiento.

### 2. Azure Data Lake Store Gen 2, Microsoft OneLake o Azure Blob Storage
- **Funcionalidad**: Conservan los resultados procesados como un archivo.

### 3. Azure SQL Database, Azure Databricks o Microsoft Fabric
- **Funcionalidad**: Conservan los resultados procesados en una tabla para consultas y análisis.

### 4. Microsoft Power BI
- **Funcionalidad**: Genera visualizaciones de datos en tiempo real en informes y paneles.


---


# Exploración de la Inteligencia en Tiempo Real de Microsoft Fabric

## Introducción
La **inteligencia en tiempo real de Microsoft Fabric** permite a las organizaciones extraer información y visualizar los datos en movimiento. Ofrece una solución integral para escenarios basados en eventos, datos de streaming y registros de datos.



## Características Principales

### 1. Convergencia de Datos
- Los datos de la organización, desde gigabytes hasta petabytes, convergen en el **centro en tiempo real**.

### 2. Conectores Sin Código
- Los conectores sin código vinculan datos de diversos orígenes de manera perfecta, permitiendo una información visual inmediata, análisis geoespaciales y reacciones basadas en desencadenadores.

### 3. Transformación de Datos
- Transforma los datos en un recurso dinámico y accionable que impulsa el valor en toda la organización y se alinea sin problemas con todas las ofertas de Microsoft Fabric.

## Centro en Tiempo Real
El **centro en tiempo real** de Microsoft Fabric actúa como un catálogo centralizado para tu organización.

### Funcionalidades del Centro en Tiempo Real
- Simplifica el acceso, la adición, la exploración y el uso compartido de datos.
- Mejora la información y la claridad visual entre dominios ampliando los orígenes de datos.
- Garantiza la **disponibilidad y accesibilidad** de los datos, permitiendo tomar decisiones rápidas y acciones informadas.
- Desbloquea una **inteligencia empresarial completa** en toda la organización mediante el uso compartido de datos de streaming de diversos orígenes.



## Exploración de Datos con Inteligencia en Tiempo Real

### Pasos para Explorar Datos
1. **Seleccionar un Flujo de Datos**:
   - Elige un flujo de datos de tu organización o de orígenes externos o internos conectados.
   
2. **Uso de Herramientas de Inteligencia en Tiempo Real**:
   - Utiliza estas herramientas para la exploración de datos y para visualizar patrones de datos, anomalías y previsión de cantidades.

### Paneles en Tiempo Real
- Los paneles en tiempo real simplifican la comprensión de los datos, accesibles para todos a través de herramientas visuales, lenguaje natural y Copilot.
- Puedes convertir la información en acciones mediante la configuración de alertas Reflex para reaccionar en tiempo real.

## Nota
Para obtener más información sobre las funcionalidades de inteligencia en tiempo real de Microsoft Fabric, consulta la [documentación de inteligencia en tiempo real de Microsoft Fabric](https://docs.microsoft.com/).


---



# Exploración del Streaming Estructurado de Apache Spark

## Introducción a Apache Spark
**Apache Spark** es un marco de procesamiento distribuido para el análisis de datos a gran escala. Puedes usar Spark en **Microsoft Azure** en los siguientes servicios:
- **Microsoft Fabric**
- **Azure Databricks**

### Características Principales
- **Procesamiento en Paralelo**: Ejecuta código (en Python, Scala o Java) en paralelo en varios nodos de clúster.
- **Procesamiento de Datos a Gran Escala**: Permite procesar grandes volúmenes de datos eficazmente.
- **Procesamiento por Lotes y Flujos**: Spark se puede usar tanto para procesamiento por lotes como para procesamiento de flujos.

## Spark Structured Streaming

### Definición
**Spark Structured Streaming** es una biblioteca que proporciona una interfaz de programación de aplicaciones (**API**) para ingerir, procesar y generar resultados de flujos de datos perpetuos.

### Funcionamiento
- **Dataframe**: Spark Structured Streaming se basa en la estructura denominada **dataframe**, que encapsula una tabla de datos.
- **Lectura de Datos en Tiempo Real**: Usa la API para leer datos de un origen en tiempo real (e.g., centro de Kafka, almacén de archivos, puerto de red) a un objeto dataframe "sin límite".
- **Definición de Consultas**: Define una consulta en el dataframe que selecciona, proyecta o suma los datos en ventanas temporales.
- **Generación de Resultados**: Los resultados de la consulta crean otro dataframe para análisis o procesamiento posterior.

### Ejemplo Práctico
Imagina que usas Spark Structured Streaming para procesar datos de sensores en tiempo real, donde cada nueva lectura se añade al dataframe sin límite y se procesan las consultas para obtener estadísticas en tiempo real.

### Ventajas
**Spark Structured Streaming** es ideal para el análisis en tiempo real cuando necesitas incorporar datos de streaming en un almacén de datos analíticos o un lago de datos basado en Spark.

## Delta Lake

### Definición
**Delta Lake** es una capa de almacenamiento de código abierto que agrega características de almacenamiento de datos como la coherencia transaccional y el cumplimiento del esquema a **Data Lake Storage**.

### Funcionamiento
- **Unificación de Datos por Lotes y Flujos**: Unifica el almacenamiento para datos por lotes y de flujos.
- **Tablas Relacionales**: Define tablas relacionales para procesamiento por lotes y de flujos en Spark.
- **Origen y Receptor de Flujos**: Una tabla de Delta Lake puede ser un origen de flujos para consultas en tiempo real o un receptor donde se escribe un flujo de datos.

### Integración con Spark
Los tiempos de ejecución de Spark en **Microsoft Fabric** y **Azure Databricks** incluyen compatibilidad con Delta Lake.

### Ejemplo Práctico
Usar Delta Lake combinado con Spark Structured Streaming para abstraer datos procesados por lotes y flujos en un lago de datos detrás de un esquema relacional para realizar consultas y análisis basados en SQL.

### Ventajas
Esta combinación es óptima para mantener un esquema relacional y coherencia transaccional mientras se permite el procesamiento de flujos y por lotes.

## Nota Adicional
Para obtener más información sobre Spark Structured Streaming y Delta Lake, consulta las guías de programación correspondientes.


---