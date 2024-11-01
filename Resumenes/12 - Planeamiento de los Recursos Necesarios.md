# 12) Planeamiento de los Recursos Necesarios

## Objetivos de Aprendizaje
Después de completar este módulo, podrás:
- **Evaluar varios requisitos de una aplicación**.

## Requisitos Previos
Antes de iniciar este módulo, debes tener experiencia en la **creación de aplicaciones en la nube** con **Microsoft C#** o un **lenguaje de programación similar**.

## Descripción del Módulo
Familiarízate con las distintas opciones de configuración para una nueva cuenta de **Azure Cosmos DB for NoSQL**.

### Contenido del Módulo
1. **Evaluar Requisitos de la Aplicación**
   - Análisis de necesidades específicas de la aplicación.
   - Determinar la mejor configuración de recursos en Azure Cosmos DB.

### Importancia
Comprender cómo configurar correctamente una cuenta de Azure Cosmos DB puede conducir a una mayor **eficiencia**, **rendimiento** y **costo-efectividad**.

---

# Introducción

A menudo, la creación de una cuenta de **Azure Cosmos DB** requiere la elección de una gran cantidad de opciones de configuración que, en principio, puede resultar algo abrumador. Aunque los valores predeterminados son válidos para una gran cantidad de escenarios, es más lógico familiarizarse con las opciones de configuración para asegurarse de que la cuenta y los recursos estén configurados de forma óptima para su solución.

## Objetivos de Aprendizaje
En este módulo, aprenderás a:
- **Preparar y configurar** una cuenta y recursos de Azure Cosmos DB para una nueva solución.
- **Evaluar varios requisitos** de una aplicación.

---

# Descripción del Rendimiento en Azure Cosmos DB

En referencia a nuestra jerarquía básica de recursos, una **base de datos** de **Azure Cosmos DB for NoSQL** es una unidad de administración para un conjunto de **contenedores independientes del esquema**. Cada contenedor es una **unidad de escalabilidad** tanto para el rendimiento como para el almacenamiento.

## Particiones y Distribución
Los **contenedores** se dividen en **particiones horizontales** y se distribuyen en todas las regiones de Azure configuradas en tu cuenta de **Azure Cosmos DB for NoSQL**.

## Aprovisionamiento del Rendimiento (reservar recursos)

### Nivel de Contenedor
- **Descripción**: El rendimiento aprovisionado (reservado) exclusivamente en el nivel de contenedor se reserva solo para este contenedor.
- **Ventajas**: Rendimiento disponible todo el tiempo y cuenta con respaldo financiero de los contratos de nivel de servicio.
- **Método Usual**: Aprovisionamiento manual del rendimiento.

### Nivel de Base de Datos
- **Descripción**: El rendimiento aprovisionado (reservado) se comparte en todos los contenedores de la base de datos.
- **Desventajas**: No se obtiene un rendimiento predecible en un contenedor específico.

### Aprovisionamiento Mixto
- **Descripción**: Combina el aprovisionamiento del rendimiento en el nivel de base de datos y en el de contenedor.
- **Restricciones**: 
  - Un contenedor con rendimiento aprovisionado (reservado) no se puede convertir en un contenedor de base de datos compartido.
  - Un contenedor de base de datos compartido no se puede convertir para tener un rendimiento dedicado.

---



# Evaluación de los Requisitos de Rendimiento

**Unidades de Solicitud por segundo (RU/s)**:
- Una manera de medir los recursos necesarios para operar con Azure Cosmos DB.
- Facilita la conversación sobre **memoria**, **CPU** y **operaciones de E/S**.

**Tipos de Operaciones que Consumen RU/s**:
- **Lecturas**
- **Escrituras**
- **Consultas**
- **Procedimientos Almacenados**

**Configuración del Rendimiento**:
- Puedes aprovisionar (reservar) **unidades de solicitud por segundo (RU/s)**.
- El mínimo es **400 RU/s**, y se puede incrementar en pasos de 100 RU/s.

**Estimación del Consumo de RU/s**:
- Algunas operaciones tienen un consumo de RU/s predecible.
- Ejemplo:
  - **Lectura**: Aproximadamente 1 RU/s por operación.
  - **Escritura**: Aproximadamente 6 RU/s por operación de un documento de 1 KB.

**Ejemplo de Cálculo de RU/s**:
1. **Escritura de un documento único**:
   - **Solicitudes por segundo**: 10,000
   - **RU por solicitud**: 10
   - **Total RU/s necesarias**: 100,000

2. **Consultas Principales**:
   - **Consulta 1**: 700 solicitudes/segundo, 100 RU por solicitud = 70,000 RU/s
   - **Consulta 2**: 200 solicitudes/segundo, 100 RU por solicitud = 20,000 RU/s
   - **Consulta 3**: 100 solicitudes/segundo, 100 RU por solicitud = 10,000 RU/s

**Total RU/s**: 200,000 RU/s

**Sugerencia**:
- Usa una hoja de cálculo para estimar cuántas RU/s necesitas.
- Puedes también probar con una aplicación y medir el consumo real de RU con el SDK de Azure Cosmos DB.

---


# Evaluación de los Requisitos de Almacenamiento de Datos

El planeamiento de una nueva cuenta de **Azure Cosmos DB** consiste en dos componentes: **rendimiento** y **almacenamiento**. Ya hemos analizado el rendimiento, pero los datos de Azure Cosmos DB también consumirán **almacenamiento de SSD facturado por GB al mes**.

## Migración de Cargas de Trabajo Transaccionales Existentes
La **calculadora de capacidad de Azure Cosmos DB** es una herramienta en línea que te ayuda a calcular los **requisitos de almacenamiento y rendimiento** de la aplicación, y traducirlos a una estimación de costos.

### Detalles Solicitados por la Calculadora
- **Total de datos almacenados**
- **Análisis casi en tiempo real**
- **Tamaño previsto de los documentos**
- **Lecturas de puntos por segundo**
- **Consultas por segundo**

Después de la estimación aproximada y la prueba de concepto, usa la calculadora de capacidad para obtener una estimación mucho más precisa de los costos para ejecutar la solución en Azure Cosmos DB.

---

# Período de Vida (TTL) en Azure Cosmos DB

Azure Cosmos DB permite establecer el **período de vida (TTL)** de los documentos en la base de datos antes de su purga automática. El TTL se mide en **segundos desde la última modificación** y se puede establecer a nivel de **contenedor** con la capacidad de invalidación por elemento.

## Configuración de TTL

### Nivel de Contenedor
- **Qué hace**: Purgar automáticamente los documentos en el momento especificado desde la última modificación.
- **Valor**: Definido como un entero en segundos. 
- **Máximo**: 2147483647 segundos.

### Expiración de TTL
La expiración de TTL es una tarea en segundo plano que se realiza mediante unidades de solicitud (RU) y se programa cuando está en modo inactivo.

### Configuración en un Contenedor
El valor de TTL de un contenedor se configura mediante la propiedad **DefaultTimeToLive** del objeto JSON del contenedor.

#### DefaultTimeToLive Expiración
- **No existe**: Los elementos no expiran automáticamente.
- **-1**: Los elementos no expirarán de forma predeterminada.
- **n segundos**: Los elementos expiran n segundos después de la última modificación.

### Configuración de TTL en un Elemento
El valor de TTL de un elemento se configura estableciendo la ruta de acceso **ttl** del elemento. Este valor solo funcionará si la propiedad **DefaultTimeToLive** está configurada para el contenedor principal. Si la ruta de acceso **ttl** está configurada para el elemento, invalidará la propiedad **DefaultTimeToLive** del contenedor principal.

#### Ejemplos

| Container.DefaultTimeToLive | Item.ttl | Expiración en segundos      |
|-----------------------------|----------|-----------------------------|
| 1000                        | null     | 1000                        |
| 1000                        | -1       | Este elemento nunca expirará|
| 1000                        | 2000     | 2000                        |
| null                        | null     | Este elemento nunca expirará|
| null                        | -1       | Este elemento nunca expirará|
| null                        | 2000     | TTL deshabilitado. Este elemento nunca expirará|

---

# Planeamiento de la Retención de Datos con Período de Vida (TTL)

**Azure Cosmos DB** solo cobra el **almacenamiento que consume directamente en tiempo real** y no es necesario reservar previamente el almacenamiento.

## Uso del TTL para Ahorro en Costos
En escenarios de **escritura elevada**, los valores de **TTL** se pueden usar para ahorrar en **costos de almacenamiento** de datos en Azure Cosmos DB. Los datos que ya se han enviado a almacenes de datos o se han almacenado en otros formularios se pueden purgar inmediatamente para garantizar que solo se mantienen los **datos nuevos y pertinentes** en el almacenamiento del SSD local.

## Soluciones para Adición y Migración de Datos
Considera soluciones como:
- **Fuente de cambios**: Controla las modificaciones en tiempo real.
- **Azure Data Warehouse**: Almacena grandes volúmenes de datos para análisis.
- **Azure Blob Storage**: Almacena archivos y datos no estructurados.

## Planificación de Retención de Datos
Al diseñar tu solución, planifica **cuánto tiempo** deberán conservarse tus datos en Azure Cosmos DB antes de migrarlos a otros espacios de la solución de Azure para **minimizar los costos de almacenamiento**.

---

