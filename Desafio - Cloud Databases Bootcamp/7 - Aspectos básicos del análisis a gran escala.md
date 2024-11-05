# 7) Exploración de los aspectos básicos del análisis a gran escala.

# Introducción a las Soluciones de Análisis de Datos a Gran Escala

## Ejemplo Práctico
Imagina que tienes una tienda en línea con millones de clientes y productos. Cada vez que un cliente hace una compra, esa información se guarda en una base de datos transaccional. Para tomar decisiones de negocio inteligentes, necesitas analizar esos datos de compras junto con otros datos, como las visitas al sitio web y los comentarios de los clientes. 

## Resumen del Tema
Las soluciones de análisis de datos a gran escala combinan el **almacenamiento de datos convencional** que se usa para admitir **inteligencia empresarial (BI)** con técnicas usadas para el **análisis de macrodatos**. Normalmente, una **solución de almacenamiento de datos convencional** implica copiar datos de **almacenes de datos transaccionales** en una **base de datos relacional** con un esquema optimizado para **consultar** y **crear modelos multidimensionales**.

Sin embargo, las **soluciones de procesamiento de macrodatos** se usan con grandes volúmenes de datos en varios formatos, que se cargan o capturan por lotes en **flujos en tiempo real** y se almacenan en un **lago de datos** desde el que se usan **motores de procesamiento distribuido** como **Apache Spark** para procesarlos.

La combinación de **almacenamiento de lago de datos flexible** y **análisis de SQL de almacenamiento de datos** ha llevado a la aparición de un diseño de análisis a gran escala a menudo denominado **almacenamiento de datos**.


---

# Descripción de la Arquitectura de un Almacenamiento de Datos

## Ejemplo Práctico 
Supongamos que gestionas una tienda en línea. Cada vez que un cliente realiza una compra, esa información se guarda en una base de datos transaccional. Para analizar las ventas y mejorar tu negocio, necesitas combinar esos datos con otros, como visitas al sitio web y comentarios de clientes.

# De que se trata?
Vamos a ver cómo cargamos los datos, dónde los almacenamos, cómo los analizamos y finalmente cómo visualizamos esos análisis para tomar decisiones informadas.

## 1. Ingesta y Procesamiento de Datos

### Ejemplo Práctico
Imagina que tienes datos de ventas en una hoja de cálculo, y cada noche cargas esos datos en una base de datos más grande para analizar las tendencias de ventas. Este proceso de cargar y transformar los datos es un ejemplo de **ETL**.

### Resumen de Ingesta y Procesamiento de Datos
La ingesta de datos es el proceso de cargar datos desde diferentes orígenes.
Los datos de varios orígenes (**almacenes transaccionales**, archivos, **flujos en tiempo real**) se cargan en un **lago de datos** o **almacenamiento relacional**. Se usa **ETL** (Extracción, Transformación y Carga) o **ELT** (Extracción, Carga y Transformación) para preparar los datos para el análisis. Los **sistemas distribuidos** permiten procesar grandes volúmenes de datos.


## 2. Almacén de Datos Analíticos

### Ejemplo Práctico
Piensa en un lago de datos como un gran almacén donde se guardan todos los datos en su forma original. Luego, puedes organizar esos datos para crear informes de ventas por producto y región.

### Resumen del Almacén de Datos Analíticos
Los **almacenes de datos analíticos** pueden ser **relacionales** o basados en sistema de archivos, y a veces combinan características de ambos.


## 3. Modelo de Datos Analíticos

### Ejemplo Práctico
Crea un cubo de datos donde se suman todas las ventas por mes y por región. Esto te ayuda a ver rápidamente las tendencias de ventas en diferentes áreas.

### Resumen del Modelo de Datos Analíticos
Los **modelos de datos analíticos** (como cubos) agregan datos para facilitar **informes**, **paneles** y **visualizaciones**.


## 4. Visualización de Datos

### Ejemplo Práctico
Usa una herramienta como Power BI para crear gráficos que muestren las ventas mensuales y comparaciones entre productos. Esto ayuda a identificar cuáles productos se venden mejor y en qué meses.

### Resumen de Visualización de Datos
Los **analistas de datos** usan modelos analíticos y almacenes de datos para crear **informes** y **paneles**. Las visualizaciones ayudan a mostrar **tendencias**, **comparaciones** y **KPI** (Indicadores Clave de Rendimiento).


---


# 1)  Exploración de Canalizaciones de Ingesta de Datos

# Exploración de Canalizaciones (flujos de trabajo, paso a paso) de Ingesta (carga) de Datos

## Ejemplo General
Imagina que gestionas una empresa que recibe datos de ventas y tráfico web desde varias plataformas. Necesitas una forma eficiente de recoger, transformar y almacenar estos datos para analizarlos.

### Resumen Rápido
Las canalizaciones (flujos de trabajo, paso a paso) de ingesta (carga) de datos organizan procesos **ETL (Extract, Transform, Load - Extracción, Transformación y Carga)** para cargar y transformar datos desde diversas fuentes hacia un almacén de datos analíticos.

## ¿De qué se trata?
Vamos a explorar cómo se ingieren (cargan) datos en un almacén de datos analíticos desde diferentes orígenes, cómo se procesan y almacenan.

## Ingesta (carga) de Datos

### Ejemplo Práctico
Imagina que tienes datos de ventas almacenados en una hoja de cálculo y datos de tráfico web que provienen de un flujo en tiempo real. Usando **Azure Data Factory (ADF)**, puedes crear una canalización (flujo de trabajo, paso a paso) que extraiga, transforme y cargue estos datos en un lago de datos para su análisis.

### Resumen de Ingesta (carga) de Datos
La ingesta (carga) de datos es el proceso de cargar datos desde múltiples orígenes hacia un sistema centralizado para su análisis, usando herramientas como **Azure Data Factory (ADF)**.

## Detalles del Proceso de Ingesta (carga) de Datos

### Creación de Canalizaciones (flujos de trabajo, paso a paso)
En **Azure**, la ingesta (carga) de datos a gran escala se implementa mejor mediante la creación de **canalizaciones (flujos de trabajo, paso a paso)** que organizan procesos de **ETL (Extract, Transform, Load - Extracción, Transformación y Carga)**. Puedes crear y ejecutar estas canalizaciones (flujos) mediante **Azure Data Factory (ADF)**.

### Administración Unificada
Puedes usar el mismo motor de canalización (flujo de trabajo, paso a paso) en **Azure Data Factory (ADF)** si quieres administrar todos los componentes de la solución de almacenamiento de datos en un área de trabajo unificada.

### Actividades en las Canalizaciones (flujos de trabajo, paso a paso)
Las canalizaciones (flujos de trabajo, paso a paso) constan de una o varias actividades que operan en los datos. Un conjunto de datos de entrada proporciona los datos de origen, y las actividades se definen como un flujo de datos que manipula incrementalmente los datos hasta que se genera un conjunto de datos de salida.

### Explicacion detallada

1. **Conjunto de Datos de Entrada**:
   - **Qué es**: Los datos originales que se van a procesar.
   - **Ejemplo**: Datos de ventas que ingresan a la canalización.

2. **Actividades**:
   - **Qué son**: Las acciones o pasos que transforman los datos.
   - **Ejemplo**: Limpiar datos, transformar datos, calcular promedios.

3. **Flujo de Datos**:
   - **Qué es**: El proceso completo de llevar los datos de una actividad a la siguiente.
   - **Ejemplo**: Datos de ventas → limpieza de datos → cálculo de promedios → almacenamiento final.

4. **Conjunto de Datos de Salida**:
   - **Qué es**: Los datos finales que han sido procesados y están listos para su uso.
   - **Ejemplo**: Datos de ventas limpios y organizados listos para análisis.



### Servicios Vinculados
Las canalizaciones (flujos de trabajo, paso a paso) utilizan **servicios vinculados** para cargar y procesar datos. Por ejemplo, puedes usar un servicio vinculado de **Azure Blob Store** para ingerir (cargar) el conjunto de datos de entrada y después servicios como **Azure SQL Database** para ejecutar un procedimiento almacenado que busque valores de datos relacionados. Luego, puedes ejecutar una tarea de procesamiento de datos en **Azure Databricks** o aplicar lógica personalizada mediante una función de Azure.

### Guardado de Datos
Finalmente, puedes guardar el conjunto de datos de salida en un servicio vinculado, como **Microsoft Fabric**.

### Actividades Integradas
Las canalizaciones (flujos de trabajo, paso a paso) también pueden incluir algunas actividades integradas, que no requieren un servicio vinculado. Estas actividades permiten realizar operaciones directamente dentro de la canalización (flujo) sin necesidad de tecnologías externas.



---

# 2) Exploración de Almacenes de Datos Analíticos

## Ejemplo General
Imagina que tienes una empresa que maneja grandes cantidades de datos transaccionales y no transaccionales. Necesitas un sistema eficiente para almacenar y analizar estos datos para obtener información valiosa.

### Resumen Rápido
Hay dos tipos comunes de almacenes de datos analíticos: **almacenamientos de datos** y **lagos de datos**.

## 1. Almacenamientos de Datos

### Ejemplo Práctico
Imagina una base de datos relacional donde los datos de ventas de tu empresa se transforman y almacenan en un esquema optimizado para análisis. Por ejemplo, una tabla de hechos podría contener datos de pedidos de ventas, que se pueden agregar por dimensiones como cliente, producto, tienda y tiempo.

### Resumen de Almacenamientos de Datos
Un **almacenamiento de datos** es una **base de datos relacional** optimizada para el análisis de datos. Utiliza un **esquema de estrella** o un **esquema de copo de nieve** para organizar datos en tablas de hechos y dimensiones.

## 2. Lagos de Datos

### Ejemplo Práctico
Imagina un almacén de archivos en un sistema de archivos distribuido. Usando tecnologías como **Spark** o **Hadoop**, puedes procesar consultas en estos archivos para obtener datos para informes y análisis.

### Resumen de Lagos de Datos
Un **lago de datos** es un **almacén de archivos** en un sistema de archivos distribuido. Permite almacenar y analizar datos estructurados, semiestructurados y no estructurados sin necesidad de definir un esquema al escribir los datos.

## 3. Enfoques Híbridos

### Ejemplo Práctico
Imagina que almacenas datos sin procesar como archivos en un lago de datos, y usas puntos de conexión de análisis SQL de **Microsoft Fabric** para exponer estos datos como tablas. Esto permite consultarlos mediante SQL.

### Resumen de Enfoques Híbridos
Un **enfoque híbrido** combina características de **lagos de datos** y **almacenamientos de datos**. Usa tecnologías como **Delta Lake** y **Microsoft Fabric** para proporcionar almacenamiento relacional y análisis SQL.

## Servicios de Azure para Almacenes Analíticos

### 1. Microsoft Fabric

### Ejemplo Práctico
Microsoft Fabric combina la integridad y confiabilidad de un almacenamiento de datos relacional con la flexibilidad de una solución Apache Spark. Incluye canalizaciones de datos integradas para la ingesta y transformación de datos.

### Resumen de Microsoft Fabric
**Microsoft Fabric** es una solución integral unificada para el análisis de datos a gran escala, combinando almacenamiento relacional y flexibilidad de Spark.

### 2. Azure Databricks

### Ejemplo Práctico
Azure Databricks proporciona una plataforma completa para el análisis de datos integrada en Apache Spark. Ofrece funcionalidades nativas de SQL y clústeres de Spark optimizados para análisis de datos y ciencia de datos.

### Resumen de Azure Databricks
**Azure Databricks** es una implementación de Azure de la plataforma Databricks, que ofrece análisis de datos integrados en Apache Spark con funcionalidades nativas de SQL.

## Nota Importante
Cada uno de estos servicios puede considerarse como un almacén de datos analíticos en el sentido de que proporcionan un esquema y una interfaz para consultar los datos. En muchos casos, los datos se almacenan realmente en un lago de datos y el servicio se usa para procesarlos y ejecutar consultas.

### Ejemplo Final
Un proceso de **ingesta de extracción, carga y transformación (ELT)** puede copiar datos en el lago de datos y usar estos servicios para transformarlos y consultarlos. Por ejemplo, una canalización podría usar un cuaderno en **Azure Databricks** para procesar datos en el lago y luego cargarlos en tablas en **Microsoft Fabric**.
