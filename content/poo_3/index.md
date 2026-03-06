+++
title = "Programmation orientée objet - 3"
weight = 11
url = "/poo_3/"

+++

## Table des matières

1. [Niveaux d'accès (Modificateurs de visibilité)](#1-niveaux-daccès-modificateurs-de-visibilité)
2. [Packages et organisation du code](#2-packages-et-organisation-du-code)
3. [Méthodes et variables statiques](#3-méthodes-et-variables-statiques)
4. [Classes imbriquées (Inner classes)](#4-classes-imbriquées-inner-classes)
5. [Le mot-clé `final`](#5-le-mot-clé-final)
6. [Énumérations (enum)](#6-énumérations-enum)
7. [Gestion des exceptions](#7-gestion-des-exceptions)
8. [Composition vs Héritage](#8-composition-vs-héritage)
9. [Principes SOLID](#9-principes-solid)
10. [Collections Java](#10-collections-java)

---

## 1. Niveaux d'accès (Modificateurs de visibilité)

Java propose **4 niveaux d'accès** pour contrôler qui peut accéder à vos classes, attributs et méthodes.

### 1.1 Les quatre modificateurs

| Modificateur | Classe | Package | Sous-classe | Monde |
|--------------|--------|---------|-------------|-------|
| `public` | ✅ | ✅ | ✅ | ✅ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| *(default)* | ✅ | ✅ | ❌ | ❌ |
| `private` | ✅ | ❌ | ❌ | ❌ |

### 1.2 Explications détaillées

**`public`** : Accessible partout

```java
public class Voiture {
    public String marque;  // Accessible partout
    
    public void demarrer() {  // Accessible partout
        System.out.println("La voiture démarre");
    }
}
```

**`private`** : Accessible seulement dans la classe

```java
public class CompteBancaire {
    private double solde;  // Seulement accessible dans CompteBancaire
    
    private void validerMontant(double montant) {  // Méthode privée
        if (montant < 0) {
            throw new IllegalArgumentException("Montant invalide");
        }
    }
    
    public void deposer(double montant) {
        validerMontant(montant);  // OK, on est dans la même classe
        solde += montant;
    }
}
```

**`protected`** : Accessible dans le package ET par les sous-classes

```java
public class Animal {
    protected String espece;  // Accessible par les enfants
    
    protected void manger() {  // Accessible par les enfants
        System.out.println("L'animal mange");
    }
}

public class Chien extends Animal {
    public void faireDuBruit() {
        System.out.println(espece);  // OK, protected accessible
        manger();  // OK, méthode protected accessible
    }
}
```

**default (aucun modificateur)** : Accessible seulement dans le même package

```java
class ClasseInterne {  // Pas de 'public' = default
    String message;  // default
    
    void afficher() {  // default
        System.out.println(message);
    }
}
```

### 1.3 Bonnes pratiques

1. **Attributs** : Toujours `private` (sauf constantes `public static final`)
2. **Méthodes publiques** : L'API de votre classe
3. **Méthodes privées** : Méthodes utilitaires internes
4. **Protected** : Uniquement si vous voulez que les sous-classes y accèdent
5. **Classes** : `public` ou default (pas de `private` ou `protected` pour les classes de premier niveau)

---

## 2. Packages et organisation du code

Un **package** est un dossier qui organise vos classes de manière logique.

### 2.1 Déclaration d'un package

**Fichier : com/ecole/etudiant/Etudiant.java**

```java
package com.ecole.etudiant;  // Doit être la première ligne

public class Etudiant {
    private String nom;
    private String prenom;
    
    public Etudiant(String nom, String prenom) {
        this.nom = nom;
        this.prenom = prenom;
    }
    
    public String getNom() { return nom; }
    public String getPrenom() { return prenom; }
}
```

### 2.2 Utilisation avec `import`

**Fichier : com/ecole/main/Main.java**

```java
package com.ecole.main;

import com.ecole.etudiant.Etudiant;  // Import de la classe Etudiant

public class Main {
    public static void main(String[] args) {
        Etudiant alice = new Etudiant("Dupont", "Alice");
        System.out.println(alice.getNom());
    }
}
```

### 2.3 Import multiple et wildcard

```java
package com.ecole.main;

// Import d'une classe spécifique
import com.ecole.etudiant.Etudiant;
import com.ecole.cours.Cours;

// Import de toutes les classes d'un package
import com.ecole.professeur.*;

// Import statique pour les constantes
import static java.lang.Math.PI;
import static java.lang.Math.sqrt;

public class Main {
    public static void main(String[] args) {
        double circonference = 2 * PI * 5;  // PI sans Math.PI
        double racine = sqrt(16);  // sqrt sans Math.sqrt
    }
}
```

### 2.4 Conventions de nommage

- **Package** : tout en minuscules, souvent inversé du nom de domaine
  - `com.entreprise.projet.module`
  - `org.apache.commons.lang`
  
- **Structure typique** :
  ```
  com.monentreprise.monprojet/
  ├── model/          (classes de données)
  ├── service/        (logique métier)
  ├── controller/     (contrôleurs)
  ├── util/           (utilitaires)
  └── exception/      (exceptions personnalisées)
  ```

---

## 3. Méthodes et variables statiques

Le mot-clé `static` signifie que quelque chose appartient à la **classe** et non à une **instance**.

### 3.1 Variables statiques

Une variable statique est **partagée** par toutes les instances de la classe.

```java
public class Etudiant {
    private String nom;
    private static int compteur = 0;  // Variable de classe
    
    public Etudiant(String nom) {
        this.nom = nom;
        compteur++;  // Incrémente à chaque création
    }
    
    public static int getNombreEtudiants() {
        return compteur;
    }
}

// Utilisation
Etudiant e1 = new Etudiant("Alice");
Etudiant e2 = new Etudiant("Bob");
Etudiant e3 = new Etudiant("Charlie");

System.out.println(Etudiant.getNombreEtudiants());  // 3
```

### 3.2 Méthodes statiques

Une méthode statique peut être appelée sans créer d'objet.

```java
public class MathUtil {
    
    // Méthode statique
    public static double calculerCirconference(double rayon) {
        return 2 * Math.PI * rayon;
    }
    
    public static int max(int a, int b) {
        return (a > b) ? a : b;
    }
}

// Utilisation - SANS créer d'objet
double c = MathUtil.calculerCirconference(5.0);
int maximum = MathUtil.max(10, 20);
```

### 3.3 Constantes statiques

Par convention, les constantes sont `public static final`.

```java
public class Config {
    public static final String VERSION = "1.0.0";
    public static final int MAX_CONNEXIONS = 100;
    public static final double TAUX_TVA = 0.15;
}

// Utilisation
System.out.println("Version: " + Config.VERSION);
double prixTTC = prixHT * (1 + Config.TAUX_TVA);
```

### 3.4 Bloc statique d'initialisation

```java
public class Database {
    private static Connection connection;
    
    // Bloc statique - s'exécute une seule fois au chargement de la classe
    static {
        try {
            connection = DriverManager.getConnection("jdbc:mysql://localhost/db");
            System.out.println("Connexion établie");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### 3.5 Restrictions des méthodes statiques

⚠️ Une méthode statique **NE PEUT PAS** :
- Accéder à `this`
- Accéder aux variables d'instance (non-statiques)
- Appeler des méthodes non-statiques directement

```java
public class Exemple {
    private int x = 10;
    private static int y = 20;
    
    public static void methodeStatique() {
        // System.out.println(x);  // ERREUR ! x n'est pas statique
        System.out.println(y);     // OK, y est statique
        // this.x = 5;             // ERREUR ! pas de 'this' en statique
    }
}
```

---

## 4. Classes imbriquées (Inner classes)

Java permet de définir une classe **à l'intérieur** d'une autre classe.

### 4.1 Classe membre (non-statique)

```java
public class Universite {
    private String nom;
    
    public Universite(String nom) {
        this.nom = nom;
    }
    
    // Classe interne membre
    public class Departement {
        private String nomDept;
        
        public Departement(String nomDept) {
            this.nomDept = nomDept;
        }
        
        public void afficher() {
            // Peut accéder aux membres de la classe externe
            System.out.println("Département " + nomDept + " de " + nom);
        }
    }
}

// Utilisation
Universite udem = new Universite("UdeM");
Universite.Departement info = udem.new Departement("Informatique");
info.afficher();  // Département Informatique de UdeM
```

### 4.2 Classe statique imbriquée

```java
public class Ecole {
    private String nom;
    
    // Classe statique imbriquée
    public static class Adresse {
        private String rue;
        private String ville;
        
        public Adresse(String rue, String ville) {
            this.rue = rue;
            this.ville = ville;
        }
        
        public void afficher() {
            System.out.println(rue + ", " + ville);
            // Ne peut PAS accéder à 'nom' de Ecole
        }
    }
}

// Utilisation - pas besoin d'instance de Ecole
Ecole.Adresse adresse = new Ecole.Adresse("123 Main St", "Montreal");
adresse.afficher();
```

### 4.3 Classes locales et anonymes

**Classe locale** : définie dans une méthode

```java
public class Exemple {
    public void faireQuelqueChose() {
        // Classe locale
        class Helper {
            void aider() {
                System.out.println("J'aide !");
            }
        }
        
        Helper h = new Helper();
        h.aider();
    }
}
```

**Classe anonyme** : pour implémenter une interface à la volée

```java
public interface Salutation {
    void direBonjour();
}

public class Main {
    public static void main(String[] args) {
        // Classe anonyme
        Salutation s = new Salutation() {
            @Override
            public void direBonjour() {
                System.out.println("Bonjour !");
            }
        };
        
        s.direBonjour();
    }
}
```

---

## 5. Le mot-clé `final`

Le mot-clé `final` signifie "ne peut pas être modifié".

### 5.1 Variables finales (constantes)

```java
public class Exemple {
    private final int VALEUR_MAX = 100;  // Ne peut plus changer
    
    public void methode() {
        final double PI = 3.14159;
        // PI = 3.14;  // ERREUR ! Variable finale
    }
}
```

### 5.2 Paramètres finaux

```java
public class Calculateur {
    public double calculer(final double montant) {
        // montant = montant * 2;  // ERREUR ! Paramètre final
        return montant * 1.15;
    }
}
```

### 5.3 Méthodes finales

Une méthode `final` **ne peut pas être redéfinie** par les sous-classes.

```java
public class Animal {
    // Cette méthode ne peut PAS être @Override
    public final void respirer() {
        System.out.println("L'animal respire");
    }
}

public class Chien extends Animal {
    // @Override
    // public void respirer() {  // ERREUR ! Méthode finale
    // }
}
```

### 5.4 Classes finales

Une classe `final` **ne peut pas être héritée**.

```java
public final class String {  // Oui, String est finale !
    // ...
}

// public class MaString extends String {  // ERREUR ! Classe finale
// }
```

**Exemples de classes finales en Java** : `String`, `Integer`, `Double`, `Math`

---

## 6. Énumérations (enum)

Un `enum` est un type spécial pour représenter un ensemble fixe de constantes.

### 6.1 Enum simple

```java
public enum JourSemaine {
    LUNDI, MARDI, MERCREDI, JEUDI, VENDREDI, SAMEDI, DIMANCHE
}

// Utilisation
JourSemaine jour = JourSemaine.LUNDI;

if (jour == JourSemaine.SAMEDI || jour == JourSemaine.DIMANCHE) {
    System.out.println("C'est la fin de semaine !");
}

// Switch avec enum
switch (jour) {
    case LUNDI:
        System.out.println("Début de semaine");
        break;
    case VENDREDI:
        System.out.println("Presque la fin !");
        break;
    default:
        System.out.println("Jour normal");
}
```

### 6.2 Enum avec attributs et méthodes

```java
public enum NiveauDifficulte {
    FACILE(1, "Débutant"),
    MOYEN(2, "Intermédiaire"),
    DIFFICILE(3, "Avancé"),
    EXPERT(4, "Expert");
    
    private final int niveau;
    private final String description;
    
    // Constructeur (toujours private)
    NiveauDifficulte(int niveau, String description) {
        this.niveau = niveau;
        this.description = description;
    }
    
    public int getNiveau() {
        return niveau;
    }
    
    public String getDescription() {
        return description;
    }
}

// Utilisation
NiveauDifficulte diff = NiveauDifficulte.DIFFICILE;
System.out.println(diff.getDescription());  // Avancé
System.out.println(diff.getNiveau());       // 3
```

### 6.3 Méthodes utiles des enums

```java
// Obtenir toutes les valeurs
for (JourSemaine jour : JourSemaine.values()) {
    System.out.println(jour);
}

// Convertir une String en enum
JourSemaine jour = JourSemaine.valueOf("LUNDI");

// Nom de la constante
String nom = JourSemaine.MARDI.name();  // "MARDI"

// Position dans l'enum (commence à 0)
int position = JourSemaine.MERCREDI.ordinal();  // 2
```

---

## 7. Gestion des exceptions

Les exceptions permettent de gérer les erreurs de manière élégante.

### 7.1 Try-Catch basique

```java
public class GestionErreurs {
    public static void main(String[] args) {
        try {
            int[] tableau = {1, 2, 3};
            System.out.println(tableau[10]);  // Index invalide
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Erreur : index hors limites");
            e.printStackTrace();
        }
        
        System.out.println("Le programme continue...");
    }
}
```

### 7.2 Blocs multiples catch

```java
public void lireFichier(String chemin) {
    try {
        FileReader fichier = new FileReader(chemin);
        BufferedReader lecteur = new BufferedReader(fichier);
        String ligne = lecteur.readLine();
        int nombre = Integer.parseInt(ligne);
        
    } catch (FileNotFoundException e) {
        System.out.println("Fichier introuvable");
    } catch (IOException e) {
        System.out.println("Erreur de lecture");
    } catch (NumberFormatException e) {
        System.out.println("Format de nombre invalide");
    }
}
```

### 7.3 Finally

Le bloc `finally` s'exécute **toujours**, qu'il y ait une exception ou non.

```java
public void traiterFichier(String chemin) {
    FileReader fichier = null;
    try {
        fichier = new FileReader(chemin);
        // Traitement...
    } catch (IOException e) {
        System.out.println("Erreur : " + e.getMessage());
    } finally {
        // S'exécute TOUJOURS
        if (fichier != null) {
            try {
                fichier.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

### 7.4 Try-with-resources (Java 7+)

Ferme automatiquement les ressources.

```java
public void lireFichier(String chemin) {
    try (FileReader fichier = new FileReader(chemin);
         BufferedReader lecteur = new BufferedReader(fichier)) {
        
        String ligne = lecteur.readLine();
        System.out.println(ligne);
        
    } catch (IOException e) {
        e.printStackTrace();
    }
    // fichier et lecteur sont automatiquement fermés
}
```

### 7.5 Lancer des exceptions

```java
public class CompteBancaire {
    private double solde;
    
    public void retirer(double montant) throws Exception {
        if (montant > solde) {
            throw new Exception("Fonds insuffisants");
        }
        solde -= montant;
    }
}

// Utilisation
try {
    compte.retirer(1000.0);
} catch (Exception e) {
    System.out.println(e.getMessage());
}
```

### 7.6 Créer des exceptions personnalisées

```java
public class SoldeInsuffisantException extends Exception {
    private double soldeActuel;
    private double montantDemande;
    
    public SoldeInsuffisantException(double soldeActuel, double montantDemande) {
        super("Solde insuffisant : " + soldeActuel + " < " + montantDemande);
        this.soldeActuel = soldeActuel;
        this.montantDemande = montantDemande;
    }
    
    public double getSoldeActuel() { return soldeActuel; }
    public double getMontantDemande() { return montantDemande; }
}

// Utilisation
public void retirer(double montant) throws SoldeInsuffisantException {
    if (montant > solde) {
        throw new SoldeInsuffisantException(solde, montant);
    }
    solde -= montant;
}
```

---

## 8. Composition vs Héritage

### 8.1 Le problème avec l'héritage

L'héritage crée un **couplage fort**. Parfois, la composition est meilleure.

**Mauvais exemple avec héritage** :

```java
// Un moteur n'EST PAS une voiture !
public class Moteur {
    public void demarrer() {
        System.out.println("Moteur démarre");
    }
}

public class Voiture extends Moteur {  // ❌ Mauvaise utilisation
    // ...
}
```

### 8.2 Solution avec composition

**Bon exemple avec composition** :

```java
public class Moteur {
    private String type;
    
    public Moteur(String type) {
        this.type = type;
    }
    
    public void demarrer() {
        System.out.println("Moteur " + type + " démarre");
    }
}

public class Voiture {
    private Moteur moteur;  // Composition : voiture HAS-A moteur
    private String marque;
    
    public Voiture(String marque, String typeMoteur) {
        this.marque = marque;
        this.moteur = new Moteur(typeMoteur);
    }
    
    public void demarrer() {
        moteur.demarrer();  // Délégation
        System.out.println("Voiture " + marque + " est prête");
    }
}
```

### 8.3 Règle d'or

- **Héritage (IS-A)** : "Un Chien **EST UN** Animal" → `extends`
- **Composition (HAS-A)** : "Une Voiture **A UN** Moteur" → attribut

Privilégiez la **composition** quand c'est possible. L'héritage devrait être réservé aux vraies relations "est-un".

---

## 9. Principes SOLID

Les principes SOLID sont 5 règles de conception en POO.

### 9.1 S - Single Responsibility Principle (Responsabilité unique)

Une classe ne devrait avoir qu'**une seule raison de changer**.

**❌ Mauvais** :

```java
public class Employe {
    private String nom;
    private double salaire;
    
    // Gestion des données
    public void calculerPaie() { }
    
    // Génération de rapports (autre responsabilité !)
    public void genererRapport() { }
    
    // Sauvegarde en BD (encore une autre responsabilité !)
    public void sauvegarderEnBD() { }
}
```

**✅ Bon** :

```java
public class Employe {
    private String nom;
    private double salaire;
    
    public double calculerPaie() {
        return salaire;
    }
    // Getters/setters...
}

public class RapportEmploye {
    public void genererRapport(Employe e) {
        // ...
    }
}

public class EmployeRepository {
    public void sauvegarder(Employe e) {
        // ...
    }
}
```

### 9.2 O - Open/Closed Principle (Ouvert/Fermé)

Les classes doivent être **ouvertes à l'extension** mais **fermées à la modification**.

**❌ Mauvais** :

```java
public class CalculateurAire {
    public double calculer(Object forme) {
        if (forme instanceof Rectangle) {
            Rectangle r = (Rectangle) forme;
            return r.largeur * r.hauteur;
        } else if (forme instanceof Cercle) {
            Cercle c = (Cercle) forme;
            return Math.PI * c.rayon * c.rayon;
        }
        // Pour ajouter une forme, on doit MODIFIER cette classe !
        return 0;
    }
}
```

**✅ Bon** :

```java
public abstract class Forme {
    public abstract double calculerAire();
}

public class Rectangle extends Forme {
    private double largeur, hauteur;
    
    @Override
    public double calculerAire() {
        return largeur * hauteur;
    }
}

public class Cercle extends Forme {
    private double rayon;
    
    @Override
    public double calculerAire() {
        return Math.PI * rayon * rayon;
    }
}

// Pas besoin de modifier le code existant pour ajouter une forme
public class Triangle extends Forme {
    private double base, hauteur;
    
    @Override
    public double calculerAire() {
        return (base * hauteur) / 2;
    }
}
```

### 9.3 L - Liskov Substitution Principle

Les objets d'une classe mère doivent pouvoir être **remplacés** par des objets de classes filles sans casser le programme.

**❌ Mauvais** :

```java
public class Rectangle {
    protected int largeur, hauteur;
    
    public void setLargeur(int l) { largeur = l; }
    public void setHauteur(int h) { hauteur = h; }
    public int getAire() { return largeur * hauteur; }
}

public class Carre extends Rectangle {
    @Override
    public void setLargeur(int l) {
        largeur = hauteur = l;  // Change les deux !
    }
    
    @Override
    public void setHauteur(int h) {
        largeur = hauteur = h;  // Change les deux !
    }
}

// Problème :
Rectangle r = new Carre();
r.setLargeur(5);
r.setHauteur(10);
System.out.println(r.getAire());  // On s'attend à 50, mais on obtient 100 !
```

**✅ Bon** :

```java
public abstract class Forme {
    public abstract int getAire();
}

public class Rectangle extends Forme {
    private int largeur, hauteur;
    
    public Rectangle(int largeur, int hauteur) {
        this.largeur = largeur;
        this.hauteur = hauteur;
    }
    
    @Override
    public int getAire() { return largeur * hauteur; }
}

public class Carre extends Forme {
    private int cote;
    
    public Carre(int cote) {
        this.cote = cote;
    }
    
    @Override
    public int getAire() { return cote * cote; }
}
```

### 9.4 I - Interface Segregation Principle

Mieux vaut plusieurs **petites interfaces spécifiques** qu'une grosse interface générale.

**❌ Mauvais** :

```java
public interface Travailleur {
    void travailler();
    void manger();
    void dormir();
}

// Un robot ne mange pas et ne dort pas !
public class Robot implements Travailleur {
    @Override
    public void travailler() { /* OK */ }
    
    @Override
    public void manger() { /* ??? */ }
    
    @Override
    public void dormir() { /* ??? */ }
}
```

**✅ Bon** :

```java
public interface Travaillable {
    void travailler();
}

public interface Mangeable {
    void manger();
}

public interface Dormable {
    void dormir();
}

public class Humain implements Travaillable, Mangeable, Dormable {
    @Override public void travailler() { }
    @Override public void manger() { }
    @Override public void dormir() { }
}

public class Robot implements Travaillable {
    @Override public void travailler() { }
}
```

### 9.5 D - Dependency Inversion Principle

Les classes de haut niveau ne doivent pas dépendre des classes de bas niveau. Les deux doivent dépendre d'**abstractions**.

**❌ Mauvais** :

```java
public class MySQLDatabase {
    public void sauvegarder(String data) {
        // Sauvegarde dans MySQL
    }
}

public class UtilisateurService {
    private MySQLDatabase db = new MySQLDatabase();  // Dépendance directe !
    
    public void creerUtilisateur(String nom) {
        db.sauvegarder(nom);
    }
}

// Si on veut changer de BD, on doit modifier UtilisateurService !
```

**✅ Bon** :

```java
public interface Database {
    void sauvegarder(String data);
}

public class MySQLDatabase implements Database {
    @Override
    public void sauvegarder(String data) {
        // Sauvegarde dans MySQL
    }
}

public class PostgreSQLDatabase implements Database {
    @Override
    public void sauvegarder(String data) {
        // Sauvegarde dans PostgreSQL
    }
}

public class UtilisateurService {
    private Database db;  // Dépend d'une abstraction
    
    public UtilisateurService(Database db) {
        this.db = db;  // Injection de dépendance
    }
    
    public void creerUtilisateur(String nom) {
        db.sauvegarder(nom);
    }
}

// Utilisation
Database db = new MySQLDatabase();  // Ou PostgreSQLDatabase
UtilisateurService service = new UtilisateurService(db);
```

---

## 10. Collections Java

Les **collections** sont des structures de données qui permettent de stocker et manipuler des groupes d'objets de manière efficace. Contrairement aux tableaux, elles sont **dynamiques** (taille variable) et offrent de nombreuses méthodes utiles.

### 10.1 Hiérarchie des Collections

```
Collection (interface)
├── List (interface) - Ordre maintenu, doublons autorisés
│   ├── ArrayList - Tableau dynamique (accès rapide par index)
│   ├── LinkedList - Liste chaînée (insertion/suppression rapide)
│   └── Vector - Comme ArrayList mais synchronisé (legacy)
│
├── Set (interface) - Pas de doublons
│   ├── HashSet - Pas d'ordre garanti, très rapide
│   ├── LinkedHashSet - Ordre d'insertion maintenu
│   └── TreeSet - Ordre naturel ou personnalisé
│
└── Queue (interface) - Files (FIFO)
    ├── PriorityQueue - File avec priorités
    └── LinkedList - Implémente aussi Queue

Map (interface) - Paires clé-valeur
├── HashMap - Pas d'ordre garanti, très rapide
├── LinkedHashMap - Ordre d'insertion maintenu
└── TreeMap - Ordre naturel des clés
```

### 10.2 ArrayList - Liste dynamique

**ArrayList** est la collection la plus utilisée. C'est un tableau redimensionnable automatiquement.

#### Création et ajout

```java
import java.util.ArrayList;

public class ExempleArrayList {
    public static void main(String[] args) {
        // Création d'une ArrayList de String
        ArrayList<String> noms = new ArrayList<>();
        
        // Ajout d'éléments
        noms.add("Alice");
        noms.add("Bob");
        noms.add("Charlie");
        
        // Ajout à un index spécifique
        noms.add(1, "Diana");  // Insère Diana en position 1
        
        System.out.println(noms);  // [Alice, Diana, Bob, Charlie]
    }
}
```

#### Accès et modification

```java
ArrayList<String> noms = new ArrayList<>();
noms.add("Alice");
noms.add("Bob");
noms.add("Charlie");

// Accès par index
String premier = noms.get(0);  // "Alice"
String dernier = noms.get(noms.size() - 1);  // "Charlie"

// Modification
noms.set(1, "Bobby");  // Remplace "Bob" par "Bobby"

// Taille
int taille = noms.size();  // 3

// Vérifier si vide
boolean estVide = noms.isEmpty();  // false

// Vérifier la présence
boolean contient = noms.contains("Alice");  // true
```

#### Suppression

```java
ArrayList<String> noms = new ArrayList<>();
noms.add("Alice");
noms.add("Bob");
noms.add("Charlie");

// Supprimer par index
noms.remove(1);  // Supprime "Bob"

// Supprimer par valeur
noms.remove("Charlie");  // Supprime "Charlie"

// Vider complètement
noms.clear();  // Liste vide
```

#### Parcourir une ArrayList

```java
ArrayList<String> noms = new ArrayList<>();
noms.add("Alice");
noms.add("Bob");
noms.add("Charlie");

// Méthode 1: Boucle for classique
for (int i = 0; i < noms.size(); i++) {
    System.out.println(noms.get(i));
}

// Méthode 2: Boucle for-each (recommandé)
for (String nom : noms) {
    System.out.println(nom);
}

// Méthode 3: forEach avec lambda (Java 8+)
noms.forEach(nom -> System.out.println(nom));
```

#### ArrayList avec des objets personnalisés

```java
public class Etudiant {
    private String nom;
    private double moyenne;
    
    public Etudiant(String nom, double moyenne) {
        this.nom = nom;
        this.moyenne = moyenne;
    }
    
    public String getNom() { return nom; }
    public double getMoyenne() { return moyenne; }
    
    @Override
    public String toString() {
        return nom + " (" + moyenne + ")";
    }
}

// Utilisation
ArrayList<Etudiant> etudiants = new ArrayList<>();
etudiants.add(new Etudiant("Alice", 85.5));
etudiants.add(new Etudiant("Bob", 72.0));
etudiants.add(new Etudiant("Charlie", 91.5));

// Parcourir
for (Etudiant e : etudiants) {
    System.out.println(e.getNom() + ": " + e.getMoyenne());
}

// Trouver la meilleure moyenne
double meilleureMoyenne = 0;
Etudiant meilleur = null;
for (Etudiant e : etudiants) {
    if (e.getMoyenne() > meilleureMoyenne) {
        meilleureMoyenne = e.getMoyenne();
        meilleur = e;
    }
}
System.out.println("Meilleur: " + meilleur);
```

### 10.3 LinkedList - Liste chaînée

**LinkedList** est optimisée pour les insertions/suppressions fréquentes.

```java
import java.util.LinkedList;

public class ExempleLinkedList {
    public static void main(String[] args) {
        LinkedList<String> liste = new LinkedList<>();
        
        // Ajout au début
        liste.addFirst("Premier");
        
        // Ajout à la fin
        liste.addLast("Dernier");
        
        // Ajout normal (à la fin)
        liste.add("Milieu");
        
        System.out.println(liste);  // [Premier, Dernier, Milieu]
        
        // Récupérer et supprimer le premier
        String premier = liste.removeFirst();
        
        // Récupérer et supprimer le dernier
        String dernier = liste.removeLast();
        
        // Voir sans supprimer
        String tete = liste.peekFirst();
        String queue = liste.peekLast();
    }
}
```

**Quand utiliser LinkedList vs ArrayList ?**

| Opération | ArrayList | LinkedList |
|-----------|-----------|------------|
| Accès par index | ⚡ Très rapide | 🐌 Lent |
| Ajout à la fin | ⚡ Rapide | ⚡ Rapide |
| Ajout au début | 🐌 Lent | ⚡ Très rapide |
| Insertion au milieu | 🐌 Lent | ⚡ Rapide |
| Mémoire | Moins | Plus |

**Règle générale** : Utilisez **ArrayList** par défaut, sauf si vous faites beaucoup d'insertions/suppressions au début ou au milieu.

### 10.4 HashSet - Ensemble sans doublons

**HashSet** ne garde pas d'ordre et n'accepte **pas de doublons**.

```java
import java.util.HashSet;

public class ExempleHashSet {
    public static void main(String[] args) {
        HashSet<String> ensemble = new HashSet<>();
        
        ensemble.add("Pomme");
        ensemble.add("Banane");
        ensemble.add("Orange");
        ensemble.add("Pomme");  // Ignoré (doublon)
        
        System.out.println(ensemble);  // [Banane, Orange, Pomme] (ordre non garanti)
        System.out.println(ensemble.size());  // 3
        
        // Vérifier la présence
        boolean existe = ensemble.contains("Banane");  // true
        
        // Supprimer
        ensemble.remove("Orange");
        
        // Parcourir
        for (String fruit : ensemble) {
            System.out.println(fruit);
        }
    }
}
```

**Exemple pratique : éliminer les doublons**

```java
ArrayList<Integer> nombres = new ArrayList<>();
nombres.add(1);
nombres.add(2);
nombres.add(2);
nombres.add(3);
nombres.add(1);
nombres.add(4);

// Convertir en HashSet pour éliminer les doublons
HashSet<Integer> sansDoublons = new HashSet<>(nombres);
System.out.println(sansDoublons);  // [1, 2, 3, 4]

// Reconvertir en ArrayList si besoin
ArrayList<Integer> resultat = new ArrayList<>(sansDoublons);
```

### 10.5 TreeSet - Ensemble trié

**TreeSet** garde les éléments **triés automatiquement**.

```java
import java.util.TreeSet;

public class ExempleTreeSet {
    public static void main(String[] args) {
        TreeSet<Integer> nombres = new TreeSet<>();
        
        nombres.add(5);
        nombres.add(2);
        nombres.add(8);
        nombres.add(1);
        nombres.add(2);  // Ignoré (doublon)
        
        System.out.println(nombres);  // [1, 2, 5, 8] - Trié automatiquement !
        
        // Récupérer le premier et le dernier
        int premier = nombres.first();  // 1
        int dernier = nombres.last();   // 8
        
        // Sous-ensembles
        TreeSet<Integer> sousEnsemble = (TreeSet<Integer>) nombres.headSet(5);  // < 5
        System.out.println(sousEnsemble);  // [1, 2]
    }
}
```

**Tri d'objets personnalisés**

```java
import java.util.TreeSet;

public class Personne implements Comparable<Personne> {
    private String nom;
    private int age;
    
    public Personne(String nom, int age) {
        this.nom = nom;
        this.age = age;
    }
    
    // Définit comment comparer deux personnes
    @Override
    public int compareTo(Personne autre) {
        return Integer.compare(this.age, autre.age);  // Tri par âge
    }
    
    @Override
    public String toString() {
        return nom + " (" + age + " ans)";
    }
}

// Utilisation
TreeSet<Personne> personnes = new TreeSet<>();
personnes.add(new Personne("Alice", 25));
personnes.add(new Personne("Bob", 30));
personnes.add(new Personne("Charlie", 20));

System.out.println(personnes);
// [Charlie (20 ans), Alice (25 ans), Bob (30 ans)]
```

### 10.6 HashMap - Dictionnaire clé-valeur

**HashMap** stocke des paires **clé → valeur**. Les clés sont uniques.

```java
import java.util.HashMap;

public class ExempleHashMap {
    public static void main(String[] args) {
        // Création d'un dictionnaire String → Integer
        HashMap<String, Integer> ages = new HashMap<>();
        
        // Ajout de paires clé-valeur
        ages.put("Alice", 25);
        ages.put("Bob", 30);
        ages.put("Charlie", 22);
        
        // Récupérer une valeur
        int ageAlice = ages.get("Alice");  // 25
        
        // Vérifier la présence d'une clé
        boolean existe = ages.containsKey("Bob");  // true
        
        // Vérifier la présence d'une valeur
        boolean a30ans = ages.containsValue(30);  // true
        
        // Modifier une valeur (même clé)
        ages.put("Alice", 26);  // Remplace 25 par 26
        
        // Supprimer
        ages.remove("Charlie");
        
        // Taille
        int taille = ages.size();  // 2
        
        System.out.println(ages);  // {Alice=26, Bob=30}
    }
}
```

#### Parcourir un HashMap

```java
HashMap<String, Integer> ages = new HashMap<>();
ages.put("Alice", 25);
ages.put("Bob", 30);
ages.put("Charlie", 22);

// Méthode 1: Parcourir les clés
for (String nom : ages.keySet()) {
    System.out.println(nom + " a " + ages.get(nom) + " ans");
}

// Méthode 2: Parcourir les valeurs
for (Integer age : ages.values()) {
    System.out.println("Age: " + age);
}

// Méthode 3: Parcourir les paires clé-valeur (recommandé)
for (Map.Entry<String, Integer> entree : ages.entrySet()) {
    System.out.println(entree.getKey() + " → " + entree.getValue());
}

// Méthode 4: forEach avec lambda (Java 8+)
ages.forEach((nom, age) -> System.out.println(nom + ": " + age));
```

#### Exemple pratique : compter les occurrences

```java
String texte = "le chat et le chien jouent avec le chat";
String[] mots = texte.split(" ");

HashMap<String, Integer> compteur = new HashMap<>();

for (String mot : mots) {
    if (compteur.containsKey(mot)) {
        // Le mot existe déjà, incrémenter
        compteur.put(mot, compteur.get(mot) + 1);
    } else {
        // Nouveau mot
        compteur.put(mot, 1);
    }
}

System.out.println(compteur);
// {le=3, chat=2, et=1, chien=1, jouent=1, avec=1}

// Version courte avec getOrDefault (Java 8+)
HashMap<String, Integer> compteur2 = new HashMap<>();
for (String mot : mots) {
    compteur2.put(mot, compteur2.getOrDefault(mot, 0) + 1);
}
```

### 10.7 TreeMap - Map trié par clés

**TreeMap** maintient les clés **triées**.

```java
import java.util.TreeMap;

public class ExempleTreeMap {
    public static void main(String[] args) {
        TreeMap<String, Double> notes = new TreeMap<>();
        
        notes.put("Charlie", 85.5);
        notes.put("Alice", 92.0);
        notes.put("Bob", 78.5);
        
        System.out.println(notes);
        // {Alice=92.0, Bob=78.5, Charlie=85.5} - Trié alphabétiquement
        
        // Première et dernière clé
        String premier = notes.firstKey();  // "Alice"
        String dernier = notes.lastKey();   // "Charlie"
    }
}
```

### 10.8 Comparaison des Collections

#### Lists

| Type | Ordre | Doublons | Accès par index | Meilleur usage |
|------|-------|----------|-----------------|----------------|
| **ArrayList** | ✅ Maintenu | ✅ Autorisés | ⚡ Rapide | Usage général |
| **LinkedList** | ✅ Maintenu | ✅ Autorisés | 🐌 Lent | Insertions fréquentes |

#### Sets

| Type | Ordre | Doublons | Performance |
|------|-------|----------|-------------|
| **HashSet** | ❌ Non garanti | ❌ Interdits | ⚡ Très rapide |
| **LinkedHashSet** | ✅ Insertion | ❌ Interdits | ⚡ Rapide |
| **TreeSet** | ✅ Trié | ❌ Interdits | 🐌 Plus lent |

#### Maps

| Type | Ordre des clés | Doublons | Performance |
|------|----------------|----------|-------------|
| **HashMap** | ❌ Non garanti | ❌ Clés uniques | ⚡ Très rapide |
| **LinkedHashMap** | ✅ Insertion | ❌ Clés uniques | ⚡ Rapide |
| **TreeMap** | ✅ Trié | ❌ Clés uniques | 🐌 Plus lent |

### 10.9 Méthodes utiles communes

#### Conversion entre collections

```java
// ArrayList → HashSet
ArrayList<String> liste = new ArrayList<>();
liste.add("A");
liste.add("B");
liste.add("A");  // doublon
HashSet<String> ensemble = new HashSet<>(liste);  // {A, B}

// HashSet → ArrayList
ArrayList<String> nouvelleListe = new ArrayList<>(ensemble);

// Tableau → ArrayList
String[] tableau = {"A", "B", "C"};
ArrayList<String> liste2 = new ArrayList<>(Arrays.asList(tableau));
```

#### Tri de collections

```java
import java.util.ArrayList;
import java.util.Collections;

ArrayList<Integer> nombres = new ArrayList<>();
nombres.add(5);
nombres.add(2);
nombres.add(8);
nombres.add(1);

// Tri croissant
Collections.sort(nombres);
System.out.println(nombres);  // [1, 2, 5, 8]

// Tri décroissant
Collections.sort(nombres, Collections.reverseOrder());
System.out.println(nombres);  // [8, 5, 2, 1]

// Mélanger aléatoirement
Collections.shuffle(nombres);

// Inverser l'ordre
Collections.reverse(nombres);
```

#### Tri d'objets personnalisés

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

class Etudiant {
    String nom;
    double moyenne;
    
    Etudiant(String nom, double moyenne) {
        this.nom = nom;
        this.moyenne = moyenne;
    }
}

ArrayList<Etudiant> etudiants = new ArrayList<>();
etudiants.add(new Etudiant("Alice", 85.5));
etudiants.add(new Etudiant("Bob", 92.0));
etudiants.add(new Etudiant("Charlie", 78.5));

// Tri par moyenne (ordre croissant)
Collections.sort(etudiants, new Comparator<Etudiant>() {
    @Override
    public int compare(Etudiant e1, Etudiant e2) {
        return Double.compare(e1.moyenne, e2.moyenne);
    }
});

// Version courte avec lambda (Java 8+)
Collections.sort(etudiants, (e1, e2) -> Double.compare(e1.moyenne, e2.moyenne));

// Version encore plus courte (Java 8+)
etudiants.sort(Comparator.comparingDouble(e -> e.moyenne));

// Tri décroissant
etudiants.sort(Comparator.comparingDouble(e -> -e.moyenne));
```

### 10.10 Exercices pratiques

#### Exercice 1 : Gestion de contacts

```java
import java.util.HashMap;
import java.util.Scanner;

public class GestionContacts {
    public static void main(String[] args) {
        HashMap<String, String> contacts = new HashMap<>();
        Scanner scanner = new Scanner(System.in);
        
        while (true) {
            System.out.println("\n1. Ajouter contact");
            System.out.println("2. Chercher numero");
            System.out.println("3. Afficher tous");
            System.out.println("4. Quitter");
            System.out.print("Choix: ");
            
            int choix = scanner.nextInt();
            scanner.nextLine();  // Consommer le retour ligne
            
            if (choix == 1) {
                System.out.print("Nom: ");
                String nom = scanner.nextLine();
                System.out.print("Numero: ");
                String numero = scanner.nextLine();
                contacts.put(nom, numero);
                System.out.println("Contact ajoute !");
                
            } else if (choix == 2) {
                System.out.print("Nom: ");
                String nom = scanner.nextLine();
                if (contacts.containsKey(nom)) {
                    System.out.println(nom + ": " + contacts.get(nom));
                } else {
                    System.out.println("Contact introuvable");
                }
                
            } else if (choix == 3) {
                System.out.println("\n=== Tous les contacts ===");
                for (String nom : contacts.keySet()) {
                    System.out.println(nom + ": " + contacts.get(nom));
                }
                
            } else if (choix == 4) {
                break;
            }
        }
    }
}
```

#### Exercice 2 : Top 3 des étudiants

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

class Etudiant {
    String nom;
    double moyenne;
    
    Etudiant(String nom, double moyenne) {
        this.nom = nom;
        this.moyenne = moyenne;
    }
    
    @Override
    public String toString() {
        return nom + ": " + moyenne;
    }
}

public class Top3Etudiants {
    public static void main(String[] args) {
        ArrayList<Etudiant> etudiants = new ArrayList<>();
        etudiants.add(new Etudiant("Alice", 85.5));
        etudiants.add(new Etudiant("Bob", 92.0));
        etudiants.add(new Etudiant("Charlie", 78.5));
        etudiants.add(new Etudiant("Diana", 95.5));
        etudiants.add(new Etudiant("Eve", 88.0));
        
        // Trier par moyenne décroissante
        etudiants.sort((e1, e2) -> Double.compare(e2.moyenne, e1.moyenne));
        
        // Afficher le top 3
        System.out.println("=== Top 3 ===");
        for (int i = 0; i < 3 && i < etudiants.size(); i++) {
            System.out.println((i + 1) + ". " + etudiants.get(i));
        }
    }
}
```

#### Exercice 3 : Statistiques de texte

```java
import java.util.HashMap;
import java.util.HashSet;

public class StatistiquesTexte {
    public static void main(String[] args) {
        String texte = "le chat et le chien jouent avec le chat noir et le chien blanc";
        String[] mots = texte.toLowerCase().split(" ");
        
        // Nombre total de mots
        System.out.println("Nombre total de mots: " + mots.length);
        
        // Nombre de mots uniques
        HashSet<String> motsUniques = new HashSet<>();
        for (String mot : mots) {
            motsUniques.add(mot);
        }
        System.out.println("Mots uniques: " + motsUniques.size());
        
        // Fréquence de chaque mot
        HashMap<String, Integer> frequences = new HashMap<>();
        for (String mot : mots) {
            frequences.put(mot, frequences.getOrDefault(mot, 0) + 1);
        }
        
        System.out.println("\nFrequences:");
        for (String mot : frequences.keySet()) {
            System.out.println(mot + ": " + frequences.get(mot));
        }
        
        // Mot le plus fréquent
        String plusFrequent = "";
        int maxFreq = 0;
        for (String mot : frequences.keySet()) {
            if (frequences.get(mot) > maxFreq) {
                maxFreq = frequences.get(mot);
                plusFrequent = mot;
            }
        }
        System.out.println("\nMot le plus frequent: " + plusFrequent + " (" + maxFreq + " fois)");
    }
}
```

### 10.11 Bonnes pratiques avec les Collections

#### 1. Utiliser l'interface dans les déclarations

```java
// ❌ Moins flexible
ArrayList<String> liste = new ArrayList<>();

// ✅ Plus flexible
List<String> liste = new ArrayList<>();
// On peut facilement changer vers LinkedList si besoin
```

#### 2. Spécifier la capacité initiale si connue

```java
// Si vous savez que vous aurez environ 1000 éléments
ArrayList<String> grande = new ArrayList<>(1000);
// Évite les redimensionnements multiples
```

#### 3. Utiliser les bonnes collections pour le bon usage

```java
// Recherche rapide de présence → HashSet
HashSet<String> motsInterdits = new HashSet<>();

// Ordre d'insertion important → LinkedHashMap
LinkedHashMap<String, Integer> cache = new LinkedHashMap<>();

// Association clé-valeur → HashMap
HashMap<String, Etudiant> index = new HashMap<>();

// Pas de doublons + tri → TreeSet
TreeSet<Integer> scores = new TreeSet<>();
```

#### 4. Faire attention aux null

```java
ArrayList<String> liste = new ArrayList<>();
liste.add(null);  // Autorisé dans ArrayList

HashSet<String> ensemble = new HashSet<>();
ensemble.add(null);  // Un seul null autorisé dans HashSet

HashMap<String, Integer> map = new HashMap<>();
map.put(null, 10);  // Une seule clé null autorisée
```

---

## Résumé des notions ajoutées

| Notion | Description |
|--------|-------------|
| **Niveaux d'accès** | `public`, `private`, `protected`, default |
| **Packages** | Organisation du code avec `package` et `import` |
| **Static** | Variables et méthodes de classe |
| **Final** | Constantes, méthodes non-redéfinissables, classes non-héritables |
| **Enum** | Types énumérés pour représenter des constantes |
| **Exceptions** | Gestion des erreurs avec try-catch-finally |
| **Composition** | Alternative à l'héritage (HAS-A vs IS-A) |
| **SOLID** | 5 principes de conception POO |
| **Classes imbriquées** | Classes à l'intérieur d'autres classes |
| **Collections** | ArrayList, LinkedList, HashSet, TreeSet, HashMap, TreeMap |

---