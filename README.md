# entregable-1-cicd

## Integrantes

**Manuela Jiménez Arredondo**

- Manuela Jiménez Arredondo — usuario de GitHub: `manujimeneza` 

## Ejecución exitosa

Enlace a una ejecución exitosa de `mi_workflow.yml`: https://github.com/manujimeneza/entregable-1-cicd/actions/runs/42389546001

## Respuestas

### 1. ¿Qué eventos configuraste para disparar tu workflow y por qué?

Configuré tres eventos:

- **`push`** en las ramas `main` y `develop`. Así el workflow se ejecuta cada vez que se suben cambios a esas ramas. Agregué `develop` además de lo pedido en el taller para poder ver cómo se aplicaba el cambio en las dos ramas.
- **`pull_request`** hacia `main`. Lo agregué para comprobar que el workflow también se ejecuta cuando se abre un PR de `develop` hacia `main`, antes de fusionar los cambios.
- **`workflow_dispatch`**, para ejecutarlo manualmente desde la pestaña Actions.

En resumen, agregamos más de lo que pedía el taller para poder observar cómo se activaba el workflow con cada evento y en cada rama.

### 2. ¿Qué sistema operativo utiliza el runner `ubuntu-latest` y por qué puede ejecutar tu workflow aunque mi computadora sea Windows o macOS?

El runner `ubuntu-latest` usa Ubuntu Linux. Es una máquina virtual que GitHub crea en la nube para cada ejecución, así que no depende de mi computadora. Mi computadora solo envía el archivo YAML a GitHub, y GitHub lo ejecuta en su propio runner.

El shell de los pasos `run` es el programa que interpreta los comandos de ese paso. Con `shell: bash` le indico al runner que use Bash para ejecutar los comandos. Por eso el comando `date` funciona de la misma forma que en Ubuntu, sin importar el sistema operativo de mi computadora.

### 3. Acciones del Marketplace de GitHub Actions

- **`github/super-linter`**: ejecuta varios linters a la vez sobre el código del repositorio (por ejemplo, para Python, YAML o Markdown). Sirve para detectar errores de estilo y de sintaxis antes de fusionar cambios.
- **`actions/cache`**: guarda y reutiliza archivos entre ejecuciones, como dependencias descargadas. Sirve para acelerar los workflows que instalan muchas librerías.
- **`actions/github-script`**: permite ejecutar código JavaScript dentro de un workflow, con acceso a la API de GitHub. Sirve para automatizar tareas como comentar en un PR o etiquetar issues.

### 4. ¿Qué es un secreto en GitHub Actions y para qué se usa? ¿Cómo lo usarías en mi workflow?

Un secreto es un valor cifrado, como una contraseña, un token o una clave de API, que se guarda en la configuración del repositorio (Settings → Secrets and variables → Actions). Sirve para usar credenciales dentro del workflow sin escribirlas en el código.

Se usan con la sintaxis `${{ secrets.NOMBRE_DEL_SECRETO }}`. GitHub oculta su valor en los logs. En este taller no necesito ningún secreto, porque el workflow solo lee el código y no se conecta a servicios externos. Si mi workflow desplegara la aplicación en un servidor, guardaría la clave de acceso como secreto y la pasaría a un paso `run` mediante una variable de entorno.

### 5. Reflexión: uso de GitHub Actions en mi flujo de trabajo diario

Después de este taller entendí mejor para qué sirve GitHub Actions, y se me ocurren varias cosas que automatizaría en mi trabajo diario. La primera sería revisar los Pull Requests antes de que lleguen al revisor, para comprobar que tengan descripción, impacto, métricas, observabilidad, plan de despliegue, las pruebas manuales que se hicieron y el changelog. Lo haría así porque hoy esas cosas dependen de que alguien se acuerde, y un workflow las revisaría siempre igual. También agregaría un paso con IA que lea el PR completo y deje comentarios comparándolo con la definición de la tarea, porque así se detectan desviaciones antes de la revisión humana y el revisor gasta menos tiempo en cosas repetitivas. Y por último me gustaría un pipeline que pruebe los endpoints entre una aplicación y otra en cada PR, porque ahora esas pruebas las hago a mano, consumen tiempo y es fácil saltarse alguna.
