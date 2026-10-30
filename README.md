Este repositorio aloja el microservicio Vehículos junto con la implementación de un pipeline Integración y Entrega Continua CI/CD empleando GitHub Actions. Se busca con esta entrega automatizar todo el ciclo de vida del software desde la ejecución pruebas hasta el despliegue dentro un entorno simulado.

Descripción del Pipeline:
El flujo trabajo se halla definido mediante el archivo github workflows ci cd yml ejecutándose automáticamente al realizar push o pull request sobre la rama main. Consta pipeline las siguientes etapas:
1. Integración Continua y Pruebas IE2
Se configura el entorno usando Java 21 mientras ejecutan pruebas unitarias integración mediante Maven mvn clean test. Para ello se emplean frameworks como JUnit 5 Mockito asegurando que la lógica negocio o los controladores funcionen correctamente antes continuar.
2. Análisis de Seguridad IE3
Se integra la herramienta Trivy para escanear el sistema archivos buscando vulnerabilidades en las dependencias y librerías. El pipeline se configura para gestionar credenciales sensibles, tal como la contraseña de base de datos, usando GitHub Secrets y evitando exponer datos en el código.
3. Contenerización IE1
Se construye una imagen Docker para la aplicación. Mediante un enfoque de múltiples etapas o multi stage build, se separa la compilación de Maven del entorno final JRE, consiguiendo así una imagen liviana y bien optimizada.
4. Despliegue y Orquestación IE4 e IE5
El despliegue automático ocurre en un entorno simulado a través de Docker Compose. Dos servicios se orquestan, siendo el microservicio de Spring Boot y una base de datos MySQL. Se configuró un healthcheck en la base de datos para garantizar que la aplicación inicie solo cuando ese servicio esté completamente operativo.
Garantía de Trazabilidad y Calidad IE4
Trazabilidad Cada ejecución del pipeline queda registrada en la pestaña Actions de GitHub. Esto permite rastrear qué commit desplegó una versión específica y revisar los logs de cada paso del proceso. Calidad: Se garantiza la calidad del código obligando a ejecutar pruebas automatizadas siempre que hay una integración. Si una prueba falla o el análisis detecta un fallo de seguridad crítico que obstruya el flujo, el pipeline detiene el despliegue de forma automática.
