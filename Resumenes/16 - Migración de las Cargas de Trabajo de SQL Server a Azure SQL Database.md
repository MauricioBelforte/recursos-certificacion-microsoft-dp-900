# 16) Migración de las Cargas de Trabajo de SQL Server a Azure SQL Database

---
# INFORMACION COMPLEMENTARIA: SQL Server como Servicio en Azure

## SQL Server por Sí Solo
SQL Server en sí mismo no es un servicio en la nube; es un sistema de gestión de bases de datos relacional (RDBMS) desarrollado por Microsoft. que puede instalarse y ejecutarse en servidores locales o virtuales.

## Opciones de Servicio en Azure

### IaaS (Infraestructura como Servicio)
- **SQL Server en Máquinas Virtuales de Azure**: Instalación de SQL Server en una máquina virtual de Azure. Esto te da control total sobre el sistema operativo y el SQL Server.

### PaaS (Plataforma como Servicio)
- **Azure SQL Database**: Un servicio gestionado que proporciona una base de datos SQL Server en la nube.
- **Azure SQL Managed Instance**: Ofrece una instancia completa de SQL Server con compatibilidad casi total con SQL Server local y todas las ventajas de PaaS.

### SaaS (Software como Servicio)
- Aunque SQL Server en sí no es SaaS, los servicios que lo utilizan, como Dynamics 365, sí lo son.

En resumen, SQL Server es una tecnología que puede ser utilizada en diversas configuraciones y servicios en la nube de Azure para adaptarse a diferentes necesidades empresariales.


---
## Objetivos de Aprendizaje
- **Explorar ventajas, funcionalidades y posibilidades de migración** que ofrece Azure SQL Database.
- **Migrar bases de datos** mediante la extensión Azure SQL Migration para Azure Data Studio y el seguimiento de las actividades de migración de bases de datos.
- **Usar la replicación transaccional** como método en línea para migrar a Azure SQL Database.
- **Explorar otros métodos** para migrar bases de datos de SQL Server a Azure SQL Database.

## Requisitos Previos
- Experiencia en la administración de bases de datos de SQL Server.
- Conocimiento de las versiones y ediciones de SQL Server.
- Conocimientos básicos de T-SQL.

---

# Migración de las Cargas de Trabajo de SQL Server a Azure SQL Database

En muchos casos, las empresas han estado usando SQL Server de forma local durante años, antes de que existieran opciones en la nube como Azure SQL Database. Esto les ha permitido tener control total sobre su infraestructura, personalizar su entorno según necesidades específicas y aprovechar inversiones previas en hardware y licencias. La transición a Azure SQL representa una modernización y una oportunidad de beneficiarse de las ventajas de la nube.

## Introducción
Azure SQL Database es un motor de base de datos PaaS que proporciona un entorno de desarrollo e implementación completo en la nube, adecuado para aplicaciones sencillas y empresariales avanzadas.

## Ventajas de Migración a SQL Database
- Modernización de aplicaciones aprovechando funcionalidades de PaaS.
- Eliminación de dependencias en componentes técnicos a nivel de instancia.
- Solución de bajo mantenimiento ideal para ciertas cargas de trabajo.

## Escenarios Adecuados para Azure SQL Database
- Simplificación de la implementación de bases de datos con uso intermitente e imprevisible.
- Nuevas bases de datos sin historial de uso donde el tamaño de proceso es difícil de estimar.
- Reducción de la complejidad en la implementación y el desarrollo.
- Requisitos de almacenamiento mayores a los ofrecidos por Azure SQL Managed Instance.

## Proceso de Migración
El proceso de migración de una base de datos de SQL Server en una máquina virtual de Azure a Azure SQL Database incluye:
1. Evaluación de bases de datos para la migración a Azure SQL.
2. Uso de herramientas de evaluación para detectar nuevas características en la plataforma de SQL Server de destino.

## Escenarios de Casos de Uso
Ejemplo: Una empresa de fabricación de bicicletas desea actualizar varios servidores de bases de datos heredados y beneficiarse de la escalabilidad y disponibilidad de Azure. Planea migrar las bases de datos de productos, existencia de piezas y recursos humanos a Azure SQL Database.

## Consideraciones Previas a la Migración
- Evaluar bases de datos para determinar la idoneidad de Azure SQL Database.
- Crear una instancia de base de datos de Azure SQL.
- Explorar métodos de migración sin conexión y en línea.

---

# Elección de la Característica de Azure SQL Database Adecuada

## Ventajas de Azure SQL Database
### Copia de Seguridad y Recuperación
- Copia de seguridad automática.
- Restauración a un momento dado.
- Retención a largo plazo hasta 10 años.

### Alta Disponibilidad
- Garantía del 99.99% de disponibilidad.
- Tres réplicas secundarias.
- Redundancia de zona con zonas de disponibilidad de Azure.

### Recuperación ante Desastres
- Restauración geográfica de copias de seguridad.
- Replicación geográfica activa.

### Escalabilidad del Servicio
- Escalado y reducción verticales dinámicos.
- Escalado horizontal con particiones.
- Grupos elásticos.

### Seguridad
- Autenticación de Microsoft Entra.
- Protección contra amenazas avanzada.
- Cifrado de datos transparente (TDE).
- Enmascaramiento de datos y Always Encrypted.
- Lista de permitidos del firewall.

### Licencias
- Modelo de compra de DTU para costos predictivos.
- Modelo de compra de núcleos virtuales con escalabilidad independiente.
- Ventaja híbrida de Azure para ahorro de costos.

## Características Exclusivas de Azure SQL Database
- **Hiperescala**: Proceso y almacenamiento escalables.
- **Escalado Automático**: Nivel sin servidor.
- **Ajuste Automático de Índices**: Creación y eliminación automática de índices.
- **Consulta Elástica**: Consultas entre varias bases de datos.
- **Trabajos Elásticos**: Reemplazo del Agente SQL Server.
- **SQL Data Sync**: Sincronización incremental de datos.
- **QPI (Información de Rendimiento de Consultas)**: Optimización de rendimiento de consultas.

## Opciones de Migración Admitidas
### Modos de Migración
- **En Línea**: Tiempo de inactividad mínimo.
- **Sin Conexión**: Tiempo de inactividad durante la migración.

### Herramientas
- **Azure Database Migration Service**: Offline.
- **Replicación Transaccional**: En línea.
- **Azure Migrate**: Offline.
- **SQL Data Sync**: Sin conexión.
- **Asistente de Importación y Exportación/BACPAC**: Offline.
- **Copia Masiva (BCP)**: Offline.
- **Azure Data Factory**: Offline.
- **Data Migration Assistant (DMA)**: Offline.

## Rendimiento de la Migración
- Supervisar E/S y latencia de archivos.
- Escalar verticalmente a núcleos Gen5 8 Crítico para la Empresa o usar Hiperescala.
- Asegurar ancho de banda de red adecuado.
- Elige nivel de servicio y tamaño de proceso altos para máximo rendimiento.
- Minimizar distancia entre archivos BACPAC y centro de datos.
- Deshabilitar actualización automática y creación de estadísticas durante migración.
- Migrar datos históricos a base de datos independiente y usar consultas elásticas.

## Reintento de Conexiones de Aplicación
- Implementar reintentos para errores transitorios.
- Esperar 5 segundos en el primer reintento, aumentar exponencialmente hasta 60 segundos.
- Reintentar SELECT en nueva conexión.

---

# Uso de la Extensión de Migración de Azure SQL para Migrar a Azure SQL Database

## Escenario
La base de datos de recursos humanos es crítica para la empresa pero se usa muy poco durante los fines de semana. Se ha previsto una migración sin conexión durante el fin de semana.

## Herramienta: Extensión de Migración de Azure SQL para Azure Data Studio
- **Propósito**: Ayuda a preparar y migrar bases de datos de SQL Server a Azure.
- **Capacidades**: Evalúa la preparación para la migración, recomienda recursos de Azure y facilita el proceso de migración.

## Proceso de Migración
### Configuración
1. Instalar la extensión de migración de Azure SQL en Azure Data Studio.
2. Iniciar el asistente para migrar a Azure SQL.

### Paso 1: Bases de Datos para Evaluación
- Elegir las bases de datos para migrar.

### Paso 2: Resultados y Recomendaciones de la Evaluación
- Evaluar la preparación para la migración.
- Recopilar datos de rendimiento de la base de datos actual.
- Proporcionar recomendaciones para la configuración de Azure SQL.

### Paso 3: Destino de Azure
- Seleccionar una cuenta de Azure y el destino de Azure SQL Database.

### Paso 4: Azure Database Migration Service
- Seleccionar una instancia de Azure Database Migration Service existente o crear una nueva.

### Paso 5: Configuración del Origen de Datos
- Escribir las credenciales para conectarse al origen.
- Seleccionar las tablas a migrar (asegúrese de que el esquema se haya creado en el destino).

### Paso 6: Resumen
- Revisar la información de migración e iniciar el proceso.

## Estado de Migración
- **Preparación para la copia**: Deshabilitar estadísticas automáticas, desencadenadores e índices.
- **Copiando**: Copia de datos en curso.
- **Copia Finalizada**: Esperando que otras tablas terminen de copiarse.
- **Regenerando Índices**: Regeneración de índices en las tablas de destino.
- **Correcto**: Todos los datos copiados y los índices regenerados.

## Consideraciones de Rendimiento
- Escalar verticalmente los recursos de Azure SQL Database antes de la migración.
- Asegurar que el entorno de ejecución de integración autohospedado pueda manejar la carga.
- Limitar el número de migraciones simultáneas a 10 por entorno de ejecución autohospedado.

## Supervisión de la Migración
### Desde Azure Data Studio
- Supervisar el progreso en la extensión de migración de Azure para Azure Data Studio.
- Ver migraciones en curso, completadas y con errores.

### Desde Azure Portal
- Supervisar la actividad mediante Azure Database Migration Service.
- Validar la base de datos de destino después de la migración.

## Migrar a Escala
### Ejemplo: Migración de Base de Datos con PowerShell
```powershell
$sourcePass = ConvertTo-SecureString "password" -AsPlainText -Force
$targetPass = ConvertTo-SecureString "password" -AsPlainText -Force

New-AzDataMigrationToSqlDb `
-ResourceGroupName MyGroup `
-SqlDbInstanceName myserver `
-Kind "SqlDb" `
-TargetDbName AdventureWorks `
-SourceDatabaseName AdventureWorks `
-SourceSqlConnectionAuthentication SQLAuthentication `
-SourceSqlConnectionDataSource myserver.microsoft.com `
-SourceSqlConnectionUserName user `
-SourceSqlConnectionPassword $sourcePass `
-Scope "/subscriptions/MySubscriptionID/resourceGroups/MyGroup/providers/Microsoft.Sql/servers/myserver" `
-TargetSqlConnectionAuthentication SQLAuthentication `
-TargetSqlConnectionDataSource myserver.database.windows.net `
-TargetSqlConnectionUserName user `
-TargetSqlConnectionPassword $targetPass `
-MigrationService "/subscriptions/MySubscriptionID/resourceGroups/MyGroup/providers/Microsoft.DataMigration/SqlMigrationServices/MyService"
```


---

# Uso de la Extensión de Migración de Azure SQL para Migrar a Azure SQL Database

## Escenario
Migración sin conexión durante el fin de semana para la base de datos de recursos humanos.

## Herramientas
### Extensión de Migración de Azure SQL para Azure Data Studio
- **Preparación para la Migración**: Evalúa la preparación y recomienda los mejores recursos de Azure.
- **Migración de Bases de Datos**: Sin costo adicional para múltiples bases de datos.

## Proceso de Migración
1. **Configuración**: Instalar la extensión de migración en Azure Data Studio e iniciar el asistente de migración.
2. **Selección de Bases de Datos**: Elegir las bases de datos a migrar.
3. **Resultados y Recomendaciones**: Evaluar la preparación y recopilar datos de rendimiento.
4. **Destino de Azure**: Seleccionar cuenta de Azure y destino de Azure SQL Database.
5. **Azure Database Migration Service**: Seleccionar o crear una instancia de DMS.
6. **Configuración del Origen de Datos**: Proveer credenciales y seleccionar tablas a migrar.
7. **Resumen**: Revisar e iniciar el proceso de migración.

## Estado de Migración
- **Preparación para la copia**: Deshabilita estadísticas, desencadenadores e índices.
- **Copiando**: Transferencia de datos del origen al destino.
- **Copia finalizada**: Espera a que otras tablas terminen de copiarse.
- **Regenerando índices**: Regeneración de índices en tablas de destino.
- **Correcto**: Datos copiados e índices regenerados.

## Consideraciones de Rendimiento
- Escalar verticalmente los recursos de proceso antes de la migración.
- Asegurar que el host de entorno de ejecución puede manejar la carga.
- Limitar a 10 migraciones simultáneas por entorno de ejecución.

## Supervisión de la Migración
- **Azure Data Studio**: Seguimiento del progreso en tiempo real.
- **Azure Portal**: Supervisión mediante Azure Database Migration Service.

## Migración a Escala
### PowerShell
Migrar base de datos:
```powershell
$sourcePass = ConvertTo-SecureString "password" -AsPlainText -Force
$targetPass = ConvertTo-SecureString "password" -AsPlainText -Force
New-AzDataMigrationToSqlDb `
-ResourceGroupName MyGroup `
-SqlDbInstanceName myserver `
-Kind "SqlDb" `
-TargetDbName AdventureWorks `
-SourceDatabaseName AdventureWorks `
-SourceSqlConnectionAuthentication SQLAuthentication `
-SourceSqlConnectionDataSource myserver.microsoft.com `
-SourceSqlConnectionUserName user `
-SourceSqlConnectionPassword $sourcePass `
-Scope "/subscriptions/MySubscriptionID/resourceGroups/MyGroup/providers/Microsoft.Sql/servers/myserver" `
-TargetSqlConnectionAuthentication SQLAuthentication `
-TargetSqlConnectionDataSource myserver.database.windows.net `
-TargetSqlConnectionUserName user `
-TargetSqlConnectionPassword $targetPass `
-MigrationService "/subscriptions/MySubscriptionID/resourceGroups/MyGroup/providers/Microsoft.DataMigration/SqlMigrationServices/MyService"
```

Migrar subconjunto de tablas:
```powershell
New-AzDataMigrationToSqlDb `
-ResourceGroupName MyGroup `
-SqlDbInstanceName myserver `
-Kind "SqlDb" `
-TargetDbName AdventureWorks `
-SourceDatabaseName AdventureWorks `
-SourceSqlConnectionAuthentication SQLAuthentication `
-SourceSqlConnectionDataSource myserver.microsoft.com `
-SourceSqlConnectionUserName user `
-SourceSqlConnectionPassword $sourcePass `
-Scope "/subscriptions/MySubscriptionID/resourceGroups/MyGroup/providers/Microsoft.Sql/servers/myserver" `
-TargetSqlConnectionAuthentication SQLAuthentication `
-TargetSqlConnectionDataSource myserver.database.windows.net `
-TargetSqlConnectionUserName user `
-TargetSqlConnectionPassword $targetPass `
-TableList "[Person].[Person]", "[Person].[EmailAddress]" `
-MigrationService "/subscriptions/MySubscriptionID/resourceGroups/MyGroup/providers/Microsoft.DataMigration/SqlMigrationServices/MyService"
```

---

# Exploración de Data Migration Assistant para Migrar a Azure SQL Database

## Tipos de Migración
1. **Esquema y datos**: Migrar estructura y datos.
2. **Solo esquema**: Migrar solo estructura.
3. **Solo datos**: Migrar solo datos, esquema ya existente.

## Evaluación
- Evaluar bases de datos en busca de problemas de compatibilidad con Data Migration Assistant.
- Revisar el informe de compatibilidad y aplicar correcciones.

## Proceso de Migración
1. **Nuevo Proyecto**: Crear proyecto de migración, seleccionar origen (SQL Server) y destino (Azure SQL Database).
2. **Conectar a Origen**: Escribir nombre y autenticación de la instancia de SQL Server de origen.
3. **Seleccionar Base de Datos**: Elegir base de datos a migrar.
4. **Conectar a Destino**: Escribir nombre y autenticación de la instancia de SQL Server de destino.
5. **Seleccionar Objetos**: Elegir objetos de esquema a migrar.
6. **Generar Script SQL**: Revisar y aplicar correcciones.
7. **Implementar Esquema**: Implementar esquema y migrar datos.

## Supervisión de la Migración
- Monitorear progreso de la migración en Data Migration Assistant.
- Ajustar valores de configuración en dma.exe.config para mejorar el rendimiento.

## Procedimientos Recomendados
- Evitar instalar y ejecutar Data Migration Assistant en la máquina host de SQL Server.
- Proporcionar una ubicación compartida accesible para servidores de origen y destino.
- Habilitar conexiones cifradas.
- Comprobar restricciones no confiables en bases de datos de origen y destino.

---

# Migración a Azure SQL Database con BACPAC

## Archivo BACPAC
- Archivo comprimido que contiene metadatos y datos de la base de datos.
- Datos pueden importarse desde Azure Blob Storage o almacenamiento local.

## Utilidad SQLPackage
- Recomendado para entornos de producción para escalabilidad y rendimiento óptimos.
- Ejecutar comandos SqlPackage en paralelo para subconjuntos de tablas acelera la importación/exportación.

## Importación de un Archivo BACPAC en Azure Portal
1. Abrir la página del servidor de bases de datos en Azure Portal.
2. Seleccionar "Importar base de datos" en la barra de herramientas.
3. Seleccionar la cuenta de almacenamiento y el contenedor del archivo BACPAC.
4. Especificar el tamaño de la nueva base de datos y proporcionar credenciales de SQL Server de destino.
5. Supervisar el progreso en la sección "Historial de importación y exportación".

## Uso de SqlPackage
- Comando de ejemplo para importar la base de datos AdventureWorks2019:
```bash
SqlPackage.exe /a:import /tcs:"Data Source=<server-name>.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=<your_server_admin_account_user_id>;Password=<your_server_admin_account_password>" /sf:AdventureWorks2019.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

## Sugerencia
- Escalar la base de datos a un nivel de servicio y tamaño de proceso más altos para aumentar la velocidad de importación.
- Reducir verticalmente después de completar la importación.

---
# Uso de un Método en Línea para Migrar a Azure SQL Database

## Replicación Transaccional
- **Definición**: Manera de mover datos entre servidores de bases de datos conectados continuamente.
- **Proceso**: Comienza con una instantánea de la base de datos y replica cambios casi en tiempo real.

## Componentes Clave
- **Publicador**: Origen de los datos.
- **Suscriptor**: Destino de los datos.
- **Distribuidor**: Recopila y distribuye cambios.
- **Artículo**: Objeto de base de datos incluido en la publicación.
- **Publicación**: Conjunto de artículos replicados.
- **Suscripción**: Solicitud de un suscriptor para una publicación.

## Configuración de Replicación Transaccional
1. **Crear Distribuidor**: Configura la base de datos del distribuidor y los publicadores.
```sql
USE [master]
GO
EXEC sp_adddistributor @distributor = N'CONTOSO-SRV', @password = N''
GO
EXEC sp_adddistributiondb @database = N'distribution', @data_folder = N'C:\...\Data', @log_folder = N'C:\...\Data'
GO
-- Adding the distribution publishers
exec sp_adddistpublisher @publisher = N'CONTOSO-SRV', @distribution_db = N'distribution'
GO
-- Enabling the replication database
use master
exec sp_replicationdboption @dbname = N'AdventureWorks', @optname = N'publish', @value = N'true'
GO
-- Adds a Log Reader agent
exec [AdventureWorks].sys.sp_addlogreader_agent @publisher_security_mode = 1
GO
```

2. **Crear Publicación Transaccional**: Publica la base de datos de origen.
```sql
USE [AdventureWorks]
GO
EXEC sp_addpublication @publication = N'REPL-AdventureWorks', @description = N'Transactional publication of AdventureWorks', @sync_method = N'concurrent'
GO
exec sp_addpublication_snapshot @publication = N'REPL-AdventureWorks', @frequency_type = 1, @alt_snapshot_folder = N'C:\REPL'
GO
```

3. **Crear Artículo para Publicación**: Define qué datos replicar.
```sql
USE [AdventureWorks]
GO
EXEC sp_addarticle @publication = N'REPL-AdventureWorks', @article = N'Person', @source_owner = N'Person', @source_object = N'Person'
GO
```

4. **Crear Suscripción y Agente de Suscripción**: Configura el suscriptor y el agente.
```sql
USE [AdventureWorks]
GO
EXEC sp_addsubscription @publication = N'REPL-AdventureWorks', @subscriber = N'contoso.database.windows.net', @destination_db = N'my-db'
GO
exec sp_addpushsubscription_agent @publication = N'REPL-AdventureWorks', @subscriber = N'contoso.database.windows.net', @subscriber_db = N'my-db'
GO
```

## Inicio y Supervisión de la Replicación

- Iniciar el trabajo de instantánea, el lector de registros y el distribuidor desde SQL Server.
- Supervisar el agente de instantáneas y el agente de registro del LOG haciendo clic derecho en la publicación y seleccionando la opción adecuada. 
- Iniciar los agentes si no están en ejecución.

### Ver Estado de Sincronización
- Hacer clic derecho en la suscripción, seleccionar "Ver estado de sincronización" y luego iniciar el agente.
- Si encuentra mensajes de error, comprobar el historial de trabajos del agente en el Agente SQL Server.
- Una vez que los agentes se ejecuten como previsto, debería ver:
  - Estado del agente de instantáneas.
  - Estado del lector del LOG.
  - Estado de sincronización.

### Completar la Migración
- Una vez que los datos se replican completamente en Azure SQL Database, dirigir las conexiones a la base de datos del suscriptor.
- Detener y quitar la replicación.

---

# Traslado a Azure SQL Database

## Migración Parcial de Datos
### Escenario
La empresa de bicicletas quiere migrar tablas de clientes y productos a Azure SQL Database, manteniendo los datos de ventas localmente.

### Métodos de Migración

#### SQL Data Sync
- **Funcionalidad**: Sincronización incremental de datos en varias bases de datos en Azure SQL Database o SQL Server locales.
- **Ventaja**: Ideal para aplicaciones híbridas y permite una rápida transición a la nube.
- **Topología**: Basada en un modelo de concentrador con una base de datos central.
- **Desventaja**: Mayor impacto en el rendimiento comparado con la replicación transaccional.
- **Configuración**: Requiere especificar una base de datos para almacenar metadatos y definir propiedades de sincronización.

#### Copia Masiva (bcp)
- **Funcionalidad**: Exportación e importación masiva de datos entre SQL Server y otros programas o bases de datos.
- **Requisitos**: Conocer el esquema y tipos de datos de las tablas, a menos que se use un archivo de formato preexistente.

#### Azure Data Factory
- **Funcionalidad**: Migración y transformación de datos de bases de datos de SQL Server de origen.
- **Uso**: Normalmente utilizado para cargas de trabajo de inteligencia empresarial (BI).

---
