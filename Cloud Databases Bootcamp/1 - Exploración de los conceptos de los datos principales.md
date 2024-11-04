# Exploración de los conceptos de los datos principales

### Introducción


En las últimas décadas, la **generación de datos** por **sistemas**, **aplicaciones** y **dispositivos** ha aumentado considerablemente, y estos datos se presentan en diversas estructuras y formatos. La facilidad para **recopilar** y **almacenar datos** ha mejorado, permitiendo que casi todas las empresas accedan a ellos.

Las **soluciones de datos** incluyen tecnologías de software y plataformas que facilitan la **recopilación**, **análisis** y **almacenamiento** de información valiosa. En un mercado competitivo, los datos son un recurso esencial. Cuando se analizan adecuadamente, los datos se transforman en información útil para la **toma de decisiones empresariales** críticas.

**Capturar**, **almacenar** y **analizar datos** es fundamental para todas las organizaciones. Este módulo proporciona información sobre las opciones de representación y almacenamiento de datos, así como sobre las **cargas de trabajo** típicas de los datos. Al completar el módulo, se establecerán las bases para comprender mejor las técnicas y servicios utilizados para trabajar con datos.

---

### Identificación de los formatos de datos

**Datos**: Colección de elementos (números, descripciones, observaciones) utilizados para registrar información. Representan entidades importantes para una organización, cada una con atributos (nombre, dirección, número de teléfono).

**Clasificación de los datos**:
1. **Datos estructurados**: Ajustados a un esquema fijo, representados en tablas con filas y columnas. Ejemplo: entidades Customer y Product en tablas.
2. **Datos semiestructurados**: Información con cierta estructura y variación entre entidades. Formato común: JSON.
   ```json
   // Customer 1
   {
     "firstName": "Joe",
     "lastName": "Jones",
     "address": {
       "streetAddress": "1 Main St.",
       "city": "New York",
       "state": "NY",
       "postalCode": "10099"
     },
     "contact": [
       {
         "type": "home",
         "number": "555 123-1234"
       },
       {
         "type": "email",
         "address": "joe@litware.com"
       }
     ]
   }

   // Customer 2
   {
     "firstName": "Samir",
     "lastName": "Nadoy",
     "address": {
       "streetAddress": "123 Elm Pl.",
       "unit": "500",
       "city": "Seattle",
       "state": "WA",
       "postalCode": "98999"
     },
     "contact": [
       {
         "type": "email",
         "address": "samir@northwind.com"
       }
     ]
   }
   ```

3. **Datos no estructurados**: Documentos, imágenes, datos de audio/vídeo, archivos binarios sin estructura específica.

**Almacenes de datos**:
- Almacenan datos en formatos estructurados, semiestructurados o no estructurados.
- Dos categorías: **Almacenes de archivos** y **Bases de datos**.

---

### Exploración del almacenamiento de archivos

La capacidad de almacenar datos en archivos es esencial en cualquier sistema informático. Los archivos pueden almacenarse localmente en discos duros o medios extraíbles, pero en muchas organizaciones, se almacenan centralmente en sistemas de almacenamiento compartido, cada vez más hospedados en la nube, lo que ofrece almacenamiento rentable, seguro y confiable.

#### Formatos de archivo
- **Archivos de texto delimitado**: Datos almacenados como texto con delimitadores. Ejemplo: CSV, TSV.
  ```plaintext
  FirstName,LastName,Email
  Joe,Jones,joe@litware.com
  Samir,Nadoy,samir@northwind.com
  ```
- **JSON**: Formato flexible para datos estructurados y semiestructurados.
  ```json
  {
    "customers": [
      {
        "firstName": "Joe",
        "lastName": "Jones",
        "contact": [
          {
            "type": "home",
            "number": "555 123-1234"
          },
          {
            "type": "email",
            "address": "joe@litware.com"
          }
        ]
      },
      {
        "firstName": "Samir",
        "lastName": "Nadoy",
        "contact": [
          {
            "type": "email",
            "address": "samir@northwind.com"
          }
        ]
      }
    ]
  }
  ```
- **XML**: Formato de datos legible que utiliza etiquetas.
  ```xml
  <Customers>
    <Customer name="Joe" lastName="Jones">
      <ContactDetails>
        <Contact type="home" number="555 123-1234"/>
        <Contact type="email" address="joe@litware.com"/>
      </ContactDetails>
    </Customer>
    <Customer name="Samir" lastName="Nadoy">
      <ContactDetails>
        <Contact type="email" address="samir@northwind.com"/>
      </ContactDetails>
    </Customer>
  </Customers>
  ```
- **BLOB**: Datos binarios grandes, como imágenes, video, audio, y documentos específicos de aplicaciones.

#### Formatos de archivo optimizados
- **Avro**: Formato basado en filas con encabezado JSON y datos binarios.
- **ORC**: Organiza los datos en columnas optimizadas para lectura/escritura en Apache Hive.
- **Parquet**: Formato de datos en columnas que almacena y procesa tipos de datos anidados de manera eficiente.

Las organizaciones almacenan datos en diferentes formatos para registrar detalles de entidades, eventos y otra información. Estos datos se pueden recuperar para análisis y generación de informes.


---

### Exploración de bases de datos

Las bases de datos se utilizan para definir un sistema central en el que los datos se pueden almacenar y consultar. Aunque un sistema de archivos es un tipo de base de datos, en un contexto profesional, nos referimos a sistemas dedicados para administrar registros de datos.

#### Bases de datos relacionales
- Usadas para almacenar y consultar **datos estructurados**.
- Los datos se almacenan en **tablas** que representan entidades (clientes, productos, pedidos de ventas).
- Cada entidad tiene una **clave principal** que la identifica de forma única.
- Las claves se usan para hacer referencia a entidades en otras tablas, permitiendo **normalizar** la base de datos y eliminar valores duplicados.
- Se administran y consultan mediante el **Lenguaje de consulta estructurado (SQL)**, basado en un estándar ANSI.

#### Bases de datos no relacionales
- No aplican un esquema relacional a los datos, conocidas como **NoSQL**.
- Tipos comunes:
  - **Clave-valor**: Cada registro tiene una clave única y un valor asociado.
  - **Documentos**: Valor es un documento JSON optimizado para análisis y consulta.
  - **Familia de columnas**: Almacenan datos tabulares con la posibilidad de agrupar columnas en familias.
  - **Grafos**: Almacenan entidades como nodos con vínculos que definen relaciones.

Las bases de datos no relacionales permiten mayor flexibilidad y están optimizadas para diferentes tipos de almacenamiento y consulta que las bases de datos relacionales.

---

### Exploración del procesamiento de datos transaccionales

Un sistema de procesamiento de datos transaccional registra transacciones que encapsulan eventos específicos, como movimientos financieros o pagos de bienes y servicios. Estos sistemas, conocidos como **procesamiento de transacciones en línea (OLTP)**, manejan grandes volúmenes de transacciones diarias y requieren acceso rápido a los datos.

#### Soluciones OLTP
- **Optimización de lectura y escritura**: Almacenan datos de manera que permiten operaciones rápidas de creación, recuperación, actualización y eliminación de registros (CRUD).
- **Semántica ACID**: 
  - **Atomicidad**: Cada transacción se completa totalmente o no se realiza.
  - **Coherencia**: Las transacciones llevan los datos de un estado válido a otro.
  - **Aislamiento**: Las transacciones simultáneas no interfieren entre sí.
  - **Durabilidad**: Una vez confirmada, una transacción permanece confirmada.

Los sistemas OLTP se utilizan para aplicaciones de línea de negocio (LOB) que procesan datos empresariales activamente.

---

### Exploración del procesamiento de datos analíticos

El procesamiento de datos analíticos utiliza sistemas de solo lectura o principalmente de lectura para almacenar grandes volúmenes de datos históricos o métricas empresariales. Los análisis pueden basarse en instantáneas de los datos en momentos específicos o en una serie de instantáneas.

#### Arquitectura común para análisis a escala empresarial:
1. **ETL (Extract, Transform, Load)**: Los datos operativos se extraen, transforman y cargan en un lago de datos para su análisis.
2. **Esquema de tablas**: Los datos se cargan en un esquema de tablas, normalmente en un almacén de lago de datos basado en Spark o en un almacenamiento de datos con un motor SQL relacional.
3. **Modelo OLAP**: Los datos se pueden agregar y cargar en un modelo de procesamiento analítico en línea (OLAP) o un cubo. Las medidas se calculan para intersecciones de dimensiones a partir de tablas de dimensiones.
4. **Consultas**: Los datos del lago de datos, el almacenamiento de datos y el modelo analítico se consultan para generar informes, visualizaciones y paneles.

#### Diferentes tipos de almacenamiento:
- **Lagos de datos**: Almacenan y analizan grandes volúmenes de datos basados en archivos.
- **Almacenes de datos**: Almacenan datos en un esquema relacional optimizado para operaciones de lectura y consultas.
- **Modelos OLAP**: Almacenamiento optimizado para cargas de trabajo analíticas con agregaciones de datos en diferentes dimensiones y niveles.

#### Usuarios en diferentes fases:
- **Científicos de datos**: Trabajan con archivos de datos en un lago de datos para explorar y crear modelos.
- **Analistas de datos**: Consultan tablas en el almacenamiento de datos para generar informes y visualizaciones complejos.
- **Usuarios profesionales**: Consumen datos agregados previamente en un modelo analítico como informes o paneles.

---

### Resumen

Los **datos** son la esencia de la mayoría de las **aplicaciones** y **soluciones de software**. Se pueden representar en muchos formatos, almacenarse en **archivos** y **bases de datos**, y usarse para registrar **transacciones** o para admitir los **análisis** y la **realización de informes**.

En este módulo ha aprendido a:
- Identificar formatos de datos comunes
- Describir las opciones para almacenar datos en archivos
- Describir las opciones para almacenar datos en bases de datos
- Describir las características de las soluciones de procesamiento de datos transaccionales
- Describir las características de las soluciones de procesamiento de datos analíticos

### Pasos siguientes
Ahora que ha obtenido información sobre algunos de los conceptos básicos relacionados con los datos, considere la posibilidad de aprender más sobre las cargas de trabajo relacionadas con los datos en Microsoft Azure mediante la certificación de Microsoft en Aspectos básicos de los datos de Azure.
