#  Base de datos Analytics desde ficheros JSON

Estas instrucciones describen cómo importar una serie de ficheros JSON dentro de colecciones de una base de datos en nuestro contenedor MongoDB.

El ejemplo utilizado proviene de la documentación de MongoDB, y consiste en una base de datos financiera con clientes, cuentas de acciones, y transacciones. Puedes encontrar la documentación [en este enlace](https://www.mongodb.com/docs/atlas/sample-data/sample-analytics/#std-label-sample-analytics).

## Carga de datos

Antes de ejecutar los siguientes pasos, asegúrate de haber creado el contenedor `mimongodb`, y que este contenedor está arrancado. Para ello, sigue las [instrucciones de instalación de Mongodb](instrucciones_mongodb.md).

1. Descarga y extrae el archivo comprimido [del siguiente enlace](https://unican-my.sharepoint.com/:u:/g/personal/delavegaa_unican_es/EX4Vsg5_6chNqXVil3x1clgB4poxvN2eSnkcXBmlzT6dOg?e=tGOeDz).
2. Abre una terminal en el directorio en el que se encuentren los ficheros json extraídos del archivo comprimido.
3. Ejecuta los siguientes comandos (uno a uno):
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
4. Comprueba en Studio3T que se ha creado la base de datos indicada y que contiene tres colecciones (`accounts`, `customers` y `transactions`)

## Consultas sobre el dataset

1. Datos de cuentas con un límite menor a 8000
2. Datos de clientes nacidos antes de 1991
3. Datos de cuentas con productos de tipo `Commodity`
    - Misma consulta, pero de tipo `Commodity` y `Derivatives` (es decir, ambos deben aparecer)
    - Misma consulta, pero de tipo `Commodity` o `Derivatives` (con que aparezca uno vale)
4. Ids de cuentas que vendieron acciones de ebay
