# Guide d'utilisation de Git
---

## Auteur : Zupanico
---

Voici un guide d'utilisation simple de Git, un logiciel de gestion de version Open-Source créée par Linus Torvalds, le créateur du noyau Linux. Il est le logiciel de version le plus populaire et il est l'engrenage qui fait tourner Git Hub, hébergeur de code appartenant à Microsoft.

### Installation
---
Pour utiliser Git sur un poste de travail, il faut en premier l'installer. Voici les liens pour les différents systèmes d'exploitation.
- [Pour Linux](https://git-scm.com/download/linux)
- [Pour Windows](https://git-scm.com/download/windows)
- [Pour Mac OS](https://git-scm.com/download/mac)

### Création d'un dépôt
---
La première étape à l'utilisation de Git est la création d'un dépôt pour stocker le code que l'on veut versionner.

Dans un nouveau répertoire créé pour le projet, entrer la commande suivante pour créer le nouveau dépôt:
```bash
git init
```

Il est aussi possible de cloner un répertoire existant pour créer une copie fonctionnelle avec la commande:
```bash
git clone /chemin/vers/repertoire
```

Ou si le répertoire est à distance:
```bash
git clone utilisateur@hote:/chemin/vers/repertoire
```

Il est possible aussi de cloner avec GitHub:
```bash
git clone git@github.com:exemple/exemple.git
```

### Gestion des fichiers et commit
---
Après avoir effectué des changements sur le code, il est possible de les commettre dans le dépôt.

Pour proposer des changements qui vont être ajoutés à l'indexage du dépôt, il faut spécifier les fichiers à rajouter:
```bash
git add <nom_fichier>
```

Si il faut rajouter tout les fichiers utiliser cette commande:
```bash
git add *
```

Ensuite,  il faut commettre les changements avec un message de validation qui va être enregistré dans la tête de notre répertoire, mais pas de notre dépôt Git. Utiliser cette commande:
```bash
git commit -m "Message de validation"
```
Ces changements vont être commis dans la branche où Git se situe actuellement.
*(Vu plus en détail dans la section des branches et des tags.)*

Après avoir fait des changements dans la tête du répertoire, il faut pousser les changements faits dans le dépôt dans la branche voulue:
```bash
git push origin <branche>
```

Si le dépôt de travail n'a pas été copié et que notre dépôt est à distance, il faut l'ajouter dans notre liste de répertoires à distance:
```bash
git remote add origin <serveur>
```

### Consultation et manipulation de l'historique
---
Lors de la rédaction de code informatique, il est très utile, voire nécessaire, de pouvoir consulter l'historique de ce qui a été effectué sur le dépôt.

Voici quelques exemples de paramètres à utiliser pour visualiser l'historique, pour plus de détails sur l'utilisation de `git log`  utiliser la commande suivante:
```bash
git log --help
```

Avec Git, il est possible de voir toute l'historique sans filtre avec la commande suivante:
```bash
git log
```

Pour voir les commits d'un auteur précis:
 ```bash
git log --author=nicolas
```

Pour voir un historique compressé dans une seule ligne:
```bash
git log --pretty=oneline
```

Pour voir un arborescence en ASCII de toutes les branches, avec tout les tags:
```bash
git log --graph --oneline --decorate --all
```

Pour voir seulement les fichiers qui ont étés changés:
```bash
git log --name-status
```

Si un changement fait localement non voulu apparaît, il est possible de remplacer le fichier local par celui répertorié par le dépôt avec la commande suivante:
```bash
git checkout -- <fichier>
```

Si par contre tout les changements locaux non-commis doivent être annulés et remplacés par la dernière version sur le dépôt de la branche *main*, utiliser les commandes suivante:
```bash
git fetch origin
git reset ==hard origin/master
```

### Les branches et les tags
---
En développement, il est important de garder son produit fonctionnel et intact. Par contre, vu que le concept du développement est de s'améliorer et d'ajouter des fonctionnalités, il y a donc un conflit.
C'est à ce moment que les branches démontrent leur utilité. Une nouvelle branche est une copie conforme de la branche principale, mais avec des modifications appliquées.
Lors de la création d'une branche, la bonne pratique est de nommer la branche selon la description courte et brève de celle-ci.
Pour une nouvelle fonctionnalité X, il est adéquat de nommer la branche `fonctionnalite_x`. 
Utiliser ce [guide]([Git Branch Naming Convention: 7 Best Practices to Follow | HackerNoon](https://hackernoon.com/git-branch-naming-convention-7-best-practices-to-follow-1c2l33g2)) de bonne pratique peut s'avérer utile pour la nomenclature des branches.
```
		  fonctionnalite_x
		  ________________
		 /                \
________/__________________\_______________>
			   master
		^					^
		|					|	 
		branche				fusionnement		
```

Pour créer une nouvelle branche avec la fonctionnalité X et changer de branche active dans la ligne de commande, utiliser la commande suivante:
```bash
git checkout -b fonctionnalite_x
```

Pour retourner dans la branche *master*, utiliser la commande suivante:
```bash
git checkout master
```

Pour supprimer une branche, utliser la commande suivante:
```bash
git branch -d fonctionnalite_x
```

La branche créée ne sera pas disponible aux autres personnes accédant au dépôt GitHub, par exemple, donc il faut la pousser avec la commande suivante:
```bash
git push origin fonctionnalite_x
```

### Partager un dépôt
---
Lors des projets de développement, il n'est pas anormal de collaborer avec d'autres développeurs, il est donc important de trouver des façons de partagers les dépôts pour le travail collaboratif.
Voici un tableau regroupant quelques façons de partager le dépôt Git:
|         Dépôt         |                                                                Pours                                                               |                                  Contres                                 |                                               Contrôle des accès                                               |                    Créer des dépôts                    |
|:---------------------:|:----------------------------------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------------:|:--------------------------------------------------------------------------------------------------------------:|:------------------------------------------------------:|
| Partage de fichiers   | Pas d'accès à Internet requis                                                                                                      | Pas incroyable avec internet                                             | Utilise les permissions des fichiers                                                                           | A besoin de préparation par dépôt de travail           |
| Démon git             | Protocole Git rapide                                                                                                               | Pas incroyable avec internet                                             | Contrôle des permissions exécrable. Mode lecture par défaut, écriture possible, mais seulement en mode anonyme | Par projet et a besoin d'être chapeauté                |
| Plain SSH server      | Toujours bonne sécurité                                                                                                            | Not internet friendly port, requires account creation per user on server | Utilise les permissions des fichiers                                                                           | Par projet initié                                      |
| Serveur SSH git-shell | Amélioration des simples serveurs SSH                                                                                              | Not internet friendly port, requires account creation per user on server | Utilise les permissions des fichiers                                                                           | Par projet initié                                      |
| Gitosis               | Ajoute une bonne gestion des utilisateurs et des dépôts à distance, demande une seul compte système                                | Pas incroyable avec internet                                             | Utilise le fichier gitosis-config                                                                              | Aucune initialisation serveur, seulement configuration |
| Apache http           | Comme la configuration normale d'Apache, demande un seul compte système, amical avec Internet                                      | Légèrement volatile                                                      | Utilise htpasswd                                                                                               | Par projet initié                                      |
| Apache http + gitweb  | Comme la configuration normale d'Apache, demande un seul compte système, amical avec Internet et ajoute une belle vue sur le dépôt | Légèrement volatile, accès en lecture seule                              | Utilise htpasswd                                                                                               | Par projet initié                                      |
| github                | Accessible avec Internet, facile à utiliser avec l'interface web                                                                   | Hébergé à l'externe                                                      | Gestion des sshkeys                                                                                            | Interface Web                                          |

### Git-Flow et GitHub flow
---
Git-Flow est une stratégie de gestion de branches dont l'idée principale est de séparer chaque étape de développement en branches différentes.
Il existe cinq types branches dans la stratégie de travail Git-Flow:
#### 1. Principale
Le maître, le *master*, la branche principale. C'est la branche qui contient le produit fonctionnel selon la philosophie de produit minium viable. Toutes les branches déviant de la principale vont être fusionnées après avoir été testées et revues plusieurs fois.
   
#### 2. Développement
Branche utilisée pendant la préproduction, le développement et test des nouvelles fonctionnalités. Selon la bonne pratique, les nouvelles fonctionnalités devraient être créées à partir de la branche de développement puis fusionnées avec *dev* une fois prêtes pour les tests.

#### 3. Fonctionnalité
Branche utilisée pour implémenter des nouvelles fonctionnalités, d'où le nom si intuitif, puis fusionnée avec la branche *dev* après avoir été testée.

#### 4. Nouvelle version
Branche utilisée pour corriger des bugs mineurs et finalisation des détails avant d'être fusionnée à la branche principale.

#### 5. Correctifs
Branche utilisée pour effectuer des changements ou des réparations rapides et simples. Cette branche doit être affectée aux branches *dev* et *main* pour que les deux branches bénéficient des changements utiles.

### Sources, liens et documentation
---
- [git - the simple guide - no deep shit! (rogerdudler.github.io)](https://rogerdudler.github.io/git-guide/)
- [Git Community Book](http://book.git-scm.com/)
- [Pro Git](http://progit.org/book/)
- [Think like a git](http://think-like-a-git.net/)
- [GitHub Help](http://help.github.com/)
- [A Visual Git Guide](http://marklodato.github.com/visual-git-guide/index-en.html)
- [How do you create a Git branch? | Solutions to Git Problems (gitkraken.com)](https://www.gitkraken.com/learn/git/problems/create-git-branch#:~:text=To%20create%20a%20new%20Git,work%20on%20the%20right%20file.)
- [Git Branch Naming Convention: 7 Best Practices to Follow | HackerNoon](https://hackernoon.com/git-branch-naming-convention-7-best-practices-to-follow-1c2l33g2)
- [Git (git-scm.com)](https://git-scm.com/)
- [Git — Wikipédia (wikipedia.org)](https://fr.wikipedia.org/wiki/Git)
- [8 ways to share your git repository (jedi.be)](https://www.jedi.be/blog/2009/05/06/8-ways-to-share-your-git-repository/)
- [What is Git Flow | How to use Git Flow | Learn Git (gitkraken.com)](https://www.gitkraken.com/learn/git/git-flow#:~:text=Git%20flow%20is%20a%20popular,different%20types%20of%20Git%20branches.)
- 
