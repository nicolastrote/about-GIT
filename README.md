# About GIT, GITHUB & GITLAB
Notes personnelles pour utiliser Git, GitHub et GitLab

## INSTALLATION
source: http://git-scm.com/downloads ils conseillent :
```
$ apt-get install git
```
Puis on le configure
```
$ git config --global color.ui true
$ git config --global user.name "YOUR NAME"
$ git config --global user.email "YOUR@EMAIL.com"
```
If you don't have ssh key, you should:
```
$ ssh-keygen -t rsa -C "YOUR@EMAIL.com"
```
The next step is to take the newly generated SSH key and add it to your Github account.
```
$ cat ~/.ssh/id_rsa.pub
```
Copy the key and paste it on github:https://github.com/settings/keys
Et tel un hero vous pouvez faire une vérification de connexion ssh :
```
$ ssh -T git@github.com
```
Once you've done this, you can check and see if it worked:
```
$ git
```

## RÉALISER UN COMMIT
```
$ git init
$ nano exemple.py
$ git add exemple.py     // fichier ajouté à l'index du projet
$ git commit -am "création du premier fichier"
```
ps : l'option -a permet de commiter des fichiers déjà connus par git
ps : l'option -m permet de rajouter un message au commit

Savoir si tous les fichiers ont bien été commité utiliser :
```
$ git status
```
réponse
```
"modified"
```

## CONNAITRE L'HISTORIQUE DES COMMITS
Connaitre toutes les modifications :
```
$ git log
```

## SE POSITIONNER SUR UN COMMIT DONNE'
```
$ git log
```
repérer le SHA de l'ancienne version ou il faut revenir
```
$ git checkout SHA
```
revenir sur le dernier commit de la branche principale
```
$ git checkout master
```
## GITIGNORE
 * créer un fichier .gitignore avec le nom des fichiers ou dossiers à ne pas suivre
 
 * Si un fichier ne suit pas les règles locales, car sur le projet il est suivi il faut re-initier les règles locales avec la commande :
 ```
  $ git rm -r --cached *lock.json
 ```
## ALIAS

 * créer un fichier .gitconfig dans votre user (pour l'utiliser sur tous les projets)
 * puis rajouter par exemple :
 ```
  [alias]
    # basic
    st = status
    df = diff
    co = checkout
    ci = commit
    br = branch -a
    who = shortlog -sne
    
    # Annuler le dernier commit
    undo = git reset --soft HEAD^
    
    # Éditer le dernier commit
    amend = commit --amend
    
    # Editer l'état
    changes = diff --name-status
    dic = diff --cached
    diffstat = diff --stat
    
    # historique
    oneline = log --pretty=oneline --abbrev-commit --graph --decorate
    
    # afficher changements
    lc = !git oneline ORIG_HEAD.. --stat --no-merges
 ```
 
 * la commande config permet de créer l'alias en ligne de commande
 ```
  $ git config --global alias.st 'status'
 ```
 
## REALISER UNE TASK A PARTIR D UNE BRANCHE EN COURS DE DEVELOPPEMENT
  * créer sa branche task et faire son checkout dessus
  * git fetch
  * `git reset --hard origin/[nom de la branche en cours de developpement]`
  * `git push -f`   pour avoir la meme branche
Ainsi à la fin du développement, la branche en cours pourra faire le cherry-pick du travail effectué dans la tache.

## REBASE TES COMMITS !

Pour travailler dans ce mode de travail, qui n'est de pousser qu'un seul commit, il faut à chaque pull de dev faire un rebase: 
  * `git pull --rebase`
ou intégrer dans la config de git
  * `git config --global pull.rebase true`

A la fin de votre travail, avant de pousser le code pour une PR, voici la démarche:
  * `git commit -am "le travail en cours"`   
  * `git push`   // le travail en cours
  * `git fetch`   // recupère bien ce qui est en remote
  * `git log`    
    dans le log on cherche la clé du commit qui précède tous tes commits, la base avant tes modifications
  * `git reset --soft 942837494792834792837492834792`  (la clé du commit)
  * relancer les tests pour s'assurer que tout va bien, sinon ajoute les modications
  * `git commit -am "le travail rebasé"`
  * `git push -f`
  * `git fetch`
  
A ce stade aller dans bitbucket dans l'onglet COMMITS. Si ton commit est bien à la base de develop, alors le travail est fini, si c'est pas le cas : 
  * git rebase origin/develop
  resoudre les conflits, sans faire de commits
  * git add   les nouveaux fichiers si nécessaire
  * git rebase --continue
  * git push -f origin ta_branch_de_travail
  
## TU T ES TROMPÉ DE BRANCH POUR TRAVAILLER ?

Exemple d'un travail réalisé sur "develop" au-lieu de "branch34"
  * commit ton travail develop en étant sur ta branch develop locale ```git commit -am "mon commit"```
  * créer sur le remote la branche "branch34"
  * realise un ```git fetch```, puis un ```git checkout branch34```
  * maintenant on recupère ton travail de develop sur branch34 avec un merge : ```git merge develop```
  * tu peux maintenant pousser ta branche locale "branch34" sur la branch remote "branch34": ```git push``` 
  
## TOUT SUR STASH

```git stash save "my_stash"```
where "my_stash" is the stash name...

```git stash list```
This will list down all your stashes.

To apply a stash and remove it from the stash stack, You can give,

```git stash pop stash@{n}```
To apply a stash and keep it in the stash stack, type:

```git stash apply stash@{n}```
Where n in the index of the stashed change.
 
## REVERT LAST COMMIT BUT KEEP CHANGES
```
$ git reset --soft HEAD~1
```
 
# TRAVAILLER AVEC GITHUB
Aller sur https://github.com, se créer un compte, noter le USER (nicolastrote) et votre MOTDEPASSE
Avec l'icon "+" créer un répertoire au même nom que votre projet (ie: conkyForGnome3 )

## 1ere solution avec clone
Récupérer le repository en le clonant, la partie "remote" sera enregistrée automatiquement par GIT:
```
$ git clone https://github.com/nicolastrote/java_spring.git
```
Pour la nouvelle branche il faudra la créer avec Github, puis:
```
$ git pull origin develop     ou master suivant le nom de la branche d'origine
$ git branch -a               pour lister toutes les branches
$ git checkout le-nom-de-la-nouvelle-branche
```
Faire le push :
```
$ git push
```
Puis faire une pull request à partir de GitHub

## 2d solution avec remote
Cette méthode permet de pousser un projet complet sur GitHub.
* Créer sous GitHub un projet sans licence ni .gitignore
* localement initialiser le git
``` git init```
* Ajouter tous les fichiers à git
```git add . ```
* Faire le premier commit
```git commit -m "first commit"```
* Créer le lien entre git et github
```git remote add origin https://github.com/nicolastrote/angular-fitness.git```
* Il est tant de pusher :)
```git push -u origin master```

## RECUPERER LES DONNEES EN LOCAL DE GITHUB
Git pull does a git fetch followed by a git merge
```
$ git pull
```
A git pull is what you would do to bring a local branch up-to-date with its remote version, while also updating your other remote-tracking branches.

## METTRE A JOUR SES BRANCHES
You can do a git fetch at any time to update your remote-tracking branches under refs/remotes/<remote>/
```
$ git fetch
```

## VIDER L HISTORIQUE DES COMMANDES
```
$ history -c
```

# TRAVAILLER AVEC GITLAB
Aller sur https://gitlab.com, se créer un compte (https://gitlab.com/nicolastrote), enregistrer sa clef publique SSH.

Cloner un repository :
une fois cloner, le remote est en place.
```
$ git clone git@gitlab.com:monrepository/lenomdelabrancheMaster.git
```
Créer une branche sur gitLab par exemple, puis faire un checkout dessus :
```
$ git checkout nom_de_la_branche_uniquement
```
Puller et Pousser son code dessus :
```
$ git pull
$ git push   
$ git push origin nom_de_la_branche_uniquement
```
Le git merge sera fait sur GitLab qui permet de voir les differences, rajouter des codes reviewers, des imprim-ecrans...

# CHEAT SHEET
![cheatsheet](https://github.com/nicolastrote/tuto_github/blob/master/Git-Cheat-Sheet.png)
