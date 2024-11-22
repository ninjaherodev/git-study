# Preparar certificación de Git 🤖

## Que es Git

Git es un sistema que permite guardar y gestionar cambios en archivos, especialmente cuando
se trabaja en equipo o en proyectos grandes. Imagina que estás escribiendo un libro y cada
vez que haces cambios, Git crea una "foto" de cómo estaba el libro en ese momento.
Así, si en algún momento quieres volver a una versión anterior (porque cambiaste de idea o
cometiste un error), puedes regresar fácilmente sin perder nada.

Además, Git ayuda a que varias personas trabajen juntas en los mismos archivos sin que se
sobreescriban sus cambios. Cada uno puede trabajar en su "copia", y al final, Git se encarga
de combinar todas las contribuciones para crear una versión completa y actualizada del
proyecto.

## Configuración Basica

para ayudar a git saber quien hizo un commit tenemos:

```bash
  git config --global user.name "hackchan"
  git config --global user.email "fabiorojas7@gmail.com"
  git config --list
```

## Inicializar un repositorio

```bash
  mkdir Cats
  cd Cats
  git init
```

## Git pull

git pull es el comando que se utiliza para actualizar tu repositorio local con los cambios más
recientes que hayan sido publicados en el repositorio remoto, fusionándolos automáticamente en
tu rama actual. Esencialmente, combina dos comandos: git fetch (que descarga los cambios) y git
merge (que los integra a tu rama activa). Esto te permite mantener tu trabajo en sincronía con
el progreso de otros colaboradores o con actualizaciones externas.

```bash
  git pull origin main
```

## Git push

git push es el comando que utilizas para subir tus cambios locales al repositorio remoto en la
misma rama o en una rama específica. Esto permite que otros colaboradores puedan acceder a tu
trabajo y continuar construyendo sobre él. git push solo sube los cambios que hayas confirmado
(con git commit) a tu repositorio local, y no afecta directamente el trabajo de otros hasta que
ellos actualicen sus propios repositorios con git pull.

```bash
  git push origin feature-branch
```

✍️ La primera vez que subes una nueva rama, es útil utilizar el flag -u (upstream) con el
comando git push, como en git push -u origin feature-branch. Esto establece la rama remota
como la predeterminada para futuras actualizaciones, facilitando los siguientes git push o
git pull.

## Git Fetch

git fetch es un comando que se usa para descargar todos los cambios del repositorio remoto,
pero sin integrarlos en tu rama actual. Este comando solo actualiza las referencias de las
ramas remotas, permitiéndote revisar qué cambios existen antes de aplicarlos en tu propio
trabajo. Esto es útil si prefieres inspeccionar los cambios y decidir cuándo y cómo fusionarlos
en tu rama.

```bash
 git fetch origin
```

Nota: Después de ejecutar git fetch, puedes ver los cambios descargados utilizando comandos como
git log origin/main. Si decides integrarlos, puedes utilizar git merge origin/main o, si quieres
actualizaciones completas, git pull.

```bash
 # ver los commits que estan en remoto que no tengo en mi local
 git log HEAD..origin/main
 git log main..origin/main

 #ver el codigo que esta en remoto y no esta integrado en mi local
 gut diff HEAD..origin/main
```

## Tipos de Fusion

A. **Fast-Forward**
Cuando la rama origen esta por delante de la rama destino git solo mueve el puntero de la rama
destino al ultimo commit de la rama origen.
  
```bash
  git merge --ff-only nombre-rama-origen
```

B. **No Fast-Forward (True merge)**
Cuando la rama origen no esta por delante de la rama destino oasea que la rama que va a recibir
los cambios tiene commits distintos a la rama que queremos fusionar en este caso git crea un
nuevo commit qie incluye todos los cambios de la rama origen a la rama destino.

```bash
  git merge nombre-rama-origen --no-ff
```

C. **Squash**

Junta todos los commits de la rama origen es un  solo commit que debe ser confirmado.

```bash
  git merge nombre-rama-origen --squash
  git commit -m "Descripción del cambio"
```

D. **Rebase**

Rebase toma los commits de la rama origen y los aplica sobre la rama destino, creando un
historial lineal. Esto es útil para integrar cambios y mantener un historial limpio.

```bash
  # Cambia a la rama `caracteristicas`
  git checkout caracteristicas
  git fetch origin
  # Realiza un rebase de `main` en tu rama `caracteristicas`
  git rebase main

  #si hay conflictos:

  git add <archivos_resueltos>
  git rebase --continue

  #si decido cancelar rebase 
  git rebase --abort
  # si a habia subido mi rama al remoto y hago rebase para volverla a subir a remoto ya que se requiere forzar para sobreescribir el historial remoto 
  git push --force-with-lease
```

## Rebase vs Merge

recomiendo que si estas en una rama que no esta compartida en remoto y solo es de uso personal realizar esa 
sincronización con la rama main con un rebase.

```bash
 git checkout feature
 git rebase main|
```

pero si estas en una rama que tiene varios colaboradores o la rama principal (main, master)
realizar un merge y que se cree ese commit de fusión.

```bash
 git checkout main
 git merge feature
```
