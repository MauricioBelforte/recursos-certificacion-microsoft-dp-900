# 4) Exploración de los Servicios de Bases de Datos Relacionales en Azure

## Servicios específicos de Azure SQL

### A. SQL Server en máquina virtual de Azure (VM)
Imagina que tienes un servidor físico con **SQL Server** en tu oficina. Ahora, con **Azure**, puedes "mover" ese servidor a una máquina virtual en la nube. Aquí te dejo los puntos clave:
1. **Máquina virtual (VM)**: Es como un ordenador dentro de otro ordenador, pero en la nube. Se ejecuta en Azure.
2. **SQL Server**: Es el software de base de datos que instalas en esa máquina virtual.
3. **Infraestructura como servicio (IaaS)**: En lugar de tener y gestionar servidores físicos, usas máquinas virtuales en la nube. Azure se encarga del hardware.
4. **Lift-and-shift**: Significa mover tus aplicaciones y datos tal cual están desde tus servidores locales a la nube, sin necesidad de hacer grandes cambios.

Esta opción es genial para cuando quieres mover tus bases de datos de SQL Server a la nube de manera rápida y sencilla, aprovechando las ventajas de la infraestructura de Azure.

---

### B. Azure SQL Managed Instance
Imagina que tienes un servidor de base de datos **SQL Server** en tu oficina. Azure SQL Managed Instance es una opción en la nube que es muy similar a tener ese servidor, pero sin tener que preocuparte por el hardware y el sistema operativo.
1. **PaaS**: Plataforma como servicio, lo que significa que muchas tareas de mantenimiento están automatizadas.
2. **Compatibilidad**: Casi completa con instancias locales de SQL Server.
3. **Automatización**: Actualizaciones de software, copias de seguridad y otras tareas de mantenimiento se manejan automáticamente.

Esta opción reduce la carga de administración y hace que sea más fácil mantener tu servidor de bases de datos.

Si su sistema usa características como servidores vinculados, **Service Broker** (un sistema de procesamiento de mensajes que se puede usar para distribuir el trabajo entre servidores) o **Correo electrónico** de base de datos (que permite a la base de datos enviar mensajes de correo electrónico a los usuarios), debe usar la opción Instancia administrada.

---

### C. Azure SQL Database
Azure SQL Database es una base de datos completamente gestionada y diseñada específicamente para la nube.
1. **PaaS**: Totalmente gestionada, por lo que no tienes que preocuparte por el hardware.
2. **Escalable**: Puede crecer con tus necesidades, perfecto para aplicaciones en la nube.
3. **Funciones**: Incluye las principales capacidades de SQL Server, así que es como tener SQL Server en la nube.

Es ideal para cuando quieres crear una nueva aplicación en la nube de manera rápida y eficiente.

Azure SQL Database está disponible como una base de datos única o un grupo elástico.

---

### D. Azure SQL Edge
Azure SQL Edge es un motor SQL diseñado para escenarios de **Internet de las Cosas (IoT)**.
1. **Optimizado para IoT**: Perfecto para trabajar con datos de serie temporal de streaming.
2. **Escenarios IoT**: Ideal para dispositivos y aplicaciones que recopilan y analizan datos en tiempo real.

Permite manejar datos en dispositivos IoT de manera eficiente y efectiva.

---
# Descripción de los Servicios y las Capacidades de Azure SQL

**Azure SQL** es un término colectivo para referirse a una familia de servicios de base de datos basados en Microsoft SQL Server en Azure. Los servicios específicos de Azure SQL incluyen:

## 1. SQL Server en Máquina Virtual de Azure (VM)
- **Descripción**: Máquina virtual en Azure con una instalación de SQL Server.
- **Tipo**: IaaS (Infraestructura como Servicio).
- **Uso Ideal**: Migración **lift-and-shift** de instalaciones locales de SQL Server a la nube.

## 2. Azure SQL Managed Instance
- **Descripción**: Opción de PaaS (Plataforma como Servicio) con compatibilidad casi completa con instancias locales de SQL Server.
- **Características**: Administración automatizada de actualizaciones, copias de seguridad y mantenimiento.
- **Beneficio**: Reducción de la carga administrativa.

## 3. Azure SQL Database
- **Descripción**: Servicio de base de datos PaaS totalmente administrado y altamente escalable diseñado para la nube.
- **Características**: Incluye las principales capacidades de SQL Server local.
- **Uso Ideal**: Creación de aplicaciones en la nube.

## 4. Azure SQL Edge
- **Descripción**: Motor SQL optimizado para escenarios de Internet de las Cosas (IoT) con datos de serie temporal de streaming.
- **Nota**: Nos centraremos en las otras opciones para escenarios de bases de datos relacionales más generales.

---
# Comparación de los Servicios de Azure SQL

## SQL Server en Máquina Virtual de Azure (VM)
- **Tipo de Servicio en la Nube**: IaaS (Infraestructura como Servicio)
- **Compatibilidad con SQL Server**: Totalmente compatible con instalaciones físicas y virtualizadas locales. Migración lift-and-shift sin cambios.
- **Arquitectura**: Instancias de SQL Server en una máquina virtual. Cada instancia puede admitir varias bases de datos.
- **Disponibilidad**: 99.99%
- **Administración**: Debe administrar el sistema operativo, SQL Server, configuración, copias de seguridad y mantenimiento.
- **Casos de Uso**: Migración o ampliación de soluciones de SQL Server local con control total sobre la configuración.

---

## Azure SQL Managed Instance
- **Tipo de Servicio en la Nube**: PaaS (Plataforma como Servicio)
- **Compatibilidad con SQL Server**: Casi completamente compatible con SQL Server. Migración con cambios mínimos en el código mediante Azure Database Migration.
- **Arquitectura**: Instancias administradas que pueden admitir varias bases de datos. Grupos de instancias para compartir recursos.
- **Disponibilidad**: 99.99%
- **Administración**: Actualizaciones, copias de seguridad y recuperación totalmente automatizados.
- **Casos de Uso**: Escenarios de migración a la nube con cambios mínimos en aplicaciones existentes.

---

## Azure SQL Database
- **Tipo de Servicio en la Nube**: PaaS (Plataforma como Servicio)
- **Compatibilidad con SQL Server**: Admite la mayoría de las funcionalidades básicas de SQL Server. Algunas características pueden no estar disponibles.
- **Arquitectura**: Base de datos única en un servidor dedicado y administrado (lógico) o grupo elástico para compartir recursos.
- **Disponibilidad**: 99.995%
- **Administración**: Actualizaciones, copias de seguridad y recuperación totalmente automatizados.
- **Casos de Uso**: Nuevas soluciones en la nube o migración de aplicaciones con dependencias mínimas de instancia.

---

# Comparación de los Servicios de Azure SQL

## SQL Server en Máquina Virtual de Azure (VM)

- **Tipo de Servicio en la Nube**: IaaS (Infraestructura como Servicio)
- **Compatibilidad con SQL Server**: Totalmente compatible con instalaciones locales. Migración lift-and-shift sin cambios.
- **Arquitectura**: Instancias de SQL Server en una máquina virtual. Cada instancia puede admitir varias bases de datos. Ofrece control total sobre el sistema operativo y el DBMS.
- **Disponibilidad**: 99.99%
- **Administración**: Debe administrar el sistema operativo, SQL Server, configuración, copias de seguridad y mantenimiento.
- **Casos de Uso**: Ideal para migraciones rápidas a la nube de aplicaciones existentes que requieren acceso a características del sistema operativo no disponibles en PaaS. También se utiliza para ampliar aplicaciones locales existentes en implementaciones híbridas.
- **Ventajas Empresariales**:
  - Satisfacer necesidades empresariales a través de implementaciones locales y en la nube.
  - Mantener el mismo conjunto de productos de servidor y herramientas de desarrollo.
  - Permitir un control total sobre todos los aspectos de la configuración del servidor y la base de datos.

---

## Azure SQL Managed Instance

- **Tipo de Servicio en la Nube**: PaaS (Plataforma como Servicio)
- **Compatibilidad con SQL Server**: Casi completamente compatible con SQL Server. Migración con cambios mínimos en el código mediante Azure Database Migration.
- **Arquitectura**: Instancias administradas que pueden admitir varias bases de datos. Grupos de instancias para compartir recursos. Se automatizan las copias de seguridad, la aplicación de revisiones y la supervisión.
- **Disponibilidad**: 99.99%
- **Administración**: Actualizaciones, copias de seguridad y recuperación totalmente automatizados. Mantiene control total sobre la seguridad y asignación de recursos.
- **Casos de Uso**: Escenarios de migración a la nube con cambios mínimos en aplicaciones existentes. Ideal para sistemas que requieren características como servidores vinculados, Service Broker o correo electrónico de base de datos.
- **Ventajas Empresariales**:
  - Menor tiempo dedicado a tareas administrativas gracias a la automatización.
  - Compatibilidad casi completa con SQL Server Enterprise Edition.
  - Admite inicios de sesión del motor de base de datos de SQL Server y Microsoft Entra ID.

---

## Azure SQL Database

- **Tipo de Servicio en la Nube**: PaaS (Plataforma como Servicio)
- **Compatibilidad con SQL Server**: Admite la mayoría de las funcionalidades básicas de SQL Server. Algunas características pueden no estar disponibles.
- **Arquitectura**:
  - **Base de datos única**: Ejecuta una sola base de datos de SQL Server. Recurso escalable automáticamente con opciones de configuración aprovisionada o sin servidor.
  - **Grupo elástico**: Múltiples bases de datos comparten recursos como memoria, almacenamiento y capacidad de procesamiento. Ideal para bases de datos con requisitos de recursos variables.
- **Disponibilidad**: 99.995%
- **Administración**: Actualizaciones, copias de seguridad y recuperación totalmente automatizados.
- **Casos de Uso**: Nuevas soluciones en la nube o migración de aplicaciones con dependencias mínimas de instancia. Adecuado para aplicaciones modernas en la nube que requieren alta disponibilidad y escalabilidad dinámica.
- **Ventajas Empresariales**:
  - Actualizaciones automáticas y aplicación de revisiones.
  - Escalabilidad dinámica para aumentar los recursos disponibles según las necesidades.
  - Alta disponibilidad garantizada del 99.99%.
  - Restauración a un momento dado y replicación en distintas regiones.
  - Advanced Threat Protection y auditoría de seguridad para detectar y corregir problemas de seguridad.

---



---







---
## Descripción de los Servicios de Azure para Bases de Datos de Código Abierto

### 1. Azure Database for MySQL
Azure Database for MySQL es una implementación **PaaS** de MySQL en la nube de Azure que se basa en la edición Community de MySQL.
- **Escalabilidad**: Proporciona un sistema de base de datos global que se puede escalar verticalmente a bases de datos grandes.
- **Gestión Totalmente Administrada**: No necesitas administrar el hardware, los componentes de red, los servidores virtuales, las revisiones de software y otros componentes subyacentes.

### 2. Azure Database for MariaDB
Azure Database for MariaDB es una implementación del sistema de administración de bases de datos **MariaDB** adaptada para ejecutarse en Azure. Se basa en la edición Community de MariaDB.
- **Gestión Totalmente Administrada**: Una vez aprovisionado el servicio y transferidos los datos, el sistema no requiere prácticamente ninguna administración más.

### 3. Azure Database for PostgreSQL
Si prefieres PostgreSQL, puedes elegir **Azure Database for PostgreSQL** para ejecutar una implementación PaaS de PostgreSQL en la nube de Azure.
- **Ventajas**: Proporciona las mismas ventajas de disponibilidad, rendimiento, escalado, seguridad y administración que MySQL.

---

## Resumen
Azure admite varios servicios de base de datos que se pueden usar para admitir nuevas aplicaciones en la nube o migrar aplicaciones existentes a la nube.

En este módulo has aprendido a:
- **Identificar las opciones para los servicios de Azure SQL**.
- **Identificar las opciones para las bases de datos de código abierto en Azure**.
- **Aprovisionar un servicio de base de datos en Azure**.
