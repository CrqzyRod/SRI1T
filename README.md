# Juanma González Márquez - SRI - 2ASIR

### Instalación de servidor web interno.

#### 1. Instalación del servidor web apache. Usaremos dos dominios mediante el archivo hosts: centro.intranet y departamentos.centro.intranet. El primero servirá el contenido mediante wordpress y el segundo una aplicación en python.

![installapache](/objetos/installapache.png)

Como podemos ver ya tenemos Apache instalado y funcionando correctamente.

![installapache2](/objetos/installapache2.png)

Creamos los virtualhost de cada dominio usando mkdir nombre en la siguiente ruta: /var/www

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/ec316b79-07c8-45d3-8c36-eff808a7b59b)

Configuramos los siguientes parámetros de configuración del servidor

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/006625fb-15aa-4370-a6ef-5c5c2d741817)

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/098ae8a2-d42d-42a4-be14-438316e67b55)

Activamos los dos 

#### 2. Activar los módulos necesarios para ejecutar php y acceder a mysql.
Primero instalaremos mysql con el siguiente comando: apt install mysql-server

![installmysql](/objetos/mysqlinstall.png)

Para confirmar que está instalado escribimos en la línea de comando mysql y vemos como entramos en el programa, para luego salir del programa usamos exit.

![mysql2](/objetos/mysql2.png)

Para instalar php usamos el siguiente comando: apt install php libapache2-mod-php php-mysql.
Con libapache2-mod-php permitimos que Apache gestione archivos php y con php-mysql permitimos que php se comunique con las bases de datos de mysql.

![php](/objetos/php.png)

Para comprobar que está bien instalado usamos php -v para ver su versión

![php2](/objetos/php2.png)

Instala y configura wordpress.
Activar el módulo "wsgi" para permitir la ejecución de aplicaciones Python.
Crea y despliega una pequeña aplicación en Python para comprobar que fucniona correctamente.
Adicionalmente protegeremos el acceso a la aplicación Python mediante autenticación.
Instala y configura awstat.
Instala un segun servidor de tu elección (nginx, lighttpd) bajo el dominio "servidor2.centro.intranet". Debes configurarlo para que sirva en el puerto 8080 y haz los cambios para ejecutar php. Instala phpmyadmin.
