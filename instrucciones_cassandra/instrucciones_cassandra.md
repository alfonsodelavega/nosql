# Instrucciones Cassandra

## Instalación

1. Seguid las instrucciones de instalación de Docker

2. Abrid una terminal: `cmd` en Windows

4. Cread un contenedor `micassandra` mediante el siguiente comando, que descarga la imagen adecuada:

   `docker run -p 9042:9042 --name micassandra -d cassandra:4.0`

## Conexión a Cassandra en modo interactivo: cqlsh

### Desde Docker Desktop

1. Acceded a la pestaña _Containers_
2. Comprobad que el contenedor `micassandra` aparece en la lista de contenedores, y que se encuentra en ejecución
3. Haced doble click en el elemento de la lista
4. En la ventana resultante, haced click en la pestaña terminal
5. Ejecutad el comando `cqlsh`, que os cambiará el prompt de la terminal a `cqlsh>`, permitiéndoos ejecutar comandos CQL sobre el contenedor

![](cqlshDockerDesktop.png)

### Desde la terminal de vuestro sistema:

1. Abrir una shell de CQL en modo interactivo en el contenedor `micassandra`:

       `docker exec -it  micassandra cqlsh`

2. El comando anterior debería cambiarnos el prompt de la terminal a `cqlsh>`, permitiéndonos ejecutar comandos CQL sobre el contenedor.

## Conexión a Cassandra desde Visual Studio Code

Visual Studio Code es un editor de texto multiplataforma que además permite instalar extensiones que pueden llegar a convertirlo en un entorno de desarrollo completo. Entre otros, estas extensiones proporcionan soporte para distintos lenguajes de programación, para gestionar control de versiones, ejecutar/depurar programas, etcétera.

1. Instalar Visual Studio Code en tu equipo: https://code.visualstudio.com/Download

2. Instalar las siguientes extensiones:

   - [SQLTools](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools)  y [SQLTools Cassandra](https://marketplace.visualstudio.com/items?itemName=JordanHury.sqltools-cassandra): permiten conectarnos al nodo de Cassandra iniciado en el contenedor Docker
   - [CQL](https://marketplace.visualstudio.com/items?itemName=LawrenceGrant.cql): Proporciona coloreado de sintaxis, plantillas de escritura, etc.

Para instalar las extensiones, podéis buscarlas directamente en el buscador del editor:

   ![instalar extensiones](instalarextensiones.png)

   Si no os aparecen las extensiones, una segunda manera de instalarlas es mediante el comando proporcionado en los enlaces de las extensiones. Por ejemplo, para instalar SQL Tools, abrimos el menú rápido de Visual Studio Code (`Ctrl + P`) y escribimos `ext install mtxr.sqltools`

3. Configurar la conexión a Cassandra en el menú SQL Tools:
  ![configurar SQL tools](configurarSQLTools.png)

4. Ejecutar consultas: seleccionamos la consulta y hacemos click derecho -> ejecutar (o mediante el atajo de teclado doble [Control + E] + [Control + E]). Debe estar la conexión a Cassandra del punto anterior establecida:
   ![ejecutar consultas](ejecutarConsulta.png)
