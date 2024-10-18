# 10) Almacenamiento de datos de aplicaciones con Azure Blob Storage 

# Introducción a Blob Storage

## ¿Qué es Blob Storage?
Los blobs proporcionan **almacenamiento de objetos en la nube** y una **API** que permite compilar aplicaciones para acceder a los datos.

### Ejemplo Práctico
Imagina que trabajas en una empresa de juegos de realidad aumentada y deseas agregar una característica para que los usuarios graben clips de vídeo de su juego. Necesitas una solución de almacenamiento que pueda controlar **miles de cargas simultáneas**, **enormes cantidades de datos de vídeo** y **archivos de registro en constante crecimiento**.

### Azure Blob Storage
**Azure Blob Storage** es adecuado para esta aplicación, ya que permite:
- Controlar **múltiples cargas simultáneas**.
- Manejar grandes volúmenes de datos de vídeo.
- Acceder a la API desde varias plataformas y lenguajes.

## Objetivos de Aprendizaje
En este módulo, aprenderás a:
- **Organizar los datos con Azure Blob Storage**.
- **Crear recursos de almacenamiento** para almacenar blobs.
- **Almacenar y recuperar datos** desde Azure Blob Storage.


---


# ¿Qué son los blobs?

## Definición
Los **blobs** son archivos para la nube. Las aplicaciones funcionan con blobs de la misma manera que con archivos en un disco, pero se puede acceder a los blobs desde cualquier lugar con conexión a Internet.

### Azure Blob Storage
**Azure Blob Storage** almacena datos no estructurados. No hay restricciones en los tipos de datos que puede contener. Un blob puede contener un **documento PDF**, **imagen JPG**, **archivo JSON**, **contenido de vídeo**, etc.

### Usos Comunes
- Aplicaciones que necesitan transmitir grandes cantidades de datos.
- Sistema de archivos para almacenar y compartir documentos y datos personales.
- Recursos web estáticos como imágenes disponibles para descarga pública.
- Componentes de Azure como **Azure Cloud Shell** y **Azure Virtual Machines** usan blobs en segundo plano.

### Limitaciones
- No eficaces para datos estructurados que se deben consultar con frecuencia.
- Tienen una latencia mayor que la memoria y los discos locales.
- No tienen características de indexación como las bases de datos.

### Ejemplo Práctico
Una aplicación con una base de datos de perfiles de usuario puede almacenar imágenes de los perfiles en blobs. Cada registro de usuario incluiría el nombre o la URL del blob que contiene la imagen del usuario.

## Estructura de Almacenamiento

### Cuentas de Almacenamiento y Contenedores
En **Blob Storage**, todos los blobs residen dentro de un **contenedor de blobs**. En una cuenta de almacenamiento se puede almacenar un número ilimitado de blobs en un contenedor y un número ilimitado de contenedores. Los contenedores son planos y solo pueden almacenar blobs, no otros contenedores.

### Etiquetas y Metadatos
- Los blobs y contenedores admiten **etiquetas y metadatos** en forma de pares de cadenas de nombre-valor.
- Las aplicaciones pueden usar etiquetas y metadatos para descripciones legibles o para determinar cómo procesar los datos.
- **Sugerencia**: Blob Storage no proporciona mecanismos para buscar u ordenar los blobs por metadatos. Use etiquetas de índice de blobs para esto.

## API y Bibliotecas de Cliente
La **API de Blob Storage** se basa en **REST**. Las bibliotecas cliente de muchos lenguajes populares lo admiten, permitiendo escribir aplicaciones que crean y eliminan blobs y contenedores, cargan y descargan datos de blob, y enumeran los blobs de un contenedor.


---

# Diseño de una Estrategia de Organización de Almacenamiento

## Cuentas de Almacenamiento
Una sola **cuenta de almacenamiento** es lo suficientemente flexible como para organizar los blobs, pero puedes usar más cuentas para separar **costes y control de acceso** de datos.

## Contenedores y Blobs

### Estrategia de Nomenclatura y Organización
- **Aplicaciones con Base de Datos**: Usan identificadores como GUID para los nombres de blob y hacen referencia a estos en los registros de la base de datos.
- **Sistema de Archivos Personal**: Nombres de contenedor y blob indican significado y estructura, similar a nombres de archivo tradicionales. Usan **directorios virtuales** para organizar blobs.

### Consideraciones Clave
- **Limitaciones sobre Nomenclatura**: Nombres de contenedores y blobs deben seguir reglas específicas (longitud y caracteres).
- **Acceso Público y Seguridad**: Contenedores pueden configurarse para permitir la descarga pública de blobs sin autenticación. 
  - **Importante**: Nunca colocar datos sensibles en un contenedor público.
- **Prefijos de Nombres de Blob (Directorios Virtuales)**: Permiten navegar por blobs como en un sistema jerárquico de archivos.

## Tipos de Blobs

### Blobs en Bloques
- **Descripción**: Compuestos por bloques de diferentes tamaños que se pueden cargar de forma independiente y en paralelo.
- **Uso Ideal**: Escenarios que requieren cargas y descargas rápidas.

### Blobs Anexos
- **Descripción**: Blobs en bloque especializados que solo permiten anexar datos nuevos.
- **Uso Ideal**: Almacenamiento de registros o escritura de datos en streaming.

### Blobs en Páginas
- **Descripción**: Admiten lecturas y escrituras de acceso aleatorio.
- **Uso Ideal**: Almacenar archivos de disco duro virtual (VHD) usados por Azure Virtual Machines.

### Recomendación
Para la mayoría de los escenarios que no requieren específicamente blobs en anexos o en páginas, los **blobs en bloques** son la mejor opción.



---


Ejercicio: creación de recursos de Azure Storage
Completado
100 XP
5 minutos
Espacio aislado activado Tiempo restante: 
Ha usado 1 de los 10 espacios aislados de hoy. Mañana habrá disponibles más espacios aislados.

Elija el lenguaje de desarrollo
Cuando tenga una idea de cómo se van a almacenar los datos en cuentas de almacenamiento, blobs y contenedores, puede pensar en los recursos de Azure que necesita para que se admita la aplicación.

Cuentas de almacenamiento
La creación de cuentas de almacenamiento es una actividad administrativa que tiene lugar antes de implementar y ejecutar la aplicación. Para crear cuentas, use un script de implementación o configuración de entorno, una plantilla de Azure Resource Manager o establézcalas manualmente. Las aplicaciones que no son herramientas administrativas no deben tener permisos para crear cuentas de almacenamiento.

Contenedores
A diferencia de la creación de cuentas de almacenamiento, la creación de contenedores es una actividad ligera que tiene sentido realizarla desde dentro de una aplicación. No es raro que las aplicaciones creen y eliminen contenedores como parte de su trabajo.

En el caso de las aplicaciones que dependen de un conjunto conocido de contenedores con nombres preconfigurados o codificados de forma rígida, puede permitir que la aplicación cree los contenedores que necesita en el inicio o el primer uso. Al permitir que la aplicación cree contenedores en lugar de hacerlo como parte de la implementación de la aplicación se elimina la necesidad de que tanto la aplicación como el proceso de implementación conozcan los nombres de los contenedores que usa la aplicación.

Ejercicio
Va a completar una aplicación sin terminar mediante la incorporación de código para usar Azure Blob Storage. Este ejercicio consiste más en explorar la API de Blob Storage que diseñar una organización y un esquema de nomenclatura. Esta es una introducción rápida de la aplicación y cómo almacena los datos.

Screenshot of the FileUploader web app for C#.

La aplicación funciona como una carpeta compartida que acepta cargas de archivos y permite que estén disponibles para su descarga. No usa una base de datos para organizar blobs. En su lugar, se corrigen los nombres de los archivos cargados y se usan como nombres de blobs directamente. Todos los archivos cargados se almacenan en un único contenedor.

El código con el que comienza compila y se ejecuta. Las partes responsables de almacenar y cargar datos están vacías. Una vez completado el código, implemente la aplicación en Azure App Service y pruébela.

Cuenta de almacenamiento
Use Azure Cloud Shell con la CLI de Azure para crear una cuenta de almacenamiento. Debe proporcionar un nombre único para la cuenta de almacenamiento. Tome nota de ello para más adelante. Reemplace <your-unique-storage-account-name> por un nombre de su preferencia. Los nombres de cuentas de almacenamiento deben tener entre 3 y 24 caracteres, y usar solo números y letras minúsculas.

Para crear la cuenta de almacenamiento, ejecute este comando.

Azure CLI

Copiar
az storage account create \
  --kind StorageV2 \
  --resource-group "learn-cd7b2787-441f-4f79-830d-b5bb56267ca0" \
  --location eastus \
  --name <your-unique-storage-account-name>
Contenedor
La aplicación con la que trabaja en este módulo usa un único contenedor. Siga el procedimiento recomendado de dejar que la aplicación cree el contenedor al inicio. Sin embargo, puede crear contenedores a partir del CLI de Azure. Si quiere ver la documentación, ejecute el comando az storage container create -h en Cloud Shell.

--name <cuenta-de-almacenamiento-mbelforte>\

<mi-app-blob-storage>




esta me sirvio
az appservice plan create --name blob-exercise-plan --resource-group "learn-7be069b9-6013-412f-9547-5cb5e38d97a0" --sku FREE --location centralus



az webapp create --name <mi-app-blob-storage> --plan blob-exercise-plan --resource-group "learn-7be069b9-6013-412f-9547-5cb5e38d97a0" \

CONNECTIONSTRING=$(az storage account show-connection-string --name <cuenta-de-almacenamiento-mbelforte> --resource-group "learn-7be069b9-6013-412f-9547-5cb5e38d97a0" --output tsv) \


az webapp config appsettings set --name <mi-app-blob-storage> --resource-group "learn-7be069b9-6013-412f-9547-5cb5e38d97a0" --settings AzureStorageConfig:ConnectionString=$CONNECTIONSTRING AzureStorageConfig:FileContainerName=files \

dotnet publish -o pub
cd pub
zip -r ../site.zip *

az webapp deployment source config-zip --src ../site.zip --name <mi-app-blob-storage> --resource-group "learn-7be069b9-6013-412f-9547-5cb5e38d97a0"

 https://<mi-app-blob-storage>.azurewebsites.net