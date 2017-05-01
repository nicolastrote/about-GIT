# tuto_github
Notes personnelles pour utiliser Git et GitHub

# INSTALLATION
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

# RÉALISER UN COMMIT
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
# CONNAITRE L'HISTORIQUE DES COMMITS
Connaitre toutes les modifications :
```
$ git log
```
# ANNEXE: SE POSITIONNER SUR UN COMMIT DONNE'
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
# TRAVAILLER AVEC GITHUB
Aller sur https://github.com, se créer un compte, noter le USER (nicolastrote) et votre MOTDEPASSE
Avec l'icon "+" créer un répertoire au même nom que votre projet (ie: conkyForGnome3 )
Créer le lien entre le git local et github :
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
# CHEAT SHEET
![cheatsheet](https://github.com/nicolastrote/tuto_github/blob/master/Git-Cheat-Sheet.png)
