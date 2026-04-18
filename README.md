# Taller Práctico de Git

¡Bienvenido a la práctica del taller de Git! Este repositorio ha sido preparado con un historial, ramas y algunos problemas intencionales para que apliques todos los conocimientos adquiridos.

Aquí utilizarás comandos de exploración, manipulación del historial, creación de archivos ignorados y resolución de conflictos. Todo utilizando únicamente archivos de texto.

Sigue las instrucciones paso a paso.

---

## Misión 1: Exploración del repositorio

Acabas de clonar/abrir este repositorio. Tu primer objetivo es entender en qué estado se encuentra y qué se ha hecho antes de que llegaras.

1. Abre tu terminal en esta carpeta (`fs-git-workshop-practice`).
2. Usa `git status` para ver el estado actual.
3. Usa `git branch` para ver en qué rama estás y qué otras ramas existen. (Pista: notarás que hay una rama llamada `borrador`).
4. Usa `git log --oneline` o `git log --graph --oneline --all` para ver el historial de commits. Observa los mensajes de los commits, hay un par que llaman la atención.
5. Crea dos archivos: `errores.log` y `sistema.log`
6. En el archivo `errores.log` agrega la linea "Error en la linea 1" con un editor de texto y guarda el archivo.
7. En el archivo `system.log` agrega la linea "Sistema inicializado" con un editor de texto y guarda el archivo.

---

## Misión 2: Eliminar el último error (usando `git reset`)

El último commit realizado en la rama `main` tiene el mensaje **"Capítulo 4 con un error tipográfico horrible"**. Resulta que ese capítulo es un desastre y no queremos que quede rastro de él en nuestro entorno local.

1. Como este commit es el más reciente (está de primero en tu `git log`), puedes eliminarlo por completo utilizando un reinicio "duro".
2. Ejecuta:
   ```bash
   git reset --hard HEAD~1
   ```
   *(Esto borrará los cambios del último commit por completo. ¡Úsalo con cuidado en la vida real!)*
3. Vuelve a ejecutar `git log --oneline` para confirmar que el "Capítulo 4" ya no existe en el historial.

---

## Misión 3: Deshacer un cambio de forma segura (usando `git revert`)

Imagina que el commit llamado **"Commit secreto que NO debió subirse"** introdujo un archivo sensible (`passwords.txt`). Como asumimos que este historial quizá ya se compartió con el equipo en el pasado, no debemos usar `reset` para borrar el historial pasado. La mejor forma de deshacer esto es con `revert`.

1. Usa `git log --oneline` para encontrar el identificador (hash corto de 7 letras/números) del commit con el mensaje **"Commit secreto que NO debió subirse"**.
2. Ejecuta el comando para revertirlo reemplazando `<hash>` con el que encontraste:
   ```bash
   git revert <hash>
   ```
3. Se abrirá tu editor de texto predeterminado de terminal (nano, vim, etc.) pidiendo confirmar el mensaje del nuevo commit de reversión. Simplemente guarda y cierra el editor. Si estas en vim para salir puedes usar `:wq`
4. Usa `ls` (mac/linux) o `dir` (windows) y nota que el archivo `passwords.txt` ha desaparecido, pero el historial (con `git log`) muestra que la reversión quedó documentada.

---

## Misión 4: Ignorando ruido con `.gitignore`

Notaste al principio que los archivos `sistema.log` y `errores.log` te molestan cada vez que haces `git status`. Son archivos autogenerados y nunca queremos subirlos al repositorio.

1. Crea un archivo llamado `.gitignore` en esta carpeta principal. Puedes hacerlo desde tu editor de código o terminal.
2. Abre el `.gitignore` y añade la siguiente línea para ignorar cualquier archivo de extensión `.log`:
   ```text
   *.log
   ```
3. Guarda el archivo `.gitignore`.
4. Ejecuta `git status`. Verás que los archivos `.log` ya no aparecen como "untracked", y en su lugar solo aparece el `.gitignore` listo para ser añadido.
5. Agrega y haz el commit del `.gitignore`:
   ```bash
   git add .gitignore
   git commit -m "Añadir .gitignore para ignorar logs"
   ```

---

## Misión 5: El Choque de Dos Mundos (Resolución de Conflictos)

Mientras tú trabajabas en `main`, un compañero estuvo escribiendo el final de la historia en la rama `borrador`. Es hora de juntar su trabajo con el tuyo.

1. Estando en la rama `main`, ejecuta el comando para fusionar la rama `borrador`:
   ```bash
   git merge borrador
   ```
2. ¡Oh no! 🚨 Recibirás un mensaje de **CONFLICT**. Git te pedirá que lo resuelvas.
3. Abre el archivo `historia.txt` en tu editor de texto.
4. Verás unas marcas extrañas dejadas por Git:
   ```text
   <<<<<<< HEAD
   (Lo que tú tienes en main)
   =======
   (Lo que tiene la otra rama)
   >>>>>>> borrador
   ```
5. Tu trabajo es borrar esas marcas (los `<`, `=`, `>`) y dejar el texto condensado en una versión final que tenga sentido combinando lo mejor de ambas ideas, o quedándote con la que prefieras. Guarda el archivo.
6. Dile a Git que ya resolviste el problema añadiendo el archivo modificado:
   ```bash
   git add historia.txt
   ```
7. Completa el merge creando el commit de fusión:
   ```bash
   git commit -m "Merge rama borrador y resolución de conflicto en la historia"
   ```

---

## ¡Felicidades! 🎉

Has completado la práctica. Has explorado el historial, reiniciado ramas, revertido commits de forma segura, ignorado archivos y resuelto conflictos usando únicamente comandos de Git. ¡Ya estás listo para colaborar sin miedo a romper cosas!
