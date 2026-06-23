# Prueba Técnica - Grenergy: Pipeline de Datos Energéticos

## 1. Arquitectura de la Solución
El proyecto implementa un pipeline ETL completo en Microsoft Fabric para la ingesta y exposición de precios eléctricos en mercados europeos.
- **Pipeline (ETL):** Notebook de PySpark en Fabric que consume APIs (XML/JSON), normaliza timestamps a UTC y convierte divisas (PLN a EUR).
- **Almacenamiento:** Delta Lake con particionado por país.
- **Exposición (API):** SQL Analytics Endpoint (nativo de Fabric) para acceso vía SQL.
- **Visualización:** Reporte en Power BI con comparativa multi-país y auditoría de anomalías.

## 2. Decisiones Técnicas
- **Escalabilidad:** Se utilizó un diccionario `CONFIG_PAISES` que permite añadir nuevos países sin modificar el flujo lógico.
- **Manejo de Granularidad:** Se normalizaron las series temporales de 15min (ENTSO-E/PSE) y 60min (SMARD) en el modelo semántico de Power BI, permitiendo agregaciones consistentes.
- **Seguridad:** Se optó por el **SQL Analytics Endpoint** sobre una API tradicional para aprovechar la autenticación nativa de **Microsoft Entra ID (OAuth2)**, eliminando la gestión de credenciales en código.
- **Endpoint API:** `nveaxm7fxvkedjdo5r4377arw4-ztbx7ideq2nuxhwdf7olc7mioa.datawarehouse.fabric.microsoft.com`

## 3. Instrucciones de Despliegue
1. Clonar el repositorio.
2. Importar el archivo `.ipynb` en un Notebook de Microsoft Fabric.
3. Configurar el `ENTSOE_TOKEN` en la variable correspondiente.
4. Ejecutar el Notebook para actualizar el Lakehouse.
