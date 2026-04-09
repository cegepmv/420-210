+++
title = "Fichiers"
weight = 15
+++

# Lecture et écriture de fichiers en Java

---

## Table des matières

1. [Lecture et écriture de fichiers texte](#1-lecture-et-écriture-de-fichiers-texte)
2. [Lecture et écriture de fichiers binaires](#2-lecture-et-écriture-de-fichiers-binaires)
3. [La classe File et Files](#3-la-classe-file-et-files)
4. [Gestion des exceptions](#4-gestion-des-exceptions)
5. [JSON avec Gson](#5-json-avec-gson)
6. [JSON avec Jackson](#6-json-avec-jackson)
7. [Mini-projets](#7-mini-projets)

---

## 1. Lecture et écriture de fichiers texte

### Pourquoi sauvegarder dans un fichier ?

Quand un programme Java s'exécute, toutes les données qu'il crée (objets, listes, variables) sont stockées dans la **mémoire vive (RAM)**. Dès que le programme se termine, ces données **disparaissent**.

Pour conserver des données entre deux exécutions du programme, on doit les écrire dans un **fichier** sur le disque dur. C'est ce qu'on appelle la **persistance des données**.

> **Analogie** : Imagine que tu travailles sur un devoir. Si tu n'enregistres pas ton fichier Word avant de fermer l'ordinateur, tout ton travail est perdu. Sauvegarder dans un fichier, c'est exactement le même principe pour un programme Java.

---

### Qu'est-ce qu'un fichier texte ?

Un fichier texte est un fichier dont le contenu est constitué de **caractères lisibles** par un humain : lettres, chiffres, symboles, espaces, retours à la ligne. On peut l'ouvrir avec n'importe quel éditeur de texte (Notepad, VSCode, etc.).

Exemples d'extensions de fichiers texte : `.txt`, `.csv`, `.json`, `.xml`, `.html`.

En Java, on lit et écrit des fichiers texte principalement avec les classes suivantes :

| Classe | Rôle | Quand l'utiliser |
|---|---|---|
| `FileWriter` | Ouvre un fichier en écriture | Base pour écrire du texte |
| `BufferedWriter` | Ajoute un tampon à `FileWriter` | Toujours, pour la performance |
| `PrintWriter` | Offre `println()` et `printf()` | Quand on veut écrire ligne par ligne facilement |
| `FileReader` | Ouvre un fichier en lecture | Base pour lire du texte |
| `BufferedReader` | Ajoute un tampon à `FileReader` | Toujours, pour la performance |
| `Scanner` | Lecture simple et flexible | Pour les débutants ou les fichiers simples |

---

### 1.1 Écriture avec FileWriter et BufferedWriter

#### Pourquoi utiliser BufferedWriter plutôt que FileWriter seul ?

`FileWriter` écrit directement sur le disque à chaque appel. `BufferedWriter` accumule d'abord les données dans un **tampon (buffer)** en mémoire, puis écrit tout en une seule fois quand le tampon est plein ou quand on ferme le fichier.

> **Analogie** : Imagine que tu dois envoyer 100 colis. Avec `FileWriter`, tu fais 100 voyages à la poste. Avec `BufferedWriter`, tu accumules tous les colis dans un camion, puis tu fais un seul voyage. C'est beaucoup plus efficace.

```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class EcrireTexte {
    public static void main(String[] args) {

        // try-with-resources : Java ferme automatiquement le fichier
        // même si une erreur se produit
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("notes.txt"))) {

            writer.write("Première ligne");   // écrire du texte
            writer.newLine();                 // aller à la ligne suivante
            writer.write("Deuxième ligne");
            writer.newLine();
            writer.write("Troisième ligne");

            System.out.println("Fichier écrit avec succès !");

        } catch (IOException e) {
            // IOException est lancée si le fichier ne peut pas être créé
            // ou si une erreur d'écriture se produit
            System.out.println("Erreur lors de l'écriture : " + e.getMessage());
        }
    }
}
```

**Ce que fait chaque ligne :**
- `new FileWriter("notes.txt")` : crée ou écrase le fichier `notes.txt` dans le répertoire courant du projet
- `new BufferedWriter(...)` : enveloppe le `FileWriter` dans un tampon
- `writer.write("...")` : écrit le texte dans le tampon
- `writer.newLine()` : insère un retour à la ligne (compatible avec tous les systèmes d'exploitation)
- Le `try-with-resources` appelle automatiquement `writer.close()` à la fin, ce qui vide le tampon et ferme le fichier

**Contenu du fichier notes.txt :**
```
Première ligne
Deuxième ligne
Troisième ligne
```

> ⚠️ **Attention :** Par défaut, `FileWriter` **écrase** le fichier s'il existe déjà. Pour **ajouter** du contenu à la fin d'un fichier existant, passer `true` comme deuxième argument :
> ```java
> new FileWriter("notes.txt", true) // true = mode ajout (append)
> ```

> ⚠️ **Erreur courante :** Oublier `writer.newLine()` entre les lignes. Si tu oublies, tout le texte sera collé sur une seule ligne dans le fichier.

---

### 1.2 Écriture avec PrintWriter

`PrintWriter` est souvent plus pratique que `BufferedWriter` car il offre les méthodes `print()`, `println()` et `printf()`, exactement comme `System.out`.

```java
import java.io.FileWriter;
import java.io.IOException;
import java.io.PrintWriter;

public class EcrireAvecPrintWriter {
    public static void main(String[] args) {

        try (PrintWriter writer = new PrintWriter(new FileWriter("produits.txt"))) {

            // println() ajoute automatiquement un retour à la ligne
            writer.println("=== Liste des produits ===");
            writer.println("Pizza Margherita - 12.99$");
            writer.println("Coca-Cola - 2.99$");
            writer.println("Tiramisu - 6.99$");

            // printf() permet de formater les nombres
            writer.printf("Total : %.2f$%n", 22.97);
            // %.2f = nombre décimal avec 2 chiffres après la virgule
            // %n = retour à la ligne (portable sur tous les OS)

        } catch (IOException e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }
}
```

**Contenu du fichier produits.txt :**
```
=== Liste des produits ===
Pizza Margherita - 12.99$
Coca-Cola - 2.99$
Tiramisu - 6.99$
Total : 22.97$
```

> 💡 **Conseil :** Si tu connais déjà `System.out.println()`, utiliser `PrintWriter` sera très naturel — c'est exactement la même syntaxe.

---

### 1.3 Lecture avec BufferedReader

`BufferedReader` lit le fichier **ligne par ligne**, ce qui est la façon la plus courante de lire un fichier texte.

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class LireTexte {
    public static void main(String[] args) {

        try (BufferedReader reader = new BufferedReader(new FileReader("notes.txt"))) {

            String ligne; // variable qui contiendra chaque ligne lue

            // readLine() lit une ligne et retourne null quand on est à la fin du fichier
            // C'est pourquoi on vérifie (ligne = reader.readLine()) != null
            while ((ligne = reader.readLine()) != null) {
                System.out.println(ligne);
            }

        } catch (IOException e) {
            System.out.println("Erreur lors de la lecture : " + e.getMessage());
        }
    }
}
```

**Décomposition de la condition du while :**
```java
while ((ligne = reader.readLine()) != null)
//      ^^^^^^^^^^^^^^^^^^^^^^^^^   ^^^^^^
//      1. Lit une ligne et          2. Vérifie si
//         l'assigne à `ligne`          ce n'est pas null
//                                      (fin du fichier)
```

**Sortie console :**
```
Première ligne
Deuxième ligne
Troisième ligne
```

> ⚠️ **Erreur courante :** Tenter de lire un fichier qui n'existe pas. Cela lance une `FileNotFoundException`. Il est recommandé de vérifier l'existence du fichier avant de le lire (voir section 4).

---

### 1.4 Lecture avec Scanner

`Scanner` est plus simple à utiliser pour les débutants. Il est très flexible : il peut lire depuis un fichier, depuis la console, depuis une chaîne de caractères, etc.

```java
import java.io.File;
import java.io.IOException;
import java.util.Scanner;

public class LireAvecScanner {
    public static void main(String[] args) {

        // On passe un objet File au Scanner (pas un nom de fichier directement)
        try (Scanner scanner = new Scanner(new File("produits.txt"))) {

            while (scanner.hasNextLine()) {      // tant qu'il reste des lignes
                String ligne = scanner.nextLine(); // lire la prochaine ligne
                System.out.println(ligne);
            }

        } catch (IOException e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }
}
```

**Différences entre BufferedReader et Scanner :**

| | `BufferedReader` | `Scanner` |
|---|---|---|
| **Performance** | Plus rapide (tampon) | Plus lente |
| **Simplicité** | Un peu plus verbeux | Plus simple |
| **Lecture mot par mot** | Non | Oui (`next()`) |
| **Lecture de nombres** | Non (conversion manuelle) | Oui (`nextInt()`, `nextDouble()`) |

> 💡 **Conseil :** Pour des fichiers simples ou des projets débutants, `Scanner` est souvent suffisant. Pour des fichiers volumineux ou des applications professionnelles, préférer `BufferedReader`.

---

### 1.5 Lire toutes les lignes en une liste

Depuis Java 11, la classe `Files` offre une méthode très pratique pour lire tout un fichier en une seule ligne de code.

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.List;

public class LireToutesLesLignes {
    public static void main(String[] args) {

        try {
            // Lire toutes les lignes d'un coup dans une List<String>
            List<String> lignes = Files.readAllLines(Path.of("produits.txt"));

            System.out.println("Nombre de lignes : " + lignes.size());

            for (String ligne : lignes) {
                System.out.println(ligne);
            }

            // On peut aussi accéder à une ligne spécifique par son index
            System.out.println("Première ligne : " + lignes.get(0));

        } catch (IOException e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }
}
```

> ⚠️ **Attention :** `Files.readAllLines()` charge **tout le fichier en mémoire**. Si le fichier est très volumineux (plusieurs gigaoctets), préfère `BufferedReader` qui lit ligne par ligne sans tout charger d'un coup.

---

### 1.6 Exemple complet — Sauvegarde et chargement d'une liste de produits

Cet exemple montre comment **écrire** une liste dans un fichier texte, puis la **relire** au prochain démarrage du programme. C'est le cycle de base de toute persistance de données.

```java
import java.io.*;
import java.util.ArrayList;
import java.util.List;

public class GestionProduitsFichier {

    static final String FICHIER = "produits.txt";

    // Sauvegarder une liste de produits dans un fichier
    public static void sauvegarder(List<String> produits) {
        try (PrintWriter writer = new PrintWriter(new FileWriter(FICHIER))) {
            for (String produit : produits) {
                writer.println(produit); // une ligne par produit
            }
            System.out.println("Sauvegarde réussie !");
        } catch (IOException e) {
            System.out.println("Erreur de sauvegarde : " + e.getMessage());
        }
    }

    // Charger la liste de produits depuis un fichier
    public static List<String> charger() {
        List<String> produits = new ArrayList<>();

        // Vérifier si le fichier existe avant d'essayer de le lire
        File fichier = new File(FICHIER);
        if (!fichier.exists()) {
            System.out.println("Aucune sauvegarde trouvée, liste vide.");
            return produits; // retourner une liste vide
        }

        try (BufferedReader reader = new BufferedReader(new FileReader(FICHIER))) {
            String ligne;
            while ((ligne = reader.readLine()) != null) {
                produits.add(ligne);
            }
            System.out.println("Chargement réussi !");
        } catch (IOException e) {
            System.out.println("Erreur de chargement : " + e.getMessage());
        }

        return produits;
    }

    public static void main(String[] args) {
        // --- Première exécution : sauvegarder ---
        List<String> produits = new ArrayList<>();
        produits.add("Pizza Margherita - 12.99$");
        produits.add("Coca-Cola - 2.99$");
        produits.add("Tiramisu - 6.99$");
        sauvegarder(produits);

        // --- Deuxième exécution simulée : charger ---
        List<String> produitsCharges = charger();
        System.out.println("\nProduits chargés :");
        for (String p : produitsCharges) {
            System.out.println("  - " + p);
        }
    }
}
```

---

## 2. Lecture et écriture de fichiers binaires

### Qu'est-ce qu'un fichier binaire ?

Un fichier binaire stocke des données sous forme d'**octets bruts** (0 et 1). Contrairement aux fichiers texte, on ne peut pas l'ouvrir dans un éditeur de texte et le lire directement — il apparaîtra comme des caractères illisibles.

L'avantage principal est qu'on peut **sauvegarder directement des objets Java** sans avoir à les convertir manuellement en texte.

> **Analogie** : Sauvegarder un objet Java dans un fichier binaire, c'est comme prendre une photo de l'objet et la stocker. Quand on recharge le fichier, on reconstitue l'objet exactement comme il était.

---

### 2.1 La sérialisation — Qu'est-ce que c'est ?

La **sérialisation** est le processus de conversion d'un objet Java en une suite d'octets pour le stocker ou le transmettre. La **désérialisation** est l'opération inverse : recréer l'objet à partir des octets.

Pour qu'un objet soit sérialisable, sa classe doit implémenter l'interface `Serializable`. Cette interface est spéciale : elle ne contient aucune méthode à implémenter — elle sert juste de "marqueur" pour dire à Java que la classe peut être sérialisée.

```java
import java.io.Serializable;

// Serializable est une interface "marqueur" : pas de méthodes à implémenter
public class Produit implements Serializable {

    // serialVersionUID est un identifiant de version
    // Si la classe change, cet ID permet de détecter les incompatibilités
    // IntelliJ peut le générer automatiquement (recommandé)
    private static final long serialVersionUID = 1L;

    private String nom;
    private double prix;

    public Produit(String nom, double prix) {
        this.nom = nom;
        this.prix = prix;
    }

    @Override
    public String toString() {
        return nom + " - " + prix + "$";
    }

    public String getNom() { return nom; }
    public double getPrix() { return prix; }
}
```

> ⚠️ **Important :** Si une classe contient des attributs qui sont eux-mêmes des objets, ces objets doivent aussi implémenter `Serializable`. Par exemple, si `Commande` contient une `List<Produit>`, alors `Produit` doit aussi être `Serializable`.

---

### 2.2 Écriture d'un objet dans un fichier binaire

```java
import java.io.*;

public class EcrireBinaire {
    public static void main(String[] args) {

        Produit p = new Produit("Pizza Margherita", 12.99);

        // ObjectOutputStream s'appuie sur FileOutputStream
        // FileOutputStream ouvre le fichier en écriture binaire
        // ObjectOutputStream permet d'y écrire des objets Java
        try (ObjectOutputStream oos = new ObjectOutputStream(
                new FileOutputStream("produit.dat"))) {

            oos.writeObject(p); // sérialiser et écrire l'objet
            System.out.println("Objet sauvegardé !");

        } catch (IOException e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }
}
```

> 💡 **Note :** Le fichier `.dat` n'est pas lisible dans un éditeur de texte. C'est normal : il contient les octets de l'objet Java.

---

### 2.3 Lecture d'un objet depuis un fichier binaire

```java
import java.io.*;

public class LireBinaire {
    public static void main(String[] args) {

        // ObjectInputStream permet de lire des objets Java depuis un fichier binaire
        try (ObjectInputStream ois = new ObjectInputStream(
                new FileInputStream("produit.dat"))) {

            // readObject() retourne un Object — il faut caster vers le bon type
            Produit p = (Produit) ois.readObject();
            System.out.println("Objet chargé : " + p);

        } catch (IOException e) {
            // Erreur si le fichier n'existe pas ou est corrompu
            System.out.println("Erreur de lecture : " + e.getMessage());
        } catch (ClassNotFoundException e) {
            // Erreur si la classe Produit n'est plus dans le projet
            System.out.println("Classe introuvable : " + e.getMessage());
        }
    }
}
```

---

### 2.4 Sauvegarder et charger une liste d'objets

On peut sauvegarder une liste entière d'objets comme si c'était un seul objet, car `ArrayList` implémente aussi `Serializable`.

```java
import java.io.*;
import java.util.ArrayList;
import java.util.List;

public class SauvegarderListe {

    static final String FICHIER = "produits.dat";

    public static void sauvegarder(List<Produit> produits) {
        try (ObjectOutputStream oos = new ObjectOutputStream(
                new FileOutputStream(FICHIER))) {
            oos.writeObject(produits); // sauvegarder la liste entière d'un coup
            System.out.println("Liste sauvegardée (" + produits.size() + " produits)");
        } catch (IOException e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }

    @SuppressWarnings("unchecked") // supprimer l'avertissement du cast
    public static List<Produit> charger() {
        File fichier = new File(FICHIER);
        if (!fichier.exists()) {
            System.out.println("Aucune sauvegarde trouvée.");
            return new ArrayList<>();
        }

        try (ObjectInputStream ois = new ObjectInputStream(
                new FileInputStream(FICHIER))) {
            // Le cast (List<Produit>) est nécessaire car readObject() retourne Object
            return (List<Produit>) ois.readObject();
        } catch (IOException | ClassNotFoundException e) {
            System.out.println("Erreur : " + e.getMessage());
            return new ArrayList<>();
        }
    }

    public static void main(String[] args) {
        // Sauvegarder
        List<Produit> produits = new ArrayList<>();
        produits.add(new Produit("Pizza Margherita", 12.99));
        produits.add(new Produit("Coca-Cola", 2.99));
        produits.add(new Produit("Tiramisu", 6.99));
        sauvegarder(produits);

        // Charger
        List<Produit> charger = charger();
        System.out.println("\nProduits chargés :");
        for (Produit p : charger) {
            System.out.println("  - " + p);
        }
    }
}
```

> ⚠️ **Limitation importante :** La sérialisation binaire est **spécifique à Java**. Un fichier `.dat` ne peut pas être lu par un programme Python, JavaScript, etc. Si tu as besoin de partager des données entre différents langages, utilise plutôt le format JSON (voir sections 5 et 6).

---

## 3. La classe File et Files

### 3.1 La classe File

`File` représente un fichier ou un dossier sur le disque. Elle ne permet pas de lire ou d'écrire du contenu — elle sert surtout à **interroger et manipuler le système de fichiers** (vérifier l'existence, obtenir des informations, créer des dossiers, etc.).

```java
import java.io.File;

public class UtiliserFile {
    public static void main(String[] args) {

        File fichier = new File("notes.txt");

        // --- Vérifications ---
        System.out.println("Existe ?           " + fichier.exists());
        System.out.println("Est un fichier ?   " + fichier.isFile());
        System.out.println("Est un dossier ?   " + fichier.isDirectory());
        System.out.println("Peut lire ?        " + fichier.canRead());
        System.out.println("Peut écrire ?      " + fichier.canWrite());

        // --- Informations ---
        System.out.println("Nom :              " + fichier.getName());
        System.out.println("Chemin relatif :   " + fichier.getPath());
        System.out.println("Chemin absolu :    " + fichier.getAbsolutePath());
        System.out.println("Taille :           " + fichier.length() + " octets");

        // --- Manipulation de dossiers ---
        File dossier = new File("monDossier");
        if (!dossier.exists()) {
            boolean cree = dossier.mkdir(); // créer un seul dossier
            System.out.println("Dossier créé : " + cree);
        }

        // mkdirs() crée aussi tous les dossiers parents manquants
        File dossierImbriqué = new File("parent/enfant/petitEnfant");
        dossierImbriqué.mkdirs();

        // --- Lister le contenu d'un dossier ---
        File dossierCourant = new File(".");
        String[] contenu = dossierCourant.list();
        if (contenu != null) {
            System.out.println("\nContenu du dossier courant :");
            for (String nom : contenu) {
                System.out.println("  " + nom);
            }
        }

        // --- Supprimer un fichier ---
        // fichier.delete(); // décommenter pour supprimer
    }
}
```

---

### 3.2 La classe Files (Java NIO)

`Files` (dans `java.nio.file`) est la version moderne de manipulation de fichiers. Elle est plus puissante et offre une syntaxe plus concise.

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardCopyOption;

public class UtiliserFiles {
    public static void main(String[] args) {

        Path source = Path.of("notes.txt");
        Path destination = Path.of("notes_copie.txt");

        try {
            // --- Vérifications ---
            System.out.println("Existe ? " + Files.exists(source));
            System.out.println("Taille : " + Files.size(source) + " octets");

            // --- Copier un fichier ---
            // REPLACE_EXISTING : écraser si le fichier destination existe déjà
            Files.copy(source, destination, StandardCopyOption.REPLACE_EXISTING);
            System.out.println("Fichier copié !");

            // --- Écrire une chaîne directement ---
            Files.writeString(Path.of("message.txt"), "Bonjour tout le monde !");

            // --- Lire tout le fichier en une chaîne ---
            String contenu = Files.readString(Path.of("message.txt"));
            System.out.println("Contenu : " + contenu);

            // --- Déplacer un fichier ---
            // Files.move(source, destination, StandardCopyOption.REPLACE_EXISTING);

            // --- Supprimer un fichier ---
            // Files.delete(destination);
            // Files.deleteIfExists(destination); // ne lance pas d'erreur si absent

        } catch (IOException e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }
}
```

**Tableau comparatif File vs Files :**

| Opération | `File` (ancienne façon) | `Files` (nouvelle façon) |
|---|---|---|
| Vérifier existence | `file.exists()` | `Files.exists(path)` |
| Copier | Manuel (lire + écrire) | `Files.copy(src, dest)` |
| Lire tout le fichier | Boucle avec BufferedReader | `Files.readString(path)` |
| Écrire une chaîne | FileWriter + write | `Files.writeString(path, str)` |
| Supprimer | `file.delete()` | `Files.delete(path)` |

---

## 4. Gestion des exceptions

### Pourquoi les fichiers lancent-ils des exceptions ?

Les opérations sur les fichiers dépendent de facteurs **extérieurs au programme** : le fichier doit exister, l'utilisateur doit avoir les permissions, le disque ne doit pas être plein, etc. Si quelque chose ne va pas, Java signale le problème en lançant une **exception**.

C'est pour cette raison que toutes les opérations sur les fichiers sont dans un bloc `try-catch`.

---

### 4.1 Les exceptions courantes

| Exception | Cause fréquente | Comment l'éviter |
|---|---|---|
| `FileNotFoundException` | Le fichier n'existe pas | Vérifier avec `file.exists()` avant de lire |
| `IOException` | Erreur générale (disque plein, permissions) | Toujours utiliser try-catch |
| `ClassNotFoundException` | Classe introuvable lors de la désérialisation | Ne pas supprimer/renommer les classes sérialisées |

---

### 4.2 Try-with-resources — La bonne pratique

Tout fichier ouvert **doit être fermé** après utilisation, sinon le système retient les ressources et cela peut causer des problèmes (fichier verrouillé, fuites mémoire).

Le **try-with-resources** (Java 7+) gère la fermeture **automatiquement**, même si une exception se produit.

```java
// ❌ Ancienne façon — dangereux car on peut oublier de fermer
BufferedReader reader = null;
try {
    reader = new BufferedReader(new FileReader("notes.txt"));
    String ligne = reader.readLine();
    System.out.println(ligne);
} catch (IOException e) {
    e.printStackTrace();
} finally {
    // Il faut penser à fermer manuellement dans finally
    if (reader != null) {
        try {
            reader.close(); // autre try-catch nécessaire !
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

// ✅ Nouvelle façon — fermeture automatique garantie
try (BufferedReader reader = new BufferedReader(new FileReader("notes.txt"))) {
    String ligne = reader.readLine();
    System.out.println(ligne);
} catch (IOException e) {
    e.printStackTrace();
}
// reader.close() est appelé automatiquement ici, même si une exception a eu lieu
```

> 💡 **Règle simple :** Tout ce qui peut être "fermé" (qui implémente `AutoCloseable`) peut et doit être mis dans un try-with-resources.

---

### 4.3 Vérifier si un fichier existe avant de le lire

```java
import java.io.*;

public class LireAvecVerification {
    public static void main(String[] args) {

        File fichier = new File("notes.txt");

        // Toujours vérifier l'existence avant de lire
        if (!fichier.exists()) {
            System.out.println("Le fichier n'existe pas encore. Aucune donnée à charger.");
            return; // sortir de la méthode proprement
        }

        // Maintenant on peut lire en toute sécurité
        try (BufferedReader reader = new BufferedReader(new FileReader(fichier))) {
            String ligne;
            while ((ligne = reader.readLine()) != null) {
                System.out.println(ligne);
            }
        } catch (IOException e) {
            System.out.println("Erreur inattendue lors de la lecture : " + e.getMessage());
        }
    }
}
```

> 💡 **Bonne pratique :** Dans les méthodes `charger()`, toujours commencer par vérifier si le fichier existe. Si ce n'est pas le cas, retourner une liste vide plutôt que de lancer une exception.

---

## 5. JSON avec Gson

### Qu'est-ce que JSON ?

**JSON** (JavaScript Object Notation) est un format texte pour représenter des données structurées. Il est devenu le standard universel pour l'échange de données entre applications.

**Exemple de fichier JSON représentant une pizza :**
```json
{
  "nom": "Pizza Margherita",
  "prix": 12.99,
  "taille": "Large",
  "garnitures": ["Tomate", "Mozzarella", "Basilic"],
  "disponible": true
}
```

**Les types de données supportés par JSON :**

| Type JSON | Exemple | Équivalent Java |
|---|---|---|
| Texte (String) | `"Bonjour"` | `String` |
| Nombre entier | `42` | `int`, `long` |
| Nombre décimal | `12.99` | `double`, `float` |
| Booléen | `true` / `false` | `boolean` |
| Tableau | `["a", "b", "c"]` | `List`, tableau |
| Objet | `{"clé": "valeur"}` | Objet Java |
| Null | `null` | `null` |

**Avantages de JSON par rapport au fichier texte simple ou binaire :**
- **Lisible par les humains** : on peut ouvrir le fichier et comprendre les données
- **Portable** : peut être lu par Python, JavaScript, C#, etc.
- **Structuré** : supporte des objets imbriqués et des listes naturellement
- **Standard** : utilisé partout dans les APIs web modernes

---

### Qu'est-ce que Gson ?

**Gson** est une bibliothèque Java développée par Google qui automatise la conversion entre objets Java et JSON. Sans Gson, il faudrait construire les chaînes JSON manuellement, ce qui est fastidieux et source d'erreurs.

> **Analogie** : Gson est comme un traducteur automatique entre le "langage Java" (objets, attributs) et le "langage JSON" (texte structuré). Tu lui donnes un objet Java, il te rend le JSON correspondant, et vice versa.

---

### 5.1 Installation de Gson

**Avec Maven** — ajouter dans `pom.xml` :
```xml
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.10.1</version>
</dependency>
```

**Avec Gradle** — ajouter dans `build.gradle` :
```groovy
implementation 'com.google.code.gson:gson:2.10.1'
```

**Sans Maven/Gradle (IntelliJ) :**
1. Télécharger le fichier `.jar` sur https://search.maven.org (chercher "gson")
2. Dans IntelliJ : `File → Project Structure → Libraries → + → Java`
3. Sélectionner le fichier `.jar` téléchargé

---

### 5.2 Les classes du projet

Pour les exemples qui suivent, voici les classes utilisées :

```java
public class Produit {
    private String nom;
    private double prix;
    private String categorie;

    public Produit(String nom, double prix, String categorie) {
        this.nom = nom;
        this.prix = prix;
        this.categorie = categorie;
    }

    // Getters
    public String getNom()       { return nom; }
    public double getPrix()      { return prix; }
    public String getCategorie() { return categorie; }

    @Override
    public String toString() {
        return nom + " (" + categorie + ") - " + prix + "$";
    }
}
```

```java
import java.util.ArrayList;
import java.util.List;

public class Commande {
    private int id;
    private String nomClient;
    private List<Produit> items;

    public Commande(int id, String nomClient) {
        this.id = id;
        this.nomClient = nomClient;
        this.items = new ArrayList<>();
    }

    public void ajouterProduit(Produit p) { items.add(p); }

    public int getId()              { return id; }
    public String getNomClient()    { return nomClient; }
    public List<Produit> getItems() { return items; }
}
```

---

### 5.3 Comment Gson mappe les attributs

Gson fait correspondre automatiquement les **noms des attributs Java** avec les **clés JSON**. Il n'y a pas besoin de configuration supplémentaire.

```
Objet Java :                    JSON généré :
─────────────────               ─────────────────────────────────────
String nom = "Margherita"  →    "nom": "Margherita"
double prix = 12.99        →    "prix": 12.99
String categorie = "Pizza" →    "categorie": "Pizza"
```

> ⚠️ **Important :** Gson accède directement aux **champs privés** de la classe, même sans getters. C'est une différence majeure avec Jackson (section 6) qui requiert des getters.

---

### 5.4 Objet Java → JSON (toJson)

```java
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;

public class GsonEcriture {
    public static void main(String[] args) {

        Produit pizza = new Produit("Pizza Margherita", 12.99, "Pizza");

        // --- Version simple ---
        Gson gson = new Gson();
        String json = gson.toJson(pizza);
        System.out.println("JSON compact :");
        System.out.println(json);
        // Résultat : {"nom":"Pizza Margherita","prix":12.99,"categorie":"Pizza"}

        // --- Version avec indentation (pretty print) ---
        // GsonBuilder permet de configurer Gson avant de le créer
        Gson gsonJoli = new GsonBuilder()
                .setPrettyPrinting() // activer l'indentation
                .create();

        String jsonJoli = gsonJoli.toJson(pizza);
        System.out.println("\nJSON indenté :");
        System.out.println(jsonJoli);
    }
}
```

**Sortie console :**
```
JSON compact :
{"nom":"Pizza Margherita","prix":12.99,"categorie":"Pizza"}

JSON indenté :
{
  "nom": "Pizza Margherita",
  "prix": 12.99,
  "categorie": "Pizza"
}
```

> 💡 **Conseil :** Toujours utiliser `setPrettyPrinting()` pour les fichiers que tu vas lire avec un éditeur de texte. Le JSON compact est utile pour les échanges réseau où la taille importe.

---

### 5.5 JSON → Objet Java (fromJson)

```java
import com.google.gson.Gson;

public class GsonLecture {
    public static void main(String[] args) {

        // Chaîne JSON (comme ce qu'on lirait depuis un fichier)
        String json = "{\"nom\":\"Pizza Margherita\",\"prix\":12.99,\"categorie\":\"Pizza\"}";

        Gson gson = new Gson();

        // Convertir le JSON en objet Java
        // Le deuxième argument indique à Gson quelle classe créer
        Produit pizza = gson.fromJson(json, Produit.class);

        System.out.println("Objet recréé : " + pizza);
        System.out.println("Nom : " + pizza.getNom());
        System.out.println("Prix : " + pizza.getPrix());
    }
}
```

**Ce que fait `fromJson` :**
1. Analyse le texte JSON
2. Crée une nouvelle instance de `Produit` (en utilisant un constructeur vide ou la réflexion)
3. Remplit chaque attribut avec la valeur correspondante du JSON
4. Retourne l'objet Java complet

---

### 5.6 Écrire un objet dans un fichier JSON

```java
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import java.io.FileWriter;
import java.io.IOException;

public class GsonEcritureFichier {
    public static void main(String[] args) {

        Produit pizza = new Produit("Pizza Margherita", 12.99, "Pizza");

        Gson gson = new GsonBuilder().setPrettyPrinting().create();

        // On passe directement le FileWriter à toJson()
        // Gson écrit dans le fichier sans charger tout le JSON en mémoire d'abord
        try (FileWriter writer = new FileWriter("produit.json")) {
            gson.toJson(pizza, writer);
            System.out.println("Fichier produit.json créé !");
        } catch (IOException e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }
}
```

**Contenu du fichier produit.json :**
```json
{
  "nom": "Pizza Margherita",
  "prix": 12.99,
  "categorie": "Pizza"
}
```

---

### 5.7 Lire un objet depuis un fichier JSON

```java
import com.google.gson.Gson;
import java.io.File;
import java.io.FileReader;
import java.io.IOException;

public class GsonLectureFichier {
    public static void main(String[] args) {

        File fichier = new File("produit.json");
        if (!fichier.exists()) {
            System.out.println("Le fichier n'existe pas.");
            return;
        }

        Gson gson = new Gson();

        // On passe le FileReader à fromJson()
        // Gson lit directement depuis le fichier
        try (FileReader reader = new FileReader(fichier)) {
            Produit pizza = gson.fromJson(reader, Produit.class);
            System.out.println("Produit chargé : " + pizza);
        } catch (IOException e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }
}
```

---

### 5.8 Écrire et lire une liste d'objets

Pour sauvegarder une liste d'objets, le JSON ressemble à un tableau :

```json
[
  { "nom": "Pizza Margherita", "prix": 12.99, "categorie": "Pizza" },
  { "nom": "Coca-Cola", "prix": 2.99, "categorie": "Boisson" }
]
```

Le problème est que Gson a besoin de savoir le **type exact** de la liste pour la reconstruire. Pour cela, on utilise `TypeToken`.

```java
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.reflect.TypeToken;
import java.io.*;
import java.lang.reflect.Type;
import java.util.ArrayList;
import java.util.List;

public class GsonListeFichier {

    static final String FICHIER = "produits.json";

    public static void sauvegarder(List<Produit> produits) {
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        try (FileWriter writer = new FileWriter(FICHIER)) {
            gson.toJson(produits, writer);
            System.out.println("Liste de " + produits.size() + " produit(s) sauvegardée !");
        } catch (IOException e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }

    public static List<Produit> charger() {
        File fichier = new File(FICHIER);
        if (!fichier.exists()) {
            System.out.println("Aucun fichier JSON trouvé, liste vide.");
            return new ArrayList<>();
        }

        Gson gson = new Gson();

        // TypeToken est nécessaire pour indiquer à Gson le type générique List<Produit>
        // Sans cela, Gson ne saurait pas que c'est une liste de Produit
        // (et non une liste de Map ou autre chose)
        Type type = new TypeToken<List<Produit>>() {}.getType();

        try (FileReader reader = new FileReader(fichier)) {
            List<Produit> produits = gson.fromJson(reader, type);
            // fromJson peut retourner null si le fichier est vide
            if (produits == null) return new ArrayList<>();
            System.out.println(produits.size() + " produit(s) chargé(s).");
            return produits;
        } catch (IOException e) {
            System.out.println("Erreur : " + e.getMessage());
            return new ArrayList<>();
        }
    }

    public static void main(String[] args) {
        // Sauvegarder
        List<Produit> produits = new ArrayList<>();
        produits.add(new Produit("Pizza Margherita", 12.99, "Pizza"));
        produits.add(new Produit("Coca-Cola", 2.99, "Boisson"));
        produits.add(new Produit("Tiramisu", 6.99, "Dessert"));
        sauvegarder(produits);

        // Charger
        List<Produit> charger = charger();
        System.out.println("\nProduits chargés :");
        for (Produit p : charger) {
            System.out.println("  - " + p);
        }
    }
}
```

---

### 5.9 Écrire et lire un objet complexe imbriqué

Gson gère automatiquement les objets imbriqués. Une `Commande` qui contient une `List<Produit>` sera sérialisée correctement sans configuration supplémentaire.

```java
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import java.io.*;

public class GsonCommandeFichier {

    static final String FICHIER = "commande.json";

    public static void sauvegarder(Commande commande) {
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        try (FileWriter writer = new FileWriter(FICHIER)) {
            gson.toJson(commande, writer);
            System.out.println("Commande #" + commande.getId() + " sauvegardée !");
        } catch (IOException e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }

    public static Commande charger() {
        File fichier = new File(FICHIER);
        if (!fichier.exists()) {
            System.out.println("Aucune commande sauvegardée.");
            return null;
        }
        Gson gson = new Gson();
        try (FileReader reader = new FileReader(fichier)) {
            Commande commande = gson.fromJson(reader, Commande.class);
            System.out.println("Commande chargée !");
            return commande;
        } catch (IOException e) {
            System.out.println("Erreur : " + e.getMessage());
            return null;
        }
    }

    public static void main(String[] args) {
        Commande commande = new Commande(1, "Alice Tremblay");
        commande.ajouterProduit(new Produit("Pizza Margherita", 12.99, "Pizza"));
        commande.ajouterProduit(new Produit("Coca-Cola", 2.99, "Boisson"));
        commande.ajouterProduit(new Produit("Tiramisu", 6.99, "Dessert"));

        sauvegarder(commande);

        Commande commandeChargee = charger();
        if (commandeChargee != null) {
            System.out.println("\nClient : " + commandeChargee.getNomClient());
            System.out.println("Produits :");
            for (Produit p : commandeChargee.getItems()) {
                System.out.println("  - " + p);
            }
        }
    }
}
```

**Contenu du fichier commande.json :**
```json
{
  "id": 1,
  "nomClient": "Alice Tremblay",
  "items": [
    {
      "nom": "Pizza Margherita",
      "prix": 12.99,
      "categorie": "Pizza"
    },
    {
      "nom": "Coca-Cola",
      "prix": 2.99,
      "categorie": "Boisson"
    },
    {
      "nom": "Tiramisu",
      "prix": 6.99,
      "categorie": "Dessert"
    }
  ]
}
```

---

## 6. JSON avec Jackson

### Qu'est-ce que Jackson ?

**Jackson** est une autre bibliothèque Java très populaire pour travailler avec JSON. Elle est souvent utilisée dans les projets professionnels, notamment avec Spring Boot. Elle est généralement plus rapide que Gson sur de gros volumes de données.

La différence principale avec Gson est que Jackson suit les conventions JavaBeans : il a besoin de **getters**, de **setters** et d'un **constructeur sans arguments** pour fonctionner. C'est plus de code à écrire, mais c'est aussi plus explicite et plus contrôlable.

**Comparaison Gson vs Jackson :**

| Critère | Gson | Jackson |
|---|---|---|
| **Constructeur sans args** | Non requis | **Obligatoire** |
| **Getters/Setters** | Non requis | **Obligatoires** |
| **Configuration** | Minimale | Un peu plus |
| **Annotations** | Rarement nécessaires | Souvent utiles |
| **Performance** | Bonne | Meilleure |
| **Utilisation typique** | Projets simples | Spring Boot, projets pro |

---

### 6.1 Installation de Jackson

**Avec Maven** :
```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.16.1</version>
</dependency>
```

**Avec Gradle** :
```groovy
implementation 'com.fasterxml.jackson.core:jackson-databind:2.16.1'
```

---

### 6.2 Adapter les classes pour Jackson

Jackson lit et écrit les données via les **getters** et **setters**, et crée les objets via le **constructeur sans arguments**. Ces trois éléments sont **obligatoires**.

```java
public class Produit {
    private String nom;
    private double prix;
    private String categorie;

    // ✅ Constructeur sans arguments — OBLIGATOIRE pour Jackson
    // Jackson l'utilise pour créer l'objet avant de le remplir
    public Produit() {}

    // Constructeur complet pour notre code
    public Produit(String nom, double prix, String categorie) {
        this.nom = nom;
        this.prix = prix;
        this.categorie = categorie;
    }

    // ✅ Getters — Jackson les utilise pour lire les valeurs (Java → JSON)
    public String getNom()       { return nom; }
    public double getPrix()      { return prix; }
    public String getCategorie() { return categorie; }

    // ✅ Setters — Jackson les utilise pour remplir l'objet (JSON → Java)
    public void setNom(String nom)           { this.nom = nom; }
    public void setPrix(double prix)         { this.prix = prix; }
    public void setCategorie(String cat)     { this.categorie = cat; }

    @Override
    public String toString() {
        return nom + " (" + categorie + ") - " + prix + "$";
    }
}
```

> ⚠️ **Erreur fréquente :** Oublier le constructeur sans arguments. Jackson lancer une `InvalidDefinitionException` avec le message "No suitable constructor found". La solution est d'ajouter `public Produit() {}`.

> ⚠️ **Erreur fréquente :** Oublier un getter. Si Jackson ne trouve pas `getNom()`, il ignorera silencieusement le champ `nom` dans le JSON.

---

### 6.3 L'ObjectMapper — La classe principale de Jackson

`ObjectMapper` est la classe centrale de Jackson. C'est l'équivalent de `Gson` dans la bibliothèque Gson. On l'instancie une fois et on la réutilise.

```java
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.SerializationFeature;

// Création de l'ObjectMapper
ObjectMapper mapper = new ObjectMapper();

// Activer l'indentation (pretty print)
mapper.enable(SerializationFeature.INDENT_OUTPUT);
```

---

### 6.4 Objet Java → JSON (writeValue)

```java
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.SerializationFeature;

public class JacksonEcriture {
    public static void main(String[] args) {

        Produit pizza = new Produit("Pizza Margherita", 12.99, "Pizza");
        ObjectMapper mapper = new ObjectMapper();

        try {
            // writeValueAsString() : convertir en chaîne JSON
            String json = mapper.writeValueAsString(pizza);
            System.out.println("JSON compact : " + json);
            // {"nom":"Pizza Margherita","prix":12.99,"categorie":"Pizza"}

            // Avec indentation
            mapper.enable(SerializationFeature.INDENT_OUTPUT);
            String jsonJoli = mapper.writeValueAsString(pizza);
            System.out.println("\nJSON indenté :\n" + jsonJoli);

        } catch (Exception e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }
}
```

---

### 6.5 JSON → Objet Java (readValue)

```java
import com.fasterxml.jackson.databind.ObjectMapper;

public class JacksonLecture {
    public static void main(String[] args) {

        String json = "{\"nom\":\"Pizza Margherita\",\"prix\":12.99,\"categorie\":\"Pizza\"}";
        ObjectMapper mapper = new ObjectMapper();

        try {
            // readValue() : convertir une chaîne JSON en objet Java
            // Le deuxième argument indique à Jackson quelle classe créer
            Produit pizza = mapper.readValue(json, Produit.class);
            System.out.println("Produit lu : " + pizza);

        } catch (Exception e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }
}
```

---

### 6.6 Écrire et lire dans un fichier JSON

```java
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.SerializationFeature;
import java.io.File;

public class JacksonFichier {
    public static void main(String[] args) {

        Produit pizza = new Produit("Pizza Margherita", 12.99, "Pizza");
        ObjectMapper mapper = new ObjectMapper();
        mapper.enable(SerializationFeature.INDENT_OUTPUT);

        try {
            // --- Écriture ---
            // writeValue() écrit directement dans un File
            mapper.writeValue(new File("produit_jackson.json"), pizza);
            System.out.println("Fichier créé !");

            // --- Lecture ---
            // readValue() lit directement depuis un File
            Produit chargee = mapper.readValue(new File("produit_jackson.json"), Produit.class);
            System.out.println("Produit chargé : " + chargee);

        } catch (Exception e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }
}
```

---

### 6.7 Écrire et lire une liste d'objets

Comme avec Gson, il faut indiquer le type exact de la liste. Jackson utilise `TypeReference` à la place du `TypeToken` de Gson.

```java
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.SerializationFeature;
import com.fasterxml.jackson.core.type.TypeReference;
import java.io.File;
import java.util.ArrayList;
import java.util.List;

public class JacksonListeFichier {

    static final String FICHIER = "produits_jackson.json";
    static ObjectMapper mapper = new ObjectMapper();

    public static void sauvegarder(List<Produit> produits) {
        mapper.enable(SerializationFeature.INDENT_OUTPUT);
        try {
            mapper.writeValue(new File(FICHIER), produits);
            System.out.println("Liste sauvegardée (" + produits.size() + " produits)");
        } catch (Exception e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }

    public static List<Produit> charger() {
        File fichier = new File(FICHIER);
        if (!fichier.exists()) {
            System.out.println("Aucun fichier trouvé, liste vide.");
            return new ArrayList<>();
        }

        try {
            // TypeReference est l'équivalent Jackson du TypeToken de Gson
            // Il indique à Jackson que c'est une List<Produit> et non juste une List
            List<Produit> produits = mapper.readValue(
                fichier,
                new TypeReference<List<Produit>>() {}
            );
            System.out.println(produits.size() + " produit(s) chargé(s).");
            return produits;
        } catch (Exception e) {
            System.out.println("Erreur : " + e.getMessage());
            return new ArrayList<>();
        }
    }

    public static void main(String[] args) {
        List<Produit> produits = new ArrayList<>();
        produits.add(new Produit("Pizza Margherita", 12.99, "Pizza"));
        produits.add(new Produit("Coca-Cola", 2.99, "Boisson"));
        produits.add(new Produit("Tiramisu", 6.99, "Dessert"));

        sauvegarder(produits);

        List<Produit> charger = charger();
        for (Produit p : charger) System.out.println("  - " + p);
    }
}
```

---

### 6.8 Les annotations Jackson utiles

Les annotations permettent de **personnaliser** la sérialisation sans modifier la logique de la classe.

```java
import com.fasterxml.jackson.annotation.JsonProperty;
import com.fasterxml.jackson.annotation.JsonIgnore;
import com.fasterxml.jackson.annotation.JsonIgnoreProperties;

// Ignorer les champs inconnus dans le JSON (utile si le JSON vient d'une API externe)
@JsonIgnoreProperties(ignoreUnknown = true)
public class Produit {

    // Renommer le champ dans le JSON
    // Le JSON contiendra "name" au lieu de "nom"
    @JsonProperty("name")
    private String nom;

    private double prix;

    // Ce champ ne sera PAS inclus dans le JSON (ni en lecture ni en écriture)
    @JsonIgnore
    private String motDePasseAdmin;

    public Produit() {}

    // getters et setters...
}
```

**JSON généré :**
```json
{
  "name": "Pizza Margherita",
  "prix": 12.99
}
```

---

### 6.9 Tableau récapitulatif Gson vs Jackson

| Fonctionnalité | Gson | Jackson |
|---|---|---|
| **Constructeur sans args** | Non requis | **Obligatoire** |
| **Getters/Setters** | Non requis | **Obligatoires** |
| **Créer l'instance** | `new Gson()` | `new ObjectMapper()` |
| **Pretty print** | `.setPrettyPrinting().create()` | `.enable(INDENT_OUTPUT)` |
| **Objet → String JSON** | `gson.toJson(objet)` | `mapper.writeValueAsString(obj)` |
| **String JSON → Objet** | `gson.fromJson(json, Classe.class)` | `mapper.readValue(json, Classe.class)` |
| **Objet → Fichier** | `gson.toJson(objet, writer)` | `mapper.writeValue(new File(...), obj)` |
| **Fichier → Objet** | `gson.fromJson(reader, Classe.class)` | `mapper.readValue(new File(...), Cl.class)` |
| **Type pour List** | `TypeToken<List<T>>` | `TypeReference<List<T>>` |

---

## 7. Mini-projets

---

### Mini-projet 1 — Carnet de contacts (fichier texte)

**Objectif** : Créer un carnet de contacts persistant qui sauvegarde les données dans un fichier texte `.txt` entre chaque exécution du programme.

**Contexte** : L'application doit fonctionner comme suit — au démarrage, elle charge automatiquement les contacts depuis le fichier s'il existe. L'utilisateur peut ajouter des contacts. À la fin, les contacts sont sauvegardés dans le fichier. Au prochain démarrage, les contacts sont rechargés.

---

#### Classe `Contact`

Crée une classe `Contact` avec les attributs suivants :
- `nom` (String)
- `telephone` (String)
- `email` (String)

La classe doit pouvoir :
- Être construite avec les trois attributs
- Se **convertir en une ligne de texte** au format `nom;telephone;email` (ex: `Alice Tremblay;514-555-0001;alice@email.com`) — cette ligne sera écrite dans le fichier
- Être **recréée depuis une ligne de texte** : une méthode statique reçoit une ligne `"Alice Tremblay;514-555-0001;alice@email.com"`, la découpe avec `split(";")` et retourne un objet `Contact`
- Avoir un `toString()` lisible

> 💡 **Indice :** Pour découper une ligne en plusieurs parties, utilise `String[] parties = ligne.split(";")`. `parties[0]` sera le nom, `parties[1]` le téléphone, `parties[2]` l'email.

---

#### Classe `CarnetContacts`

Crée une classe `CarnetContacts` avec :
- Un attribut `contacts` de type `List<Contact>`, initialisé à une `ArrayList` vide
- Une constante `FICHIER = "contacts.txt"` qui indique le nom du fichier

La classe doit avoir les méthodes suivantes :

**`ajouter(Contact c)`**
- Ajoute le contact à la liste en mémoire
- Affiche un message de confirmation

**`afficher()`**
- Si la liste est vide, affiche "Aucun contact."
- Sinon, affiche tous les contacts avec `System.out.println`

**`sauvegarder()`**
- Ouvre le fichier `contacts.txt` en écriture avec `PrintWriter`
- Pour chaque contact dans la liste, écrit une ligne avec `contact.versLigne()`
- Affiche le nombre de contacts sauvegardés
- Gère les exceptions avec try-catch

**`charger()`**
- Vérifie si le fichier existe avec `new File(FICHIER).exists()`. Si non, affiche un message et retourne sans erreur
- Vide la liste en mémoire avant de charger
- Lit le fichier ligne par ligne avec `BufferedReader`
- Pour chaque ligne, crée un `Contact` avec `Contact.depuisLigne(ligne)` et l'ajoute à la liste
- Affiche le nombre de contacts chargés
- Gère les exceptions avec try-catch

---

#### Dans le `main`

1. Créer un `CarnetContacts`
2. Appeler `charger()` pour charger les contacts existants
3. Afficher les contacts chargés
4. Ajouter 3 nouveaux contacts
5. Afficher tous les contacts
6. Appeler `sauvegarder()`
7. Créer un **deuxième** `CarnetContacts`, appeler `charger()` dessus et afficher les contacts pour confirmer que la sauvegarde a bien fonctionné

<details>
<summary>💡 Solution</summary>

**Classe Contact :**
```java
public class Contact {
    private String nom;
    private String telephone;
    private String email;

    public Contact(String nom, String telephone, String email) {
        this.nom = nom;
        this.telephone = telephone;
        this.email = email;
    }

    public String versLigne() {
        return nom + ";" + telephone + ";" + email;
    }

    public static Contact depuisLigne(String ligne) {
        String[] parties = ligne.split(";");
        return new Contact(parties[0], parties[1], parties[2]);
    }

    @Override
    public String toString() {
        return "Contact{nom='" + nom + "', tel='" + telephone + "', email='" + email + "'}";
    }

    public String getNom() { return nom; }
}
```

**Classe CarnetContacts :**
```java
import java.io.*;
import java.util.ArrayList;
import java.util.List;

public class CarnetContacts {

    static final String FICHIER = "contacts.txt";
    private List<Contact> contacts = new ArrayList<>();

    public void ajouter(Contact c) {
        contacts.add(c);
        System.out.println("Contact ajouté : " + c.getNom());
    }

    public void afficher() {
        if (contacts.isEmpty()) {
            System.out.println("Aucun contact.");
            return;
        }
        for (Contact c : contacts) {
            System.out.println(c);
        }
    }

    public void sauvegarder() {
        try (PrintWriter writer = new PrintWriter(new FileWriter(FICHIER))) {
            for (Contact c : contacts) {
                writer.println(c.versLigne());
            }
            System.out.println(contacts.size() + " contact(s) sauvegardé(s).");
        } catch (IOException e) {
            System.out.println("Erreur de sauvegarde : " + e.getMessage());
        }
    }

    public void charger() {
        contacts.clear();
        File fichier = new File(FICHIER);
        if (!fichier.exists()) {
            System.out.println("Aucun fichier de contacts trouvé.");
            return;
        }
        try (BufferedReader reader = new BufferedReader(new FileReader(FICHIER))) {
            String ligne;
            while ((ligne = reader.readLine()) != null) {
                contacts.add(Contact.depuisLigne(ligne));
            }
            System.out.println(contacts.size() + " contact(s) chargé(s).");
        } catch (IOException e) {
            System.out.println("Erreur de chargement : " + e.getMessage());
        }
    }

    public static void main(String[] args) {
        CarnetContacts carnet = new CarnetContacts();
        carnet.charger();

        System.out.println("Contacts existants :");
        carnet.afficher();

        carnet.ajouter(new Contact("Alice Tremblay", "514-555-0001", "alice@email.com"));
        carnet.ajouter(new Contact("Bob Martin", "438-555-0002", "bob@email.com"));
        carnet.ajouter(new Contact("Claire Dupont", "450-555-0003", "claire@email.com"));

        System.out.println("\nTous les contacts :");
        carnet.afficher();

        carnet.sauvegarder();

        System.out.println("\nSimulation d'un redémarrage :");
        CarnetContacts carnet2 = new CarnetContacts();
        carnet2.charger();
        carnet2.afficher();
    }
}
```

</details>

---

### Mini-projet 2 — Gestionnaire de produits (JSON avec Gson)

**Objectif** : Créer un gestionnaire de produits qui sauvegarde et charge une liste de produits au format JSON en utilisant Gson. Les données doivent survivre entre deux exécutions du programme.

**Contexte** : L'application charge la liste existante au démarrage, permet d'ajouter et retirer des produits, recalcule automatiquement le total, et sauvegarde la liste mise à jour à la fin.

---

#### Classe `Produit`

Utilise la classe `Produit` avec `nom`, `prix` et `categorie`. Assure-toi d'avoir des getters.

> ⚠️ **Rappel Gson :** Pas besoin de constructeur sans args ni de setters — Gson accède directement aux champs privés.

---

#### Classe `GestionnaireProduits`

Crée une classe `GestionnaireProduits` avec :
- Un attribut `produits` de type `List<Produit>`, initialisé à une `ArrayList` vide
- Un attribut `gson` de type `Gson`, créé avec `new GsonBuilder().setPrettyPrinting().create()`
- Une constante `FICHIER = "produits.json"`

La classe doit avoir les méthodes suivantes :

**`ajouter(Produit p)`**
- Ajoute le produit à la liste
- Affiche un message de confirmation avec le produit ajouté

**`retirer(String nom)`**
- Retire le premier produit dont le nom correspond (insensible à la casse)
- Utilise `removeIf` avec une lambda : `produits.removeIf(p -> p.getNom().equalsIgnoreCase(nom))`
- Affiche un message de confirmation

**`calculerTotal()`**
- Parcourt la liste et additionne tous les prix
- Retourne le total en `double`

**`afficher()`**
- Si la liste est vide, affiche "Aucun produit."
- Sinon affiche chaque produit avec son prix, et le total à la fin

**`sauvegarder()`**
- Ouvre un `FileWriter` sur le fichier JSON
- Appelle `gson.toJson(produits, writer)` pour écrire la liste
- Affiche un message de confirmation
- Gère les exceptions

**`charger()`**
- Vérifie si le fichier existe. Sinon, retourne sans erreur
- Utilise `TypeToken<List<Produit>>` pour indiquer à Gson le type de la liste
- Lit avec `FileReader` et appelle `gson.fromJson(reader, type)`
- Si le résultat est `null`, initialise une liste vide
- Affiche le nombre de produits chargés

---

#### Dans le `main`

1. Créer un `GestionnaireProduits`
2. Charger les données existantes
3. Afficher les produits chargés avec le total
4. Ajouter 3 produits : une pizza, une boisson, un dessert
5. Afficher la liste mise à jour avec le total
6. Retirer un produit par son nom
7. Afficher la liste finale avec le nouveau total
8. Sauvegarder
9. Créer un **deuxième** `GestionnaireProduits`, charger et afficher pour confirmer

<details>
<summary>💡 Solution</summary>

```java
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.reflect.TypeToken;
import java.io.*;
import java.lang.reflect.Type;
import java.util.ArrayList;
import java.util.List;

public class GestionnaireProduits {

    static final String FICHIER = "produits.json";
    private List<Produit> produits = new ArrayList<>();
    private Gson gson = new GsonBuilder().setPrettyPrinting().create();

    public void ajouter(Produit p) {
        produits.add(p);
        System.out.println("Ajouté : " + p);
    }

    public void retirer(String nom) {
        produits.removeIf(p -> p.getNom().equalsIgnoreCase(nom));
        System.out.println("Produit '" + nom + "' retiré.");
    }

    public double calculerTotal() {
        double total = 0;
        for (Produit p : produits) total += p.getPrix();
        return total;
    }

    public void afficher() {
        if (produits.isEmpty()) {
            System.out.println("Aucun produit.");
            return;
        }
        System.out.println("=== Liste des produits ===");
        for (Produit p : produits) {
            System.out.println("  - " + p);
        }
        System.out.printf("Total : %.2f$%n", calculerTotal());
    }

    public void sauvegarder() {
        try (FileWriter writer = new FileWriter(FICHIER)) {
            gson.toJson(produits, writer);
            System.out.println("Sauvegardé dans " + FICHIER);
        } catch (IOException e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }

    public void charger() {
        File fichier = new File(FICHIER);
        if (!fichier.exists()) {
            System.out.println("Aucun fichier JSON trouvé.");
            return;
        }
        Type type = new TypeToken<List<Produit>>() {}.getType();
        try (FileReader reader = new FileReader(fichier)) {
            produits = gson.fromJson(reader, type);
            if (produits == null) produits = new ArrayList<>();
            System.out.println(produits.size() + " produit(s) chargé(s).");
        } catch (IOException e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }

    public static void main(String[] args) {
        GestionnaireProduits g = new GestionnaireProduits();

        g.charger();
        System.out.println("Au démarrage :");
        g.afficher();

        g.ajouter(new Produit("Pizza Margherita", 12.99, "Pizza"));
        g.ajouter(new Produit("Coca-Cola", 2.99, "Boisson"));
        g.ajouter(new Produit("Tiramisu", 6.99, "Dessert"));

        System.out.println("\nAprès ajouts :");
        g.afficher();

        g.retirer("Coca-Cola");

        System.out.println("\nAprès retrait :");
        g.afficher();

        g.sauvegarder();

        System.out.println("\nSimulation d'un redémarrage :");
        GestionnaireProduits g2 = new GestionnaireProduits();
        g2.charger();
        g2.afficher();
    }
}
```

</details>

---

### Mini-projet 3 — Sauvegarde de commandes (JSON avec Jackson)

**Objectif** : Créer un système qui sauvegarde et charge plusieurs commandes au format JSON en utilisant Jackson. Chaque commande contient une liste de produits.

**Contexte** : L'application permet de créer des commandes pour différents clients, les sauvegarde toutes dans un seul fichier JSON, et peut les recharger au prochain démarrage.

---

#### Adapter les classes pour Jackson

Avant de commencer, tu dois t'assurer que tes classes `Produit` et `Commande` sont compatibles avec Jackson :

**Pour `Produit` :**
- Ajouter un constructeur sans arguments `public Produit() {}`
- Ajouter des setters pour tous les attributs : `setNom()`, `setPrix()`, `setCategorie()`
- Les getters et `toString()` existants restent inchangés

**Pour `Commande` :**
- Ajouter un constructeur sans arguments `public Commande() {}`
- Ajouter des setters : `setId()`, `setNomClient()`, `setItems()`
- Garder le constructeur complet et la méthode `ajouterProduit()`

> ⚠️ **Rappel Jackson :** Sans constructeur sans arguments, Jackson lance une erreur `InvalidDefinitionException`. Sans setters, les champs resteront à leur valeur par défaut lors du chargement.

---

#### Classe `GestionnaireCommandes`

Crée une classe `GestionnaireCommandes` avec :
- Un attribut `commandes` de type `List<Commande>`, initialisé à une `ArrayList` vide
- Un attribut `mapper` de type `ObjectMapper`, configuré avec `INDENT_OUTPUT`
- Une constante `FICHIER = "commandes.json"`

La classe doit avoir les méthodes suivantes :

**`ajouterCommande(Commande c)`**
- Ajoute la commande à la liste
- Affiche l'id et le nom du client

**`calculerTotalCommande(Commande c)`**
- Parcourt les produits de la commande et retourne le total en `double`

**`afficher()`**
- Si la liste est vide, affiche "Aucune commande."
- Pour chaque commande, affiche l'id, le nom du client, la liste des produits et le total calculé avec `calculerTotalCommande()`

**`sauvegarder()`**
- Utilise `mapper.writeValue(new File(FICHIER), commandes)`
- Affiche un message de confirmation
- Gère les exceptions avec try-catch

**`charger()`**
- Vérifie si le fichier existe. Sinon, retourne sans erreur
- Utilise `new TypeReference<List<Commande>>() {}` pour indiquer le type à Jackson
- Appelle `mapper.readValue(fichier, typeRef)`
- Affiche le nombre de commandes chargées

---

#### Dans le `main`

1. Créer un `GestionnaireCommandes`
2. Charger les commandes existantes
3. Afficher les commandes chargées
4. Créer la commande 1 pour "Alice Tremblay" avec 2 produits
5. Créer la commande 2 pour "Bob Martin" avec 2 produits différents
6. Ajouter les deux commandes au gestionnaire
7. Afficher toutes les commandes avec leurs totaux
8. Sauvegarder
9. Simuler un redémarrage : créer un nouveau gestionnaire, charger et afficher

<details>
<summary>💡 Solution</summary>

> ⚠️ Les classes `Produit` et `Commande` doivent avoir un constructeur sans args et des setters.

```java
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.SerializationFeature;
import com.fasterxml.jackson.core.type.TypeReference;
import java.io.File;
import java.util.ArrayList;
import java.util.List;

public class GestionnaireCommandes {

    static final String FICHIER = "commandes.json";
    private List<Commande> commandes = new ArrayList<>();
    private ObjectMapper mapper = new ObjectMapper();

    public GestionnaireCommandes() {
        mapper.enable(SerializationFeature.INDENT_OUTPUT);
    }

    public void ajouterCommande(Commande c) {
        commandes.add(c);
        System.out.println("Commande #" + c.getId() + " ajoutée pour " + c.getNomClient());
    }

    public double calculerTotalCommande(Commande c) {
        double total = 0;
        for (Produit p : c.getItems()) total += p.getPrix();
        return total;
    }

    public void afficher() {
        if (commandes.isEmpty()) {
            System.out.println("Aucune commande.");
            return;
        }
        System.out.println("=== Toutes les commandes ===");
        for (Commande c : commandes) {
            System.out.printf("Commande #%d — %s%n", c.getId(), c.getNomClient());
            for (Produit p : c.getItems()) {
                System.out.println("    - " + p);
            }
            System.out.printf("    Total : %.2f$%n", calculerTotalCommande(c));
        }
    }

    public void sauvegarder() {
        try {
            mapper.writeValue(new File(FICHIER), commandes);
            System.out.println("Commandes sauvegardées dans " + FICHIER);
        } catch (Exception e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }

    public void charger() {
        File fichier = new File(FICHIER);
        if (!fichier.exists()) {
            System.out.println("Aucun fichier trouvé.");
            return;
        }
        try {
            commandes = mapper.readValue(fichier, new TypeReference<List<Commande>>() {});
            System.out.println(commandes.size() + " commande(s) chargée(s).");
        } catch (Exception e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }

    public static void main(String[] args) {
        GestionnaireCommandes g = new GestionnaireCommandes();

        g.charger();
        System.out.println("Au démarrage :");
        g.afficher();

        Commande cmd1 = new Commande(1, "Alice Tremblay");
        cmd1.ajouterProduit(new Produit("Pizza Margherita", 12.99, "Pizza"));
        cmd1.ajouterProduit(new Produit("Coca-Cola", 2.99, "Boisson"));

        Commande cmd2 = new Commande(2, "Bob Martin");
        cmd2.ajouterProduit(new Produit("Pepperoni", 14.99, "Pizza"));
        cmd2.ajouterProduit(new Produit("Tiramisu", 6.99, "Dessert"));

        g.ajouterCommande(cmd1);
        g.ajouterCommande(cmd2);

        System.out.println("\nAprès ajouts :");
        g.afficher();

        g.sauvegarder();

        System.out.println("\nSimulation d'un redémarrage :");
        GestionnaireCommandes g2 = new GestionnaireCommandes();
        g2.charger();
        g2.afficher();
    }
}
```

</details>

---

### Résumé — Quand utiliser quoi ?

| Situation | Solution recommandée |
|---|---|
| Données simples (liste de noms, scores) | Fichier texte `.txt` avec `PrintWriter` / `BufferedReader` |
| Données structurées à partager | JSON avec **Gson** (simple) ou **Jackson** (professionnel) |
| Objets Java (usage interne Java seulement) | Sérialisation binaire avec `ObjectOutputStream` |
| Projet Spring Boot | **Jackson** (intégré par défaut) |
| Projet simple ou cours débutant | **Gson** (moins de configuration) |
| Données partagées entre plusieurs langages | **JSON** (universel) |