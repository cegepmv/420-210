+++
title = "Java FX"
weight = 14
+++
# Notes de cours — JavaFX avec SceneBuilder

---

## Table des matières

1. [Introduction à JavaFX et SceneBuilder](#1-introduction-à-javafx-et-scenebuilder)
2. [Structure d'un projet JavaFX](#2-structure-dun-projet-javafx)
3. [Mise en page — Layouts](#3-mise-en-page--layouts)
4. [Les composants de base](#4-les-composants-de-base)
5. [FXML et lien avec le contrôleur](#5-fxml-et-lien-avec-le-contrôleur)
6. [Les événements et handlers](#6-les-événements-et-handlers)
7. [Exercices pratiques](#7-exercices-pratiques)

---

## 1. Introduction à JavaFX et SceneBuilder

### Qu'est-ce que JavaFX ?

JavaFX est une bibliothèque Java qui permet de créer des **interfaces graphiques** (GUI — Graphical User Interface). C'est ce qui permet de créer des fenêtres, des boutons, des champs de texte, etc.

Avant JavaFX, il y avait Swing. JavaFX est plus moderne et plus facile à utiliser.

### Qu'est-ce que SceneBuilder ?

SceneBuilder est un outil visuel qui permet de **concevoir l'interface graphique par glisser-déposer**, sans écrire de code. Il génère automatiquement un fichier **FXML** qui décrit l'interface.

```
SceneBuilder  →  génère un fichier  →  HelloView.fxml
```

### Les concepts clés

| Concept | Description |
|---|---|
| **Stage** | La fenêtre principale de l'application |
| **Scene** | Le contenu affiché dans la fenêtre |
| **Node** | Tout élément visuel (bouton, label, image...) |
| **FXML** | Fichier XML qui décrit l'interface graphique |
| **Controller** | Classe Java qui gère les événements de l'interface |

### Le modèle MVC dans JavaFX

JavaFX suit le patron de conception **MVC (Modèle - Vue - Contrôleur)** :

```
Vue (fichier .fxml)  ←→  Contrôleur (fichier .java)  ←→  Modèle (classes Java)
```

- La **Vue** définit l'apparence (ce qu'on voit)
- Le **Contrôleur** gère les actions (ce qui se passe quand on clique)
- Le **Modèle** contient les données (la logique métier)

### Installation

1. Télécharger **SceneBuilder** : https://gluonhq.com/products/scene-builder/
2. Dans **IntelliJ IDEA** : `File → Settings → Languages & Frameworks → JavaFX → Path to SceneBuilder`
3. Créer un nouveau projet JavaFX dans IntelliJ

---

## 2. Structure d'un projet JavaFX

### Arborescence typique

```
MonProjet/
├── src/
│   └── main/
│       ├── java/
│       │   └── com/exemple/
│       │       ├── MainApp.java          ← Point d'entrée
│       │       └── HelloController.java  ← Contrôleur
│       └── resources/
│           └── com/exemple/
│               └── hello-view.fxml       ← Vue (SceneBuilder)
└── pom.xml (ou build.gradle)
```

### La classe principale — MainApp.java

C'est le point d'entrée de toute application JavaFX. Elle doit étendre `Application` et implémenter la méthode `start()`.

```java
import javafx.application.Application;
import javafx.fxml.FXMLLoader;
import javafx.scene.Scene;
import javafx.stage.Stage;
import java.io.IOException;

public class MainApp extends Application {

    @Override
    public void start(Stage stage) throws IOException {
        // Charger le fichier FXML
        FXMLLoader fxmlLoader = new FXMLLoader(MainApp.class.getResource("hello-view.fxml"));

        // Créer la scène avec une taille de 400x300
        Scene scene = new Scene(fxmlLoader.load(), 400, 300);

        // Configurer la fenêtre
        stage.setTitle("Mon Application");
        stage.setScene(scene);
        stage.show();
    }

    public static void main(String[] args) {
        launch();
    }
}
```

### Le fichier FXML minimal

Un fichier FXML généré par SceneBuilder ressemble à ceci :

```xml
<?xml version="1.0" encoding="UTF-8"?>

<?import javafx.scene.control.Button?>
<?import javafx.scene.control.Label?>
<?import javafx.scene.layout.VBox?>

<VBox alignment="CENTER" spacing="20"
      xmlns:fx="http://javafx.com/fxml"
      fx:controller="com.exemple.HelloController">

    <Label fx:id="messageLabel" text="Bonjour !"/>
    <Button text="Cliquer ici" onAction="#handleBouton"/>

</VBox>
```

Points importants :
- `fx:controller` → indique quelle classe Java gère cette vue
- `fx:id` → donne un nom au composant pour y accéder depuis le contrôleur
- `onAction="#handleBouton"` → appelle la méthode `handleBouton()` dans le contrôleur

---

## 3. Mise en page — Layouts

Les **layouts** sont des conteneurs qui organisent les composants dans la fenêtre.

### VBox — disposition verticale

Organise les composants **les uns en dessous des autres**.

```xml
<VBox spacing="10" padding="20">
    <Label text="Premier"/>
    <Label text="Deuxième"/>
    <Button text="Troisième"/>
</VBox>
```

En Java :
```java
VBox vbox = new VBox(10); // 10 = espacement entre les éléments
vbox.setPadding(new Insets(20));
vbox.getChildren().addAll(label1, label2, bouton);
```

### HBox — disposition horizontale

Organise les composants **côte à côte**.

```xml
<HBox spacing="10" alignment="CENTER">
    <Button text="Oui"/>
    <Button text="Non"/>
    <Button text="Annuler"/>
</HBox>
```

En Java :
```java
HBox hbox = new HBox(10);
hbox.setAlignment(Pos.CENTER);
hbox.getChildren().addAll(boutonOui, boutonNon, boutonAnnuler);
```

### GridPane — disposition en grille

Organise les composants dans un **tableau de lignes et colonnes**.

```xml
<GridPane hgap="10" vgap="10" padding="20">
    <Label text="Nom :"        GridPane.columnIndex="0" GridPane.rowIndex="0"/>
    <TextField                 GridPane.columnIndex="1" GridPane.rowIndex="0"/>
    <Label text="Prénom :"     GridPane.columnIndex="0" GridPane.rowIndex="1"/>
    <TextField                 GridPane.columnIndex="1" GridPane.rowIndex="1"/>
    <Button text="Confirmer"   GridPane.columnIndex="1" GridPane.rowIndex="2"/>
</GridPane>
```

En Java :
```java
GridPane grid = new GridPane();
grid.setHgap(10);
grid.setVgap(10);
grid.setPadding(new Insets(20));

grid.add(new Label("Nom :"),  0, 0); // colonne 0, ligne 0
grid.add(champNom,            1, 0); // colonne 1, ligne 0
grid.add(new Label("Prénom :"), 0, 1);
grid.add(champPrenom,         1, 1);
grid.add(boutonConfirmer,     1, 2);
```

### BorderPane — disposition en zones

Divise la fenêtre en **5 zones** : Top, Bottom, Left, Right, Center.

```xml
<BorderPane>
    <top>    <Label text="Titre"       /> </top>
    <left>   <Label text="Menu"        /> </left>
    <center> <Label text="Contenu"     /> </center>
    <right>  <Label text="Infos"       /> </right>
    <bottom> <Label text="Statut"      /> </bottom>
</BorderPane>
```

En Java :
```java
BorderPane borderPane = new BorderPane();
borderPane.setTop(labelTitre);
borderPane.setLeft(labelMenu);
borderPane.setCenter(labelContenu);
borderPane.setRight(labelInfos);
borderPane.setBottom(labelStatut);
```

### Tableau récapitulatif des layouts

| Layout | Utilisation |
|---|---|
| **VBox** | Formulaires, listes verticales |
| **HBox** | Barres de boutons, menus horizontaux |
| **GridPane** | Formulaires avec étiquettes et champs alignés |
| **BorderPane** | Structure principale d'une fenêtre |
| **StackPane** | Superposer des éléments |
| **FlowPane** | Éléments qui s'adaptent à la taille de la fenêtre |

---

## 4. Les composants de base

### Label — afficher du texte

Sert à afficher du texte non modifiable par l'utilisateur.

```xml
<Label fx:id="monLabel" text="Bonjour !" />
```

```java
@FXML
private Label monLabel;

// Modifier le texte
monLabel.setText("Nouveau texte");

// Obtenir le texte
String texte = monLabel.getText();
```

### Button — bouton cliquable

```xml
<Button fx:id="monBouton" text="Cliquer" onAction="#handleClic"/>
```

```java
@FXML
private Button monBouton;

// Désactiver le bouton
monBouton.setDisable(true);

// Modifier le texte
monBouton.setText("Cliqué !");
```

### TextField — champ de saisie sur une ligne

```xml
<TextField fx:id="champNom" promptText="Entrez votre nom"/>
```

```java
@FXML
private TextField champNom;

// Lire ce que l'utilisateur a écrit
String nom = champNom.getText();

// Effacer le contenu
champNom.clear();

// Pré-remplir le champ
champNom.setText("Valeur par défaut");
```

### TextArea — zone de texte multiligne

```xml
<TextArea fx:id="zoneTexte" promptText="Écrivez ici..." wrapText="true"/>
```

```java
@FXML
private TextArea zoneTexte;

String contenu = zoneTexte.getText();
zoneTexte.appendText("\nNouvelle ligne ajoutée");
```

### CheckBox — case à cocher

```xml
<CheckBox fx:id="maCase" text="J'accepte les conditions"/>
```

```java
@FXML
private CheckBox maCase;

// Vérifier si elle est cochée
boolean estCochee = maCase.isSelected();

// Cocher/décocher par programme
maCase.setSelected(true);
```

### RadioButton — bouton radio (choix exclusif)

Les RadioButtons doivent appartenir au même `ToggleGroup` pour être exclusifs.

```xml
<ToggleGroup fx:id="groupeTaille"/>
<RadioButton text="Small"  toggleGroup="$groupeTaille"/>
<RadioButton text="Medium" toggleGroup="$groupeTaille" selected="true"/>
<RadioButton text="Large"  toggleGroup="$groupeTaille"/>
```

```java
@FXML
private ToggleGroup groupeTaille;

// Obtenir le bouton sélectionné
RadioButton selectionne = (RadioButton) groupeTaille.getSelectedToggle();
String valeur = selectionne.getText(); // "Small", "Medium" ou "Large"
```

### ComboBox — liste déroulante

```xml
<ComboBox fx:id="maListe" promptText="Choisir..."/>
```

```java
@FXML
private ComboBox<String> maListe;

// Ajouter des options
maListe.getItems().addAll("Option 1", "Option 2", "Option 3");

// Obtenir la valeur sélectionnée
String choix = maListe.getValue();
```

### PasswordField — champ mot de passe

```xml
<PasswordField fx:id="champMotDePasse" promptText="Mot de passe"/>
```

```java
@FXML
private PasswordField champMotDePasse;

String motDePasse = champMotDePasse.getText();
```

### Slider — curseur

```xml
<Slider fx:id="monCurseur" min="0" max="100" value="50"/>
```

```java
@FXML
private Slider monCurseur;

double valeur = monCurseur.getValue(); // entre 0 et 100
```

---

## 5. FXML et lien avec le contrôleur

### Comment SceneBuilder et le contrôleur sont liés

```
hello-view.fxml          HelloController.java
─────────────────        ────────────────────────────
fx:controller="..."  →   public class HelloController
fx:id="monLabel"     →   @FXML private Label monLabel
onAction="#handleClic" → @FXML private void handleClic()
```

### Créer le lien dans SceneBuilder

1. Ouvrir le fichier `.fxml` avec SceneBuilder
2. Dans le panneau **Controller** (en bas à gauche), entrer le nom complet de la classe contrôleur : `com.exemple.HelloController`
3. Sélectionner un composant, aller dans **Code** (panneau de droite)
4. Dans **fx:id**, donner un nom au composant
5. Dans **On Action**, entrer le nom de la méthode à appeler (sans le `#`)

### Exemple complet — hello-view.fxml

```xml
<?xml version="1.0" encoding="UTF-8"?>

<?import javafx.scene.control.*?>
<?import javafx.scene.layout.*?>

<VBox spacing="15" padding="20" alignment="CENTER"
      xmlns:fx="http://javafx.com/fxml"
      fx:controller="com.exemple.HelloController">

    <Label text="Calculateur de prix"/>

    <HBox spacing="10" alignment="CENTER">
        <Label text="Nom du produit :"/>
        <TextField fx:id="champNom" promptText="ex: Pizza"/>
    </HBox>

    <HBox spacing="10" alignment="CENTER">
        <Label text="Prix :"/>
        <TextField fx:id="champPrix" promptText="ex: 12.99"/>
    </HBox>

    <Button text="Calculer avec 10% de rabais" onAction="#handleCalculer"/>

    <Label fx:id="labelResultat" text=""/>

</VBox>
```

### Exemple complet — HelloController.java

```java
import javafx.fxml.FXML;
import javafx.scene.control.Label;
import javafx.scene.control.TextField;

public class HelloController {

    // Lier les composants du FXML avec @FXML
    @FXML
    private TextField champNom;

    @FXML
    private TextField champPrix;

    @FXML
    private Label labelResultat;

    // Méthode appelée quand on clique sur le bouton
    @FXML
    private void handleCalculer() {
        String nom = champNom.getText();
        String prixTexte = champPrix.getText();

        if (nom.isEmpty() || prixTexte.isEmpty()) {
            labelResultat.setText("Veuillez remplir tous les champs.");
            return;
        }

        double prix = Double.parseDouble(prixTexte);
        double prixAvecRabais = prix * 0.90;

        labelResultat.setText(nom + " avec rabais : " + String.format("%.2f", prixAvecRabais) + "$");
    }
}
```

### La méthode initialize()

Si tu as besoin d'initialiser des composants **au chargement de la vue** (ex: remplir une ComboBox), utilise la méthode `initialize()` :

```java
@FXML
public void initialize() {
    // Cette méthode est appelée automatiquement après le chargement du FXML
    maComboBox.getItems().addAll("Pizza", "Boisson", "Dessert");
    maComboBox.setValue("Pizza"); // sélection par défaut
    labelResultat.setText(""); // vider le label au démarrage
}
```

---

## 6. Les événements et handlers

### Qu'est-ce qu'un événement ?

Un **événement** est une action déclenchée par l'utilisateur : clic de souris, frappe au clavier, déplacement de curseur, etc. Un **handler** (gestionnaire) est la méthode Java qui réagit à cet événement.

### Événement sur un bouton — onAction

C'est l'événement le plus courant.

Dans le FXML :
```xml
<Button text="Valider" onAction="#handleValider"/>
```

Dans le contrôleur :
```java
@FXML
private void handleValider() {
    System.out.println("Bouton cliqué !");
}
```

### Événement sur un TextField — au changement de texte

```java
@FXML
private TextField champRecherche;

@FXML
public void initialize() {
    // Déclenché à chaque fois que le texte change
    champRecherche.textProperty().addListener((observable, ancienneValeur, nouvelleValeur) -> {
        System.out.println("Nouveau texte : " + nouvelleValeur);
    });
}
```

### Événement sur une CheckBox

```xml
<CheckBox fx:id="maCase" text="Activer" onAction="#handleCase"/>
```

```java
@FXML
private void handleCase() {
    if (maCase.isSelected()) {
        System.out.println("Case cochée !");
    } else {
        System.out.println("Case décochée !");
    }
}
```

### Événement sur un Slider

```java
@FXML
private Slider monCurseur;

@FXML
private Label labelValeur;

@FXML
public void initialize() {
    monCurseur.valueProperty().addListener((observable, ancienne, nouvelle) -> {
        labelValeur.setText("Valeur : " + (int) monCurseur.getValue());
    });
}
```

### Événement clavier — onKeyPressed

```xml
<TextField fx:id="champTexte" onKeyPressed="#handleTouche"/>
```

```java
import javafx.scene.input.KeyEvent;

@FXML
private void handleTouche(KeyEvent event) {
    System.out.println("Touche appuyée : " + event.getCode());

    // Réagir à la touche Entrée
    if (event.getCode().toString().equals("ENTER")) {
        System.out.println("Entrée pressée !");
    }
}
```

### Afficher une alerte — Alert

Les alertes permettent d'afficher des messages à l'utilisateur.

```java
import javafx.scene.control.Alert;

// Alerte d'information
Alert alerte = new Alert(Alert.AlertType.INFORMATION);
alerte.setTitle("Information");
alerte.setHeaderText("Opération réussie");
alerte.setContentText("Le produit a été ajouté à la commande.");
alerte.showAndWait();

// Alerte d'erreur
Alert erreur = new Alert(Alert.AlertType.ERROR);
erreur.setTitle("Erreur");
erreur.setHeaderText("Champ invalide");
erreur.setContentText("Veuillez entrer un prix valide.");
erreur.showAndWait();

// Alerte de confirmation
Alert confirmation = new Alert(Alert.AlertType.CONFIRMATION);
confirmation.setTitle("Confirmation");
confirmation.setHeaderText("Supprimer le produit ?");
confirmation.setContentText("Cette action est irréversible.");

Optional<ButtonType> resultat = confirmation.showAndWait();
if (resultat.isPresent() && resultat.get() == ButtonType.OK) {
    System.out.println("L'utilisateur a confirmé.");
}
```

### Validation des champs

Bonne pratique : toujours valider les champs avant de les utiliser.

```java
@FXML
private void handleAjouter() {
    String nom = champNom.getText().trim();
    String prixTexte = champPrix.getText().trim();

    // Vérifier que les champs ne sont pas vides
    if (nom.isEmpty()) {
        afficherErreur("Le nom ne peut pas être vide.");
        return;
    }

    // Vérifier que le prix est un nombre valide
    double prix;
    try {
        prix = Double.parseDouble(prixTexte);
    } catch (NumberFormatException e) {
        afficherErreur("Le prix doit être un nombre valide.");
        return;
    }

    // Vérifier que le prix est positif
    if (prix <= 0) {
        afficherErreur("Le prix doit être supérieur à 0.");
        return;
    }

    // Si tout est valide, continuer
    labelResultat.setText("Produit ajouté : " + nom + " à " + prix + "$");
}

private void afficherErreur(String message) {
    Alert erreur = new Alert(Alert.AlertType.ERROR);
    erreur.setTitle("Erreur de saisie");
    erreur.setHeaderText(null);
    erreur.setContentText(message);
    erreur.showAndWait();
}
```

---

## 7. Exercices pratiques

---

### Exercice 1 — Calculateur de rabais

**Objectif** : Créer une interface qui calcule le prix d'un produit après rabais.

**Interface à créer dans SceneBuilder :**
- Un `TextField` pour le nom du produit
- Un `TextField` pour le prix original
- Un `Slider` de 0 à 50 qui représente le pourcentage de rabais
- Un `Label` qui affiche le pourcentage du slider en temps réel (ex: `Rabais : 20%`)
- Un `Button` "Calculer"
- Un `Label` pour afficher le résultat

**Comportement attendu :**
- Quand l'utilisateur bouge le slider, le label du pourcentage se met à jour immédiatement
- Quand l'utilisateur clique sur "Calculer", le label résultat affiche : `Pizza : 10.39$ (rabais de 20%)`
- Si un champ est vide ou invalide, une alerte d'erreur s'affiche

---

### Exercice 2 — Formulaire d'ajout de produit

**Objectif** : Créer un formulaire qui permet d'ajouter un produit à une liste.

**Interface à créer dans SceneBuilder :**
- Un `TextField` pour le nom
- Un `TextField` pour le prix
- Une `ComboBox` avec les catégories : `Pizza`, `Boisson`, `Dessert`
- Un `Button` "Ajouter"
- Un `TextArea` (non modifiable) qui affiche la liste des produits ajoutés
- Un `Label` qui affiche le total

**Comportement attendu :**
- Quand on clique sur "Ajouter", le produit s'ajoute à la `TextArea` et le total se met à jour
- Les champs `TextField` se vident après l'ajout
- Si un champ est vide, une alerte s'affiche

---

### Exercice 3 — Mini commande de repas (projet intégré)

**Objectif** : Créer une interface graphique pour le projet de commande de repas.

**Interface suggérée :**

```
┌─────────────────────────────────────────────┐
│  COMMANDE DE REPAS          [Nouvelle cmd]  │
├──────────────────────┬──────────────────────┤
│  Ajouter un produit  │  Commande en cours   │
│                      │                      │
│  Nom : [________]    │  • Pizza Medium 12$  │
│  Prix : [_______]    │  • Coca-Cola    3$   │
│                      │  • Tiramisu     7$   │
│  Type :              │                      │
│  ○ Pizza             │  ──────────────────  │
│  ○ Boisson           │  Total : 22.00$      │
│  ○ Dessert           │                      │
│                      │  Rabais : [__]%      │
│  [   Ajouter   ]     │  [Appliquer rabais]  │
└──────────────────────┴──────────────────────┘
```

**Comportement attendu :**
- Sélectionner le type de produit avec les `RadioButton`
- Selon le type sélectionné, des champs supplémentaires apparaissent (ex: taille pour Pizza, volume pour Boisson)
- Le bouton "Ajouter" ajoute le produit à la liste et met à jour le total
- Le bouton "Appliquer rabais" recalcule le total avec le rabais entré
- Le bouton "Nouvelle commande" vide la liste

---

### Conseils généraux

- Toujours utiliser `fx:id` pour les composants auxquels tu dois accéder depuis le contrôleur
- Ne jamais oublier `@FXML` devant les attributs et méthodes liés au FXML
- Toujours valider les champs avant de les utiliser
- Utiliser `initialize()` pour configurer les composants au démarrage
- En cas d'erreur `NullPointerException`, vérifier que le `fx:id` dans le FXML correspond exactement au nom de l'attribut dans le contrôleur