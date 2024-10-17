# 2) Exploración de Conceptos Fundamentales de Datos Relacionales

## Normalización

### A. Principios de Normalización
1. **Separar cada entidad** en su propia tabla.
2. **Separar cada atributo discreto** en su propia columna.
3. **Identificar de forma única** cada instancia de entidad (fila) mediante una **clave principal**.
4. Usar columnas de **clave externa** para vincular entidades relacionadas.

Las instancias de cada entidad se identifican de forma única mediante un identificador u otro valor de clave, conocido como **clave principal**; y cuando una entidad hace referencia a otra (por ejemplo, un pedido tiene un cliente asociado), la clave principal de la entidad relacionada se almacena como una **clave externa**.

### B. SQL (Lenguaje de Consulta Estructurado)
**SQL** significa **Lenguaje de consulta estructurado** (por sus siglas en inglés) y se usa para comunicarse con una **base de datos relacional**. Es el lenguaje estándar para los sistemas de administración de bases de datos relacionales.

Puedes usar instrucciones SQL como **SELECT, INSERT, UPDATE, DELETE, CREATE** y **DROP** para realizar prácticamente cualquier tarea que deba llevarse a cabo con una base de datos.

Algunos dialectos populares de SQL incluyen:
1. **Transact-SQL (T-SQL)**: Esta versión de SQL la usan los servicios Microsoft SQL Server y Azure SQL.

### C. Tipos de Instrucción SQL
Las instrucciones SQL se agrupan en tres grupos lógicos principales:
1. **Lenguaje de definición de datos (DDL)**
2. **Lenguaje de control de datos (DCL)**
3. **Lenguaje de manipulación de datos (DML)**

---

## Resumen

Las **bases de datos relacionales** ofrecen una manera común para que las aplicaciones transaccionales almacenen y administren datos. Constan de un **esquema de tablas**, que se vinculan a través de **valores de clave comunes**. Puedes usar **SQL** para consultar y manipular los datos de las tablas, y puedes enriquecer la base de datos mediante la creación de objetos como **vistas, procedimientos almacenados** e **índices**.

En este módulo has aprendido a:
- **Identificar las características** de los datos relacionales.
- **Definir la normalización**.
- **Identificar los tipos de instrucción SQL**.
- **Identificar objetos de base de datos relacionales comunes**.

---
