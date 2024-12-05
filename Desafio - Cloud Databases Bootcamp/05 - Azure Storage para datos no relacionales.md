# 5) Exploración de Azure Storage para datos no relacionales.

En este módulo, explorará las funcionalidades principales de Microsoft OneLake y Azure Storage, y aprenderá cómo se usa para admitir aplicaciones que necesitan almacenes de datos no relacionales.


# Exploración de los Servicios de Almacenamiento en Azure

## Ejemplo Práctico
Imagina una empresa que necesita almacenar y acceder a una gran cantidad de datos. Con los servicios de almacenamiento de Azure, pueden almacenar archivos, datos no estructurados, y compartir documentos entre empleados sin necesidad de invertir en hardware físico.

## Servicios Incluidos en Azure Storage

### Azure Blob Storage
- **Uso**: Almacena grandes cantidades de datos no estructurados como archivos, videos e imágenes.
- **Ideal Para**: Archivos multimedia, copias de seguridad y datos de aplicaciones.

### Azure Data Lake Storage Gen2
- **Uso**: Combina la escalabilidad y el control de costos de Azure Blob Storage con capacidades adicionales para almacenar y procesar grandes volúmenes de datos en una estructura jerárquica.
- **Ideal Para**: Análisis de macrodatos y machine learning.

### Azure Files
- **Uso**: Crea recursos compartidos de archivos en la nube, permitiendo compartir archivos de manera similar a los recursos compartidos de archivos en redes locales.
- **Ideal Para**: Compartir documentos entre empleados y departamentos.

### Azure Queue Storage
- **Uso**: Ofrece colas de mensajes para la comunicación entre componentes de aplicaciones distribuidas.
- **Ideal Para**: Gestión de tareas y flujos de trabajo asíncronos.

### Azure Table Storage
- **Uso**: Almacena datos estructurados con un esquema flexible, ideal para datos no relacionales.
- **Ideal Para**: Almacenar grandes cantidades de datos no estructurados y metadatos.

## Resumen
Azure Storage proporciona una variedad de servicios para diferentes necesidades de almacenamiento y procesamiento de datos, todos construidos sobre la misma infraestructura robusta y escalable.

---






# Exploración de Azure Blob Storage

## Qué es Azure Blob Storage
Azure Blob Storage es un servicio que permite almacenar grandes cantidades de datos no estructurados como objetos binarios grandes, o blobs, en la nube. Las aplicaciones pueden leerlos y escribirlos mediante la API de Azure Blob Storage.

## Estructura de Almacenamiento
- **Contenedores**: En una cuenta de Azure Storage, los blobs se almacenan en contenedores. Un contenedor agrupa blobs relacionados y controla quién puede leer y escribir en ellos.
- **Jerarquía de Carpetas Virtuales**: Dentro de un contenedor, puedes organizar los blobs en una jerarquía de carpetas virtuales usando el carácter "/".

## Tipos de Blobs
- **Blobs en Bloques**: Tratados como un conjunto de bloques, cada uno de hasta 4000 MiB. Ideales para objetos binarios grandes que cambian con poca frecuencia.
- **Blobs en Páginas**: Organizados como una colección de páginas de tamaño fijo de 512 bytes. Optimizados para operaciones de lectura y escritura aleatorias.
- **Blobs en Anexos**:  Solo puede agregar bloques al final de un blob en anexos; no se admite la actualización o eliminación de bloques existentes.  Ideales para escenarios donde se agregan datos continuamente.

## Niveles de Acceso
- **Acceso Frecuente**: El nivel predeterminado. Usado para blobs a los que se accede con frecuencia. Almacenamiento en medios de alto rendimiento.
- **Acceso Esporádico**: Para datos a los que se accede con poca frecuencia. Menor costo de almacenamiento.
- **Acceso de Archivo**: Para datos históricos que raramente se necesitan. El menor costo de almacenamiento pero mayor latencia.

## Administración del Ciclo de Vida
Puedes crear directivas de administración del ciclo de vida para automatizar el movimiento de blobs entre niveles de acceso (Frecuente, Esporádico, Archivo) y eliminar blobs obsoletos basándose en el tiempo desde la última modificación.

---


## Exploración de Azure Data Lake Storage Gen2



## ¿Qué es un lago de datos (Data Lake)? Copilot
Un **lago de datos** es un sistema de almacenamiento que permite guardar grandes cantidades de datos en su formato original, ya sean estructurados, semiestructurados o no estructurados.

### Ejemplo Práctico:
Piensa en un lago real. Puedes arrojar cualquier cosa al lago: troncos, piedras, hojas, etc. De manera similar, en un lago de datos, puedes almacenar archivos de texto, imágenes, videos, datos de sensores, etc., todos juntos en un mismo lugar.

### Características Clave:
1. **Almacenamiento en su Forma Original**: Puedes almacenar cualquier tipo de datos sin necesidad de transformarlos o estructurarlos previamente.
2. **Escalabilidad**: Puede manejar enormes volúmenes de datos, creciendo según tus necesidades.
3. **Flexibilidad**: Los datos se pueden analizar y procesar de diferentes maneras, sin necesidad de moverlos o duplicarlos.
4. 

### ¿Qué es Azure Data Lake Storage Gen2?
Azure Data Lake Storage Gen2 es una versión mejorada y más reciente de Azure Data Lake Store (Gen1). Se integra con Azure Storage, combinando la escalabilidad y control de costos de Azure Blob Storage con las capacidades del sistema de archivos jerárquico.

### Características Principales
1. **Almacenamiento Jerárquico**: Permite organizar los datos en una estructura de carpetas y subcarpetas, similar a un sistema de archivos tradicional.
2. **Compatibilidad**: Funciona bien con soluciones de análisis de macrodatos que manejan datos estructurados, semiestructurados y no estructurados.
3. **Integración con Azure Storage**: Aprovecha la escalabilidad del almacenamiento en blobs y los niveles de almacenamiento para controlar costos.

### Uso con Sistemas de Análisis
- **Azure Databricks**: Puede montar un sistema de archivos distribuido hospedado en Azure Data Lake Store Gen2 para procesar grandes volúmenes de datos.
- **Microsoft Fabric**: Los inquilinos de Microsoft Fabric aprovisionan automáticamente OneLake, basado en Azure Data Lake Storage Gen2.

### Cómo Crear un Sistema de Archivos Gen2
1. **Habilitar Espacio de Nombres Jerárquico**: Debes activar esta opción en una cuenta de Azure Storage al crearla, o actualizar una cuenta existente.
2. **Proceso Unidireccional**: Una vez que actualizas una cuenta de almacenamiento para que soporte un espacio de nombres jerárquico, no puedes revertirla a un espacio de nombres plano.

### Resumen
Azure Data Lake Storage Gen2 ofrece una solución robusta para el almacenamiento de datos en un formato jerárquico, aprovechando la escalabilidad y el control de costos de Azure Blob Storage. Es ideal para manejar grandes volúmenes de datos en soluciones de análisis de macrodatos.

---


# Exploración de Microsoft OneLake en Fabric


## ¿Qué es Microsoft OneLake? Copilot
OneLake es el lago de datos de Microsoft, integrado en Microsoft Fabric y basado en Azure Data Lake Storage Gen2.

### Ventajas de OneLake
- **Lago de Datos Unificado**: Todos los datos de tu organización en un solo lugar.
- **Propiedad Distribuida y Colaboración**: Diferentes equipos pueden acceder y colaborar en los mismos datos.
- **Abierto y Compatible**: Funciona bien con herramientas de análisis de datos como Azure Databricks.
- **Fácil Navegación**: Puedes explorar los datos desde tu computadora como si fuera un sistema de archivos normal.

### Integración con Sistemas de Análisis
- **Azure Databricks**: Puede montar un sistema de archivos distribuido hospedado en Azure Data Lake Storage Gen2 para procesar grandes volúmenes de datos.
- **Microsoft Fabric**: Los inquilinos de Microsoft Fabric aprovisionan automáticamente OneLake, basado en Azure Data Lake Storage Gen2.

### Cómo Crear un Sistema de Archivos Gen2
1. **Habilitar Espacio de Nombres Jerárquico**: Activa esta opción en una cuenta de Azure Storage al crearla, o actualiza una cuenta existente.
2. **Proceso Unidireccional**: Una vez que actualizas una cuenta de almacenamiento para que soporte un espacio de nombres jerárquico, no puedes revertirla a un espacio de nombres plano.

## Resumen
OneLake ofrece una solución robusta y centralizada para el almacenamiento de datos, permitiendo a las organizaciones compartir y colaborar en un único lago de datos. Aprovecha la escalabilidad y el control de costos de Azure Data Lake Storage Gen2, siendo ideal para el análisis y gestión de grandes volúmenes de datos.

---




## ¿Qué es Microsoft OneLake?
OneLake es un lago de datos único, unificado y lógico diseñado para toda tu organización. Viene automáticamente con todos los inquilinos de Microsoft Fabric y sirve como repositorio central para todos los datos de análisis, tanto estructurados como no estructurados.

## Ventajas Clave de OneLake
1. **Lago de Datos Unificado**: Proporciona un único lago de datos para toda la organización, eliminando la necesidad de crear varios lagos de datos para diferentes grupos.
2. **Propiedad Distribuida y Colaboración**: Permite crear áreas de trabajo dentro de un inquilino, lo que facilita la administración de datos por diferentes partes de la organización y promueve la colaboración mientras mantiene los límites de gobernanza.
3. **Abierto y Compatible**: Construido sobre Azure Data Lake Storage (ADLS) Gen2 y almacena los datos en formato Delta Parquet. Compatible con las API y SDK de ADLS Gen2 existentes.
4. **Fácil de Navegar**: Es sencillo navegar por los datos de OneLake desde Windows mediante el explorador de archivos de OneLake.

## Integración con Sistemas de Análisis
- **Azure Databricks**: Puede montar un sistema de archivos distribuido hospedado en Azure Data Lake Storage Gen2 para procesar grandes volúmenes de datos.
- **Microsoft Fabric**: Los inquilinos de Microsoft Fabric aprovisionan automáticamente OneLake, basado en Azure Data Lake Storage Gen2.

## Cómo Crear un Sistema de Archivos Gen2
1. **Habilitar Espacio de Nombres Jerárquico**: Activa esta opción en una cuenta de Azure Storage al crearla, o actualiza una cuenta existente.
2. **Proceso Unidireccional**: Una vez actualizas una cuenta de almacenamiento para que soporte un espacio de nombres jerárquico, no puedes revertirla a un espacio de nombres plano.

## Resumen
OneLake ofrece una solución robusta y centralizada para el almacenamiento de datos, permitiendo a las organizaciones compartir y colaborar en un único lago de datos. Aprovecha la escalabilidad y el control de costos de Azure Data Lake Storage Gen2, siendo ideal para el análisis y gestión de grandes volúmenes de datos.

---


# Exploración de Azure Files

## Ejemplo Práctico
Imagina una oficina donde todos los empleados necesitan acceder a los mismos documentos y archivos. Con Azure Files, puedes almacenar esos archivos en la nube y permitir que todos los empleados accedan a ellos desde cualquier ubicación, eliminando la necesidad de costosos servidores físicos y mejorando la colaboración.

## ¿Qué es Azure Files?
Azure Files es un servicio que te permite crear **recursos compartidos de archivos en la nube**, similares a los que se encuentran en las redes locales de las organizaciones. Permite almacenar archivos y conceder acceso a esos archivos a varios usuarios y aplicaciones.

## Ventajas de Azure Files
- **Eliminación de Costos de Hardware**: Al hospedar recursos compartidos de archivos en Azure, las organizaciones eliminan los costos de hardware y el mantenimiento.
- **Alta Disponibilidad y Escalabilidad**: Proporciona alta disponibilidad y almacenamiento escalable para los archivos.

## Características Clave
1. **Cuenta de Almacenamiento**: Azure File Storage se crea en una cuenta de almacenamiento, permitiendo compartir hasta **100 TB** de datos en una sola cuenta.
2. **Tamaño de Archivos y Conexiones**: El tamaño máximo de un solo archivo es de **1 TB**, y admite hasta **2000 conexiones simultáneas** por cada archivo compartido.
3. **Cargar Archivos**: Puedes cargar archivos mediante Azure Portal o herramientas como AzCopy.
4. **Azure File Sync**: Permite sincronizar las copias almacenadas localmente en caché con los datos de Azure File Storage.

## Niveles de Rendimiento
- **Estándar**: Usa hardware basado en disco duro. 
- **Premium**: Usa discos de estado sólido y ofrece mayor rendimiento, pero a una tarifa superior.

## Protocolos de Uso Compartido
1. **SMB (Server Message Block)**: Utilizado comúnmente entre varios sistemas operativos (Windows, Linux, macOS).
2. **NFS (Network File System)**: Utilizado por algunas versiones de Linux y macOS. Requiere una cuenta de almacenamiento de nivel Premium y una red virtual configurada para controlar el acceso.

---



# Exploración de Tablas de Azure

## Ejemplo Práctico
Imagina que necesitas una forma flexible y eficiente de almacenar información de clientes, donde cada cliente puede tener diferentes cantidades de teléfonos y direcciones. **Azure Table Storage** permite almacenar todos estos datos sin necesidad de una estructura fija, facilitando el almacenamiento y la búsqueda de información.

## ¿Qué es Azure Table Storage?
Azure Table Storage es una **solución de almacenamiento NoSQL** que usa tablas para contener **elementos de datos de clave-valor**. Cada elemento se representa mediante una fila con columnas para los campos de datos.

### Características Clave
- **Claves Únicas**: Cada fila tiene una clave única compuesta por una **clave de partición** y una **clave de fila**.
- **Columnas Flexibles**: Las columnas de cada fila pueden variar, permitiendo almacenar datos semiestructurados.
- **Desnormalización**: Los datos se desnormalizan, lo que significa que cada fila contiene los datos completos de una entidad lógica (como toda la información de un cliente).

### Ejemplo Práctico en Detalle
Una tabla de clientes en Azure Table Storage podría almacenar:
- Nombre
- Apellido
- Números de teléfono
- Direcciones

Cada fila podría tener un número diferente de teléfonos y direcciones, a diferencia de una base de datos relacional que requeriría múltiples tablas para esta información.

### Ventajas de Particionar
- **Agrupar Filas Relacionadas**: Las filas con la misma clave de partición se almacenan juntas, mejorando la organización y el rendimiento.
- **Escalabilidad y Rendimiento**: Las particiones pueden agrandarse o reducirse según sea necesario y mejorar la eficiencia de búsqueda.

### Claves de Partición y Fila
- **Clave de Partición**: Identifica la partición que contiene la fila.
- **Clave de Fila**: Es única para cada fila dentro de la partición.

### Consultas Eficientes
El esquema de claves permite realizar rápidamente:
- **Consultas de Punto**: Identificar una sola fila.
- **Consultas por Rango**: Capturar un bloque contiguo de filas en una partición.

---

