TP 4

# Exercice 1. Commandes de base

## 1. Commencez par mettre à jour votre système avec les commandes vues dans le cours.
On peut mettre a jour notre système avec la commande sudo apt update.
## 2. Créez un alias “maj” de la ou des commande(s) de la question précédente. Où faut-il enregistrer cet
alias pour qu’il ne soit pas perdu au prochain redémarrage ?
Pour crée un l'alias "maj" il faut faire la commande suivante alias maj='sudo apt update'. Il faut enregistrer l'alias dans le fichier .bashrc car celui-ci estr lu a chaque démarrage.
## 3. Utilisez le fichier /var/log/dpkg.log pour obtenir les 5 derniers paquets installés sur votre machine.
```
grep installed /var/log/dpkg.log | tail -n5 | cut -d: -f1
```
![image](https://user-images.githubusercontent.com/77662970/194319416-68c55fd1-a7d0-4016-b6cb-7314c65506dc.png)

## 4. Listez les derniers paquets qui ont été installés explicitement avec la commande apt install
```
cat "apt install" /var/log/apt/history.log | cut -d ' ' -f4
```
![image](https://user-images.githubusercontent.com/77662970/194703926-94bc9730-15b2-458c-b692-c9aaa142f438.png)

## 5. Utilisez les commandes dpkg et apt pour compter de deux manières différentes le nombre de total de
paquets installés sur la machine (ne pas hésiter à consulter le manuel !). Comment explique-t-on la
(petite) différence de comptage ? Pourquoi ne peut-on pas utiliser directement le fichier dpkg.log ?

```
dpkg -l | wc -l
``` 
```
apt list --installed | wc -l
```
Cette différence de comptage est du a des ligne d'erreur et ou de commentaire qui sont pris en compte.
On ne peut pas utiliser le fichier dpkg.log car comme son nom l'indique il est present pour garder un historique des différent paquet utiliser.

![image](https://user-images.githubusercontent.com/77662970/194320614-4f22978b-8304-4562-9dbd-960f3e2e15c0.png)


## 6. Combien de paquets sont disponibles en téléchargement sur les dépôts Ubuntu ?
```
apt list | wc -l
```
on peut observer 69054 paquet disponible.

![image](https://user-images.githubusercontent.com/77662970/194320763-66054f1e-bf8e-4f78-abb1-d0813e4bfee7.png)

## 7. A quoi servent les paquets glances, tldr et hollywood ? Installez-les et testez-les
L'outil glances est comparables au gestionnaire des taches de windows.Pour lancer cette outil il faut juste entrer ```glences```. Tldr permet de rendre plus accéssibles les information du manuelle, il va simplifier le manuelle est nous afficher que les point les plus importants pour l'utilisateur, c'est-a-dire, la commande et ses options.
L'outil hollywood est un outil 'fun' c'est a dire il va simuler une attaque informatique est va alors afficher plusieurs information, du binaire et autre qui feront croire que vous realiser une attaque informatique.
## 8. Quels paquets proposent de jouer au sudoku ?
Le paquet qui permet d'installer sudoku est ```apt install gnome-sudoku```.

# Exercice 2
A partir de quel paquet est installée la commande ls ? Comment obtenir cette information en une
seule commande, pour n’importe quel programme ? Utilisez la réponse à cette question pour écrire un
script appelé origine-commande (sans l’extension .sh) prenant en argument le nom d’une commande, et
indiquant quel paquet l’a installée.
```dpkg -S /bin/ls``` 
est la commande qui permet de voir quel est le paquet qui a installée la commande ls. Le paquet est ```coreutils: /bin/ls```
En une seule commande cela reviendrai a faire 
```
which -a ls | xargs dpkg -S 2>/dev/null | cut -f1 -d:
```
le script est le suivant:

```
#!/bin/bash
which -a $1 | xargs dpkg -S 2>/dev/null | cut -f1 -d:
```


# Exercice 3
Ecrire une commande qui affiche “INSTALLÉ” ou “NON INSTALLÉ” selon le nom et le statut du package
spécifié dans cette commande.
```
dpkh -l coreutils 2>/dev/null | grep"^ii" > /dev/null && echo "install" || echo "pas installée"
```
# Exercice 4
Lister les programmes livrés avec coreutils. En particulier, on remarque que l’un deux se nomme [. De
quoi s’agit-il ?

```
dpkg -L coreutils
```

# Exercice 5
Installez les paquets emacs et lynx à l’aide de la version graphique d’aptitude (et prenez deux minutes
pour vous renseigner et tester ces paquets).

Emacs est un éditeur de texte et lynx est un navigater web en mode text

# Exercice 6

Certains logiciels ne figurent pas dans les dépôts officiels. C’est le cas par exemple de la version ”officielle”
de Java depuis qu’elle est développée par Oracle. Dans ces cas, on peut parfois se tourner vers un ”dépôt
personnel” ou PPA.
1. Installer la version Oracle de Java (avec l’ajout des PPA)
sudo add-apt-repository ppa:linuxuprising/java
sudo apt update
sudo apt install oracle-java15-installer
2. Vérifiez qu’un nouveau fichier a été créé dans /etc/apt/sources.list.d. Que contient-il ?

![image](https://user-images.githubusercontent.com/77662970/194323636-90dd102a-9c85-4f78-9c60-8c3bce927c89.png)

# Exercice 7
Lorsqu’un logiciel n’est disponible ni dans les dépôts officiels, ni dans un PPA, ou encore parce qu’on
souhaite n’installer qu’une partie de ses fonctionnalités, on peut se tourner vers la compilation du code source.
C’est ce que nous allons faire ici, avec le programme cbonsai (https://gitlab.com/jallbrit/cbonsai)
```
git clone https://gitlab.com/jallbrit/cbonsai
```
```
sudo apt install libncursesw5-dev
```
```
sudo apt install make
```
Le résultat :

![image](https://user-images.githubusercontent.com/77662970/194325903-8d405d55-8519-4596-939b-f462e527533c.png)

# Exercice 8
Dans cet exercice, vous allez créer vos propres paquets et dépôts, ce qui vous permettra de gérer les
programmes que vous écrivez comme s’ils provenaient de dépôts officiels

![image](https://user-images.githubusercontent.com/77662970/194327065-a5ab09d7-9aa1-439d-b3e6-d2051f6758e0.png)

![image](https://user-images.githubusercontent.com/77662970/194326982-197e431b-2fb0-4e32-8255-a885108a8c1f.png)

2.

![image](https://user-images.githubusercontent.com/77662970/194327851-2b6129db-72d7-4dd1-b8f8-74abfc4705aa.png)

3.

![image](https://user-images.githubusercontent.com/77662970/194334321-bb2722ad-ceb1-440c-a353-a9ab3dc27f9e.png)



