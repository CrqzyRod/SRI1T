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
##### Empezaremos configurando la base de datos.Iniciamos sesión con el usuario root en mysql. Con el parámetro -u indicamos el usuario y con -p indicamos que nos solicite contraseña.

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/5ab74f4f-259d-4dac-bb06-4e94a5c678f1)

Una vez logeados introducimos el siguiente comando para crear nuestra base de datos en la cual almacenaremos el sitio al que vamos a servir. 

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/ed9e0239-5506-46b6-a11b-e68eea9458f3)

Creamos el usuario que será el administrador de la base de datos. El primer parámetro es el nombre del usuario, seguido de la máquina con la que podremos acceder, si usamos % tendremos acceso desde todas las máquinas, y con identified by establecemos la contraseña.

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/1e54933d-47c7-481c-af09-bd4c10cb347e)

Ahora daremos permisos al usuario en la base de datos.

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/d3fd7270-b47e-4dd9-935f-bdaf151fbaf3)

Una vez configurado todo usamos el comando FLUSH PRIVILEGES para hacer un reinicio y se apliquen los cambios.

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/e1bc5662-ffaf-4c31-a5ca-bae5ddaf69df)

##### Instalamos extensiones adicionales de PHP.

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/e94bd0c1-497a-4dfc-827f-4b63b0032b19)

##### Configuración de apache para permitir reemplazos y reescrituras .htaccess.

Entramos en el fichero de configuración del virtualhost y escribimos el siguiente comando para permitir archivos .htaccess.

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/1fad591e-4d0f-4d69-add4-9528f50afdd9)

Habilitamos el módulo de reescritura usando el siguiente comando.

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/d9e7c0c5-4d38-4d78-8463-acf78a2e3eea)

Una vez habilitados los cambios, para verificar que no hay errores, usamos apache2ctl configtest,es posible que nos salga este error, no afectaría a la funcionalidad del sitio, si queremos corregirlo, debemos agregar una directiva ServerName en el archivo de configuración principal de apache en /etc/apache2/apache2.conf.

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/0ed30f07-e89b-4ebf-8c08-93bba7182f29)

##### Descarga de Wordpress
Para descargar WordPress nos situamos en la carpeta que queramos descargarlo e introducimos la siguiente línea de comando. Luego lo descargamos usando tar.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/78b47cc6-27e0-40ff-ad0a-0ba65a583fce)

Vamos a crear un archivo para añadir los ficheros creados anteriormente.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/1498d1d2-ca34-41f4-8a10-a53b02b8ba73)

Copiaremos el archivo de configuración que lee WordPress usando el de muestra que trae.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/4af85c9e-8a09-4014-9b9e-1b63c4ee0f36)

Activar el módulo "wsgi" para permitir la ejecución de aplicaciones Python.
Crea y despliega una pequeña aplicación en Python para comprobar que fucniona correctamente.
Adicionalmente protegeremos el acceso a la aplicación Python mediante autenticación.
Instala y configura awstat.
Instala un segun servidor de tu elección (nginx, lighttpd) bajo el dominio "servidor2.centro.intranet". Debes configurarlo para que sirva en el puerto 8080 y haz los cambios para ejecutar php. Instala phpmyadmin.
