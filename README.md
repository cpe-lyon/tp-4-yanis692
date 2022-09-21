[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-c66648af7eb3fe8bc4f294546bfd86ef473780cde1dea487d3c4ff354943c9ae.svg)](https://classroom.github.com/online_ide?assignment_repo_id=8562805&assignment_repo_type=AssignmentRepo)

# Exercice 1. Commandes de base

1. On peut mettre a jour notre système avec la commande sudo apt update.

2.Pour crée un l'alias "maj" il faut faire la commande suivante alias maj='sudo apt update'. Il faut enregistrer l'alias dans le fichier .bashrc car celui-ci estr lu a chaque démarrage.

3. 

4.

5. 
```
dpkg -l | wc -l
``` 
```
apt list --installed | wc -l
```
Cette différence de comptage est du a des ligne d'erreur et ou de commentaire qui sont pris en compte.
On ne peut pas utiliser le fichier dpkg.log car comme son nom l'indique il est present pour garder un historique des différent paquet utiliser.

6. ```
cat /etc/apt/sources.list
``` on peut observer 20 liens disponible.

7. L'outil glances est comparables au gestionnaire des taches de windows.Pour lancer cette outil il faut juste entrer ```glences```. Tldr permet de rendre plus accéssibles les information du manuelle, il va simplifier le manuelle est nous afficher que les point les plus importants pour l'utilisateur, c'est-a-dire, la commande et ses options.
L'outil hollywood est un outil 'fun' c'est a dire il va simuler une attaque informatique est va alors afficher plusieurs information, du binaire et autre qui feront croire que vous realiser une attaque informatique.

8.Le paquet qui permet d'installer sudoku est apt install gnome-sudoku.

# Exercice 2

```dpkg -S /bin/ls``` 
est la commande qui permet de voir quel est le paquet qui a installée la commande ls. Le paquet est ```coreutils: /bin/ls```
En une seule commande cela reviendrai a faire 
```wich -a ls | xargs dpkg -S 2>/dev/null | cut -f1 -d:```
le script est le suivant:

```
#!/bin/bash
wich -a $1 | xargs dpkg -S 2>/dev/null | cut -f1 -d:
```


# Exercice 3

```
dpkh -l coreutils 2>/dev/null | grep"^ii" > /dev/null && echo "install" || echo "pas installée"
```
# Exercice 4

'''
dpkg -L coreutils
'''

# Exercice 5
