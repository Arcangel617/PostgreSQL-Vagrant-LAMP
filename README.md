# PostgreSQL, phppgAdmin, Ubuntu 14.04 (trusty), Apache, MySQL y PHP5 en Vagrant

#### Consideraciones previas
- Se asume que [Vagrant](https://www.vagrantup.com/) ya está instalado en el sistema host. 

#### Requerimientos
- Vagrant
- Git

### Clonar el repositorio
```
$ git clone repository_url
```
### Instalación de Apache, MySQL y PHP5
```
$ sudo apt-get install lamp-server^
```
> **Nota:** No olvidarse del ^ al final.

### Instalación de PostgreSQL
```
$ sudo apt-get install postgresql postgresql-contrib
```
Agregamos soporte para el motor de base de datos
```
$ sudo apt-get install php5-pgsql
```
### Instalación de phppgAdmin
```
$ sudo apt-get install phppgadmin
```
Una vez instalado incluimos al final del archivo **/etc/apache2/apache2.conf** la siguiente línea:
```
Include /etc/apache2/conf.d/phppgadmin
```
> **Nota:** Pueden utilizar el editor o mecanismo que quieran.

guardamos y reiniciamos el servicio de apache:
```
$ sudo service apache2 restart
```
### Permitir acceso remoto
Para poder acceder desde otra pc tendremos que editar la configuración de phppgadmin. Para ello en el archivo **/etc/apache2/conf.d/phppgadmin** buscamos la siguiente línea:
```
allow from 127.0.0.0/255.0.0.0 ::1/128
# allow from all
```
y la editamos de tal forma que nos quede así:
```
# allow from 127.0.0.0/255.0.0.0 ::1/128
allow from all
```
### Creación de un nuevo rol
Para poder gestionar nuestras bases de datos lo mejor será crearnos un rol para postgres. Para ello dentro iniciamos sesión con el rol postgres de la siguiente manera:
```
$ sudo -i -u postgres
```
Si todo fue bien se nos devolverá un prompt como el siguiente:
```
postgres@vagrant-ubuntu-trusty-64:~$
```
ejecutamos la siguiente instrucción:
```
createuser --interactive -P nombre_de_tu_rol
```
> Como vamos a necesitar poder gestionar por completo nuestra base de datos, tendremos que crear un super usuario.  
> El flag **--interactive** nos solicitará una serie de datos.  
> El flag **-P** se  solicitará un password con el cual accederemos después.  
> **nombre_de_tu_rol** sería el usuario de nuestra base de datos.

Listo. Ya tenemos configurado postgres.
Para acceder bastará con ingresar a [http://localhost:8080/phppgadmin](http://localhost:8080/phppgadmin)
> **Nota:** El puerto variará en base a la configuración que cada uno decida utilizar para vagrant.