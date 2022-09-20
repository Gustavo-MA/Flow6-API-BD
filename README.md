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
Tambien configuramos nuestra funcion Query, para poder realizar las inserciones en nuestra base de datos: en esta pondremos las instrucciones:

msg.topic="INSERT INTO clima(`Nombre`,`Temperatura`,`Humedad`) VALUES ('Gustavo',"+global.get("tempAPI") +","+global.get("humAPI")+");";

return msg;
![image](https://user-images.githubusercontent.com/111370930/189793240-50cb6ff5-ed11-40c0-9eba-ea3a5b1e6efa.png)

RESULTADOS:

Hacemos Deploy y por ultimo nos dirigimos a nuestra tabla para seleccionar los datos que se han insertado para visualizar los resultados.
POdemos observar en la sigiuente imagen los resultados en consola que se insertaron  a nuestra tabla clima por medio de nuestro Flow6.
En donde se muestran los datos insertados del clima obtenidos previamente del API del flow clonado y la fecha de registro en el cual se inserto
el dato:
![image](https://user-images.githubusercontent.com/111370930/189793688-1a96f80d-0f34-42c3-8d4e-9916e284b686.png)


GRAFANA
Grafana es una interfaz que nos permite  vizualizar datos, en nuestro caso particular, los datos que existen en nuestra DB de clima anteriormente creada en nuestra base codigoIoT.

Instalacion.

- sudo apt-get install -y adduser libfontconfig1
- wget https://dl.grafana.com/enterprise/release/grafana-enterprise_9.1.4_amd64.deb
- sudo dpkg -i grafana-enterprise_9.1.4_amd64.deb

Para arrancar por primera vez se teclea en la terminal:

sudo /bin/systemctl daemon-reload
- sudo /bin/systemctl enable grafana-server
- sudo /bin/systemctl start grafana-server

Para arrancar grafana:
-- sudo /bin/systemctl start grafana-server

Para abrir el entonrno de grafana ponermos en el navegador web:
- localhost:3000

Iniciar sesion
- User: admin
- Password: admin
- Nueva contraseña: hugohugo

Serealiza la configuracion en Graffana de la BD:


Para poder agregar las graficas a nuestro dashboard de note-red se tiene el codigo embed de cada panel
dando clic sobre compartir (share/embed) y coopiar el codigo se muestra,

Y posteriormente copiar este codigo en: nodo Template en el Flow de NodeRed, en mi caso es:

<iframe src="http://localhost:3000/d-solo/uS4153MVz/climaporapi?-orgId=1&from=1662996598509&to=1663082998509&panelId=2"width="1000" height="700" frameborder="0"></iframe>
Ver captura de pantalla:


tambien  tenemos que editar la configuracion de grafana para permitir la vizualizacio en el navegador configurando el archivo:
 grafana.ini que se encuentra en /etc/grafana

y descomentar y modificar la instruccion:

- allow_embed = true



Podemos vizualizar como ahora al realizar deploy en nuestro dashboard, se vizualizan los datos de Granada de los datos previos obtenidos de nuestra BD.


Realizamos la misma accion para los nodos de temperatrua y clima repitiendo los pasos antertiores en grafana:

Por ultimo podemos modificar la sentencia de los bloques where para que nos muestre solo los datos de algun usuario especifico en indicadores gauch,
se muesrta la presentacion final de los dashboard con datos del embed de grafana:





Evidencias

Repositorio github:https://github.com/Gustavo-MA/Flow6-API-BD/blob/main/README.md

Créditos

Desarrollado por Gustavo Medina e-mail: gustavo.medina@uaem.edu.mx

