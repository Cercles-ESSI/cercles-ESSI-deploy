# cercles-ESSI-deploy

---

## **Requisitos de Instalación**

Antes de proceder con la instalación de CERCLES haciendo uso de Docker Compose, asegúrate de cumplir con los siguientes requisitos según tu sistema operativo:

1.**Docker y Docker Compose**:
  
  1.1 En Windows: Descargar e instalar Docker Desktop desde [Docker](https://www.docker.com/products/docker-desktop/).Reinicia el sistema tras completar el proceso.
  
  1.2 En Linux (Ubuntu): Instalar mediante terminal:
  ```bash
    sudo apt-get update
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
  ```
  (Opcional: Añade tu usuario al grupo docker con sudo usermod -aG docker $USER para ejecutar comandos sin sudo).

---
## **Pasos de Instalación**

### **1. Clonar el repositorio del proyecto**

El primer paso para comenzar la instalación es descargar el código fuente al sistema. Para facilitar este proceso, se utiliza el repositorio de integración llamado `cercles-ESSI-deploy`. Este repositorio contiene los archivos de orquestación de Docker y enlaza directamente los repositorios del Frontend y el Backend mediante submódulos de Git.

Para obtener todos los archivos correctamente, abre una terminal y ejecuta el siguiente comando, indicando de manera explícita la URL pública del repositorio y la opción para descargar los submódulos asociados:

```bash
git clone --recurse-submodules https://github.com/Cercles-ESSI/cercles-ESSI-deploy.git
```

### **2. Configurar el correo para el primer inicio de sesión**

Una vez descargado el código, y como es la primera vez que se arranca el sistema, es necesario configurar una cuenta de Google para permitir el primer inicio de sesión (dado que la aplicación utiliza el sistema de autenticación cerrado de OAuth).

Para hacerlo, edita el archivo `application-secret.properties`, ubicado dentro del directorio del Backend en `/backend/src/main/resources/`. En este archivo debes definir tu correo de Google y tu nombre completo siguiendo esta estructura:

```properties
app.initial-email=maryx51202@gmail.com
app.initial-name=Mary Ojuyenum
```

*(De manera alternativa, este primer usuario también se podría dar de alta modificando directamente la base de datos una vez creada y añadiendo el registro manualmente).*

### **3. Configuración de una base de datos externa (Opcional)**

Por defecto, el orquestador está preparado para instanciar automáticamente un contenedor de MariaDB para que el sistema funcione de manera totalmente autónoma en cualquier ordenador. Sin embargo, si se desea desplegar la aplicación en un entorno de producción que ya dispone de su propio servidor de base de datos, se puede hacer el despliegue aún más ligero.

Para conseguirlo, solo tienes que editar el archivo `docker-compose.yml` y realizar los siguientes cambios sin necesidad de tocar el código fuente:

* Eliminar completamente el bloque del servicio `db` y los volúmenes asociados (`volumes: db_data`).
* Eliminar la dependencia `depends_on: - db` dentro del servicio `backend`.
* Modificar la variable de entorno `SPRING_DATASOURCE_URL` (y las credenciales `USERNAME` y `PASSWORD`) para apuntar directamente a la dirección de la base de datos externa.

### **4. Arranque del proyecto y verificación**

Con las credenciales iniciales configuradas, sitúate con la terminal en la raíz del directorio recién clonado (donde se encuentra el archivo `docker-compose.yml`) e inicia y compila los contenedores de Docker con el siguiente comando:

```bash
docker compose up --build -d
```

Una vez que el motor de Docker haya descargado las imágenes base, compilado el código y los servicios de la base de datos, el Backend y el Frontend hayan arrancado completamente, el proceso finaliza verificando que la plataforma se encuentra operativa. 

Para comprobarlo, abre tu navegador web y accede a la dirección local habilitada por el puerto configurado: http://localhost:3000. Si todo es correcto, se mostrará la pantalla de inicio de sesión.

---

## **Documentación**

---

| Archivo                                                      | Nombre                             | Descripción                                                |
|--------------------------------------------------------------|------------------------------------|------------------------------------------------------------|
| [Manual de usuario](https://github.com/Cercles-ESSI/cercles-ESSI-deploy/wiki) | Manual de usuario                  | Guía para los usuarios de la aplicación CERCLES, explicando cómo usar las funcionalidades. |
| [Swagger API](https://cercles-essi.github.io/cercles-ESSI-backend/) | Documentación Swagger API           | Acceso al Swagger que describe la API RESTful de CERCLES, creado mediante una GitHub Page |

---

## **Licencia**

This project is licensed under the Apache License 2.0 - see the [LICENSE](https://github.com/Cercles-ESSI/cercles-ESSI-frontend/blob/main/LICENSE) file for details.

---
