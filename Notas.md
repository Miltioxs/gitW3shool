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

git branch -D || git branch -d (elimina la rama con -d o forzar con -D )

git restore --staged <file> (saca los cambios de un archivo del staging area, regresaria al working directory)
git reset HEAD~ (deshacer el ultimo commit hecho y llevarlo al working)
git commit --amend (modifica el contenido del mensaje del commit o se pueden agregar nuevos archivos al commit)

# Ejemplo para agregar un archivo nuevo a un commit
1. git add Notas.md
2. git commit --amend --no-edit (para no editar el mensaje del commit --no-edit)

Summary of SSH Concepts and Commands

    SSH key pair - A public and private key for secure access
    ssh-keygen - Generate a new SSH key pair
    ssh-add - Add your private key to the SSH agent
    ssh -T git@github.com - Test SSH connection
    ssh-add -l - List loaded SSH keys
    ssh-add -d - Remove a key from agent

eval $(ssh-agent -s) (habilitar ssh agent en WSL)
ssh-keygen -t rsa -b 4096 -C "<mail>" (generar ssh key)
ssh-add ~/.ssh/id_rsa (a;adir el key a mi agente ssh)
cat ~/.ssh/id_rsa.pub (copiar mi llave publica)
ssh-add -l (listar las llaves cargadas al agente ssh)

ssh -T git@github.com (probar conexion luego de haber agregar la llave ssh en github)

git remote add origin git@github.com:Miltioxs/gitW3shool.git (agregar el origen remoto por primera vez)
git remote set-url origin git@github.com:Miltioxs/gitW3shool.git (actualizar remoto para usar ssh)

git push --set-upstream origin main ()

git fetch origin
git status
git log origin/<branch>


git switch branch-name

git push origin --delete branch-name (eliminar rama remota)
git branch -m old-name new-name (renombrar ramas)

git branch -a (ver ramas remotas que no estan localmente)
git branch -r (ver ramas remotas)

git revert (deshace el ultimo commit y crea uno nuevo que revierte los cambios), 
    |_ mantiene el historial de commits intacto
    |_ es la forma mas segura para deshacer cambios en un repositorio compartido

    git revert HEAD (Revierte el ultimo commit)
    git revert <commit> (Revierte a un commit specifico)
    git revert HEAD~2 
    git revert --no-edit (skipea el editor de mensajes del commit)
    git log --oneline (muestra el historial de commit)

Tips & Best Practices

Here are some tips and best practices to keep in mind when using Git Revert:

    Use git revert instead of git reset when you want to undo a previous commit, but still keep the commit history intact.
    Use git log --oneline to find the commit you want to undo.
    Use git revert HEAD --no-edit to create a new commit that reverses the changes.

git reset (mueve mi rama a un diferente commit)
    usar cuando:
        - deshacer commits, unstage files, or clean up history
    
    git reset --soft <commit> Mover el HEAD a un commit, pero mantenes los cambios en el area Staged, para juntar todo en solo commmit, o reescribir el historial de commits 

    git reset --mixed <commit> Mover el HEAD a un commit, unstage changes (default), entiendo que pasa los cambios a working directory

    git reset --hard <commit> Mover el HEAD a un commit, descarta todos los cambios

    git rest <file> Unstage un archivo

    git long --online Muestra el historial de commits 