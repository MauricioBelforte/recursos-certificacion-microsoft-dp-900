# 14) Traslado de Datos a Azure Cosmos DB for NoSQL y desde Este

## Objetivos de Aprendizaje
Después de completar este módulo, podrás:
- **Migrar datos con los servicios de Azure**.
- **Migrar datos con Spark o Kafka**.

## Requisitos Previos
Antes de iniciar este módulo, debes tener experiencia en la **creación de aplicaciones en la nube** con **Microsoft C#** o un **lenguaje de programación similar**.

## Descripción del Módulo
En este módulo, aprenderás a migrar datos **dentro y fuera** de **Azure Cosmos DB for NoSQL** mediante **servicios de Azure** y **soluciones de código abierto**.

### Contenido del Módulo

1. **Introducción a la Migración de Datos**:
   - Conceptos y estrategias para la migración de datos a Azure Cosmos DB.

2. **Uso de Servicios de Azure para Migrar Datos**:
   - Azure Data Factory.
   - Azure Data Box.

3. **Uso de Soluciones de Código Abierto para Migrar Datos**:
   - Apache Spark.
   - Apache Kafka.

4. **Prácticas Recomendadas**:
   - Estrategias para una migración exitosa.
   - Manejo de datos a gran escala y en tiempo real.

---

# Introducción

Poco después de crear una nueva cuenta de **Azure Cosmos DB**, no es raro migrar nuevos datos a la cuenta. Hay servicios tanto dentro como fuera de Azure que puedes considerar para esta tarea. En este módulo, aprenderás sobre varios **servicios nativos de Azure** y de **código abierto** que se pueden usar para mover datos **dentro y fuera** de **Azure Cosmos DB for NoSQL**.

## Objetivos de Aprendizaje
Después de completar este módulo, podrás:
- **Migrar datos con los servicios de Azure**.
- **Migrar datos con Spark o Kafka**.

---

# Mover Datos con Azure Data Factory

**Azure Data Factory** es un servicio nativo para **extraer datos, transformarlos y cargarlos** en receptores y almacenes sin un servidor. Desde una perspectiva de integración de datos, esto significa que puede serializar los datos de un almacén de datos a otro, independientemente de los matices de cada uno, siempre que pueda transformar razonablemente los datos entre cada paradigma de datos.

## Configurar
**Azure Cosmos DB for NoSQL** está disponible como servicio vinculado en **Azure Data Factory**. Este tipo de servicio vinculado se admite como origen de ingesta de datos y como destino (receptor) de salida de datos. Para ambos, la configuración es idéntica. Puede configurar el servicio mediante el **Azure Portal** o bien mediante un objeto **JSON**.

```json
{
    "name": "<example-name-of-linked-service>",
    "properties": {
        "type": "CosmosDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<cosmos-endpoint>;AccountKey=<cosmos-key>;Database=<cosmos-database>"
        }
    }
}


```

_Sugerencia_: Como alternativa, puede usar **entidades de servicio** o **identidades administradas** para conectarse a una cuenta de Azure Cosmos DB for NoSQL con Azure Data Factory.

## Lectura desde Azure Cosmos DB
En **Azure Data Factory**, al leer datos de **Azure Cosmos DB for NoSQL**, debemos configurar nuestro servicio vinculado como **origen**. Esto leerá los datos. Para configurar esto, debemos crear una **consulta SQL** de los datos en los que queremos leer.

Por ejemplo:
```sql
SELECT id, categoryId, price, quantity, name FROM products WHERE price > 500
```

En **Azure Data Factory**, nuestra actividad de origen tiene un objeto **JSON** de configuración que podemos usar para establecer propiedades como la consulta:

```json
{
    "source": {
        "type": "CosmosDbSqlApiSource",
        "query": "SELECT id, categoryId, price, quantity, name FROM products WHERE price > 500",
        "preferredRegions": [
            "East US",
            "West US"
        ]
    }
}
```

## Escritura a Azure Cosmos DB
En **Azure Data Factory**, al almacenar datos de **Azure Cosmos DB for NoSQL**, debemos configurar nuestro servicio vinculado como **receptor**. Esto cargará nuestros datos. Para configurar esto, debemos establecer nuestro comportamiento de escritura.

Por ejemplo, podemos hacer una operación **upsert** de los datos y sobrescribir los elementos que puedan tener un identificador único correspondiente (campo id).

Nuestra actividad de recepción también tiene un objeto **JSON** de configuración:

```json
{
    "sink": {
        "type": "CosmosDbSqlApiSink",
        "writeBehavior": "upsert"
    }
}
```

---


# Movimiento de Datos mediante un Conector de Kafka

**Apache Kafka** es una plataforma de **código abierto** que se usa para transmitir eventos de forma distribuida. Muchas empresas usan Kafka para **escenarios de integración de datos de alto rendimiento a gran escala**. **Kafka Connect** es una herramienta dentro de su conjunto para transmitir datos entre Kafka y otros sistemas de datos, incluyendo **Azure Cosmos DB** como origen de datos o destino (receptor) de datos.

## Configurar
Los conectores de **Kafka Connect** para **Azure Cosmos DB** están disponibles como un proyecto de código abierto en GitHub en **microsoft/kafka-connect-cosmosdb**. Las instrucciones para descargar e instalar manualmente el archivo JAR están disponibles en el repositorio.

### Configuración
Se deben establecer cuatro propiedades de configuración para configurar correctamente la conectividad con una cuenta de **Azure Cosmos DB for NoSQL**.

| Propiedad                                | Valor                                               |
|------------------------------------------|-----------------------------------------------------|
| connect.cosmos.connection.endpoint       | URI del punto de conexión de la cuenta              |
| connect.cosmos.master.key                | Clave de cuenta                                     |
| connect.cosmos.databasename              | Nombre del recurso de la base de datos              |
| connect.cosmos.containers.topicmap       | Asignación de los temas de Kafka a los contenedores |

### Asignación de Temas a Contenedores
Cada contenedor debe asignarse a un tema. Por ejemplo, supongamos que desea que el contenedor products se asigne al tema prodlistener y el contenedor customers al tema custlistener. En ese caso, debe usar la siguiente cadena de asignación CSV: prodlistener#products,custlistener#customers.



## Escritura a Azure Cosmos DB
Vamos a escribir datos en **Azure Cosmos DB** mediante la creación de un tema. En **Apache Kafka**, todos los mensajes se envían mediante temas. 

### Crear un Nuevo Tema
```bash
kafka-topics --create 
    --zookeeper localhost:2181 
    --topic prodlistener 
    --replication-factor 1 
    --partitions 1
```

### Iniciar un Productor y Escribir Registros
```bash
kafka-console-producer 
    --broker-list localhost:9092 
    --topic prodlistener
```

Y en la consola, puedes escribir estos tres registros en el tema. Una vez hecho esto, estos registros se confirman en el contenedor de **Azure Cosmos DB for NoSQL** asignado al tema (products).

```json
{"id": "0ac8b014-c3f4-4db0-8a1f-434bab460938", "name": "handlebar", "categoryId": "78148556-4e84-44be-abae-9755dde9c9e3"}
{"id": "54ba00da-50cf-44d8-b122-1d18bd1db400", "name": "handlebar", "categoryId": "eb642a5e-0c6f-4c83-b96b-bb2903b85e59"}
{"id": "381dde84-e6c2-4583-b66c-e4a4116f7d6e", "name": "handlebar", "categoryId": "cf8ae707-6d74-4563-831a-06e15a70a0dc"}
```

## Lectura desde Azure Cosmos DB
Puedes crear un conector de origen en **Kafka Connect** con un objeto de configuración **JSON**.

```json
{
  "name": "cosmosdb-source-connector",
  "config": {
    "connector.class": "com.azure.cosmos.kafka.connect.source.CosmosDBSourceConnector",
    "tasks.max": "1",
    "key.converter": "org.apache.kafka.connect.json.JsonConverter",
    "value.converter": "org.apache.kafka.connect.json.JsonConverter",
    "connect.cosmos.task.poll.interval": "100",
    "connect.cosmos.connection.endpoint": "<cosmos-endpoint>",
    "connect.cosmos.master.key": "<cosmos-key>",
    "connect.cosmos.databasename": "<cosmos-database>",
    "connect.cosmos.containers.topicmap": "<kafka-topic>#<cosmos-container>",
    "connect.cosmos.offset.useLatest": false,
    "value.converter.schemas.enable": "false",
    "key.converter.schemas.enable": "false"
  }
}
```

### Ejemplo de Configuración
| Propiedad                             | Descripción                                           |
|---------------------------------------|-------------------------------------------------------|
| connect.cosmos.connection.endpoint    | https://dp420.documents.azure.com:443/                |
| connect.cosmos.master.key             | C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw== |
| connect.cosmos.databasename           | cosmicworks                                           |
| connect.cosmos.containers.topicmap    | prodlistener#products                                 |

### Archivo de Configuración de Ejemplo
```json
{
  "name": "cosmosdb-source-connector",
  "config": {
    "connector.class": "com.azure.cosmos.kafka.connect.source.CosmosDBSourceConnector",
    "tasks.max": "1",
    "key.converter": "org.apache.kafka.connect.json.JsonConverter",
    "value.converter": "org.apache.kafka.connect.json.JsonConverter",
    "connect.cosmos.task.poll.interval": "100",
    "connect.cosmos.connection.endpoint": "https://dp420.documents.azure.com:443/",
    "connect.cosmos.master.key": "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==",
    "connect.cosmos.databasename": "cosmicworks",
    "connect.cosmos.containers.topicmap": "prodlistener#products",
    "connect.cosmos.offset.useLatest": false,
    "value.converter.schemas.enable": "false",
    "key.converter.schemas.enable": "false"
  }
}
```

---

# Movimiento de Datos mediante Stream Analytics

**Azure Stream Analytics** es un motor de procesamiento de eventos en **tiempo real** diseñado para procesar datos de transmisión rápida de varios orígenes simultáneamente. Puede agregar, analizar, transformar e incluso mover datos a otros almacenes de datos para un análisis más profundo y posterior.

## Configurar
**Azure Stream Analytics** admite varios receptores de salida, incluido **Azure Cosmos DB for NoSQL**.

### Configuración
La configuración de la salida de **Azure Cosmos DB for NoSQL** consiste en seleccionar la cuenta dentro de la suscripción o proporcionar sus credenciales, que normalmente incluyen:

| Propiedad          | Descripción                                          |
|--------------------|------------------------------------------------------|
| Output alias       | Alias para hacer referencia a esta salida en la consulta |
| Account ID         | URI del punto de conexión de la cuenta               |
| Account Key        | Clave de cuenta                                      |
| Database           | Nombre del recurso de la base de datos               |
| Container name     | Nombre del contenedor                                 |

La base de datos y el contenedor ya deben existir en la cuenta de **Azure Cosmos DB for NoSQL** antes de usar el receptor de salida.

## Escritura a Azure Cosmos DB
Los resultados de la consulta de **Azure Stream Analytics** se procesarán como una salida **JSON** cuando se escriban en **Azure Cosmos DB for NoSQL**.

Además, los elementos se actualizan/insertan (**upsert**) en **Azure Cosmos DB for NoSQL** en función del valor del campo **id**. Normalmente, los elementos se insertan en **Azure Cosmos DB for NoSQL**. Si ya existe un elemento con el mismo identificador único, se supone que la operación es una operación de actualización en lugar de una operación de inserción.

---

# Movimiento de Datos mediante el Conector Spark de Azure Cosmos DB

Con **Azure Synapse Analytics** y **Azure Synapse Link para Azure Cosmos DB**, puedes crear un procesamiento analítico y transaccional híbrido nativo de nube (HTAP) para ejecutar análisis sobre los datos en **Azure Cosmos DB for NoSQL**.

## Configurar
Primero, asegúrate de que **Synapse Link** está habilitado en el nivel de cuenta. Esto se puede lograr mediante el **Azure Portal** o mediante la **CLI de Azure**:

```bash
az cosmosdb create --name <name> --resource-group <resource-group> --enable-analytical-storage true
```

También puedes usar **Azure PowerShell**:

```powershell
New-AzCosmosDBAccount -ResourceGroupName <resource-group> -Name <name>  -Location <location> -EnableAnalyticalStorage true
```

Al crear un contenedor, habilita el **almacenamiento analítico** en el nivel de contenedor de uno en uno. Esto se puede lograr con el portal o con la **CLI de Azure**:

```bash
az cosmosdb sql container create --resource-group <resource-group> --account <account> --database <database> --name <name> --partition-key-path <partition-key-path> --throughput <throughput> --analytical-storage-ttl -1
```

O con **Azure PowerShell**:

```powershell
New-AzCosmosDBSqlContainer -ResourceGroupName <resource-group> -AccountName <account> -DatabaseName <database> -Name <name> -PartitionKeyPath <partition-key-path> -Throughput <throughput> -AnalyticalStorageTtl -1
```

_Sugerencia_: También puedes usar los distintos **SDK de desarrollador** para habilitar o deshabilitar el almacenamiento analítico a nivel de contenedor o Synapse Link en el nivel de cuenta.

## Lectura desde Azure Cosmos DB
**Nota**: Los siguientes ejemplos de Python deben realizarse en el área de trabajo de **Azure Synapse Analytics**.

Hay dos opciones para consultar datos desde **Azure Cosmos DB for NoSQL**:

1. **Cargar un DataFrame de Spark**:
```python
productsDataFrame = spark.read.format("cosmos.olap")\
    .option("spark.synapse.linkedService", "cosmicworks_serv")\
    .option("spark.cosmos.container", "products")\
    .load()
```

2. **Crear una tabla de Spark**:
```python
create table products_qry using cosmos.olap options (
    spark.synapse.linkedService 'cosmicworks_serv',
    spark.cosmos.container 'products')
```

## Escritura a Azure Cosmos DB
**Nota**: Los siguientes ejemplos de Python deben realizarse en el área de trabajo de **Azure Synapse Analytics**.

Para escribir datos nuevos en **Azure Cosmos DB** desde un **DataFrame de Spark**:

```python
productsDataFrame.write.format("cosmos.oltp")\
    .option("spark.synapse.linkedService", "cosmicworks_serv")\
    .option("spark.cosmos.container", "products")\
    .mode('append')\
    .save()
```

Para transmitir datos desde un **DataFrame**:

```python
query = productsDataFrame\
    .writeStream\
    .format("cosmos.oltp")\
    .option("spark.synapse.linkedService", "cosmicworks_serv")\
    .option("spark.cosmos.container", "products")\
    .option("checkpointLocation", "/tmp/runIdentifier/")\
    .outputMode("append")\
    .start()

query.awaitTermination()
```

---

