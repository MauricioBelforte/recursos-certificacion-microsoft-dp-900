# 9) Exploración de los Aspectos Básicos de la Visualización de Datos

## Introducción
Conozca los principios fundamentales del modelado de datos analíticos y la visualización de datos, usando **Microsoft Power BI** como plataforma para explorar estos principios en acción.

## Objetivos de Aprendizaje
En este módulo aprenderás a:
- Describir un proceso de alto nivel para crear soluciones de informes con **Microsoft Power BI**.
- Describir los principios básicos del **modelado de datos analíticos**.
- Identificar los tipos comunes de **visualización de datos** y sus usos.
- Crear un informe interactivo con **Power BI Desktop**.

## 1. Crear Soluciones de Informes con Microsoft Power BI

### Proceso de Alto Nivel
1. **Conectar y Preparar los Datos**:
   - Conecta Power BI a diversas fuentes de datos.
   - Limpia y transforma los datos para su análisis.
   
2. **Modelar los Datos**:
   - Crea relaciones entre las tablas de datos.
   - Define medidas y cálculos necesarios para el análisis.

3. **Visualizar los Datos**:
   - Usa gráficos y tablas para representar los datos de manera visual.
   - Personaliza los informes según las necesidades de los usuarios.

4. **Compartir y Colaborar**:
   - Publica los informes en el servicio Power BI.
   - Comparte los informes con otros usuarios y colabora en tiempo real.

## 2. Principios Básicos del Modelado de Datos Analíticos

### Definición
El modelado de datos analíticos implica organizar y estructurar los datos para facilitar el análisis y la visualización.

### Pasos Principales
- **Definir Entidades y Relaciones**: Identifica las entidades clave y cómo se relacionan entre sí.
- **Normalización y Desnormalización**: Decide cuándo normalizar (dividir en tablas más pequeñas) y cuándo desnormalizar (combinar tablas).
- **Creación de Medidas y Cálculos**: Define métricas clave y cálculos necesarios para el análisis.

## 3. Tipos Comunes de Visualización de Datos

### Tipos y Usos
- **Gráficos de Barras**: Comparar cantidades entre diferentes categorías.
- **Gráficos de Líneas**: Mostrar tendencias a lo largo del tiempo.
- **Diagramas de Dispersión**: Mostrar la relación entre dos variables.
- **Mapas Geoespaciales**: Representar datos en un contexto geográfico.
- **Tablas y Matrices**: Mostrar datos detallados en un formato estructurado.

## 4. Crear un Informe Interactivo con Power BI Desktop

### Pasos para Crear un Informe
1. **Importar Datos**: Conecta Power BI Desktop a la fuente de datos deseada.
2. **Preparar los Datos**: Limpia y transforma los datos para el análisis.
3. **Crear Visualizaciones**: Añade gráficos, tablas y otros elementos visuales al informe.
4. **Personalizar el Informe**: Ajusta el diseño y la apariencia según las necesidades.
5. **Publicar y Compartir**: Publica el informe en el servicio Power BI y compártelo con otros usuarios.


---

# Descripción de las Herramientas y el Flujo de Trabajo de Power BI

## Introducción
Existen muchas herramientas de visualización de datos, como **Microsoft Excel** y **Azure Databricks**, pero para un análisis empresarial a gran escala se necesita una **solución integrada** como **Microsoft Power BI**.

## Microsoft Power BI
**Microsoft Power BI** es un conjunto de herramientas y servicios en **Microsoft Fabric** que permite a los analistas de datos crear **visualizaciones de datos interactivas**.

## Flujo de Trabajo en Power BI
1. **Power BI Desktop**:
   - **Importar datos** de múltiples orígenes.
   - **Combinar y organizar los datos** en un modelo de datos de análisis.
   - **Crear informes** con visualizaciones interactivas.

2. **Servicio Power BI**:
   - **Publicar modelos de datos e informes** en la nube.
   - **Realizar modelado básico** de datos y edición de informes.
   - **Programar actualizaciones** de los datos y **compartir informes** con otros usuarios.

## Consumo de Informes
- Los usuarios pueden **ver informes, paneles y aplicaciones** en el servicio Power BI a través de un **navegador web** o en **dispositivos móviles** con la app de Power BI.


---


# Descripción de los Conceptos Básicos del Modelado de Datos

## Modelos Analíticos
Los **modelos analíticos** permiten estructurar los datos para admitir el análisis. Se basan en **tablas de datos relacionadas** y definen los **valores numéricos** (medidas) y las **entidades** por las que se quieren agregar (dimensiones).

### Ejemplo Práctico
Un modelo podría incluir una tabla con medidas numéricas para las ventas (ingresos o cantidad) y dimensiones para productos, clientes y tiempo. Esto permite agregar medidas de venta en varias dimensiones (e.g., ingresos totales por cliente).

## Estructura Multidimensional
El modelo forma una estructura multidimensional, conocida como **cubo**, donde cualquier punto de intersección de las dimensiones representa una medida agregada.

## Tablas y Esquema

### Tablas de Dimensiones
- Representan las entidades por las que se quieren agregar las medidas numéricas (producto, cliente).
- Cada entidad se representa con una fila con un valor de clave único y columnas que representan los atributos (nombres, categorías, direcciones).

### Tablas de Hechos
- Las **medidas numéricas** se almacenan en tablas de hechos.
- Cada fila representa un evento registrado con medidas numéricas asociadas (ventas, ingresos).

### Esquema de Estrella y Copo de Nieve
- **Esquema de Estrella**: Una tabla de hechos relacionada con una o varias tablas de dimensiones.
- **Esquema de Copo de Nieve**: Tablas de dimensiones relacionadas con tablas adicionales que contienen más detalles.

## Jerarquías de Atributos
Las **jerarquías de atributos** permiten rastrear datos o explorar en profundidad valores agregados en distintos niveles de una dimensión jerárquica (e.g., año, mes, día).

### Ejemplo Práctico
En la tabla **Product**, una jerarquía podría incluir categoría y producto. En la tabla **Customer**, una jerarquía podría representar clientes por ciudad. En la tabla **Time**, una jerarquía podría ser año, mes y día.

## Modelado Analítico en Microsoft Power BI
Puedes usar **Power BI** para definir un modelo analítico a partir de tablas de datos importadas desde varios orígenes.

### Pasos Principales
- **Crear relaciones** entre tablas de hechos y dimensiones.
- **Definir jerarquías**.
- **Establecer tipos de datos y formatos** de presentación.
- Administrar otras propiedades de los datos para definir un modelo enriquecido para el análisis.


---


# Descripción de Consideraciones para la Visualización de Datos

## Introducción
Después de crear un modelo, se puede usar para generar visualizaciones de datos que se pueden incluir en un informe.

### Power BI y Visualizaciones de Datos
**Power BI** incluye un amplio conjunto de **visualizaciones integradas**, que se pueden ampliar con visualizaciones personalizadas y de terceros.

## Tipos Comunes de Visualización de Datos

### Tablas y Texto
- **Descripción**: Son la manera más sencilla de comunicar datos.
- **Uso**: Las tablas son útiles para mostrar numerosos valores relacionados. Las tarjetas de texto muestran cifras o métricas importantes.
- **Ejemplo**: Tabla de ventas por producto y tarjeta de texto con ingresos totales.

### Gráficos de Barras y de Columnas
- **Descripción**: Buena manera de comparar visualmente valores numéricos para categorías discretas.
- **Ejemplo**: Gráfico de columnas con ingresos por categoría de cada ciudad.

### Gráficos de Líneas
- **Descripción**: Útiles para comparar valores clasificados y examinar tendencias, a menudo a lo largo del tiempo.
- **Ejemplo**: Gráfico de líneas con tendencia de ingresos a lo largo del tiempo por categoría de producto.

### Gráficos Circulares
- **Descripción**: Comparan visualmente los valores clasificados como proporciones de un total.
- **Ejemplo**: Gráfico circular con la proporción de ventas por categoría de producto.

### Gráficos de Dispersión
- **Descripción**: Útiles para comparar dos medidas numéricas e identificar relaciones o correlaciones.
- **Ejemplo**: Gráfico de dispersión con el gasto en marketing frente a los ingresos.

### Mapas
- **Descripción**: Excelente manera de comparar visualmente los valores de diferentes áreas geográficas o ubicaciones.
- **Ejemplo**: Mapa con ingresos comparativos por ciudad.

## Informes Interactivos en Power BI

### Descripción
En **Power BI**, los elementos visuales de los datos relacionados de un informe se vinculan automáticamente entre sí, proporcionando **interactividad**.

### Ejemplo
Al seleccionar una categoría en una visualización, se filtra y resalta automáticamente en otras visualizaciones relacionadas del informe.
- **Ejemplo Visual**: Selección de Seattle en un gráfico de columnas filtra las demás visualizaciones para mostrar valores solo de Seattle.


---