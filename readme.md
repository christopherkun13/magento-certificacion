# Docker Magento 2.4 Para Movistar

_Implementación proyecto Movistar Magento 2.4, Documento desarrollado por Magento Prime 🤖  y Team Rocket 🚀_

## Despliego Docker Primeros pasos

_Estas instrucciones te permitirán obtener una copia del proyecto en funcionamiento en tu máquina local para propósitos de desarrollo y pruebas._

_Tambien es importante que clonen el poryecto antes de realizar los pasos descritos mas adelante_

```
git clone http://git.tchile.local/ControlDeVersiones/Everis_MG-VentaEmpresas_MSS-108 movistar.test
```

_Editar archivo hosts_

```
Modificar Archivo
    - Windows   C:\Windows\System32\drivers\etc\hosts (Como Administrador)
    - MAC OS 	/private/etc/hosts
    - Linux     /etc/hosts

Agregar 

127.0.0.1   movistar.test
```


_Una vez clonado el repositorio configurar la terminal en la direccion del repositorio_

```
cd movistar.test
```


Mira **Deployment** para conocer como desplegar el proyecto.


### 1. Pre-requisitos 📋

1.1 Primero instalar Docker y Docker Compose en los siguientes links:

* Docker:  https://docs.docker.com/engine/install/ubuntu/#installation-methods
* Docker Compose: https://docs.docker.com/compose/install/

Para Windows:

* https://docs.docker.com/docker-for-windows/install/

Para Mac OSX:

* https://docs.docker.com/docker-for-mac/install/


1.2 Antes de realizar la ejecucion de _docker-compose_ revisar si no se encuentran los siguientes servicios en ejecución (_mysql_ _nginx_) dentro de tu equipo con el siguiente comando de Linux:

```
sudo service mysql status

sudo service nginx status
```

El comando te muestra en color verde si se encuentra funcionando, para deshabilitarlo utilizar lo siguiente:

```
sudo service mysql stop

sudo service nginx stop
```

En caso de tener instalado Valet, detener el servicio

```
valet stop
```

### 2. Compilación 🔧
2.0 Ingresar al directorio VentaEmpresa_web 
```
    cd VentaEmpresa_web
```
2.1 Crear los siguientes directorios dentro de la carpeta _src_ con la siguiente linea

```
    mkdir -p ./src/es_data1 ./src/es_log1 ./src/mysql_data1 ./src/mysql_log1 ./src/nginx_log1 ./src/phpfpm_log1 ./src/redis_data1 ./src/sock_data1
```
2.2 Completado los puntos anteriores, procedemos con la ejecución del docker-compose.yml de la siguiente manera:
    

```
./shell/build
```

2.3 Para validar que los contenedores esten ejecutados correctamente 

```
docker-compose ps
```
_Todos los contenedores deben estar en status UP_ 

2.4 Instalar dependencias de Magento

```
./shell/composer install
```

2.5 Copiar la base de datos (Solicitar a lider tecnico o alguien del equipo una copia de la base de datos)

```
./shell/mysql_load name_db file.sql
```

2.6 Copiar el siguiente archivo en src/app_magento/app/etc y renombrarlo como env.php

```
env.php.example.magento
```

2.7 Ejecutar un setup:upgrade

```
./shell/magento se:up
```

2.8 Cree un usuario para el administrador de magento

El siguiente comando le solicitará los siguientes datos _nombre de administrador_, _contraseña_, _email_, _firstname_, _lastname_ que debes ir ingresandolos cada vez que se te lo solicita, en caso de que no ingreses algunos de estos datos NO se ejecutara el comando interno dentro de este script.

```
./shell/create_user_magento
```

2.9 Finalmente ingresar a las siguiente rutas:

* [http://movistar.test](http://movistar.test)
* [http://movistar.test/admin](http://movistar.test/admin)

## 3. Scripts

Todos los script se encuentran dentro de la carpeta shell
#### Los siguientes comando son ejemplos de ejecución

* build: Ejecuta el script de docker-compose y levanta los contenedores

```
./shell/build
```
* composer: Permite ejecutar todas las instrucciones de composer

```
./shell/composer --version
```
* create_user_magento: Crea usuario administrador de magento (revisar punto 2.8)

```
./shell/create_user_magento 
```
* magento: Permite ejecutar todas las instrucciones de magento

```
./shell/magento cache:clear
```
* mysql_export: Permite crear un dump de la base de datos

```
./shell/mysql_export nombre_db
```
* mysql_load: Permite importar la base de datos

```
./shell/mysql_load dbname path_file.sql
```
* restart: Reinicia los contenedores
```
./shell/restart
```
* start: Inicia los contenedores

```
./shell/start
```
* stop: Detiene los contenedores

```
.shell/stop
```
## 4. Construido con 🛠️

_Menciona las herramientas que utilizaste para crear tu proyecto_

* [Visual Studio Code](https://code.visualstudio.com/) - El framework web usado
* [Docker](https://hub.docker.com/) - Documentación y referencias
* [Docker extension] - Visualización y administración de contenedores


## 5. Autores ✒️

_Menciona a todos aquellos que ayudaron a levantar el proyecto desde sus inicios_

* **Gustavo Vazquez** - 
* **Christopher Bueno** - 
* **Daniel Gómez** -
* **Yoselin Chavez** - 
* **Diego Oyarzo** - 


---
⌨️ con ❤️ por Team Docker 🤖 🚀
