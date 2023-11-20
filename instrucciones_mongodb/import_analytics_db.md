#  Base de datos Analytics desde ficheros JSON

Estas instrucciones describen cómo importar una serie de ficheros JSON dentro de colecciones de una base de datos en nuestro contenedor MongoDB.

## Ficheros de Ejemplo

El ejemplo proviene de la documentación de MongoDB, y consiste en una base de datos financiera con clientes, cuentas de acciones, y transacciones. Puedes encontrar la documentación [en este enlace](https://www.mongodb.com/docs/atlas/sample-data/sample-analytics/#std-label-sample-analytics).

Puedes descargarte los ficheros JSON que utilizaremos en los siguientes: [customers](https://raw.githubusercontent.com/mcampo2/mongodb-sample-databases/master/sample_analytics/customers.json), [accounts](https://raw.githubusercontent.com/mcampo2/mongodb-sample-databases/master/sample_analytics/accounts.json), [transactions](https://raw.githubusercontent.com/mcampo2/mongodb-sample-databases/master/sample_analytics/transactions.json).

## Carga de datos

1. Abre una terminal en el directorio en el que se encuentren los ficheros que has descargado.
2. Ejecuta los siguientes comandos (uno a uno):
```bash
# Copy json files to docker container
docker cp customers.json mimongodb:/tmp/customers.json
docker cp accounts.json mimongodb:/tmp/accounts.json
docker cp transactions.json mimongodb:/tmp/transactions.json

# Import json file into a collection of a database
# Both the database and the collection are created if they do not exist
docker exec mimongodb mongoimport -d analyticsdb -c customers --file /tmp/customers.json
docker exec mimongodb mongoimport -d analyticsdb -c accounts --file /tmp/accounts.json
docker exec mimongodb mongoimport -d analyticsdb -c transactions --file /tmp/transactions.json
```
3. Comprueba en Studio3T que se ha creado la base de datos indicada y que contiene tres colecciones (`accounts`, `customers` y `transactions`)

## Posibles consultas a realizar y optimizar

- Datos de cuentas con un límite menor a 10,000
- Datos de cuentas con productos de tipo `"Commodity"`
- Datos de clientes nacidos antes de 1991
- Ids de cuentas que vendieron acciones de ebay
