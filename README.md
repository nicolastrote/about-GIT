# GIT et GITHUB
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
# Pour ignorer des fichiers
 * créer un fichier .gitignore avec le nom des fichiers ou dossiers à ne pas suivre
 
 * Si un fichier ne suit pas les règles locales, car sur le projet il est suivi il faut re-initier les règles locales avec la commande :
 ```
  $ git rm --cached docker-compose.yml
 ```

## TRAVAILLER AVEC GITLAB

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
Créer le lien entre le git local et GitHub :
```
$ git remote add origin https://github.com/nicolastrote/conkyForGnome3.git
```
Faire le push :
```
$ git push origin master
```
Si cela ne marche pas, on peut forcer le push (dans le cas où vous aviez déjà travailler dans github, et que vous voulez écraser votre ancien projet github par celui de votre pc)
```
$ git push -f origin master
```

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
