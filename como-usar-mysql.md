# Como usar Mysql

Este en un pequeño tutorial de como usar MySQL usando Docker + Ubuntu20.04 dentro de la caja de Vagrant 

# Requerimientos

En necesario instalar MySQL cliente para poder probar mysql dentro de la caja de Vagrant.

Sigue estos pasos para instalar MySQL cliente:

- Paso  1)

Actualizar repositorio para Ubuntu20.04 dentro de la caja de Vagrant

ver https://techiescode.com/how-to-install-mysql-client-on-ubuntu-20-04-lts/

```shell
$ sudo apt-get update
```

- Paso  2)

Instalar MySQL cliente para Ubuntu20.04 dentro de la caja de Vagrant

```shell
$ sudo apt-get install mysql-client
```

# Instrucciones (de 3 pasos)

- Paso 1)

Correr un contenedor docker con un servicio de MySQL.

Se define `root` como usuario y se define `root` como contraseña para acceder a MySQL.

```shell
$ docker run -d --name docker-servicio-mysql -e MYSQL_ROOT_PASSWORD=root -p 3306:3306 mysql:5.7
```

- Paso 2) (1era Forma)

Acceder al servicio de MySQL.

Es necesario ingresar la contraseña defina, en este caso ``root``

```shell
$ mysql -h127.0.0.1 -P3306 -uroot -p
```

- Paso 3) (2da forma)

Acceder al servicio de MySQL dentro del contenedor docker

```shell
$ docker run -it --rm --link docker-servicio-mysql mysql:5.7 mysql -hdocker-servicio-mysql -uroot -p
```

# Comandos básicos

Aquí tienes una lista de comandos básicos y esenciales para MySQL:

### Comandos Básicos de MySQL

1. **Conectar al Servidor MySQL**

   ```bash
   mysql -u <username> -p
   ```

   Por ejemplo, para conectarte como `root`:

   ```bash
   mysql -u root -p
   ```

   Después de ejecutar este comando, se te pedirá que ingreses la contraseña.

2. **Mostrar Bases de Datos**

   ```sql
   SHOW DATABASES;
   ```

3. **Seleccionar una Base de Datos**

   ```sql
   USE <database_name>;
   ```

   Por ejemplo:

   ```sql
   USE mydatabase;
   ```

4. **Mostrar Tablas en una Base de Datos**

   ```sql
   SHOW TABLES;
   ```

5. **Mostrar la Estructura de una Tabla**

   ```sql
   DESCRIBE <table_name>;
   ```

   Por ejemplo:

   ```sql
   DESCRIBE users;
   ```

6. **Crear una Nueva Base de Datos**

   ```sql
   CREATE DATABASE <database_name>;
   ```

   Por ejemplo:

   ```sql
   CREATE DATABASE mydatabase;
   ```

7. **Eliminar una Base de Datos**

   ```sql
   DROP DATABASE <database_name>;
   ```

   Por ejemplo:

   ```sql
   DROP DATABASE mydatabase;
   ```

8. **Crear una Nueva Tabla**

   ```sql
   CREATE TABLE <table_name> (
       column1_name column1_datatype,
       column2_name column2_datatype,
       ...
   );
   ```

   Por ejemplo:

   ```sql
   CREATE TABLE users (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(100),
       age INT
   );
   ```

9. **Eliminar una Tabla**

   ```sql
   DROP TABLE <table_name>;
   ```

   Por ejemplo:

   ```sql
   DROP TABLE users;
   ```

10. **Insertar un Nuevo Registro**

    ```sql
    INSERT INTO <table_name> (column1, column2, ...)
    VALUES (value1, value2, ...);
    ```

    Por ejemplo:

    ```sql
    INSERT INTO users (name, age)
    VALUES ('Alice', 30);
    ```

11. **Consultar Registros**

    ```sql
    SELECT column1, column2, ...
    FROM <table_name>
    WHERE condition;
    ```

    Por ejemplo:

    ```sql
    SELECT * FROM users WHERE age > 25;
    ```

12. **Actualizar Registros**

    ```sql
    UPDATE <table_name>
    SET column1 = value1, column2 = value2, ...
    WHERE condition;
    ```

    Por ejemplo:

    ```sql
    UPDATE users
    SET age = 31
    WHERE name = 'Alice';
    ```

13. **Eliminar Registros**

    ```sql
    DELETE FROM <table_name>
    WHERE condition;
    ```

    Por ejemplo:

    ```sql
    DELETE FROM users
    WHERE name = 'Alice';
    ```

14. **Mostrar los Registros Insertados**

    ```sql
    SELECT * FROM <table_name>;
    ```

    Por ejemplo:

    ```sql
    SELECT * FROM users;
    ```

### Comandos de Administración del Servidor MySQL

1. **Iniciar el Servidor MySQL**

   ```bash
   sudo systemctl start mysql
   ```

2. **Detener el Servidor MySQL**

   ```bash
   sudo systemctl stop mysql
   ```

3. **Reiniciar el Servidor MySQL**

   ```bash
   sudo systemctl restart mysql
   ```

4. **Verificar el Estado del Servidor MySQL**

   ```bash
   sudo systemctl status mysql
   ```

5. **Verificar la Configuración del Servidor**

   Puedes revisar la configuración en el archivo `/etc/mysql/my.cnf` o el directorio `/etc/mysql/`.

6. **Hacer un Backup de una Base de Datos**

   ```bash
   mysqldump -u <username> -p <database_name> > backup.sql
   ```

7. **Restaurar una Base de Datos desde un Backup**

   ```bash
   mysql -u <username> -p <database_name> < backup.sql
   ```

### Resumen

- **Conectar**: `mysql -u <username> -p`
- **Mostrar bases de datos**: `SHOW DATABASES;`
- **Seleccionar base de datos**: `USE <database_name>;`
- **Mostrar tablas**: `SHOW TABLES;`
- **Mostrar estructura de una tabla**: `DESCRIBE <table_name>;`
- **Crear base de datos**: `CREATE DATABASE <database_name>;`
- **Eliminar base de datos**: `DROP DATABASE <database_name>;`
- **Crear tabla**: `CREATE TABLE <table_name> (...);`
- **Eliminar tabla**: `DROP TABLE <table_name>;`
- **Insertar registro**: `INSERT INTO <table_name> (column1, column2, ...) VALUES (value1, value2, ...);`
- **Consultar registros**: `SELECT column1, column2, ... FROM <table_name> WHERE condition;`
- **Actualizar registros**: `UPDATE <table_name> SET column1 = value1 WHERE condition;`
- **Eliminar registros**: `DELETE FROM <table_name> WHERE condition;`
- **Backup**: `mysqldump -u <username> -p <database_name> > backup.sql`
- **Restaurar**: `mysql -u <username> -p <database_name> < backup.sql`

Estos comandos te proporcionarán una base sólida para trabajar con MySQL.