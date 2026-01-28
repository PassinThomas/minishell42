# Minishell - Projet 42

Bienvenue dans **Minishell**, un projet de l'école 42. L'objectif principal est de recréer un shell UNIX minimaliste en implémentant des fonctionnalités essentielles tout en respectant les normes POSIX.

## 📌 A propos du Projet

### Objectif
Ce projet est une exploration approfondie du fonctionnement interne d'un shell. Il met en avant des aspects pratiques comme la gestion des processus, le parsing des commandes et la communication entre processus au moyen de pipes.

### Concepts Mis en Pratique
- **Gestion des processus** : Utilisation de `fork()`, `execve()` et de `waitpid()`.
- **Parsing des commandes** :
    - Implémentation d'un analyseur lexical capable de décomposer les commandes en tokens.
    - Gestion des arguments, redirections (`<`, `>`, `>>`) et pipes (`|`).
    - Construction d'une **structure arborescente** pour représenter chaque commande à l'aide de **listes chaînées**.
- **Gestion des redirections** : Ouverture et modification des descripteurs de fichiers pour gérer les entrées et sorties.
- **Liste Chaînée** : Utilisation de listes chaînées pour conserver les informations des commandes analysées, comme les paramètres, les types de redirections, etc.
- **Signaux** : Implémentation de la gestion de `SIGINT` (Ctrl+C), `SIGQUIT` (Ctrl+\) et `EOF` (Ctrl+D).

---

## 🔧 Built-ins Implémentés

Voici les commandes intégrées (built-ins) développées pour le projet :
- **`echo`** : Affiche du texte avec une gestion de l'option `-n` pour éviter la nouvelle ligne.
- **`cd`** : Change le répertoire de travail.
- **`pwd`** : Affiche le répertoire courant.
- **`export`** : Ajoute ou modifie des variables d'environnement.
- **`unset`** : Supprime des variables d'environnement.
- **`env`** : Liste toutes les variables d'environnement actuelles.
- **`exit`** : Quitte le shell avec un code de statut spécifique.

Chaque commande est gérée avec ses erreurs potentielles, comme les répertoires inexistants, les permissions refusées, ou les arguments invalides.

---

## 🚀 Installation et Exécution

### Cloner le projet
Commencez par récupérer le projet avec cette commande :
```bash
git clone https://github.com/PassinThomas/minishell42.git
```

### Compilation
Un **Makefile** est disponible pour simplifier la compilation. Les différentes commandes disponibles sont :
- **`make`** : Compile le shell.
- **`make clean`** : Supprime les fichiers objets après compilation.
- **`make fclean`** : Supprime les fichiers objets et l'exécutable.
- **`make re`** : Exécute `fclean` puis recompile le programme.

Pour compiler le projet, utilisez simplement :
```bash
make
```

### Lancement
Une fois le shell compilé, exécutez-le avec :
```bash
./minishell
```

---

## ⚙️ Détails Techniques

### Parsing des Commandes
Le parsing a été conçu pour gérer des commandes complexes incluant :
- Les redirections (`<`, `>`, `>>`).
- Le piping (`|`).
- Les espaces et guillemets (`'`, `"`).
- Les expansions comme `$VARIABLE` et `~`.

Un analyseur lexical décompose l'entrée utilisateur en **tokens**, qui sont ensuite structurés en **nœuds de commandes**. Ces nœuds sont liés entre eux grâce à des **listes chaînées** représentant les relations entre les commandes.

### Gestion des Environnements
Les variables d'environnement sont chargées au démarrage du shell et gérées dynamiquement lors de l'exécution. Cela permet d'implémenter les fonctions `env`, `export`, et `unset` pour ajouter, afficher ou supprimer des variables.

### Redirections et Pipes
Le shell redirige les entrées/sorties via les descripteurs de fichier. Pour les pipelines (`|`), chaque commande est exécutée dans un processus enfant, et les flux sont redirigés pour permettre la communication entre les processus.

### Fonctionnalités Notables
- **Gestion des erreurs robustes** : Si une commande échoue, des messages clairs sont affichés.
- **Expansions** : Remplacement des variables (`$VAR`) et gestion des codes de retour (`$?`).
- **Signaux Unix** : Interruption (`Ctrl+C`), fin de fichier (`Ctrl+D`) et gestion de la sortie avec un statut précis (`exit`).

---

_Fait par PassinThomas pour l'école 42._
