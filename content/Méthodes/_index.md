+++
title = "Méthodes"
weight = 5
url = "/methodes/"

+++

# 🛠️ Les Méthodes en Java : Segmenter pour mieux régner

En programmation, une méthode est un **bloc de code nommé** qui contient une séquence d'instructions. Au lieu d'écrire tout votre code dans le bloc principal (`main`), vous créez des unités de travail spécialisées que vous pouvez appeler au besoin.

> **L'analogie de la boîte** : Imaginez une méthode comme une boîte fermée. Vous ne voyez pas forcément l'engrenage à l'intérieur, mais vous savez comment l'utiliser en appuyant sur un bouton ou en y insérant des données.

---

## 1. La boîte d'action simple (`void` sans paramètre)

Il s'agit du type de méthode le plus élémentaire. Elle ne demande aucune information et ne renvoie aucune donnée. Elle exécute simplement une tâche prédéfinie.

* **`void`** : Ce mot-clé signifie "vide". Il indique que la méthode ne rend rien au programme.
* **`()`** : Les parenthèses vides indiquent que la boîte ne nécessite aucune donnée d'entrée pour fonctionner.

```java
public static void afficherEntete() {
    System.out.println("******************************");
    System.out.println("   BIENVENUE AU SYSTÈME      ");
    System.out.println("******************************");
}
```
---

---

## 2. La boîte avec instructions (`void` avec paramètres)

Cette méthode a besoin d'informations pour fonctionner (des paramètres), mais elle ne renvoie toujours pas de résultat au programme. Elle utilise les entrées pour effectuer une action, comme un affichage personnalisé.

* **Paramètres** : Ce sont les variables déclarées entre les parenthèses. Elles servent de "fiches d'instructions" pour la méthode.



```java
public static void saluerUtilisateur(String prenom, int age) {
    System.out.println("Bonjour " + prenom + " !");
    System.out.println("Vous avez " + age + " ans.");
}
```

---

## 3. La boîte de calcul (Avec paramètres et retour)

C'est l'analogie complète de la **machine distributrice** :
1.  Vous insérez des données (l'argent) : ce sont les **Paramètres**.
2.  La machine transforme l'entrée : c'est le **Traitement**.
3.  Elle vous éjecte un produit (le bonbon) : c'est le **Retour**.

* **Type de retour** : On remplace `void` par le type de la donnée qui sortira de la boîte (ex: `int`, `double`, `String`).
* **Instruction `return`** : C'est le mécanisme qui permet d'expulser la valeur finale hors de la méthode.



```java
public static double calculerTaxe(double montantBrut) {
    double taxe = montantBrut * 0.15; // Calcul de la taxe de 15%
    return taxe; // On éjecte le résultat vers l'appelant
}
```
---

## 4. Synthèse : Quel type de boîte choisir ?

Pour déterminer la structure de votre méthode, vous devez vous poser deux questions fondamentales avant même de commencer à coder.

### Le guide de décision
1. **Entrée (Paramètres) :** Est-ce que ma machine a besoin de données extérieures pour fonctionner ?
2. **Sortie (Retour) :** Est-ce que ma machine doit fournir une réponse que je vais réutiliser plus tard dans mon code ?



### Tableau récapitulatif des structures

| Type de méthode | Type de retour | Paramètres | Analogie de la boîte |
| :--- | :--- | :--- | :--- |
| **Action pure** | `void` | Aucun `()` | **Le bouton "Alarme"** : on appuie, le son sort, aucune information n'est demandée. |
| **Action paramétrée** | `void` | Présents | **Le haut-parleur** : on lui donne un texte, il le diffuse, mais il ne nous redonne rien en main. |
| **Calculatrice** | `int`, `double`, etc. | Présents | **La machine distributrice** : on insère de l'argent, la machine traite, et nous redonne un produit. |

---

### 💡 La règle d'or : "Une tâche, une boîte"
Une erreur fréquente est de vouloir créer une boîte qui fait trop de choses (ex: calculer, afficher, et sauvegarder). 

* **Mauvaise pratique :** Une méthode géante difficile à corriger.
* **Bonne pratique :** Plusieurs petites méthodes simples qui s'appellent entre elles. Cela rend votre code modulaire et beaucoup plus facile à déboguer pour vos travaux pratiques.

## 5. Exemples supplémentaires par mise en situation

### A. La boîte "Vérificatrice" (Type boolean)
Cette boîte reçoit une information et répond simplement par **Vrai** ou **Faux**. C'est très utile pour valider des conditions de jeu.

* **Entrée** : L'âge de l'utilisateur.
* **Sortie** : Un signal (Vrai/Faux) indiquant si l'accès est permis.

```java
public static boolean estMajeur(int age) {
    if (age >= 18) {
        return true;
    } else {
        return false;
    }
}
```