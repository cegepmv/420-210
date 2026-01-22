+++
title = "Introduction"
type = "chapter"
weight = 1
url = "/1-intro/"

+++

## 1. Qu'est-ce que Java ?

Java est à la fois un **langage de programmation orienté objet** et une **plateforme informatique**. Sa philosophie principale est le **WORA** (*Write Once, Run Anywhere*) : écrivez votre code une fois, et exécutez-le n'importe où sans modification.

### Les trois piliers de Java : JDK, JRE et JVM

Pour comprendre comment Java fonctionne, il faut distinguer ces trois composants essentiels :

* **JDK (Java Development Kit)** : C'est la boîte à outils complète pour le développeur. Elle contient le compilateur (`javac`), les bibliothèques de base et le JRE.
* **JRE (Java Runtime Environment)** : C'est l'environnement nécessaire pour **exécuter** un programme Java. Il contient les bibliothèques de classes et la JVM.
* **JVM (Java Virtual Machine)** : C'est le cœur du système. Elle interprète le "Bytecode" pour que l'ordinateur puisse le comprendre.

> 🔗 **Ressource complémentaire :** <a href="https://datascientest.com/langage-java-tout-savoir" target="_blank">Java : Les fondamentaux expliqués (JDK, JRE et JVM)</a>

---

## 2. Caractéristiques principales du langage

* **Orienté Objet (POO)** : Tout est considéré comme un "objet" (une entité avec des caractéristiques et des comportements).
* **Gestion automatique de la mémoire** : Grâce au **Garbage Collector** (Ramasse-miettes), Java libère automatiquement la mémoire inutilisée.
* **Sécurité** : Conçu pour les environnements réseaux, il possède des barrières strictes contre les accès mémoire non autorisés.
* **Multi-thread** : Java permet d'exécuter plusieurs parties d'un programme simultanément.

---

## 3. Installation, compilation et exécution

### Installation
Vous devez installer un **JDK** (comme OpenJDK ou Oracle JDK). Vérifiez l'installation avec la commande :
`java -version`

### Compilation et exécution d’un programme Java

D'abord, tu dois t'assurer que Java est bien installé sur ton ordinateur
* Ouvre une invite de commandes (cmd) sous Windows (Terminal sous Mac/Linux).
* Tape la commande `java -version`. Cette commande devrait vous dire la version de Java qui est installé sur votre ordinateur.
* Tape aussi la commande `javac -version`. Cette commande devrait te dire la version du compilateur de Java installé sur ton ordinateur
_Note: Ces commandes fonctionnent seulement si Java et le compilateur de Java sont installés et que le chemin où le répertoire de Java se trouve est mis dans le `PATH` des variables d'environnement (À expliquer en classe pour que ce soit plus clair)_

### Exécution du code dans le fichier Main.java
* Ouvre une invite de commandes (cmd) sous Windows (Terminal sous Mac/Linux).
* Navigue vers le dossier où se trouve votre fichier .java
* Exécute la commande `java Main.java`.

Traditionnellement, Java fonctionne en deux étapes :

1. **Compilation** : Le code source (`.java`) est transformé en bytecode (`.class`) grâce à la commande :

   ```bash
   javac Main.java
   ```

2. **Exécution** : Le bytecode est ensuite exécuté avec la commande :

   ```bash
   java Main
   ```

> 💡 *Astuce : Depuis une version relativement récente de Java, il est aussi possible d’exécuter directement un fichier `.java` sans passer explicitement par l’étape de compilation (`javac`).*

```bash
java Main.java
```

Cela permet d’exécuter rapidement un programme, mais à noter :

* Le fichier `.class` est **généré temporairement**.
* Il est ensuite **supprimé automatiquement** après l’exécution.

> 📝 Cette méthode est pratique pour tester du code rapidement, mais dans un projet structuré, on utilise généralement `javac` suivi de `java`.
---
### Compilation et exécution sans le PATH configuré

Si vous recevez l'erreur : `'javac' n'est pas reconnu en tant que commande interne...`, cela signifie que votre système ne sait pas où se trouve le dossier `bin` du JDK. Vous devez alors utiliser le **chemin absolu**.


1. **Compiler le fichier**:  Il faut appeler l'exécutable `javac` directement.
* ***Sur Windows*** : 
    ```cmd
    "C:\Program Files\Java\jdk-21\bin\javac" Main.java
    ```
* ***Sur macOS / Linux*** :
    ```bash
    /usr/lib/jvm/jdk-21/bin/javac Main.java
    ```
*Résultat : Un fichier `Main.class` apparaît dans votre dossier.*

2. **Exécuter le programme** : Il faut appeler l'exécutable `java` (la JVM).
* **Sur Windows** : 
    ```cmd
    "C:\Program Files\Java\jdk-21\bin\java" Main
    ```
* **Sur macOS / Linux** :
    ```bash
    /usr/lib/jvm/jdk-21/bin/java Main
    ```

---

### Résoudre l'erreur de Classpath (`-cp`)

C'est l'erreur la plus frustrante pour les débutants : `Could not find or load main class`. Cela arrive quand la JVM ne sait pas **où chercher** vos fichiers `.class`.

###### L'option `-cp` (ou `-classpath`)
Cette option force Java à regarder dans des répertoires précis.

* **Chercher dans le dossier actuel (`.`)** :
    ```bash
    java -cp . Main
    ```
* **Chercher dans un dossier spécifique (ex: `bin`)** :
    ```bash
    java -cp bin Main
    ```
* **Chercher dans plusieurs dossiers ou JARs** :
    * *Windows* : `java -cp ".;lib/mysql.jar" Main` (séparateur `;`)
    * *Linux/Mac* : `java -cp .:lib/mysql.jar Main` (séparateur `:`)

---

## 4. Les outils de développement (IDE)

Bien que vous puissiez écrire du Java dans un simple bloc-notes, les développeurs utilisent des **IDE** (Environnements de Développement Intégrés) pour être plus efficaces. Ces logiciels regroupent l'édition de code, la compilation automatique et le débogage.

| IDE | Points forts |
| :--- | :--- |
| **IntelliJ IDEA** | Développé par JetBrains. C'est le plus moderne et le plus intelligent (recommandé pour la productivité). |
| **Eclipse** | Historique, entièrement gratuit et open-source. Très utilisé dans les grandes entreprises. |
| **VS Code** | Très léger et polyvalent. Nécessite l'installation du "Java Extension Pack" pour fonctionner. |