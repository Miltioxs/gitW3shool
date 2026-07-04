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
ssh-keygen -t rsa -b 4096 -C "x" (generar ssh key)
ssh-add ~/.ssh/id_rsa (a;adir el key a mi agente ssh)
cat ~/.ssh/id_rsa.pub (copiar mi llave publica)
ssh-add -l (listar las llaves cargadas al agente ssh)

ssh -T git@github.com (probar conexion luego de haber agregar la llave ssh en github)

git remote add origin git@github.com:Miltioxs/gitW3shool.git (agregar el origen remoto por primera vez)
git remote set-url origin git@github.com:Miltioxs/gitW3shool.git (actualizar remoto para usar ssh)

git push --set-upstream origin main ()