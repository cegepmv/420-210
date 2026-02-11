+++
title = "Exercices - POO"
weight = 10
url = "/exos_poo/"

+++

# Exercices de Programmation Orientée Objet - Complet

Ce document contient des exercices détaillés couvrant **toutes les notions de POO** vues dans les cours, organisés par niveau de difficulté.

---

## Table des matières

### Niveau Débutant (⭐)
1. [Classes et objets basiques](#exercices-niveau-débutant-)
2. [Attributs et méthodes](#exercices-niveau-débutant-)
3. [Constructeurs](#exercices-niveau-débutant-)
4. [Getters et Setters](#exercices-niveau-débutant-)

### Niveau Intermédiaire (⭐⭐)
5. [Encapsulation](#exercices-niveau-intermédiaire-)
6. [Héritage](#exercices-niveau-intermédiaire-)
7. [Surcharge de méthodes](#exercices-niveau-intermédiaire-)
8. [Static et Final](#exercices-niveau-intermédiaire-)
9. [Collections de base](#exercices-niveau-intermédiaire-)

### Niveau Avancé (⭐⭐⭐)
10. [Polymorphisme](#exercices-niveau-avancé-)
11. [Classes abstraites](#exercices-niveau-avancé-)
12. [Interfaces](#exercices-niveau-avancé-)
13. [Exceptions](#exercices-niveau-avancé-)
14. [Collections avancées](#exercices-niveau-avancé-)
15. [Enum](#exercices-niveau-avancé-)

### Niveau Expert (⭐⭐⭐⭐)
16. [Projets intégrateurs](#exercices-niveau-expert-)
17. [Principes SOLID](#exercices-niveau-expert-)
18. [Composition vs Héritage](#exercices-niveau-expert-)

---

## Exercices Niveau Débutant ⭐

### Exercice 1.1 — Classe Livre

**Objectifs** : Classes, attributs, constructeur basique

Créez une classe `Livre` avec :
- Attributs publics : `titre` (String), `auteur` (String), `nombrePages` (int)
- Un constructeur qui initialise tous les attributs
- Une méthode `afficherInfo()` qui affiche toutes les informations du livre

**Testez** :
```java
Livre livre1 = new Livre("1984", "George Orwell", 328);
Livre livre2 = new Livre("Le Petit Prince", "Antoine de Saint-Exupéry", 96);
livre1.afficherInfo();
livre2.afficherInfo();
```

**Sortie attendue** :
```
Titre: 1984, Auteur: George Orwell, Pages: 328
Titre: Le Petit Prince, Auteur: Antoine de Saint-Exupéry, Pages: 96
```

---

### Exercice 1.2 — Classe Rectangle

**Objectifs** : Méthodes avec retour de valeur

Créez une classe `Rectangle` avec :
- Attributs publics : `largeur` (double), `hauteur` (double)
- Un constructeur
- Une méthode `calculerAire()` qui retourne l'aire (largeur × hauteur)
- Une méthode `calculerPerimetre()` qui retourne le périmètre (2 × (largeur + hauteur))
- Une méthode `estCarre()` qui retourne `true` si c'est un carré

**Testez** :
```java
Rectangle r1 = new Rectangle(5.0, 3.0);
Rectangle r2 = new Rectangle(4.0, 4.0);

System.out.println("Aire: " + r1.calculerAire());
System.out.println("Perimetre: " + r1.calculerPerimetre());
System.out.println("Est carre: " + r2.estCarre());
```

---

### Exercice 1.3 — Classe CompteBancaire Simple

**Objectifs** : Méthodes qui modifient l'état de l'objet

Créez une classe `CompteBancaire` avec :
- Attributs publics : `titulaire` (String), `solde` (double)
- Un constructeur qui prend le titulaire et le solde initial
- Une méthode `deposer(double montant)` qui ajoute au solde
- Une méthode `retirer(double montant)` qui retire du solde
- Une méthode `afficherSolde()` qui affiche le titulaire et le solde

**Testez** :
```java
CompteBancaire compte = new CompteBancaire("Alice", 1000.0);
compte.afficherSolde();
compte.deposer(500.0);
compte.retirer(200.0);
compte.afficherSolde();
```

---

### Exercice 1.4 — Classe Cercle

**Objectifs** : Utilisation de Math.PI et de méthodes mathématiques

Créez une classe `Cercle` avec :
- Attribut public : `rayon` (double)
- Un constructeur
- Une méthode `calculerAire()` qui retourne π × rayon²
- Une méthode `calculerCirconference()` qui retourne 2 × π × rayon
- Une méthode `calculerDiametre()` qui retourne 2 × rayon

**Indice** : Utilisez `Math.PI` pour π

---

### Exercice 1.5 — Classe Produit

**Objectifs** : Classes avec plusieurs méthodes

Créez une classe `Produit` avec :
- Attributs publics : `nom` (String), `prix` (double), `quantite` (int)
- Un constructeur
- Une méthode `calculerValeurStock()` qui retourne prix × quantité
- Une méthode `appliquerRemise(double pourcentage)` qui réduit le prix
- Une méthode `ajouterStock(int quantite)` qui augmente la quantité
- Une méthode `afficherInfo()`

**Testez** :
```java
Produit p = new Produit("Laptop", 1200.0, 5);
p.afficherInfo();
System.out.println("Valeur stock: " + p.calculerValeurStock());
p.appliquerRemise(10);  // 10% de réduction
p.ajouterStock(3);
p.afficherInfo();
```

---

### Exercice 1.6 — Classe Personne

**Objectifs** : Manipulation de strings et calculs d'âge

Créez une classe `Personne` avec :
- Attributs publics : `nom` (String), `prenom` (String), `anneeNaissance` (int)
- Un constructeur
- Une méthode `getNomComplet()` qui retourne "Prénom Nom"
- Une méthode `calculerAge()` qui retourne l'âge actuel (utilisez 2025 comme année actuelle)
- Une méthode `estMajeur()` qui retourne `true` si âge ≥ 18

---

### Exercice 1.7 — Classe Temperature

**Objectifs** : Conversions et calculs

Créez une classe `Temperature` avec :
- Attribut public : `celsius` (double)
- Un constructeur
- Une méthode `toFahrenheit()` qui retourne la température en Fahrenheit (F = C × 9/5 + 32)
- Une méthode `toKelvin()` qui retourne la température en Kelvin (K = C + 273.15)
- Une méthode `afficher()` qui affiche dans les 3 unités

---

### Exercice 1.8 — Tableau d'objets

**Objectifs** : Créer et manipuler un tableau d'objets

Réutilisez la classe `Livre` de l'exercice 1.1.

Dans votre `Main` :
1. Créez un tableau de 5 livres
2. Remplissez le tableau avec différents livres
3. Affichez tous les livres avec une boucle
4. Trouvez et affichez le livre avec le plus de pages
5. Calculez le nombre moyen de pages

---

## Exercices Niveau Intermédiaire ⭐⭐

### Exercice 2.1 — Encapsulation complète

**Objectifs** : Private, getters, setters avec validation

Reprenez la classe `CompteBancaire` et modifiez-la :
- Rendez **tous** les attributs `private`
- Créez des **getters** pour tous les attributs
- Créez un **setter** pour `titulaire` (ne doit pas être vide)
- Modifiez `deposer()` pour refuser les montants négatifs ou zéro
- Modifiez `retirer()` pour vérifier les fonds insuffisants
- Ajoutez une méthode `transferer(CompteBancaire destination, double montant)`

**Testez** :
```java
CompteBancaire c1 = new CompteBancaire("Alice", 1000.0);
CompteBancaire c2 = new CompteBancaire("Bob", 500.0);

c1.transferer(c2, 300.0);
c1.afficherSolde();  // 700.0
c2.afficherSolde();  // 800.0

c1.transferer(c2, 1000.0);  // Doit afficher une erreur
```

---

### Exercice 2.2 — Héritage : Véhicules

**Objectifs** : Héritage, super, redéfinition

Créez une hiérarchie de classes :

**Classe parent `Vehicule`** :
- Attributs privés : `marque`, `modele`, `annee`
- Constructeur
- Méthode `afficherInfo()`
- Méthode `calculerAge()` (retourne 2025 - annee)

**Classe enfant `Voiture`** (extends Vehicule) :
- Attribut privé supplémentaire : `nombrePortes`
- Constructeur qui appelle `super()`
- Redéfinition de `afficherInfo()` pour inclure le nombre de portes

**Classe enfant `Moto`** (extends Vehicule) :
- Attribut privé supplémentaire : `cylindree`
- Constructeur qui appelle `super()`
- Redéfinition de `afficherInfo()` pour inclure la cylindrée

**Testez** dans un tableau polymorphe :
```java
Vehicule[] flotte = new Vehicule[3];
flotte[0] = new Voiture("Toyota", "Corolla", 2020, 4);
flotte[1] = new Moto("Harley", "Sportster", 2019, 883);
flotte[2] = new Voiture("Honda", "Civic", 2022, 4);

for (Vehicule v : flotte) {
    v.afficherInfo();
    System.out.println("Age: " + v.calculerAge() + " ans\n");
}
```

---

### Exercice 2.3 — Surcharge de méthodes

**Objectifs** : Overloading de méthodes

Créez une classe `Calculatrice` avec plusieurs versions de la méthode `additionner()` :
- `additionner(int a, int b)` → retourne la somme de 2 entiers
- `additionner(int a, int b, int c)` → retourne la somme de 3 entiers
- `additionner(double a, double b)` → retourne la somme de 2 doubles
- `additionner(int[] nombres)` → retourne la somme d'un tableau d'entiers

**Testez** :
```java
Calculatrice calc = new Calculatrice();
System.out.println(calc.additionner(2, 3));
System.out.println(calc.additionner(2, 3, 4));
System.out.println(calc.additionner(2.5, 3.7));
System.out.println(calc.additionner(new int[]{1, 2, 3, 4, 5}));
```

---

### Exercice 2.4 — Surcharge de constructeurs

**Objectifs** : Chaînage de constructeurs avec this()

Créez une classe `Employe` avec :
- Attributs privés : `nom`, `prenom`, `salaire`, `departement`
- **Constructeur 1** : `Employe(String nom, String prenom, double salaire, String departement)`
- **Constructeur 2** : `Employe(String nom, String prenom, double salaire)` → appelle constructeur 1 avec "Non assigné" pour le département
- **Constructeur 3** : `Employe(String nom, String prenom)` → appelle constructeur 2 avec salaire de 30000.0
- Méthode `afficherInfo()`

**Testez les 3 constructeurs** :
```java
Employe e1 = new Employe("Dupont", "Alice", 50000.0, "IT");
Employe e2 = new Employe("Martin", "Bob", 45000.0);
Employe e3 = new Employe("Tremblay", "Charlie");

e1.afficherInfo();
e2.afficherInfo();
e3.afficherInfo();
```

---

### Exercice 2.5 — Static : Compteur d'instances

**Objectifs** : Variables et méthodes statiques

Créez une classe `Etudiant` avec :
- Attributs privés : `nom`, `numeroEtudiant`
- **Attribut static** : `compteur` (initialisé à 0)
- **Attribut static final** : `UNIVERSITE = "UdeM"`
- Constructeur qui incrémente `compteur` et assigne automatiquement un numéro (compteur actuel)
- **Méthode static** : `getNombreEtudiants()` qui retourne le compteur
- Méthode normale : `afficherInfo()`

**Testez** :
```java
System.out.println("Universite: " + Etudiant.UNIVERSITE);
System.out.println("Nombre initial: " + Etudiant.getNombreEtudiants());

Etudiant e1 = new Etudiant("Alice");
Etudiant e2 = new Etudiant("Bob");
Etudiant e3 = new Etudiant("Charlie");

System.out.println("Nombre apres creation: " + Etudiant.getNombreEtudiants());
e1.afficherInfo();
e2.afficherInfo();
```

**Sortie attendue** :
```
Universite: UdeM
Nombre initial: 0
Nombre apres creation: 3
Nom: Alice, Numero: 1
Nom: Bob, Numero: 2
```

---

### Exercice 2.6 — Final : Configuration

**Objectifs** : Constantes finales, méthodes finales

Créez une classe `Configuration` avec :
- **Constantes static final** : 
  - `VERSION = "1.0.0"`
  - `MAX_CONNEXIONS = 100`
  - `TIMEOUT_SECONDES = 30`
- Une **méthode finale** `afficherConfig()` qui affiche toutes les constantes
- Une méthode normale `validerConnexions(int nombre)` qui retourne `true` si nombre ≤ MAX_CONNEXIONS

Créez une classe `ConfigurationAvancee` qui hérite de `Configuration` et essayez (pour voir l'erreur) de redéfinir `afficherConfig()`.

---

### Exercice 2.7 — ArrayList basique

**Objectifs** : Utilisation de ArrayList

Créez un programme qui :
1. Crée une `ArrayList<String>` de prénoms
2. Ajoute 5 prénoms
3. Affiche tous les prénoms avec une boucle
4. Demande à l'utilisateur un prénom à chercher (utilisez Scanner)
5. Affiche si le prénom existe dans la liste
6. Supprime un prénom et affiche la nouvelle liste
7. Affiche la taille finale de la liste

---

### Exercice 2.8 — ArrayList d'objets

**Objectifs** : ArrayList avec objets personnalisés

Réutilisez la classe `Produit` de l'exercice 1.5.

Dans votre `Main` :
1. Créez une `ArrayList<Produit>`
2. Ajoutez 6 produits différents
3. Affichez tous les produits
4. Calculez la valeur totale du stock (somme de toutes les valeurs)
5. Trouvez le produit le plus cher
6. Trouvez tous les produits avec un prix > 50.0 et affichez-les
7. Supprimez tous les produits avec quantité = 0

---

### Exercice 2.9 — HashMap : Dictionnaire

**Objectifs** : Utilisation de HashMap

Créez un programme "dictionnaire français-anglais" avec :
1. Un `HashMap<String, String>` qui associe mots français → mots anglais
2. Ajoutez 10 paires (ex: "chat" → "cat", "chien" → "dog", etc.)
3. Demandez à l'utilisateur un mot français (Scanner)
4. Affichez la traduction si elle existe, sinon "Mot introuvable"
5. Affichez tous les mots du dictionnaire
6. Comptez combien de mots commencent par "c"

---

## Exercices Niveau Avancé ⭐⭐⭐

### Exercice 3.1 — Polymorphisme : Animaux

**Objectifs** : Polymorphisme, redéfinition, tableaux polymorphes

Créez une hiérarchie :

**Classe `Animal`** (normale, pas abstraite) :
- Attributs privés : `nom`, `age`
- Constructeur
- Méthode `faireDuBruit()` qui affiche "L'animal fait du bruit"
- Méthode `afficherInfo()`

**Classes enfants** :
- **`Chien`** : redéfinit `faireDuBruit()` pour afficher "Ouaf!"
- **`Chat`** : redéfinit `faireDuBruit()` pour afficher "Miaou!"
- **`Vache`** : redéfinit `faireDuBruit()` pour afficher "Meuh!"

Dans `Main` :
1. Créez un tableau `Animal[]` de 6 animaux (mélange de chiens, chats, vaches)
2. Parcourez le tableau et appelez `faireDuBruit()` pour chacun
3. Comptez combien il y a de chiens (utilisez `instanceof`)
4. Calculez l'âge moyen de tous les animaux

---

### Exercice 3.2 — Classe abstraite : Formes géométriques

**Objectifs** : Classes abstraites, méthodes abstraites

Créez une hiérarchie :

**Classe abstraite `Forme`** :
- Attribut protégé : `couleur`
- Constructeur
- **Méthodes abstraites** : `calculerAire()`, `calculerPerimetre()`
- Méthode normale : `afficherCouleur()`

**Classes concrètes** :
- **`Rectangle`** : attributs `largeur`, `hauteur`
- **`Cercle`** : attribut `rayon`
- **`Triangle`** : attributs `base`, `hauteur`, `cote1`, `cote2`

Dans `Main` :
1. Créez un tableau `Forme[]` avec 5 formes différentes
2. Affichez l'aire et le périmètre de chaque forme
3. Trouvez la forme avec la plus grande aire
4. Calculez l'aire totale de toutes les formes

**Formules** :
- Rectangle : aire = l×h, périmètre = 2(l+h)
- Cercle : aire = πr², périmètre = 2πr
- Triangle : aire = (b×h)/2, périmètre = b+c1+c2

---

### Exercice 3.3 — Interface : Électronique

**Objectifs** : Interfaces, implémentation multiple

Créez les interfaces :

**Interface `Rechargeable`** :
- `void recharger()`
- `int getNiveauBatterie()`
- `boolean estCharge()` (retourne true si batterie ≥ 80)

**Interface `Connecte`** :
- `void connecterWifi(String reseau)`
- `void deconnecterWifi()`
- `boolean estConnecte()`

**Classe `Smartphone`** (implements Rechargeable, Connecte) :
- Attributs privés : `marque`, `modele`, `batterie`, `reseauActuel`
- Implémentez toutes les méthodes des interfaces
- Ajoutez une méthode `utiliser(int minutes)` qui diminue la batterie de 1% par 10 minutes

**Classe `Ordinateur`** (implements Rechargeable, Connecte) :
- Même structure que Smartphone

**Classe `Montre`** (implements Rechargeable seulement) :
- Pas de connexion wifi

Dans `Main` :
1. Créez un tableau `Rechargeable[]` avec 5 appareils
2. Rechargez tous les appareils
3. Affichez lesquels sont connectés au wifi (utilisez `instanceof Connecte`)

---

### Exercice 3.4 — Exceptions : Gestion bancaire robuste

**Objectifs** : Try-catch, exceptions personnalisées

Créez une exception personnalisée :

**`SoldeInsuffisantException`** (extends Exception) :
- Attributs : `soldeActuel`, `montantDemande`
- Constructeur qui prend ces valeurs
- Message : "Solde insuffisant: {soldeActuel} < {montantDemande}"

Modifiez `CompteBancaire` :
- Méthode `retirer()` qui lance `SoldeInsuffisantException` si fonds insuffisants
- Méthode `transferer()` qui lance l'exception si transfert impossible

Dans `Main` :
```java
CompteBancaire c1 = new CompteBancaire("Alice", 1000.0);
CompteBancaire c2 = new CompteBancaire("Bob", 500.0);

try {
    c1.retirer(1500.0);
} catch (SoldeInsuffisantException e) {
    System.out.println("Erreur: " + e.getMessage());
    System.out.println("Solde actuel: " + e.getSoldeActuel());
}

try {
    c1.transferer(c2, 800.0);
    c1.transferer(c2, 500.0);  // Ceci devrait échouer
} catch (SoldeInsuffisantException e) {
    System.out.println("Transfert impossible: " + e.getMessage());
}
```

---

### Exercice 3.5 — Enum : Système de réservation

**Objectifs** : Énumérations avec attributs

Créez un enum `JourSemaine` :
- Valeurs : LUNDI, MARDI, MERCREDI, JEUDI, VENDREDI, SAMEDI, DIMANCHE
- Attributs : `numero` (1-7), `estWeekend` (boolean)
- Constructeur privé
- Méthodes : `getNumero()`, `estWeekend()`, `getJourSuivant()`

Créez une classe `Reservation` :
- Attributs : `nom`, `jour` (JourSemaine), `nombrePersonnes`
- Méthode `calculerPrix()` : 50$ par personne en semaine, 70$ par personne le weekend

Dans `Main` :
1. Créez 5 réservations pour différents jours
2. Affichez le prix total de chaque réservation
3. Calculez le revenu total
4. Affichez combien de réservations sont en weekend

---

### Exercice 3.6 — Collections : Gestion d'étudiants

**Objectifs** : ArrayList, HashMap, tri

Créez une classe `Etudiant` :
- Attributs : `nom`, `prenom`, `numeroEtudiant`, `moyenne`
- Constructeur, getters, `toString()`

Dans `Main`, créez :
1. Une `ArrayList<Etudiant>` avec 10 étudiants
2. Un `HashMap<Integer, Etudiant>` qui associe numéro → étudiant
3. Affichez les étudiants triés par moyenne (ordre décroissant)
4. Trouvez et affichez le top 3
5. Calculez la moyenne générale de la classe
6. Créez un `HashSet<String>` des noms de famille uniques
7. Affichez combien d'étudiants ont une moyenne ≥ 80

---

### Exercice 3.7 — TreeSet : Classement

**Objectifs** : TreeSet, Comparable

Créez une classe `Joueur` (implements Comparable<Joueur>) :
- Attributs : `pseudo`, `score`
- Implémentez `compareTo()` pour trier par score décroissant (score le plus élevé en premier)
- Si scores égaux, trier alphabétiquement par pseudo

Dans `Main` :
1. Créez un `TreeSet<Joueur>`
2. Ajoutez 8 joueurs avec différents scores
3. Affichez le classement (TreeSet affiche automatiquement trié)
4. Affichez le top 3
5. Ajoutez un nouveau joueur et montrez le nouveau classement

---

### Exercice 3.8 — HashMap avancé : Statistiques de texte

**Objectifs** : HashMap, analyse de données

Créez un programme qui :
1. Lit un texte long (utilisez un String avec plusieurs phrases)
2. Compte la fréquence de chaque mot (HashMap<String, Integer>)
3. Affiche les 5 mots les plus fréquents
4. Compte combien de mots différents il y a
5. Trouve le mot le plus long
6. Crée un HashMap<Integer, ArrayList<String>> qui groupe les mots par longueur

**Exemple de texte** :
```java
String texte = "le chat et le chien jouent dans le jardin le chat aime le soleil " +
               "le chien aime courir le jardin est grand et beau";
```

---

## Exercices Niveau Expert ⭐⭐⭐⭐

### Exercice 4.1 — Projet : Système de bibliothèque

**Objectifs** : Intégration de plusieurs concepts

Créez un système complet avec :

**Classe abstraite `Document`** :
- Attributs : `titre`, `auteur`, `annee`, `estEmprunte`
- Méthode abstraite : `calculerFraisRetard(int joursRetard)`
- Méthodes normales : `emprunter()`, `retourner()`

**Classes concrètes** :
- **`Livre`** : attribut `nombrePages`, frais = 0.50$ par jour
- **`DVD`** : attribut `duree`, frais = 1.00$ par jour
- **`Magazine`** : attribut `numero`, frais = 0.25$ par jour

**Classe `Membre`** :
- Attributs : `nom`, `numeroMembre`, `documentsEmpruntes` (ArrayList<Document>)
- Méthodes : `emprunterDocument()`, `retournerDocument()`, `afficherEmprunts()`

**Classe `Bibliotheque`** :
- Attributs : `nom`, `documents` (ArrayList<Document>), `membres` (HashMap<Integer, Membre>)
- Méthodes :
  - `ajouterDocument()`
  - `ajouterMembre()`
  - `rechercherDocument(String titre)`
  - `afficherDocumentsDisponibles()`
  - `genererRapport()` (nombre total de documents, nombre emprunté, etc.)

Créez un menu interactif permettant de :
1. Ajouter un document
2. Ajouter un membre
3. Emprunter un document
4. Retourner un document
5. Afficher tous les documents
6. Afficher les emprunts d'un membre
7. Générer un rapport
8. Quitter

---

### Exercice 4.2 — Projet : Système de commande en ligne

**Objectifs** : POO complète, collections avancées

**Interface `Livrable`** :
- `double calculerFraisLivraison()`
- `int estimerDelaiLivraison()`

**Classe `Produit`** :
- Attributs : `nom`, `prix`, `poids`, `categorie`

**Classe `Panier`** :
- HashMap<Produit, Integer> pour stocker produit → quantité
- Méthodes : `ajouter()`, `retirer()`, `calculerTotal()`, `vider()`

**Classe `Commande`** (implements Livrable) :
- Attributs : `numero`, `client`, `panier`, `adresse`, `statut` (enum)
- Méthode `calculerFraisLivraison()` basée sur le poids total
- Méthode `appliquerCodePromo(String code)` (HashMap des codes promo)

**Enum `StatutCommande`** :
- EN_PREPARATION, EXPEDIEE, EN_LIVRAISON, LIVREE, ANNULEE

**Classe `Client`** :
- Attributs : `nom`, `email`, `adresse`, `historiqueCommandes` (ArrayList)
- Méthodes : `passerCommande()`, `afficherHistorique()`, `calculerTotalDepense()`

Implémentez un système complet avec menu permettant de :
- Créer un compte client
- Ajouter des produits au panier
- Passer une commande
- Voir l'historique des commandes
- Calculer les statistiques (total dépensé, commandes par statut, etc.)

---

### Exercice 4.3 — SOLID : Refactoring

**Objectifs** : Appliquer les principes SOLID

Voici du **mauvais code** qui viole plusieurs principes SOLID :

```java
public class Employee {
    private String name;
    private double salary;
    private String type; // "manager", "developer", "designer"
    
    public double calculatePay() {
        if (type.equals("manager")) {
            return salary * 1.5;
        } else if (type.equals("developer")) {
            return salary * 1.2;
        } else {
            return salary;
        }
    }
    
    public void saveToDatabase() {
        // Code SQL pour sauvegarder
        System.out.println("INSERT INTO employees...");
    }
    
    public void generateReport() {
        // Génère un rapport
        System.out.println("=== Employee Report ===");
        System.out.println("Name: " + name);
        System.out.println("Salary: " + salary);
    }
}
```

**Votre mission** :
1. Identifiez quels principes SOLID sont violés
2. Refactorisez le code pour respecter les principes SOLID :
   - **S** : Séparez les responsabilités
   - **O** : Rendez extensible sans modification
   - **L** : Assurez la substituabilité
   - **I** : Créez des interfaces spécifiques
   - **D** : Inversez les dépendances

**Créez** :
- Une classe abstraite ou interface pour les employés
- Des classes séparées pour Manager, Developer, Designer
- Une classe séparée pour la sauvegarde (EmployeeRepository)
- Une classe séparée pour les rapports (EmployeeReportGenerator)
- Des interfaces appropriées

---

### Exercice 4.4 — Composition vs Héritage : Véhicules

**Objectifs** : Comprendre quand utiliser composition plutôt qu'héritage

**Partie 1 : Mauvaise conception avec héritage**

Créez cette hiérarchie (pour voir le problème) :
```
Vehicule
  ├── VehiculeAMoteur
  │     ├── Voiture
  │     └── Moto
  └── VehiculeSansMoteur
        ├── Velo
        └── Trottinette
```

Problème : Et si on a une voiture électrique ? Un vélo électrique ?

**Partie 2 : Bonne conception avec composition**

Refactorisez en utilisant la composition :

**Interface `Propulsion`** :
- `void avancer()`
- `void arreter()`
- `String getType()`

**Classes de propulsion** :
- `MoteurEssence` implements Propulsion
- `MoteurElectrique` implements Propulsion
- `PedaleHumaine` implements Propulsion

**Classe `Vehicule`** :
- Attribut : `Propulsion propulsion` (composition!)
- Constructeur qui prend une Propulsion
- Méthode `demarrer()` qui délègue à propulsion

Créez ensuite :
- `Voiture` avec `MoteurEssence`
- `VoitureElectrique` avec `MoteurElectrique`
- `Velo` avec `PedaleHumaine`
- `VeloElectrique` avec `MoteurElectrique`

Montrez que c'est beaucoup plus flexible !

---

### Exercice 4.5 — Projet intégrateur : Jeu de cartes

**Objectifs** : Projet complet utilisant tous les concepts

Créez un jeu de BlackJack avec :

**Enum `Couleur`** :
- COEUR, CARREAU, TREFLE, PIQUE
- Attribut : `symbole` ("♥", "♦", "♣", "♠")

**Enum `Valeur`** :
- AS, DEUX, TROIS, ..., DIX, VALET, DAME, ROI
- Attributs : `points` (1-13), `affichage` ("A", "2", ..., "K")

**Classe `Carte`** :
- Attributs : `couleur`, `valeur`
- Méthode `getValeurBlackjack()` (As=1 ou 11, figures=10)

**Classe `Paquet`** :
- ArrayList<Carte> avec les 52 cartes
- Méthodes : `melanger()`, `piocher()`, `estVide()`

**Classe abstraite `Joueur`** :
- Attributs : `nom`, `main` (ArrayList<Carte>)
- Méthode abstraite : `decidePiocher(int scoreActuel, Carte carteVisible)`
- Méthodes normales : `recevoirCarte()`, `calculerScore()`, `afficherMain()`

**Classes concrètes** :
- `JoueurHumain` : demande à l'utilisateur
- `Croupier` : pioche si score < 17

**Classe `PartieBlackjack`** :
- Gère le déroulement du jeu
- HashMap<Joueur, Integer> pour les scores
- Méthodes : `distribuerCartes()`, `jouer()`, `determinerGagnant()`

**Statistiques** (classe séparée) :
- Nombre de parties jouées
- Nombre de victoires du joueur
- Pourcentage de victoire

Implémentez un jeu complet avec plusieurs manches !

---

### Exercice 4.6 — Collections avancées : Réseau social

**Objectifs** : Collections complexes, graphes

Créez un mini réseau social avec :

**Classe `Utilisateur`** :
- Attributs : `pseudo`, `nom`, `age`, `amis` (HashSet<Utilisateur>)
- Méthodes : `ajouterAmi()`, `retirerAmi()`, `estAmiAvec()`

**Classe `Publication`** :
- Attributs : `auteur`, `contenu`, `date`, `likes` (HashSet<Utilisateur>)
- Méthodes : `aimer()`, `retirerLike()`, `getNombreLikes()`

**Classe `ReseauSocial`** :
- HashMap<String, Utilisateur> : pseudo → utilisateur
- ArrayList<Publication> : toutes les publications
- Méthodes avancées :
  - `suggererAmis(Utilisateur u)` : retourne les amis d'amis qui ne sont pas encore amis
  - `trouverCheminAmitie(Utilisateur u1, Utilisateur u2)` : algorithme de parcours
  - `utilisateursPopulaires(int seuil)` : utilisateurs avec > seuil amis
  - `publicationsPopulaires()` : publications avec le plus de likes
  - `calculerDegréSeparation(Utilisateur u1, Utilisateur u2)` : "6 degrees of separation"

Implémentez des algorithmes de parcours de graphe pour trouver les chemins d'amitié !

---

## Solutions - Exercices Débutants

### Solution 1.1 — Classe Livre

```java
public class Livre {
    public String titre;
    public String auteur;
    public int nombrePages;
    
    public Livre(String titre, String auteur, int nombrePages) {
        this.titre = titre;
        this.auteur = auteur;
        this.nombrePages = nombrePages;
    }
    
    public void afficherInfo() {
        System.out.println("Titre: " + titre + ", Auteur: " + auteur + ", Pages: " + nombrePages);
    }
}

// Main
public class Main {
    public static void main(String[] args) {
        Livre livre1 = new Livre("1984", "George Orwell", 328);
        Livre livre2 = new Livre("Le Petit Prince", "Antoine de Saint-Exupéry", 96);
        livre1.afficherInfo();
        livre2.afficherInfo();
    }
}
```

---

### Solution 1.2 — Classe Rectangle

```java
public class Rectangle {
    public double largeur;
    public double hauteur;
    
    public Rectangle(double largeur, double hauteur) {
        this.largeur = largeur;
        this.hauteur = hauteur;
    }
    
    public double calculerAire() {
        return largeur * hauteur;
    }
    
    public double calculerPerimetre() {
        return 2 * (largeur + hauteur);
    }
    
    public boolean estCarre() {
        return largeur == hauteur;
    }
}

// Main
public class Main {
    public static void main(String[] args) {
        Rectangle r1 = new Rectangle(5.0, 3.0);
        Rectangle r2 = new Rectangle(4.0, 4.0);
        
        System.out.println("Aire: " + r1.calculerAire());
        System.out.println("Perimetre: " + r1.calculerPerimetre());
        System.out.println("Est carre: " + r2.estCarre());
    }
}
```

---

### Solution 1.3 — Classe CompteBancaire Simple

```java
public class CompteBancaire {
    public String titulaire;
    public double solde;
    
    public CompteBancaire(String titulaire, double solde) {
        this.titulaire = titulaire;
        this.solde = solde;
    }
    
    public void deposer(double montant) {
        solde += montant;
        System.out.println("Depot de " + montant + " effectue");
    }
    
    public void retirer(double montant) {
        solde -= montant;
        System.out.println("Retrait de " + montant + " effectue");
    }
    
    public void afficherSolde() {
        System.out.println(titulaire + " - Solde: " + solde);
    }
}

// Main
public class Main {
    public static void main(String[] args) {
        CompteBancaire compte = new CompteBancaire("Alice", 1000.0);
        compte.afficherSolde();
        compte.deposer(500.0);
        compte.retirer(200.0);
        compte.afficherSolde();
    }
}
```

---

### Solution 1.4 — Classe Cercle

```java
public class Cercle {
    public double rayon;
    
    public Cercle(double rayon) {
        this.rayon = rayon;
    }
    
    public double calculerAire() {
        return Math.PI * rayon * rayon;
    }
    
    public double calculerCirconference() {
        return 2 * Math.PI * rayon;
    }
    
    public double calculerDiametre() {
        return 2 * rayon;
    }
}

// Main
public class Main {
    public static void main(String[] args) {
        Cercle c = new Cercle(5.0);
        System.out.printf("Aire: %.2f%n", c.calculerAire());
        System.out.printf("Circonference: %.2f%n", c.calculerCirconference());
        System.out.printf("Diametre: %.2f%n", c.calculerDiametre());
    }
}
```

---

### Solution 1.8 — Tableau d'objets

```java
public class Main {
    public static void main(String[] args) {
        // 1. Créer un tableau de 5 livres
        Livre[] bibliotheque = new Livre[5];
        
        // 2. Remplir le tableau
        bibliotheque[0] = new Livre("1984", "George Orwell", 328);
        bibliotheque[1] = new Livre("Le Petit Prince", "Antoine de Saint-Exupéry", 96);
        bibliotheque[2] = new Livre("Harry Potter", "J.K. Rowling", 450);
        bibliotheque[3] = new Livre("Le Seigneur des Anneaux", "J.R.R. Tolkien", 1200);
        bibliotheque[4] = new Livre("Fondation", "Isaac Asimov", 255);
        
        // 3. Afficher tous les livres
        System.out.println("=== Tous les livres ===");
        for (Livre livre : bibliotheque) {
            livre.afficherInfo();
        }
        
        // 4. Trouver le livre avec le plus de pages
        Livre plusLong = bibliotheque[0];
        for (Livre livre : bibliotheque) {
            if (livre.nombrePages > plusLong.nombrePages) {
                plusLong = livre;
            }
        }
        System.out.println("\nLivre le plus long:");
        plusLong.afficherInfo();
        
        // 5. Calculer le nombre moyen de pages
        int totalPages = 0;
        for (Livre livre : bibliotheque) {
            totalPages += livre.nombrePages;
        }
        double moyenne = (double) totalPages / bibliotheque.length;
        System.out.printf("\nNombre moyen de pages: %.2f%n", moyenne);
    }
}
```

---

## Solutions - Exercices Intermédiaires

### Solution 2.1 — Encapsulation complète

```java
public class CompteBancaire {
    private String titulaire;
    private double solde;
    
    public CompteBancaire(String titulaire, double solde) {
        this.titulaire = titulaire;
        this.solde = solde;
    }
    
    // Getters
    public String getTitulaire() {
        return titulaire;
    }
    
    public double getSolde() {
        return solde;
    }
    
    // Setter avec validation
    public void setTitulaire(String titulaire) {
        if (titulaire == null || titulaire.trim().isEmpty()) {
            System.out.println("Erreur: le titulaire ne peut pas etre vide");
            return;
        }
        this.titulaire = titulaire;
    }
    
    public void deposer(double montant) {
        if (montant <= 0) {
            System.out.println("Erreur: le montant doit etre positif");
            return;
        }
        solde += montant;
        System.out.println("Depot de " + montant + " effectue");
    }
    
    public void retirer(double montant) {
        if (montant <= 0) {
            System.out.println("Erreur: le montant doit etre positif");
            return;
        }
        if (montant > solde) {
            System.out.println("Erreur: fonds insuffisants");
            return;
        }
        solde -= montant;
        System.out.println("Retrait de " + montant + " effectue");
    }
    
    public void transferer(CompteBancaire destination, double montant) {
        if (montant > solde) {
            System.out.println("Erreur: fonds insuffisants pour le transfert");
            return;
        }
        this.retirer(montant);
        destination.deposer(montant);
        System.out.println("Transfert de " + montant + " vers " + destination.getTitulaire());
    }
    
    public void afficherSolde() {
        System.out.println(titulaire + " - Solde: " + solde);
    }
}
```

---

### Solution 2.2 — Héritage : Véhicules

```java
// Classe parent
public class Vehicule {
    private String marque;
    private String modele;
    private int annee;
    
    public Vehicule(String marque, String modele, int annee) {
        this.marque = marque;
        this.modele = modele;
        this.annee = annee;
    }
    
    public void afficherInfo() {
        System.out.println(marque + " " + modele + " (" + annee + ")");
    }
    
    public int calculerAge() {
        return 2025 - annee;
    }
    
    // Getters
    public String getMarque() { return marque; }
    public String getModele() { return modele; }
    public int getAnnee() { return annee; }
}

// Classe enfant Voiture
public class Voiture extends Vehicule {
    private int nombrePortes;
    
    public Voiture(String marque, String modele, int annee, int nombrePortes) {
        super(marque, modele, annee);
        this.nombrePortes = nombrePortes;
    }
    
    @Override
    public void afficherInfo() {
        super.afficherInfo();
        System.out.println("  Nombre de portes: " + nombrePortes);
    }
    
    public int getNombrePortes() { return nombrePortes; }
}

// Classe enfant Moto
public class Moto extends Vehicule {
    private int cylindree;
    
    public Moto(String marque, String modele, int annee, int cylindree) {
        super(marque, modele, annee);
        this.cylindree = cylindree;
    }
    
    @Override
    public void afficherInfo() {
        super.afficherInfo();
        System.out.println("  Cylindree: " + cylindree + " cc");
    }
    
    public int getCylindree() { return cylindree; }
}

// Main
public class Main {
    public static void main(String[] args) {
        Vehicule[] flotte = new Vehicule[3];
        flotte[0] = new Voiture("Toyota", "Corolla", 2020, 4);
        flotte[1] = new Moto("Harley", "Sportster", 2019, 883);
        flotte[2] = new Voiture("Honda", "Civic", 2022, 4);
        
        for (Vehicule v : flotte) {
            v.afficherInfo();
            System.out.println("Age: " + v.calculerAge() + " ans\n");
        }
    }
}
```

---

### Solution 2.5 — Static : Compteur d'instances

```java
public class Etudiant {
    private String nom;
    private int numeroEtudiant;
    private static int compteur = 0;
    public static final String UNIVERSITE = "UdeM";
    
    public Etudiant(String nom) {
        this.nom = nom;
        compteur++;
        this.numeroEtudiant = compteur;
    }
    
    public static int getNombreEtudiants() {
        return compteur;
    }
    
    public void afficherInfo() {
        System.out.println("Nom: " + nom + ", Numero: " + numeroEtudiant);
    }
}

// Main
public class Main {
    public static void main(String[] args) {
        System.out.println("Universite: " + Etudiant.UNIVERSITE);
        System.out.println("Nombre initial: " + Etudiant.getNombreEtudiants());
        
        Etudiant e1 = new Etudiant("Alice");
        Etudiant e2 = new Etudiant("Bob");
        Etudiant e3 = new Etudiant("Charlie");
        
        System.out.println("Nombre apres creation: " + Etudiant.getNombreEtudiants());
        e1.afficherInfo();
        e2.afficherInfo();
        e3.afficherInfo();
    }
}
```

---

## Note sur les solutions

Les solutions complètes pour les exercices avancés et experts sont volontairement omises pour encourager la pratique autonome. Voici quelques conseils :

**Pour les exercices avancés (⭐⭐⭐)** :
- Commencez par dessiner un diagramme de classes
- Implémentez une fonctionnalité à la fois
- Testez chaque méthode avant de passer à la suivante
- N'hésitez pas à créer des méthodes helper privées

**Pour les exercices experts (⭐⭐⭐⭐)** :
- Planifiez votre architecture avant de coder
- Utilisez des noms de variables et méthodes descriptifs
- Commentez les parties complexes
- Testez avec différents scénarios
- Refactorisez si le code devient trop complexe

**Debugging Tips** :
- Utilisez `System.out.println()` pour tracer l'exécution
- Vérifiez toujours les cas limites (listes vides, valeurs nulles, etc.)
- Testez avec des données variées
- Utilisez le débogueur de votre IDE
