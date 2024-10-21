### Crear contenedor de Postgres sin que exponga los puertos. Usar la imagen: postgres:11.21-alpine3.17

    docker run -d --name postgres-cont --env POSTGRES_PASSWORD=mysecretpassword postgres:11.21-alpine3.17


### Crear un cliente de postgres. Usar la imagen: dpage/pgadmin4

    docker run -d --name pgadmin-client -p 8080:80 -e PGADMIN_DEFAULT_EMAIL=admin@example.com -e PGADMIN_DEFAULT_PASSWORD=password dpage/pgadmin4 

La figura presenta el esquema creado en donde los puertos son:
- a: 5432
- b: 80
- c: 8080

![Imagen](img/esquema-ejercicio3.PNG)

## Desde el cliente
### Acceder desde el cliente al servidor postgres creado.
![ejercicio-postgre](evidencia/loginPostgre.png)
### Crear la base de datos info, y dentro de esa base la tabla personas, con id (serial) y nombre (varchar), agregar un par de registros en la tabla, obligatorio incluir su nombre.

    CREATE DATABASE info
    WITH
    OWNER = postgres
    ENCODING = 'UTF8'
    LC_COLLATE = 'en_US.utf8'
    LC_CTYPE = 'en_US.utf8'
    TABLESPACE = pg_default
    CONNECTION LIMIT = -1
    IS_TEMPLATE = False;


    CREATE TABLE personas (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100));

    INSERT INTO personas (nombre) VALUES
    ('Anthony Morales'),
    ('Lamine Yamal');

 ![ejercicio-postgre](evidencia/tablePersonas.png)

## Desde el servidor postgresl
### Acceder al servidor
### Conectarse a la base de datos info
    docker exec -it postgres-cont sh

    / # psql -U postgres -d info

    info=# select * from personas;
### Realizar un select *from personas
![ejercicio-postgre](evidencia/tablePersonasSrv.png)