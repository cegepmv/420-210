+++
title = "Introduction à POO"
weight = 8
url = "/poo/"

+++

## Avant de commencer : pourquoi la POO ?

Jusqu'à présent, vous avez écrit des programmes avec des variables et des méthodes statiques. Ça marche très bien pour des programmes simples. Mais imaginez que vous deviez gérer une liste de 500 étudiants, chacun avec un nom, un numéro d'étudiant et une note.

Avec des variables séparées, ça ressemblerait à ça :

```java
String nom1 = "Alice";
int numero1 = 12345;
double note1 = 88.5;

String nom2 = "Bob";
int numero2 = 12346;
double note2 = 75.0;

String nom3 = "Charlie";
int numero3 = 12347;
double note3 = 92.0;

// ... 497 autres fois ???
```

C'est impossible à gérer. La POO existe pour **organiser le code** comme on organise les choses dans la vie réelle.

---

## 1. La grande idée : le moule et les objets

### 1.1 Une analogie concrète

Pensez à un **plan de maison**.

- Le **plan** vous montre la disposition des pièces, la taille, où est la cuisine, où est la chambre.
- À partir de ce plan, vous pouvez **construire plusieurs maisons**.
- Chaque maison a les mêmes pièces, mais la couleur des murs peut être différente, le mobilier peut changer, etc.

En POO :
- Le **plan** = la **classe**
- Chaque **maison construite** = un **objet** (on dit aussi une **instance**)

Une classe est donc un **moule**. On la définit une seule fois, puis on l'utilise pour créer autant d'objets qu'on veut.

---

## 2. Notre première classe : Animal

### 2.1 Pourquoi Animal ?

Tous les animaux ont certaines caractéristiques communes :
- Un nom
- Une espèce
- Un nombre de pattes
- Un son qu'ils font

Plutôt que de créer des variables séparées pour chaque animal, on va créer un **moule Animal**.

### 2.2 Écriture de la classe

En Java, chaque classe va dans son propre fichier. Le fichier doit avoir le même nom que la classe.

**Fichier : Animal.java**
```java
public class Animal
{
    // Ces variables appartiennent à chaque objet.
    // On les appelle des ATTRIBUTS.
    public String nom;
    public String espece;
    public int nombrePattes;
    public String son;
}
```

C'est tout ! On a juste décrit **ce qu'un animal contient**.

> **À noter :** En Java, le type chaîne de caractères s'écrit `String` avec un grand S.

### 2.3 Créer des objets à partir de la classe

Le code qui crée et utilise des objets se trouve dans une autre classe qui contient la méthode `main`.

**Fichier : Main.java**
```java
public class Main
{
    public static void main(String[] args)
    {
        // On crée un premier animal
        Animal monChien = new Animal();
        monChien.nom = "Rex";
        monChien.espece = "Chien";
        monChien.nombrePattes = 4;
        monChien.son = "Ouaf!";

        // On crée un deuxième animal avec le même moule
        Animal monChat = new Animal();
        monChat.nom = "Whiskers";
        monChat.espece = "Chat";
        monChat.nombrePattes = 4;
        monChat.son = "Miaou!";

        // Un troisième
        Animal monPoisson = new Animal();
        monPoisson.nom = "Nemo";
        monPoisson.espece = "Poisson";
        monPoisson.nombrePattes = 0;
        monPoisson.son = "...";
    }
}
```

Le mot-clé **`new`** est celui qui crée un nouvel objet.

### 2.4 Utiliser les attributs

```java
System.out.println(monChien.nom);           // Affiche: Rex
System.out.println(monChat.son);            // Affiche: Miaou!
System.out.println(monPoisson.nombrePattes); // Affiche: 0
```

Le point (**`.`**) permet d'accéder à un attribut d'un objet. On dit qu'on "accède à un membre de l'objet".

---

## 3. Les méthodes : donner des comportements à nos objets

### 3.1 Pourquoi des méthodes ?

Un animal ne fait pas qu'exister. Il **fait des choses** :
- Il peut faire un son
- On peut lui afficher ses informations

Une **méthode** est une fonction qui appartient à une classe. Elle décrit un comportement de l'objet.

### 3.2 Ajout de méthodes à la classe Animal

**Fichier : Animal.java**
```java
public class Animal
{
    public String nom;
    public String espece;
    public int nombrePattes;
    public String son;

    // Méthode qui fait parler l'animal
    public void faireSon()
    {
        System.out.println(nom + " dit: " + son);
    }

    // Méthode qui affiche les informations
    public void afficherInfo()
    {
        System.out.println("--- Informations ---");
        System.out.println("Nom: " + nom);
        System.out.println("Espece: " + espece);
        System.out.println("Nombre de pattes: " + nombrePattes);
    }
}
```

> **Convention Java :** Les noms de méthodes commencent par une minuscule : `faireSon()`, pas `FaireSon()`.

### 3.3 Appeler une méthode

**Fichier : Main.java**
```java
public class Main
{
    public static void main(String[] args)
    {
        Animal monChien = new Animal();
        monChien.nom = "Rex";
        monChien.espece = "Chien";
        monChien.nombrePattes = 4;
        monChien.son = "Ouaf!";

        monChien.faireSon();      // Affiche: Rex dit: Ouaf!
        monChien.afficherInfo();  // Affiche les infos de Rex
    }
}
```

On appelle une méthode avec le point, exactement comme on accède à un attribut, mais avec des parenthèses à la fin.

### 3.4 Méthodes avec des paramètres et retour de valeur

**Fichier : Animal.java**
```java
public class Animal
{
    public String nom;
    public String espece;
    public int nombrePattes;
    public String son;

    public void faireSon()
    {
        System.out.println(nom + " dit: " + son);
    }

    public void afficherInfo()
    {
        System.out.println("--- Informations ---");
        System.out.println("Nom: " + nom);
        System.out.println("Espece: " + espece);
        System.out.println("Nombre de pattes: " + nombrePattes);
    }

    // Méthode qui prend un paramètre
    public void faireSonNFois(int n)
    {
        for (int i = 0; i < n; i++)
        {
            System.out.println(nom + " dit: " + son);
        }
    }

    // Méthode qui retourne une valeur (boolean)
    public boolean estQuadrupede()
    {
        return nombrePattes == 4;
    }
}
```

**Fichier : Main.java**
```java
public class Main
{
    public static void main(String[] args)
    {
        Animal monChien = new Animal();
        monChien.nom = "Rex";
        monChien.nombrePattes = 4;
        monChien.son = "Ouaf!";

        monChien.faireSonNFois(3);
        // Affiche:
        // Rex dit: Ouaf!
        // Rex dit: Ouaf!
        // Rex dit: Ouaf!

        boolean quadrupede = monChien.estQuadrupede();
        System.out.println(quadrupede); // Affiche: true
    }
}
```

> **À noter :** En Java, le type booléen s'écrit `boolean` (tout en minuscules), et les valeurs sont `true` / `false`.

---

## 4. Le constructeur : initialiser un objet proprement

### 4.1 Le problème

Avec notre classe actuelle, on doit d'abord créer l'objet, puis remplir chaque attribut un par un. C'est long et on risque d'oublier un attribut.

```java
// Long et risqué
Animal monChien = new Animal();
monChien.nom = "Rex";
monChien.espece = "Chien";
monChien.nombrePattes = 4;
monChien.son = "Ouaf!";
```

### 4.2 La solution : le constructeur

Le **constructeur** est une méthode spéciale qui s'exécute automatiquement au moment où on crée un objet avec `new`. Il permet de donner les valeurs en même temps qu'on crée l'objet.

**Fichier : Animal.java**
```java
public class Animal
{
    public String nom;
    public String espece;
    public int nombrePattes;
    public String son;

    // C'est le constructeur !
    // Il a le même nom que la classe.
    // Il n'a pas de type de retour.
    public Animal(String nom, String espece, int nombrePattes, String son)
    {
        this.nom = nom;
        this.espece = espece;
        this.nombrePattes = nombrePattes;
        this.son = son;
    }

    public void faireSon()
    {
        System.out.println(nom + " dit: " + son);
    }

    public void afficherInfo()
    {
        System.out.println("--- Informations ---");
        System.out.println("Nom: " + nom);
        System.out.println("Espece: " + espece);
        System.out.println("Nombre de pattes: " + nombrePattes);
    }
}
```

### 4.3 Le mot-clé `this`

Dans le constructeur ci-dessus, vous voyez `this.nom = nom;`.

Le problème : le paramètre du constructeur s'appelle `nom`, et l'attribut de la classe s'appelle aussi `nom`. Comment distinguer les deux ?

- **`this.nom`** = l'attribut de l'objet en cours de création
- **`nom`** (sans this) = le paramètre reçu par le constructeur

```java
// this.nom    →  l'attribut de l'objet
// nom         →  la valeur passée en paramètre
this.nom = nom;
```

### 4.4 Création d'objets avec le constructeur

**Fichier : Main.java**
```java
public class Main
{
    public static void main(String[] args)
    {
        // Beaucoup plus propre !
        Animal monChien    = new Animal("Rex", "Chien", 4, "Ouaf!");
        Animal monChat     = new Animal("Whiskers", "Chat", 4, "Miaou!");
        Animal monSerpent  = new Animal("Slinky", "Serpent", 0, "Ssss!");

        monChien.faireSon();   // Rex dit: Ouaf!
        monChat.faireSon();    // Whiskers dit: Miaou!
        monSerpent.faireSon(); // Slinky dit: Ssss!
    }
}
```

---

## 5. Une classe plus réaliste : Etudiant

Appliquons tout ce qu'on a vu avec un exemple plus proche de votre vie quotidienne.

**Fichier : Etudiant.java**
```java
public class Etudiant
{
    public String nom;
    public String prenom;
    public int numeroEtudiant;
    public double[] notes;   // Tableau de notes

    public Etudiant(String nom, String prenom, int numeroEtudiant)
    {
        this.nom = nom;
        this.prenom = prenom;
        this.numeroEtudiant = numeroEtudiant;
        this.notes = new double[0]; // Pas de notes au départ
    }

    // Ajoute une note à l'étudiant
    public void ajouterNote(double note)
    {
        // On crée un nouveau tableau plus grand
        double[] nouvelles_notes = new double[notes.length + 1];

        for (int i = 0; i < notes.length; i++)
        {
            nouvelles_notes[i] = notes[i];
        }

        nouvelles_notes[notes.length] = note;
        notes = nouvelles_notes;
    }

    // Calcule la moyenne des notes
    public double calculerMoyenne()
    {
        if (notes.length == 0)
        {
            return 0.0;
        }

        double somme = 0;
        for (double note : notes)
        {
            somme += note;
        }

        return somme / notes.length;
    }

    // Affiche les informations complètes
    public void afficherInfo()
    {
        System.out.println("=== Fiche Etudiant ===");
        System.out.println("Nom: " + prenom + " " + nom);
        System.out.println("Numero: " + numeroEtudiant);
        System.out.println("Nombre de notes: " + notes.length);
        System.out.printf("Moyenne: %.2f%n", calculerMoyenne());
    }

    // Retourne si l'étudiant a réussi (moyenne >= 60)
    public boolean aReussi()
    {
        return calculerMoyenne() >= 60.0;
    }
}
```

**Fichier : Main.java**
```java
public class Main
{
    public static void main(String[] args)
    {
        Etudiant alice = new Etudiant("Dupont", "Alice", 12345);
        alice.ajouterNote(85.0);
        alice.ajouterNote(92.0);
        alice.ajouterNote(78.0);

        Etudiant bob = new Etudiant("Martin", "Bob", 12346);
        bob.ajouterNote(55.0);
        bob.ajouterNote(48.0);
        bob.ajouterNote(62.0);

        // Affichage
        alice.afficherInfo();
        // === Fiche Etudiant ===
        // Nom: Alice Dupont
        // Numero: 12345
        // Nombre de notes: 3
        // Moyenne: 85.00

        bob.afficherInfo();
        // === Fiche Etudiant ===
        // Nom: Bob Martin
        // Numero: 12346
        // Nombre de notes: 3
        // Moyenne: 55.00

        // Vérification
        System.out.println("Alice a reussi: " + alice.aReussi());  // true
        System.out.println("Bob a reussi: " + bob.aReussi());      // false
    }
}
```

> **À noter :** En Java, on utilise `notes.length` (sans parenthèses) pour obtenir la taille d'un tableau. On utilise aussi `for (double note : notes)` pour parcourir un tableau — c'est la boucle for-each en Java.

---

## 6. Plusieurs objets dans un tableau

Puisque chaque objet est une valeur comme une autre, on peut les mettre dans des tableaux.

**Fichier : Main.java**
```java
public class Main
{
    public static void main(String[] args)
    {
        // Création d'un tableau d'étudiants
        Etudiant[] etudiants = new Etudiant[3];

        etudiants[0] = new Etudiant("Dupont", "Alice", 12345);
        etudiants[0].ajouterNote(85.0);
        etudiants[0].ajouterNote(92.0);

        etudiants[1] = new Etudiant("Martin", "Bob", 12346);
        etudiants[1].ajouterNote(55.0);
        etudiants[1].ajouterNote(48.0);

        etudiants[2] = new Etudiant("Tremblay", "Charlie", 12347);
        etudiants[2].ajouterNote(70.0);
        etudiants[2].ajouterNote(75.0);

        // On peut parcourir le tableau avec une boucle for-each
        for (Etudiant e : etudiants)
        {
            System.out.printf("%s %s - Moyenne: %.2f%n", e.prenom, e.nom, e.calculerMoyenne());
        }
        // Affiche:
        // Alice Dupont - Moyenne: 88.50
        // Bob Martin - Moyenne: 51.50
        // Charlie Tremblay - Moyenne: 72.50
    }
}
```

---

## 7. Résumé des concepts

| Concept | Ce que c'est | Analogie |
|---------|-------------|----------|
| **Classe** | Un moule qui décrit un type d'objet | Le plan de maison |
| **Objet** | Une instance créée à partir d'une classe | Une maison construite |
| **Attribut** | Une variable qui appartient à un objet | La couleur des murs |
| **Méthode** | Une fonction qui appartient à une classe | Une action que peut faire la maison |
| **Constructeur** | Une méthode spéciale qui initialise l'objet | Le moment où on ameuble la maison |
| **`new`** | Le mot-clé pour créer un objet | Le moment où on commence la construction |
| **`this`** | Désigne l'objet en cours | "cette maison-ci" |
| **`.` (point)** | Permet d'accéder aux attributs/méthodes | La clé qui ouvre la maison |

### Rappel des conventions Java

| Chose | Convention | Exemple |
|-------|-----------|---------|
| Nom de classe | Commence par une majuscule | `Animal`, `Etudiant` |
| Nom de méthode | Commence par une minuscule | `faireSon()`, `calculerMoyenne()` |
| Nom d'attribut | Commence par une minuscule | `nom`, `nombrePattes` |
| Fichier | Même nom que la classe publique | `Animal.java` |
| Booléen | Tout en minuscules | `boolean`, `true`, `false` |
| Chaîne | Grand S | `String` |
| Taille d'un tableau | `.length` sans parenthèses | `notes.length` |

---

## 8. Exercices

---

### Exercice 1 — Créer une classe simple
**Niveau : ⭐ Débutant**

Créez une classe appelée `Voiture` (dans le fichier `Voiture.java`) avec les attributs suivants :
- `marque` (String)
- `modele` (String)
- `annee` (int)
- `couleur` (String)

Puis, dans votre classe `Main`, créez trois voitures différentes et affichage chacun de leurs attributs avec `System.out.println`.

Sortie attendue :
```
Voiture 1: Toyota Camry 2020, Couleur: Rouge
Voiture 2: Honda Civic 2019, Couleur: Bleu
Voiture 3: Ford Mustang 2022, Couleur: Noir
```

---

### Exercice 2 — Classe avec méthodes
**Niveau : ⭐ Débutant**

Reprenez la classe `Voiture` de l'exercice 1 et ajoutez :

1. Une méthode `afficherInfo()` qui affiche toutes les informations de la voiture sur la console.
2. Une méthode `estAncienne()` qui retourne `true` si l'année est avant 2015, `false` sinon.

Testez avec ces voitures dans `Main` :
```java
Voiture v1 = new Voiture();
v1.marque = "Toyota"; v1.modele = "Camry"; v1.annee = 2020; v1.couleur = "Rouge";

Voiture v2 = new Voiture();
v2.marque = "Ford"; v2.modele = "Model T"; v2.annee = 2010; v2.couleur = "Noir";

v1.afficherInfo();
v2.afficherInfo();
System.out.println("v1 est ancienne: " + v1.estAncienne()); // false
System.out.println("v2 est ancienne: " + v2.estAncienne()); // true
```

---

### Exercice 3 — Ajout d'un constructeur
**Niveau : ⭐⭐ Intermédiaire**

Modifiez la classe `Voiture` pour qu'elle possède un constructeur qui prend les quatre attributs en paramètres. Puis créez trois voitures en utilisant le constructeur.

La création doit ressembler à ceci :
```java
Voiture v1 = new Voiture("Toyota", "Camry", 2020, "Rouge");
```

---

### Exercice 4 — Classe CompteBancaire
**Niveau : ⭐⭐ Intermédiaire**

Créez une classe appelée `CompteBancaire` avec :

**Attributs :**
- `titulaire` (String) — le nom du propriétaire
- `solde` (double) — le montant d'argent dans le compte

**Constructeur :**
- Prend `titulaire` et un `soldeInitial` en paramètres

**Méthodes :**
- `deposer(double montant)` — ajoute de l'argent au solde. Si le montant est négatif ou zéro, afficher un message d'erreur.
- `retirer(double montant)` — retire de l'argent du solde. Si le montant dépasse le solde actuel, afficher "Fonds insuffisants". Si le montant est négatif ou zéro, afficher un message d'erreur.
- `afficherSolde()` — affiche le nom du titulaire et le solde actuel.

Testez avec ce code dans `Main` :
```java
CompteBancaire compte = new CompteBancaire("Alice", 1000.0);
compte.afficherSolde();   // Alice - Solde: 1000.00

compte.deposer(500.0);
compte.afficherSolde();   // Alice - Solde: 1500.00

compte.retirer(200.0);
compte.afficherSolde();   // Alice - Solde: 1300.00

compte.retirer(2000.0);   // Affiche: Fonds insuffisants
compte.afficherSolde();   // Alice - Solde: 1300.00 (inchangé)
```

---

### Exercice 5 — Classe avec tableau interne
**Niveau : ⭐⭐ Intermédiaire**

Créez une classe appelée `Cuisine` qui représente une cuisine avec une liste de recettes.

**Attributs :**
- `nom` (String) — le nom de la cuisine (ex: "Cuisine de Marie")
- `recettes` (String[]) — un tableau de noms de recettes

**Constructeur :**
- Prend uniquement le `nom`. Le tableau `recettes` commence vide.

**Méthodes :**
- `ajouterRecette(String recette)` — ajoute une recette au tableau (même logique que `ajouterNote` dans la classe Etudiant).
- `afficherRecettes()` — affiche le nom de la cuisine puis toutes les recettes numérotées.
- `combienDeRecettes()` — retourne le nombre de recettes (int).

Testez dans `Main` :
```java
Cuisine cuisine = new Cuisine("Cuisine de Marie");
cuisine.ajouterRecette("Pates carbonara");
cuisine.ajouterRecette("Salade Cesar");
cuisine.ajouterRecette("Soupe a l'oignon");

cuisine.afficherRecettes();
// Cuisine de Marie a 3 recette(s):
// 1. Pates carbonara
// 2. Salade Cesar
// 3. Soupe a l'oignon
```

---

### Exercice 6 — Plusieurs objets dans un tableau
**Niveau : ⭐⭐⭐ Avancé**

Utilisez la classe `CompteBancaire` de l'exercice 4. Dans votre `Main` :

1. Créez un tableau de 4 comptes bancaires avec des noms et des soldes initiaux différents.
2. Parcourez le tableau et affichage le solde de chaque compte.
3. Parcourez le tableau et trouvez **le compte avec le plus grand solde**. Affichage son nom et son solde.
4. Parcourez le tableau et calculez la **somme totale** de tous les soldes.

Sortie attendue :
```
--- Tous les comptes ---
Alice - Solde: 1500.00
Bob - Solde: 3200.00
Charlie - Solde: 750.00
Diana - Solde: 4100.00

--- Resultats ---
Plus grand solde: Diana - 4100.00
Somme totale: 9550.00
```

---

### Exercice 7 — Classe complète : Animal
**Niveau : ⭐⭐⭐ Avancé**

Reprenez la classe `Animal` du cours (celle avec le constructeur). Dans votre `Main`, créez un tableau de 5 animaux différents, puis :

1. Faites parler chaque animal avec `faireSon()`.
2. Comptez combien d'animaux sont quadrupèdes avec `estQuadrupede()`.
3. Trouvez l'animal avec le plus grand nombre de pattes.

Sortie attendue :
```
--- Tous les animaux parlent ---
Rex dit: Ouaf!
Whiskers dit: Miaou!
Slinky dit: Ssss!
Tweety dit: Piou!
Charlotte dit: ...

--- Statistiques ---
Nombre de quadrupedes: 2
Animal avec le plus de pattes: Charlotte (8 pattes)
```

---

## Solutions des exercices

> **Note pour l'étudiant :** Essayez de résoudre les exercices vous-mêmes avant de regarder les solutions ! C'est la meilleure façon d'apprendre.

---

### Solution — Exercice 1

**Fichier : Voiture.java**
```java
public class Voiture
{
    public String marque;
    public String modele;
    public int annee;
    public String couleur;
}
```

**Fichier : Main.java**
```java
public class Main
{
    public static void main(String[] args)
    {
        Voiture v1 = new Voiture();
        v1.marque = "Toyota";
        v1.modele = "Camry";
        v1.annee = 2020;
        v1.couleur = "Rouge";

        Voiture v2 = new Voiture();
        v2.marque = "Honda";
        v2.modele = "Civic";
        v2.annee = 2019;
        v2.couleur = "Bleu";

        Voiture v3 = new Voiture();
        v3.marque = "Ford";
        v3.modele = "Mustang";
        v3.annee = 2022;
        v3.couleur = "Noir";

        System.out.println("Voiture 1: " + v1.marque + " " + v1.modele + " " + v1.annee + ", Couleur: " + v1.couleur);
        System.out.println("Voiture 2: " + v2.marque + " " + v2.modele + " " + v2.annee + ", Couleur: " + v2.couleur);
        System.out.println("Voiture 3: " + v3.marque + " " + v3.modele + " " + v3.annee + ", Couleur: " + v3.couleur);
    }
}
```

---

### Solution — Exercice 2

**Fichier : Voiture.java**
```java
public class Voiture
{
    public String marque;
    public String modele;
    public int annee;
    public String couleur;

    public void afficherInfo()
    {
        System.out.println(marque + " " + modele + " " + annee + ", Couleur: " + couleur);
    }

    public boolean estAncienne()
    {
        return annee < 2015;
    }
}
```

**Fichier : Main.java**
```java
public class Main
{
    public static void main(String[] args)
    {
        Voiture v1 = new Voiture();
        v1.marque = "Toyota"; v1.modele = "Camry"; v1.annee = 2020; v1.couleur = "Rouge";

        Voiture v2 = new Voiture();
        v2.marque = "Ford"; v2.modele = "Model T"; v2.annee = 2010; v2.couleur = "Noir";

        v1.afficherInfo();
        v2.afficherInfo();
        System.out.println("v1 est ancienne: " + v1.estAncienne());
        System.out.println("v2 est ancienne: " + v2.estAncienne());
    }
}
```

---

### Solution — Exercice 3

**Fichier : Voiture.java**
```java
public class Voiture
{
    public String marque;
    public String modele;
    public int annee;
    public String couleur;

    public Voiture(String marque, String modele, int annee, String couleur)
    {
        this.marque = marque;
        this.modele = modele;
        this.annee = annee;
        this.couleur = couleur;
    }

    public void afficherInfo()
    {
        System.out.println(marque + " " + modele + " " + annee + ", Couleur: " + couleur);
    }

    public boolean estAncienne()
    {
        return annee < 2015;
    }
}
```

**Fichier : Main.java**
```java
public class Main
{
    public static void main(String[] args)
    {
        Voiture v1 = new Voiture("Toyota", "Camry", 2020, "Rouge");
        Voiture v2 = new Voiture("Honda", "Civic", 2019, "Bleu");
        Voiture v3 = new Voiture("Ford", "Mustang", 2022, "Noir");

        v1.afficherInfo();
        v2.afficherInfo();
        v3.afficherInfo();
    }
}
```

---

### Solution — Exercice 4

**Fichier : CompteBancaire.java**
```java
public class CompteBancaire
{
    public String titulaire;
    public double solde;

    public CompteBancaire(String titulaire, double soldeInitial)
    {
        this.titulaire = titulaire;
        this.solde = soldeInitial;
    }

    public void deposer(double montant)
    {
        if (montant <= 0)
        {
            System.out.println("Erreur: le montant doit etre positif");
            return;
        }

        solde += montant;
        System.out.printf("Depot de %.2f effectue%n", montant);
    }

    public void retirer(double montant)
    {
        if (montant <= 0)
        {
            System.out.println("Erreur: le montant doit etre positif");
            return;
        }

        if (montant > solde)
        {
            System.out.println("Fonds insuffisants");
            return;
        }

        solde -= montant;
        System.out.printf("Retrait de %.2f effectue%n", montant);
    }

    public void afficherSolde()
    {
        System.out.printf("%s - Solde: %.2f%n", titulaire, solde);
    }
}
```

**Fichier : Main.java**
```java
public class Main
{
    public static void main(String[] args)
    {
        CompteBancaire compte = new CompteBancaire("Alice", 1000.0);
        compte.afficherSolde();

        compte.deposer(500.0);
        compte.afficherSolde();

        compte.retirer(200.0);
        compte.afficherSolde();

        compte.retirer(2000.0);
        compte.afficherSolde();
    }
}
```

---

### Solution — Exercice 5

**Fichier : Cuisine.java**
```java
public class Cuisine
{
    public String nom;
    public String[] recettes;

    public Cuisine(String nom)
    {
        this.nom = nom;
        this.recettes = new String[0];
    }

    public void ajouterRecette(String recette)
    {
        String[] nouvelles_recettes = new String[recettes.length + 1];

        for (int i = 0; i < recettes.length; i++)
        {
            nouvelles_recettes[i] = recettes[i];
        }

        nouvelles_recettes[recettes.length] = recette;
        recettes = nouvelles_recettes;
    }

    public void afficherRecettes()
    {
        System.out.println(nom + " a " + recettes.length + " recette(s):");
        for (int i = 0; i < recettes.length; i++)
        {
            System.out.println("  " + (i + 1) + ". " + recettes[i]);
        }
    }

    public int combienDeRecettes()
    {
        return recettes.length;
    }
}
```

**Fichier : Main.java**
```java
public class Main
{
    public static void main(String[] args)
    {
        Cuisine cuisine = new Cuisine("Cuisine de Marie");
        cuisine.ajouterRecette("Pates carbonara");
        cuisine.ajouterRecette("Salade Cesar");
        cuisine.ajouterRecette("Soupe a l'oignon");

        cuisine.afficherRecettes();
        System.out.println("Nombre de recettes: " + cuisine.combienDeRecettes());
    }
}
```

---

### Solution — Exercice 6

**Fichier : Main.java**
```java
public class Main
{
    public static void main(String[] args)
    {
        CompteBancaire[] comptes = new CompteBancaire[4];
        comptes[0] = new CompteBancaire("Alice", 1500.0);
        comptes[1] = new CompteBancaire("Bob", 3200.0);
        comptes[2] = new CompteBancaire("Charlie", 750.0);
        comptes[3] = new CompteBancaire("Diana", 4100.0);

        // Afficher tous les comptes
        System.out.println("--- Tous les comptes ---");
        for (CompteBancaire compte : comptes)
        {
            compte.afficherSolde();
        }

        // Trouver le plus grand solde
        CompteBancaire plusGrand = comptes[0];
        for (CompteBancaire compte : comptes)
        {
            if (compte.solde > plusGrand.solde)
            {
                plusGrand = compte;
            }
        }

        // Calculer la somme totale
        double somme = 0;
        for (CompteBancaire compte : comptes)
        {
            somme += compte.solde;
        }

        System.out.println("\n--- Resultats ---");
        System.out.printf("Plus grand solde: %s - %.2f%n", plusGrand.titulaire, plusGrand.solde);
        System.out.printf("Somme totale: %.2f%n", somme);
    }
}
```

---

### Solution — Exercice 7

**Fichier : Main.java**
```java
public class Main
{
    public static void main(String[] args)
    {
        Animal[] animaux = new Animal[5];
        animaux[0] = new Animal("Rex", "Chien", 4, "Ouaf!");
        animaux[1] = new Animal("Whiskers", "Chat", 4, "Miaou!");
        animaux[2] = new Animal("Slinky", "Serpent", 0, "Ssss!");
        animaux[3] = new Animal("Tweety", "Oiseau", 2, "Piou!");
        animaux[4] = new Animal("Charlotte", "Araignee", 8, "...");

        // Faire parler tous les animaux
        System.out.println("--- Tous les animaux parlent ---");
        for (Animal a : animaux)
        {
            a.faireSon();
        }

        // Compter les quadrupèdes
        int compteurQuadrupedes = 0;
        for (Animal a : animaux)
        {
            if (a.estQuadrupede())
            {
                compteurQuadrupedes++;
            }
        }

        // Trouver l'animal avec le plus de pattes
        Animal plusDePattes = animaux[0];
        for (Animal a : animaux)
        {
            if (a.nombrePattes > plusDePattes.nombrePattes)
            {
                plusDePattes = a;
            }
        }

        System.out.println("\n--- Statistiques ---");
        System.out.println("Nombre de quadrupedes: " + compteurQuadrupedes);
        System.out.println("Animal avec le plus de pattes: " + plusDePattes.nom + " (" + plusDePattes.nombrePattes + " pattes)");
    }
}
```