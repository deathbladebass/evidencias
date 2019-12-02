# Tarea 01.
Primero tenemos que abrir una consola donde tengamos nuestra clave privada y darle permisos:
````chmod 400 AWSAdrian.pem````

Despues nos conectaremos mediante SSH:
````ssh -i "AWSAdrian.pem" ubuntu@ec2-52-55-225-137.compute-1.amazonaws.com````

Una vez conectados instalaremos lo siguiente:
- [Apache](#apache)
- [MySQL](#mysql)
- [PHP](#php)

## Apache

Antes que nada haremos un update
````sudo apt-get update````
![](img/update.png)

Y ahora instalaremos apache.
````sudo apt-get install apache2````
![](img/install_apache.png)

Ahora tendremos que ajustar el Firewall para permitir el trafico.
````sudo ufw allow in "Apache Full"````
![](img/firewall_apache.png)

Si lo hemos hecho correctamente podremos entrar a la ip publica en nuestro navegador y veremos el index de apache.
![](img/apache_instalado.png)

## MySQL

Instalaremos MySQL, para ello usaremos este comando:
````sudo apt install mysql-server````
![](img/install_mysql.png)

Ahora usaremos este comando para ejecutar un script de seguridad:
````sudo mysql_secure_installation````

Nos pedira algunas configuraciones y la contraseña de root:
![](img/mysql_security.png)

Una vez configurado podremos usar MySQL con el comando ***sudo mysql***.
![](img/mysql_instalado.png)

## PHP

Instalaremos PHP usando este comando:
````sudo apt install php libapache2-mod-php php-mysql````
![](img/php_instalado.png)

Ahora tendremos que configurar apache para que index.php tenga preferencia.
Para eso editaremos el archivo ***dir.conf***:
````sudo nano /etc/apache2/mods-enabled/dir.conf````
Estara asi:
![](img/php_index1.png)
Lo dejamos asi:
![](img/php_index2.png)

Reiniciamos apache:
````sudo systemctl restart apache2````

Ahora configuramos los virtual hosts:
Primero creamos una carpeta para nuestro dominio.
````sudo mkdir /var/www/adrian.fpz1920.com````

Ahora aplicamos permisos en la carpeta.
````sudo chown -R $USER:$USER /var/www/adrian.fpz1920.com````
````sudo chmod -R 755 /var/www/adrian.fpz1920.com````

Ahora creamos un index para nuestro dominio:
````nano /var/www/adrian.fpz1920.com/index.php````

Ahora creamos el archivo del virtual host:
````sudo nano /etc/apache2/sites-available/adrian.fpz1920.com.conf````

![](img/virtualhost.png)

Vamos a activar el host:
````sudo a2ensite adrian.fpz1920.com.conf````

Y desactivamos el default:
````sudo a2dissite 000-default.conf````

Hacemos un test para comprobar errores:
````sudo apache2ctl configtest````

Si no hay ningun fallo reiniciamos apache:
````sudo systemctl restart apache2````

Ahora para comprobar que PHP esta funcionando correctamente crearemos un pequeño script.
````sudo nano /var/www/adrian.fpz1920.com/info.php````
![](img/script.png)

Ahora si entramos a ese archivo desde el dominio aparecera esto:
![](img/script2.png)