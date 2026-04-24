# Infraestructura Web Escalable con Docker

Este proyecto despliega una infraestructura web completa con balanceo de carga, proxy inverso y aislamiento de red.

## Características
- **Proxy Inverso:** Nginx escuchando en el puerto 80.
- **Balanceo de Carga:** Distribución de tráfico entre dos backends.
- **Seguridad:** Los servidores web están en una red interna privada.
- **Volumen Compartido:** Contenido multimedia compartido entre backends.

## Requisitos
- Windows 11 con [Docker Desktop](https://www.docker.com/products/docker-desktop/) instalado.
- PowerShell.

## Despliegue rápido

1. **Clonar el repositorio:**
   git clone https://github.com/Eric-Alba/examen-carlos
   cd examen-carlos

2. **Levantar la infraestructura:**
   docker-compose up -d

3. **Cargar contenido multimedia:** docker cp index.html entorno-docker-web1-1:/usr/share/nginx/html/
   docker cp Hola.png entorno-docker-web1-1:/usr/share/nginx/html/
   docker cp videoplayback.mp4 entorno-docker-web1-1:/usr/share/nginx/html/

4. **Acceso:** Abre http://localhost en tu navegador.

## Estructura del Proyecto
- docker-compose.yml: Definición de servicios, redes y volúmenes.
- nginx.conf: Configuración del balanceador de carga.
- index.html: Página principal con soporte multimedia.
