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

Creamos el archivo en el que se instalar las actualizaciones de Wordpress para que si Wordpress tuviera que hacerlo por su cuenta no tuvieramos problemas con los permisos.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/27c0616f-4353-488f-9b4f-0cd6c1968617)

##### Configurar el directorio de WordPress
Primero damos permisos al usuario y al grupo www-data que es el que puede escribir archivos de WordPress.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/e04658ad-066e-4164-a52e-681525a69ab0)

Establecemos los permisos a directorios y ficheros de wordpress.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/c8c0c262-b93c-45bf-aa06-1c09befdb64f)

Ahora vamos a configurar unos cambios en el archivo de configuración principal de WordPress. Vamos a ajustar las claves secretas para proporcionar más seguridad a nuestra instalación. WordPress tiene un generador de estos valores, usaremos el siguiente comando para ejecutarlo.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/6c47da23-ffa0-4e5a-9cab-9c24b8222d74)

Ahora copiamos estos valores en el archivo de configuración de WordPress. Lo abrimos con nano.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/181f2563-b83f-42ed-8770-3f9eba1e391f)

Buscamos el apartado en el que se encuentran los valores y los copiamos.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/54cbd77f-a875-4614-acf1-674e101c6d1a)

Ahora vamos a ajustar los parámetros de nuestra base de datos en el fichero de configuración. Añadiremos nuestro nombre, usuario y contraseña creados anteriormente. También agregaremos otra línea la cual indica la forma en la que escribirá WordPress en el sistema de archivos.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/623552e3-7074-4293-aab7-48163e73efcc)

Una vez completado todo si entramos en un navegador usando el dominio creado, se nos abrirá la interfaz gráfica de configuración de WordPress.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/e6344ccd-aed9-41d7-be5d-16e936d7767a)

Rellenamos los campos con nuestros datos y pulsamos instalar.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/3972ac1c-cc2a-4f4a-858b-e5147b52de6b)

Se nos ha instalado WordPress y ahora podemos iniciar sesión.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/c57d4bb2-0d18-4293-9385-360fcf3a07f5)

Al iniciar sesión entramos en la interfaz gráfica de configuración de páginas web WordPress.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/64f6e27d-c660-4ee0-a1ea-61360c93343c)

##### 4.Activar el módulo "wsgi" para permitir la ejecución de aplicaciones Python.

Primero haremos que Apache incorpore un soporte para servir archivos Python, para ello ejecutaremos la siguiente línea de comandos.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/fec4e96c-ee34-4859-b9f6-75cffab69961)

Una vez activado el módulo reiniciamos Apache para aplicar los cambios.

##### 5.Crea y despliega una pequeña aplicación en Python para comprobar que funciona correctamente.

Antes de crear y desplegar la aplicación en Python tenemos que crear los directorios necesarios. Debemos tener un directorio principal destinado a montar toda la aplicación en el cuál añadiremos los distintos directorios de configuración. La arquitectura de este directorio estára dividida en dos partes.
1.  Estará destinada al almacenaje de nuestra aplicación Python y será un directorio privado.
2.  Estará destinada a servir el contenido siendo un directorio público en el cuál almacenaremos archivos estáticos.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/f7dfbf09-791b-4521-aa9d-28647507da4e)

Así quedaría la estructura de nuestro directorio departamentos.centro.intranet.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/9e0edf3e-55d9-40c1-b93e-be862163574b)

Ahora crearemos un controlador que será un archivo almacenado en nuestro directorio pythonapp, el cual se encargue de las peticiones realizadas por el usuario. Lo crearemos usando el editor de texto nano.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/b9103183-4ec8-4606-aaf2-231504ed04b9)

Configuración del virtualhost. 

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/48c7e8a6-25f4-4ecd-a63b-e6a60a223451)

Una vez configurado el virtualhost habilitamos el sitio web y recargamos apache.

Si accedemos en un navegador con nuestro dominios podemos ver como el texto escrito anteriormente en el fichero controller aparece por pantalla.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/f262ec5f-c1b4-44d5-8963-d4d73544cd0b)

##### 6.Adicionalmente protegeremos el acceso a la aplicación Python mediante autenticación.

Para poder proteger el acceso a la aplicación de Python tenemos que instalar primero el paquete de utilidades de Apache. En mi caso ya lo tengo y por eso me sale el siguiente mensaje diciendo que ya está instalado en su versión más reciente.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/90664987-878c-44de-a55d-66ed41b680d2)

Ahora crearemos el archivo de la contraseña usando el comando htpasswd. La primera vez que se use este comando debemos añadir la opción -c para crear el passwdfile. Para ello especificamos un nombre de usuario que será el que usaremos más tarde para autenticarnos en la aplicación Python. En mi caso crearé una carpeta llamada password en los archivos de configuración del dominio departamentos.centro.intranet.

juanma será el nombre con el que nos autenticaremos y luego nos pedirá que repitamos la contraseña

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/78ef306e-e751-4bb4-bdee-4c8d6dd507fd)

Si visualizamos el contenido de la carpeta donde hemos guardado la contraseña podemos ver el nombre de usuario que hemos creado y junto a él la contraseña cifrada.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/8805a5ea-fd9f-4b66-baf9-e77c8d06f5be)

Ahora configuraremos el virtualhost para añadir la siguiente directiva.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/2e57cc5b-d8a2-4972-9ccd-273878d64cb8)

Si entramos en nuestra aplicación web nos sale la siguiente ventana para introducir nuestras credenciales.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/b2ee9d98-595a-45c1-a202-c03b9371e7cd)

##### 7.Instala y configura awstat.

Instalamos awstat con el comando apt-get install awstats

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/1516b272-e764-4e26-bfb2-82b94bf25a5a)

Si usamos el siguiente comando en la consola y accedemos desde el navegador a nuestro dominio podemos ver las estadísticas.

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/c26a0e2f-6236-47d8-b6e7-8945be29763c)

Configuramos el archivo de configuración awstats en Apache con los siguientes parámetros y reinciamos Apache.

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/eb5c2301-d883-42c4-b34a-e93724e79469)

Copiamos el archivo de configuración por defecto de awstats para cada servidor en el que lo queramos añadir. Configuramos los siguientes parámetros dentro del fichero usando nano para poder editarlo. Editaremos LogFile,SiteDomain y HostAliases.

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/4aa6564f-5b7e-44f5-bc88-bfced5106c1e)

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/09fafd6e-6a7d-4470-be05-fc984aabd450)

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/fbb2bfac-9f8a-4a53-a47e-9ad45d6faa81)

Ahora ejecutararemos el siguiente comando para actualizar los ficheros.

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/846b689c-0716-42ea-ac77-d849f0c4c564)

Finalmente si entramos en la ruta establecida de nuestro dominio podemos ver todas las estadísticas que se muestran.

![image](https://github.com/CrqzyRod/SRI1T/assets/122454007/8ef944d1-b62f-40d7-b12a-7ecdf1407199)

##### 8.Instala un segundo servidor de tu elección (nginx, lighttpd) bajo el dominio "servidor2.centro.intranet". Debes configurarlo para que sirva en el puerto 8080 y haz los cambios para ejecutar php. Instala phpmyadmin.
Para instalar nginx usamos el siguiente comando
![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/ed09e303-cb99-4ea6-b93a-c5b31f8b2200)

Lo iniciamos
![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/2d13d2ea-0081-40ce-9652-e4fae8ef25cc)

Modificamos el archivo hosts

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/03ff2e21-c6ab-47d5-bca8-9b25fed42e6f)

Modificamos el puerto en el que va a servir y la ruta donde se encuentra
![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/452fab42-6369-41e4-9c5d-47fd0482144b)

Si entramos con el dominio y el puerto que hemos añadido podemos ver como carga nginx

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/0eedf402-556b-4ea5-8310-2793ae7b5e83)

Instalamos los siguientes paquetes para instalar mysql y php

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/74d397c7-ba29-487c-951d-da9cd116194c)

Modificamos el siguiente fichero de configuración

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/51d88266-1a54-4c58-894d-79d3efd159c0)

Si entramos de nuevo después de haber modificado el fichero de configuración de nginx y activando las siguientes líneas podemos ver como muestra la información de php.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/6c435930-9871-4a6c-938c-912cd29283b2)

Usamos el siguiente comando para instalar phpmyadmin.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/caee3af2-12a7-481a-93a3-f368b356421b)

Una vez introducido el código damos aceptar sin marcar nada

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/edeeb4b6-aa71-4984-a3f2-a536c4737f19)

Le damos a sí

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/6748a320-0e4d-48d5-b442-7020952818c9)

Creamos un enlace simbólico en la ruta donde se encuentre nuestro directorio.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/aa9bb896-b389-4a16-8de2-1b819b2707a0)

En el fichero de configuración del servidor nginx añadimos index.php

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/28a7339d-ef63-4680-a04a-cc3eb54dd45b)

Si entramos en un navegador en el dominio configurado anteriormente añadiendo /phpmyadmin podemos entrar en la página de phpmyadmin.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/98c16511-449c-4dd5-b3b3-0daf3ce9ced2)

Si introducimos nuestros datos podemos acceder y visualizar la base de datos que hemos creado anteriormente.

![imagen](https://github.com/CrqzyRod/SRI1T/assets/122454007/171c6516-aa1e-46b0-a3f6-119f282f7524)

