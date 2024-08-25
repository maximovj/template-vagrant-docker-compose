# Como usar Vagrant

# Comandos a usar desde el shell (Máquina HOST)

Para ver los boxes de maquinas virtuales instalados en el sistema

```shell
$ vagrant box list
```

Para iniciar la maquina virtual 

```shell
$ vagrant up
```

Para acceder a la maquina virtual

```shell
$ vagrant ssh
```

Utiliza esta información para conectarte directamente a la máquina virtual usando SSH:

```shell
$ ssh -p 2222 vagrant@127.0.0.1
```

Para apagar la maquina virtual

```shell
$ vagrant halt
```

Eliminar la máquina Vagrant: Esto eliminará la máquina virtual, incluidos todos los discos virtuales y configuraciones asociadas. <br/>
Si estás absolutamente seguro de querer eliminar todo sin confirmaciones, puedes usar el flag -f o --force para evitar que se te solicite la confirmación antes de eliminar.

```shell
$ vagrant destroy
```

Para volver ejecutar el script de Vagranfile

```shell
$ vagrant provision
```

Si quieres ejecutar varios provisionadores específicos en una sola ejecución, puedes listarlos separados por comas:

```shell
vagrant provision --provision-with shell, install-docker, install-docker-compose, install-tools, run-workspace, show-information
```

Sincronización de carpetas: Aunque ya está configurado en tu Vagrantfile, puedes forzar la sincronización de carpetas manualmente si es necesario.

```shell
$ vagrant rsync
```

Conectar puertos: Los puertos están configurados para reenvío automático, pero si es necesario, puedes forzar la conexión de puertos.

```shell
$ vagrant port
```

Ver el estado de la máquina Vagrant: Muestra el estado actual de la máquina virtual Vagrant.

```shell
$ vagrant status
```

Obtener la información de conexión SSH de la máquina virtual. Puedes encontrar la IP asignada a la máquina virtual en el archivo de configuración Vagrantfile bajo la sección config.vm.network.

```shell
$ vagrant ssh-config
```

# Comandos a usar desde el shell (Máquina GUEST)

Este comando sirve para construir un nuevo contenedor usando el archivo Dockerfile

```shell
$ docker build . -t <nombre-mi-contenedor>:<version/etiqueta>
```

Este comando sirve para correr un contenedor docker en segundo plano

```shell
$ docker run -d -p 3000:3000 <nombre-mi-contenedor>:<version/etiqueta>
```

Ver lista de imágenes de docker

```shell
$ docker images
```

Ver la lista de todos los contenedores de docker
```shell
$ docker ps -a
```
