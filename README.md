# Git Tutoriel

Git est un logiciel de gestion de versions. Il est capable de :
- suivre l'évolution d'un fichier ligne par ligne
- archiver les anciennes versions
- retenir qui a effectué chaque modification et pourquoi
- fusionner les modifications pour éviter que le travail d'une personne soit écrasé
- travailler par branches (versions parallèles d'un même projet)

Git est très rapide. Il est complexe et demande un certain temps d'adaptation, mais c'est aussi le
cas pour les autres outils du même genre.

Git est à l'origine conçu pour linux. Il a été créé par Linus Torvald, qui est entre autre l'homme
à l'origine de Linux. Il se distingue par sa rapidité et sa gestion des branches qui permettent de
développer en parallèle de nouvelles fonctionnalités. Il est également utilisable sur windows et mac.

## configuration de git :
activer les couleurs:
git config --global color.diff auto
git config --global color.status auto
git config --global color.branch auto

pseudo:
git config --global user.name "votre_pseudo"

e-mail:
git config --global user.email moi@email.com

On peut également modifier le fichier de configuration de git (sur Linux: ~/.gitconfig).

## Créer un nouveau dépôt ou cloner un dépôt existant
Il existe deux possibilités pour commencer à travailler sur git:
- Créer un nouveau dépôt vide
- Cloner un dépôt existant (pour travailler sur un projet existant)

### Créer un nouveau dépôt
Commencez par créer un dossier du nom de votre projet. Par exemple je crée le dossier /home/gevisk/Programs/git.test
pour héberger mon projet test "git.test" :
cd /home/gevisk/Programs/
mkdir git.test

Déplacez-vous dans le dossier :
cd git.test

Puis initialisez le dépôt dans ce dossier avec la commande suivante :
git init

Le projet Git vient d'être créé ! Un dossier caché .git est apparu. Je vous invite à aller regarder les fichiers
à l'intérieur.

### Cloner un dépôt existant
Cloner un dépôt existant consiste à récupérer l'historique et tous les fichiers d'un projet Git.

Clonons par exemple ce projet. Pour cela on utilise la commande suivante :
git clone $DEPOT
où $DEPOT est l'addresse du projet à cloner (terminée par .git)

## Modifié le code et effectuer des commits
A ce stade, nous avons créé ou cloné un dépôt Git.

La commande 'git status' indique les fichiers récemment modifiés :


