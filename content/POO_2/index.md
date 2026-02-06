+++
title = "Programmation orientée objet - 2"
weight = 8
url = "/poo_2/"

+++
# Introduction à la POO — Partie 2
---

## Introduction

Dans la première partie du cours, vous avez appris les bases de la POO :
- Créer des classes et des objets
- Utiliser des attributs et des méthodes
- Créer des constructeurs
- Manipuler des tableaux d'objets

Maintenant, nous allons voir les **4 grands principes de la POO** :
1. **L'encapsulation** — protéger les données
2. **L'héritage** — réutiliser du code
3. **Le polymorphisme** — utiliser des objets de manière flexible
4. **L'abstraction** — définir des contrats

---

## 1. L'encapsulation : protéger vos données

### 1.1 Le problème avec `public`

Jusqu'à présent, tous nos attributs étaient `public`. Ça veut dire que n'importe qui peut les modifier :

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
}
```

Le problème :

```java
CompteBancaire compte = new CompteBancaire("Alice", 1000.0);

// Quelqu'un peut faire n'importe quoi !
compte.solde = -5000.0;  // Solde négatif ?? Impossible !
compte.solde = 999999999.0; // Fraude !
```

### 1.2 La solution : `private`

On rend les attributs **privés** avec le mot-clé `private`. Personne de l'extérieur ne peut y accéder directement.

```java
public class CompteBancaire
{
    private String titulaire;  // PRIVATE maintenant
    private double solde;      // PRIVATE maintenant
    
    public CompteBancaire(String titulaire, double soldeInitial)
    {
        this.titulaire = titulaire;
        this.solde = soldeInitial;
    }
}
```

Maintenant, ce code ne compile plus :

```java
CompteBancaire compte = new CompteBancaire("Alice", 1000.0);
compte.solde = -5000.0;  // ERREUR DE COMPILATION !
```

### 1.3 Les getters et setters

Pour accéder aux attributs privés de manière contrôlée, on crée des **méthodes publiques** :

- **Getter** : méthode qui retourne la valeur d'un attribut
- **Setter** : méthode qui modifie la valeur d'un attribut (avec validation)

```java
public class CompteBancaire
{
    private String titulaire;
    private double solde;
    
    public CompteBancaire(String titulaire, double soldeInitial)
    {
        this.titulaire = titulaire;
        this.solde = soldeInitial;
    }
    
    // GETTER pour titulaire
    public String getTitulaire()
    {
        return titulaire;
    }
    
    // GETTER pour solde
    public double getSolde()
    {
        return solde;
    }
    
    // SETTER pour solde (avec validation)
    public void setSolde(double nouveauSolde)
    {
        if (nouveauSolde < 0)
        {
            System.out.println("Erreur: le solde ne peut pas etre negatif");
            return;
        }
        solde = nouveauSolde;
    }
    
    public void deposer(double montant)
    {
        if (montant <= 0)
        {
            System.out.println("Erreur: montant invalide");
            return;
        }
        solde += montant;
    }
    
    public void retirer(double montant)
    {
        if (montant <= 0 || montant > solde)
        {
            System.out.println("Erreur: retrait impossible");
            return;
        }
        solde -= montant;
    }
    
    public void afficherSolde()
    {
        System.out.printf("%s - Solde: %.2f%n", titulaire, solde);
    }
}
```

Utilisation :

```java
CompteBancaire compte = new CompteBancaire("Alice", 1000.0);

// Accès en lecture
System.out.println(compte.getTitulaire());  // Alice
System.out.println(compte.getSolde());      // 1000.0

// Modification contrôlée
compte.setSolde(-500.0);  // Affiche une erreur, ne modifie pas
compte.deposer(500.0);    // OK, solde devient 1500.0
```

### 1.4 Pourquoi l'encapsulation ?

| Avantage | Explication |
|----------|-------------|
| **Protection** | Empêche les modifications invalides |
| **Validation** | On peut vérifier les données avant de les accepter |
| **Flexibilité** | On peut changer l'implémentation interne sans casser le code externe |
| **Contrôle** | On décide exactement ce qui est accessible de l'extérieur |

**Règle d'or :** Tous les attributs doivent être `private`. Créez des getters/setters seulement si nécessaire.

---

## 2. L'héritage : réutiliser du code

### 2.1 Le problème : code répété

Imaginez que vous devez créer plusieurs types de véhicules :

```java
public class Voiture
{
    private String marque;
    private String modele;
    private int annee;
    private int nombrePortes;
    
    // ... méthodes ...
}

public class Moto
{
    private String marque;  // Répété !
    private String modele;  // Répété !
    private int annee;      // Répété !
    private boolean aSidecar;
    
    // ... méthodes ...
}

public class Camion
{
    private String marque;  // Répété !
    private String modele;  // Répété !
    private int annee;      // Répété !
    private double chargeMaximale;
    
    // ... méthodes ...
}
```

Tous les véhicules ont une marque, un modèle et une année. On se répète !

### 2.2 La solution : l'héritage

On crée une classe **parent** (ou **superclasse**) qui contient les attributs communs.

**Fichier : Vehicule.java**
```java
public class Vehicule
{
    private String marque;
    private String modele;
    private int annee;
    
    public Vehicule(String marque, String modele, int annee)
    {
        this.marque = marque;
        this.modele = modele;
        this.annee = annee;
    }
    
    public void afficherInfo()
    {
        System.out.println(marque + " " + modele + " (" + annee + ")");
    }
    
    // Getters
    public String getMarque() { return marque; }
    public String getModele() { return modele; }
    public int getAnnee() { return annee; }
}
```

Ensuite, les classes **enfants** (ou **sous-classes**) héritent de la classe parent avec le mot-clé `extends` :

**Fichier : Voiture.java**
```java
public class Voiture extends Vehicule
{
    private int nombrePortes;
    
    public Voiture(String marque, String modele, int annee, int nombrePortes)
    {
        super(marque, modele, annee);  // Appelle le constructeur du parent
        this.nombrePortes = nombrePortes;
    }
    
    public int getNombrePortes()
    {
        return nombrePortes;
    }
}
```

**Fichier : Moto.java**
```java
public class Moto extends Vehicule
{
    private boolean aSidecar;
    
    public Moto(String marque, String modele, int annee, boolean aSidecar)
    {
        super(marque, modele, annee);
        this.aSidecar = aSidecar;
    }
    
    public boolean aSidecar()
    {
        return aSidecar;
    }
}
```

**Fichier : Camion.java**
```java
public class Camion extends Vehicule
{
    private double chargeMaximale;
    
    public Camion(String marque, String modele, int annee, double chargeMaximale)
    {
        super(marque, modele, annee);
        this.chargeMaximale = chargeMaximale;
    }
    
    public double getChargeMaximale()
    {
        return chargeMaximale;
    }
}
```

### 2.3 Le mot-clé `super`

Le mot-clé `super` permet d'appeler le constructeur de la classe parent.

```java
public Voiture(String marque, String modele, int annee, int nombrePortes)
{
    super(marque, modele, annee);  // Initialise les attributs du parent
    this.nombrePortes = nombrePortes;  // Initialise l'attribut spécifique
}
```

**Important :** L'appel à `super()` doit être la **première ligne** du constructeur de la classe enfant.

### 2.4 Utilisation

```java
public class Main
{
    public static void main(String[] args)
    {
        Voiture maVoiture = new Voiture("Toyota", "Camry", 2020, 4);
        Moto maMoto = new Moto("Harley", "Sportster", 2019, false);
        Camion monCamion = new Camion("Ford", "F-150", 2021, 1500.0);
        
        // Tous héritent de afficherInfo()
        maVoiture.afficherInfo();  // Toyota Camry (2020)
        maMoto.afficherInfo();     // Harley Sportster (2019)
        monCamion.afficherInfo();  // Ford F-150 (2021)
        
        // Chacun a ses attributs spécifiques
        System.out.println("Portes: " + maVoiture.getNombrePortes());
        System.out.println("Sidecar: " + maMoto.aSidecar());
        System.out.println("Charge max: " + monCamion.getChargeMaximale());
    }
}
```

### 2.5 Redéfinition de méthodes (Override)

Une classe enfant peut **redéfinir** une méthode du parent pour changer son comportement.

**Fichier : Camion.java (version améliorée)**
```java
public class Camion extends Vehicule
{
    private double chargeMaximale;
    
    public Camion(String marque, String modele, int annee, double chargeMaximale)
    {
        super(marque, modele, annee);
        this.chargeMaximale = chargeMaximale;
    }
    
    public double getChargeMaximale()
    {
        return chargeMaximale;
    }
    
    // REDÉFINITION de la méthode afficherInfo()
    @Override
    public void afficherInfo()
    {
        super.afficherInfo();  // Appelle la version du parent
        System.out.println("Charge maximale: " + chargeMaximale + " kg");
    }
}
```

Maintenant :

```java
Camion monCamion = new Camion("Ford", "F-150", 2021, 1500.0);
monCamion.afficherInfo();
// Affiche:
// Ford F-150 (2021)
// Charge maximale: 1500.0 kg
```

L'annotation `@Override` est optionnelle mais recommandée. Elle dit au compilateur : "Je redéfinis une méthode du parent".

---

## 3. Le polymorphisme : flexibilité maximale

### 3.1 Qu'est-ce que le polymorphisme ?

**Polymorphisme** = "plusieurs formes"

En Java, ça veut dire qu'une variable de type parent peut contenir un objet enfant.

```java
Vehicule v1 = new Voiture("Toyota", "Camry", 2020, 4);
Vehicule v2 = new Moto("Harley", "Sportster", 2019, false);
Vehicule v3 = new Camion("Ford", "F-150", 2021, 1500.0);
```

Pourquoi c'est utile ? Regardez :

```java
public class Main
{
    public static void main(String[] args)
    {
        // Un tableau qui contient différents types de véhicules
        Vehicule[] flotte = new Vehicule[3];
        flotte[0] = new Voiture("Toyota", "Camry", 2020, 4);
        flotte[1] = new Moto("Harley", "Sportster", 2019, false);
        flotte[2] = new Camion("Ford", "F-150", 2021, 1500.0);
        
        // On peut traiter tous les véhicules de la même façon
        for (Vehicule v : flotte)
        {
            v.afficherInfo();
        }
    }
}
```

Sortie :
```
Toyota Camry (2020)
Harley Sportster (2019)
Ford F-150 (2021)
Charge maximale: 1500.0 kg
```

Remarquez que même si `v` est de type `Vehicule`, quand on appelle `afficherInfo()` sur le camion, c'est la **version redéfinie** qui s'exécute !

### 3.2 Exemple concret : système de paiement

**Fichier : Employe.java**
```java
public class Employe
{
    private String nom;
    private int id;
    
    public Employe(String nom, int id)
    {
        this.nom = nom;
        this.id = id;
    }
    
    public String getNom() { return nom; }
    public int getId() { return id; }
    
    // Méthode qui sera redéfinie par les enfants
    public double calculerSalaire()
    {
        return 0.0;
    }
}
```

**Fichier : EmployeHoraire.java**
```java
public class EmployeHoraire extends Employe
{
    private double tauxHoraire;
    private int heuresTravaillees;
    
    public EmployeHoraire(String nom, int id, double tauxHoraire)
    {
        super(nom, id);
        this.tauxHoraire = tauxHoraire;
        this.heuresTravaillees = 0;
    }
    
    public void ajouterHeures(int heures)
    {
        heuresTravaillees += heures;
    }
    
    @Override
    public double calculerSalaire()
    {
        return tauxHoraire * heuresTravaillees;
    }
}
```

**Fichier : EmployeSalarie.java**
```java
public class EmployeSalarie extends Employe
{
    private double salaireAnnuel;
    
    public EmployeSalarie(String nom, int id, double salaireAnnuel)
    {
        super(nom, id);
        this.salaireAnnuel = salaireAnnuel;
    }
    
    @Override
    public double calculerSalaire()
    {
        return salaireAnnuel / 12.0;  // Salaire mensuel
    }
}
```

**Fichier : EmployeCommission.java**
```java
public class EmployeCommission extends Employe
{
    private double salaireBase;
    private double totalVentes;
    private double tauxCommission;
    
    public EmployeCommission(String nom, int id, double salaireBase, double tauxCommission)
    {
        super(nom, id);
        this.salaireBase = salaireBase;
        this.tauxCommission = tauxCommission;
        this.totalVentes = 0;
    }
    
    public void ajouterVente(double montant)
    {
        totalVentes += montant;
    }
    
    @Override
    public double calculerSalaire()
    {
        return salaireBase + (totalVentes * tauxCommission);
    }
}
```

**Utilisation — Le pouvoir du polymorphisme :**

```java
public class Main
{
    public static void main(String[] args)
    {
        // Différents types d'employés
        EmployeHoraire emp1 = new EmployeHoraire("Alice", 101, 15.50);
        emp1.ajouterHeures(160);
        
        EmployeSalarie emp2 = new EmployeSalarie("Bob", 102, 60000.0);
        
        EmployeCommission emp3 = new EmployeCommission("Charlie", 103, 2000.0, 0.05);
        emp3.ajouterVente(10000.0);
        emp3.ajouterVente(5000.0);
        
        // On peut tous les mettre dans un tableau de type Employe
        Employe[] employes = { emp1, emp2, emp3 };
        
        // Calcul de la paie pour tout le monde
        double totalPaie = 0;
        for (Employe e : employes)
        {
            double salaire = e.calculerSalaire();
            System.out.printf("%s: %.2f$%n", e.getNom(), salaire);
            totalPaie += salaire;
        }
        
        System.out.printf("Total de la paie: %.2f$%n", totalPaie);
    }
}
```

Sortie :
```
Alice: 2480.00$
Bob: 5000.00$
Charlie: 2750.00$
Total de la paie: 10230.00$
```

**Le polymorphisme nous permet de traiter des objets différents de façon uniforme !**

---

## 4. Classes abstraites : forcer un contrat

### 4.1 Le problème

Dans notre classe `Employe`, la méthode `calculerSalaire()` retourne 0.0. Ça n'a pas de sens — un employé doit avoir un calcul de salaire spécifique.

On ne veut **jamais** créer un objet `Employe` directement. On veut seulement créer des `EmployeHoraire`, `EmployeSalarie`, etc.

### 4.2 La solution : classe abstraite

On déclare la classe `Employe` comme **abstraite** avec le mot-clé `abstract` :

**Fichier : Employe.java (version abstraite)**
```java
public abstract class Employe
{
    private String nom;
    private int id;
    
    public Employe(String nom, int id)
    {
        this.nom = nom;
        this.id = id;
    }
    
    public String getNom() { return nom; }
    public int getId() { return id; }
    
    // Méthode ABSTRAITE - pas d'implémentation
    public abstract double calculerSalaire();
}
```

Maintenant :

```java
Employe e = new Employe("Test", 1);  // ERREUR DE COMPILATION !
// Cannot instantiate the type Employe
```

Mais les classes enfants fonctionnent toujours :

```java
Employe e = new EmployeHoraire("Alice", 101, 15.50);  // OK !
```

### 4.3 Méthodes abstraites

Une **méthode abstraite** :
- N'a pas de corps (pas d'implémentation)
- Se termine par un point-virgule
- **Oblige** les classes enfants à la redéfinir

```java
public abstract double calculerSalaire();  // Pas de { }
```

Si une classe enfant ne redéfinit pas la méthode abstraite, ça ne compile pas.

### 4.4 Exemple : formes géométriques

**Fichier : Forme.java**
```java
public abstract class Forme
{
    private String couleur;
    
    public Forme(String couleur)
    {
        this.couleur = couleur;
    }
    
    public String getCouleur()
    {
        return couleur;
    }
    
    // Méthodes abstraites - chaque forme calcule différemment
    public abstract double calculerAire();
    public abstract double calculerPerimetre();
}
```

**Fichier : Rectangle.java**
```java
public class Rectangle extends Forme
{
    private double largeur;
    private double hauteur;
    
    public Rectangle(String couleur, double largeur, double hauteur)
    {
        super(couleur);
        this.largeur = largeur;
        this.hauteur = hauteur;
    }
    
    @Override
    public double calculerAire()
    {
        return largeur * hauteur;
    }
    
    @Override
    public double calculerPerimetre()
    {
        return 2 * (largeur + hauteur);
    }
}
```

**Fichier : Cercle.java**
```java
public class Cercle extends Forme
{
    private double rayon;
    
    public Cercle(String couleur, double rayon)
    {
        super(couleur);
        this.rayon = rayon;
    }
    
    @Override
    public double calculerAire()
    {
        return Math.PI * rayon * rayon;
    }
    
    @Override
    public double calculerPerimetre()
    {
        return 2 * Math.PI * rayon;
    }
}
```

**Fichier : Triangle.java**
```java
public class Triangle extends Forme
{
    private double base;
    private double hauteur;
    private double cote1;
    private double cote2;
    
    public Triangle(String couleur, double base, double hauteur, double cote1, double cote2)
    {
        super(couleur);
        this.base = base;
        this.hauteur = hauteur;
        this.cote1 = cote1;
        this.cote2 = cote2;
    }
    
    @Override
    public double calculerAire()
    {
        return (base * hauteur) / 2.0;
    }
    
    @Override
    public double calculerPerimetre()
    {
        return base + cote1 + cote2;
    }
}
```

**Utilisation :**

```java
public class Main
{
    public static void main(String[] args)
    {
        Forme[] formes = new Forme[3];
        formes[0] = new Rectangle("Rouge", 5.0, 3.0);
        formes[1] = new Cercle("Bleu", 4.0);
        formes[2] = new Triangle("Vert", 6.0, 4.0, 5.0, 5.0);
        
        for (Forme f : formes)
        {
            System.out.println("Forme " + f.getCouleur());
            System.out.printf("  Aire: %.2f%n", f.calculerAire());
            System.out.printf("  Perimetre: %.2f%n", f.calculerPerimetre());
        }
    }
}
```

---

## 5. Interfaces : contrats purs

### 5.1 Qu'est-ce qu'une interface ?

Une **interface** est un contrat 100% abstrait. Elle définit **ce qu'une classe doit faire**, mais pas **comment**.

Différence avec une classe abstraite :
- Une classe ne peut hériter que d'**une seule** classe (abstraite ou non)
- Une classe peut implémenter **plusieurs** interfaces

### 5.2 Création d'une interface

**Fichier : Volant.java**
```java
public interface Volant
{
    void voler();
    void atterrir();
}
```

**Important :** 
- Les méthodes d'une interface sont automatiquement `public` et `abstract`
- On ne met pas le mot-clé `abstract`, juste la signature
- Pas de constructeur dans une interface

### 5.3 Implémentation d'une interface

On utilise le mot-clé `implements` :

**Fichier : Avion.java**
```java
public class Avion implements Volant
{
    private String modele;
    private int altitude;
    
    public Avion(String modele)
    {
        this.modele = modele;
        this.altitude = 0;
    }
    
    @Override
    public void voler()
    {
        altitude = 10000;
        System.out.println(modele + " vole a " + altitude + " metres");
    }
    
    @Override
    public void atterrir()
    {
        altitude = 0;
        System.out.println(modele + " a atterri");
    }
}
```

**Fichier : Oiseau.java**
```java
public class Oiseau implements Volant
{
    private String espece;
    private int altitude;
    
    public Oiseau(String espece)
    {
        this.espece = espece;
        this.altitude = 0;
    }
    
    @Override
    public void voler()
    {
        altitude = 100;
        System.out.println(espece + " vole a " + altitude + " metres");
    }
    
    @Override
    public void atterrir()
    {
        altitude = 0;
        System.out.println(espece + " s'est pose");
    }
}
```

**Utilisation :**

```java
public class Main
{
    public static void main(String[] args)
    {
        Volant[] volants = new Volant[2];
        volants[0] = new Avion("Boeing 747");
        volants[1] = new Oiseau("Aigle");
        
        for (Volant v : volants)
        {
            v.voler();
            v.atterrir();
        }
    }
}
```

Sortie :
```
Boeing 747 vole a 10000 metres
Boeing 747 a atterri
Aigle vole a 100 metres
Aigle s'est pose
```

### 5.4 Implémenter plusieurs interfaces

**Fichier : Nageable.java**
```java
public interface Nageable
{
    void nager();
}
```

**Fichier : Canard.java**
```java
public class Canard implements Volant, Nageable
{
    private String nom;
    
    public Canard(String nom)
    {
        this.nom = nom;
    }
    
    @Override
    public void voler()
    {
        System.out.println(nom + " vole bas au-dessus de l'eau");
    }
    
    @Override
    public void atterrir()
    {
        System.out.println(nom + " se pose sur l'eau");
    }
    
    @Override
    public void nager()
    {
        System.out.println(nom + " nage tranquillement");
    }
}
```

```java
Canard donald = new Canard("Donald");
donald.voler();
donald.atterrir();
donald.nager();
```

### 5.5 Classe abstraite vs Interface

| Critère | Classe abstraite | Interface |
|---------|------------------|-----------|
| Héritage | Une seule classe parent | Plusieurs interfaces |
| Attributs | Peut avoir des attributs | Pas d'attributs (seulement des constantes) |
| Constructeur | Peut avoir un constructeur | Pas de constructeur |
| Méthodes concrètes | Peut avoir des méthodes normales | Seulement des signatures (Java 7) |
| Quand l'utiliser ? | Relation "est un" avec code partagé | Relation "peut faire" |

**Exemple :**
- `Chien` **est un** `Animal` → classe abstraite ou héritage normal
- `Chien` **peut** `Nager` → interface `Nageable`

---

## 6. Exercices

---

### Exercice 1 — Encapsulation
**Niveau : ⭐ Débutant**

Reprenez la classe `Etudiant` de la partie 1. Modifiez-la pour :
1. Rendre tous les attributs `private`
2. Créer des getters pour tous les attributs
3. Créer un setter `setNumeroEtudiant(int numero)` qui refuse les numéros négatifs

Testez dans `Main` :
```java
Etudiant e = new Etudiant("Dupont", "Alice", 12345);
System.out.println(e.getNom());  // OK
e.setNumeroEtudiant(-100);       // Doit afficher une erreur
e.setNumeroEtudiant(99999);      // OK
```

---

### Exercice 2 — Héritage simple
**Niveau : ⭐⭐ Intermédiaire**

Créez une hiérarchie de classes pour des instruments de musique :

1. Classe parent `Instrument` avec :
   - Attributs : `nom` (String), `prix` (double)
   - Constructeur
   - Méthode `afficherInfo()`

2. Classe enfant `Guitare` qui hérite de `Instrument` avec :
   - Attribut supplémentaire : `nombreCordes` (int)
   - Constructeur qui appelle `super()`
   - Redéfinition de `afficherInfo()` pour inclure le nombre de cordes

3. Classe enfant `Piano` qui hérite de `Instrument` avec :
   - Attribut supplémentaire : `nombreTouches` (int)
   - Constructeur qui appelle `super()`
   - Redéfinition de `afficherInfo()` pour inclure le nombre de touches

Testez :
```java
Guitare g = new Guitare("Fender Stratocaster", 1200.0, 6);
Piano p = new Piano("Yamaha Grand", 15000.0, 88);

g.afficherInfo();
p.afficherInfo();
```

---

### Exercice 3 — Polymorphisme
**Niveau : ⭐⭐ Intermédiaire**

Utilisez les classes de l'exercice 2. Dans `Main` :
1. Créez un tableau de type `Instrument[]` avec 4 instruments (2 guitares, 2 pianos)
2. Parcourez le tableau et appelez `afficherInfo()` pour chaque instrument
3. Calculez le prix total de tous les instruments

---

### Exercice 4 — Classe abstraite
**Niveau : ⭐⭐⭐ Avancé**

Créez un système pour calculer l'aire de différentes formes en 3D :

1. Classe abstraite `Forme3D` avec :
   - Attribut : `nom` (String)
   - Constructeur
   - Méthode abstraite : `double calculerVolume()`
   - Méthode abstraite : `double calculerSurface()`

2. Classe `Cube` qui étend `Forme3D` :
   - Attribut : `cote` (double)
   - Implémentation des méthodes abstraites

3. Classe `Sphere` qui étend `Forme3D` :
   - Attribut : `rayon` (double)
   - Implémentation des méthodes abstraites

**Formules :**
- Cube : volume = côté³, surface = 6 × côté²
- Sphère : volume = (4/3) × π × rayon³, surface = 4 × π × rayon²

Testez dans un tableau polymorphe.

---

### Exercice 5 — Interface
**Niveau : ⭐⭐⭐ Avancé**

Créez une interface `Rechargeable` avec :
- Méthode `void recharger()`
- Méthode `int niveauBatterie()`

Créez deux classes qui implémentent cette interface :
1. `Telephone` avec attribut `batterie` (int de 0 à 100)
2. `Ordinateur` avec attribut `batterie` (int de 0 à 100)

Dans `Main`, créez un tableau de `Rechargeable[]` et rechargez tous les appareils.

---

### Exercice 6 — Projet complet
**Niveau : ⭐⭐⭐⭐ Très avancé**

Créez un système de gestion de zoo :

1. Interface `Bruyant` avec méthode `void faireDuBruit()`
2. Classe abstraite `Animal` avec :
   - Attributs : `nom`, `age`, `poids`
   - Méthode abstraite : `String getRegimeAlimentaire()`
3. Classes concrètes :
   - `Lion` extends `Animal` implements `Bruyant`
   - `Elephant` extends `Animal` implements `Bruyant`
   - `Serpent` extends `Animal` (ne fait pas de bruit)

Dans `Main` :
- Créez un tableau de 5 animaux
- Parcourez et affichez les infos de chaque animal
- Faites faire du bruit à tous les animaux bruyants (utilisez `instanceof`)

---

## Solutions des exercices

> **Note :** Essayez vraiment de faire les exercices avant de regarder les solutions !

---

### Solution — Exercice 1

**Fichier : Etudiant.java**
```java
public class Etudiant
{
    private String nom;
    private String prenom;
    private int numeroEtudiant;
    private double[] notes;
    
    public Etudiant(String nom, String prenom, int numeroEtudiant)
    {
        this.nom = nom;
        this.prenom = prenom;
        this.numeroEtudiant = numeroEtudiant;
        this.notes = new double[0];
    }
    
    // Getters
    public String getNom() { return nom; }
    public String getPrenom() { return prenom; }
    public int getNumeroEtudiant() { return numeroEtudiant; }
    public double[] getNotes() { return notes; }
    
    // Setter avec validation
    public void setNumeroEtudiant(int numero)
    {
        if (numero < 0)
        {
            System.out.println("Erreur: le numero ne peut pas etre negatif");
            return;
        }
        numeroEtudiant = numero;
    }
    
    public void ajouterNote(double note)
    {
        double[] nouvelles_notes = new double[notes.length + 1];
        for (int i = 0; i < notes.length; i++)
        {
            nouvelles_notes[i] = notes[i];
        }
        nouvelles_notes[notes.length] = note;
        notes = nouvelles_notes;
    }
    
    public double calculerMoyenne()
    {
        if (notes.length == 0) return 0.0;
        
        double somme = 0;
        for (double note : notes)
        {
            somme += note;
        }
        return somme / notes.length;
    }
}
```

---

### Solution — Exercice 2

**Fichier : Instrument.java**
```java
public class Instrument
{
    private String nom;
    private double prix;
    
    public Instrument(String nom, double prix)
    {
        this.nom = nom;
        this.prix = prix;
    }
    
    public void afficherInfo()
    {
        System.out.printf("%s - Prix: %.2f$%n", nom, prix);
    }
    
    public String getNom() { return nom; }
    public double getPrix() { return prix; }
}
```

**Fichier : Guitare.java**
```java
public class Guitare extends Instrument
{
    private int nombreCordes;
    
    public Guitare(String nom, double prix, int nombreCordes)
    {
        super(nom, prix);
        this.nombreCordes = nombreCordes;
    }
    
    @Override
    public void afficherInfo()
    {
        super.afficherInfo();
        System.out.println("  Nombre de cordes: " + nombreCordes);
    }
}
```

**Fichier : Piano.java**
```java
public class Piano extends Instrument
{
    private int nombreTouches;
    
    public Piano(String nom, double prix, int nombreTouches)
    {
        super(nom, prix);
        this.nombreTouches = nombreTouches;
    }
    
    @Override
    public void afficherInfo()
    {
        super.afficherInfo();
        System.out.println("  Nombre de touches: " + nombreTouches);
    }
}
```

---

### Solution — Exercice 3

**Fichier : Main.java**
```java
public class Main
{
    public static void main(String[] args)
    {
        Instrument[] instruments = new Instrument[4];
        instruments[0] = new Guitare("Fender Stratocaster", 1200.0, 6);
        instruments[1] = new Guitare("Gibson Les Paul", 2500.0, 6);
        instruments[2] = new Piano("Yamaha Grand", 15000.0, 88);
        instruments[3] = new Piano("Steinway", 50000.0, 88);
        
        System.out.println("=== Inventaire ===");
        double total = 0;
        for (Instrument i : instruments)
        {
            i.afficherInfo();
            total += i.getPrix();
        }
        
        System.out.printf("%nPrix total: %.2f$%n", total);
    }
}
```

---

### Solution — Exercice 4

**Fichier : Forme3D.java**
```java
public abstract class Forme3D
{
    private String nom;
    
    public Forme3D(String nom)
    {
        this.nom = nom;
    }
    
    public String getNom() { return nom; }
    
    public abstract double calculerVolume();
    public abstract double calculerSurface();
}
```

**Fichier : Cube.java**
```java
public class Cube extends Forme3D
{
    private double cote;
    
    public Cube(double cote)
    {
        super("Cube");
        this.cote = cote;
    }
    
    @Override
    public double calculerVolume()
    {
        return cote * cote * cote;
    }
    
    @Override
    public double calculerSurface()
    {
        return 6 * cote * cote;
    }
}
```

**Fichier : Sphere.java**
```java
public class Sphere extends Forme3D
{
    private double rayon;
    
    public Sphere(double rayon)
    {
        super("Sphere");
        this.rayon = rayon;
    }
    
    @Override
    public double calculerVolume()
    {
        return (4.0 / 3.0) * Math.PI * rayon * rayon * rayon;
    }
    
    @Override
    public double calculerSurface()
    {
        return 4 * Math.PI * rayon * rayon;
    }
}
```

**Fichier : Main.java**
```java
public class Main
{
    public static void main(String[] args)
    {
        Forme3D[] formes = new Forme3D[3];
        formes[0] = new Cube(5.0);
        formes[1] = new Sphere(3.0);
        formes[2] = new Cube(2.5);
        
        for (Forme3D f : formes)
        {
            System.out.println(f.getNom());
            System.out.printf("  Volume: %.2f%n", f.calculerVolume());
            System.out.printf("  Surface: %.2f%n", f.calculerSurface());
        }
    }
}
```

---

### Solution — Exercice 5

**Fichier : Rechargeable.java**
```java
public interface Rechargeable
{
    void recharger();
    int niveauBatterie();
}
```

**Fichier : Telephone.java**
```java
public class Telephone implements Rechargeable
{
    private String modele;
    private int batterie;
    
    public Telephone(String modele, int batterieInitiale)
    {
        this.modele = modele;
        this.batterie = batterieInitiale;
    }
    
    @Override
    public void recharger()
    {
        batterie = 100;
        System.out.println(modele + " recharge a 100%");
    }
    
    @Override
    public int niveauBatterie()
    {
        return batterie;
    }
    
    public String getModele() { return modele; }
}
```

**Fichier : Ordinateur.java**
```java
public class Ordinateur implements Rechargeable
{
    private String modele;
    private int batterie;
    
    public Ordinateur(String modele, int batterieInitiale)
    {
        this.modele = modele;
        this.batterie = batterieInitiale;
    }
    
    @Override
    public void recharger()
    {
        batterie = 100;
        System.out.println(modele + " recharge a 100%");
    }
    
    @Override
    public int niveauBatterie()
    {
        return batterie;
    }
    
    public String getModele() { return modele; }
}
```

**Fichier : Main.java**
```java
public class Main
{
    public static void main(String[] args)
    {
        Rechargeable[] appareils = new Rechargeable[3];
        appareils[0] = new Telephone("iPhone", 25);
        appareils[1] = new Ordinateur("MacBook", 50);
        appareils[2] = new Telephone("Samsung", 10);
        
        System.out.println("=== Avant rechargement ===");
        for (Rechargeable a : appareils)
        {
            System.out.println("Batterie: " + a.niveauBatterie() + "%");
        }
        
        System.out.println("%n=== Rechargement ===");
        for (Rechargeable a : appareils)
        {
            a.recharger();
        }
        
        System.out.println("%n=== Apres rechargement ===");
        for (Rechargeable a : appareils)
        {
            System.out.println("Batterie: " + a.niveauBatterie() + "%");
        }
    }
}
```

---

### Solution — Exercice 6

**Fichier : Bruyant.java**
```java
public interface Bruyant
{
    void faireDuBruit();
}
```

**Fichier : Animal.java**
```java
public abstract class Animal
{
    private String nom;
    private int age;
    private double poids;
    
    public Animal(String nom, int age, double poids)
    {
        this.nom = nom;
        this.age = age;
        this.poids = poids;
    }
    
    public String getNom() { return nom; }
    public int getAge() { return age; }
    public double getPoids() { return poids; }
    
    public abstract String getRegimeAlimentaire();
    
    public void afficherInfo()
    {
        System.out.printf("%s - %d ans - %.1f kg - %s%n", 
            nom, age, poids, getRegimeAlimentaire());
    }
}
```

**Fichier : Lion.java**
```java
public class Lion extends Animal implements Bruyant
{
    public Lion(String nom, int age, double poids)
    {
        super(nom, age, poids);
    }
    
    @Override
    public String getRegimeAlimentaire()
    {
        return "Carnivore";
    }
    
    @Override
    public void faireDuBruit()
    {
        System.out.println(getNom() + " rugit: ROAAAAR!");
    }
}
```

**Fichier : Elephant.java**
```java
public class Elephant extends Animal implements Bruyant
{
    public Elephant(String nom, int age, double poids)
    {
        super(nom, age, poids);
    }
    
    @Override
    public String getRegimeAlimentaire()
    {
        return "Herbivore";
    }
    
    @Override
    public void faireDuBruit()
    {
        System.out.println(getNom() + " barrit: PAAAAAW!");
    }
}
```

**Fichier : Serpent.java**
```java
public class Serpent extends Animal
{
    public Serpent(String nom, int age, double poids)
    {
        super(nom, age, poids);
    }
    
    @Override
    public String getRegimeAlimentaire()
    {
        return "Carnivore";
    }
}
```

**Fichier : Main.java**
```java
public class Main
{
    public static void main(String[] args)
    {
        Animal[] zoo = new Animal[5];
        zoo[0] = new Lion("Simba", 5, 190.0);
        zoo[1] = new Elephant("Dumbo", 10, 5000.0);
        zoo[2] = new Serpent("Kaa", 3, 15.0);
        zoo[3] = new Lion("Nala", 4, 150.0);
        zoo[4] = new Elephant("Tantor", 15, 6000.0);
        
        System.out.println("=== Animaux du zoo ===");
        for (Animal a : zoo)
        {
            a.afficherInfo();
        }
        
        System.out.println("%n=== Les animaux bruyants ===");
        for (Animal a : zoo)
        {
            if (a instanceof Bruyant)
            {
                Bruyant bruyant = (Bruyant) a;
                bruyant.faireDuBruit();
            }
        }
    }
}
```

---

## Résumé des 4 principes de la POO

| Principe | Ce que c'est | Pourquoi c'est important |
|----------|-------------|--------------------------|
| **Encapsulation** | Cacher les détails internes avec `private` | Protection des données, validation |
| **Héritage** | Réutiliser du code avec `extends` | Évite la répétition, organise le code |
| **Polymorphisme** | Traiter des objets différents de façon uniforme | Flexibilité, code générique |
| **Abstraction** | Définir des contrats avec classes abstraites et interfaces | Force une structure, garantit l'implémentation |
