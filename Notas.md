merge --no-ff <rama> (Historial de commits)
merge --squash (un solo commit de todo, no trae el historial de commit)

(git stash lo que permite es guardar el los cambios sin hacer commit)
git stash (guarda el estado de los cambios, para cambiar de forma segura a otra rama)
git stash push -m "<content>" (para guardar en un stack incluyendo un mensaje de los cambios)
git stash list (listar los commits )
git stash show -p || git stash show (muetra las diferencias del archivo vs lo que esta en el stack)
git stash apply (aplicar cambios del ultimo stack) o uno especifico git stash apply stash@{1}
git stash pop (aplicar ultimo stack y eliminarlo)
git stash drop <stash@{N}> (Eliminar un stash especifico de la lista)
git stash clear (limpia todos los stash)
git stash branch <name-branch> <stash@{N}> (crea y aplica los cambios en una rama, el stash debe existir)