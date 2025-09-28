# Jambatu WordPress Template

Este proyecto contiene una configuración de Docker Compose para ejecutar WordPress con persistencia de datos.

## Servicios incluidos

- **WordPress**: Aplicación principal en el puerto 8080
- **MySQL 8.0**: Base de datos en el puerto 3306 (interno)
- **phpMyAdmin**: Interfaz web para administrar la base de datos en el puerto 8081

## Configuración

1. Copia el archivo de configuración de ejemplo:
   ```bash
   cp env.example .env
   ```

2. Edita el archivo `.env` con tus credenciales deseadas:
   ```
   MYSQL_DATABASE=wordpress_db
   MYSQL_USER=wordpress_user
   MYSQL_PASSWORD=tu_password_seguro
   MYSQL_ROOT_PASSWORD=tu_root_password_seguro
   ```

## Uso

### Iniciar los servicios
```bash
docker-compose up -d
```

### Ver logs
```bash
docker-compose logs -f
```

### Detener los servicios
```bash
docker-compose down
```

### Detener y eliminar volúmenes (¡CUIDADO! Esto borrará todos los datos)
```bash
docker-compose down -v
```

## Acceso

- **WordPress**: http://localhost:8080
- **phpMyAdmin**: http://localhost:8081

## Persistencia de datos

Los datos se almacenan en volúmenes Docker:
- `wordpress_data`: Contenido de WordPress
- `mysql_data`: Base de datos MySQL

Esto garantiza que los datos se mantengan aunque se detengan los contenedores.

## Configuración para archivos grandes

El proyecto está configurado para permitir la subida de archivos de hasta 200MB:

- **PHP**: `upload_max_filesize = 200M` y `post_max_size = 200M`
- **MySQL**: `max_allowed_packet = 256M`
- **Memoria**: `memory_limit = 512M`
- **Tiempo de ejecución**: `max_execution_time = 300s`

## Estructura de directorios

```
.
├── docker-compose.yml
├── php.ini (configuración de PHP para archivos grandes)
├── env.example
├── .env (crear desde env.example)
└── wp-content/ (opcional, para temas y plugins personalizados)
```
