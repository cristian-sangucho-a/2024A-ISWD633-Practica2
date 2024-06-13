# Apredizajes
Conectar contenedor mediante redes y mapear puertos para poder exponer los contenedores,ademas, aprender como usar contenedores de bases de datos y el wordpress

En el ejercicio 3: se necesitaron varias configuracion extra
El contenedor de docker necesitas especificar el puerto de conexion y una contraseña o POSTGRES_HOST_AUTH_METHOD
```
docker run -d --name postgres --env-file=envvarpg.env -p 5432:5432 -e POSTGRES_HOST_AUTH_METHOD=trust postgres:11.21-alpine3.17
```

luego obtener la ip de ejecucion del postgress
```
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' postgres
```
y en pgadmin debe especificar el puerto con el que creaste el contenedor y la ip de postgres
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/7795517c-9cd7-4cd6-beb4-fc2110790892)
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/9789a29d-2f50-40e7-a0aa-263c5e629cee)
y el username superusuario por defecto es 'postgres'

Luego en el pgadmin ejecuta el query
````
CREATE DATABASE info;

CREATE TABLE personas (
  id SERIAL PRIMARY KEY,
  nombre VARCHAR(255)
);

INSERT INTO personas (nombre) VALUES ('Cristian Sangucho'), ('Pepe'), ('Jose'), ('Maria'), ('DB'), ('Mongo');
````
 ![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/8abdb41c-7137-4a63-8c23-6e008e7e121a)

