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

git Amend 
    Habilita la modifica del commit mas reciente 

    Cuando usarlo: 
        Necesidad de hacer cambios peque;os al ultimo commit
        Corregir errores, 
        Agregar archivos olvidados, faltantes
        Actualizar el mensaje del commit

        git commit --amend -m "mensaje"

    Remover Archivo del ultimo commit
        1. git reset HEAD^ -- <file> remueve el archivo del staging area
        2. git commit --amend

git rebase

    Rebasing mueve o combina una secuencia de commit en una nuevo commit

    Usado para 
        Limpiar
        Tener un historial lineal del proyecto
    
    Cuando usar rebase: 
        Mantener limpio, historial del proyecto lineal
        Evitar merge commit innecesarios
        Combinar multiple commits en uno solo
        Editar o reordenar commits 
    
    Ejemplo
        git checkout feature-branch
        git rebase main

    git rebase -i <base> Interactive Rebase -- edit, reorder, squash or fix up commits before a certain point. 

    git rebase -i HEAD~3
        open an editor where you can
            pick keep the commit as is 
            squash combine commits together
            edit pause to change a commit 
            reword change just the commit message

    git rebase --continue 
    git reabse --abort 
    git rebase --skip 

git reflog
    recover lost commits or changes
    
    git reflog expire --expire=30.days refs/heads/main
    git gc --prune=now

git recovery 
    means getting back lost commits, branches or files

    git keeps a record of recent changes so you can undo mistakes-even after a reset or delete 

    cuando usar
        Accidentalmente eliminar un branch o un file 
        Reset your branch a un commit previo y lose changes
        Necesidad de recuperar commits o cambios perdidos
    
    git reflog

    q -b branch-name <commit-hash> -- Restore a deleted branch, if you deleted a branch but the commits are still in reflog, you can recreate it

    Recover a deleted od changed file 
        git restore filename.txt 
    
    Recover from a hard reset 
        1. git reflog 
        2. git reset --hard HEAD@{2}

.gitattributes
    special file that tells how to handle specific file in repositories

    controls things: 
        - line endings
        - file types 
        - merge behavior
        - custom diff tools
        - ...

    when to use
        - enforce consistent line endings across different OS
        - mark files as binary 
        - enable git LFS for large files
        - set up custom diff or merge tools for special file types
        - control how files are exported in archives
    
    Create or Edit:
        1. go to the root of your repository
        2. create or edit the .gitattributes file
        3. Add rules, one per line, for git should treat files
    
        examples:
            1. Force Unix Line Endings for All Text Files - *.txt text eol=lf
            2. Set LF for Shell Scripts - *.sh text eol=lf
            3. Mark PNG Files as Binary - *.png binary
            4. Track PSD Files with LFS - *.psd filter=lfs diff=lfs merge=lfs -text
            5. Custom Diff for Markdown - *.md diff=markdown
            6. Check Attributes of a File - git check-attr --all README.md
            7. Ignore Files on Export - docs/* export-ignore

git LFS
    Large File Storage (LFS): extension for git that helps manage large files (like videos, images, or dataset) efficiently

    Instead of storing biug files directly in repository, LFS stores a small pointer file in repo and keeps the real content on a separate server. 

    That keeps the repo fast and small

    Every one who clones the repo gets the pointer, and Git LFS fetches the real file content as needed. 

    when to use
        - need to version large files
        - the project exceeds the file size limits of standard git hosting
        - want to keep your repository size manageable and fast
    
    installation
        1. download  git-lfs.github.com.
        2. Initialize LFS in the repository git lfs install
    
    Track files
        examples
            git lfs track "*.psd"
            git lfs track "*.zip"
            git lfs track "images/*.{png,jpg}"

    Check LFS Status
        git lfs ls-files
    
    Untrack/Remove Files 
        1. Edit .gitattributes
        2. or Run the untrack command - git lfs untrack "*.psd" -> git add .gitattributes

    Tips & Best Practices
        Use LFS only for files that are too large or change too often for regular git 
        check if your hosting provider supports LFS before using it
        Monitor your LFS storage quota

git signing
    Signing a commit is like putting your personal signature on your work

    What is GPG?
        GPG (GNU Privacy Guard) is a tool taht lets you create a digital key, kind of like a secret pwd, to sign things

        git uses GPG keys to sign commits and tags

        This helps prove your identity and ensures your code hasn't been tampered with.

    Why and When Should You Sign Commits?
        - To prove your commits really came from you
        - To help others trust your code (especially in open source projects)
        - Some companies or projects require signed commits for security
        - If you don't sign, your commits are still valid, just not verified
    
    How to Set Up Commit Signing
        Create a GPG key (if you don't have one):
            gpg --full-generate-key

        Find your key ID 
            gpg --list-secret-keys --keyid-format=long
        
        Set Signing Key
            git config --global user.signingkey <your-key-id>

        How to Sign Commits and Tags
            To sign a commit, use:
                git commit -S -m "message"

            To sign a tag, use:
                git tag -s v1.0 -m "version 1.0"
        
        Sign All Commits Automatically
            git config --global commit.gpgSign true
        
        How to Check if a Commit is Signed
            git log --show-signature

git cherry-pick & Patch

    cherry-pick 
        lets you copy a single commit from one branch to another. 
    
    Patch
        is a file with changes from one or more commits. you can share a patch or apply it ot another repository, even if it's'unrelated to your own

    when use
        cherry-pick
            to copy a commit between branches in the same repository 
        patches 
            to share changes as files, or when working across different repositories 
    
    How to Cherry-pick a Commit 
        Cherry-pick a Commit - git cherry-pick abc1234
    
    Edit the Commit Message
        git cherry-pick abc1234 --edit
    
    Apply Without Committing
        git cherry-pick abc1234 --no-commit
    
    Add Commit Origin
        Use -x to add a line to the commit message showing where the commit came from:
        git cherry-pick abc1234 -x
    
    Handling Conflicts
        If there are conflicts, Git will pause and ask you to fix them. After fixing, run:
        1. git add .
        2. git cherry-pick --continue
    
    Abort Cherry-pick
        git cherry-pick --abort

    How to Create a Patch
        git format-patch -1 abc1234

        Multiple Commits
            git format-patch HEAD~3
        
        How to Apply a Patch
            git apply 0001-some-change.patch

        Apply a Patch and Keep Metadata
            git am 0001-some-change.patch
        
        Reverse a Patch
            git apply -R 0001-some-change.patch