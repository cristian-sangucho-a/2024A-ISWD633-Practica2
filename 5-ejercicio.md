## Esquema para el ejercicio
![Imagen](imagenes/esquema-ejercicio5.PNG)

### Crear la red
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/92060d49-00d8-4f6d-b9e3-ae94a5e45c6a)

```
>docker network create net-wp -d bridge
```

### Crear el contenedor mysql a partir de la imagen mysql:8, configurar las variables de entorno necesarias
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/8e9be2fb-988d-40ea-b24d-1d0b515077cc)

```
>docker run -d --name sql8 --network net-wp --env-file=envvar.env mysql:8
```

### Crear el contenedor wordpress a partir de la imagen: wordpress, configurar las variables de entorno necesarias
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/e44b1cab-64c5-42f7-8f04-466363a64078)
```
>docker run -d --name wp --network net-wp -p 80:80 wordpress
```

De acuerdo con el trabajo realizado, en la el esquema de ejercicio el puerto a es 80

Ingresar desde el navegador al wordpress y finalizar la configuración de instalación.
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/749c49c7-7a13-4924-b210-ed5b89c7948f)
en las variables de entorno debes especificar
```
MYSQL_USER=1234
MYSQL_PASSWORD=1234
```
luego crea una base da datos en el contenodos de mysql
```
docker exec -it sql8 mysql -uroot -p
GRANT ALL PRIVILEGES ON wordpress.* TO '1234'@'%';
FLUSH PRIVILEGES;
CREATE DATABASE wordpress;
SHOW DATABASES;
```
Debe especificar el user y password y en la direccion el nombre del contenedor por que estan en la misma red

![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/c65d85b3-cc0e-4dac-a4ea-92a295ac6ac2)
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/98a72b70-cf53-4304-b088-4d90ee951b7c)

Finalmente ya puedes iniciar sesion

Desde el panel de admin: cambiar el tema y crear una nueva publicación.

Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/2b02a9e8-705f-4854-b63f-698088c112f3)


### Eliminar el contenedor wordpress
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/3e40193b-e565-44f4-a66e-ea3df78b35ad)


### Crear nuevamente el contenedor wordpress
Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress

### ¿Qué ha sucedido, qué puede observar?
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/cae6c03f-81f6-4b2e-81df-091c8ca85f2b)

![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/a70ad82c-bf85-43b4-ab9d-3a7eedcc21c9)

Nuevamente, inicial el asistente de instalacion y si lo completas con los datos previos
ingresas a la misma cuenta donde esta alacenada la publicacion previa





