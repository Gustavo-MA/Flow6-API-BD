# Flow6-API-BD
Apartir de Flow5, se crea un Flow para guardar los dato de API en una BD con datos desde OpenWeather I

Introduccion

Se crea un flow en notered que es capaz de obtener los datos de temperatura y clima medante un portal web OpenWeather de donde se obtiene los datos climatologicos que posterioermente pondran ser graficados en un dashboard de nuestra computadora mediante un notered. Posterior a ello se conecta a un broquer publico para mostrar los datos de todos los participantes.

Ubuntu 20.04 NodeJS NPM NodeRed Nodos Dashboard

Instrucciones y requisitos previos (Previamente instalados)

Para que el flow arranque , se deben instalar los siguientes requisitos:

Instalación de NodeJS. Se recomienda tener instalado NodeJS en alguna versión LTS. Al momento de creación de este documento, se usó la versión 16.17.0LTS. Esta instalación debe incluir las Build-Tools para hacer uso de NPM Instalación de NodeRed. La instalación se realiza por NPM. Al momento de la creación de este contenido, se usó la versión 3.0.2

-sudo apt install curl curl -curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash - sudo apt-get install -y nodejs sudo apt-get install -y bulid -esential sudo npm install -g -unsite-perm node-red node red --version

Instrucciones de preparación del entorno Para ejecutar este flow, Se clona el fow5 y se renombra como flow6 --> Clima por API-Base de Datos: 
Se aprovechan las variables globales del flow anterior.
Y se agregan un TimeStamp  Una funcion llamada QUery y una entidad BD, como se muestra en la siguiente imagen:


![image](https://user-images.githubusercontent.com/111370930/189792013-65c089f1-aceb-4814-8b2c-6daf5a36f0a1.png)


Se instala MySQL
con los siguientes comandos:
sudo apt update
- sudo apt install mysql-server
y se genera una base de datos llamada codigoIoT;
se usa la base de datos con la instruccion use codigoIoT
y dentro de  esta base en uso se crea una tabla clima con los siguientes columnas:
Conn el comando:
create table clima (id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY, fecha TIMESTAMP DEFAULT CURRENT_TIMESTAMP, nombre VARCHAR (248) NOT NULL, temperatura FLOAT (4,2) NOT NULL, humedad INT (3) NOT NULL);

![image](https://user-images.githubusercontent.com/111370930/189792114-978cde60-3d4e-4fcc-b847-e091abfcd36f.png)

Para conectar  la base de datos se debe de crear un usuario, con los comandos:

create user 'angel'@'localhost' identified by '1234';

Y se le otorgan los privilegios correspondientes al usuario raiz:
- grant all privileges on *.* to 'angel'@'localhost';

Para configurar la base de datos se debe configurarar nuestra entidad, indicar la base de datos asi como el usario al cual va acceder, ctal como se muestra en la siguiente imagen:
![image](https://user-images.githubusercontent.com/111370930/189792802-ed67548e-c0ee-455a-bd94-45daf0c797ae.png)

Donde indicaremos el host, el puerto, el usuario y la contraseña anteriormente configuradas.
