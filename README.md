# Juanma González Márquez - SRI - 2ASIR

### Instalación de servidor web interno.

1. Instalación del servidor web apache. Usaremos dos dominios mediante el archivo hosts: centro.intranet y departamentos.centro.intranet. El primero servirá el contenido mediante wordpress y el segundo una aplicación en python.

2. Activar los módulos necesarios para ejecutar php y acceder a mysql.
3. Instala y configura wordpress.
4. Activar el módulo "wsgi" para permitir la ejecución de aplicaciones Python.
5. Crea y despliega una pequeña aplicación en Python para comprobar que fucniona correctamente.
6. Adicionalmente protegeremos el acceso a la aplicación Python mediante autenticación.
7. Instala y configura awstat.
8. Instala un segun servidor de tu elección (nginx, lighttpd) bajo el dominio "servidor2.centro.intranet". Debes configurarlo para que sirva en el puerto 8080 y haz los cambios para ejecutar php. Instala phpmyadmin.
