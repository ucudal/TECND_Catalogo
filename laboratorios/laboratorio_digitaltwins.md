# Laboratorio: Simulación de un Data Center con Azure Digital Twins

## 🎯 Objetivo
El objetivo de este es:
- Crear y configurar un modelo de **Digital Twin** en **Azure Digital Twins**.
- Desplegar una **Function App en Azure** que simule datos de sensores (temperatura).
- Conectar la Function App con Azure Digital Twins y actualizar propiedades de un gemelo digital.
- Visualizar y monitorear los datos simulados.
- Desplegar otra **Function App en Azure** que permita accionar sistemas de control como aire acondicionado o deshumidificadores.

---

## 📝 Descripción
Se plantea un escenario donde debemos **monitorear un Data Center**.  
Los sensores de **temperatura, humedad, voltaje y consumo eléctrico** serán simulados por una **Function App en Azure**, que enviará datos periódicamente al modelo definido en Azure Digital Twins.  

En una segunda etapa, se podrán definir reglas para accionar sistemas de control como aire acondicionado o deshumidificadores.

---

## 🚀 Pasos

### 1. Crear un recurso de Azure Digital Twins
1. Crear un nuevo recurso → **Azure Digital Twins**.
2. Anotar la **URL de la instancia** (ejemplo: `https://<nombre>.api.<region>.digitaltwins.azure.net`).

---

### 2. Definir el modelo del Data Center (DTDL)
Usaremos un modelo simplificado:

```json
{
 "@id": "dtmi:tnd:DataCenter;1",
 "@type": "Interface",
 "@context": "dtmi:dtdl:context;2",
 "displayName": "DataCenter",
 "contents": [
  {
   "@type": "Property",
   "name": "temperature",
   "displayName": "Temperature",
   "schema": "double"
  },
  {
   "@type": "Property",
   "name": "humidity",
   "displayName": "Humidity",
   "schema": "double"
  },
  {
   "@type": "Property",
   "name": "voltage",
   "displayName": "Voltage",
   "schema": "double"
  },
  {
   "@type": "Property",
   "name": "powerConsumption",
   "displayName": "Power Consumption",
   "schema": "double"
  },
  {
   "@type": "Property",
   "name": "airConditioner",
   "displayName": "Air Conditioner",
   "schema": "boolean"
  },
  {
   "@type": "Property",
   "name": "dehumidifier",
   "displayName": "Dehumidifier",
   "schema": "boolean"
  },
  {
   "@type": "Property",
   "name": "alert",
   "displayName": "Alert",
   "schema": "string"
  }
 ]
}
```
### 3. Crear un gemelo digital
Con el modelo cargado, crear un gemelo llamado `DataCenter1`.

---

### 4. Crear la Function App en Azure
1. Crear una función de tipo **Timer Trigger** que simule valores de sensores y los envíe al gemelo digital.  

Ejemplo simplificado en Python:

```python
import datetime, logging, os, random
import azure.functions as func
from azure.digitaltwins.core import DigitalTwinsClient
from azure.identity import DefaultAzureCredential

def main(mytimer: func.TimerRequest) -> None:
    utc_timestamp = datetime.datetime.utcnow().isoformat()
    logging.info(f"Timer executed at {utc_timestamp}")

    # Simulación de datos
    temperature = round(random.uniform(18, 35), 2)
    humidity = round(random.uniform(30, 80), 2)
    voltage = round(random.uniform(210, 230), 2)
    power = round(random.uniform(1000, 5000), 2)

    # Conexión a ADT
    adt_url = os.environ["ADT_SERVICE_URL"]
    cred = DefaultAzureCredential()
    client = DigitalTwinsClient(adt_url, cred)

    # Actualizar twin
    twin_id = "DataCenter1"
    patch = [
        {"op": "replace", "path": "/temperature", "value": temperature},
        {"op": "replace", "path": "/humidity", "value": humidity},
        {"op": "replace", "path": "/voltage", "value": voltage},
        {"op": "replace", "path": "/powerConsumption", "value": power}
    ]
    client.update_digital_twin(twin_id, patch)

    logging.info(
        f"Updated {twin_id} with T={temperature}, H={humidity}, V={voltage}, P={power}"
    )

```
### 5. Verificar datos
1. Desde **Azure Digital Twins Explorer**, observar cómo se actualizan las propiedades de **temperatura**, **humedad**, **voltaje** y **consumo eléctrico** con cada ejecución de la Function App.

### 6. Crear una nueva Function App en Azure
1. Crear una función que lea el estado del **gemelo digital** y accione el aire acondicionado si la temperatura es mayor a 23° y/o el deshumidificador si el porcentaje de humdad es mayor al 65%.
---

### 7. Entregables
- 📸 **Captura de pantalla** del modelo cargado en Azure Digital Twins.  
- 📸 **Captura de pantalla** de la Function App ejecutándose (logs con datos simulados).  
- 📸 **Captura de pantalla** del gemelo `DataCenter1` mostrando los valores actualizados.  
- 📝 Un **documento breve (máx. 1 página)** explicando qué otras acciones podrían implementar.  
---
