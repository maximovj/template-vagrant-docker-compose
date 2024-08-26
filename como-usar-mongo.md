# Como usar MongoDB

Este en un pequeño tutorial de como usar MongoDB usando Docker + Ubuntu20.04 dentro de la caja de Vagrant

# Requerimientos

En necesario instalar MongoDB cliente para poder probar MongoDB dentro de la caja de Vagrant.

Sigue estos pasos para instalar MongoDB cliente:

- Paso 1)

Actualizar repositorio para Ubuntu20.04 dentro de la caja de Vagrant.

ver https://www.mongodb.com/docs/mongodb-shell/install/

```shell
$ sudo apt-get update -qq -y
```

- Paso 2)

Instalar MongoDB cliente para Ubuntu20.04 dentro de la caja de Vagrant

```shell
$ sudo apt-get install gnupg
$ wget -qO- https://www.mongodb.org/static/pgp/server-7.0.asc | sudo tee /etc/apt/trusted.gpg.d/server-7.0.asc
$ echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
$ sudo apt-get update -qq -y
$ sudo apt-get install -y mongodb-mongosh
```

- Paso 3)

Verificar la instalación de MongoDB

```shell
$ mongosh --version
```

# Instrucciones

- Paso 1)

Correr un contenedor docker con un servicio de MongoDB.

Se define `root` como usuario y se define `root` como contraseña para acceder a MongoDB.

```shell
$ docker run -d --name docker-servicio-mongodb -p 27017:27017 mongo:6.0
```

- Paso 2) (1era Forma)

Acceder al servicio de MongoDB.

Es necesario ingresar la contraseña defina, en este caso `root`

```shell
$ mongosh --host localhost --port 27017
```

- Paso 3) (2da forma)

Acceder al servicio de MongoDB dentro del contenedor docker

```shell
$ docker run -it --rm --link docker-servicio-mongodb mongo:6.0 mongo --host docker-servicio-mongodb
```

# Comandos básicos

Aquí tienes una lista de comandos básicos y esenciales para MongoDB, tanto en la línea de comandos del `mongo` shell como para la administración del servidor MongoDB:

### Comandos Básicos del `mongo` Shell

1. **Conectar al Servidor MongoDB**

   ```bash
   mongo --host <host> --port <port>
   ```

   Por ejemplo, para conectarte a un contenedor en tu máquina local:

   ```bash
   mongo --host 127.0.0.1 --port 27017
   ```

2. **Mostrar Bases de Datos**

   ```javascript
   show dbs
   ```

3. **Seleccionar una Base de Datos**

   ```javascript
   use <database_name>
   ```

   Por ejemplo:

   ```javascript
   use mydatabase
   ```

4. **Mostrar Colecciones en una Base de Datos**

   ```javascript
   show collections
   ```

5. **Crear una Colección y Insertar Documentos**

   ```javascript
   db.<collection_name>.insertOne({ key: "value" })
   ```

   Ejemplo:

   ```javascript
   db.users.insertOne({ name: "Alice", age: 30 });
   ```

6. **Consultar Documentos**

   ```javascript
   db.<collection_name>.find()
   ```

   Para obtener documentos con una condición:

   ```javascript
   db.users.find({ age: { $gt: 25 } });
   ```

7. **Actualizar Documentos**

   ```javascript
   db.<collection_name>.updateOne({ query }, { $set: { key: "new_value" } })
   ```

   Ejemplo:

   ```javascript
   db.users.updateOne({ name: "Alice" }, { $set: { age: 31 } });
   ```

8. **Eliminar Documentos**

   ```javascript
   db.<collection_name>.deleteOne({ query })
   ```

   Ejemplo:

   ```javascript
   db.users.deleteOne({ name: "Alice" });
   ```

9. **Eliminar una Colección**

   ```javascript
   db.<collection_name>.drop()
   ```

   Ejemplo:

   ```javascript
   db.users.drop();
   ```

10. **Eliminar una Base de Datos**

    ```javascript
    db.dropDatabase();
    ```

    Debes estar en la base de datos que deseas eliminar antes de ejecutar este comando.

### Comandos de Administración del Servidor MongoDB

1. **Iniciar el Servidor MongoDB**

   ```bash
   sudo systemctl start mongod
   ```

2. **Detener el Servidor MongoDB**

   ```bash
   sudo systemctl stop mongod
   ```

3. **Reiniciar el Servidor MongoDB**

   ```bash
   sudo systemctl restart mongod
   ```

4. **Verificar el Estado del Servidor MongoDB**

   ```bash
   sudo systemctl status mongod
   ```

5. **Verificar la Configuración del Servidor**

   ```bash
   mongod --config /etc/mongod.conf --verbose
   ```

6. **Verificar el Log del Servidor MongoDB**

   Puedes revisar los logs en `/var/log/mongodb/mongod.log` (o en la ubicación especificada en tu archivo de configuración).

7. **Hacer un Backup de una Base de Datos**

   ```bash
   mongodump --db <database_name> --out /path/to/backup
   ```

8. **Restaurar una Base de Datos desde un Backup**

   ```bash
   mongorestore --db <database_name> /path/to/backup/<database_name>
   ```

### Resumen

- **Conectar**: `mongo --host <host> --port <port>`
- **Mostrar bases de datos**: `show dbs`
- **Seleccionar base de datos**: `use <database_name>`
- **Mostrar colecciones**: `show collections`
- **Insertar documento**: `db.<collection_name>.insertOne({ key: "value" })`
- **Consultar documentos**: `db.<collection_name>.find()`
- **Actualizar documento**: `db.<collection_name>.updateOne({ query }, { $set: { key: "new_value" } })`
- **Eliminar documento**: `db.<collection_name>.deleteOne({ query })`
- **Eliminar colección**: `db.<collection_name>.drop()`
- **Eliminar base de datos**: `db.dropDatabase()`

Estos comandos te ayudarán a manejar y administrar MongoDB de manera efectiva.