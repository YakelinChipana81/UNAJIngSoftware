# UNAJIngSoftware – Config Server y microservicio de catálogo

Práctica: Config Server y microservicio de catálogo con PostgreSQL y Swagger
(guía del Mtro. Noe Wilber Tipo Mamani, EPISS – UNAJ).

## Componentes

| Componente          | Puerto | Rol                                    |
|---------------------|--------|----------------------------------------|
| ms-config-server    | 7070   | Lee la configuración desde este GitHub |
| ms-catalogo-service | 8081   | CRUD de Categoría + Swagger            |
| PostgreSQL          | 5432   | Base de datos `ms_catalogo`            |

## Versiones

Java 17 · Maven 3.6.3+ · Spring Boot 4.1.2 · Spring Cloud 2025.1.4 · springdoc-openapi 3.2.0

## Estructura

```
UNAJIngSoftware/
├── config-data/
│   └── ms-catalogo-service-development.yml   <- configuración que sirve el Config Server
├── ms-config-server/                          <- puerto 7070 (usuario root / 123456)
└── ms-catalogo-service/                       <- puerto 8081
    └── src/main/java/com/ejemplo/mscatalogo
        ├── controller/CategoriaController.java
        ├── entity/Categoria.java
        ├── repository/CategoriaRepository.java
        ├── service/CategoriaService.java
        ├── service/impl/CategoriaServiceImpl.java
        └── MsCatalogoServiceApplication.java
```

## Cómo ejecutar

1. Crear la base de datos (usuario `postgres`, clave `123456`, puerto `5432`):
   ```sql
   CREATE DATABASE ms_catalogo;
   ```
2. Levantar `ms-config-server` y verificar (usuario `root`, clave `123456`):
   http://localhost:7070/ms-catalogo-service/development
3. Levantar `ms-catalogo-service`. En consola debe aparecer
   `Fetching config from server at : http://localhost:7070` y `Tomcat started on port 8081`.
4. Swagger:
   - http://localhost:8081/doc/swagger-ui.html
   - http://localhost:8081/v3/api-docs
5. Probar `POST /categoria` con `{ "nombre": "Electrónica" }`, luego
   `GET /categoria`, `GET /categoria/1`, `PUT /categoria/1` y `DELETE /categoria/1`.
6. Verificar en PostgreSQL: `SELECT * FROM categoria;`

Desde consola, en cada carpeta del proyecto: `mvnw.cmd spring-boot:run` (Windows) o `./mvnw spring-boot:run`.
