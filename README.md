# Tienda de Perritos - Backend y Base de Datos

## Descripción del Proyecto
El presente repositorio contiene el código fuente correspondiente al backend y los manifiestos de infraestructura de la base de datos para el proyecto "Tienda de Perritos". El sistema se encarga de procesar la lógica de negocio y gestionar la conexión de datos.

## Arquitectura y Tecnologías
La infraestructura se orquesta mediante **Amazon EKS (Elastic Kubernetes Service)**, asegurando alta disponibilidad y escalabilidad.
* **Lenguaje/Framework:** Node.js.
* **Base de Datos:** MySQL.
* **Registro de Contenedores:** Amazon ECR.
* **Orquestación:** Kubernetes (Manifiestos `Deployment`, `Service`, `HPA`, `Secret`).

## Flujo de Integración y Despliegue Continuo (CI/CD)
Se implementa un flujo de trabajo automatizado mediante **GitHub Actions**. Ante cada actualización en la rama principal, el sistema ejecuta las siguientes acciones:
1. Se autentica de manera segura en el entorno de AWS.
2. Se construye la imagen Docker del backend.
3. Se almacena la nueva imagen en Amazon ECR con la etiqueta `eks-v1`.
4. Se actualiza el clúster EKS y se aplican los manifiestos de Kubernetes alojados en la carpeta `k8s/`, generando dinámicamente los secretos de la base de datos para no exponer credenciales en el código fuente.

## Estructura del Repositorio
* `/`: Código fuente de la aplicación (Node.js).
* `/db`: Archivos de inicialización e imagen de la base de datos MySQL.
* `/k8s`: Manifiestos YAML para el despliegue en Kubernetes (Deployment, Services, HPA y Namespace).

## Instrucciones de Configuración
Para replicar el despliegue automatizado, se requiere la configuración de los siguientes secretos en el entorno del repositorio:
* `AWS_ACCESS_KEY_ID`
* `AWS_SECRET_ACCESS_KEY`
* `AWS_SESSION_TOKEN`
* `MYSQL_ROOT_PASSWORD`