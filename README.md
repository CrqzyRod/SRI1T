# Juanma González Márquez - SRI - 2ASIR

### Instalación de servidor web interno.

#### 1. Instalación del servidor web apache. Usaremos dos dominios mediante el archivo hosts: centro.intranet y departamentos.centro.intranet. El primero servirá el contenido mediante wordpress y el segundo una aplicación en python.

![installapache](/objetos/installapache.png)

Como podemos ver ya tenemos Apache instalado y funcionando correctamente.

![installapache2](/objetos/installapache2.png)

Creamos los virtualhost de cada dominio usando mkdir nombre en la siguiente ruta: /var/www

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/ec316b79-07c8-45d3-8c36-eff808a7b59b)

Añadimos un fichero index.html en cada que será la pagina principal de nuestro dominio

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/9bc2f3df-a7b3-42d3-b6a1-4edd1de10cf8)

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/4a79a1de-5848-4835-b500-2f1a68ed5a00)

Configuramos los siguientes parámetros de configuración del servidor

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/eaa5a8a9-084b-4bbf-997f-85cf4cea6002)

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/f9eedf82-381f-4cb7-81ef-cb896dd0ed95)

Habilitamos los hosts con el siguiente comando: a2ensite hosts.
Luego usamos systemctl reload apache2 para reiniciar apache.

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/3f961d88-9d6f-4789-845a-dfcdd9140fa3)

Añadimos los dominios al fichero hosts

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/08dea050-7c58-49bc-8185-143f479fd4af)

Si ingresamos el dominio que hemos añadido en un navegador podemos ver el contenido que hay en el fichero creado anteriormente.

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/32273f78-162e-4841-ae07-4ea17448a509)

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/2faefa8c-57f0-4216-9743-ceeefe0789ae)

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

#### 3. Instala y configura wordpress.
Empezaremos iniciando sesión con el usuario root en mysql. Con el parámetro -u indicamos el usuario y con -p indicamos que nos solicite contraseña.

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/5ab74f4f-259d-4dac-bb06-4e94a5c678f1)

Una vez logeados introducimos el siguiente comando para crear nuestra base de datos en la cual almacenaremos el sitio al que vamos a servir. 

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/ed9e0239-5506-46b6-a11b-e68eea9458f3)

Creamos el usuario que será el administrador de la base de datos. El primer parámetro es el nombre del usuario, seguido de la máquina con la que podremos acceder, si usamos % tendremos acceso desde todas las máquinas, y con identified by establecemos la contraseña.

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/1e54933d-47c7-481c-af09-bd4c10cb347e)

Ahora daremos permisos al usuario en la base de datos

Activar el módulo "wsgi" para permitir la ejecución de aplicaciones Python.
Crea y despliega una pequeña aplicación en Python para comprobar que fucniona correctamente.
Adicionalmente protegeremos el acceso a la aplicación Python mediante autenticación.
Instala y configura awstat.
Instala un segun servidor de tu elección (nginx, lighttpd) bajo el dominio "servidor2.centro.intranet". Debes configurarlo para que sirva en el puerto 8080 y haz los cambios para ejecutar php. Instala phpmyadmin.
