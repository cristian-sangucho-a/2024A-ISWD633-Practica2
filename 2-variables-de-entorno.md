# Variables de Entorno
### ¿Qué son las variables de entorno
Es una variable dinámica que puede afectar al comportamiento de los procesos en ejecución en un ordenador. Son parte del entorno en el que se ejecuta un proceso.

### Para crear un contenedor con variables de entorno

```
docker run -d --name <nombre contenedor> -e <nombre variable1>=<valor1> -e <nombre variable2>=<valor2>
```

### Crear un contenedor a partir de la imagen de nginx:alpine con las siguientes variables de entorno: username y role. Para la variable de entorno rol asignar el valor admin.

![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/7fdf556a-b410-4fc8-b20a-76f206ff249b)


### Crear un contenedor con mysql:8 , mapear todos los puertos

### ¿El contenedor se está ejecutando?
No, al ejecutar 
´´´
docker ps -a
´´´
En el contenedor sql muestra
Exited (1) 4 minutes ago  

### Identificar el problema
´´´´
docker logs sql8


2024-06-07 13:45:02+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.4.0-1.el9 started.
2024-06-07 13:45:04+00:00 [Note] [Entrypoint]: Switching to dedicated user 'mysql'
2024-06-07 13:45:04+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.4.0-1.el9 started.
2024-06-07 13:45:05+00:00 [ERROR] [Entrypoint]: Database is uninitialized and password option is not specified
    You need to specify one of the following as an environment variable:
    - MYSQL_ROOT_PASSWORD
    - MYSQL_ALLOW_EMPTY_PASSWORD
    - MYSQL_RANDOM_ROOT_PASSWORD

no tiene las suficientes variables de entorno.
´´´´


### Eliminar el contenedor creado con mysql:8 

´´´´
C:\Users\LabP3E010\containers>docker rm sql8

sql8
´´´´


### Para crear un contenedor con variables de entorno especificadas
- Portabilidad: Las aplicaciones se vuelven más portátiles y pueden ser desplegadas en diferentes entornos (desarrollo, pruebas, producción) simplemente cambiando el archivo de variables de entorno.
- Centralización: Todas las configuraciones importantes se centralizan en un solo lugar, lo que facilita la gestión y auditoría de las configuraciones.
- Consistencia: Asegura que todos los miembros del equipo de desarrollo o los entornos de despliegue utilicen las mismas configuraciones.
- Evitar Exposición en el Código: Mantener variables sensibles como contraseñas, claves API, y tokens fuera del código fuente reduce el riesgo de exposición accidental a través del control de versiones.
- Control de Acceso: Los archivos de variables de entorno pueden ser gestionados con permisos específicos, limitando quién puede ver o modificar la configuración sensible.

Previo a esto es necesario crear el archivo y colocar las variables en un archivo, **.env** se ha convertido en una convención estándar, pero también es posible usar cualquier extensión como **.txt**.
```
docker run -d --name <nombre contenedor> --env-file=<nombreArchivo>.<extensión> <nombre imagen>
```
**Considerar**
Es necesario especificar la ruta absoluta del archivo si este se encuentra en una ubicación diferente a la que estás ejecutando el comando docker run.

### Crear un contenedor con mysql:8 , mapear todos los puertos y configurar las variables de entorno mediante un archivo
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/678a43da-8a84-4921-8784-70fc789c0754)


![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/0b9f286b-ea99-45cf-8041-6a7c099dafa6)


### ¿Qué bases de datos existen en el contenedor creado?
```
docker exec -it sql8 mysql -u root -p -e "show databases;"
```
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/0928aa62-be07-4c51-908d-b118c1f56f25)

