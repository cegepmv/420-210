+++
title = "Opérateurs"
weight = 3
url = "/operateurs/"

+++


### Opérateurs Arithmétiques en Java

| Opérateur | Nom | Description | Exemple | Résultat |
| :--- | :--- | :--- | :--- | :--- |
| `+` | **Addition** | Somme de deux valeurs | `int x = 10 + 5;` | `15` |
| `-` | **Soustraction** | Différence entre deux valeurs | `int x = 20 - 8;` | `12` |
| `*` | **Multiplication** | Produit de deux valeurs | `double x = 5.5 * 2;` | `11.0` |
| `/` | **Division** | Quotient de la division | `int x = 10 / 3;` | `3` (Entier) |
| `%` | **Modulo** | Reste de la division entière | `int x = 10 % 3;` | `1` |
---

### Opérateurs d'incrémentation et de décrémentation

| Opérateur | Nom | Position | Description | Exemple | Résultat (x) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `++x` | **Pré-incrémentation** | Avant | Incrémente, puis retourne la valeur | `int y = ++x;` | Augmenté de 1 |
| `x++` | **Post-incrémentation** | Après | Retourne la valeur, puis incrémente | `int y = x++;` | Augmenté de 1 |
| `--x` | **Pré-décrémentation** | Avant | Décrémente, puis retourne la valeur | `int y = --x;` | Diminué de 1 |
| `x--` | **Post-décrémentation** | Après | Retourne la valeur, puis décrémente | `int y = x--;` | Diminué de 1 |


#### Pourquoi la position est-elle importante ?

La différence réside dans la **valeur retournée** par l'expression au moment de l'exécution :

* **Pré (`++x`) :** Mise à jour d'abord, puis utilisation immédiate.
* **Post (`x++`) :** Utilisation de la valeur actuelle, puis mise à jour juste après.


#### Exemple de comparaison :
```java
int a = 10;
int b = 10;

int resultatA = ++a; // a devient 11, puis resultatA reçoit 11
int resultatB = b++; // resultatB reçoit 10, puis b devient 11

// À la fin :
// a est 11, resultatA est 11
// b est 11, resultatB est 10

```
---

### Opérateurs Logiques en Java

Les opérateurs logiques permettent de tester plusieurs conditions à la fois et retournent toujours une valeur booléenne (`true` ou `false`).

| Opérateur | Nom | Description | Exemple |
| :--- | :--- | :--- | :--- |
| `&&` | **ET (AND)** | Retourne `true` si **toutes** les conditions sont vraies | `(age >= 18 && aPermis)` |
| `\|\|` | **OU (OR)** | Retourne `true` si **au moins une** condition est vraie | `(estSamedi \|\| estDimanche)` |
| `!` | **NON (NOT)** | Inverse la valeur logique | `!estConnecte` |
| `^` | **OU exclusif (XOR)** | Retourne `true` si **une seule** condition est vraie | `(optionA ^ optionB)` |


#### Tables de vérité (Résumé)

| A | B | A && B | A \|\| B | A ^ B | !A |
| :---: | :---: | :---: | :---: | :---: | :---: |
| `true` | `true` | `true` | `true` | `false` | `false` |
| `true` | `false` | `false` | `true` | `true` | `false` |
| `false` | `true` | `false` | `true` | `true` | `true` |
| `false` | `false` | `false` | `false` | `false` | `true` |


#### Le concept de "Court-circuit" (Short-circuit)

Les opérateurs `&&` et `||` sont dits **à court-circuit** en Java :

1. **Avec `&&` :** Si la première condition est **fausse**, la seconde n’est pas évaluée.
2. **Avec `||` :** Si la première condition est **vraie**, Java s’arrête immédiatement.

> **Astuce :** Placez toujours la condition la plus risquée ou coûteuse en deuxième position.


#### Opérateurs logiques : Court-circuit vs Évaluation complète

| Type | ET | OU | Comportement |
| :--- | :---: | :---: | :--- |
| **Court-circuit** | `&&` | `\|\|` | Évalue la 2e condition uniquement si nécessaire |
| **Évaluation complète** | `&` | `\|` | Évalue toujours les deux conditions |


#### Pourquoi utiliser l’évaluation complète (`&` et `|`) ?

Ces opérateurs sont utilisés lorsque la deuxième condition contient un **effet de bord** qui doit absolument être exécuté (incrémentation, appel de méthode, etc.).


#### Exemple de différence

```java
int compteur = 0;
boolean conditionFausse = false;

// Cas 1 : Court-circuit (&&)
if (conditionFausse && ++compteur > 0) { }
System.out.println(compteur); // Affiche 0

// Cas 2 : Évaluation complète (&)
if (conditionFausse & ++compteur > 0) { }
System.out.println(compteur); // Affiche 1
```
---

### Opérateurs de comparaison en Java

Les opérateurs de comparaison permettent de vérifier la relation entre deux expressions.  
Le résultat est toujours une valeur booléenne (`true` ou `false`).

| Opérateur | Nom | Description | Exemple | Résultat |
| :--- | :--- | :--- | :--- | :--- |
| `==` | **Égalité** | `true` si les valeurs primitives sont identiques | `5 == 5` | `true` |
| `!=` | **Inégalité** | `true` si les valeurs sont différentes | `5 != 3` | `true` |
| `>` | **Plus grand que** | `true` si la valeur de gauche est strictement supérieure | `10 > 5` | `true` |
| `<` | **Plus petit que** | `true` si la valeur de gauche est strictement inférieure | `2 < 1` | `false` |
| `>=` | **Plus grand ou égal** | `true` si la valeur de gauche est supérieure ou égale | `5 >= 5` | `true` |
| `<=` | **Plus petit ou égal** | `true` si la valeur de gauche est inférieure ou égale | `4 <= 3` | `false` |


#### Confusion entre `=` et `==`
Erreur fréquente chez les débutants :
* `=` est l’opérateur d’assignation.
* `==` est l’opérateur de comparaison.


#### Comparaison de chaînes de caractères (`String`) en Java
⚠️ En Java, l’opérateur `==` compare les **références**, pas le contenu des chaînes. Pour comparer les valeurs des chaines de caractères, il faut utiliser la fonction `equals` ou sa version ``equalsIgnoreCase`

```java
String nomUn = "Bob";
String nomDeux = "bob";

boolean sontEgaux = nomUn.equals(nomDeux); // false (sensible à la casse)
boolean sontEgauxNonSensible = nomUn.equals(nomDeux); // true (ignore les casses)
```