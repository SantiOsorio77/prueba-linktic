# prueba-linktic

# E-commerce Application

Este proyecto es una aplicación de e-commerce desplegada en AWS con un frontend en un bucket de S3, un backend en una instancia EC2, y una base de datos en RDS. La integración continua y el control de versiones se manejan con Azure Pipelines.

## URL de despliegue

El proyecto está desplegado y accesible desde la siguiente URL: [E-commerce](http://pruebafrontlink.s3-website.us-east-2.amazonaws.com/).
usuarios: admin,user
contraseñas admin123, user123

## Requisitos previos

Antes de comenzar, debe asegurarse de tener instalados los siguientes requisitos:

- **AWS CLI**: [Instalación y configuración](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
- **Node.js**: [Descargar Node.js](https://nodejs.org/)
- **Angular CLI**: Si trabajas con el frontend localmente, instala Angular CLI con `npm install -g @angular/cli`.
- **Java 17**: Asegúrate de tener instalado [Java 17](https://www.oracle.com/java/technologies/javase-jdk17-downloads.html).
- **Maven**: Para compilar el backend, necesitas [Maven](https://maven.apache.org/install.html).
- **Docker**: Para el desarrollo local, es útil tener Docker configurado.
- **AWS Account**: Necesitarás una cuenta en AWS con acceso a RDS, EC2, y S3.
- **Azure DevOps Account**: Para el control de versiones con Azure Pipelines.

## Configuración

### Base de datos

La base de datos está desplegada en RDS (Amazon Relational Database Service). A continuación,los detalles del esquema de la base de datos:

- **Tabla Pedidos (`pedidos`)**
  - `id`: bigint, auto_increment
  - `cantidad`: int
  - `fecha`: datetime
  - `total`: double
  - `producto_id`: bigint (relacionado con la tabla `productos`)

- **Tabla Productos (`productos`)**
  - `id`: bigint, auto_increment
  - `cantidad`: int
  - `descripcion`: varchar(255)
  - `nombre`: varchar(255)
  - `precio`: double

### Backend

El backend está desarrollado con **Java 17** y **Spring Boot** y Está desplegado en una instancia de **EC2** en AWS.

#### Ejecución local del backend

1. Clona el repositorio:
   ```bash
   git clone <https://github.com/SantiOsorio77/PruebaBack.git>
   cd backend
   ```

2. Configura las propiedades de la base de datos en el archivo `application.properties` o `application.yml` en `src/main/resources`:

    ```properties
    spring.application.name=PruebaEcommerceBack
    spring.datasource.url=jdbc:mysql://pruebaback.ctaqm2a26qkt.us-east-2.rds.amazonaws.com:3306/pruebaback
    spring.datasource.username=admin
    spring.datasource.password=pruebaback
    spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

    spring.jpa.hibernate.ddl-auto=update
    spring.jpa.show-sql=true
    spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect

    springdoc.api-docs.path=/api-docs
    springdoc.swagger-ui.path=/ecommerce
    server.port=9000
    ```

3. Compila y ejecuta el proyecto con Maven:
   ```bash
   mvn clean install
   mvn spring-boot:run
   ```

### Frontend

El frontend está desarrollado con **Angular 17** y está desplegado en un bucket de **S3** en AWS.

#### Ejecución local del frontend

1. Clona el repositorio:
   ```bash
   git clone <https://github.com/SantiOsorio77/PruebaTecnicaFrontEnd.git>
   cd frontend
   ```

2. Instala las dependencias de Angular:
   ```bash
   npm install
   ```

3. Inicia el servidor de desarrollo:
   ```bash
   ng serve
   ```

4. Accede a la aplicación en `http://localhost:4200`.

### Despliegue

#### Despliegue en AWS

- **Backend**: Desplegado en una instancia de EC2, se debe configurar el servicio de Spring Boot para que corra en el servidor con un archivo `.jar`.
EC2:
![image](https://github.com/user-attachments/assets/5764d90b-172d-456c-afb2-aa9fd4fcd1d9)


- **Frontend**: Desplegado en un bucket S3 con acceso público habilitado.
Bucket S3:
![image](https://github.com/user-attachments/assets/dd26f8b0-1dc5-42ea-aed1-6e91799259ee)


- **Base de Datos**: La base de datos está en Amazon RDS con MySQL.
  RDS:
![image](https://github.com/user-attachments/assets/1f3d5f08-2cb0-4aa2-845e-fdf7fbd1bf2e)


#### Control de Versiones con Azure Pipelines

El proyecto utiliza **Azure Pipelines** para la integración continua y despliegue. El archivo de configuración se encuentra en el repositorio como `azure-pipelines.yml`.

## Contribución

1. Crea una copia del proyecto.
2. Crea una nueva rama (`git checkout -b feature/nueva-funcionalidad`).
3. Realiza los cambios necesarios.
4. Haz commit de tus cambios (`git commit -m 'Añadir nueva funcionalidad'`).
5. Haz push a la rama (`git push origin feature/nueva-funcionalidad`).
6. Crea un Pull Request.
