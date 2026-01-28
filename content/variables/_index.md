+++
title = "Variables"
weight = 2
url = "/variables/"

+++

## 🎯 Qu'est-ce qu'une variable?

Une variable, c'est comme un casier dans votre vestiaire du cégep. Vous pouvez y mettre vos affaires, les changer, les oublier (oups), et même y mettre n'importe quoi (tant que ça rentre et que c'est du bon type).

* L'identificateur (Le nom) : C'est l'étiquette sur le casier (ex: 304). C'est ce qui permet au programme de retrouver l'endroit exact en mémoire.

* La valeur (Le contenu) : C'est ce que tu déposes à l'intérieur (ton manuel de programmation, ton ordinateur).

* Le type (Le format) : C'est la taille et la configuration du casier. Un casier pour un vélo n'a pas la même forme qu'un casier pour un manteau.

Autre définition: Une **variable**, c’est comme une boîte dans laquelle on range une valeur. Elle a toujours **trois éléments essentiels** :<br>
👉 `type nom = valeur;`

Par exemple : 
```java
    int var1 = 42;
```
Ici :
* 🧾 `int` → le type de la variable (entier)
* 🏷️ `var1` → le nom de la variable
* 🎁 `42` → la valeur qu’elle contient

## Les types
En Java, les types de données sont divisés en deux grandes familles :

* 🧱 **Les types primitifs** (8 types)
* 🧩 **Les types références** (classes comme `String`, `Scanner`, etc.)

Les types **primitifs** sont les **briques de base** de tout programme Java. Ils permettent de représenter les informations simples : **nombres, caractères, booléens**.

![Types primitifs](/420-210/images/dimType.png)

### 🧮a. Les nombres entiers

Ils servent à stocker des **valeurs sans virgule**, positives ou négatives. Chaque type utilise un certain nombre d’octets et a une plage de valeurs définie :

| Type    | Taille (bits / octets) | Valeur minimale            | Valeur maximale           | Exemple           |
| ------- | ---------------------- | -------------------------- | ------------------------- | ----------------- |
| `byte`  | 8 bits (1 octet)       | -128                       | 127                       | `byte b = 10;`    |
| `short` | 16 bits (2 octets)     | -32 768                    | 32 767                    | `short s = 1000;` |
| `int`   | 32 bits (4 octets)     | -2 147 483 648             | 2 147 483 647             | `int i = 42;`     |
| `long`  | 64 bits (8 octets)     | -9 223 372 036 854 775 808 | 9 223 372 036 854 775 807 | `long l = 100L;`  |

* Il existe des **constantes** utiles comme `Integer.MAX_VALUE` ou `Long.MIN_VALUE` pour obtenir ces limites sans les retenir.

---

### 🌊 b. Les nombres à virgule (flottants)

Ils permettent de représenter des **valeurs décimales** (≈ des réels), avec une approximation en base 2.

| Type     | Taille (bits / octets) | Précision                      | Valeur min / max         | Exemple             |
| -------- | ---------------------- | ------------------------------ | ------------------------ | ------------------- |
| `float`  | 32 bits (4 octets)     | \~7 chiffres significatifs     | ±1.4×10⁻⁴⁵ → ±3.4×10³⁸   | `float f = 3.14f;`  |
| `double` | 64 bits (8 octets)     | \~15-16 chiffres significatifs | ±4.9×10⁻³²⁴ → ±1.8×10³⁰⁸ | `double d = 2.718;` |

💡 En Java, **les littéraux décimaux sont des `double` par défaut**. Pour un `float`, on ajoute un **`f`** à la fin.

---

### 🔤 c. Le caractère

Le type `char` représente **un seul caractère Unicode** (lettre, symbole, emoji, etc.) :

| Type   | Taille (bits) | Plage Unicode                | Exemple         |
| ------ | ------------- | ---------------------------- | --------------- |
| `char` | 16 bits       | 0 à 65 535 (U+0000 à U+FFFF) | `char c = 'A';` |

🎨 Les caractères sont entourés de **quotes simples** (`'A'`) et peuvent contenir aussi des caractères spéciaux ou emojis :

```java
char lettre = 'f';
```

---

### 🔘 d. Le booléen

Un `boolean` est un type logique qui représente **vrai ou faux**, souvent utilisé dans les conditions :

| Type      | Valeurs possibles | Exemple                  |
| --------- | ----------------- | ------------------------ |
| `boolean` | `true` ou `false` | `boolean actif = false;` |

💬 Très utile pour représenter des états binaires : activé/désactivé, visible/caché, connecté/non connecté...

```java
boolean estPret = true;
boolean estFini = false;
```
---

### ✨ Récap visuel

| Catégorie     | Types                          | Rôle principal                         |
| ------------- | ------------------------------ | -------------------------------------- |
| 🧮 Entiers    | `byte`, `short`, `int`, `long` | Stocker des nombres sans virgule       |
| 🌊 Flottants  | `float`, `double`              | Représenter des valeurs décimales      |
| 🔤 Caractères | `char`                         | Représenter un caractère Unicode       |
| 🔘 Booléens   | `boolean`                      | Représenter une valeur vraie ou fausse |

---


###  Les chaînes de caractères (String ) c’est quoi?
🍥 [Lien vers la classe String de l'API Java](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/lang/String.html)

En Java, une **chaîne de caractères** (ou *String*) est un objet qui représente une **séquence de caractères**.
Contrairement à certains langages où les chaînes sont simplement des tableaux de caractères (`char[]`), en Java, elles sont des **objets** de la classe `String`.

Exemple :

```java
String message = "Bonjour !";
```
---

#### Utilisation simple

Créer une chaîne :

```java
String nom = "Alice";

//Afficher une chaîne :

System.out.println(nom);
```

Connaître la longueur :

```java
int longueur = nom.length(); // renvoie 5
```

---

### Concaténation

La **concaténation** permet de **combiner plusieurs chaînes** en une seule.

### Utilisation de l’opérateur `+` :

```java
String prenom = "Alice";
String message = "Bonjour, " + prenom + " !";
System.out.println(message); // Bonjour, Alice !
```

### Concaténation avec des nombres :

```java
int age = 20;
String info = "Elle a " + age + " ans.";
System.out.println(info); // Elle a 20 ans.
```

### 1. **Méthodes Statistiques de la classe `String`**

Les méthodes **statiques** de la classe `String` ne nécessitent pas de créer une instance de `String` pour les utiliser. Vous les appelez directement sur la classe elle-même. Voici quelques exemples de méthodes statiques courantes :


#### Exemple 1 : `String.format()`
Cette méthode statique permet de formater une chaîne de caractères en utilisant des espaces réservés (placeholders).

```java
public class ExempleStringStatic {
    public static void main(String[] args) {
        String name = "Alice";
        int age = 30;
        String formattedString = String.format("Nom : %s, Âge : %d", name, age);
        System.out.println(formattedString);
    }
}
```

**Sortie attendue** :
```
Nom : Alice, Âge : 30
```
---

### 2. **Méthodes Non Statiques de la classe `String`**

Les méthodes **non-statiques** nécessitent une instance de la classe `String` pour être utilisées. Vous devez créer un objet `String` pour appeler ces méthodes. Voici quelques exemples :

#### Exemple 1 : `length()`
Cette méthode retourne la longueur (nombre de caractères) de la chaîne de caractères.

```java
public class ExempleStringNonStatic {
    public static void main(String[] args) {
        String message = "Bonjour";
        int length = message.length();  // Appel de la méthode non statique
        System.out.println("La longueur de la chaîne est : " + length);
    }
}
```

**Sortie attendue** :
```
La longueur de la chaîne est : 7
```

#### Exemple 2 : `charAt()`
Cette méthode retourne le caractère situé à une position spécifiée dans la chaîne.

```java
public class ExempleStringNonStatic {
    public static void main(String[] args) {
        String message = "Java";
        char character = message.charAt(2);  // Récupère le caractère à l'indice 2
        System.out.println("Le caractère à l'indice 2 est : " + character);
    }
}
```

**Sortie attendue** :
```
Le caractère à l'indice 2 est : v
```

#### Exemple 3 : `substring()`
Cette méthode retourne une sous-chaîne de la chaîne principale en fonction des indices donnés.

```java
public class ExempleStringNonStatic {
    public static void main(String[] args) {
        String message = "Bienvenue";
        String substring = message.substring(3, 7);  // Extrait de l'indice 3 à 6
        System.out.println("Sous-chaîne : " + substring);
    }
}
```

**Sortie attendue** :
```
Sous-chaîne : nven
```

#### Exemple 4 : `toLowerCase()` et `toUpperCase()`
Ces méthodes convertissent tous les caractères de la chaîne en minuscules ou en majuscules.

```java
public class ExempleStringNonStatic {
    public static void main(String[] args) {
        String message = "Java Programming";
        String lower = message.toLowerCase();  // Convertir en minuscules
        String upper = message.toUpperCase();  // Convertir en majuscules
        System.out.println("En minuscules : " + lower);
        System.out.println("En majuscules : " + upper);
    }
}
```

**Sortie attendue** :
```
En minuscules : java programming
En majuscules : JAVA PROGRAMMING
```

#### Exemple 5 : `contains()`
Cette méthode permet de vérifier si une chaîne contient une sous-chaîne spécifiée.

```java
public class ExempleStringNonStatic {
    public static void main(String[] args) {
        String message = "Java est génial!";
        boolean contains = message.contains("génial");  // Vérifie si "génial" est dans la chaîne
        System.out.println("La chaîne contient 'génial' ? " + contains);
    }
}
```

**Sortie attendue** :
```
La chaîne contient 'génial' ? true
```

---
<!-- 
### Méthode `concat()` :

```java
String a = "Hello";
String b = "World";
String c = a.concat(" ").concat(b);
System.out.println(c); // Hello World
```
 -->


### Résumé des différences entre les méthodes statiques et non-statiques :

- **Méthodes statiques** : 
  - Appelées sur la classe elle-même, **pas besoin d'instance**.
  - Exemples : `String.valueOf()`, `String.format()`, `String.join()`.
  
- **Méthodes non-statiques** : 
  - Appelées sur une instance de la classe `String`.
  - Exemples : `length()`, `charAt()`, `substring()`, `toLowerCase()`.

---

###   🔄 Conversion implicite vs explicite en Java

La conversion permet de changer le type d’une donnée pour l’adapter à une autre variable ou expression.


#### a. Conversion implicite (promotion automatique)

* Java effectue **automatiquement** la conversion quand il n’y a **pas de risque de perte de données**.
* Se produit souvent quand on passe d’un type **plus petit** à un type **plus grand**.

### Exemples classiques :

| De     | Vers     | Exemple         |
| ------ | -------- | --------------- |
| `int`  | `double` | `double d = 5;` |
| `byte` | `int`    | `int x = 10;`   |

```java
int a = 10;
double b = a;  // Conversion implicite
```

---

#### b. Conversion explicite (casting)

* Nécessaire quand il y a un **risque de perte de données** ou **incompatibilité**.
* Le programmeur doit forcer la conversion avec un **cast** `(type)`.

#### Exemples classiques :

| De       | Vers  | Exemple                  |
| -------- | ----- | ------------------------ |
| `double` | `int` | `int x = (int) 9.99;`    |
| `long`   | `int` | `int y = (int) 100000L;` |

```java
double x = 9.99;
int y = (int) x;  // Conversion explicite, décimale perdue
```

---

#### c. Différences clés

| Aspect                 | Conversion implicite        | Conversion explicite           |
| ---------------------- | --------------------------- | ------------------------------ |
| Nécessite une action ? | Non, automatique            | Oui, cast obligatoire `(type)` |
| Risque de perte        | Non                         | Oui                            |
| Sens                   | Du plus petit au plus grand | Du plus grand au plus petit    |
| Exemples               | `int` → `double`            | `double` → `int`               |

---

#### d. En résumé

* **Conversion implicite** = sûre, automatique, du type petit vers grand.
* **Conversion explicite** = risquée, forcée, du type grand vers petit.
* Utilise toujours le casting explicite pour éviter les erreurs de compilation.

---

#### 🧠 À retenir

* Java convertit **tout seul** quand c’est sûr.
* Pour tout ce qui peut perdre des infos, il faut **caster** manuellement.
* Sois vigilant avec les conversions explicites, elles peuvent tronquer ou modifier la valeur.




### Conversion des types

Le terme le plus utilisé pour la technique de conversion est « Casting ».


#### Cas 1

##### Conversion 1 : String vers les numériques
<img src="/420-210/images/1.png">

##### Conversion 2 : Les numériques vers une String en utilisant la méthode valueOf()
<img src="/420-210/images/2.png">

##### Conversion 3 : Les numériques vers une String en utilisant la méthode toString()
<img src="/420-210/images/3.png">

##### Conversion 4 : String vers les primitifs
<img src="/420-210/images/4.png">

##### Conversion 5 : Primitifs vers String
<img src="/420-210/images/5.png">

##### Conversion 6 : Les primitifs vers une String en utilisant la méthode valueOf()
<img src="/420-210/images/6.png">


### Automatique vs manuelle

Conversion automatique : il s’agit d’une conversion d'un type plus petit en un type plus grand

byte -> short -> char -> int -> long -> float -> double

<img src="/420-210/images/7.png">

#### Cas 2

Conversion manuelle : 

il s’agit de la conversion d'un type plus grand en un type de taille plus petite. Il suffit de rajouter le casting du type voulu à droite.

double -> float -> long -> int -> char -> short -> byte
double d = 2000.23;
float f = (float)d;
long l = (long) f;

Quand on diminue la taille il y a parfois une perte d'information comme si l'on passe de float à int:
```java
    float a = 4.53F;
    System.out.println((int) a);
        
    //4
```
### Pour résumer : 

- Dans le cas d’une conversion de petit vers grand ➔ on ne fait rien.
- Dans le cas d’une conversion d’un grand vers un petit ➔ il faut « Caster » la partie droite en type du petit.


---