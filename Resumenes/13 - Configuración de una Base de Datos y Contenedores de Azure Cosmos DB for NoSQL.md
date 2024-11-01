# 13) Configuración de una Base de Datos y Contenedores de Azure Cosmos DB for NoSQL

## Objetivos de Aprendizaje
Después de completar este módulo, podrás:
- **Comparar las distintas ofertas de servicio y rendimiento** para Azure Cosmos DB.
- **Migrar entre el rendimiento estándar y el rendimiento de escalabilidad automática**.

## Descripción del Módulo
En este módulo, aprenderás a elegir entre las distintas ofertas de rendimiento en **Azure Cosmos DB for NoSQL**.

### Unidades del Módulo

1. **Comparación de Ofertas de Servicio**:
   - **Rendimiento Estándar**: Adecuado para cargas de trabajo con patrones de uso predecibles.
   - **Escalabilidad Automática**: Ajusta automáticamente el rendimiento según la demanda.

2. **Configuración de la Base de Datos**:
   - Opciones de configuración para optimizar la eficiencia y el rendimiento.

3. **Configuración de Contenedores**:
   - Configuración de contenedores para manejar diferentes cargas de trabajo y tipos de datos.

4. **Migración de Rendimiento**:
   - Procedimientos y consideraciones para migrar entre rendimiento estándar y escalabilidad automática.

5. **Optimización de Costos**:
   - Estrategias para minimizar los costos mientras se mantiene un rendimiento óptimo.


---

# Introducción

Las aplicaciones tienen muchos patrones diferentes: pueden tener un **uso predecible** o alcanzar un máximo con **picos repentinos de tráfico**. **Azure Cosmos DB** tiene varias maneras de hospedar cargas de trabajo que se asignan directamente a cómo se ejecutan las aplicaciones en el mundo real, tanto si las aplicaciones son predecibles como si se basan completamente en el crecimiento.

## Objetivos de Aprendizaje
Después de completar este módulo, podrás:
- **Comparar las distintas ofertas de servicio y rendimiento** para Azure Cosmos DB.
- **Migrar entre el rendimiento estándar y el rendimiento de escalabilidad automática**.

---

# Azure Cosmos DB sin Servidor

**Azure Cosmos DB sin servidor** es un modelo basado en el consumo en el que cada solicitud consume **unidades de solicitud (RU/s)**. Este modelo elimina la necesidad de aprovisionar previamente las unidades de solicitud de rendimiento con antelación.

## Casos de Uso del Modo sin Servidor

El modo sin servidor es ideal para aplicaciones con **tráfico impredecible** o con **ráfagas**. Puede usar el modo sin servidor con aplicaciones como las siguientes:
- Una **nueva aplicación** con cargas de usuarios difíciles de predecir.
- Una **nueva aplicación de prototipo** dentro de la organización.
- **Integración de un proceso sin servidor** en un servicio como **Azure Functions**.
- **Nuevo desarrollador** que acaba de empezar a trabajar con Azure Cosmos DB.
- **Aplicación de poco tráfico** que no envía ni recibe numerosos datos.


---


# Comparación entre Rendimiento Aprovisionado y Sin Servidor

## Cargas de Trabajo
- **Rendimiento Aprovisionado**: Ideal para cargas de trabajo con **patrones de tráfico predecibles** que requieren rendimiento continuo y predecible.
- **Modo Sin Servidor**: Perfecto para cargas de trabajo con **tráfico muy variable** y picos inesperados.

## Unidades de Solicitud (RU/s)
- **Rendimiento Aprovisionado**: Un número fijo de RU/s está disponible cada segundo para cada contenedor. Este número puede actualizarse manualmente o mediante escalabilidad automática.
- **Modo Sin Servidor**: No requiere planificación ni aprovisionamiento previo. Ofrece rendimiento hasta un límite de servicio.

## Distribución Global
- **Rendimiento Aprovisionado**: Admite la distribución de datos a un número ilimitado de regiones de Azure.
- **Modo Sin Servidor**: Solo se puede ejecutar en una única región de Azure.

## Límites de Almacenamiento
- **Rendimiento Aprovisionado**: Permite almacenar datos ilimitados en un contenedor.
- **Modo Sin Servidor**: Permite hasta 50 GB de datos en un contenedor.

---


# Escalabilidad Automática del Rendimiento en Azure Cosmos DB

A menudo se puede estimar dónde se encontrará la carga de trabajo en cuanto al rendimiento, pero no se sabrá exactamente hasta que esté en producción. Es útil conocer:
- **La cantidad máxima de dinero que estamos dispuestos a gastar**.
- **La cantidad mínima de rendimiento que estamos listos para tolerar**.

Con esta información, se puede definir un **rango** que representa la ejecución de la aplicación en un nivel de rendimiento cómodo sin gastos excesivos.

## Beneficios de la Escalabilidad Automática
- Con **Azure Cosmos DB**, podemos definir un rango de **unidades de solicitud por segundo (RU/s)** para escalar la base de datos o el contenedor de forma automática e instantánea.
- Las RU/s de rendimiento se ajustan automáticamente en función del uso en tiempo real.

## Casos de Uso
- **Cargas de trabajo con patrones de tráfico variables o impredecibles**.
- Minimizar la **capacidad no utilizada** que normalmente se aprovisionaría previamente.

---

# Comparación entre el Rendimiento Estándar (Manual) y el Rendimiento de Escalabilidad Automática

## Cargas de Trabajo
- **Rendimiento Estándar**: Adecuado para cargas de trabajo con **tráfico estable**.
- **Rendimiento de Escalabilidad Automática**: Más adecuado para **tráfico impredecible**. Garantiza que el rendimiento aprovisionado oscile entre el rendimiento mínimo aceptable y el gasto máximo permitido.

## Unidades de Solicitud (RU/s)
- **Rendimiento Estándar**: Requiere asignar un número estático de RU/s con antelación.
- **Escalabilidad Automática**: Solo se establece el máximo y el mínimo facturado será el 10 % del máximo cuando haya cero solicitudes.

## Escenarios
- **Rendimiento Estándar**: 
  - Recomendado cuando el equipo puede **predecir con precisión** la cantidad de rendimiento necesario y estas necesidades no cambiarán con el tiempo.
  - Ideal cuando se consume la RU/s completa aprovisionada durante > 66 % de las horas al mes.
- **Escalabilidad Automática**:
  - Útil si el equipo **no puede predecir las necesidades de rendimiento** con precisión.
  - Ideal cuando se usa la cantidad máxima de rendimiento durante < 66 % de las horas al mes.

## Limitación de Velocidad
- **Rendimiento Estándar**: Permanece estático en la RU/s establecida. Las solicitudes que la sobrepasen se limitan con una respuesta que indica que se debe esperar antes de volver a intentarlo.
- **Escalabilidad Automática**: Se escalará verticalmente hasta el número máximo de RU/s antes de que se indiquen respuestas de limitación de velocidad similares.

---

# Migración entre el Rendimiento Estándar (Manual) y el Rendimiento de Escalabilidad Automática

Los contenedores existentes se pueden migrar a y desde la **escalabilidad automática** mediante **Azure Portal**, la **CLI de Azure** o **Azure PowerShell**. Durante el proceso de migración, el sistema aplicará automáticamente un valor de **unidad de solicitud por segundo (RU/s)** al contenedor.

## Nota
Siempre puedes cambiar este valor de **RU/s** después de que se haya producido la migración.

---

