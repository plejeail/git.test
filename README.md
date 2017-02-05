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

```bash
git config --global color.diff auto
git config --global color.status auto
git config --global color.branch auto
```

pseudo:

```bash
git config --global user.name "votre_pseudo"
```
e-mail:

```bash
git config --global user.email moi@email.com
```

On peut également modifier le fichier de configuration de git (sur Linux: ~/.gitconfig).

## Créer un nouveau dépôt ou cloner un dépôt existant
Il existe deux possibilités pour commencer à travailler sur git:
- Créer un nouveau dépôt vide
- Cloner un dépôt existant (pour travailler sur un projet existant)

### Créer un nouveau dépôt
Commencez par créer un dossier du nom de votre projet. Par exemple je crée le dossier /home/gevisk/Programs/git.test
pour héberger mon projet test "git.test" :

```bash
cd /home/gevisk/Programs/
mkdir git.test
```

Déplacez-vous dans le dossier :

```bash
cd git.test
```

Puis initialisez le dépôt dans ce dossier avec la commande suivante :
git init

Le projet Git vient d'être créé ! Un dossier caché .git est apparu. Je vous invite à aller regarder les fichiers
à l'intérieur.

### Cloner un dépôt existant
Cloner un dépôt existant consiste à récupérer l'historique et tous les fichiers d'un projet Git.

Clonons par exemple ce projet. Pour cela on utilise la commande suivante :

```bash
git clone $DEPOT
```
où $DEPOT est l'addresse du projet à cloner (terminée par .git)

## Méthode de travail
Lorsqu'on travaille avec Git, on suit en général toujours les étapes suivantes :
0. Créer une nouvelle branche pour éviter de casser le code de la branche principale
1. modifier le code source
2. tester le programme
3. faire un commit pour soumettre les changements à Git quand on est satisfait
4. recommencer à l'étape 1 pour une autre modification
5. fusionner la nouvelle branche avec lla branche principale quand on a terminé les modifications et que l'on s'est assuré que le code marche

### Modifier le code et le soumettre à Git
A ce stade, nous avons créé ou cloné un dépôt Git.

La commande 'git status' indique les fichiers récemment modifiés :

```
On branch master
nothing to commit, working tree clean
```

Ce message nous informe que rien n'a été modifié. Vous pouvez créer un fichier ou en modifier un si vous avez cloné un projet. Après avoir sauvegardé vos modifications relancé la commande et voyez les résultats.

Vous pouvez voir les changements lignes par ligne :

```bash
git diff
```

Les lignes ajoutées sont précédées d'un "+" tandis que les lignes enlevées sont précédées d'un "-". Si vous avez 
configuré git pour utiliser des couleurs, les lignes modifiées sont colorées et donc facilement repérables.

Vous devez ajouter les fichiers à la liste des fichiers commitables :

```bash
git add file1 file2 ...
```

puis faire le commit :

```bash
git commit
```

Utiliser la commande add est essentiel pour intégrer de nouveaux fichiers dans le projet.
Si vous voulez commiter tous les fichiers listés par ```git status``` vous pouvez utiliser :

```bash
git commit -a
```

Vous pouvez également choisir à la main les fichiers à commiter :
```bash
git commit file1 file2 ...
```

Lorsque la commande commmit est lancée, l'éditeur par défaut s'ouvre. Vous devez alors taper un message qui décrit
les changements effectués.

Une fois cela fait, git va officiellement sauvegarder les changements et les ajoutera à la liste des changements du
projet. Le commit est local : Il n'affectera le projet que sur votre ordinateur !

### Annuler un commit

Si une erreur s'est introduite nous pouvons annuler le commit qui l'a causée. Pour cela nous allons d'abord apprendre
à vérifier les logs.

#### Vérifier les logs
Nous pouvons consulté l'historique des logs avec la commande suivante :

```bash
git log
git log -p # pour avoir les modifications explicitées
git log --stat # avoir un résumé plus court
```

Mon résultat :
```
commit babbf273a970f0b6fbd44836596ffe45fb99cbe2
Author: plejeail <pierre.lejeail@hotmail.fr>
Date:   Sun Feb 5 17:07:03 2017 +0100

    Un autre commit est arrivé

commit 8b747fc7a5bfeae1bbb81e9512521b790023953f
Author: plejeail <pierre.lejeail@hotmail.fr>
Date:   Sun Feb 5 16:35:18 2017 +0100

    Vous avez effectué un commit
```

Chaque commit est décrit par un identifiant en héxadécimal, l'auteur du commit, la date, et le message décrivant les
modifications.

#### Correction d'une erreur
Pour changer le message du dernier comit :

```
git commit --amend
```

Annuler les modifications d'un commit :

```
git reset $COMMIT
```

où ```$COMMIT``` peut prendre les valeurs :
- ```HEAD ```: dernier commit
- ```HEAD^ ```: avant-dernier
- ```HEAD^^ ```: avant-avant-dernier
- ```HEAD~2 ```: avant-avant-dernier (notation équivalente)
- ```babbf273a970f0b6fbd44836596ffe45fb99cbe2 ```: l'identifiant d'un commit
- ```babbf273 ```: vous n'êtes pas obliger d'écrire l'identifiant en entier, tant que git ne risque pas de le confondre


Seul le commit est retiré, les fichiers eux sont toujours modifiés. Pour restaurer les fichiers, il faut rajouter
l'option '--hard' à l'instruction ```git reset```.

#### Restaurer les modifications au dernier commit
Si vous avez modifié un fichier mais que vous ne l'avez pas encore commiter, vous pouvez le restaurer tel qu'il
était au dernier commit en utilisant la commande :
```bash
git checkout file
```

## Echanger avec le serveur
Pour le moment, nous avons tout effectué en local. Il est temps de voir comment interagir avec d'autre personnes.

Pour télécharger les nouveauté depuis le serveur, On utilise la commande pull :
```bash
git pull
```

Si vous avez effectué des changements, ils seront automatiquement fusionnés avec la nouvelle version. Si la même
zone de code a été modifiée par vous et une autre personne, Git vous prévient. Vous devez alors modifié manuellement
les fichiers concernés (les lignes modifiées sont délimitées par « <<<<<<<<< »).
