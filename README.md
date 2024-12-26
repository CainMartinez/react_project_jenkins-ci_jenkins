# Proyecto CI/CD con Jenkins para Despliegue de React

## Resumen
Este proyecto implementa una pipeline automatizada en Jenkins para gestionar el flujo de trabajo de una aplicación React. La pipeline abarca desde la instalación de dependencias y ejecución de pruebas hasta el despliegue final en Vercel, incluyendo notificaciones mediante Telegram. Este documento describe los pasos necesarios, las configuraciones clave y los conceptos utilizados para configurar y ejecutar esta integración continua.

---

## ¿Qué es Jenkins?
Jenkins es una plataforma de automatización de código abierto que permite configurar procesos CI/CD. Con ella, se pueden definir tareas como pruebas, compilaciones y despliegues de forma flexible.

### Ventajas principales:
- **Gratuito y extensible**: Admite una amplia variedad de plugins para integrar herramientas.
- **Compatible con VCS**: Funciona con sistemas como GitHub, GitLab y Bitbucket.
- **Definiciones declarativas**: Permite gestionar pipelines mediante scripts (`Jenkinsfile`), facilitando su versión junto al código fuente.

---

## El Jenkinsfile
El `Jenkinsfile` es el núcleo de la pipeline. Este archivo define cada etapa del proceso, proporcionando claridad y documentación del flujo de trabajo.

### ¿Por qué usar un Jenkinsfile?
- Centraliza la configuración del pipeline.
- Es replicable y versionable.
- Permite integrar cambios rápidamente.

---

## Notificaciones por Telegram
Para mantener informados a los desarrolladores, se utiliza un bot de Telegram que envía actualizaciones sobre el estado del pipeline en tiempo real.

### ¿Cómo se configura?
1. Crear un bot en Telegram y obtener su token de acceso.
2. Configurar el token en Jenkins como una credencial segura.
3. Utilizar scripts personalizados para enviar mensajes con el estado de las etapas.

---

## Configuración Inicial

### Requisitos
1. **Instalación de Jenkins**: Descarga la última versión en [jenkins.io](https://www.jenkins.io/).
2. **Node.js**:
   - Instala el plugin NodeJS en Jenkins.
   - Configura una versión global de Node.js desde `Manage Jenkins > Global Tool Configuration`.
3. **Cuenta en Vercel**: Crea una cuenta en [vercel.com](https://vercel.com/) y genera un token de acceso.
4. **Acceso SSH**: Asegúrate de que Jenkins tiene una clave SSH para acceder al repositorio.

### Configuración de la Pipeline
1. Crea un nuevo proyecto en Jenkins como `Pipeline`.
2. Agrega las credenciales necesarias:
   - Clave SSH para GitHub.
   - Tokens de Telegram y Vercel como texto seguro.
3. Configura el pipeline para que utilice un script desde el control de versiones (`Pipeline script from SCM`).

---

## Estructura del Jenkinsfile

El archivo define las siguientes etapas principales:

1. **Instalación de Dependencias**:
   - Instala los módulos necesarios para React y la CLI de Vercel.
2. **Análisis estático (Linter)**:
   - Verifica la calidad del código con ESLint.
3. **Pruebas Unitarias**:
   - Ejecuta pruebas con Jest para validar el correcto funcionamiento.
4. **Actualización del README**:
   - Modifica el archivo `README.md` con los resultados de las pruebas.
5. **Commit y Push**:
   - Guarda los cambios automáticamente en el repositorio remoto.
6. **Compilación**:
   - Genera una versión optimizada para producción.
7. **Despliegue**:
   - Publica la aplicación en Vercel.
8. **Notificación**:
   - Envía un resumen de los resultados al bot de Telegram.

---

## Scripts Personalizados

### Envío de Notificaciones
Se utiliza un script para enviar mensajes al bot de Telegram. El mensaje incluye detalles sobre el estado de cada etapa.

### Actualización de Repositorio
Otro script realiza el commit y push de cambios relevantes al repositorio.

---

## Resultados Esperados

El pipeline automatiza todo el flujo de trabajo, desde la validación del código hasta el despliegue final. Los desarrolladores reciben notificaciones en Telegram con un resumen como este:

## RESULTADO DE LOS ÚLTIMOS TESTS

![Success](https://img.shields.io/badge/tested%20with-Cypress-04C38E.svg)
