# Infraestructura Web Automática con Docker (Examen Carlos)

Este proyecto despliega un entorno de alta disponibilidad totalmente automatizado. Al levantar los contenedores, el contenido multimedia se carga automáticamente mediante *bind mounts*.

## Características
- **Acceso Único:** Puerto 80 (Nginx Proxy).
- **Alta Disponibilidad:** Dos backends (web1 y web2) sirviendo el mismo contenido.
- **Carga Automática:** Los archivos en la carpeta ./html se vinculan directamente a los servidores.
- **Aislamiento Total:** Los servidores web no son accesibles directamente desde el host, solo a través del proxy.

## Requisitos
- Windows 11 con Docker Desktop.
- Git instalado.

## Despliegue

1. **Clonar y entrar:**
   git clone https://github.com/Eric-Alba/examen-carlos
   cd examen-carlos

2. **Levantar todo:**
   docker-compose up -d

3. **Ver en el navegador:**
   Ve a http://localhost

## ¿Cómo verificar que funciona correctamente?

### A. Verificación de Balanceo de Carga
Para ver cómo el proxy reparte el tráfico entre los dos servidores:
docker-compose logs -f proxy
Refresca el navegador varias veces y verás en los logs cómo las peticiones se alternan o se distribuyen.

### B. Verificación de Alta Disponibilidad
Si un servidor "muere", el otro debe seguir funcionando:
- Apaga un backend: docker-compose stop web1
- Refresca la web: Verás que el contenido sigue ahí (ahora servido solo por web2).
- Vuelve a encenderlo: docker-compose start web1

### C. Verificación de Aislamiento
Intenta acceder directamente a un backend por su IP interna desde tu navegador. No podrás, porque no tienen puertos mapeados al exterior. Solo el Proxy tiene permiso para hablar con ellos.
<img width="554" height="754" alt="image" src="https://github.com/user-attachments/assets/de53292b-329a-4dad-bba2-8a11c1c5f429" />

### D. Verificación de Volumen Compartido
Cualquier cambio que hagas en el archivo ./html/index.html de tu ordenador se reflejará instantáneamente en ambos servidores sin necesidad de reiniciar nada.
