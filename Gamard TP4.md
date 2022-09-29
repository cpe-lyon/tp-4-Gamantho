#  Compte rendu TP 4 

### Exercice 1 

### Question 1 
```-sudo apt update / sudo apt upgrade```

### Question2 
pour créer un alias on utilise la commande : ```alias maj='sudo apt update'``` 
il faut l'enregistrer dans le dossier bashrc pour qu'il ne soit pas supprimer au démarrage

### Question 3 
2022-09-26 09:00:20 status half-configured install-info:amd64 6.8-4build1
2022-09-26 09:00:20 status installed install-info:amd64 6.8-4build1
2022-09-26 09:00:20 trigproc libc-bin:amd64 2.35-0ubuntu3.1 <none>
2022-09-26 09:00:20 status half-configured libc-bin:amd64 2.35-0ubuntu3.1
2022-09-26 09:00:20 status installed libc-bin:amd64 2.35-0ubuntu3.1

### Question 4
 On utilise la commande ```apt list --installed``` pour lister tout les dernier paquets installés explicitement avec la commande apt install
 
### Question 5 
On peut lister le nombre de paquets pour dpkg avec : 
```dpkg --list | wc --lines```
pour apt on utilise ```apt list --installed | wc -l.```
Le différence de comptage est entre la commande dpkg et apt est que la commande dpkg compte aussi les paquets supprimé. Il est impossible d'utilisé le fichier dpkg.log car il ne contient pas le nombre de paquets installés.

### Question 6 
On peut lister les paquets disponibles en téléchargement sur les dépôts Ubuntu avec la commande suivante :  ```apt-cache search . | wc -l```

### Question 7 
Glances est une application en mode caractère (ligne de commande) qui permet d'afficher l'état des principales ressources d'un système, de sa charge et du fonctionnement des applications.
Le paquet tldr nous permet de simplifier les pages des manuels
Le paquet Hollywood simule une fenêtre de hacking.

### Question 8 
On peut trouver les paquets permettant de jouer au sudoku en utilisant la commande vu plus haut ```apt-cache search sudoku```.

## Exercice 2 

Pour voir a partir de quel paquet est installé la commande ls on utilise la commande ```dpkg -S ls```

## Exercice 3 
Avec cette commande on peut afficher le status du package ```dpkg -s nom_du_paquet | grep status```.

## Exercice 4 
On peut lister les programmes avec la commande ```-apt-cache show coreutils```.

## Exercice 5 
```aptitude install (emacs/lynx)```

## Exercice 6 
Après l'ajout de Oracle dans le répertoire /etc/apt/sources.list.d on trouve le fichier : linuxuprising-ubuntu-java-jammy.list 

## Exercice 7 

### Question 2
On peut installer le logiciel avec la commande ```-sudo make install``` 

### Question 3 
Checkinstall permet de créer très facilement un paquet deb à partir des sources d'un logiciel.

## Exercice 8 

### Question 1 
On créer le sous dossier avec la commande ```-mkdir origine-commande```
```-mkdir DEBIAN``` 

### Question 2
On créer le fichier avec la commande ```-touch control``` 
Et on l'édit avec la commande suivante ```-nano touch```
et on rentre les données suivante : 
```
Package: origine-commande #nom du paquet 
Version: 0.1 #numéro de version
 Maintainer: Foo Bar #votre nom 
 Architecture: all #les architectures cibles de notre paquet (i386, amd64...) 
 Description: Cherche l'origine d'une commande
 Section: utils #notre programme est un utilitaire 
 Priority: optional #ce n'est pas un paquet indispendable
 ```
## Création du dépôt personnel avec reprepro 

### Question 1 
Pour créer le dossier repo-cpe on utilise la commande suivante : 
``` mkdir repo-cpe```

### Question 2 
Pour y créer les 2 sous dossiers on utilise la commande suivante : 
``` mkdir repo-cpe/conf```
``` mkdir repo-cpe/packages```

### Question 3 
Dans le dossier conf on créer le fichier distributions avec la commande suivante : ``` touch conf/distributions``` et on rentre les données suivante 

Origin: Un nom, une URL, ou tout texte expliquant la provenance du dépôt 
Label: Nom du dépôt // Suite: stable 
Codename: focal #!! A MODIFIER selon la distribution cible !! Architectures: i386 amd64 #(architectures cibles) 
Components: universe #(correspond à notre cas) 
Description: Une description du dépôt

### Question 4 
Dans le dossier repo-cpe on génère l’arborescence du dépôt avec la commande suivante ``reprepro -b . export``

### Question 5 
On copie le paquet origine-commande.deb dans le dossier packages : 
``cp origine-commande.deb ../repo-cpe/packages``
et on l'exécute : ``reprepro -b . includedeb cosmic origine-commande.deb``

### Question 6 
On doit à présent indiquer qu'il existe un nouveau dépôt pour cela on utilse la commande suivante : ``deb file:/home/VOTRE_NOM/repo-cpe cosmic multiverse``.
 
 ## Signature du dépôt avec GPG

### Question 1 

Commencez par créer une nouvelle paire de clés avec la commande 
``gpg --gen-key``

### Question 2 
 Ajoutez à la configuration du dépôt (fichier distributions la ligne suivante : ``SignWith: yes``

### Question 3 
Ajoutez la clé à votre dépôt : 

``reprepro --ask-passphrase -b . export ``

Attention ! Cette méthode n’est pas sécurisée et obsolète ; dans un contexte professionnel, on utiliserait plutot un gpg-agent.

### Question 4 
Ajoutez votre clé publique à votre dépôt avec la commande 
``gpg --export -a "auteur" > public.key``

### Question 5 
Enfin, ajoutez cette clé à la liste des clés fiables connues de apt : 

``sudo apt-key add public.key ``

Félicitations ! La configuration est (enfin) terminée ! Vérifiez que vous pouvez installer votre paquet comme n’importe quel autre paquet.


