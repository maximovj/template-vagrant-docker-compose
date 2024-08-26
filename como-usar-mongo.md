# Como usar MongoDB

Este en un pequeño tutorial de como usar MongoDB usando Docker + Ubuntu20.04 dentro de la caja de Vagrant 

# Requerimientos

En necesario instalar MongoDB cliente para poder probar MongoDB dentro de la caja de Vagrant.

Sigue estos pasos para instalar MongoDB cliente:

- Paso  1)

Actualizar repositorio para Ubuntu20.04 dentro de la caja de Vagrant.

ver https://www.mongodb.com/docs/mongodb-shell/install/

```shell
$ sudo apt-get update -qq -y
```

- Paso  2)

Instalar MongoDB cliente para Ubuntu20.04 dentro de la caja de Vagrant

```shell
$ sudo apt-get install gnupg
$ wget -qO- https://www.mongodb.org/static/pgp/server-7.0.asc | sudo tee /etc/apt/trusted.gpg.d/server-7.0.asc
$ echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
$ sudo apt-get update -qq -y
$ sudo apt-get install -y mongodb-mongosh
```

- Paso  3)

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

Es necesario ingresar la contraseña defina, en este caso ``root``

```shell
$ mongosh --host localhost --port 27017
```

- Paso 3) (2da forma)

Acceder al servicio de MongoDB dentro del contenedor docker

```shell
$ docker run -it --rm --link docker-servicio-mongodb mongo:6.0 mongo --host docker-servicio-mongodb
```