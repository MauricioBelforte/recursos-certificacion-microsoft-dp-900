# 6) Exploración de los aspectos básicos de Azure Cosmos DB.


Azure Cosmos DB es un servicio de base de datos en la nube altamente escalable para datos NoSQL, de Microsoft que admite varias APIs para interactuar con él.

Estos modelos almacenan datos en otras estructuras, como documentos, gráficos, almacenes de clave-valor y almacenes de familias de columnas.

#### Cosmos DB usa índices y particiones para proporcionar un rendimiento rápido de lectura y escritura y se puede escalar a volúmenes masivos de datos. Puede habilitar escrituras en varias regiones, agregando las regiones de Azure que prefiera a su cuenta de Cosmos DB para que los usuarios distribuidos globalmente puedan trabajar con datos en su réplica local.

# Descripción de Azure Cosmos DB

## Ejemplo Práctico
Imagina que desarrollas una aplicación de juegos que requiere latencia baja y manejo de grandes volúmenes de datos en tiempo real. **Azure Cosmos DB** es ideal para esto, ya que puede manejar ráfagas de actividad y proporcionar una experiencia de juego inmersiva con datos personalizados y estadísticas en tiempo real.

## ¿Qué es Azure Cosmos DB?
Azure Cosmos DB es un **sistema de administración de bases de datos NoSQL** que admite varias interfaces de programación de aplicaciones (**API**). Esto permite a los desarrolladores usar la semántica de programación de muchos tipos comunes de almacenes de datos para trabajar con datos en una base de datos Cosmos DB.

### Características Clave
- **APIs**: Permite a los desarrolladores usar APIs familiares para almacenar y consultar datos.
- **Índices y Particiones**: Usa índices y particiones para proporcionar un rendimiento rápido de lectura y escritura.
- **Escalabilidad Global**: Puede habilitar escrituras en varias regiones y agregar regiones de Azure para usuarios distribuidos globalmente.

### Cuándo Usar Cosmos DB
1. **IoT y Telemática**: Ideal para sistemas que ingieren grandes cantidades de datos en ráfagas de actividad. Los datos pueden ser usados en servicios analíticos como **Azure Machine Learning**, **Microsoft Fabric** y **Power BI**.
2. **Comercio y Marketing**: Usado en plataformas de comercio electrónico como la **Tienda Windows** y **Xbox Live**. Almacena datos de catálogo y procesa eventos de pedidos.
3. **Juegos**: Proporciona una experiencia de juego inmersiva con baja latencia y capacidad para manejar picos masivos en la velocidad de solicitudes.
4. **Aplicaciones Web y Móviles**: Modelo de interacciones sociales, integración con servicios de terceros y creación de experiencias personalizadas. Compatible con **iOS** y **Android** mediante el marco **Xamarin Framework**.

### Beneficios
- **Automatización**: Crea y mantiene índices automáticamente, reduciendo la sobrecarga administrativa.
- **Particiones Automáticas**: Asigna espacio para particiones automáticamente, cada una creciendo hasta **10 GB**.

### Escenarios Recomendados
- **IoT y Telemática**: Manejo eficiente de datos de ráfagas.
- **Comercio y Marketing**: Procesamiento de pedidos y datos de catálogo.
- **Juegos**: Latencia baja y manejo de grandes volúmenes de datos en tiempo real.
- **Aplicaciones Web y Móviles**: Personalización y rapidez.

---



# Identificación de las API de Azure Cosmos DB

## Ejemplo Práctico
Imagina que estás desarrollando una aplicación de comercio electrónico que necesita manejar grandes volúmenes de datos de productos y usuarios en tiempo real. **Azure Cosmos DB** es ideal para esto, ya que puede escalar globalmente y proporciona baja latencia para una experiencia de usuario óptima.

## ¿Qué es Azure Cosmos DB?
Azure Cosmos DB es una **base de datos distribuida totalmente administrada y sin servidor** para aplicaciones de cualquier tamaño o escala, compatible con cargas de trabajo relacionales y no relacionales. Permite a los desarrolladores usar motores de base de datos de código abierto como **PostgreSQL, MongoDB y Apache Cassandra**.

# LAS SIGUIENTES SON LAS APIS

### Azure Cosmos DB para NoSQL
- **Modelo de Datos del Documento**: Administra los datos en formato de documento JSON.
- **Sintaxis SQL**: Utiliza sintaxis SQL para trabajar con los datos.

**Consulta SQL**:
```sql
SELECT * FROM customers c WHERE c.id = "joe@litware.com"
```
**Resultado**:
```json
{
  "id": "joe@litware.com",
  "name": "Joe Jones",
  "address": {
    "street": "1 Main St.",
    "city": "Seattle"
  }
}
```

### Azure Cosmos DB para MongoDB
- **Formato JSON Binario (BSON)**: Permite usar bibliotecas de cliente y código de MongoDB.

**Consulta MQL**:
```javascript
db.products.find({id: 123})
```
**Resultado**:
```json
{
  "id": 123,
  "name": "Hammer",
  "price": 2.99
}
```

### Azure Cosmos DB para PostgreSQL
- **Base de Datos Relacional Nativa de PostgreSQL**: Distribuida globalmente y particiona automáticamente los datos.

**Consulta SQL**:
```sql
SELECT ProductName, Price FROM Products WHERE ProductID = 123;
```
**Resultado**:
| ProductName | Price |
|-------------|-------|
| Hammer      | 2.99  |

### Azure Cosmos DB para Table
- **Tablas de Clave-Valor**: Similar a Azure Table Storage pero con mayor escalabilidad y rendimiento.

**Ejemplo de Tabla**:
| PartitionKey | RowKey | Name      | Email              |
|--------------|--------|-----------|--------------------|
| 1            | 123    | Joe Jones | joe@litware.com    |
| 1            | 124    | Samir Nadoy| samir@northwind.com|

**Consulta API**:
```text
https://endpoint/Customers(PartitionKey='1',RowKey='124')
```

### Azure Cosmos DB para Apache Cassandra
- **Compatibilidad con Cassandra**: Usa una estructura de almacenamiento de familia de columnas.

**Consulta SQL**:
```sql
SELECT * FROM Employees WHERE ID = 2
```

### Azure Cosmos DB para Apache Gremlin
- **Estructura de Grafos**: Define entidades como vértices y relaciones como bordes.

**Agregar Vértice**:
```apache
g.addV('employee').property('id', '3').property('firstName', 'Alice')
g.V('3').addE('reports to').to(g.V('1'))
```

**Consultar Vértices**:
```apache
g.V().hasLabel('employee').order().by('id')
```

## Resumen
Azure Cosmos DB proporciona una solución escalable y de baja latencia para diversas aplicaciones, admitiendo múltiples APIs y tipos de datos para adaptarse a diferentes necesidades de almacenamiento y procesamiento.

---



Azure Cosmos DB proporciona una solución de base de datos a escala global para datos no relacionales.

En este módulo aprenderá a:

Describir e las características y funcionalidades clave de Azure Cosmos DB

Identificación de las API de Azure Cosmos DB

Aprovisionar y usar una instancia de Azure Cosmos DB