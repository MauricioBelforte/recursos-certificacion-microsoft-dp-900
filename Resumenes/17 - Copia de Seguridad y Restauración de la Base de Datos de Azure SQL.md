# 17) Copia de Seguridad y Restauración de la Base de Datos de Azure SQL

## Objetivos de Aprendizaje
- **Configurar copias de seguridad y la retención** de una base de datos de Azure SQL.
- **Restaurar** una base de datos de Azure SQL.

## Requisitos Previos
- Conocimientos básicos del servicio **Azure SQL Database**.
- Conocimientos básicos de **Azure PowerShell**.

---

# Copia de Seguridad y Restauración de la Base de Datos de Azure SQL

## Introducción
Una organización de venta al por menor migró su base de datos de ERP a Azure SQL Database, conteniendo datos operativos críticos. Es necesario configurar directivas de **retención y copia de seguridad** para protegerse contra la pérdida de datos y estar familiarizado con los **pasos de recuperación** en caso necesario.

Azure SQL Database crea automáticamente **copias de seguridad** de las bases de datos. Es crucial comprender los detalles de cada nivel de servicio, historial de restauración a un momento dado, **retención a largo plazo** y otros aspectos básicos.

## Objetivos de Aprendizaje
- Configurar **copias de seguridad** y la **retención** de una base de datos de Azure SQL.
- Restaurar una única base de datos de **Azure SQL**.

## Requisitos Previos
- Conocimientos básicos del servicio **Azure SQL Database**.
- Conocimientos básicos de **Azure PowerShell**.

---

# Copia de Seguridad de Azure SQL Database

## Almacenamiento de las Copias de Seguridad
- Azure SQL Database crea automáticamente **copias de seguridad** y las guarda durante 7 a 35 días.
- Almacenadas como blobs en una cuenta de almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS).

## Tipos de Copias de Seguridad
1. **Copias de Seguridad Completas**: Copia todo en la base de datos y en los registros de transacciones. Realizada una vez a la semana.
2. **Copias de Seguridad Diferenciales**: Copia los cambios desde la última copia de seguridad completa. Realizada cada 12 horas.
3. **Copias de Seguridad Transaccionales**: Copia los registros de transacciones, permitiendo restaurar hasta un momento específico. 

## Usos de las Copias de Seguridad
- Restaurar una nueva copia de una base de datos existente.
- Restaurar una base de datos eliminada hasta el momento de la eliminación.
- Restaurar la base de datos en una ubicación o región alternativa.
- Restaurar una base de datos a partir de una copia de seguridad a largo plazo (LTR).

## Niveles de Servicio y Copias de Seguridad
- **Básico**: Retención de una semana.
- **Estándar y Premium**: Retención de cinco semanas.
- Retención configurable de entre 0 y 35 días.

## Frecuencia de Copias de Seguridad
- Copias de seguridad automáticas completas, diferenciales y de registros de transacciones.
- Primera copia de seguridad completa al crear la base de datos.
- LTR: Copias de seguridad completas semanales hasta 10 años en Azure Blob Storage.

## Costos de Almacenamiento
- Basados en el tamaño de las instancias y el almacenamiento mensual.
- Azure Backup incluye siete días de copias de seguridad automatizadas en RA-GRS por defecto.
- Consumo adicional de almacenamiento se cobra por gigabytes por mes.

## Ventajas de las Copias de Seguridad de Azure SQL Database
- Reducción de costos de infraestructura.
- Amplia variedad de características de copia de seguridad y protección de datos.
- Tres copias de los datos en tres ubicaciones diferentes en el centro de datos principal y en un centro remoto.
- Cifrado de datos antes de salir de la base de datos de origen.

---



# Ejercicio: Configuración de Copias de Seguridad de Azure SQL Database

## Configuración de Copias de Seguridad
### Objetivo
Crear una base de datos en Azure y configurar copias de seguridad con una retención de 28 días.

### Creación de un Servidor Lógico y una Base de Datos
Utiliza la CLI de Azure para crear un servidor lógico de SQL Database y una base de datos.

#### Comandos en Azure Cloud Shell
1. Configurar variables:
```powershell
$serverName = "erpserver-$(Get-Random)"
$location = $(Get-AzResourceGroup -ResourceGroupName learn-f5b52e38-cefb-4bbd-8bca-a6a4d0917a78).location
$sqlAdmin = Get-Credential -credential dbadmin
```
password: @dminNuevo10 




2. Crear el servidor lógico:
```powershell
New-AzSqlServer `
    -ResourceGroupName learn-f5b52e38-cefb-4bbd-8bca-a6a4d0917a78 `
    -Location $location `
    -ServerName $serverName `
    -SqlAdministratorCredentials $sqlAdmin
```

3. Crear la base de datos:
```powershell
New-AzSqlDatabase `
    -ResourceGroupName learn-f5b52e38-cefb-4bbd-8bca-a6a4d0917a78 `
    -ServerName $serverName `
    -DatabaseName sql-erp-db
```

### Detalles del Comando
- **$serverName**: Nombre del servidor con un número aleatorio para garantizar unicidad global.
- **$location**: Ubicación del servidor en la ubicación del grupo de recursos.
- **$sqlAdmin**: Credenciales usadas para acceder al servidor lógico de base de datos de Azure SQL.
- **New-AzSqlServer**: Crea un servidor lógico de Azure SQL Database.
- **New-AzSqlDatabase**: Crea una base de datos aprovisionada de núcleo virtual de uso general con hardware de serie Estándar y 2 núcleos virtuales.

---

# Ejercicio: Configuración de Copias de Seguridad de Azure SQL Database

## Configuración de la Directiva de Retención de Copia de Seguridad
### Objetivo
Crear una base de datos en Azure y configurar copias de seguridad con una retención de 28 días.

### Pasos en Azure Portal
1. **Examinar la Directiva de Retención**:
   - En Azure Portal, seleccionar "Todos los recursos".
   - Seleccionar el servidor lógico de base de datos `erpserver-NNNN`.
   - En el panel de navegación izquierdo, seleccionar "Copias de seguridad".
   - En "Directivas de retención", seleccionar la base de datos `sql-erp-db`.
   - Seleccionar "Configurar directivas".
   - Mover la barra deslizante de "Restauración a un momento dado" a 28 días.
   - Seleccionar "Aplicar" y después "Sí".

### Permitir Acceso a la Red al Servidor Lógico de la Base de Datos
1. **Configurar Reglas de Firewall**:
   - En el servidor lógico de base de datos `erpserver-NNNN`, en el panel de navegación izquierdo, seleccionar "Redes".
   - En "Reglas de firewall", seleccionar "Agregar la dirección IPv4 del cliente".
   - Proporcionar la dirección IP IPv4 actual.
     EN ESTA PARTE TUVE QUE CAMBIAR LO QUE FIGURABA AHI POR MI IPv4 QUE SAQUE DE UNA PAGINA
   - En "Excepciones", activar la casilla "Permitir que los servicios y recursos de Azure accedan a este servidor".
   - Seleccionar "Guardar".

### Adición de Datos a la Base de Datos
1. **Crear una Tabla**:
   - En el panel de navegación izquierdo, seleccionar "Bases de datos SQL" y luego `sql-erp-db`.
   - Seleccionar "Editor de consultas (versión preliminar)".
   - Iniciar sesión con las credenciales `dbadmin`.
   - Ejecutar el siguiente comando SQL:
     ```sql
     CREATE TABLE Person(
         PersonId INT IDENTITY PRIMARY KEY,
         FirstName NVARCHAR(50) NOT NULL,
         LastName NVARCHAR(50) NOT NULL,
         DateOfBirth DATE NOT NULL
     )
     ```

2. **Agregar un Registro**:
   - Seleccionar "Nueva consulta".
   - Ejecutar el siguiente comando SQL:
     ```sql
     INSERT INTO Person (FirstName, LastName, DateOfBirth)
     VALUES ('Lucas', 'Ball', '1987-11-03');
     ```

3. **Consultar la Base de Datos**:
   - Seleccionar "Nueva consulta".
   - Ejecutar el siguiente comando SQL:
     ```sql
     SELECT * FROM dbo.Person;
     ```

---



# Conservación del Historial de Copias de Seguridad con Directivas de Retención a Largo Plazo

## Necesidad de Retención a Largo Plazo
Las empresas necesitan conservar **copias de seguridad** durante meses o años para proteger datos críticos y cumplir con regulaciones de protección de datos.

## Directivas de Retención de Copias de Seguridad a Largo Plazo
- **Automáticas**: Copias disponibles para restauración durante un máximo de 35 días.
- **Retención a Largo Plazo (LTR)**: Permite almacenar copias de seguridad hasta 10 años en blobs de almacenamiento RA-GRS.

## Funcionamiento de la Retención a Largo Plazo
- **Copias Automáticas**: LTR copia automáticamente las copias de seguridad en diferentes blobs con prioridad baja.
- **Directiva Configurable**: Debe configurarse una directiva para iniciarlas y administrarlas.

## Procedimientos para Directivas de Retención a Largo Plazo
- **Frecuencia de Copias de Seguridad**:
  - **W**: Copia semanal.
  - **M**: Copia mensual (primera semana de cada mes).
  - **Y**: Copia anual.

- **Duración de Retención**:
  - **W=10**: 10 semanas.
  - **Y=3**: 3 años.

## Ejemplos de Directivas de Retención a Largo Plazo
- **W=0, M=0, Y=5, WeekOfYear=3**: Conserva la copia de seguridad de la tercera semana del año durante cinco años.
- **W=0, M=10, Y=0**: Conserva la primera copia de seguridad completa de cada mes durante 10 meses.
- **W=12, M=0, Y=0**: Conserva cada copia de seguridad semanal durante 12 semanas.
- **W=4, M=12, Y=10, WeekOfYear=1**: Conserva cada copia de seguridad semanal durante cuatro semanas, la primera mensual durante 12 meses y la primera anual durante 10 años.

## Configuración de Directivas de Retención en PowerShell
### Examinar Directiva de Retención
```powershell
Get-AzSqlDatabase `
    -ResourceGroupName <ResourceGroupName> `
    -ServerName <ServerName> `
    | Get-AzSqlDatabaseLongTermRetentionPolicy
```

### Configurar Directiva
```powershell
Set-AzSqlDatabaseBackupLongTermRetentionPolicy `
    -ServerName <ServerName> `
    -DatabaseName <DatabaseName> `
    -ResourceGroupName <ResourceGroupName> `
    -WeeklyRetention P10W `
    -YearlyRetention P3Y `
    -WeekOfYear 1
```

---

# Recuperación de Datos mediante la Restauración de una Instancia de Azure SQL Database

## Qué se Puede Restaurar
- **Copias de Seguridad Automatizadas**: Copian bases de datos a blobs en cuentas de almacenamiento RA-GRS.
- **Opciones de Restauración**:
  - Crear una base de datos en el mismo servidor recuperada a un momento dado.
  - Crear una base de datos en el mismo servidor recuperada en el momento de la eliminación.
  - Crear una nueva base de datos en cualquier servidor de la misma región recuperada en el momento de las copias de seguridad más recientes.
  - Crear una nueva base de datos en cualquier servidor de cualquier región recuperada hasta el momento de las copias de seguridad con replicación más recientes.

## Funcionamiento de la Restauración
- **Proceso**: Azure restaura la base de datos de la cuenta de almacenamiento en el servidor lógico de Azure SQL Database especificado.
- **Duración**: Varía según el tamaño de la base de datos, registros de transacciones, ancho de banda de la red y número de operaciones de restauración simultáneas. La mayoría finalizan en menos de 12 horas.
- **Recomendación**: Realizar restauraciones de prueba regularmente.

## Realización de una Restauración a un Momento Dado
### Opciones
1. **Reemplazo de la Base de Datos**:
   - Especificar el mismo tamaño de procesamiento y nivel de servicio.
   - Cambiar el nombre de la base de datos original y asignar a la restaurada el nombre original mediante comandos ALTER DATABASE de T-SQL.
2. **Recuperación de Datos**:
   - Usar comandos de T-SQL para extraer datos de la base de datos restaurada e insertarlos en la original.

### Procedimientos
- **Azure Portal**: Seleccionar "Restaurar" en la página de información general de la base de datos y especificar la hora.
- **PowerShell**: Usar el cmdlet `Restore-AzSqlDatabase`.
- **CLI de Azure**: Usar el comando `az sql db restore`.

## Restauración de una Base de Datos Eliminada
- **Procedimiento**:
  - En el portal, ir a la página Información general del servidor de bases de datos.
  - En el área Operaciones, seleccionar "Bases de datos eliminadas".
  - Especificar cualquier momento hasta el momento de la eliminación y seleccionar "Aceptar".

## Restauraciones Geográficas
- **Procedimiento**:
  - Agregar una nueva base de datos a un servidor de Azure SQL Database.
  - Seleccionar "Copia de seguridad" en la lista desplegable "Seleccionar origen" y elegir la copia de seguridad desde la que restaurar.

---

# Ejercicio: Recuperación de Datos mediante la Restauración de una Instancia de Azure SQL Database

## Confirmación de Copias de Seguridad Activas
1. **Establecer Variable SQL Server**:
   ```powershell
   $sqlserver = Get-AzSqlServer
   ```

2. **Comprobar Copias de Seguridad Continuas**:
   ```powershell
   Get-AzSqlDatabaseRestorePoint `
       -ResourceGroupName learn-f5b52e38-cefb-4bbd-8bca-a6a4d0917a78 `
       -DatabaseName sql-erp-db `
       -ServerName $sqlserver.ServerName
   ```

## Eliminación de una Tabla de la Base de Datos
1. En Azure Portal, seleccionar "Todos los recursos", elegir `erpserver-NNNN`, seleccionar "Bases de datos SQL" y luego `sql-erp-db`.
2. Seleccionar "Editor de consultas (versión preliminar)" e iniciar sesión con `dbadmin`.
3. Ejecutar el siguiente comando para eliminar la tabla:
   ```sql
   DROP TABLE Person
   ```

4. Comprobar las tablas de la base de datos:
   ```sql
   SELECT schema_name(t.schema_id) as schema_name,
          t.name as table_name
   FROM sys.tables t
   ORDER BY schema_name, table_name;
   ```

## Restauración a un Momento Dado
1. En Azure Portal, seleccionar "Todos los recursos" y luego `sql-erp-db`.
2. Seleccionar "Restaurar" en la parte superior de la página Información general.
3. Completar la pestaña "Aspectos básicos" con estos valores:
   - **Selección del origen**: A un momento dado
   - **Nombre de la base de datos**: `sql-erp-db-xxxxx`
   - **Punto de restauración**: Seleccionar una hora hace 10 minutos
   - **Servidor**: `erpserver-xxxxx`
   - **¿Quiere usar un grupo elástico de SQL?**: No
   - **Proceso y almacenamiento**: Valor predeterminado
   - **Redundancia del almacenamiento de copia de seguridad**: Almacenamiento de copia de seguridad con redundancia local
4. Seleccionar "Crear". La restauración tardará varios minutos en completarse.

## Visualización de la Base de Datos Restaurada
1. En Azure Portal, seleccionar "Todos los recursos" y luego `sql-erp-db-restored`.
2. Seleccionar "Editor de consultas (versión preliminar)" e iniciar sesión con `dbadmin`.
3. Comprobar las tablas de la base de datos:
   ```sql
   SELECT schema_name(t.schema_id) as schema_name,
          t.name as table_name
   FROM sys.tables t
   ORDER BY schema_name, table_name;
   ```

4. Confirmar que la tabla contiene los datos:
   ```sql
   SELECT * FROM Person;
   ```

---

