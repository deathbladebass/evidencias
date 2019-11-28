# Tarea 01.
Primero tenemos que abrir una consola donde tengamos nuestra clave privada y darle permisos:
````chmod 400 AWSAdrian.pem````

Despues nos conectaremos mediante SSH:
````ssh -i "AWSAdrian.pem" ubuntu@ec2-52-55-225-137.compute-1.amazonaws.com````

Una vez conectados instalaremos lo siguiente:
- [Apache](#apache)
- [MySQL](#mysql)
- [PHP](#php)
