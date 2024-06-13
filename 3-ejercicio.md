### Crear contenedor de Postgres sin que exponga los puertos. Usar la imagen: postgres:11.21-alpine3.17

### Crear un cliente de postgres. Usar la imagen: dpage/pgadmin4
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/3685cc7f-4774-4050-b84f-85cc472d8663)


La figura presenta el esquema creado en donde los puertos son:
- a: (80)
- b: (80)
- c: (5432)

![Imagen](imagenes/esquema-ejercicio3.PNG)

## Desde el cliente
### Acceder desde el cliente al servidor postgres creado.
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/d0747d2f-aec5-47ef-b7d3-e8bb8811a109)

### Crear la base de datos info, y dentro de esa base la tabla personas, con id (serial) y nombre (varchar), agregar un par de registros en la tabla, obligatorio incluir su nombre.

## Desde el servidor postgresl
### Acceder al servidor
### Conectarse a la base de datos info
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/753110dd-9472-4256-9565-0ca83fffb3fd)

### Realizar un select *from personas
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/f1a66dca-7c3d-4252-812a-5dc145c725f1)



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


