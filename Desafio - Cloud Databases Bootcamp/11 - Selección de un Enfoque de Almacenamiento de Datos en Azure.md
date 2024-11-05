# 11) Selección de un Enfoque de Almacenamiento de Datos en Azure

## Objetivos de Aprendizaje
En este módulo, aprenderás a:
- **Clasificar los datos** como **estructurados**, **semiestructurados** o **no estructurados**.
- **Determinar las necesidades operativas**, los **requisitos de latencia** y los **requisitos de transacción** de los datos.
- **Determinar si los datos requieren transacciones**.

## Conceptos Clave

### Clasificación de Datos
- **Estructurados**: Datos organizados en un formato específico, como tablas en una base de datos.
- **Semiestructurados**: Datos que no se ajustan completamente a un esquema rígido, como JSON o XML.
- **No estructurados**: Datos sin una estructura predefinida, como videos, imágenes y documentos de texto.

### Necesidades Operativas y Requisitos
- **Operativas**: Determinar la frecuencia y tipo de acceso que necesitarán los datos.
- **Latencia**: El tiempo de respuesta requerido para acceder a los datos.
- **Transacciones**: Necesidades de transacción como la **integridad** y la **consistencia** de los datos.

### Soluciones de Almacenamiento de Datos en Azure
- **Azure Storage**: Almacenamiento para datos no estructurados.
- **Azure SQL Database**: Almacenamiento para datos estructurados y transaccionales.
- **Azure Cosmos DB**: Almacenamiento para datos semiestructurados y aplicaciones que requieren latencia baja.

## Ejemplo Práctico

Imagina que trabajas en una empresa que necesita almacenar y procesar diferentes tipos de datos:
- **Imágenes y videos** de marketing (**datos no estructurados**).
- **Registros de transacciones financieras** (**datos estructurados**).
- **Documentos JSON** generados por sensores IoT (**datos semiestructurados**).

La selección de la solución de almacenamiento adecuada dependerá de las características de los datos y las necesidades específicas de tu aplicación.

---


# Introducción

Los **datos** tienen distintas formas y tamaños. No hay una solución de almacenamiento única que se adapte a todos los datos. Por ejemplo, un sitio web de comercio minorista en línea tiene varios conjuntos de datos distintos que se usan para dirigir el negocio: **datos de catálogo de productos**, **archivos multimedia** como fotos y vídeos, y **datos empresariales financieros**. Cada conjunto de datos tiene requisitos diferentes. Su trabajo consiste en determinar cuál es la mejor solución de almacenamiento.

### Factores Clave
Para decidir la solución de almacenamiento óptima, considera:
- **Cómo clasificar los datos**.
- **Cómo se utilizarán los datos**.
- **Cómo obtener el mejor rendimiento de la aplicación**.

## Objetivos de Aprendizaje
En este módulo, aprenderás a:
- **Clasificar los datos** como **estructurados**, **semiestructurados** o **no estructurados**.
- **Determinar cómo se utilizarán los datos**.
- **Determinar si los datos necesitan transacciones**.

---

# Clasificación de los Datos

En un negocio minorista en línea, puede haber diferentes tipos de datos. Cada tipo de datos podría beneficiarse de una solución de almacenamiento diferente.

## Tipos de Datos

### Datos Estructurados
- **Descripción**: A veces denominados **datos relacionales**, todos los datos tienen los mismos campos o propiedades. Tienen la misma organización y forma (**esquema**).
- **Beneficios**: Fácil de realizar búsquedas mediante **SQL**. Ideal para **sistemas CRM**, **reservas** y **administración de inventarios**.
- **Ejemplo**: Tablas de base de datos con filas y columnas.
- **Ventajas**: Fácil de escribir, consultar y analizar.
- **Desventajas**: La evolución de los datos es más complicada si se agregan o quitan campos.

### Datos Semiestructurados
- **Descripción**: Menos organizados que los datos estructurados. No se almacenan en un formato relacional. Contienen **etiquetas** que indican la organización y jerarquía. También conocidos como **datos no relacionales** o **NoSQL**.
- **Ejemplo**: Pares clave-valor.
- **Lenguajes de Serialización**: XML, JSON y YAML.
  - **XML**: Flexible y puede expresar datos complejos, pero es más voluminoso.
  
  - <Person Age="23">
    <FirstName>Quinn</FirstName>
    <LastName>Anderson</LastName>
    <Hobbies>
        <Hobby Type="Sports">Golf</Hobby>
        <Hobby Type="Leisure">Reading</Hobby>
        <Hobby Type="Leisure">Guitar</Hobby>
    </Hobbies>
    </Person>

  - **JSON**: Ligero y fácil de leer, popular en servicios web.
    {
    "firstName": "Quinn",
    "lastName": "Anderson",
    "age": "23",
    "hobbies": [
            { "type": "Sports", "value": "Golf" },
            { "type": "Leisure", "value": "Reading" },
            { "type": "Leisure", "value": "Guitar" }
        ]
    }

  - **YAML**: Más legible para los humanos, usado en archivos de configuración.
    firstName: Quinn
    lastName: Anderson
    age: 23
    hobbies:
      - type: Sports
        value: Golf
      - type: Leisure
        value: Reading
      - type: Leisure
        value: Guitar



### Datos No Estructurados
- **Descripción**: La organización de los **datos no estructurados** es indefinida. Se entregan en formato de archivo, como fotos o vídeos. El archivo puede contener **metadatos semiestructurados**, pero el contenido principal no está estructurado.
- **Ejemplo**: Archivos multimedia como fotos, vídeos y archivos de audio, documentos de Word, archivos de texto y archivos de registro.

## Clasificación de Datos: Evaluación de los Tipos de Datos
Comprender las diferencias para poder clasificar los datos te ayudará a elegir la solución de almacenamiento correcta.

- **Datos estructurados**: Organizables en tablas y columnas.
- **Datos semiestructurados**: Organizados con propiedades y valores claros, pero diversos.
- **Datos no estructurados**: No encajan en tablas o columnas, sin esquema uniforme.

### Ejemplo Práctico

- **Datos del catálogo de productos**: Semiestructurados. Ejemplo: Productos con SKU, descripción, cantidad, precio, etc.
- **Fotografías y vídeos**: No estructurados. Ejemplo: Archivos multimedia sin estructura definida.
- **Datos empresariales**: Estructurados. Ejemplo: Datos de ventas e inventario para inteligencia empresarial.

---


# Determinar las Necesidades de Operación

Después de identificar el **tipo de datos** que quieres almacenar (estructurados, semiestructurados o no estructurados), el siguiente paso consiste en **determinar cómo usarás los datos**. Esto te ayudará a planear la solución de almacenamiento de datos adecuada.

## Operaciones y Latencia

### Preguntas Clave
- ¿Va a realizar **búsquedas simples** mediante un campo de identificador?
- ¿Necesitas **consultar uno o más campos** de la base de datos?
- ¿Cuántas operaciones de **creación, actualización y eliminación** tienes previsto ejecutar?
- ¿Necesitas ejecutar **consultas analíticas complejas**?
- ¿Con qué **rapidez** se deben procesar estas operaciones?

Las respuestas a estas preguntas te ayudarán a decidir cuál es la mejor solución de almacenamiento para los datos.

## Evaluación de los Tipos de Datos

### Datos del Catálogo de Productos
- **Necesidades del Cliente**: Consultar el catálogo de productos para buscar un elemento o una categoría específica.
- **Operaciones de Lectura y Escritura**: Actualizar las cantidades del producto cuando se realiza un pedido. Las operaciones de actualización deben ser tan rápidas como las de lectura.

### Fotografías y Vídeos
- **Requisitos de Recuperación**: Necesitan tiempos de recuperación rápidos pero no necesitan consultarse de forma independiente.
- **Operaciones de Creación y Actualización**: Menos frecuentes y de menor prioridad. Pueden basarse en los resultados de la consulta del producto e incluir el identificador o la dirección URL del vídeo como propiedad en los datos del producto.

### Datos Empresariales
- **Análisis de Datos Históricos**: Los datos empresariales son de **solo lectura** y se usan para realizar **análisis complejos**.
- **Latencia**: Aceptable tener cierta latencia en los resultados.

---

# Agrupación de Varias Operaciones en una Transacción

Si un cambio en un fragmento de datos debe tener como resultado un cambio en otro, una aplicación tendrá que agrupar una serie de actualizaciones de datos. Puede usar **transacciones** para agrupar estas actualizaciones. 

## ¿Qué es una Transacción?
Una transacción es un grupo lógico de operaciones de base de datos que se ejecutan juntas. Si se produce un error en un evento de una serie de actualizaciones, toda la serie se puede revertir o deshacer.

### Garantías ACID
- **Atomicidad**: Una transacción se debe ejecutar exactamente una vez y debe ser atómica. O se realiza en su totalidad, o no se realiza.
- **Coherencia**: Garantiza que los datos sean coherentes tanto antes como después de la transacción.
- **Aislamiento**: Cada transacción no se ve afectada por otras transacciones.
- **Durabilidad**: Los cambios realizados como resultado de una transacción se guardan de forma permanente en el sistema.

## Diferencias entre OLTP y OLAP
- **OLTP (Procesamiento de Transacciones en Línea)**:
  - Admiten muchos usuarios, tiempos de respuesta rápidos y grandes volúmenes de datos.
  - Ejemplo: **Azure SQL Database**.
- **OLAP (Procesamiento Analítico en Línea)**:
  - Admiten menos usuarios, tiempos de respuesta más largos y transacciones grandes y complejas.
  - Ejemplo: **Azure Analysis Services**.

### Evaluación de los Tipos de Datos

#### Datos del Catálogo de Productos
- **Necesidad de Transacciones**: Sí.
- **Ejemplo**: Actualizar el inventario del artículo al verificar el pago.

#### Fotografías y Vídeos
- **Necesidad de Transacciones**: No.
- **Ejemplo**: Modificaciones solo cuando se realizan actualizaciones o se agregan nuevos archivos.

#### Datos Empresariales
- **Necesidad de Transacciones**: No.
- **Ejemplo**: Datos históricos y de solo lectura, utilizados para análisis complejos.

---


# Elección de una Solución de Almacenamiento en Azure

La elección de la **solución de almacenamiento correcta** puede conducir a un mejor rendimiento, ahorro de costos y capacidad de administración mejorada. Cada tipo de datos tiene requisitos de almacenamiento diferentes. Considera siempre el tipo de datos, las operaciones necesarias, la latencia prevista y la necesidad de compatibilidad transaccional.

## Datos del Catálogo de Productos

### Clasificación de Datos
- **Semiestructurados**: Debido a la necesidad de ampliar o modificar el esquema para nuevos productos.

### Operaciones
- **Lectura**: Gran número de operaciones de lectura, con posibilidad de consultar muchos campos de la base de datos.
- **Escritura**: Gran número de operaciones para realizar el seguimiento del inventario en constante cambio.

### Rendimiento y Latencia
- **Alto rendimiento** y **baja latencia**.

### Compatibilidad Transaccional
- **Necesaria**: Los datos del producto están vinculados al pago y el inventario.

### Servicio Recomendado
- **Azure Cosmos DB**: Admite datos semiestructurados o NoSQL, compatible con **ACID** y **SQL** para consultas. Replica los datos con facilidad en cualquier parte del mundo. Cinco niveles de coherencia disponibles.

## Fotografías y Vídeos

### Clasificación de Datos
- **No estructurados**.

### Operaciones
- **Recuperación**: Solo por identificador, gran número de operaciones de lectura con baja latencia.
- **Creación y Actualización**: Menos frecuentes, pueden tener mayor latencia.

### Rendimiento y Latencia
- **Baja latencia** y **alto rendimiento** para recuperaciones por identificador.

### Compatibilidad Transaccional
- **No necesaria**.

### Servicio Recomendado
- **Azure Blob Storage**: Admite almacenamiento de archivos, funciona con **Azure Content Delivery Network** para reducir la latencia.

## Datos Empresariales

### Clasificación de Datos
- **Estructurados**.

### Operaciones
- **Consultas de Análisis Complejas**: Solo lectura en varias bases de datos.

### Rendimiento y Latencia
- **Esperada** cierta latencia en los resultados debido a la naturaleza compleja de las consultas.

### Compatibilidad Transaccional
- **No necesaria**.

### Servicio Recomendado
- **Azure SQL Database**: Consultas SQL, emparejado con **Azure Analysis Services** para crear un modelo semántico.

---


