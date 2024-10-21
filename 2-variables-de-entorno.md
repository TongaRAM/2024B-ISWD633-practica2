# Variables de Entorno
### ¿Qué son las variables de entorno
Son valores que guardan informacion acerca del entorno del sistema y que a su vez repercuten en el comportamiento de este.

### Para crear un contenedor con variables de entorno?

```
docker run -d --name <nombre contenedor> -e <nombre variable1>=<valor1> -e <nombre variable2>=<valor2>
```

### Crear un contenedor a partir de la imagen de nginx:alpine con las siguientes variables de entorno: username y role. Para la variable de entorno rol asignar el valor admin.


    docker run -d --name srv-nginx -e username=anthony -e role=admin nginx:alpine

    docker exec -it srv-nginx sh

    / # echo $username
    / # echo $role


    

# CAPTURA CON LA COMPROBACIÓN DE LA CREACIÓN DE LAS VARIABLES DE ENTORNO DEL CONTENEDOR ANTERIOR

![variable_entorno](evidencia/varEntornoUser.png)

### Crear un contenedor con mysql:8 , mapear todos los puertos
    docker run -d --name mysql-cont --publish published=3306,target=3306 mysql:8

### ¿El contenedor se está ejecutando?

    No, solo esta creado el contenedor.

### Identificar el problema

    El problema surge dado que se tiene que especificar alguna de las siguientes variables de entorno: 
    - MYSQL_ROOT_PASSWORD
    - MYSQL_ALLOW_EMPTY_PASSWORD
    - MYSQL_RANDOM_ROOT_PASSWORD

### Eliminar el contenedor creado con mysql:8 

    docker rm mysql-cont

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

    docker run -d --name mysql-cont --env-file=./mysql_config_var.txt mysql:8

![variable_entorno](evidencia/mysqlVar.png)

# CAPTURA CON LA COMPROBACIÓN DE LA CREACIÓN DE LAS VARIABLES DE ENTORNO DEL CONTENEDOR ANTERIOR 

![variable_entorno](evidencia/checkMysqlVar.png)

### ¿Qué bases de datos existen en el contenedor creado?
    docker exec -it mysql-cont mysql -u root -p

    <password admin>

    SHOW DATABASES;

![variable_entorno](evidencia/mysqlDB.png)

