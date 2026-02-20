+++
title = "Exercices de révision"
weight = 7
url = "/exo_revisions/"

+++

---

## 🎮 Projet 1 : Système de Gestion de Notes Scolaires

### 📋 Contexte
Vous devez créer un système pour gérer et analyser les notes d'une classe d'étudiants. Le système permettra de calculer des statistiques, d'attribuer des mentions et de générer des rapports.

### 🎯 Objectifs pédagogiques
- Manipulation de tableaux
- Calculs statistiques (moyenne, min, max)
- Structures conditionnelles pour la classification
- Boucles pour parcourir des données
- Méthodes avec paramètres et valeurs de retour

### 📝 Instructions 

Créez une classe `GestionNotes` avec les méthodes suivantes :

#### 1. Méthode `calculerMoyenne`
**But :** Calculer la moyenne arithmétique d'un tableau de notes.

**Paramètres :**
- `notes` : un tableau de `double` contenant les notes

**Retour :** La moyenne sous forme de `double`

**Algorithme :**
- Parcourir toutes les notes du tableau
- Additionner toutes les notes
- Diviser la somme par le nombre de notes
- Retourner le résultat

**Exemple :** Pour les notes [15.5, 12.0, 18.0], la moyenne est (15.5 + 12.0 + 18.0) / 3 = 15.17

---

#### 2. Méthode `trouverMaximum`
**But :** Trouver la note la plus élevée dans le tableau.

**Paramètres :**
- `notes` : un tableau de `double`

**Retour :** La note maximale (`double`)

**Algorithme :**
- Initialiser une variable avec la première note
- Parcourir toutes les autres notes
- Si une note est supérieure au maximum actuel, la remplacer
- Retourner le maximum trouvé

---

#### 3. Méthode `trouverMinimum`
**But :** Trouver la note la plus basse dans le tableau.

**Paramètres :**
- `notes` : un tableau de `double`

**Retour :** La note minimale (`double`)

**Algorithme :** Similaire à `trouverMaximum`, mais en cherchant la plus petite valeur.

---

#### 4. Méthode `compterReussites`
**But :** Compter combien d'étudiants ont une note supérieure ou égale à 10 (seuil de réussite).

**Paramètres :**
- `notes` : un tableau de `double`

**Retour :** Le nombre d'étudiants ayant réussi (`int`)

**Algorithme :**
- Initialiser un compteur à 0
- Parcourir toutes les notes
- Pour chaque note >= 10, incrémenter le compteur
- Retourner le compteur

---

#### 5. Méthode `obtenirMention`
**But :** Déterminer la mention obtenue selon la moyenne d'un étudiant.

**Paramètres :**
- `moyenne` : la moyenne de l'étudiant (`double`)

**Retour :** Une chaîne de caractères (`String`) représentant la mention

**Règles de mentions :**
- moyenne >= 16 : "Très Bien"
- moyenne >= 14 : "Bien"
- moyenne >= 12 : "Assez Bien"
- moyenne >= 10 : "Passable"
- moyenne < 10 : "Échec"

**Algorithme :**
- Utiliser une série de conditions if/else if/else
- Comparer la moyenne aux seuils (du plus élevé au plus bas)
- Retourner la mention correspondante

---

#### 6. Méthode `afficherRapport`
**But :** Générer et afficher un rapport complet des statistiques de la classe.

**Paramètres :**
- `notes` : un tableau de `double`

**Retour :** `void` (la méthode affiche directement à l'écran)

**Informations à afficher :**
1. Nombre total d'étudiants (taille du tableau)
2. Moyenne générale de la classe (utiliser `calculerMoyenne`)
3. Note maximale et minimale (utiliser les méthodes correspondantes)
4. Taux de réussite en pourcentage : (nombre de réussites / total) × 100
5. Distribution des mentions :
   - Compter combien d'étudiants ont chaque mention
   - Pour cela, parcourir toutes les notes, calculer la mention de chaque note, et compter

**Format d'affichage attendu :**
```
===== RAPPORT DE NOTES =====
Nombre d'étudiants : 10
Moyenne générale : 12.60
Note maximale : 18.00
Note minimale : 7.50
Taux de réussite : 70.00%
Distribution des mentions :
  - Très Bien : 2
  - Bien : 2
  - Assez Bien : 2
  - Passable : 1
  - Échec : 3
```

---

#### 7. Méthode `main`
**But :** Tester toutes les fonctionnalités du système.

**Instructions :**
- Créer un tableau de notes de test : `{15.5, 8.0, 12.5, 18.0, 9.5, 14.0, 16.5, 11.0, 7.5, 13.5}`
- Appeler la méthode `afficherRapport` avec ce tableau
- Tester également les méthodes individuellement pour vérifier leur bon fonctionnement

---

### ✅ Critères de validation
- [ ] Toutes les méthodes sont créées avec les bons paramètres et types de retour
- [ ] La moyenne est calculée correctement
- [ ] Le maximum et minimum sont trouvés correctement
- [ ] Le comptage des réussites fonctionne
- [ ] Les mentions sont attribuées selon les bons seuils
- [ ] Le rapport affiche toutes les informations demandées
- [ ] Le code est lisible avec des noms de variables significatifs

### 💡 Conseils
- Testez chaque méthode individuellement avant de créer le rapport complet
- Utilisez `System.out.printf("%.2f", nombre)` pour formater les nombres avec 2 décimales
- Pour calculer un pourcentage : `(partieDouble / totalDouble) * 100.0`

---

## 💰 Projet 2 : Calculateur de Salaire et Impôts

### 📋 Contexte
Développez un système de calcul de salaire net avec différentes déductions, heures supplémentaires, bonus et impôts. Ce système doit générer une fiche de paie complète.

### 🎯 Objectifs pédagogiques
- Calculs arithmétiques complexes
- Conditions imbriquées pour les tranches d'imposition
- Formules mathématiques appliquées
- Organisation de code en méthodes réutilisables

### 📝 Instructions 

Créez une classe `CalculateurSalaire` avec les méthodes suivantes :

#### 1. Méthode `calculerSalaireBrut`
**But :** Calculer le salaire brut mensuel en prenant en compte les heures supplémentaires.

**Paramètres :**
- `tauxHoraire` : taux horaire en euros (`double`)
- `heuresTravaillees` : nombre d'heures travaillées dans le mois (`int`)

**Retour :** Le salaire brut (`double`)

**Règles :**
- Le nombre d'heures normales par mois est 151.67 heures
- Les heures au-delà sont des heures supplémentaires
- Les heures supplémentaires sont payées avec un bonus de 25%

**Algorithme :**
- Si heuresTravaillees <= 151.67 : salaire = tauxHoraire × heuresTravaillees
- Sinon :
  - Calculer le salaire des heures normales : 151.67 × tauxHoraire
  - Calculer les heures supplémentaires : heuresTravaillees - 151.67
  - Calculer le salaire des heures sup : heuresSup × tauxHoraire × 1.25
  - Additionner les deux montants

**Exemple :** Si tauxHoraire = 15$ et heures = 170
- Heures normales : 151.67 × 15 = 2275.05$
- Heures supplémentaires : 18.33 × 15 × 1.25 = 343.69$
- Total brut : 2618.74$

---

#### 2. Méthode `calculerCotisations`
**But :** Calculer le montant des cotisations sociales.

**Paramètres :**
- `salaireBrut` : salaire brut mensuel (`double`)

**Retour :** Montant des cotisations (`double`)

**Règle :** Les cotisations représentent 22% du salaire brut

**Formule :** `salaireBrut * 0.22`

---

#### 3. Méthode `calculerImpot`
**But :** Calculer l'impôt sur le revenu annuel selon le système de tranches progressives.

**Paramètres :**
- `salaireAnnuelNet` : salaire net annuel après cotisations (`double`)

**Retour :** Montant total de l'impôt annuel (`double`)

**Tranches d'imposition :**
- 0 à 10 000$ : 0%
- 10 001$ à 25 000$ : 11%
- 25 001$ à 50 000$ : 30%
- Au-delà de 50 000$ : 41%

**Algorithme (système de tranches) :**
- L'impôt se calcule tranche par tranche
- Exemple pour un salaire de 30 000$ :
  - Tranche 1 (0-10000) : 10000 × 0% = 0$
  - Tranche 2 (10001-25000) : 15000 × 11% = 1650$
  - Tranche 3 (25001-30000) : 5000 × 30% = 1500$
  - Total impôt : 3150$

**Pseudo-code :**
```
impot = 0
reste = salaireAnnuelNet

Si reste > 10000:
    impot += (min(reste, 25000) - 10000) × 0.11
Si reste > 25000:
    impot += (min(reste, 50000) - 25000) × 0.30
Si reste > 50000:
    impot += (reste - 50000) × 0.41
```

---

#### 4. Méthode `calculerBonus`
**But :** Calculer le bonus annuel selon l'ancienneté et la performance.

**Paramètres :**
- `salaireBrut` : salaire brut mensuel (`double`)
- `anciennete` : années d'ancienneté (`int`)
- `performance` : note de performance de 0 à 10 (`int`)

**Retour :** Montant du bonus mensuel (`double`)

**Règles :**
- Si performance < 7 : aucun bonus (retourner 0)
- Si performance >= 7 :
  - Bonus de base : 5% du salaire brut
  - Bonus d'ancienneté : +1% par année d'ancienneté (maximum +10%)
  - Le bonus total ne peut pas dépasser 15% du salaire brut

**Exemple :** 
- Salaire brut = 2000$, ancienneté = 8 ans, performance = 8
- Bonus de base : 2000 × 5% = 100$
- Bonus ancienneté : 2000 × 8% = 160$ (limité à 10% = 200$)
- Total bonus : 100 + 160 = 260$

---

#### 5. Méthode `genererFichePaie`
**But :** Générer et afficher une fiche de paie complète.

**Paramètres :**
- `nom` : nom de l'employé (`String`)
- `tauxHoraire` : taux horaire (`double`)
- `heuresTravaillees` : heures travaillées (`int`)
- `anciennete` : années d'ancienneté (`int`)
- `performance` : note de performance (`int`)

**Retour :** `void`

**Calculs à effectuer et afficher :**
1. Calculer le salaire brut (utiliser `calculerSalaireBrut`)
2. Calculer le nombre d'heures supplémentaires : max(0, heuresTravaillees - 151.67)
3. Calculer les cotisations (utiliser `calculerCotisations`)
4. Calculer le salaire net avant impôt : salaireBrut - cotisations
5. Calculer le bonus mensuel (utiliser `calculerBonus`)
6. Calculer le salaire annuel net : (salaire net + bonus) × 12
7. Calculer l'impôt annuel estimé (utiliser `calculerImpot`)
8. Calculer l'impôt mensuel : impôt annuel / 12
9. Calculer le salaire net mensuel final : salaire net + bonus - impôt mensuel

**Format d'affichage :**
```
╔════════════════════════════════════╗
║         FICHE DE PAIE              ║
╚════════════════════════════════════╝
Employé : Jean Dupont
Période : Janvier 2026

--- DÉTAILS DES HEURES ---
Heures travaillées : 170h
Heures supplémentaires : 18.33h
Taux horaire : 15.50$

--- CALCUL DU SALAIRE ---
Salaire brut : 2618.74$
Cotisations sociales (22%) : 576.12$
Salaire net avant impôt : 2042.62$
Bonus de performance : 131.00$
Salaire net avant impôt : 2173.62$

--- IMPÔTS (estimation annuelle) ---
Salaire annuel net : 26083.44$
Impôt annuel estimé : 1765.17$
Impôt mensuel : 147.10$

--- NET À PAYER ---
Salaire net mensuel : 2026.52$
```

---

#### 6. Méthode `main`
**But :** Tester le système avec plusieurs cas.

**Tests à effectuer :**
- Cas 1 : Employé standard sans heures sup
- Cas 2 : Employé avec heures supplémentaires
- Cas 3 : Employé avec haute performance et ancienneté
- Cas 4 : Employé avec basse performance (pas de bonus)

---

### ✅ Critères de validation
- [ ] Les heures supplémentaires sont calculées avec le bon taux (25%)
- [ ] Les cotisations sont correctement appliquées (22%)
- [ ] Le système de tranches d'imposition fonctionne correctement
- [ ] Le bonus est calculé selon les règles (performance et ancienneté)
- [ ] La fiche de paie affiche tous les éléments demandés
- [ ] Les montants sont arrondis à 2 décimales

### 💡 Conseils
- Testez chaque méthode séparément avec des valeurs simples
- Utilisez `System.out.printf("%.2f$%n", montant)` pour l'affichage
- Faites attention aux conversions int/double dans les calculs
- Vérifiez les cas limites (0 heures sup, performance minimale, etc.)

---

## 🎲 Projet 3 : Jeu de Devinette Avancé

### 📋 Contexte
Créez un jeu où l'ordinateur génère un nombre aléatoire et le joueur doit le deviner. Le jeu donne des indices de proximité et calcule un score selon la performance.

### 🎯 Objectifs pédagogiques
- Utilisation de la classe Random
- Boucles while pour le jeu
- Conditions multiples pour les indices
- Interaction avec l'utilisateur (Scanner)
- Calcul de scores

### 📝 Instructions 

Créez une classe `JeuDevinette` avec les méthodes suivantes :

#### 1. Méthode `genererNombre`
**But :** Générer un nombre aléatoire dans un intervalle.

**Paramètres :**
- `min` : valeur minimale (`int`)
- `max` : valeur maximale (`int`)

**Retour :** Nombre aléatoire entre min et max inclus (`int`)

**Algorithme :**
```java
Random random = new Random();
// Générer un nombre entre 0 et (max-min)
// Ajouter min pour obtenir un nombre entre min et max
```

**Formule :** `random.nextInt(max - min + 1) + min`

---

#### 2. Méthode `calculerDifference`
**But :** Calculer la différence absolue entre deux nombres.

**Paramètres :**
- `nombre1` : premier nombre (`int`)
- `nombre2` : deuxième nombre (`int`)

**Retour :** Différence absolue (`int`)

**Formule :** `Math.abs(nombre1 - nombre2)`

---

#### 3. Méthode `donnerIndice`
**But :** Fournir un indice textuel selon la proximité de la proposition.

**Paramètres :**
- `proposition` : nombre proposé par le joueur (`int`)
- `secret` : nombre à deviner (`int`)

**Retour :** Message d'indice (`String`)

**Règles :**
- Calculer la différence avec `calculerDifference`
- Selon la différence :
  - <= 5 : "🔥 Brûlant ! Vous êtes très proche !"
  - <= 10 : "♨️ Chaud ! Vous approchez !"
  - <= 20 : "🌡️ Tiède... continuez dans cette direction"
  - > 20 : "❄️ Froid ! Vous êtes loin"

**Bonus :** Ajouter aussi si le nombre est trop grand ou trop petit :
- "Le nombre secret est plus petit"
- "Le nombre secret est plus grand"

---

#### 4. Méthode `calculerScore`
**But :** Calculer le score final selon le nombre d'essais et la difficulté.

**Paramètres :**
- `nombreEssais` : nombre de tentatives utilisées (`int`)
- `difficulte` : niveau choisi : "Facile", "Moyen" ou "Difficile" (`String`)

**Retour :** Score (entre 0 et 1000+) (`int`)

**Formule de base :** `1000 - (nombreEssais × 50)`

**Multiplicateurs de difficulté :**
- "Facile" : ×1 (pas de bonus)
- "Moyen" : ×1.5
- "Difficile" : ×2

**Score minimum :** 0 (ne peut pas être négatif)

**Exemple :** 
- 8 essais en mode Difficile
- Score de base : 1000 - (8 × 50) = 600
- Avec multiplicateur ×2 : 600 × 2 = 1200

**Algorithme :**
```
scoreBase = 1000 - (nombreEssais × 50)
Si scoreBase < 0 alors scoreBase = 0

Selon difficulte:
  "Facile" : multiplicateur = 1.0
  "Moyen" : multiplicateur = 1.5
  "Difficile" : multiplicateur = 2.0

scoreFinal = scoreBase × multiplicateur
```

---

#### 5. Méthode `jouerPartie`
**But :** Gérer une partie complète du jeu.

**Paramètres :**
- `difficulte` : niveau choisi ("Facile", "Moyen", "Difficile") (`String`)

**Retour :** Score obtenu (`int`)

**Règles selon la difficulté :**
- Facile : nombre entre 1 et 50
- Moyen : nombre entre 1 et 100
- Difficile : nombre entre 1 et 200

**Algorithme  :**

1. Déterminer min et max selon la difficulté
2. Générer le nombre secret avec `genererNombre`
3. Initialiser le compteur d'essais à 0
4. Créer un Scanner pour lire les entrées

5. Boucle de jeu (tant que pas trouvé) :
   - Incrémenter le compteur d'essais
   - Afficher "Essai #X - Entrez un nombre :"
   - Lire la proposition du joueur
   
   - Si proposition == secret :
     - Afficher "🎉 Bravo ! Vous avez trouvé en X essais !"
     - Sortir de la boucle
   
   - Sinon :
     - Appeler `donnerIndice` et afficher le message
     - Continuer la boucle

6. Calculer le score avec `calculerScore`
7. Afficher "Score obtenu : X points"
8. Retourner le score

---

#### 6. Méthode `afficherMenu`
**But :** Afficher le menu de sélection de difficulté.

**Retour :** `void`

**Affichage :**
```
╔═══════════════════════════════╗
║     JEU DE DEVINETTE 🎲      ║
╚═══════════════════════════════╝

Choisissez votre difficulté :
1. 😊 Facile (1-50)
2. 🤔 Moyen (1-100)
3. 😈 Difficile (1-200)
4. 🚪 Quitter

Votre choix :
```

---

#### 7. Méthode `main`
**But :** Gérer le programme principal avec menu et statistiques.

**Algorithme :**

```
Initialiser :
  - scoreTotal = 0
  - nombreParties = 0
  - Scanner scanner

Boucle principale (continuer = true) :
  1. Afficher le menu
  2. Lire le choix du joueur
  
  3. Selon le choix :
     - 1 : jouer en mode Facile
     - 2 : jouer en mode Moyen
     - 3 : jouer en mode Difficile
     - 4 : sortir de la boucle
     - Autre : afficher "Choix invalide"
  
  4. Si une partie a été jouée :
     - Ajouter le score à scoreTotal
     - Incrémenter nombreParties
     - Demander "Voulez-vous rejouer ? (o/n)"
     - Lire la réponse
     - Si "n" : continuer = false

Après la boucle :
  Afficher les statistiques finales :
    - Nombre de parties jouées
    - Score total
    - Score moyen (si parties > 0)
    - Meilleur type de partie jouée
```

---

### ✅ Critères de validation
- [ ] Le nombre secret est bien généré aléatoirement
- [ ] Les indices de proximité sont corrects
- [ ] Le score est calculé selon la formule avec multiplicateur
- [ ] Le jeu se termine quand le joueur trouve
- [ ] Les statistiques finales sont correctes
- [ ] Le menu fonctionne avec tous les choix
- [ ] Le joueur peut rejouer ou quitter

### 💡 Conseils
- Testez d'abord avec un nombre fixe au lieu d'aléatoire pour déboguer
- Ajoutez des `System.out.println` pour suivre la progression
- Gérez les cas où l'utilisateur entre des lettres au lieu de nombres (try-catch)
- Améliorez l'expérience avec des emojis et des couleurs ANSI

### 🎁 Extensions possibles
- Ajouter un nombre maximum de tentatives
- Créer un mode "duel" (2 joueurs)
- Sauvegarder les meilleurs scores dans un fichier
- Ajouter un mode "Expert" avec intervalle très large

---

## 📅 Projet 4 : Calculateur de Dates

### 📋 Contexte
Créez un système complet de manipulation de dates sans utiliser les classes Java de dates (LocalDate, etc.). Tout doit être calculé manuellement avec des algorithmes.

### 🎯 Objectifs pédagogiques
- Algorithmes mathématiques
- Conditions complexes imbriquées
- Manipulation de nombres
- Validation de données

### 📝 Instructions 

Créez une classe `CalculateurDates` avec les méthodes suivantes :

#### 1. Méthode `estBissextile`
**But :** Déterminer si une année est bissextile.

**Paramètres :**
- `annee` : année à tester (`int`)

**Retour :** `true` si bissextile, `false` sinon (`boolean`)

**Règle officielle :**
Une année est bissextile si :
- Elle est divisible par 4 ET (non divisible par 100 OU divisible par 400)

**Exemples :**
- 2024 : divisible par 4 et pas par 100 → bissextile
- 2000 : divisible par 400 → bissextile
- 1900 : divisible par 100 mais pas par 400 → non bissextile
- 2023 : pas divisible par 4 → non bissextile

**Formule logique :**
```
(annee % 4 == 0) && ((annee % 100 != 0) || (annee % 400 == 0))
```

---

#### 2. Méthode `nombreJoursDansMois`
**But :** Retourner le nombre de jours dans un mois donné.

**Paramètres :**
- `mois` : numéro du mois (1-12) (`int`)
- `annee` : année (pour gérer février) (`int`)

**Retour :** Nombre de jours (`int`)

**Règles :**
- Janvier (1), Mars (3), Mai (5), Juillet (7), Août (8), Octobre (10), Décembre (12) : 31 jours
- Avril (4), Juin (6), Septembre (9), Novembre (11) : 30 jours
- Février (2) : 28 jours (29 si année bissextile)

**Algorithme :**
```
Si mois == 2:
    Si estBissextile(annee):
        retourner 29
    Sinon:
        retourner 28

Si mois == 4 ou 6 ou 9 ou 11:
    retourner 30

Sinon:
    retourner 31
```

---

#### 3. Méthode `dateValide`
**But :** Vérifier si une date est valide.

**Paramètres :**
- `jour` : jour (1-31) (`int`)
- `mois` : mois (1-12) (`int`)
- `annee` : année (`int`)

**Retour :** `true` si valide, `false` sinon (`boolean`)

**Vérifications :**
1. Le mois doit être entre 1 et 12
2. L'année doit être positive (> 0)
3. Le jour doit être entre 1 et le nombre de jours du mois
   (utiliser `nombreJoursDansMois`)

**Exemples :**
- 29/02/2024 : valide (année bissextile)
- 29/02/2023 : invalide (pas bissextile)
- 31/04/2024 : invalide (avril a 30 jours)
- 15/13/2024 : invalide (mois 13 n'existe pas)

---

#### 4. Méthode `jourDeLannee`
**But :** Calculer le numéro du jour dans l'année (1-366).

**Paramètres :**
- `jour`, `mois`, `annee` : la date (`int`)

**Retour :** Numéro du jour (1er janvier = 1) (`int`)

**Algorithme :**
1. Vérifier que la date est valide
2. Initialiser total = 0
3. Pour chaque mois avant le mois actuel :
   - Ajouter le nombre de jours de ce mois au total
4. Ajouter le jour du mois actuel
5. Retourner le total

**Exemple :** 15 mars 2024
- Janvier : 31 jours
- Février : 29 jours (bissextile)
- Mars : 15 jours
- Total : 31 + 29 + 15 = 75ème jour de l'année

---

#### 5. Méthode `jourDeLaSemaine`
**But :** Déterminer quel jour de la semaine correspond à une date.

**Paramètres :**
- `jour`, `mois`, `annee` : la date (`int`)

**Retour :** Nom du jour ("Lundi", "Mardi", etc.) (`String`)

**Algorithme simplifié (formule de Zeller modifiée) :**

Pour simplifier, utilisez cette formule :
```
Si mois < 3:
    mois = mois + 12
    annee = annee - 1

q = jour
m = mois
k = annee % 100
j = annee / 100

h = (q + (13*(m+1))/5 + k + k/4 + j/4 - 2*j) % 7
```

Convertir h en jour :
- h = 0 : Samedi
- h = 1 : Dimanche
- h = 2 : Lundi
- h = 3 : Mardi
- h = 4 : Mercredi
- h = 5 : Jeudi
- h = 6 : Vendredi

**Alternative plus simple :**
Vous pouvez aussi créer un tableau de référence avec des dates connues et calculer la différence en jours.

---

#### 6. Méthode `calculerAge`
**But :** Calculer l'âge exact d'une personne.

**Paramètres :**
- `jourNaissance`, `moisNaissance`, `anneeNaissance` : date de naissance
- `jourActuel`, `moisActuel`, `anneeActuel` : date actuelle

**Retour :** Âge en années (`int`)

**Algorithme :**
```
age = anneeActuel - anneeNaissance

Si moisActuel < moisNaissance:
    age = age - 1
Sinon si moisActuel == moisNaissance et jourActuel < jourNaissance:
    age = age - 1

retourner age
```

**Exemple :**
- Né le 15/03/2000
- Date actuelle : 28/01/2026
- Différence d'années : 2026 - 2000 = 26
- Mais le mois (01) est avant mars (03) → encore 25 ans
- Âge : 25 ans

---

#### 7. Méthode `determinerSaison`
**But :** Déterminer la saison selon la date.

**Paramètres :**
- `jour`, `mois` : la date (sans l'année) (`int`)

**Retour :** Nom de la saison (`String`)

**Règles (hémisphère nord) :**
- Printemps : du 21 mars au 20 juin
- Été : du 21 juin au 20 septembre
- Automne : du 21 septembre au 20 décembre
- Hiver : du 21 décembre au 20 mars

**Algorithme :**
```
Si (mois == 3 et jour >= 21) ou (mois == 4 ou 5) ou (mois == 6 et jour < 21):
    retourner "Printemps"

Si (mois == 6 et jour >= 21) ou (mois == 7 ou 8) ou (mois == 9 et jour < 21):
    retourner "Été"

Si (mois == 9 et jour >= 21) ou (mois == 10 ou 11) ou (mois == 12 et jour < 21):
    retourner "Automne"

Sinon:
    retourner "Hiver"
```

---

#### 8. Méthode `differenceEnJours`
**But :** Calculer le nombre de jours entre deux dates.

**Paramètres :**
- Date 1 : `jour1`, `mois1`, `annee1`
- Date 2 : `jour2`, `mois2`, `annee2`

**Retour :** Nombre de jours de différence (`int`)

**Algorithme (méthode simplifiée) :**

1. Vérifier que les deux dates sont valides
2. Convertir chaque date en "nombre de jours depuis une référence"
   Par exemple, depuis l'an 1 ou depuis l'an 2000
3. Calculer la différence absolue

**Pour convertir une date en jours depuis l'an 2000 :**
```
joursDepuis2000 = 0

Pour chaque année de 2000 à (annee - 1):
    Si bissextile: joursDepuis2000 += 366
    Sinon: joursDepuis2000 += 365

joursDepuis2000 += jourDeLannee(jour, mois, annee)
```

4. Faire ce calcul pour les deux dates
5. Retourner la différence absolue

---

#### 9. Méthode `afficherRapportDate`
**But :** Afficher un rapport complet d'analyse d'une date.

**Paramètres :**
- `jour`, `mois`, `annee` : la date à analyser (`int`)

**Retour :** `void`

**Informations à afficher :**
1. La date au format "DD/MM/YYYY"
2. Si la date est valide ou non
3. Le jour de la semaine
4. Le numéro du jour dans l'année
5. La saison
6. Si l'année est bissextile
7. Nombre de jours restants dans l'année
8. Nombre de jours dans le mois
9. Combien de jours jusqu'à la fin du mois

**Format attendu :**
```
╔════════════════════════════════════╗
║     ANALYSE DE DATE COMPLÈTE      ║
╚════════════════════════════════════╝

Date : 15/08/2024
Jour de la semaine : Jeudi
Jour de l'année : 228/366
Saison : Été

Informations sur l'année :
  - Année bissextile : Oui
  - Jours restants : 138

Informations sur le mois :
  - Août a 31 jours
  - Jours restants ce mois : 16
```

---

#### 10. Méthode `main`
**But :** Tester toutes les fonctionnalités.

**Tests à effectuer :**
1. Afficher le rapport pour plusieurs dates
2. Tester `calculerAge` avec différentes dates de naissance
3. Tester `differenceEnJours` entre deux dates
4. Tester des dates invalides
5. Tester des années bissextiles et non-bissextiles

---

### ✅ Critères de validation
- [ ] La détection d'année bissextile fonctionne correctement
- [ ] Le nombre de jours par mois est correct (y compris février)
- [ ] La validation de date détecte toutes les erreurs
- [ ] Le calcul du jour de l'année est précis
- [ ] Le jour de la semaine est correct
- [ ] Le calcul d'âge fonctionne même pour les dates limites
- [ ] La différence entre dates est exacte
- [ ] Les saisons sont correctement déterminées

### 💡 Conseils
- Testez d'abord les années bissextiles : 2000, 2024, 1900, 2100
- Testez février : 28/02 et 29/02 pour années bissextiles et non-bissextiles
- Testez des dates limites : 31/12, 1/1, 29/02
- Vérifiez les calculs avec un calendrier réel

### 🎁 Extensions possibles
- Ajouter la conversion entre calendriers (grégorien, julien)
- Calculer le nombre de jours ouvrables entre deux dates
- Trouver les dates de Pâques (algorithme de Gauss)
- Calculer les jours fériés

---

## 🏦 Projet 5 : Simulateur de Compte Bancaire

### 📋 Contexte
Développez un système complet de simulation de compte bancaire avec transactions, découvert, intérêts, frais et projections d'épargne.

### 🎯 Objectifs pédagogiques
- Gestion d'état (solde)
- Validation de transactions
- Calculs financiers
- Simulation temporelle

### 📝 Instructions 

Créez une classe `CompteBancaire` avec les méthodes suivantes :

#### 1. Méthode `effectuerDepot`
**But :** Effectuer un dépôt sur le compte.

**Paramètres :**
- `soldeActuel` : solde avant l'opération (`double`)
- `montant` : montant à déposer (`double`)

**Retour :** Nouveau solde après dépôt, ou -1 si invalide (`double`)

**Règles de validation :**
- Le montant doit être strictement positif (> 0)
- Si invalide, retourner -1 et ne pas modifier le solde

**Algorithme :**
```
Si montant <= 0:
    Afficher "Erreur : montant invalide"
    Retourner -1

nouveauSolde = soldeActuel + montant
Afficher "Dépôt de X$ effectué. Nouveau solde : Y$"
Retourner nouveauSolde
```

---

#### 2. Méthode `effectuerRetrait`
**But :** Effectuer un retrait avec gestion du découvert.

**Paramètres :**
- `soldeActuel` : solde actuel (`double`)
- `montant` : montant à retirer (`double`)
- `decouvertAutorise` : montant de découvert maximum (`double`)

**Retour :** Nouveau solde, ou -1 si impossible (`double`)

**Règles :**
- Le montant doit être positif
- Le solde après retrait doit rester >= -decouvertAutorise
- Si impossible, retourner -1

**Exemple :**
- Solde actuel : 100$
- Découvert autorisé : 200$
- Retrait possible jusqu'à : 100 + 200 = 300$
- Si retrait de 250$ : possible (nouveau solde = -150$)
- Si retrait de 350$ : impossible

**Algorithme :**
```
Si montant <= 0:
    Retourner -1

nouveauSolde = soldeActuel - montant

Si nouveauSolde < -decouvertAutorise:
    Afficher "Erreur : découvert dépassé"
    Retourner -1

Si nouveauSolde < 0:
    Afficher "Attention : vous êtes à découvert"

Afficher "Retrait de X$ effectué"
Retourner nouveauSolde
```

---

#### 3. Méthode `calculerInterets`
**But :** Calculer les intérêts mensuels pour un solde créditeur.

**Paramètres :**
- `solde` : solde du compte (`double`)
- `tauxAnnuel` : taux d'intérêt annuel en pourcentage (`double`)

**Retour :** Montant des intérêts (`double`)

**Règles :**
- Les intérêts ne sont calculés que si le solde est positif
- Si solde <= 0 : retourner 0
- Formule mensuelle : solde × (tauxAnnuel / 100) / 12

**Exemple :**
- Solde : 1000$
- Taux annuel : 2%
- Intérêts mensuels : 1000 × (2 / 100) / 12 = 1.67$

---

#### 4. Méthode `calculerFraisDecouvert`
**But :** Calculer les frais appliqués en cas de découvert.

**Paramètres :**
- `solde` : solde actuel (`double`)

**Retour :** Montant des frais (`double`)

**Règle :** 
- Si solde < 0 : frais de 8$
- Sinon : 0$

**Note :** Dans une vraie banque, ce serait des frais par jour de découvert, mais on simplifie ici.

---

#### 5. Méthode `determinerTypeCompte`
**But :** Déterminer le type de compte selon le solde moyen.

**Paramètres :**
- `soldeMoyen` : solde moyen sur la période (`double`)

**Retour :** Type de compte (`String`)

**Classification :**
- >= 5000$ : "Premium"
- >= 2000$ : "Gold"
- < 2000$ : "Standard"

---

#### 6. Méthode `calculerFraisGestion`
**But :** Calculer les frais de gestion mensuels.

**Paramètres :**
- `typeCompte` : type du compte (`String`)
- `nombreTransactions` : nombre de transactions du mois (`int`)

**Retour :** Montant des frais (`double`)

**Grille tarifaire :**

**Premium :**
- Gratuit (toutes transactions)

**Gold :**
- Gratuit si <= 20 transactions
- 5$ si > 20 transactions

**Standard :**
- 10$ de frais de base
- + 0,50$ par transaction au-delà de 10 transactions gratuites

**Exemples :**
- Standard avec 15 transactions : 10 + (5 × 0.50) = 12.50$
- Standard avec 8 transactions : 10$
- Gold avec 25 transactions : 5$
- Premium avec 100 transactions : 0$

---

#### 7. Méthode `virementPossible`
**But :** Vérifier si un virement est réalisable.

**Paramètres :**
- `soldeActuel` : solde actuel (`double`)
- `montant` : montant du virement (`double`)
- `decouvertAutorise` : découvert maximum (`double`)

**Retour :** `true` si possible, `false` sinon (`boolean`)

**Condition :** `soldeActuel - montant >= -decouvertAutorise`

---

#### 8. Méthode `simulerMois`
**But :** Simuler un mois complet d'opérations bancaires.

**Paramètres :**
- `soldeInitial` : solde au début du mois (`double`)
- `depots` : tableau des dépôts du mois (`double[]`)
- `retraits` : tableau des retraits du mois (`double[]`)
- `tauxInteret` : taux annuel (`double`)
- `decouvertAutorise` : découvert maximum (`double`)

**Retour :** `void` (affiche les résultats)

**Algorithme  :**

```
1. Initialiser :
   - solde = soldeInitial
   - nombreTransactions = 0
   - sommePositions = 0 (pour calculer le solde moyen)
   - compteurJours = 30

2. Afficher l'en-tête
   "=== SIMULATION MENSUELLE ==="
   "Solde initial : X$"

3. Traiter tous les dépôts :
   Pour chaque dépôt dans le tableau :
     - nouveauSolde = effectuerDepot(solde, dépôt)
     - Si valide : solde = nouveauSolde
     - nombreTransactions++
     - sommePositions += solde

4. Traiter tous les retraits :
   Pour chaque retrait dans le tableau :
     - nouveauSolde = effectuerRetrait(solde, retrait, découvert)
     - Si valide : solde = nouveauSolde
     - nombreTransactions++
     - sommePositions += solde

5. Calculer le solde moyen :
   soldeMoyen = sommePositions / (nombreTransactions + 1)

6. Déterminer le type de compte :
   typeCompte = determinerTypeCompte(soldeMoyen)

7. Appliquer intérêts ou frais de découvert :
   Si solde > 0 :
     - interets = calculerInterets(solde, tauxInteret)
     - solde += interets
     - Afficher "Intérêts créditeurs : +X$"
   Sinon :
     - frais = calculerFraisDecouvert(solde)
     - solde -= frais
     - Afficher "Frais de découvert : -X$"

8. Appliquer les frais de gestion :
   fraisGestion = calculerFraisGestion(typeCompte, nombreTransactions)
   solde -= fraisGestion
   Afficher "Frais de gestion : -X$"

9. Afficher le récapitulatif :
   - Type de compte
   - Nombre de transactions
   - Solde moyen
   - Solde final

Format d'affichage :
"""
=== SIMULATION MENSUELLE ===
Solde initial : 1000.00$

--- OPÉRATIONS DU MOIS ---
Dépôt de 500.00$ effectué. Nouveau solde : 1500.00$
Dépôt de 300.00$ effectué. Nouveau solde : 1800.00$
...
Retrait de 150.00$ effectué. Nouveau solde : 1650.00$
...

--- FIN DE MOIS ---
Intérêts créditeurs : +1.67$
Frais de gestion (Standard) : -10.00$

=== RÉCAPITULATIF ===
Type de compte : Standard
Solde moyen du mois : 1450.00$
Nombre de transactions : 7
Solde final : 1641.67$
"""
```

---

#### 9. Méthode `projeterEpargne`
**But :** Calculer le solde futur avec épargne régulière et intérêts composés.

**Paramètres :**
- `soldeInitial` : solde de départ (`double`)
- `depotMensuel` : montant épargné chaque mois (`double`)
- `tauxInteret` : taux annuel (`double`)
- `nombreMois` : durée de la projection (`int`)

**Retour :** Solde projeté (`double`)

**Algorithme :**
```
solde = soldeInitial

Pour i de 1 à nombreMois :
  1. Ajouter le dépôt mensuel :
     solde += depotMensuel
  
  2. Calculer les intérêts du mois :
     interets = calculerInterets(solde, tauxInteret)
     solde += interets
  
  3. (Optionnel) Afficher l'état après chaque mois :
     "Mois X : +depotMensuel$ +interets$ → solde$"

Retourner solde
```

**Exemple de calcul manuel :**
- Solde initial : 1000$
- Dépôt mensuel : 200$
- Taux annuel : 2%
- Durée : 3 mois

Mois 1 :
- Solde après dépôt : 1000 + 200 = 1200$
- Intérêts : 1200 × 0.02 / 12 = 2$
- Nouveau solde : 1202$

Mois 2 :
- Solde après dépôt : 1202 + 200 = 1402$
- Intérêts : 1402 × 0.02 / 12 = 2.34$
- Nouveau solde : 1404.34$

Et ainsi de suite...

---

#### 10. Méthode `main`
**But :** Tester toutes les fonctionnalités avec des scénarios réalistes.

**Scénarios à tester :**

**Test 1 : Simulation mensuelle normale**
```java
double soldeInitial = 1000.0;
double[] depots = {500.0, 300.0, 200.0};
double[] retraits = {150.0, 80.0, 200.0, 50.0};
double tauxInteret = 2.0;
double decouvertAutorise = 200.0;

simulerMois(soldeInitial, depots, retraits, tauxInteret, decouvertAutorise);
```

**Test 2 : Situation de découvert**
```java
double soldeInitial = 100.0;
double[] depots = {};
double[] retraits = {50.0, 80.0, 100.0};
// Solde final devrait être négatif avec frais
```

**Test 3 : Projection d'épargne**
```java
double soldeFutur = projeterEpargne(1000, 200, 2.0, 12);
System.out.println("Après 12 mois : " + soldeFutur + "$");
```

**Test 4 : Tests des types de compte**
```java
System.out.println("Solde 1500$ → " + determinerTypeCompte(1500));
System.out.println("Solde 3000$ → " + determinerTypeCompte(3000));
System.out.println("Solde 6000$ → " + determinerTypeCompte(6000));
```

---

### ✅ Critères de validation
- [ ] Les dépôts et retraits valident correctement les montants
- [ ] Le découvert est bien géré (pas de dépassement)
- [ ] Les intérêts sont calculés uniquement sur solde positif
- [ ] Les frais de découvert s'appliquent correctement
- [ ] La classification des comptes fonctionne
- [ ] Les frais de gestion sont calculés selon les bonnes règles
- [ ] La projection d'épargne inclut les intérêts composés
- [ ] Tous les montants sont affichés avec 2 décimales

### 💡 Conseils
- Utilisez `System.out.printf("%.2f$%n", montant)` pour formater
- Testez d'abord chaque méthode individuellement
- Vérifiez les cas limites (solde à 0, découvert au maximum, etc.)
- Ajoutez des messages clairs pour suivre les opérations

### 🎁 Extensions possibles
- Ajouter un historique des transactions (tableau ou ArrayList)
- Créer une méthode pour générer un relevé PDF
- Implémenter des virements entre comptes
- Ajouter des notifications de seuil de solde
- Créer un système de budget mensuel avec alertes

---

## 🎯 Projet 6 : Analyseur de Texte

### 📋 Contexte
Créez un outil d'analyse textuelle complet qui peut compter les mots, analyser la structure, calculer des statistiques et transformer le texte.

### 🎯 Objectifs pédagogiques
- Manipulation de chaînes de caractères (String)
- Méthodes de String (split, substring, charAt, length, etc.)
- Boucles sur les caractères
- Conditions pour classification

### 📝 Instructions 

Créez une classe `AnalyseurTexte` avec les méthodes suivantes :

#### 1. Méthode `compterMots`
**But :** Compter le nombre de mots dans un texte.

**Paramètres :**
- `texte` : texte à analyser (`String`)

**Retour :** Nombre de mots (`int`)

**Définition d'un mot :** Séquence de caractères séparée par des espaces

**Algorithme :**
```
1. Supprimer les espaces au début et à la fin : texte.trim()
2. Si le texte est vide : retourner 0
3. Découper le texte en mots : String[] mots = texte.split("\\s+")
   (\\s+ signifie : un ou plusieurs espaces)
4. Retourner la longueur du tableau de mots
```

**Exemples :**
- "Bonjour le monde" → 3 mots
- "Java    est    génial" → 3 mots (espaces multiples)
- "" → 0 mots
- "   " → 0 mots

---

#### 2. Méthode `compterPhrases`
**But :** Compter le nombre de phrases dans un texte.

**Paramètres :**
- `texte` : texte à analyser (`String`)

**Retour :** Nombre de phrases (`int`)

**Définition :** Une phrase se termine par `.` ou `!` ou `?`

**Algorithme :**
```
compteur = 0
Pour chaque caractère c du texte :
    Si c == '.' ou c == '!' ou c == '?' :
        compteur++
Retourner compteur
```

**Alternative avec méthode String :**
```java
int compteur = 0;
for (int i = 0; i < texte.length(); i++) {
    char c = texte.charAt(i);
    if (c == '.' || c == '!' || c == '?') {
        compteur++;
    }
}
return compteur;
```

---

#### 3. Méthode `compterVoyelles`
**But :** Compter le nombre de voyelles dans un texte.

**Paramètres :**
- `texte` : texte à analyser (`String`)

**Retour :** Nombre de voyelles (`int`)

**Voyelles :** a, e, i, o, u, y (et leurs majuscules)

**Algorithme :**
```
1. Convertir le texte en minuscules : texte.toLowerCase()
2. Initialiser compteur = 0
3. Pour chaque caractère c :
     Si c est dans "aeiouy" :
         compteur++
4. Retourner compteur
```

**Méthode pour vérifier si c'est une voyelle :**
```java
boolean estVoyelle(char c) {
    c = Character.toLowerCase(c);
    return c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u' || c == 'y';
}
```

---

#### 4. Méthode `compterConsonnes`
**But :** Compter le nombre de consonnes (lettres qui ne sont pas des voyelles).

**Paramètres :**
- `texte` : texte à analyser (`String`)

**Retour :** Nombre de consonnes (`int`)

**Algorithme :**
```
compteur = 0
Pour chaque caractère c :
    Si c est une lettre ET ce n'est pas une voyelle :
        compteur++

Retourner compteur
```

**Vérifier si c'est une lettre :**
```java
Character.isLetter(c)
```

---

#### 5. Méthode `longueurMoyenneMots`
**But :** Calculer la longueur moyenne des mots.

**Paramètres :**
- `texte` : texte à analyser (`String`)

**Retour :** Longueur moyenne (`double`)

**Algorithme :**
```
1. Découper le texte en mots
2. Si aucun mot : retourner 0.0
3. Initialiser somme = 0
4. Pour chaque mot :
     somme += longueur du mot (mot.length())
5. Retourner somme / nombre de mots
```

**Exemple :**
- "Bonjour le monde" → (7 + 2 + 5) / 3 = 4.67

---

#### 6. Méthode `motLePlusLong`
**But :** Trouver le mot le plus long dans le texte.

**Paramètres :**
- `texte` : texte à analyser (`String`)

**Retour :** Le mot le plus long (`String`)

**Algorithme :**
```
1. Découper le texte en mots
2. Si aucun mot : retourner ""
3. Initialiser :
     motMax = premier mot
     longueurMax = longueur du premier mot
4. Pour chaque mot suivant :
     Si longueur du mot > longueurMax :
         motMax = ce mot
         longueurMax = longueur de ce mot
5. Retourner motMax
```

**En cas d'égalité :** Retourner le premier trouvé

---

#### 7. Méthode `compterOccurrences`
**But :** Compter combien de fois un mot spécifique apparaît (insensible à la casse).

**Paramètres :**
- `texte` : texte à analyser (`String`)
- `motCherche` : mot à chercher (`String`)

**Retour :** Nombre d'occurrences (`int`)

**Règles :**
- Insensible à la casse ("Java" = "java" = "JAVA")
- Mot entier seulement ("le" ne doit pas compter dans "Manuel")

**Algorithme :**
```
1. Convertir texte et motCherche en minuscules
2. Découper le texte en mots
3. Initialiser compteur = 0
4. Pour chaque mot :
     Si mot (en minuscules) == motCherche (en minuscules) :
         compteur++
5. Retourner compteur
```

---

#### 8. Méthode `calculerLisibilite`
**But :** Calculer un indice de lisibilité du texte.

**Paramètres :**
- `texte` : texte à analyser (`String`)

**Retour :** Score de lisibilité (0-100, plus élevé = plus facile) (`double`)

**Formule simplifiée (inspirée de Flesch) :**
```
206.835 - (1.015 × mots par phrase) - (84.6 × syllabes par mot)
```

**Pour simplifier :** Estimez le nombre de syllabes en comptant les voyelles

**Algorithme :**
```
1. Compter le nombre de mots (W)
2. Compter le nombre de phrases (S)
3. Compter le nombre de voyelles (V) comme approximation des syllabes

4. Si S == 0, retourner 0 (éviter division par zéro)

5. motsParPhrase = W / S
6. syllabesParMot = V / W

7. score = 206.835 - (1.015 × motsParPhrase) - (84.6 × syllabesParMot)

8. Limiter le score entre 0 et 100 :
   Si score > 100 : score = 100
   Si score < 0 : score = 0

9. Retourner score
```

---

#### 9. Méthode `determinerNiveauComplexite`
**But :** Déterminer le niveau de complexité selon l'indice de lisibilité.

**Paramètres :**
- `indiceLisibilite` : score calculé (`double`)

**Retour :** Niveau de complexité (`String`)

**Classification :**
- >= 90 : "Très facile"
- >= 70 : "Facile"
- >= 50 : "Moyen"
- >= 30 : "Difficile"
- < 30 : "Très difficile"

---

#### 10. Méthode `inverserTexte`
**But :** Inverser l'ordre des mots dans le texte.

**Paramètres :**
- `texte` : texte à inverser (`String`)

**Retour :** Texte avec mots dans l'ordre inverse (`String`)

**Exemple :**
- "Bonjour le monde" → "monde le Bonjour"

**Algorithme :**
```
1. Découper le texte en mots
2. Créer un nouveau String vide (résultat)
3. Parcourir le tableau de mots de la fin au début :
     Pour i de (longueur-1) à 0 (décroissant) :
         Ajouter mots[i] au résultat
         Ajouter un espace (sauf pour le dernier)
4. Retourner résultat
```

---

#### 11. Méthode `filtrerMotsCourts`
**But :** Supprimer tous les mots plus courts qu'une longueur donnée.

**Paramètres :**
- `texte` : texte à filtrer (`String`)
- `longueurMin` : longueur minimale (`int`)

**Retour :** Texte filtré (`String`)

**Algorithme :**
```
1. Découper le texte en mots
2. Créer un String vide pour le résultat
3. Pour chaque mot :
     Si longueur du mot >= longueurMin :
         Ajouter le mot au résultat
         Ajouter un espace
4. Retirer l'espace final (trim)
5. Retourner résultat
```

**Exemple :**
- Texte : "Je suis un développeur Java"
- Longueur min : 4
- Résultat : "suis développeur Java"

---

#### 12. Méthode `genererRapport`
**But :** Générer et afficher un rapport complet d'analyse.

**Paramètres :**
- `texte` : texte à analyser (`String`)

**Retour :** `void`

**Informations à afficher :**
```
╔════════════════════════════════════╗
║      ANALYSE DE TEXTE COMPLÈTE    ║
╚════════════════════════════════════╝

TEXTE ANALYSÉ :
[Afficher le texte]

--- STATISTIQUES GÉNÉRALES ---
Nombre de caractères (avec espaces) : X
Nombre de caractères (sans espaces) : Y
Nombre de mots : Z
Nombre de phrases : N
Nombre de voyelles : V
Nombre de consonnes : C

--- ANALYSE DES MOTS ---
Longueur moyenne des mots : X.XX caractères
Mot le plus long : "XXXXXXXXX" (X lettres)
Mots par phrase (moyenne) : X.XX

--- LISIBILITÉ ---
Indice de lisibilité : XX.XX
Niveau de complexité : XXXXXX

--- COMPOSITION ---
Voyelles : XX% du texte
Consonnes : XX% du texte
```

**Algorithme  :**
```
1. Afficher l'en-tête
2. Afficher le texte
3. Calculer et afficher :
   - Longueur avec espaces : texte.length()
   - Longueur sans espaces : texte.replace(" ", "").length()
   - Appeler compterMots(texte)
   - Appeler compterPhrases(texte)
   - Appeler compterVoyelles(texte)
   - Appeler compterConsonnes(texte)
4. Calculer et afficher :
   - Appeler longueurMoyenneMots(texte)
   - Appeler motLePlusLong(texte)
   - Mots par phrase : compterMots / compterPhrases
5. Calculer et afficher :
   - Appeler calculerLisibilite(texte)
   - Appeler determinerNiveauComplexite(indice)
6. Calculer les pourcentages :
   - % voyelles : (voyelles / longueurSansEspaces) × 100
   - % consonnes : (consonnes / longueurSansEspaces) × 100
```

---

#### 13. Méthode `main`
**But :** Tester toutes les fonctionnalités.

**Tests à effectuer :**

**Test 1 : Texte exemple**
```java
String texte = "Java est un langage de programmation orienté objet. " +
               "Il est largement utilisé pour développer des applications. " +
               "Ce langage offre une grande portabilité et robustesse.";

genererRapport(texte);
```

**Test 2 : Transformations**
```java
System.out.println("
--- TRANSFORMATIONS ---");
System.out.println("Texte inversé : " + inverserTexte(texte));
System.out.println("Sans mots courts (<4) : " + filtrerMotsCourts(texte, 4));
```

**Test 3 : Occurrences**
```java
System.out.println("
--- RECHERCHE ---");
System.out.println("Occurrences de 'Java' : " + compterOccurrences(texte, "Java"));
System.out.println("Occurrences de 'est' : " + compterOccurrences(texte, "est"));
```

**Test 4 : Cas limites**
```java
String texteVide = "";
String texteUnMot = "Bonjour";
String texteEspaces = "   Multiple    espaces   ";
// Tester avec ces cas
```

---

### ✅ Critères de validation
- [ ] Le comptage de mots gère les espaces multiples
- [ ] Les voyelles incluent y et sont insensibles à la casse
- [ ] Les consonnes n'incluent que les lettres
- [ ] La recherche d'occurrences est insensible à la casse
- [ ] L'inversion de texte préserve l'ordre dans chaque mot
- [ ] Le filtrage conserve les espaces correctement
- [ ] Le rapport affiche toutes les informations demandées
- [ ] Les pourcentages sont calculés correctement

### 💡 Conseils
- Utilisez String.split("\\s+") pour gérer les espaces multiples
- Character.isLetter(c) est utile pour identifier les lettres
- Testez avec des textes en majuscules, minuscules et mixtes
- Gérez les cas où le texte est vide ou null

### 🎁 Extensions possibles
- Ajouter la détection de mots-clés (programmation, Java, etc.)
- Créer un correcteur orthographique basique
- Analyser la ponctuation utilisée
- Détecter les mots répétés consécutifs
- Générer un nuage de mots (afficher les mots les plus fréquents)

---

## 🎰 Projet 7 : Machine à Sous (Slot Machine)

### 📋 Contexte
Créez un jeu de machine à sous complet avec rouleaux, symboles, calcul de gains, système de crédits et statistiques de session.

### 🎯 Objectifs pédagogiques
- Génération de nombres aléatoires
- Logique de jeu et conditions complexes
- Gestion d'état (crédits, tours)
- Interaction utilisateur avec Scanner
- Calculs de probabilités et gains

### 📝 Instructions 

Créez une classe `MachineASous` avec les méthodes suivantes :

#### 1. Méthode `genererSymbole`
**But :** Générer aléatoirement un symbole de rouleau.

**Paramètres :** Aucun

**Retour :** Un symbole (`String`)

**Symboles disponibles :**
- 🍒 Cerise
- 🍋 Citron
- 🍊 Orange
- 🔔 Cloche
- ⭐ Étoile
- 💎 Diamant
- 7 Sept

**Algorithme :**
```
1. Créer un tableau : String[] symboles = {"🍒", "🍋", "🍊", "🔔", "⭐", "💎", "7"}
2. Générer un index aléatoire entre 0 et 6 :
   Random random = new Random();
   int index = random.nextInt(7);
3. Retourner symboles[index]
```

**Note :** Tous les symboles ont la même probabilité (1/7).

---

#### 2. Méthode `lancerRouleaux`
**But :** Lancer les trois rouleaux et retourner les symboles.

**Paramètres :** Aucun

**Retour :** Tableau de 3 symboles (`String[]`)

**Algorithme :**
```
1. Créer un tableau de taille 3 : String[] rouleaux = new String[3]
2. Pour i de 0 à 2 :
     rouleaux[i] = genererSymbole()
3. Retourner rouleaux
```

---

#### 3. Méthode `afficherRouleaux`
**But :** Afficher les rouleaux de manière visuelle et attractive.

**Paramètres :**
- `rouleaux` : tableau de 3 symboles (`String[]`)

**Retour :** `void`

**Format d'affichage :**
```
╔════════════════════╗
║   🍒 │ 🍋 │ 🍊   ║
╚════════════════════╝
```

**Algorithme :**
```java
System.out.println("╔════════════════════╗");
System.out.println("║   " + rouleaux[0] + " │ " + rouleaux[1] + " │ " + rouleaux[2] + "   ║");
System.out.println("╚════════════════════╝");
```

---

#### 4. Méthode `troisSymbolesIdentiques`
**But :** Vérifier si les trois symboles sont identiques.

**Paramètres :**
- `rouleaux` : tableau de 3 symboles (`String[]`)

**Retour :** `true` si les 3 sont identiques, `false` sinon (`boolean`)

**Algorithme :**
```
Retourner rouleaux[0].equals(rouleaux[1]) && rouleaux[1].equals(rouleaux[2])
```

**Note :** Utiliser `.equals()` et non `==` pour comparer des String

---

#### 5. Méthode `deuxSymbolesIdentiques`
**But :** Vérifier si exactement 2 symboles sur 3 sont identiques.

**Paramètres :**
- `rouleaux` : tableau de 3 symboles (`String[]`)

**Retour :** `true` si 2 sont identiques, `false` sinon (`boolean`)

**Algorithme :**
```
Si les 3 sont identiques : retourner false
Si rouleaux[0] == rouleaux[1] : retourner true
Si rouleaux[0] == rouleaux[2] : retourner true
Si rouleaux[1] == rouleaux[2] : retourner true
Sinon : retourner false
```

---

#### 6. Méthode `obtenirMultiplicateur`
**But :** Retourner le multiplicateur de gain selon le symbole.

**Paramètres :**
- `symbole` : le symbole (`String`)

**Retour :** Multiplicateur (`int`)

**Table des multiplicateurs :**
- 🍒 (Cerise) : ×2
- 🍋 (Citron) : ×3
- 🍊 (Orange) : ×4
- 🔔 (Cloche) : ×5
- ⭐ (Étoile) : ×10
- 💎 (Diamant) : ×20
- 7 (Sept) : ×50 (JACKPOT!)

**Algorithme avec switch :**
```java
switch (symbole) {
    case "🍒": return 2;
    case "🍋": return 3;
    case "🍊": return 4;
    case "🔔": return 5;
    case "⭐": return 10;
    case "💎": return 20;
    case "7": return 50;
    default: return 0;
}
```

---

#### 7. Méthode `calculerGains`
**But :** Calculer les gains d'un tour selon les rouleaux et la mise.

**Paramètres :**
- `rouleaux` : tableau de 3 symboles (`String[]`)
- `mise` : montant misé (`double`)

**Retour :** Montant gagné (`double`)

**Règles de gains :**
- **3 symboles identiques :** mise × multiplicateur du symbole
- **2 symboles identiques :** mise × 1.5
- **Aucune correspondance :** 0

**Algorithme :**
```
Si troisSymbolesIdentiques(rouleaux) :
    symbole = rouleaux[0]
    multiplicateur = obtenirMultiplicateur(symbole)
    gains = mise × multiplicateur
    retourner gains

Sinon si deuxSymbolesIdentiques(rouleaux) :
    gains = mise × 1.5
    retourner gains

Sinon :
    retourner 0.0
```

**Exemples :**
- 🍒 🍒 🍒 avec mise de 5$ → 5 × 2 = 10$
- 💎 💎 💎 avec mise de 10$ → 10 × 20 = 200$
- 🍋 🍋 🍊 avec mise de 5$ → 5 × 1.5 = 7.50$
- 🍒 🍋 🍊 avec mise de 5$ → 0$

---

#### 8. Méthode `afficherResultat`
**But :** Afficher un message selon les gains.

**Paramètres :**
- `gains` : montant gagné (`double`)
- `mise` : montant misé (`double`)

**Retour :** `void`

**Messages selon les gains :**
- gains == 0 : "❌ Perdu ! Vous perdez X$"
- gains == mise : "🤝 Remboursé ! Vous récupérez votre mise"
- gains < mise × 5 : "💰 Petit gain ! Vous gagnez X$"
- gains < mise × 20 : "🎉 Beau gain ! Vous gagnez X$"
- gains >= mise × 20 : "🎊 JACKPOT ! Vous gagnez X$ !!!"

**Algorithme :**
```java
if (gains == 0) {
    System.out.printf("❌ Perdu ! Vous perdez %.2f$%n", mise);
} else if (gains == mise) {
    System.out.println("🤝 Remboursé ! Vous récupérez votre mise");
} else if (gains < mise * 5) {
    System.out.printf("💰 Petit gain ! Vous gagnez %.2f$%n", gains);
} else if (gains < mise * 20) {
    System.out.printf("🎉 Beau gain ! Vous gagnez %.2f$%n", gains);
} else {
    System.out.printf("🎊 JACKPOT ! Vous gagnez %.2f$ !!!%n", gains);
}
```

---

#### 9. Méthode `afficherStatistiques`
**But :** Afficher les statistiques de la session de jeu.

**Paramètres :**
- `toursJoues` : nombre de tours joués (`int`)
- `toursGagnes` : nombre de tours avec gains (`int`)
- `creditsInitiaux` : crédits au début (`double`)
- `creditsFinaux` : crédits à la fin (`double`)

**Retour :** `void`

**Format d'affichage :**
```
╔══════════════════════════════╗
║   STATISTIQUES DE SESSION    ║
╚══════════════════════════════╝
Tours joués : X
Tours gagnés : Y
Taux de réussite : Z.Z%

Crédits de départ : XX.XX$
Crédits finaux : YY.YY$
[Bénéfice/Perte] : ±ZZ.ZZ$
```

**Algorithme :**
```
1. Afficher l'en-tête
2. Afficher tours joués et tours gagnés
3. Si toursJoues > 0 :
     tauxReussite = (toursGagnes / toursJoues) × 100
     Afficher le taux
4. Afficher crédits initiaux et finaux
5. Calculer la différence :
     difference = creditsFinaux - creditsInitiaux
6. Si différence > 0 :
     Afficher "✅ Bénéfice : +X$"
   Si différence < 0 :
     Afficher "❌ Perte : X$" (valeur absolue)
   Sinon :
     Afficher "🤝 À l'équilibre"
```

---

#### 10. Méthode `jouerTour`
**But :** Jouer un tour complet de machine à sous.

**Paramètres :**
- `credits` : crédits disponibles (`double`)
- `mise` : montant de la mise (`double`)

**Retour :** Nouveaux crédits après le tour (`double`)

**Algorithme  :**
```
1. Vérifier si la mise est possible :
   Si mise > credits :
       Afficher "❌ Crédits insuffisants !"
       Retourner credits (inchangés)

2. Déduire la mise :
   credits = credits - mise

3. Afficher l'animation :
   System.out.println("
🎰 Les rouleaux tournent...")
   (Optionnel : ajouter une pause)

4. Lancer les rouleaux :
   rouleaux = lancerRouleaux()

5. Afficher les rouleaux :
   afficherRouleaux(rouleaux)

6. Calculer les gains :
   gains = calculerGains(rouleaux, mise)

7. Afficher le résultat :
   afficherResultat(gains, mise)

8. Ajouter les gains aux crédits :
   credits = credits + gains

9. Afficher le nouveau solde :
   System.out.printf("Nouveau solde : %.2f$%n", credits)

10. Retourner credits
```

---

#### 11. Méthode `jouer` (jeu principal)
**But :** Gérer le jeu complet avec boucle de jeu et menu.

**Paramètres :** Aucun

**Retour :** `void`

**Algorithme complet :**
```
1. Initialiser :
   Scanner scanner = new Scanner(System.in);
   double credits = 100.0;  // Crédits de départ
   double creditsInitiaux = credits;
   int toursJoues = 0;
   int toursGagnes = 0;

2. Afficher l'écran de bienvenue :
   ╔══════════════════════════════╗
   ║    MACHINE À SOUS 🎰         ║
   ╚══════════════════════════════╝
   Crédits de départ : 100.00$

   TABLE DES GAINS :
   🍒 🍒 🍒 : ×2
   🍋 🍋 🍋 : ×3
   🍊 🍊 🍊 : ×4
   🔔 🔔 🔔 : ×5
   ⭐ ⭐ ⭐ : ×10
   💎 💎 💎 : ×20
   7  7  7  : ×50 JACKPOT!
   2 symboles identiques : ×1.5

3. Boucle de jeu (tant que credits >= 1) :
   a. Afficher le menu :
      "\n💰 Crédits : X.XX$"
      "Choisissez votre mise :"
      "1. 1$"
      "2. 2$"
      "3. 5$"
      "4. 10$ (max)"
      "0. Quitter"
      "Votre choix : "

   b. Lire le choix du joueur

   c. Selon le choix :
      - 0 : sortir de la boucle
      - 1 : mise = 1
      - 2 : mise = 2
      - 3 : mise = 5
      - 4 : mise = 10
      - Autre : afficher "Choix invalide", continuer

   d. Vérifier que la mise <= credits
      Sinon : afficher erreur, continuer

   e. Jouer le tour :
      creditsAvant = credits
      credits = jouerTour(credits, mise)
      toursJoues++

   f. Si credits > creditsAvant :
      toursGagnes++

   g. Attendre avant le prochain tour (optionnel) :
      System.out.println("
Appuyez sur Entrée pour continuer...");
      scanner.nextLine();

4. Fin du jeu :
   Si credits < 1 :
       Afficher "
💔 Vous n'avez plus de crédits !"
   Sinon :
       Afficher "
👋 Merci d'avoir joué !"

5. Afficher les statistiques finales :
   afficherStatistiques(toursJoues, toursGagnes, creditsInitiaux, credits);

6. Fermer le scanner :
   scanner.close();
```

---

#### 12. Méthode `main`
**But :** Lancer le jeu.

**Code :**
```java
public static void main(String[] args) {
    jouer();
}
```

---

### ✅ Critères de validation
- [ ] Les symboles sont générés aléatoirement
- [ ] Les trois rouleaux sont indépendants
- [ ] Le calcul des gains suit les règles exactes
- [ ] Les crédits sont correctement mis à jour
- [ ] Le jeu s'arrête quand crédits < 1
- [ ] Les statistiques sont calculées correctement
- [ ] Le taux de réussite est un pourcentage entre 0 et 100
- [ ] L'affichage est clair et attractif

### 💡 Conseils
- Testez d'abord avec des symboles fixes pour vérifier la logique
- Utilisez `System.out.printf("%.2f$", montant)` pour formater l'argent
- Ajoutez des `Thread.sleep(1000)` pour des pauses dramatiques (importer java.lang.Thread)
- Vérifiez tous les cas : 3 identiques, 2 identiques, aucun
- Testez les cas limites : crédits à 0, mise maximale, etc.

### 🎁 Extensions possibles
- Ajouter des symboles spéciaux (Wild, Scatter)
- Implémenter des tours gratuits (free spins)
- Créer des niveaux de difficulté (probabilités différentes)
- Ajouter un système de jackpot progressif
- Sauvegarder les meilleurs scores
- Créer un système de multiplicateurs en cascade
- Ajouter des sons (avec des caractères BEEP)

---

## 📊 Grille d'évaluation générale

Pour chaque projet, voici comment vous serez évalué :

### Fonctionnalité (50 points)
- [ ] Toutes les méthodes demandées sont implémentées (20 pts)
- [ ] Les méthodes fonctionnent correctement (20 pts)
- [ ] Les calculs sont exacts (10 pts)

### Qualité du code (30 points)
- [ ] Noms de variables et méthodes clairs (10 pts)
- [ ] Code bien indenté et lisible (10 pts)
- [ ] Commentaires pertinents (10 pts)

### Robustesse (20 points)
- [ ] Validation des entrées utilisateur (10 pts)
- [ ] Gestion des cas limites (5 pts)
- [ ] Pas d'erreurs à l'exécution (5 pts)

**Total : 100 points par projet**

---

## 💡 Conseils généraux pour tous les projets

### 1. Méthodologie de développement
1. **Lire** entièrement les instructions
2. **Planifier** : liste des méthodes à créer
3. **Développer** méthode par méthode (commencer par les plus simples)
4. **Tester** chaque méthode individuellement
5. **Intégrer** progressivement
6. **Déboguer** en cas de problème
7. **Améliorer** le code (refactoring)

### 2. Techniques de débogage
- Utiliser `System.out.println()` pour afficher les valeurs
- Tester avec des valeurs simples et connues
- Isoler le problème (quelle méthode ne fonctionne pas ?)
- Vérifier les types de données (int vs double)
- Attention aux divisions par zéro

### 3. Bonnes pratiques Java
```java
// ✅ Bon
public static double calculerMoyenne(double[] notes) {
    if (notes == null || notes.length == 0) {
        return 0.0;
    }
    double somme = 0.0;
    for (double note : notes) {
        somme += note;
    }
    return somme / notes.length;
}

// ❌ Mauvais
public static double calcul(double[] n) {
    double s = 0;
    for (int i = 0; i < n.length; i++) {
        s = s + n[i];
    }
    return s / n.length;  // Erreur possible si n.length == 0
}
```

### 4. Checklist avant de soumettre
- [ ] Le code compile sans erreur
- [ ] Toutes les méthodes demandées sont présentes
- [ ] Les tests dans `main` fonctionnent
- [ ] Le code est indenté correctement
- [ ] Les noms de variables sont explicites
- [ ] Les cas limites sont gérés
- [ ] Des commentaires expliquent la logique complexe

---

## 🚀 Ordre recommandé des projets

**Pour débutants :**
1. Projet 1 (Gestion de Notes) - Le plus simple
2. Projet 4 (Calculateur de Dates) - Logique pure
3. Projet 6 (Analyseur de Texte) - Manipulation de String

**Pour intermédiaires :**
4. Projet 5 (Compte Bancaire) - Plus de logique
5. Projet 2 (Calculateur de Salaire) - Calculs complexes

**Pour avancés :**
6. Projet 3 (Jeu de Devinette) - Interaction utilisateur
7. Projet 7 (Machine à Sous) - Le plus complet

---

## 📚 Ressources Java utiles

### Méthodes String importantes
- `length()` : longueur de la chaîne
- `charAt(index)` : caractère à la position
- `substring(debut, fin)` : sous-chaîne
- `split(regex)` : découper en tableau
- `trim()` : supprimer espaces début/fin
- `toLowerCase()` / `toUpperCase()`
- `equals(autre)` : comparer deux String
- `replace(ancien, nouveau)` : remplacer

### Méthodes de tableaux
- `array.length` : taille du tableau
- `Arrays.toString(array)` : afficher un tableau

### Classe Math
- `Math.abs(x)` : valeur absolue
- `Math.max(a, b)` : maximum
- `Math.min(a, b)` : minimum
- `Math.pow(x, y)` : puissance
- `Math.round(x)` : arrondir

### Classe Random
```java
Random random = new Random();
int nombre = random.nextInt(100);  // 0-99
int nombreDe = random.nextInt(6) + 1;  // 1-6
```

### Scanner
```java
Scanner scanner = new Scanner(System.in);
int nombre = scanner.nextInt();
double decimal = scanner.nextDouble();
String texte = scanner.nextLine();
scanner.close();  // Important !
```
