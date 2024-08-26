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