+++
title = "Structures de contrôle"
weight = 4
url = "/structures/"

+++


## Les structures de contrôle en Java

### Introduction

Jusqu’à présent, vos programmes s’exécutaient **ligne par ligne**, de haut en bas, comme une recette suivie à la lettre.  
Les **structures de contrôle** permettent de **prendre des décisions** et de **répéter des actions**.

👉 Grâce à elles, un programme devient **intelligent**, **dynamique** et **utile dans la vraie vie**.

On distingue trois grandes familles :
1. Les **structures conditionnelles** (faire un choix)
2. Les **structures répétitives** (répéter une action)
3. Les **structures de contrôle de flux** (modifier le déroulement)

---

## 1. Les structures conditionnelles

Les structures conditionnelles permettent d’exécuter du code **seulement si une condition est vraie**.

### 1.1 La structure `if`

#### Syntaxe
```java
if (condition) {
    // instructions exécutées si la condition est vraie
}
```
> **Règle importante :**  
> La condition doit toujours être **une expression booléenne**, c’est-à-dire une expression qui retourne `true` ou `false`.

### 1.1 La structure `if`

#### Syntaxe
```java
if (condition) {
    // instructions exécutées si la condition est vraie
}
```
La condition est évaluée :

* si elle est true, le bloc est exécuté

* si elle est false, le bloc est ignoré

#### Exemple
```java
int age = 18;

if (age >= 18) {
    System.out.println("Accès autorisé");
}
```

### 1.2 La structure if / else

Permet de choisir entre deux chemins possibles.

#### Syntaxe

```java
if (condition) {
    // exécuté si la condition est vraie
} else {
    // exécuté si la condition est fausse
}
```

#### Exemple
```java
int temperature = 15;

if (temperature >= 20) {
    System.out.println("Il fait chaud");
} else {
    System.out.println("Il fait frais");
}
```

Un seul des deux blocs sera exécuté.

---

## ❓ L’opérateur ternaire en Java

L’opérateur **ternaire** est une **forme abrégée du `if...else`**, qui permet d’**écrire des conditions simples en une seule ligne**.

Il est souvent utilisé pour **rendre le code plus concis**, surtout lorsqu’on veut **affecter une valeur selon une condition**.

---

## 🧰 Syntaxe de base

```java
(condition) ? valeurSiVrai : valeurSiFaux;
```

C’est comme dire :
**"Si la condition est vraie, retourne ceci ; sinon, retourne cela."**

---

## 📦 Exemple simple

```java
int âge = 20;
String statut = (âge >= 18) ? "Majeur" : "Mineur";

System.out.println(statut);  // Affiche : Majeur
```

✳️ C’est équivalent à :

```java
String statut;
if (âge >= 18) {
    statut = "Majeur";
} else {
    statut = "Mineur";
}
```

---

## ⚙️ Utilisation typique

L’opérateur ternaire est **très utilisé pour affecter une valeur** selon une condition :

```java
double note = 85;
String résultat = (note >= 60) ? "Réussi" : "Échoué";
```

On peut aussi l’utiliser directement dans un `System.out.println()` :

```java
System.out.println((note >= 90) ? "Excellent" : "À améliorer");
```

---

## 🛑 À éviter pour les cas complexes

Même si l'opérateur ternaire est pratique, il **devient illisible si la condition ou les valeurs sont longues** :

```java
// Trop compliqué !
String grade = (score >= 90) ? "A" : (score >= 75) ? "B" : "C";
// 🤯 Difficile à lire et à maintenir
```

➡️ Dans ces cas-là, préfère une structure `if...else` classique.

---

## 🔥 À retenir

* L’opérateur ternaire est une **forme courte de `if...else`**.
* Il s’écrit : `(condition) ? valeurSiVrai : valeurSiFaux;`
* Très utile pour **initialiser une variable** selon une condition.
* À **éviter** si la logique devient trop complexe ou trop imbriquée.
* Rends le code **plus compact**, mais pas toujours plus clair.

---

### 1.3 La structure if / else if / else

Utilisée lorsqu’il y a plusieurs choix possibles.

#### Syntaxe
```java
if (condition1) {
    // cas 1
} else if (condition2) {
    // cas 2
} else {
    // cas par défaut
}
```

#### Exemple
```java
int note = 72;

if (note >= 90) {
    System.out.println("Excellent");
} else if (note >= 60) {
    System.out.println("Réussi");
} else {
    System.out.println("Échec");
}
```

Les conditions sont testées dans l’ordre, et Java s’arrête dès qu’une condition est vraie.

### 1.4 Erreurs fréquentes avec les conditions
**Confusion entre `=` et ``==``**
```java
if (x = 5) { } // ERREUR

if (x == 5) { } // CORRECT
```

**Oubli des accolades**
```java
if (x > 0)
    System.out.println("Positif");
    System.out.println("Fin");
```

Dans ce cas, "Fin" s’affiche toujours.

---

## 🎛️ Les instructions `switch` en Java

L’instruction **`switch`** permet de **tester la valeur d’une variable** et d’exécuter **différents blocs de code** selon son **contenu exact**.

C’est une **alternative plus claire aux chaînes de `if...else if`** quand on compare **une même variable** à **plusieurs valeurs possibles**.

---

## 🧰 Syntaxe de base

```java
switch (variable) {
    case valeur1:
        // Code si variable == valeur1
        break;

    case valeur2:
        // Code si variable == valeur2
        break;

    default:
        // Code si aucune des valeurs ne correspond
}
```

### 🧱 Éléments clés :

| Mot-clé   | Rôle                                    |
| --------- | --------------------------------------- |
| `case`    | Spécifie une **valeur à tester**        |
| `break`   | Termine le `switch`, évite les "chutes" |
| `default` | (optionnel) Bloc exécuté **par défaut** |

---

## 📦 Exemple simple

```java
int jour = 3;

switch (jour) {
    case 1:
        System.out.println("Lundi");
        break;
    case 2:
        System.out.println("Mardi");
        break;
    case 3:
        System.out.println("Mercredi");
        break;
    default:
        System.out.println("Jour inconnu");
}
```

➡️ Affichera : `Mercredi`

---

## ⚠️ Le `break` est important !

Sans le `break`, le programme **continue dans les cases suivantes**, même si elles ne correspondent pas :

```java
int x = 2;

switch (x) {
    case 1:
        System.out.println("Un");
    case 2:
        System.out.println("Deux");
    case 3:
        System.out.println("Trois");
}
```

➡️ Affichera :

```
Deux  
Trois
```

---

## 🧠 Le bloc `default`

Le mot-clé `default` permet de **gérer les cas non prévus** :

```java
char lettre = 'z';

switch (lettre) {
    case 'a':
        System.out.println("Voyelle A");
        break;
    case 'e':
        System.out.println("Voyelle E");
        break;
    default:
        System.out.println("Autre lettre");
}
```

---

## 🔁 Compatibilité du `switch`

En Java, tu peux utiliser `switch` avec les types suivants :

| Type autorisé                  | Exemples           |
| ------------------------------ | ------------------ |
| `int`, `short`, `byte`, `char` | `switch (entier)`  |
| `String` (depuis Java 7)       | `switch (nom)`     |
| `enum`                         | `switch (couleur)` |

❌ Pas compatible avec `float`, `double`, `boolean`, ni avec des expressions complexes.

---

## 🔥 À retenir

* `switch` est pratique pour **tester des cas précis**.
* Utilise `break` pour **éviter les exécutions non désirées**.
* Le bloc `default` est **optionnel** mais utile.
* Compatible avec **`int`, `char`, `String`, `enum`**, etc.
* Plus lisible que plusieurs `else if` quand on compare **la même variable**.

---


## 2. Les structures répétitives (boucles)

Les boucles permettent de **répéter un bloc de code** tant qu’une condition est respectée.

### 2.1 La boucle while

La condition est testée avant chaque répétition.

#### Syntaxe
```java
while (condition) {
    // instructions répétées
}
```

#### Exemple
```java
int compteur = 1;

while (compteur <= 5) {
    System.out.println(compteur);
    compteur++;
}
```

### 2.2 La boucle do / while

Le bloc s’exécute au moins une fois, puis la condition est testée.

#### Syntaxe
```java
do {
    // instructions
} while (condition);
```

#### Exemple
```java
int choix;

do {
    System.out.println("Menu affiché");
    choix = 0;
} while (choix != 0);
```
### 2.3 La boucle for

Utilisée lorsque le nombre de répétitions est connu à l’avance.

#### Syntaxe
```java
for (initialisation; condition; incrémentation) {
    // instructions
}
```

#### Exemple
```java
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

### 2.4 Comparaison des boucles
| Boucle | Utilisation recommandée |
| :--- | :--- |
while |	Nombre de répétitions inconnu |
do/while |	Au moins une exécution nécessaire
for |	Nombre de répétitions connu


### 3. Les structures de contrôle du flux
### 3.1 L’instruction break

Permet de **sortir immédiatement** d’une boucle.

```java
for (int i = 1; i <= 10; i++) {
    if (i == 5) {
        break;
    }
    System.out.println(i);
}
```

### 3.2 L’instruction continue

Permet de **passer directement à l’itération suivante.**

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue;
    }
    System.out.println(i);
}
```