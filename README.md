# Introducción a GitHub Actions y su uso en Integración Continua y Despliegue Continuo

## Conceptos básicos de Integración Continua (CI) y Despliegue Continuo (CD)

### Definición y propósito de CI/CD

- CI/CD es un conjunto de prácticas para automatizar la integración y entrega del código en proyectos de software.

- La integración continua (CI) busca que cada cambio en el código se integre y pruebe automáticamente para evitar errores.

- El despliegue continuo (CD) automatiza la entrega del software a entornos de producción o intermedios como testing o staging.

- Estas prácticas permiten procesos repetibles, confiables y automáticos, evitando errores humanos y listas manuales de instrucciones.

### Flujo típico de trabajo con Git y ramas

- Los desarrolladores trabajan en ramas separadas para nuevas características o correcciones, manteniendo una rama principal (main) y una de desarrollo (dev).

- Se hacen commits locales y luego se crea un Pull Request para solicitar la integración de los cambios a la rama principal o de desarrollo.

- El Pull Request permite revisar los cambios, ver diferencias (diff) y aprobar o solicitar modificaciones antes de hacer merge.

- En equipos, otros desarrolladores revisan el código; en proyectos individuales, uno mismo puede aprobar sus Pull Requests.

### Importancia de la automatización en CI/CD

- No se puede confiar solo en la memoria para ejecutar pruebas y verificaciones en el orden correcto.

- Las herramientas de CI/CD automatizan pruebas, linting, compilación y despliegue, asegurando calidad y consistencia.

- Se pueden definir eventos que disparan acciones automáticas, como commits, Pull Requests o cambios en ramas específicas.

- La automatización permite hacer despliegues de prueba o previews automáticos para Pull Requests, facilitando demos sin intervención manual.

## GitHub Actions: características y funcionamiento

### Qué es GitHub Actions y su integración con GitHub

- GitHub Actions es la herramienta de CI/CD integrada en GitHub que permite automatizar flujos de trabajo (workflows) basados en eventos del repositorio.

- Los workflows son archivos YAML que definen cuándo y cómo se ejecutan las acciones, como en push, Pull Requests o releases.

- GitHub Actions se ejecuta en runners, máquinas virtuales proporcionadas por GitHub que corren Linux (usualmente Ubuntu).

- La integración nativa con GitHub facilita su uso sin configuraciones adicionales y permite acceder desde la interfaz web o extensiones en editores como Visual Studio Code.

### Estructura y sintaxis de los workflows

- Los archivos de configuración usan YAML, una sintaxis basada en tabulaciones que agrupa claves y subclaves para definir eventos, jobs y steps.

- Un workflow tiene un nombre, eventos que lo disparan (on), jobs que agrupan tareas, y steps que son comandos o invocaciones a otras acciones.

- Los steps pueden ejecutar comandos bash o usar acciones predefinidas (uses) desarrolladas por terceros o el propio equipo.

- La correcta indentación es crucial para evitar errores, similar a Python, y existen herramientas y extensiones que ayudan con la edición y autocompletado.

### Ejecución y gestión de workflows en GitHub

- Cada ejecución de un workflow consume minutos de runner, con un límite gratuito de 2000 minutos mensuales para repositorios privados.

- Los logs de ejecución quedan almacenados y accesibles para revisión detallada de cada paso y resultado.

- Se pueden configurar variables de entorno y secretos para manejar credenciales, tokens o claves SSH de forma segura.

- GitHub Actions soporta integración con Docker, permitiendo construir imágenes, subirlas a registries y desplegarlas automáticamente.

## Herramientas alternativas y comparación con GitHub Actions

### Otras plataformas de CI/CD populares

- GitLab CI/CD: integrada en GitLab, permite ejecutar pipelines similares a GitHub Actions, con versión gratuita y paga.

- Jenkins: herramienta open source muy personalizable que se puede correr en infraestructura propia, con amplia flexibilidad.

- CircleCI, Travis CI, Turtle CI: otras opciones comerciales o gratuitas para integración continua con diferentes características.

- Bitbucket Pipelines: solución integrada para repositorios alojados en Bitbucket, con configuración de pipelines para CI/CD.

### Ventajas y desventajas de GitHub Actions

- Ventajas:

	- Integración nativa con GitHub, sin necesidad de configuraciones externas.

	- Soporte excelente para Docker y contenedores.

	- Marketplace con acciones predefinidas y comunidad activa.

	- Acceso desde editores como Visual Studio Code con extensiones oficiales.

- Desventajas:

	- Menos flexible o configurable que Jenkins o GitLab CI/CD en escenarios avanzados.

	- Costos más altos por minuto de ejecución en planes pagos.

	- Dependencia de un único proveedor; si GitHub falla, no se pueden ejecutar workflows.

### Transferencia de conocimiento entre herramientas CI/CD

- Los conceptos de integración y despliegue continuo son universales y aplicables a cualquier herramienta.

- Aprender GitHub Actions facilita el aprendizaje de otras plataformas como GitLab CI/CD o Jenkins.

- En equipos, generalmente hay especialistas en DevOps que configuran y mantienen los pipelines.

- Los desarrolladores suelen consumir workflows ya creados, modificándolos mínimamente o usándolos tal cual.

## Configuración avanzada y buenas prácticas en GitHub Actions

### Uso de variables de entorno y secretos

- GitHub permite definir variables y secretos en la configuración del repositorio para proteger credenciales.

- Estas variables se referencian en los workflows con la sintaxis  ${{ secrets.NOMBRE_SECRETO }} .

- Es común usar secretos para claves SSH, tokens de acceso a Docker Hub o APIs externas.

- Cada repositorio puede tener sus propias claves para mayor seguridad y control de acceso.

### Organización y modularización de workflows

- Se pueden crear workflows independientes para build, test, deploy y orquestarlos mediante llamadas entre workflows.

- La directiva  needs  permite definir dependencias entre jobs para controlar el orden de ejecución.

- Separar lógica reutilizable en acciones propias evita duplicación y facilita mantenimiento.

- Los workflows se almacenan en la carpeta  .github/workflows  dentro del repositorio, versionados junto al código.

### Ejecución y monitoreo de workflows

- Los workflows se disparan automáticamente según eventos configurados, como push a ramas específicas o Pull Requests.

- La interfaz de GitHub muestra el estado de ejecución, logs detallados y permite revisar errores paso a paso.

- Se pueden cancelar ejecuciones en curso y configurar para que ejecuciones repetidas anulen las anteriores.

- Extensiones en Visual Studio Code permiten gestionar y revisar workflows sin salir del editor.

### Seguridad y gestión de accesos

- Es recomendable generar claves SSH específicas para cada repositorio y usuario para limitar riesgos.

- Las claves públicas se configuran en los servidores de destino y las privadas se almacenan como secretos en GitHub.

- GitHub Actions permite requerir aprobaciones específicas para merges en Pull Requests, aumentando la seguridad.

- Se pueden configurar revisores obligatorios y Draft Pull Requests para mejorar el control del código antes de integrarlo.

## Ejemplo práctico: creación y ejecución de un workflow básico

### Primer workflow "Hola Mundo"

- Se crea un archivo YAML con nombre arbitrario, por ejemplo  hola-mundo.yml , en  .github/workflows .

- Se define el evento que dispara el workflow, por ejemplo  on: push  a la rama main.

- Se configura un job que se ejecuta en un runner Ubuntu y contiene un step que ejecuta un comando bash simple, como  echo "Hola MUNDO" .

- Al hacer commit y push del archivo, el workflow se ejecuta automáticamente y se puede ver el resultado en la pestaña Actions de GitHub.

### Incorporación de checkout y comandos adicionales

- Para trabajar con el código del repositorio, se usa la acción oficial  actions/checkout@v4  para clonar el repositorio en el runner.

- Luego se pueden ejecutar comandos como  npm install ,  npm run build  o tests, según el proyecto.

- Se pueden definir múltiples jobs para build, test y deploy, y orquestarlos con dependencias usando  needs .

- Los logs muestran el contenido del directorio, variables de entorno y resultados de cada paso, facilitando la depuración.

### Uso de workflows llamados desde otros workflows

- Se pueden crear workflows que se ejecutan solo cuando son invocados por otros workflows mediante  on: workflow_call .

- Esto permite reutilizar lógica común, como build o test, en diferentes pipelines.

- La integración entre workflows facilita mantener orden y modularidad en procesos complejos.

- Se pueden definir inputs y outputs para parametrizar la ejecución de workflows llamados.

### Gestión de errores y salvaguardas

- GitHub Actions permite detener la ejecución si un paso falla, evitando despliegues con errores.

- Se pueden configurar notificaciones para alertar a los desarrolladores sobre fallos en la integración o despliegue.

- El linting y la validación de código son pasos comunes para asegurar calidad antes de integrar cambios.

- Estas salvaguardas ayudan a detectar y corregir errores lo antes posible, mejorando la estabilidad del proyecto.

## Futuro y aplicaciones prácticas de GitHub Actions

### Integración con despliegues en servidores y cloud

- GitHub Actions puede automatizar despliegues a servidores propios o servicios cloud como VPS, Netlify, Vercel o Railway.

- Se pueden ejecutar comandos remotos vía SSH para actualizar aplicaciones, reiniciar servicios o desplegar contenedores.

- La automatización reduce tiempos y errores en despliegues manuales, facilitando entregas frecuentes y confiables.

- En talleres y proyectos reales se muestra cómo configurar estas integraciones paso a paso.

### Compatibilidad con múltiples lenguajes y frameworks

- GitHub Actions soporta proyectos en Python, JavaScript, TypeScript, PHP, C#, Ruby y otros lenguajes populares.

- La configuración es adaptable a cualquier stack tecnológico, permitiendo ejecutar scripts, tests y builds específicos.

- La comunidad ofrece acciones predefinidas para muchos frameworks y herramientas, acelerando la configuración.

- Esto hace que GitHub Actions sea una solución versátil para proyectos de diversa índole y tamaño.

### Especialización y roles en equipos de desarrollo

- En equipos grandes, los desarrolladores de DevOps suelen encargarse de crear y mantener workflows complejos.

- Los desarrolladores de aplicación consumen estas acciones sin necesidad de profundizar en su configuración.

- Aprender GitHub Actions es valioso para roles de DevOps y para desarrolladores que quieran automatizar sus proyectos personales.

- La experiencia con GitHub Actions facilita la transición a otras herramientas CI/CD y mejora la productividad.

### Recursos y próximos pasos para aprender GitHub Actions

- GitHub ofrece documentación oficial, Marketplace con acciones preconstruidas y extensiones para editores.

- Se recomienda practicar creando workflows básicos y luego avanzar a configuraciones más complejas con múltiples jobs y llamadas entre workflows.

- En talleres y videos se muestran ejemplos prácticos de despliegue automático a servidores y gestión de secretos.

- La comunidad y el ecosistema de GitHub Actions están en constante crecimiento, ofreciendo nuevas funcionalidades y mejoras.