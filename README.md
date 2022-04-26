# monitorizar

 
 # CHECKMK
 ![image](https://user-images.githubusercontent.com/94168011/165063328-b8fde21d-4f62-4e37-8d85-a55de91efad8.png)
 ![image](https://user-images.githubusercontent.com/94168011/165064102-16daba08-4348-4aee-bb7a-e32074a27eed.png)
# ZABBIX
![image](https://user-images.githubusercontent.com/94168147/165064331-6caea90e-eb72-4d93-b4d2-1e072a07ab94.png)






| Herramienta | Licencia | Panel web | Instalacion | Mapa de red | Comunidad | Reglas Preconfiguradas | Dashboard Configurable | Configuracion de Plugins | Alertas | Multiplataforma |
:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|
 **`ZABBIX`** | COMMUNITY | SI | FÁCIL | SI | ACTIVA | MÚLTIPLES REGLAS | ALTA CONFIGURACIÓN | SI | SI | WINDOWS/LINUX |
 **`CHECKMK`** | COMMUNITY/ENTERPRISE| SI  | FÁCIL | SI | ACTIVA | MÚLTIPLES REGLAS | ALTA CONFIGURACIÓN | SI | SI | LINUX |

---------------------------------------------------------------------------------------------

# INSTALACIÓN DE ZABBIX
## Instalar el repositorio de Zabbix:
```
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-1+ubuntu20.04_all.deb
dpkg -i zabbix-release_6.0-1+ubuntu20.04_all.deb
apt update
```
## Instala el servidor, la interfaz y el agente de Zabbix:
```
apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```
## Crear base de datos inicial:
```
mysql -uroot -p
**password**
mysql> create database zabbix character set utf8mb4 collate utf8mb4_bin;
mysql> create user zabbix@localhost identified by 'password';
mysql> grant all privileges on zabbix.* to zabbix@localhost;
mysql> quit;
```
## En el servidor Zabbix, importe el esquema y los datos iniciales:
```
zcat /usr/share/doc/zabbix-sql-scripts/mysql/server.sql.gz | mysql -uzabbix -p zabbix
```
## Configurar la base de datos para el servidor Zabbix:
Editar archivo /etc/zabbix/zabbix_server.conf
```
DBPassword=password
```
## Inicia los procesos del agente y del servidor Zabbix:
Inicia los procesos del agente y del servidor Zabbix y configúralos para que se inicien con el sistema.
```
systemctl restart zabbix-server zabbix-agent apache2
systemctl enable zabbix-server zabbix-agent apache2
```
## Configurar la interfaz de Zabbix:
Conéctate a tu interfaz Zabbix recién instalada: http://server_ip_or_name/zabbix
![image](https://user-images.githubusercontent.com/94168147/165143989-6f90876f-76c8-49cb-b37c-90ef25418215.png)

# INSTALACIÓN CHECKMK
Para la instalacion nos dirigimos a la pagina de la aplicacion en cuestion Checkmk y escogemos el sistema operativo sobre el que se va a realizar la instalacion.
![image](https://user-images.githubusercontent.com/94168011/165365853-8ac40f2d-4005-4ef4-8e4c-6eb8d4e50abf.png)

## Una vez descargado comenzamos la instalacion del programa:
```
sudo apt install ./check-mk-raw-1.6.0p27_0.focal_amd64.deb
```
## Creacion del servidor de monitorizacion.
```
sudo omd create prueba
```
![image](https://user-images.githubusercontent.com/94168011/165368541-f92dd2f8-479f-4845-8cc9-184d7bbc0814.png)

## tras crear el servidor dependiendo de los hosts que tengas eliges el sistema operativo y te bajas el agente de la pagina creada anteriormente.
![image](https://user-images.githubusercontent.com/94168011/165369312-bd973648-a386-4ba3-8fda-d2deed8e674a.png)

## elegimos el SO que necesitemos.
![image](https://user-images.githubusercontent.com/94168011/165369427-4738b748-1a1c-4155-9c1a-a515a4bf0dc3.png)
Instalamos el agente en la maquina a escanear y lo añadimos a nuestro servidor de monitorización.


