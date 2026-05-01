+++
title = "Git"
weight = 16
+++

# Notes de cours — Git & GitHub

> **Prérequis :** Avoir Git installé sur votre ordinateur et un compte GitHub créé

---

## Table des matières

1. [Qu'est-ce que Git ?](#1-quest-ce-que-git-)
2. [Qu'est-ce que GitHub ?](#2-quest-ce-que-github-)
3. [Concepts fondamentaux](#3-concepts-fondamentaux)
4. [Les commandes essentielles de Git](#4-les-commandes-essentielles-de-git)
5. [Travailler avec GitHub](#5-travailler-avec-github)
6. [Le cycle de travail typique](#6-le-cycle-de-travail-typique)
7. [Les branches](#7-les-branches)
8. [Utiliser Git avec IntelliJ IDEA (projets Java)](#8-utiliser-git-avec-intellij-idea-projets-java)
9. [Erreurs fréquentes et solutions](#9-erreurs-fréquentes-et-solutions)
10. [Résumé des commandes](#10-résumé-des-commandes)

---

## 1. Qu'est-ce que Git ?

**Git** est un système de **contrôle de version**. Il permet de :

- Enregistrer l'historique de toutes les modifications apportées à votre code
- Revenir à une version précédente si vous faites une erreur
- Travailler en équipe sans écraser le travail des autres
- Comprendre qui a modifié quoi et pourquoi

> 💡 **Analogie :** Imaginez Git comme un système de sauvegarde intelligent pour votre code, qui garde une photo de votre projet à chaque fois que vous le lui demandez.

---

## 2. Qu'est-ce que GitHub ?

**GitHub** est une plateforme en ligne qui héberge vos projets Git dans le **cloud**. Il permet de :

- Sauvegarder votre code en ligne (sur un serveur distant)
- Partager votre code avec d'autres développeurs
- Collaborer en équipe sur le même projet
- Présenter vos projets comme un portfolio

> 💡 **Analogie :** Si Git est le système de sauvegarde local sur votre ordinateur, GitHub est le disque dur externe en ligne où tout le monde peut accéder à vos sauvegardes.

---

## 3. Concepts fondamentaux

| Terme | Définition |
|---|---|
| **Repository (dépôt)** | Le dossier de votre projet suivi par Git |
| **Commit** | Une "photo" de votre code à un moment précis |
| **Branch (branche)** | Une version parallèle de votre projet |
| **Clone** | Copier un dépôt distant sur votre ordinateur |
| **Push** | Envoyer vos commits vers GitHub |
| **Pull** | Récupérer les dernières modifications depuis GitHub |
| **Merge** | Fusionner deux branches ensemble |
| **Staging area** | Zone de préparation avant un commit |

### Schéma du flux de travail

```
Votre ordinateur                          GitHub (en ligne)
─────────────────────────────             ───────────────────
 Fichiers modifiés
       │
       │  git add
       ▼
 Zone de staging (index)
       │
       │  git commit
       ▼
 Dépôt local (historique)   ──git push──►  Dépôt distant
                            ◄──git pull──
```

---

## 4. Les commandes essentielles de Git

### 4.1 Initialiser un dépôt local

```bash
git init
```
Crée un nouveau dépôt Git dans le dossier courant.

---

### 4.2 Vérifier l'état du dépôt

```bash
git status
```
Affiche les fichiers modifiés, les fichiers prêts à être commités, etc.

---

### 4.3 Ajouter des fichiers à la zone de staging

```bash
# Ajouter un fichier spécifique
git add nom_du_fichier.java

# Ajouter tous les fichiers (nouveaux, modifiés ET supprimés)
git add --all
```

> 💡 **Pourquoi `--all` ?** Contrairement à `git add .` qui ne couvre que le dossier courant, `git add --all` prend en compte **l'intégralité du dépôt** : les nouveaux fichiers, les fichiers modifiés, et aussi les fichiers que vous avez **supprimés**.

---

### 4.4 Créer un commit

```bash
git commit -m "Description claire de ce que vous avez fait"
```

> 💡 **Bonne pratique :** Écrivez des messages de commit clairs et au présent.  
> ✅ `"Ajoute la validation du formulaire de connexion"`  
> ❌ `"modifs"` ou `"blabla"`

---

### 4.5 Voir l'historique des commits

```bash
git log
```

Pour un affichage plus compact :

```bash
git log --oneline
```

---

### 4.6 Annuler des modifications non commitées

```bash
# Annuler les modifications d'un fichier (avant git add)
git restore nom_du_fichier.java

# Retirer un fichier de la zone de staging (après git add)
git restore --staged nom_du_fichier.java
```

---

## 5. Travailler avec GitHub

### 5.1 Lier votre dépôt local à GitHub

1. Créez un nouveau dépôt sur GitHub (bouton **"New repository"**)
2. Copiez l'URL du dépôt (ex. : `https://github.com/votre-nom/mon-projet.git`)
3. Dans votre terminal :

```bash
# Lier le dépôt distant
git remote add origin https://github.com/votre-nom/mon-projet.git

# Vérifier la connexion
git remote -v
```

---

### 5.2 Envoyer votre code vers GitHub (Push)

```bash
# Premier push (définit la branche principale)
git push -u origin main

# Pushs suivants
git push
```

---

### 5.3 Récupérer le code depuis GitHub (Pull)

```bash
git pull
```

---

### 5.4 Cloner un dépôt existant

```bash
git clone https://github.com/votre-nom/mon-projet.git
```
Télécharge le projet complet avec tout son historique.

---

## 6. Le cycle de travail typique

Voici les étapes que vous répéterez constamment :

```
1. git pull             ← Récupérer les dernières modifications
2. (modifier votre code)
3. git status           ← Vérifier ce qui a changé
4. git add --all        ← Préparer les modifications
5. git commit -m ""     ← Sauvegarder avec un message
6. git push             ← Envoyer sur GitHub
```

---

## 7. Les branches

Les branches permettent de travailler sur une fonctionnalité sans toucher au code principal.

### 7.1 Créer et changer de branche

```bash
# Créer une nouvelle branche et s'y déplacer
git checkout -b ma-nouvelle-fonctionnalite

# Lister toutes les branches
git branch

# Changer de branche
git checkout main
```

### 7.2 Fusionner une branche dans main

```bash
# Se placer sur main
git checkout main

# Fusionner votre branche
git merge ma-nouvelle-fonctionnalite
```

### 7.3 Supprimer une branche (après fusion)

```bash
git branch -d ma-nouvelle-fonctionnalite
```

---

## 8. Utiliser Git avec IntelliJ IDEA (projets Java)

IntelliJ IDEA intègre Git et GitHub directement dans l'interface, ce qui facilite grandement le travail.

### 8.1 Prérequis dans IntelliJ

Avant tout, vérifiez qu'IntelliJ détecte bien Git :

`File` → `Settings` (ou `Preferences` sur Mac) → `Version Control` → `Git`

Le chemin vers l'exécutable Git devrait être détecté automatiquement. Cliquez sur **"Test"** pour confirmer.

---

### 8.2 Cas 1 — Vous avez déjà un projet Java existant (sans Git)

> Vous avez créé votre projet, vous avez du code, et vous voulez maintenant le mettre sur GitHub.

**Étape 1 : Initialiser Git dans le projet**

`VCS` (menu du haut) → `Create Git Repository...`  
→ Sélectionnez le dossier racine de votre projet → `OK`

IntelliJ initialise Git et la barre de statut en bas devient active (vous verrez le nom de la branche `main` ou `master`).

**Étape 2 : Faire le premier commit**

- Les fichiers apparaissent en rouge dans l'arborescence (non suivis)
- Allez dans `Git` → `Commit...` (ou `Ctrl+K` / `Cmd+K`)
- Cochez les fichiers à inclure (ou sélectionnez tout)
- Écrivez un message de commit (ex. : `"Initial commit"`)
- Cliquez sur **"Commit"**

**Étape 3 : Créer le dépôt sur GitHub et le lier**

`Git` → `GitHub` → `Share Project on GitHub`

- Connectez-vous à votre compte GitHub si ce n'est pas déjà fait
- Donnez un nom au dépôt
- Choisissez **Public** ou **Private**
- Cliquez sur **"Share"**

IntelliJ crée automatiquement le dépôt sur GitHub et y envoie votre code. ✅

---

### 8.3 Cas 2 — Vous créez un nouveau projet Java dans IntelliJ

> Vous partez de zéro et vous voulez que votre projet soit sur GitHub dès le début.

**Option A : Créer le projet et GitHub en même temps**

1. `File` → `New Project`
2. Configurez votre projet Java normalement
3. Dans la fenêtre de création, cochez ✅ **"Create Git repository"**
4. Cliquez sur **"Create"**

Votre projet est créé avec Git déjà initialisé localement.

5. Ensuite, pour le mettre sur GitHub : `Git` → `GitHub` → `Share Project on GitHub`

---

**Option B : Cloner un dépôt GitHub existant (projet déjà sur GitHub)**

Si le dépôt existe déjà sur GitHub (ex. : un dépôt créé par votre professeur) :

1. `File` → `New` → `Project from Version Control...`
2. Sélectionnez **"GitHub"** (ou collez directement l'URL)
3. Connectez-vous à GitHub
4. Choisissez le dépôt dans la liste
5. Choisissez où enregistrer le projet sur votre ordinateur
6. Cliquez sur **"Clone"**

IntelliJ télécharge le projet et l'ouvre automatiquement. ✅

---

### 8.4 Opérations Git courantes dans IntelliJ

Une fois connecté à GitHub, vous pouvez faire toutes les opérations Git depuis l'interface :

| Action | Raccourci / Menu |
|---|---|
| **Commit** | `Ctrl+K` / `Cmd+K` |
| **Push** | `Ctrl+Shift+K` / `Cmd+Shift+K` |
| **Pull** | `Ctrl+T` / `Cmd+T` |
| **Historique** | `Git` → `Show Git Log` |
| **Nouvelle branche** | Cliquez sur le nom de branche en bas à droite |
| **Voir les différences** | Clic droit sur un fichier → `Git` → `Compare with HEAD` |

> 💡 **Conseil :** Le panneau **"Git"** en bas de l'écran affiche l'historique complet des commits, les branches et les modifications. Prenez le temps de l'explorer !

---

### 8.5 Se connecter à GitHub depuis IntelliJ

Si IntelliJ vous demande de vous authentifier :

`File` → `Settings` → `Version Control` → `GitHub` → **"+"** pour ajouter un compte

Deux options :
- **"Log In via GitHub"** → ouvre un navigateur pour s'authentifier (recommandé)
- **"Log In with Token"** → nécessite de créer un token d'accès personnel sur GitHub

> ⚠️ **Note :** GitHub n'accepte plus les mots de passe simples. Si vous utilisez le terminal, vous devrez utiliser un **token d'accès personnel (PAT)** ou une **clé SSH**. IntelliJ gère cette authentification automatiquement via le navigateur.

---

## 9. Erreurs fréquentes et solutions

### ❌ "rejected — non-fast-forward" lors d'un push

Le dépôt distant a des modifications que vous n'avez pas en local.

```bash
git pull       # D'abord récupérer les modifications
git push       # Ensuite pousser les vôtres
```

---

### ❌ Conflit de fusion (Merge conflict)

Un conflit survient quand deux personnes modifient la même ligne. Git marque le fichier :

```
<<<<<<< HEAD
Votre version du code
=======
La version de l'autre personne
>>>>>>> origin/main
```

**Solution :**
1. Ouvrez le fichier et choisissez manuellement quelle version garder
2. Supprimez les marqueurs `<<<<<<<`, `=======`, `>>>>>>>`
3. Faites un `git add` puis un `git commit`

Dans IntelliJ, un outil graphique de résolution de conflits s'ouvre automatiquement. ✅

---

### ❌ "detached HEAD state"

Vous avez navigué vers un ancien commit. Pour revenir à la normale :

```bash
git checkout main
```

---

## 10. Résumé des commandes

```bash
# ── Initialisation ─────────────────────────────────────────
git init                                   # Créer un dépôt local
git clone <url>                            # Copier un dépôt distant

# ── Suivi des fichiers ─────────────────────────────────────
git status                                 # Voir l'état du dépôt
git add <fichier>                          # Ajouter un fichier spécifique
git add --all                              # Ajouter tous les fichiers (nouveaux, modifiés, supprimés)
git commit -m "message"                    # Créer un commit

# ── Historique ─────────────────────────────────────────────
git log                                    # Historique complet
git log --oneline                          # Historique compact

# ── Connexion à GitHub ─────────────────────────────────────
git remote add origin <url>                # Lier à GitHub
git remote -v                              # Vérifier la liaison

# ── Synchronisation ────────────────────────────────────────
git push -u origin main                    # Premier push
git push                                   # Pousser les commits
git pull                                   # Récupérer les modifications

# ── Branches ───────────────────────────────────────────────
git branch                                 # Lister les branches
git checkout -b <nom>                      # Créer et changer de branche
git checkout main                          # Revenir à main
git merge <nom>                            # Fusionner une branche
git branch -d <nom>                        # Supprimer une branche

# ── Annulation ─────────────────────────────────────────────
git restore <fichier>                      # Annuler les modifications
git restore --staged <fichier>             # Retirer du staging
```

---

> 📚 **Pour aller plus loin :**
> - Documentation officielle de Git : [git-scm.com/doc](https://git-scm.com/doc)
> - Guide GitHub : [docs.github.com](https://docs.github.com)
> - Git interactif en ligne : [learngitbranching.js.org](https://learngitbranching.js.org)