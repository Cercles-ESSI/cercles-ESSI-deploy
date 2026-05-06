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
  
2. **IDE** (Opcional para despliegue): Visual Studio Code (VSC) o cualquier otro IDE para proyectos backend y frontend (como IntelliJ o Eclipse).

---

## **Pasos de Instalación**

### **1. Configurar la Conexión a la API de TAIGA y el correo para el primer login**

Edita el archivo `application-secret.properties`, ubicado en `src/main/resources` del proyecto backend.

En este archivo debes poner la URL de la API de Taiga y definir tu correo de Google y tu nombre para poder entrar la primera vez. Un ejemplo sería: 

```properties

#API Taiga
taiga.api.url=https://api.taiga.io/api/v1/
# Reemplazar por el correo de Google con el que harás el primer login
app.initial-email=maryx51202@gmail.com
app.initial-name=Mary Ojuyenum
```

### **2. Iniciar el proyecto**

Inicia el docker  y verifica que la aplicación esté funcionando accediendo a `http://localhost:3030`.

---

## **Documentación**

---

| Archivo                                                      | Nombre                             | Descripción                                                |
|--------------------------------------------------------------|------------------------------------|------------------------------------------------------------|
| [Manual de usuario](https://github.com/cercles-tfg/cercles-tfg-frontend/blob/main/docs/Manual%20de%20usuario.pdf) | Manual de usuario                  | Guía para los usuarios de la aplicación CERCLES, explicando cómo usar las funcionalidades. |
| [Swagger API](https://cercles-tfg.github.io/cercles-tfg-backend/) | Documentación Swagger API           | Acceso al Swagger que describe la API RESTful de CERCLES, creado mediante una GitHub Page |

---

## **Licencia**

This project is licensed under the Apache License 2.0 - see the [LICENSE](https://github.com/cercles-tfg/.github/blob/main/LICENSE) file for details.

---
