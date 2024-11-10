# 2) Exploración de Roles y Servicios de Datos

## 1. Roles en la Gestión de Datos

### A. Administradores de bases de datos
- Administran bases de datos.
- Asignan permisos a los usuarios.
- Almacenan copias de seguridad de datos.
- Restauran datos en caso de error.

### B. Ingenieros de datos
- Administran la infraestructura y los procesos para la integración de datos.
- Aplican rutinas de limpieza de datos.
- Identifican reglas de gobernanza de datos.
- Implementan canalizaciones para transferir y transformar datos entre sistemas.

### C. Analistas de datos
- Exploran y analizan datos.
- Crean visualizaciones y gráficos para que las organizaciones tomen decisiones fundamentadas.

---

# Identificación de los Servicios de Datos

Microsoft Azure es una plataforma en la nube usada por grandes organizaciones para sus aplicaciones y la infraestructura de TI. Incluye numerosos servicios para soportar soluciones en la nube, tanto para datos transaccionales como analíticos.

---

## 2. Servicios Principales de Datos en la Nube

### A. Azure SQL
Azure SQL es una familia de soluciones de base de datos relacionales basadas en Microsoft SQL Server. Incluye:
1. **Azure SQL Database**: Una base de datos PaaS totalmente administrada.
2. **Azure SQL Managed Instance**: Una instancia hospedada de SQL Server con mantenimiento automatizado y configuración flexible.
3. **Máquina virtual de Azure SQL**: Una máquina virtual con SQL Server, ofreciendo máxima capacidad de configuración y responsabilidad administrativa.

Administradores de bases de datos usan Azure SQL para aplicaciones de línea de negocio (LOB) que necesitan almacenar datos transaccionales. Ingenieros de datos y analistas pueden utilizar Azure SQL para ETL (Extracción, Transformación y Carga) y crear informes.

---

### B. Azure Database para Bases de Datos Relacionales de Código Abierto
Azure ofrece servicios administrados para bases de datos relacionales de código abierto populares, como:
1. **Azure Database for MySQL**: Un sistema fácil de usar comúnmente empleado en aplicaciones LAMP (Linux, Apache, MySQL, PHP).
2. **Azure Database for MariaDB**: Una versión mejorada y optimizada de MySQL, con compatibilidad con Oracle Database.
3. **Azure Database for PostgreSQL**: Una base de datos híbrida que permite almacenar datos relacionales y no relacionales.

Al igual que con Azure SQL, los administradores de bases de datos son responsables de gestionar estas bases de datos para aplicaciones transaccionales y proporcionan datos para ingenieros y analistas.

---

### C. Azure Cosmos DB
Azure Cosmos DB es un sistema de base de datos no relacional (NoSQL) a escala global que admite varias interfaces de programación de aplicaciones (API), permitiendo almacenar y administrar datos como documentos JSON, pares clave-valor, familias de columnas y gráficos.
1. **Administración**: Los administradores de bases de datos pueden aprovisionar y administrar instancias de Cosmos DB, aunque normalmente los desarrolladores de software gestionan el almacenamiento de datos NoSQL.
2. **Ingenieros de Datos**: Integran orígenes de datos de Cosmos DB en soluciones analíticas.
3. **Analistas de Datos**: Utilizan datos de Cosmos DB para modelado y elaboración de informes.

---

### D. Azure Storage
Azure Storage es un servicio básico de Azure que permite almacenar datos en:
1. **Contenedores de blobs**: Almacenamiento escalable y rentable para archivos binarios.
2. **Recursos compartidos de archivos**: Recursos compartidos de archivos de red.
3. **Tablas**: Almacenamiento de clave-valor para aplicaciones que necesitan leer y escribir datos rápidamente.

Ingenieros de datos usan Azure Storage para hospedar lagos de datos, organizando archivos en un sistema de archivos distribuido.

---

### E. Azure Data Factory
Azure Data Factory es un servicio que permite definir y programar canalizaciones de datos para transferir y transformar datos. Integra canalizaciones con otros servicios de Azure para ingerir, procesar y conservar datos.

Ingenieros de datos usan Azure Data Factory para construir soluciones ETL que llenan almacenes de datos analíticos con datos transaccionales.

---

### F. Microsoft Fabric
Microsoft Fabric es una plataforma unificada de análisis SaaS basada en un almacén de datos abierto y regulado que incluye funcionalidades para:
1. Ingesta de datos y ETL.
2. Análisis de almacén de lago de datos.
3. Ciencia de datos y aprendizaje automático.
4. Análisis en tiempo real.
5. Visualización de datos.
6. Gobernanza y administración de datos.
7. Información basada en inteligencia artificial.

Ingenieros de datos usan Microsoft Fabric para crear soluciones unificadas de análisis de datos centralizadas con Microsoft OneLake.

---

### G. Azure Databricks
Azure Databricks es una versión integrada de Azure de la plataforma Databricks, combinando Apache Spark con la semántica de base de datos SQL y una interfaz de administración integrada para análisis de datos a gran escala.
1. **Ingenieros de Datos**: Usan Databricks y Spark para crear almacenes de datos analíticos.
2. **Analistas de Datos**: Utilizan cuadernos nativos en Azure Databricks para consultar y visualizar datos.

---

### H. Azure Stream Analytics
Azure Stream Analytics es un motor de procesamiento de flujos en tiempo real que captura, procesa y escribe resultados de flujos de datos para análisis o procesamiento posterior.

Ingenieros de datos incorporan Azure Stream Analytics en arquitecturas de análisis de datos para ingesta y visualización en tiempo real.

---

### I. Azure Data Explorer
Azure Data Explorer es una plataforma de análisis de macrodatos totalmente administrada e independiente que ofrece consultas de alto rendimiento de datos de registro y telemetría.

Analistas de datos usan Azure Data Explorer para consultar y analizar datos con atributos de marca de tiempo, como archivos de registro y datos de telemetría de IoT.

---

### J. Microsoft Purview
Microsoft Purview ofrece una solución para la gobernanza y la detectabilidad de datos en toda la empresa. Permite crear un mapa de datos y realizar un seguimiento del linaje de datos en varios orígenes y sistemas.

Ingenieros de datos usan Microsoft Purview para aplicar gobernanza de datos, garantizando la integridad de los datos utilizados en cargas de trabajo analíticas.

---

