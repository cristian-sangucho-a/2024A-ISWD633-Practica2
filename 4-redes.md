# Redes
Las redes son un componente fundamental que permite la comunicación entre contenedores, así como la comunicación de los contenedores con el mundo exterior. 
![Imagen](imagenes/redes.PNG)
- Bridge: Esta es la red por defecto en Docker. Permite la comunicación entre contenedores en el mismo host. Cada contenedor conectado a la red bridge tiene una IP propia en la subred de la red bridge.
    -  Brige por default: Cuando se ejecuta un contenedor, Docker crea automáticamente una red de tipo bridge por default. Esta red se utiliza para permitir la comunicación entre contenedores en el mismo host. Cada contenedor conectado a esta red obtiene su propia dirección IP en la subred de la red bridge.
    - Bridge creada por nosotros: Un usuario también puede crear sus propias redes de tipo bridge en Docker. Esto puede ser útil para organizar y segmentar los contenedores de una aplicación de manera más controlada. Al crear una red bridge personalizada, se puede especificar un rango de direcciones IP y otras configuraciones de red específicas. Los contenedores conectados a esta red utilizarán las direcciones IP de la subred definida por el usuario.
- Host: Con esta red, los contenedores comparten la red del host en lugar de tener su propia interfaz de red. Esto puede mejorar el rendimiento de red, pero los contenedores pueden entrar en conflicto con los puertos del host si intentan utilizar los mismos puertos.
- None: Con esta red, se deshabilita la configuración de red. Los contenedores que usan esta red tienen su propia red de bucle invertido y no pueden comunicarse con otros contenedores a menos que se conecten explícitamente a una red.

### Crear una red de tipo bridge

```
docker network create <nombre red> -d bridge
```

### Crear un contenedor vinculado a una red

```
docker run -d --name <nombre contenedor> --network <nombre red> <nombre imagen>
```

### Para saber a qué red está conectado un contenedor

```
docker inspect <nombre contenedor>
```
ó
```
docker network inspect <nombre red> 
```

### Vincular contenedor a una red
```
docker network connect <nombre red> <nombre contenedor>
```

### Para desvincular un contenedor de una red
```
docker network disconnect <nombre red> <nombre contenedor>
```

### Para listar las redes existentes
```
docker network ls
```

### Crear los contenedores y las redes que se presentan en el esquema. Usar para todos los contenedores la imagen de nginx:alpine

![Imagen](imagenes/esquema-ejercicio-redes.PNG)

# COLOCAR UNA CAPTURA DE LAS REDES EXISTENTES CREADAS
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/44aba2bd-4ac7-436c-adb5-fab9655ba242)


# COLOCAR UNA(S) CAPTURAS(S) DE LOS CONTENEDORES CREADOS EN DONDE SE EVIDENCIE A QUÉ RED ESTÁN VINCULADOS
````
C:\Users\intel\dockerContainers>docker network inspect net-curso01
[
    {
        "Name": "net-curso01",
        "Id": "df3f9c6384a9cd4be9b12d5f38dc8458773ffcefdf197009054011629367e6a2",
        "Created": "2024-06-13T19:30:36.540542481Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "364cdfeaa992b75ddc858f60cd5dc16aae6b7e2a64557451cb99f0994005bdc2": {
                "Name": "c2",
                "EndpointID": "19ca736f22e381525ce1823b2c220f65d77913cb9f409cf85f5ed2b331ed8934",
                "MacAddress": "02:42:ac:12:00:03",
                "IPv4Address": "172.18.0.3/16",
                "IPv6Address": ""
            },
            "b9bdd955832a7f904988f197ffc02b66d43b5c1684df2a496089c8fe589843f3": {
                "Name": "c1",
                "EndpointID": "222885d363a3b5658b1fc0528951da787105524a3082f5327bfd5b6a9cb419cb",
                "MacAddress": "02:42:ac:12:00:02",
                "IPv4Address": "172.18.0.2/16",
                "IPv6Address": ""
            },
            "bab00a2eb76261007f6494aaa8af6182393d90d3c9738193666b257752ebf001": {
                "Name": "c3",
                "EndpointID": "0dad6f9c3c5b5598ea26dd208e902de8dd73c33aa8c2d4918ebb6051e1446be8",
                "MacAddress": "02:42:ac:12:00:04",
                "IPv4Address": "172.18.0.4/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]
````
C:\Users\intel\dockerContainers>docker network inspect net-curso02
[
    {
        "Name": "net-curso02",
        "Id": "6e3d45edd303b23178ad55e9ec43e0a76785ae57f5021a2a29d38e50e6287e49",
        "Created": "2024-06-13T19:30:40.285493515Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.19.0.0/16",
                    "Gateway": "172.19.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "bab00a2eb76261007f6494aaa8af6182393d90d3c9738193666b257752ebf001": {
                "Name": "c3",
                "EndpointID": "bd253ba819cdb57297e75aa150ca606cc67ac099d2ef5159b5ced4ad03f342db",
                "MacAddress": "02:42:ac:13:00:03",
                "IPv4Address": "172.19.0.3/16",
                "IPv6Address": ""
            },
            "bd2593134b8ebbff18afd7ac6971940b0b908123328ee43e14c1a2d77cd96a29": {
                "Name": "c4",
                "EndpointID": "431df147396dc7c7679133f211fd3145d3a21668b081e989627bc9e066e2d470",
                "MacAddress": "02:42:ac:13:00:02",
                "IPv4Address": "172.19.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]
````

````

### Para eliminar las redes creadas
```
docker network rm <nombre de la red>
```
![image](https://github.com/cristian-sangucho-a/2024A-ISWD633-Practica2/assets/93937686/501543fb-899a-4bc6-946a-fd0059984305)

