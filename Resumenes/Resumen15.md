# 15) REPASAR Implementación de Soluciones PaaS con Azure SQL

## Objetivos de Aprendizaje
Después de completar este módulo, podrás:
- Tener más conocimientos sobre **SQL Server** en una oferta de **plataforma como servicio (PaaS)**
- Comprender las opciones de **implementación y aprovisionamiento** de PaaS
- Comprender los **grupos elásticos**
- Examinar **Azure SQL Managed Instance**
- Explorar **Azure SQL Edge**
- Configurar una plantilla para la implementación de **PaaS**

## Conceptos Clave

### 1. SQL Server en PaaS
- **Azure SQL Database**: Base de datos relacional totalmente gestionada (OLTP).
- **Azure SQL Managed Instance**: PaaS con compatibilidad total con SQL Server (OLTP).

### 2. Implementación y Aprovisionamiento de PaaS
- **Modelos de Servicio**: Base de datos única, grupo elástico, instancias administradas.
- **Opciones de Escalabilidad**: Vertical y horizontal.

### 3. Grupos Elásticos
- **Descripción**: Compartir recursos entre varias bases de datos.
- **Usos**: Ideal para aplicaciones SaaS con múltiples inquilinos.

### 4. Azure SQL Managed Instance
- **Características**: Alta compatibilidad con SQL Server.
- **Beneficios**: Migraciones sin cambios significativos en el código.

### 5. Azure SQL Edge
- **Descripción**: Versión optimizada para IoT y edge computing.
- **Usos**: Escenarios de baja latencia y entornos restringidos.

### 6. Plantillas para la Implementación de PaaS
- **ARM Templates**: Automatización y gestión de recursos en Azure.
- **Beneficios**: Automación, consistencia, repetibilidad.

---

# Explorar una Única Base de Datos SQL

## Implementación mediante el Portal
El proceso para crear una base de datos singleton en Azure SQL Database mediante el portal es sencillo:
1. Selecciona "bases de datos SQL" en el menú.
2. Haz clic en "Crear" y proporciona la siguiente información:
   - Grupo de recursos
   - Nombre de la base de datos
   - Servidor lógico
   - Uso de grupo elástico (opcional)
   - Recursos de proceso y almacenamiento

## Implementación mediante PowerShell o CLI
Puedes implementar la base de datos mediante PowerShell o la CLI de Azure. Aquí un ejemplo de comandos PowerShell:

```powershell
# Connect-AzAccount
$SubscriptionId = ''
$resourceGroupName = "myResourceGroup-$(Get-Random)"
$location = "westus2"
$adminSqlLogin = "SqlAdmin"
$password = "ChangeYourAdminPassword1"
$serverName = "server-$(Get-Random)"
$databaseName = "mySampleDatabase"
$startIp = "0.0.0.0"
$endIp = "0.0.0.0"
Set-AzContext -SubscriptionId $subscriptionId
$resourceGroup = New-AzResourceGroup -Name $resourceGroupName -Location $location
$server = New-AzSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminSqlLogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
$serverFirewallRule = New-AzSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "AllowedIPs" -StartIpAddress $startIp -EndIpAddress $endIp
$database = New-AzSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -RequestedServiceObjectiveName "S0" -SampleName "AdventureWorksLT"
```

También se puede usar la CLI de Azure para implementar Azure SQL Database. Aquí un ejemplo:

```bash
#!/bin/bash
# set execution context (if necessary)
az account set --subscription <replace with your subscription name or id>

# Set the resource group name and location for your server
resourceGroupName=myResourceGroup-$RANDOM
location=westus2

# Set an admin login and password for your database
adminlogin=ServerAdmin
password=`openssl rand -base64 16`
# password=<EnterYourComplexPasswordHere1>

# The logical server name has to be unique in all of Azure
servername=server-$RANDOM

# The ip address range that you want to allow to access your DB
startip=0.0.0.0
endip=0.0.0.0

# Create a resource group
az group create \
  --name $resourceGroupName \
  --location $location

# Create a logical server in the resource group
az sql server create \
  --name $servername \
  --resource-group $resourceGroupName \
  --location $location \
  --admin-user $adminlogin \
  --admin-password $password

# Configure a firewall rule for the server
az sql server firewall-rule create \
  --resource-group $resourceGroupName \
  --server $servername \
  -n AllowYourIp \
  --start-ip-address $startip \
  --end-ip-address $endip

# Create a database in the server
az sql db create \
  --resource-group $resourceGroupName \
  --server $servername \
  --name mySampleDatabase \
  --sample-name AdventureWorksLT \
  --edition GeneralPurpose \
  --family Gen4 \
  --capacity 1

# Echo random password
echo $password
```

## Implementación con Plantillas de Azure Resource Manager
Las plantillas de Azure Resource Manager ofrecen control detallado sobre los recursos. Un ejemplo de PowerShell para implementar una plantilla basada en GitHub es:

```powershell
$projectName = Read-Host -Prompt "Enter a project name"
$location = Read-Host -Prompt "Enter an Azure location (i.e. centralus)"
$adminUser = Read-Host -Prompt "Enter the SQL server administrator username"
$adminPassword = Read-Host -Prompt "Enter the SQL server administrator password" -AsSecureString
$resourceGroupName = "${projectName}rg"
New-AzResourceGroup -Name $resourceGroupName -Location $location
New-AzResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateUri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-sql-logical-server/azuredeploy.json" -administratorLogin $adminUser -administratorLoginPassword $adminPassword
```

---

# Implementación de un Grupo Elástico de Azure SQL Database

## Descripción
Los **grupos elásticos** permiten comprar recursos de proceso de Azure (CPU, memoria, almacenamiento) y compartirlos entre varias bases de datos en el mismo grupo. Administrar recursos de grupo elástico ahorra costos y facilita la escalabilidad.

## Creación de Nuevos Grupos Elásticos
1. En Azure Portal, hacer clic en "Crear un recurso".
2. Buscar "Grupo de bases de datos elásticas SQL".
3. Hacer clic en "Crear" y seguir las instrucciones para configurar el grupo.

## Adición de una Base de Datos a un Grupo Existente
1. En Azure Portal, buscar el grupo al que se quiere agregar la base de datos.
2. Seleccionar las bases de datos a agregar.
3. Hacer clic en "Aplicar" para agregar la base de datos al grupo elástico.

## Administración de Recursos del Grupo
En Azure Portal, se puede:
- Ver el uso de los recursos y qué base de datos consume más recursos.
- Ajustar el tamaño del grupo, incluyendo DTU, núcleos virtuales y tamaño de almacenamiento.
- Configurar el nivel de servicio.
- Administrar los recursos por base de datos, agregándolas o quitándolas del grupo.

## Ventajas de los Grupos Elásticos
- Supervisar el uso de recursos de base de datos.
- Facilitar el escalado horizontal o vertical del grupo.
- Balancear la carga de trabajo para evitar que una base de datos monopolice los recursos del grupo.

Un grupo elástico es ideal para bases de datos de varios inquilinos, donde cada inquilino tiene su propia copia de la base de datos, ayudando a equilibrar la carga de trabajo y optimizar recursos.

---

# Descripción de Hiperescala de Base de Datos SQL

## Azure SQL Database Hiperescala
- Permite bases de datos de 100 TB o más.
- Técnicas de escalado horizontal para agregar nodos de proceso según el tamaño de los datos.
- Costos similares a Azure SQL Database, pero con un costo por terabyte de almacenamiento.
- Una vez convertida a Hiperescala, no puede volver a ser una base de datos regular.

## Ventajas de Hiperescala
- Elimina los límites prácticos tradicionales de bases de datos en la nube.
- Crecimiento de almacenamiento según sea necesario sin un tamaño máximo definido.
- Escalabilidad horizontal para cargas de trabajo de lectura intensiva.
- Creación de copias de seguridad instantáneas.
- Escalabilidad vertical y horizontal rápida.
- Restauraciones rápidas de base de datos.

## Escalabilidad
### Vertical
- Escalar verticalmente recursos como CPU y memoria y reducir verticalmente en tiempo constante.
### Horizontal
- Provisión de réplicas de proceso para atender solicitudes de lectura y descargar la carga del proceso principal.
- Réplicas de solo lectura también funcionan como servidores en espera activa.

## Arquitectura de Hiperescala
- Separa el motor de procesamiento de consultas de los componentes de almacenamiento a largo plazo.
- Capacidad de almacenamiento escalable fácilmente hasta 100 TB o más.
- Escalabilidad rápida de los recursos de proceso.

## Consideraciones sobre la Seguridad
- **Seguridad de Red**: Reglas de firewall de IP y firewall de red virtual.
- **Administración de Acceso**:
  - Autenticación de SQL
  - Autenticación de Microsoft Entra
  - Autenticación de Windows para entidades de seguridad de Microsoft Entra (versión preliminar)
- **Seguridad de Nivel de Fila**: Control de acceso a filas de una tabla de base de datos.
- **Protección contra Amenazas**:
  - Auditoría de actividades de base de datos.
  - Protección avanzada contra amenazas con alertas de actividades sospechosas.
- **Information Protection**:
  - Seguridad de la capa de transporte (cifrado en tránsito)
  - Cifrado de datos transparente (cifrado en reposo)
  - Administración de claves con Azure Key Vault
  - Always Encrypted (cifrado en uso)
  - Enmascaramiento de datos dinámicos

## Consideraciones de Rendimiento
- **Orientado a Clientes con Grandes Bases de Datos**: Para modernizar aplicaciones mediante su traslado a la nube.
- **Funciones de Rendimiento**:
  - Copias de seguridad casi instantáneas basadas en instantáneas de archivos en Azure Blob Storage.
  - Restauraciones rápidas de bases de datos en minutos.
  - Mayor rendimiento general con tiempos más rápidos de confirmación de transacciones.
  - Escalado horizontal rápido con réplicas de solo lectura.
  - Escalado vertical rápido de recursos de proceso.

## Implementación de la Hiperescala de Azure SQL Database
1. Vaya a la página "Seleccione una opción de implementación de SQL".
2. En "Bases de datos SQL", deje Tipo de recurso en "Base de datos única" y seleccione "Crear".
3. Complete los campos en la pestaña "Aspectos básicos".
4. Seleccione "Crear nuevo" para el Servidor y complete la información del servidor.
5. En "Proceso y almacenamiento", seleccione "Configurar base de datos".
6. En "Nivel de servicio", seleccione "Hiperescala".
7. En "Configuración de hardware", seleccione la configuración adecuada, por ejemplo, Gen5.
8. Ajuste el control deslizante "Núcleos virtuales" si es necesario y seleccione "Aplicar".
9. Configure "Redes" y "Seguridad" según sea necesario.
10. En la pestaña "Revisar y crear", seleccione "Crear".

---

# Examinar Azure SQL Managed Instance

## Descripción
Azure SQL Managed Instance es una instancia de SQL Server totalmente funcional y casi 100 % compatible con el ecosistema local. Incluye características como Agente SQL, tempdb, consulta entre bases de datos y Common Language Runtime (CLR). Utiliza la infraestructura de Azure SQL Database y ofrece ventajas de PaaS como copias de seguridad automáticas, revisiones automáticas y alta disponibilidad integrada.

## Características de Azure SQL Managed Instance
- Permite restauraciones desde copias de seguridad locales.
- Hasta 100 bases de datos y acceso a bases de datos del sistema.
- Incluye consultas entre bases de datos y CLR.
- Permite el uso del Agente SQL.

## Opciones
### Niveles de Servicio
- **Crítico para la empresa**: Incluye OLTP en memoria y una instancia secundaria legible.
- **De uso general**: No incluye OLTP en memoria ni instancia secundaria legible.

### Característica de Vinculación (Versión Preliminar)
- Funcionalidad híbrida de replicación de bases de datos de instancias de SQL Server a Azure SQL Managed Instance.
- Replica los datos mediante grupos de disponibilidad distribuidos.
- Solución de recuperación ante desastres híbrida y base de datos secundaria de solo lectura.

### Grupo de Instancias (Versión Preliminar)
- Permite migrar pequeñas instancias de SQL Server a la nube.
- Provisión rápida de recursos en función de requisitos y recursos de migración totales.
- Tiempo de implementación rápido de hasta cinco minutos.

## Alta Disponibilidad
- SLA del 99.99 %.
- Replicación de almacenamiento para la disponibilidad (nivel De uso general) o varias réplicas (nivel Crítico para la empresa).

## Copias de Seguridad
- Copias de seguridad automáticas configuradas automáticamente.
- Permite realizar manualmente una copia de seguridad de solo copia de una base de datos.
- Retención a largo plazo (LTR) hasta 10 años en almacenamiento de blobs de Azure con redundancia geográfica.
- Horarios de copias de seguridad:
  - Completa: una vez a la semana.
  - Diferencial: cada 12 horas.
  - Registro de transacciones: cada 5-10 minutos.

## Recuperación ante Desastres
- Grupos de conmutación por error automática para recuperación ante desastres.
- Replica asincrónicamente los datos en una instancia secundaria en la región de Azure emparejada.
- Puntos de conexión de lectura y escritura y de solo lectura.

---

# Describir SQL Edge

## Descripción
Azure SQL Edge es un motor de base de datos relacional optimizado para cargas de trabajo de IoT. Ofrece funcionalidades para transmitir, procesar y analizar datos relacionales y no relacionales, como JSON, grafos y datos de serie temporal. Se basa en la versión más reciente del Motor de base de datos de SQL Server.

## Ventajas
- **Sintaxis y Herramientas de T-SQL Conocidas**: Los desarrolladores pueden usar Azure Portal, SQL Server Management Studio, Azure Data Studio, Visual Studio Code y SQL Server Data Tools en Visual Studio.
- **Portabilidad**: Versión en contenedor del Motor de base de datos de SQL Server optimizada para IoT. Compatible con Windows y Linux.
- **Compatibilidad con Varios Estados de Conexión y Sincronización de Datos**: Admite escenarios conectados, desconectados e híbridos semiconectados. Sincronización de datos incrementales con Azure SQL Data Sync.

## Streaming de Datos Integrado y Aprendizaje Automático
- **Streaming de Datos**: Compatible con la transmisión de datos hacia y desde varias entradas y salidas. Utiliza la tecnología de Azure Stream Analytics.
- **Aprendizaje Automático**: Admite la inferencia de aprendizaje automático y la instrucción PREDICT.

## Consideraciones sobre la Seguridad
- **Controles de Cifrado y Acceso de Datos**: Cifrado de datos transparente (TDE), seguridad de nivel de fila y enmascaramiento dinámico de datos.
- **Seguridad en el Transporte de Red**: Usa TLS y certificados para cifrar toda la comunicación.
- **Microsoft Defender para IoT**: Solución de seguridad centralizada para detectar y identificar dispositivos IoT, vulnerabilidades y amenazas.

## Implementación de Azure SQL Edge desde el Azure Marketplace
1. Tener un IoT Hub aprovisionado con al menos un dispositivo IoT Edge.
2. Buscar el módulo Azure SQL Edge en el Azure Marketplace y seleccionar "Obtener ahora".
3. Seleccionar la SKU de plan de software deseada y continuar.
4. Especificar el nombre del dispositivo IoT Edge y crear el módulo.
5. En la hoja "Establecer módulos en el dispositivo", elegir "AzureSQLEdge" en Módulos de IoT Edge.
6. Configurar la contraseña de la cuenta de administrador de SQL Edge y otras opciones de configuración.
7. Configurar el enrutamiento de mensajes para el módulo.
8. Revisar y crear el módulo. La lista de módulos notificados del dispositivo mostrará AzureSQLEdge en estado de ejecución.

---

