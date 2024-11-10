# Preparar certificación de Git 🤖


# Tipos de Fusion

1. **Fast-Forward** 
Cuando la rama origen esta por delante de la rama destino git solo mueve el puntero de la rama destino al ultimo commit de la rama origen.
  
```bash
  git merge --ff-only nombre-rama-origen
```

    
2. **No Fast-Forward (True merge)**

Cuando la rama origen no esta por delante de la rama destino oasea que la rama que va a recibir los cambios tiene commits distintos a la rama que queremos fusionar en este caso git crea un nuevo commit qie incluye todos los cambios de la rama origen a la rama destino.

```bash
  git merge nombre-rama-origen --no-ff
```

3. **Squash**

Junta todos los commits de la rama origen es un  solo commit que debe ser confirmado.

```bash
  git merge nombre-rama-origen --squash
  git commit -m "Descripción del cambio"
```

4. **Rebase**

Rebase toma los commits de la rama origen y los aplica sobre la rama destino, creando un historial lineal. Esto es útil para integrar cambios y mantener un historial limpio.

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
