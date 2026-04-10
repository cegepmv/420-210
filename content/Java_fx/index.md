+++
title = "Java FX"
weight = 14
+++
# JavaFX avec SceneBuilder

---

## Table des matières

1. [Introduction à JavaFX et SceneBuilder](#1-introduction-à-javafx-et-scenebuilder)
2. [Structure d'un projet JavaFX](#2-structure-dun-projet-javafx)
3. [Mise en page — Layouts](#3-mise-en-page--layouts)
4. [Les composants de base](#4-les-composants-de-base)
5. [Images et médias](#5-images-et-médias)
6. [FXML et lien avec le contrôleur](#6-fxml-et-lien-avec-le-contrôleur)
7. [Les événements et handlers](#7-les-événements-et-handlers)
8. [ListView et TableView](#8-listview-et-tableview)
9. [Navigation entre plusieurs vues FXML](#9-navigation-entre-plusieurs-vues-fxml)
10. [Animations](#10-animations)
11. [Exercices pratiques](#11-exercices-pratiques)

---

## 1. Introduction à JavaFX et SceneBuilder

### Pourquoi JavaFX ?

Quand on crée un programme Java en console, l'utilisateur interagit avec du texte. Avec **JavaFX**, on crée des applications avec une vraie **interface graphique** : fenêtres, boutons, menus, tableaux, etc. C'est ce qu'on appelle une application **GUI** (Graphical User Interface).

> **Analogie :** La console, c'est comme communiquer par SMS en texte brut. JavaFX, c'est comme une vraie application mobile avec des boutons et des images.

### Qu'est-ce que SceneBuilder ?

SceneBuilder est un **éditeur visuel** qui permet de construire l'interface graphique par **glisser-déposer** sans écrire de code. Il génère automatiquement un fichier **FXML** qui décrit l'interface.

```
Tu dessines dans SceneBuilder  →  Il génère un fichier .fxml  →  Java lit ce fichier au démarrage
```

### Les concepts fondamentaux

| Concept | Description | Analogie |
|---|---|---|
| **Stage** | La fenêtre principale | Le cadre d'un tableau |
| **Scene** | Le contenu de la fenêtre | La toile dans le cadre |
| **Node** | Tout élément visuel | Un objet sur la toile |
| **Layout** | Conteneur qui organise les Nodes | Des étagères qui rangent les objets |
| **FXML** | Fichier XML décrivant l'interface | Le plan d'architecte |
| **Controller** | Classe Java qui gère les actions | L'électricien qui branche les boutons |

### Le modèle MVC dans JavaFX

JavaFX encourage le patron de conception **MVC (Modèle - Vue - Contrôleur)** qui sépare les responsabilités :

```
┌─────────────────────────────────────────────────────┐
│                    Application JavaFX                │
│                                                     │
│  ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│  │     VUE      │     │ CONTRÔLEUR   │     │   MODÈLE     │
│  │  .fxml file  │ ←→  │  .java file  │ ←→  │  .java file  │
│  │  (apparence) │     │   (actions)  │     │  (données)   │
│  └──────────────┘     └──────────────┘     └──────────────┘
└─────────────────────────────────────────────────────┘
```

- **Vue** (`hello-view.fxml`) : définit ce que l'utilisateur voit
- **Contrôleur** (`HelloController.java`) : réagit aux clics, valide les champs
- **Modèle** (`Produit.java`, `Commande.java`) : contient les données et la logique métier

### Installation

1. Télécharger **SceneBuilder** : https://gluonhq.com/products/scene-builder/
2. Dans **IntelliJ** : `File → Settings → Languages & Frameworks → JavaFX → Path to SceneBuilder`
3. Créer un projet JavaFX dans IntelliJ (choisir le template JavaFX)
4. Pour ouvrir un `.fxml` avec SceneBuilder : clic droit sur le fichier → `Open in SceneBuilder`

---

## 2. Structure d'un projet JavaFX

### Arborescence d'un projet JavaFX

```
MonProjet/
├── src/
│   └── main/
│       ├── java/
│       │   └── com/exemple/
│       │       ├── MainApp.java              ← Point d'entrée
│       │       ├── HelloController.java      ← Contrôleur de la vue principale
│       │       └── model/
│       │           └── Produit.java          ← Classe modèle
│       └── resources/
│           └── com/exemple/
│               ├── hello-view.fxml           ← Vue principale (SceneBuilder)
│               ├── detail-view.fxml          ← Autre vue
│               ├── styles.css                ← Styles CSS
│               └── images/
│                   └── logo.png              ← Images
└── pom.xml
```

> ⚠️ **Important :** Les fichiers FXML et les images doivent être dans le dossier `resources`, avec le **même chemin de package** que les classes Java. C'est ce qui permet de les trouver avec `getResource()`.

### La classe principale — MainApp.java

```java
import javafx.application.Application;
import javafx.fxml.FXMLLoader;
import javafx.scene.Scene;
import javafx.stage.Stage;
import java.io.IOException;

public class MainApp extends Application {

    @Override
    public void start(Stage stage) throws IOException {

        // Charger le fichier FXML depuis les resources
        FXMLLoader fxmlLoader = new FXMLLoader(
            MainApp.class.getResource("hello-view.fxml")
        );

        // Créer la scène : fxmlLoader.load() retourne le layout racine
        Scene scene = new Scene(fxmlLoader.load(), 600, 400);

        // Optionnel : ajouter une feuille de style CSS
        scene.getStylesheets().add(
            MainApp.class.getResource("styles.css").toExternalForm()
        );

        // Configurer et afficher la fenêtre
        stage.setTitle("Mon Application JavaFX");
        stage.setMinWidth(400);   // largeur minimale
        stage.setMinHeight(300);  // hauteur minimale
        stage.setScene(scene);
        stage.show();
    }

    public static void main(String[] args) {
        launch(); // démarre l'application JavaFX
    }
}
```

### Cycle de vie d'une application JavaFX

```
main() → launch() → init() → start() → [L'application tourne] → stop()
```

- `init()` : appelé avant `start()`, utile pour initialiser des ressources (optionnel, rarement utilisé)
- `start()` : méthode principale, on y crée la fenêtre
- `stop()` : appelé quand l'application se ferme, utile pour sauvegarder des données

```java
@Override
public void stop() {
    System.out.println("Application fermée — sauvegarder les données ici");
}
```

---

## 3. Mise en page — Layouts

### Qu'est-ce qu'un layout ?

Un **layout** est un conteneur invisible qui organise automatiquement ses enfants selon des règles précises. Choisir le bon layout est essentiel pour créer une interface claire et responsive.

> **Analogie :** Un layout est comme un meuble de rangement. Un VBox est une étagère verticale, un HBox est une barre de rangement horizontale, un GridPane est une commode avec des tiroirs en grille.

---

### 3.1 VBox — Disposition verticale

**Utilisation :** Empiler des composants les uns en dessous des autres. Idéal pour les formulaires, les listes d'éléments, les barres latérales.

```
┌─────────────┐
│   Label     │
│─────────────│
│  TextField  │
│─────────────│
│   Button    │
└─────────────┘
```

**FXML :**
```xml
<VBox spacing="10" padding="20" alignment="CENTER_LEFT"
      xmlns:fx="http://javafx.com/fxml">

    <Label text="Nom :"/>
    <TextField promptText="Entrez votre nom"/>
    <Label text="Email :"/>
    <TextField promptText="Entrez votre email"/>
    <Button text="Envoyer" maxWidth="Infinity"/>

</VBox>
```

**Java :**
```java
import javafx.geometry.Insets;
import javafx.geometry.Pos;
import javafx.scene.control.*;
import javafx.scene.layout.VBox;

VBox vbox = new VBox();
vbox.setSpacing(10);               // espace entre les enfants
vbox.setPadding(new Insets(20));   // marges intérieures (haut, droite, bas, gauche)
vbox.setAlignment(Pos.CENTER_LEFT); // alignement des enfants

Label label = new Label("Nom :");
TextField textField = new TextField();
textField.setPromptText("Entrez votre nom");
Button bouton = new Button("Envoyer");

vbox.getChildren().addAll(label, textField, bouton);
// getChildren() retourne la liste des enfants du VBox
```

**Propriétés importantes :**

| Propriété | Description | Valeur exemple |
|---|---|---|
| `spacing` | Espace entre chaque enfant | `10` |
| `padding` | Marges intérieures | `"20"` ou `"10 20 10 20"` |
| `alignment` | Alignement des enfants | `CENTER`, `TOP_LEFT`, `BOTTOM_RIGHT` |
| `fillWidth` | Les enfants prennent toute la largeur | `true` / `false` |

---

### 3.2 HBox — Disposition horizontale

**Utilisation :** Placer des composants côte à côte. Idéal pour les barres de boutons, les menus horizontaux, les champs avec étiquettes sur la même ligne.

```
┌─────────────────────────────────┐
│  Bouton1  │  Bouton2  │  Bouton3│
└─────────────────────────────────┘
```

**FXML :**
```xml
<HBox spacing="10" alignment="CENTER" padding="15">

    <Button text="Annuler" styleClass="btn-secondary"/>
    <Button text="Réinitialiser" styleClass="btn-warning"/>
    <Button text="Confirmer" styleClass="btn-primary"/>

</HBox>
```

**Java :**
```java
import javafx.geometry.Pos;
import javafx.scene.control.Button;
import javafx.scene.layout.HBox;

HBox hbox = new HBox(10); // 10 = spacing
hbox.setAlignment(Pos.CENTER);
hbox.setPadding(new Insets(15));

Button btnAnnuler   = new Button("Annuler");
Button btnReset     = new Button("Réinitialiser");
Button btnConfirmer = new Button("Confirmer");

hbox.getChildren().addAll(btnAnnuler, btnReset, btnConfirmer);
```

**Faire qu'un bouton prend tout l'espace restant :**
```xml
<HBox spacing="10">
    <Button text="Retour"/>
    <!-- HBox.hgrow="ALWAYS" fait que ce bouton prend tout l'espace restant -->
    <Button text="Suivant" HBox.hgrow="ALWAYS" maxWidth="Infinity"/>
</HBox>
```

```java
import javafx.scene.layout.Priority;
HBox.setHgrow(btnSuivant, Priority.ALWAYS);
btnSuivant.setMaxWidth(Double.MAX_VALUE);
```

---

### 3.3 GridPane — Disposition en grille

**Utilisation :** Organiser des composants en lignes et colonnes. C'est le layout idéal pour les formulaires avec étiquettes alignées.

```
┌──────────────┬──────────────────────┐
│  Nom :       │  [TextField]         │
├──────────────┼──────────────────────┤
│  Email :     │  [TextField]         │
├──────────────┼──────────────────────┤
│  Catégorie : │  [ComboBox]          │
├──────────────┴──────────────────────┤
│              [Bouton Envoyer]       │
└─────────────────────────────────────┘
```

**FXML :**
```xml
<GridPane hgap="10" vgap="10" padding="20"
          xmlns:fx="http://javafx.com/fxml">

    <!-- columnIndex="colonne" rowIndex="ligne" (commence à 0) -->
    <Label text="Nom :"        GridPane.columnIndex="0" GridPane.rowIndex="0"/>
    <TextField fx:id="champNom" GridPane.columnIndex="1" GridPane.rowIndex="0"/>

    <Label text="Email :"      GridPane.columnIndex="0" GridPane.rowIndex="1"/>
    <TextField fx:id="champEmail" GridPane.columnIndex="1" GridPane.rowIndex="1"/>

    <Label text="Catégorie :"  GridPane.columnIndex="0" GridPane.rowIndex="2"/>
    <ComboBox fx:id="maCombo"  GridPane.columnIndex="1" GridPane.rowIndex="2"/>

    <!-- columnSpan="2" : occupe 2 colonnes -->
    <Button text="Envoyer"
            GridPane.columnIndex="0" GridPane.rowIndex="3"
            GridPane.columnSpan="2"
            maxWidth="Infinity"/>

</GridPane>
```

**Java :**
```java
import javafx.scene.layout.GridPane;
import javafx.scene.layout.ColumnConstraints;

GridPane grid = new GridPane();
grid.setHgap(10); // espace horizontal entre colonnes
grid.setVgap(10); // espace vertical entre lignes
grid.setPadding(new Insets(20));

// Définir les contraintes de colonnes (largeurs)
ColumnConstraints col1 = new ColumnConstraints(100); // colonne étiquettes : 100px fixe
ColumnConstraints col2 = new ColumnConstraints();
col2.setHgrow(Priority.ALWAYS); // colonne champs : prend tout l'espace restant
grid.getColumnConstraints().addAll(col1, col2);

// Ajouter les composants : add(node, colonne, ligne)
grid.add(new Label("Nom :"),  0, 0);
grid.add(champNom,            1, 0);
grid.add(new Label("Email :"), 0, 1);
grid.add(champEmail,          1, 1);

// Avec colspan : add(node, colonne, ligne, colonnesOccupees, lignesOccupees)
grid.add(btnEnvoyer, 0, 2, 2, 1); // colonne 0, ligne 2, occupe 2 colonnes, 1 ligne
```

---

### 3.4 BorderPane — Disposition en zones

**Utilisation :** Structure principale d'une fenêtre. Divise l'espace en 5 zones : Top, Bottom, Left, Right, Center. La zone Center prend tout l'espace disponible.

```
┌─────────────────────────────────┐
│              TOP                │
├────────┬────────────┬───────────┤
│        │            │           │
│  LEFT  │   CENTER   │   RIGHT   │
│        │            │           │
├────────┴────────────┴───────────┤
│             BOTTOM              │
└─────────────────────────────────┘
```

**FXML :**
```xml
<BorderPane xmlns:fx="http://javafx.com/fxml">

    <top>
        <HBox style="-fx-background-color: #2c3e50; -fx-padding: 10;">
            <Label text="Mon Application" style="-fx-text-fill: white; -fx-font-size: 18;"/>
        </HBox>
    </top>

    <left>
        <VBox spacing="5" style="-fx-background-color: #ecf0f1; -fx-padding: 10;" prefWidth="150">
            <Button text="Accueil"   maxWidth="Infinity"/>
            <Button text="Produits"  maxWidth="Infinity"/>
            <Button text="Commandes" maxWidth="Infinity"/>
            <Button text="Réglages"  maxWidth="Infinity"/>
        </VBox>
    </left>

    <center>
        <StackPane>
            <Label text="Contenu principal ici" alignment="CENTER"/>
        </StackPane>
    </center>

    <right>
        <VBox spacing="5" padding="10" prefWidth="150">
            <Label text="Infos rapides" style="-fx-font-weight: bold;"/>
            <Label text="Total : 22.97$"/>
            <Label text="Produits : 3"/>
        </VBox>
    </right>

    <bottom>
        <HBox style="-fx-background-color: #bdc3c7; -fx-padding: 5;">
            <Label text="Prêt"/>
        </HBox>
    </bottom>

</BorderPane>
```

**Java :**
```java
import javafx.scene.layout.BorderPane;

BorderPane borderPane = new BorderPane();

// Chaque zone accepte un seul Node (qui peut lui-même être un layout)
borderPane.setTop(barreMenu);
borderPane.setLeft(panneauNavigation);
borderPane.setCenter(contenuPrincipal);
borderPane.setRight(panneauInfo);
borderPane.setBottom(barreStatut);
```

> 💡 **Conseil :** Utilise `BorderPane` comme layout racine de tes fenêtres principales. C'est le layout le plus adapté pour une application complète avec menu, contenu et barre de statut.

---

### 3.5 StackPane — Superposition

**Utilisation :** Superposer des composants les uns sur les autres. Idéal pour afficher un texte sur une image, créer des overlays, ou centrer un contenu dans un espace.

```
┌─────────────────────┐
│  [Image en fond]    │
│  [Texte par-dessus] │  ← superposés
│  [Bouton par-dessus]│
└─────────────────────┘
```

**FXML :**
```xml
<StackPane>
    <!-- Premier enfant = en dessous, dernier enfant = au-dessus -->
    <Rectangle width="300" height="200" fill="#3498db"/>
    <Label text="Texte sur fond bleu"
           style="-fx-text-fill: white; -fx-font-size: 18; -fx-font-weight: bold;"/>
</StackPane>
```

**Exemple pratique — Image avec texte superposé :**
```xml
<StackPane prefWidth="300" prefHeight="200">
    <ImageView fx:id="imageFond" fitWidth="300" fitHeight="200" preserveRatio="false"/>
    <VBox alignment="BOTTOM_LEFT" style="-fx-padding: 15;">
        <Label text="Titre de la carte"
               style="-fx-text-fill: white; -fx-font-size: 16; -fx-font-weight: bold;"/>
        <Label text="Sous-titre"
               style="-fx-text-fill: #ecf0f1; -fx-font-size: 12;"/>
    </VBox>
</StackPane>
```

**Java :**
```java
import javafx.geometry.Pos;
import javafx.scene.layout.StackPane;

StackPane stack = new StackPane();

// Positionnement individuel dans le StackPane
StackPane.setAlignment(labelTexte, Pos.BOTTOM_LEFT);
StackPane.setMargin(labelTexte, new Insets(0, 0, 10, 10));

stack.getChildren().addAll(imageView, labelTexte);
```

---

### 3.6 AnchorPane — Positionnement ancré

**Utilisation :** Positionner des composants par rapport aux bords du conteneur. Quand le conteneur est redimensionné, les composants restent ancrés à leurs bords définis.

```
┌─────────────────────────────────┐
│[Bouton ancré en haut à gauche]  │
│                                 │
│         [Label centré]          │
│                                 │
│   [Bouton ancré en bas à droite]│
└─────────────────────────────────┘
```

**FXML :**
```xml
<AnchorPane prefWidth="400" prefHeight="300"
            xmlns:fx="http://javafx.com/fxml">

    <!-- Ancré à 10px du haut et 10px de la gauche -->
    <Button text="Haut Gauche"
            AnchorPane.topAnchor="10"
            AnchorPane.leftAnchor="10"/>

    <!-- Ancré à 10px du bas et 10px de la droite -->
    <Button text="Bas Droite"
            AnchorPane.bottomAnchor="10"
            AnchorPane.rightAnchor="10"/>

    <!-- Ancré des 4 côtés = s'étire avec le conteneur -->
    <TextArea fx:id="zoneTexte"
              AnchorPane.topAnchor="50"
              AnchorPane.bottomAnchor="50"
              AnchorPane.leftAnchor="10"
              AnchorPane.rightAnchor="10"/>

</AnchorPane>
```

**Java :**
```java
import javafx.scene.layout.AnchorPane;

AnchorPane anchorPane = new AnchorPane();

Button btnHautGauche = new Button("Haut Gauche");
AnchorPane.setTopAnchor(btnHautGauche, 10.0);
AnchorPane.setLeftAnchor(btnHautGauche, 10.0);

Button btnBasDroite = new Button("Bas Droite");
AnchorPane.setBottomAnchor(btnBasDroite, 10.0);
AnchorPane.setRightAnchor(btnBasDroite, 10.0);

// TextArea qui s'étire dans toutes les directions
TextArea textArea = new TextArea();
AnchorPane.setTopAnchor(textArea, 50.0);
AnchorPane.setBottomAnchor(textArea, 50.0);
AnchorPane.setLeftAnchor(textArea, 10.0);
AnchorPane.setRightAnchor(textArea, 10.0);

anchorPane.getChildren().addAll(btnHautGauche, btnBasDroite, textArea);
```

> 💡 **Cas d'usage typique :** SceneBuilder utilise souvent `AnchorPane` comme layout racine par défaut. C'est utile quand tu veux un contrôle précis sur la position de chaque élément, ou quand tu veux qu'un élément s'étire avec la fenêtre.

---

### 3.7 FlowPane — Disposition en flux

**Utilisation :** Organise les composants horizontalement (ou verticalement) et passe automatiquement à la ligne suivante quand l'espace manque. Idéal pour des galeries de boutons ou de tags.

```
┌──────────────────────────────────┐
│  [Tag1] [Tag2] [Tag3] [Tag4]     │
│  [Tag5] [Tag6]                   │  ← passe à la ligne automatiquement
└──────────────────────────────────┘
```

**FXML :**
```xml
<FlowPane hgap="10" vgap="10" padding="15" prefWrapLength="300">
    <Button text="Java"/>
    <Button text="JavaFX"/>
    <Button text="SceneBuilder"/>
    <Button text="FXML"/>
    <Button text="CSS"/>
    <Button text="JSON"/>
    <Button text="Gson"/>
    <Button text="Jackson"/>
</FlowPane>
```

**Java :**
```java
import javafx.scene.layout.FlowPane;

FlowPane flowPane = new FlowPane();
flowPane.setHgap(10);  // espace horizontal entre éléments
flowPane.setVgap(10);  // espace vertical entre lignes
flowPane.setPadding(new Insets(15));
flowPane.setPrefWrapLength(300); // largeur avant retour à la ligne

for (String tag : new String[]{"Java", "JavaFX", "CSS", "JSON"}) {
    Button btn = new Button(tag);
    flowPane.getChildren().add(btn);
}
```

---

### 3.8 TilePane — Disposition en tuiles

**Utilisation :** Comme FlowPane, mais tous les enfants ont la **même taille** (la taille du plus grand). Idéal pour des grilles d'images ou de cartes uniformes.

```
┌──────────┬──────────┬──────────┐
│  Tuile1  │  Tuile2  │  Tuile3  │
├──────────┼──────────┼──────────┤
│  Tuile4  │  Tuile5  │  Tuile6  │
└──────────┴──────────┴──────────┘
```

**FXML :**
```xml
<TilePane hgap="10" vgap="10" padding="15" prefColumns="3">
    <Button text="Produit 1" prefWidth="120" prefHeight="80"/>
    <Button text="Produit 2" prefWidth="120" prefHeight="80"/>
    <Button text="Produit 3" prefWidth="120" prefHeight="80"/>
    <Button text="Produit 4" prefWidth="120" prefHeight="80"/>
    <Button text="Produit 5" prefWidth="120" prefHeight="80"/>
</TilePane>
```

**Java :**
```java
import javafx.scene.layout.TilePane;

TilePane tilePane = new TilePane();
tilePane.setHgap(10);
tilePane.setVgap(10);
tilePane.setPrefColumns(3); // 3 colonnes
tilePane.setPrefTileWidth(120);
tilePane.setPrefTileHeight(80);
```

---

### 3.9 SplitPane — Panneau divisé

**Utilisation :** Divise l'espace en deux (ou plus) zones redimensionnables par l'utilisateur. Idéal pour un panneau gauche/droit (arbre + détail, liste + aperçu).

```
┌──────────┬──────────────────────┐
│          │                      │
│  Liste   │  ←divider→  Détail  │  ← l'utilisateur peut déplacer le séparateur
│          │                      │
└──────────┴──────────────────────┘
```

**FXML :**
```xml
<SplitPane dividerPositions="0.3"
           xmlns:fx="http://javafx.com/fxml">

    <!-- Panneau gauche : 30% de la largeur -->
    <VBox style="-fx-background-color: #f8f9fa; -fx-padding: 10;">
        <Label text="Navigation" style="-fx-font-weight: bold;"/>
        <Button text="Section 1" maxWidth="Infinity"/>
        <Button text="Section 2" maxWidth="Infinity"/>
    </VBox>

    <!-- Panneau droit : 70% de la largeur -->
    <StackPane style="-fx-background-color: white;">
        <Label text="Contenu principal" alignment="CENTER"/>
    </StackPane>

</SplitPane>
```

**Java :**
```java
import javafx.scene.control.SplitPane;

SplitPane splitPane = new SplitPane();
splitPane.getItems().addAll(panneauGauche, panneauDroit);
splitPane.setDividerPositions(0.3); // 30% pour le panneau gauche
```

---

### 3.10 ScrollPane — Panneau défilant

**Utilisation :** Ajoute des barres de défilement quand le contenu est plus grand que l'espace disponible.

**FXML :**
```xml
<ScrollPane fitToWidth="true" prefHeight="300">
    <!-- fitToWidth="true" : le contenu s'adapte à la largeur du ScrollPane -->
    <VBox spacing="5" padding="10">
        <!-- Beaucoup de contenu... -->
        <Label text="Ligne 1"/>
        <Label text="Ligne 2"/>
        <!-- ... etc ... -->
    </VBox>
</ScrollPane>
```

**Java :**
```java
import javafx.scene.control.ScrollPane;

ScrollPane scrollPane = new ScrollPane();
scrollPane.setContent(monVBox);         // définir le contenu
scrollPane.setFitToWidth(true);         // s'adapter à la largeur
scrollPane.setFitToHeight(false);       // ne pas s'adapter à la hauteur
scrollPane.setPrefHeight(300);          // hauteur visible
scrollPane.setVbarPolicy(ScrollPane.ScrollBarPolicy.ALWAYS);   // toujours afficher la scrollbar verticale
scrollPane.setHbarPolicy(ScrollPane.ScrollBarPolicy.NEVER);    // cacher la scrollbar horizontale
```

---

### 3.11 TabPane — Onglets

**Utilisation :** Organise le contenu en plusieurs onglets. L'utilisateur clique sur un onglet pour voir son contenu.

```
┌──────────┬──────────┬──────────┐
│ Onglet 1 │ Onglet 2 │ Onglet 3 │
├──────────┴──────────┴──────────┤
│                                │
│   Contenu de l'onglet actif    │
│                                │
└────────────────────────────────┘
```

**FXML :**
```xml
<TabPane tabClosingPolicy="UNAVAILABLE"
         xmlns:fx="http://javafx.com/fxml">

    <!-- tabClosingPolicy="UNAVAILABLE" : empêche de fermer les onglets -->

    <Tab text="Produits">
        <VBox spacing="10" padding="15">
            <Label text="Liste des produits" style="-fx-font-size: 16; -fx-font-weight: bold;"/>
            <ListView fx:id="listeProduits"/>
        </VBox>
    </Tab>

    <Tab text="Commandes">
        <VBox spacing="10" padding="15">
            <Label text="Historique des commandes"/>
            <TableView fx:id="tableCommandes"/>
        </VBox>
    </Tab>

    <Tab text="Réglages">
        <GridPane hgap="10" vgap="10" padding="15">
            <Label text="Langue :"     GridPane.columnIndex="0" GridPane.rowIndex="0"/>
            <ComboBox              GridPane.columnIndex="1" GridPane.rowIndex="0"/>
            <Label text="Thème :"      GridPane.columnIndex="0" GridPane.rowIndex="1"/>
            <ComboBox              GridPane.columnIndex="1" GridPane.rowIndex="1"/>
        </GridPane>
    </Tab>

</TabPane>
```

**Java :**
```java
import javafx.scene.control.Tab;
import javafx.scene.control.TabPane;

TabPane tabPane = new TabPane();
tabPane.setTabClosingPolicy(TabPane.TabClosingPolicy.UNAVAILABLE);

Tab tab1 = new Tab("Produits");
tab1.setContent(monVBoxProduits);

Tab tab2 = new Tab("Commandes");
tab2.setContent(maTableCommandes);

tabPane.getTabs().addAll(tab1, tab2);

// Détecter le changement d'onglet
tabPane.getSelectionModel().selectedItemProperty().addListener(
    (obs, ancienOnglet, nouvelOnglet) -> {
        System.out.println("Onglet sélectionné : " + nouvelOnglet.getText());
    }
);

// Sélectionner un onglet par programme
tabPane.getSelectionModel().select(0); // premier onglet
```

---

### 3.12 Tableau récapitulatif des layouts

| Layout | Utilisation principale | Points clés |
|---|---|---|
| **VBox** | Formulaires, listes verticales | `spacing`, `alignment` |
| **HBox** | Barres de boutons, éléments côte à côte | `spacing`, `HBox.hgrow` |
| **GridPane** | Formulaires avec étiquettes alignées | `columnIndex`, `rowIndex`, `columnSpan` |
| **BorderPane** | Structure principale d'une fenêtre | Top, Left, Center, Right, Bottom |
| **StackPane** | Superposer des éléments | Z-order, centrage automatique |
| **AnchorPane** | Positionnement précis par rapport aux bords | `topAnchor`, `rightAnchor`, etc. |
| **FlowPane** | Tags, boutons qui passent à la ligne | `hgap`, `vgap`, `prefWrapLength` |
| **TilePane** | Grilles d'éléments de même taille | `prefColumns`, `prefTileWidth` |
| **SplitPane** | Deux panneaux redimensionnables | `dividerPositions` |
| **ScrollPane** | Contenu défilant | `fitToWidth`, `VbarPolicy` |
| **TabPane** | Contenu organisé en onglets | `tabClosingPolicy`, `Tab` |

---

## 4. Les composants de base

### 4.1 Label — Afficher du texte

```xml
<Label fx:id="monLabel" text="Bonjour !" style="-fx-font-size: 16; -fx-font-weight: bold;"/>
```

```java
@FXML private Label monLabel;

monLabel.setText("Nouveau texte");
monLabel.setStyle("-fx-text-fill: red;");
monLabel.setWrapText(true); // retour à la ligne automatique
String texte = monLabel.getText();
```

---

### 4.2 Button — Bouton cliquable

```xml
<Button fx:id="monBouton" text="Cliquer" onAction="#handleClic"
        style="-fx-background-color: #3498db; -fx-text-fill: white;"/>
```

```java
@FXML private Button monBouton;

monBouton.setDisable(true);        // désactiver
monBouton.setVisible(false);       // cacher
monBouton.setText("Chargement..."); // changer le texte
monBouton.setDefaultButton(true);  // activé par la touche Entrée
monBouton.setCancelButton(true);   // activé par la touche Échap
```

---

### 4.3 TextField — Champ de saisie

```xml
<TextField fx:id="champNom" promptText="Entrez votre nom" maxLength="50"/>
```

```java
@FXML private TextField champNom;

String nom = champNom.getText();        // lire
champNom.setText("Valeur initiale");    // écrire
champNom.clear();                       // vider
champNom.setEditable(false);            // lecture seule
champNom.selectAll();                   // sélectionner tout
```

---

### 4.4 TextArea — Zone de texte multiligne

```xml
<TextArea fx:id="zoneTexte" promptText="Écrivez ici..."
          wrapText="true" prefRowCount="5"/>
```

```java
@FXML private TextArea zoneTexte;

String contenu = zoneTexte.getText();
zoneTexte.appendText("\nNouvelle ligne");
zoneTexte.setWrapText(true);  // retour à la ligne automatique
```

---

### 4.5 CheckBox — Case à cocher

```xml
<CheckBox fx:id="maCase" text="J'accepte les conditions" onAction="#handleCase"/>
```

```java
@FXML private CheckBox maCase;

boolean estCochee = maCase.isSelected();
maCase.setSelected(true);

// État indéterminé (ni coché ni décoché)
maCase.setAllowIndeterminate(true);
maCase.setIndeterminate(true);
```

---

### 4.6 RadioButton — Bouton radio

Les `RadioButton` doivent appartenir au même `ToggleGroup` pour être exclusifs.

```xml
<fx:define>
    <ToggleGroup fx:id="groupeTaille"/>
</fx:define>

<RadioButton text="Small"  toggleGroup="$groupeTaille"/>
<RadioButton text="Medium" toggleGroup="$groupeTaille" selected="true"/>
<RadioButton text="Large"  toggleGroup="$groupeTaille"/>
```

```java
@FXML private ToggleGroup groupeTaille;

// Lire la sélection
RadioButton selectionne = (RadioButton) groupeTaille.getSelectedToggle();
if (selectionne != null) {
    String valeur = selectionne.getText(); // "Small", "Medium" ou "Large"
}

// Écouter les changements
groupeTaille.selectedToggleProperty().addListener((obs, ancien, nouveau) -> {
    RadioButton rb = (RadioButton) nouveau;
    System.out.println("Sélectionné : " + rb.getText());
});
```

---

### 4.7 ComboBox — Liste déroulante

```xml
<ComboBox fx:id="maCombo" promptText="Choisir une catégorie"/>
```

```java
@FXML private ComboBox<String> maCombo;

@FXML
public void initialize() {
    maCombo.getItems().addAll("Pizza", "Boisson", "Dessert");
    maCombo.setValue("Pizza"); // sélection par défaut
}

String choix = maCombo.getValue();

// Écouter les changements
maCombo.valueProperty().addListener((obs, ancienne, nouvelle) -> {
    System.out.println("Nouvelle valeur : " + nouvelle);
});
```

---

### 4.8 Slider — Curseur

```xml
<Slider fx:id="monSlider" min="0" max="100" value="50"
        showTickMarks="true" showTickLabels="true" majorTickUnit="25"/>
```

```java
@FXML private Slider monSlider;

double valeur = monSlider.getValue();

monSlider.valueProperty().addListener((obs, ancienne, nouvelle) -> {
    System.out.println("Valeur : " + (int) nouvelle.doubleValue());
});
```

---

### 4.9 ProgressBar et ProgressIndicator

```xml
<ProgressBar fx:id="maProgressBar" progress="0.0" prefWidth="200"/>
<ProgressIndicator fx:id="monIndicateur" progress="-1"/> <!-- -1 = indéterminé -->
```

```java
@FXML private ProgressBar maProgressBar;
@FXML private ProgressIndicator monIndicateur;

maProgressBar.setProgress(0.75); // 75%
monIndicateur.setProgress(0.5);  // 50%
monIndicateur.setProgress(-1);   // animation de chargement infinie
```

---

### 4.10 DatePicker — Sélecteur de date

```xml
<DatePicker fx:id="monDatePicker" promptText="Choisir une date"/>
```

```java
import java.time.LocalDate;

@FXML private DatePicker monDatePicker;

LocalDate date = monDatePicker.getValue();
if (date != null) {
    System.out.println("Date : " + date); // 2024-03-15
}

// Pré-remplir avec la date d'aujourd'hui
monDatePicker.setValue(LocalDate.now());
```

---

## 5. Images et médias

### 5.1 Afficher une image — ImageView

`ImageView` est le composant JavaFX pour afficher des images. Il faut d'abord créer un objet `Image`, puis l'assigner à un `ImageView`.

**Structure des ressources :**
```
src/main/resources/com/exemple/
├── images/
│   ├── logo.png
│   ├── pizza.jpg
│   └── fond.png
└── hello-view.fxml
```

**FXML :**
```xml
<?import javafx.scene.image.ImageView?>
<?import javafx.scene.image.Image?>

<!-- Image depuis les resources du projet -->
<ImageView fx:id="monImage" fitWidth="200" fitHeight="150" preserveRatio="true">
    <image>
        <Image url="@images/pizza.jpg"/>
    </image>
</ImageView>
```

> 💡 **Le préfixe `@`** dans FXML signifie "chemin relatif par rapport au fichier FXML". C'est la façon recommandée de référencer les images dans SceneBuilder.

**Java — Charger depuis les resources :**
```java
import javafx.scene.image.Image;
import javafx.scene.image.ImageView;

@FXML private ImageView monImage;

@FXML
public void initialize() {
    // Méthode 1 : depuis les resources du projet (recommandée)
    Image image = new Image(getClass().getResourceAsStream("images/pizza.jpg"));
    monImage.setImage(image);

    // Méthode 2 : depuis une URL web
    Image imageWeb = new Image("https://exemple.com/image.jpg");
    monImage.setImage(imageWeb);

    // Méthode 3 : depuis un chemin absolu (déconseillé — dépend de la machine)
    // Image imageLocale = new Image("file:///C:/images/pizza.jpg");
}
```

**Java — Configurer l'ImageView :**
```java
// Dimensions
monImage.setFitWidth(200);       // largeur max
monImage.setFitHeight(150);      // hauteur max
monImage.setPreserveRatio(true); // conserver les proportions

// Si false : l'image est étirée pour remplir exactement fitWidth x fitHeight
monImage.setPreserveRatio(false);

// Lissage (antialiasing) — recommandé pour les petites images redimensionnées
monImage.setSmooth(true);

// Changer l'image dynamiquement (ex: lors d'un clic)
@FXML
private void changerImage() {
    Image nouvelleImage = new Image(getClass().getResourceAsStream("images/autre.jpg"));
    monImage.setImage(nouvelleImage);
}
```

---

### 5.2 Image dans un bouton

```xml
<?import javafx.scene.image.ImageView?>

<Button text="Supprimer" onAction="#handleSupprimer">
    <graphic>
        <ImageView fitWidth="16" fitHeight="16">
            <image><Image url="@images/delete-icon.png"/></image>
        </ImageView>
    </graphic>
</Button>
```

**Java :**
```java
Image icone = new Image(getClass().getResourceAsStream("images/delete-icon.png"));
ImageView iconView = new ImageView(icone);
iconView.setFitWidth(16);
iconView.setFitHeight(16);

Button btnSupprimer = new Button("Supprimer", iconView);
```

---

### 5.3 Image de fond avec CSS

```java
// Dans le contrôleur ou dans MainApp
monPane.setStyle(
    "-fx-background-image: url('" +
    getClass().getResource("images/fond.png").toExternalForm() +
    "'); " +
    "-fx-background-size: cover; " +   // couvrir tout l'espace
    "-fx-background-position: center;"  // centrer
);
```

**Ou dans un fichier CSS :**
```css
/* styles.css */
.root {
    -fx-background-image: url("images/fond.png");
    -fx-background-size: cover;
    -fx-background-position: center;
    -fx-background-repeat: no-repeat;
}
```

---

### 5.4 Effets sur les images

JavaFX propose plusieurs effets visuels applicables sur n'importe quel Node.

```java
import javafx.scene.effect.*;

// Ombre portée
monImage.setEffect(new DropShadow(10, Color.BLACK));

// Flou gaussien
monImage.setEffect(new GaussianBlur(5));

// Luminosité / Contraste
ColorAdjust colorAdjust = new ColorAdjust();
colorAdjust.setBrightness(0.2);   // -1.0 à 1.0
colorAdjust.setContrast(0.1);     // -1.0 à 1.0
colorAdjust.setSaturation(-0.5);  // -1.0 = niveaux de gris, 1.0 = très saturé
monImage.setEffect(colorAdjust);

// Supprimer l'effet
monImage.setEffect(null);
```

---

### 5.5 Charger une image depuis un FileChooser

```java
import javafx.stage.FileChooser;
import java.io.File;

@FXML
private void choisirImage() {
    FileChooser fileChooser = new FileChooser();
    fileChooser.setTitle("Choisir une image");

    // Filtrer pour n'afficher que les images
    fileChooser.getExtensionFilters().addAll(
        new FileChooser.ExtensionFilter("Images", "*.png", "*.jpg", "*.jpeg", "*.gif"),
        new FileChooser.ExtensionFilter("Tous les fichiers", "*.*")
    );

    // Ouvrir la boîte de dialogue
    // stage doit être accessible (passer en paramètre ou récupérer depuis un Node)
    File fichier = fileChooser.showOpenDialog(monBouton.getScene().getWindow());

    if (fichier != null) {
        Image image = new Image(fichier.toURI().toString());
        monImageView.setImage(image);
    }
}
```

---

## 6. FXML et lien avec le contrôleur

### 6.1 Comment SceneBuilder et le contrôleur communiquent

```
hello-view.fxml                    HelloController.java
──────────────────────────         ──────────────────────────────────────
fx:controller="...Controller"  →   public class HelloController
fx:id="monLabel"               →   @FXML private Label monLabel
onAction="#handleClic"         →   @FXML private void handleClic()
```

### 6.2 Règles importantes

1. **`@FXML`** doit être placé devant chaque attribut et méthode liés au FXML
2. Le **`fx:id`** dans le FXML doit correspondre **exactement** au nom de l'attribut Java
3. Le nom de méthode dans **`onAction`** doit correspondre **exactement** au nom de la méthode Java (sans le `#`)
4. Le **`fx:controller`** doit contenir le **nom complet** de la classe (avec le package)

### 6.3 Exemple complet FXML + Contrôleur

**hello-view.fxml :**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<?import javafx.scene.control.*?>
<?import javafx.scene.layout.*?>

<VBox spacing="15" padding="20" alignment="CENTER"
      xmlns:fx="http://javafx.com/fxml"
      fx:controller="com.exemple.HelloController">

    <Label text="Calculateur de prix" style="-fx-font-size: 18; -fx-font-weight: bold;"/>

    <GridPane hgap="10" vgap="10">
        <Label text="Produit :"  GridPane.columnIndex="0" GridPane.rowIndex="0"/>
        <TextField fx:id="champNom" promptText="ex: Pizza"
                   GridPane.columnIndex="1" GridPane.rowIndex="0"/>

        <Label text="Prix ($) :" GridPane.columnIndex="0" GridPane.rowIndex="1"/>
        <TextField fx:id="champPrix" promptText="ex: 12.99"
                   GridPane.columnIndex="1" GridPane.rowIndex="1"/>
    </GridPane>

    <Slider fx:id="sliderRabais" min="0" max="50" value="0"
            showTickLabels="true" showTickMarks="true" majorTickUnit="10"/>
    <Label fx:id="labelRabais" text="Rabais : 0%"/>

    <HBox spacing="10" alignment="CENTER">
        <Button text="Réinitialiser" onAction="#handleReset"/>
        <Button text="Calculer" onAction="#handleCalculer"
                style="-fx-background-color: #27ae60; -fx-text-fill: white;"/>
    </HBox>

    <Label fx:id="labelResultat" text="" style="-fx-font-size: 14;"/>

</VBox>
```

**HelloController.java :**
```java
import javafx.fxml.FXML;
import javafx.scene.control.*;

public class HelloController {

    @FXML private TextField champNom;
    @FXML private TextField champPrix;
    @FXML private Slider sliderRabais;
    @FXML private Label labelRabais;
    @FXML private Label labelResultat;

    // initialize() est appelé automatiquement après le chargement du FXML
    // C'est ici qu'on configure les listeners et valeurs initiales
    @FXML
    public void initialize() {
        // Mettre à jour le label quand le slider bouge
        sliderRabais.valueProperty().addListener((obs, ancienne, nouvelle) -> {
            int rabais = (int) nouvelle.doubleValue();
            labelRabais.setText("Rabais : " + rabais + "%");
        });
    }

    @FXML
    private void handleCalculer() {
        String nom = champNom.getText().trim();
        String prixTexte = champPrix.getText().trim();

        if (nom.isEmpty() || prixTexte.isEmpty()) {
            labelResultat.setText("⚠ Veuillez remplir tous les champs.");
            labelResultat.setStyle("-fx-text-fill: orange;");
            return;
        }

        try {
            double prix = Double.parseDouble(prixTexte);
            int rabais = (int) sliderRabais.getValue();
            double prixFinal = prix * (1 - rabais / 100.0);

            labelResultat.setText(String.format(
                "%s : %.2f$ (rabais %d%%)", nom, prixFinal, rabais
            ));
            labelResultat.setStyle("-fx-text-fill: #27ae60;");

        } catch (NumberFormatException e) {
            labelResultat.setText("⚠ Le prix doit être un nombre valide.");
            labelResultat.setStyle("-fx-text-fill: red;");
        }
    }

    @FXML
    private void handleReset() {
        champNom.clear();
        champPrix.clear();
        sliderRabais.setValue(0);
        labelResultat.setText("");
    }
}
```

### 6.4 La méthode initialize()

`initialize()` est appelée **automatiquement** par JavaFX après que tous les composants `@FXML` ont été injectés. C'est l'endroit idéal pour :

- Remplir une `ComboBox` ou `ListView`
- Configurer des `Listener` sur des propriétés
- Initialiser des valeurs par défaut
- Configurer les colonnes d'une `TableView`

```java
@FXML
public void initialize() {
    // ✅ Les composants @FXML sont disponibles ici
    maComboBox.getItems().addAll("Option 1", "Option 2", "Option 3");
    maListView.getItems().addAll("Item 1", "Item 2", "Item 3");
    labelStatut.setText("Prêt");
}
```

> ⚠️ **Erreur courante :** Essayer d'accéder à un composant `@FXML` dans le **constructeur**. À ce moment-là, les composants ne sont pas encore injectés et valent `null`. Toujours utiliser `initialize()` à la place.

---

## 7. Les événements et handlers

### 7.1 Événement sur un bouton — onAction

```java
@FXML
private void handleValider() {
    System.out.println("Bouton cliqué !");
}
```

### 7.2 Écouter les changements de texte

```java
champTexte.textProperty().addListener((observable, ancienneValeur, nouvelleValeur) -> {
    // Appelé à chaque fois que le texte change
    System.out.println("Texte : " + nouvelleValeur);

    // Exemple : désactiver le bouton si le champ est vide
    monBouton.setDisable(nouvelleValeur.trim().isEmpty());
});
```

### 7.3 Événement clavier

```java
@FXML
private void handleTouche(KeyEvent event) {
    switch (event.getCode()) {
        case ENTER  -> handleValider();
        case ESCAPE -> handleAnnuler();
        default     -> {}
    }
}
```

### 7.4 Afficher une alerte

```java
import javafx.scene.control.Alert;
import javafx.scene.control.ButtonType;
import java.util.Optional;

// Alerte d'information
private void afficherInfo(String message) {
    Alert alerte = new Alert(Alert.AlertType.INFORMATION);
    alerte.setTitle("Information");
    alerte.setHeaderText(null); // null = pas de sous-titre
    alerte.setContentText(message);
    alerte.showAndWait();
}

// Alerte d'erreur
private void afficherErreur(String message) {
    Alert erreur = new Alert(Alert.AlertType.ERROR);
    erreur.setTitle("Erreur");
    erreur.setHeaderText("Une erreur s'est produite");
    erreur.setContentText(message);
    erreur.showAndWait();
}

// Alerte de confirmation
private boolean confirmer(String message) {
    Alert confirmation = new Alert(Alert.AlertType.CONFIRMATION);
    confirmation.setTitle("Confirmation");
    confirmation.setHeaderText(null);
    confirmation.setContentText(message);

    Optional<ButtonType> resultat = confirmation.showAndWait();
    return resultat.isPresent() && resultat.get() == ButtonType.OK;
}

// Utilisation
@FXML
private void handleSupprimer() {
    if (confirmer("Voulez-vous vraiment supprimer cet élément ?")) {
        // Supprimer...
        afficherInfo("Élément supprimé avec succès.");
    }
}
```

### 7.5 Validation des champs

```java
private boolean validerChamps() {
    String nom = champNom.getText().trim();
    String prixTexte = champPrix.getText().trim();

    if (nom.isEmpty()) {
        afficherErreur("Le nom ne peut pas être vide.");
        champNom.requestFocus(); // mettre le curseur dans ce champ
        return false;
    }

    if (prixTexte.isEmpty()) {
        afficherErreur("Le prix ne peut pas être vide.");
        return false;
    }

    try {
        double prix = Double.parseDouble(prixTexte);
        if (prix <= 0) {
            afficherErreur("Le prix doit être supérieur à 0.");
            return false;
        }
    } catch (NumberFormatException e) {
        afficherErreur("Le prix doit être un nombre valide (ex: 12.99).");
        return false;
    }

    return true; // tout est valide
}
```

---

## 8. ListView et TableView

### 8.1 ListView — Liste simple

`ListView` affiche une liste d'éléments sélectionnables. C'est l'équivalent graphique d'une `List<String>`.

**FXML :**
```xml
<ListView fx:id="maListe" prefHeight="200" onMouseClicked="#handleSelection"/>
```

**Java — Utilisation de base :**
```java
import javafx.collections.FXCollections;
import javafx.collections.ObservableList;
import javafx.scene.control.ListView;

@FXML private ListView<String> maListe;

@FXML
public void initialize() {
    // ObservableList : JavaFX met à jour l'affichage automatiquement
    // quand on ajoute ou retire des éléments
    ObservableList<String> items = FXCollections.observableArrayList(
        "Pizza Margherita",
        "Coca-Cola",
        "Tiramisu"
    );
    maListe.setItems(items);

    // Sélection simple (un seul élément à la fois)
    maListe.getSelectionModel().setSelectionMode(SelectionMode.SINGLE);

    // Sélection multiple (Ctrl+clic)
    maListe.getSelectionModel().setSelectionMode(SelectionMode.MULTIPLE);
}

@FXML
private void handleSelection() {
    String selection = maListe.getSelectionModel().getSelectedItem();
    if (selection != null) {
        System.out.println("Sélectionné : " + selection);
    }
}

// Ajouter un élément
maListe.getItems().add("Nouveau produit");

// Retirer l'élément sélectionné
String selectionne = maListe.getSelectionModel().getSelectedItem();
maListe.getItems().remove(selectionne);

// Écouter les changements de sélection
maListe.getSelectionModel().selectedItemProperty().addListener(
    (obs, ancienItem, nouvelItem) -> {
        if (nouvelItem != null) {
            System.out.println("Nouvel item sélectionné : " + nouvelItem);
        }
    }
);
```

**ListView avec des objets personnalisés :**
```java
// ListView<Produit> au lieu de ListView<String>
@FXML private ListView<Produit> listeProduits;

@FXML
public void initialize() {
    ObservableList<Produit> produits = FXCollections.observableArrayList(
        new Produit("Pizza Margherita", 12.99, "Pizza"),
        new Produit("Coca-Cola", 2.99, "Boisson")
    );
    listeProduits.setItems(produits);

    // JavaFX appelle toString() pour afficher chaque item
    // Assure-toi que Produit a un bon toString()
}
```

**Personnaliser l'affichage avec CellFactory :**
```java
listeProduits.setCellFactory(listView -> new ListCell<Produit>() {
    @Override
    protected void updateItem(Produit produit, boolean empty) {
        super.updateItem(produit, empty);
        if (empty || produit == null) {
            setText(null);
            setGraphic(null);
        } else {
            // Créer un HBox pour chaque cellule
            HBox hbox = new HBox(10);
            Label labelNom = new Label(produit.getNom());
            Label labelPrix = new Label(String.format("%.2f$", produit.getPrix()));
            labelPrix.setStyle("-fx-text-fill: #27ae60; -fx-font-weight: bold;");
            hbox.getChildren().addAll(labelNom, labelPrix);
            setGraphic(hbox);
        }
    }
});
```

---

### 8.2 TableView — Tableau de données

`TableView` affiche des données sous forme de tableau avec colonnes. C'est le composant le plus complet pour afficher des listes d'objets.

**FXML :**
```xml
<?import javafx.scene.control.TableView?>
<?import javafx.scene.control.TableColumn?>

<TableView fx:id="tableauProduits" prefHeight="300">
    <columns>
        <TableColumn fx:id="colNom"       text="Nom"       prefWidth="150"/>
        <TableColumn fx:id="colPrix"      text="Prix"      prefWidth="80"/>
        <TableColumn fx:id="colCategorie" text="Catégorie" prefWidth="100"/>
    </columns>
    <placeholder>
        <Label text="Aucun produit dans la liste"/>
    </placeholder>
</TableView>
```

**Java — Configuration complète :**
```java
import javafx.beans.property.SimpleStringProperty;
import javafx.beans.property.SimpleDoubleProperty;
import javafx.collections.FXCollections;
import javafx.collections.ObservableList;
import javafx.scene.control.*;

@FXML private TableView<Produit> tableauProduits;
@FXML private TableColumn<Produit, String> colNom;
@FXML private TableColumn<Produit, Double> colPrix;
@FXML private TableColumn<Produit, String> colCategorie;

@FXML
public void initialize() {
    // Configurer chaque colonne : indiquer quel attribut afficher
    colNom.setCellValueFactory(cellData ->
        new SimpleStringProperty(cellData.getValue().getNom())
    );

    colPrix.setCellValueFactory(cellData ->
        new SimpleDoubleProperty(cellData.getValue().getPrix()).asObject()
    );

    colCategorie.setCellValueFactory(cellData ->
        new SimpleStringProperty(cellData.getValue().getCategorie())
    );

    // Formater la colonne Prix pour afficher "12.99$"
    colPrix.setCellFactory(col -> new TableCell<Produit, Double>() {
        @Override
        protected void updateItem(Double prix, boolean empty) {
            super.updateItem(prix, empty);
            if (empty || prix == null) {
                setText(null);
            } else {
                setText(String.format("%.2f$", prix));
                setStyle("-fx-alignment: CENTER-RIGHT;");
            }
        }
    });

    // Charger les données
    ObservableList<Produit> produits = FXCollections.observableArrayList(
        new Produit("Pizza Margherita", 12.99, "Pizza"),
        new Produit("Coca-Cola", 2.99, "Boisson"),
        new Produit("Tiramisu", 6.99, "Dessert")
    );
    tableauProduits.setItems(produits);
}
```

**Récupérer l'élément sélectionné :**
```java
// Sélection simple
Produit selectionne = tableauProduits.getSelectionModel().getSelectedItem();
if (selectionne != null) {
    System.out.println("Produit sélectionné : " + selectionne.getNom());
}

// Écouter les changements de sélection
tableauProduits.getSelectionModel().selectedItemProperty().addListener(
    (obs, ancien, nouveau) -> {
        if (nouveau != null) {
            // Remplir un formulaire avec les données du produit sélectionné
            champNom.setText(nouveau.getNom());
            champPrix.setText(String.valueOf(nouveau.getPrix()));
        }
    }
);
```

**Ajouter, modifier et supprimer des lignes :**
```java
// Ajouter une ligne
@FXML
private void handleAjouter() {
    if (!validerChamps()) return;
    Produit nouveau = new Produit(champNom.getText(), Double.parseDouble(champPrix.getText()), "Pizza");
    tableauProduits.getItems().add(nouveau);
    champNom.clear();
    champPrix.clear();
}

// Supprimer la ligne sélectionnée
@FXML
private void handleSupprimer() {
    Produit selectionne = tableauProduits.getSelectionModel().getSelectedItem();
    if (selectionne == null) {
        afficherErreur("Sélectionnez un produit à supprimer.");
        return;
    }
    if (confirmer("Supprimer " + selectionne.getNom() + " ?")) {
        tableauProduits.getItems().remove(selectionne);
    }
}
```

**Tri et recherche dans une TableView :**
```java
import javafx.collections.transformation.FilteredList;
import javafx.collections.transformation.SortedList;

@FXML private TextField champRecherche;

@FXML
public void initialize() {
    // ... configuration des colonnes ...

    ObservableList<Produit> tousLesProduits = FXCollections.observableArrayList(/* ... */);

    // FilteredList : filtre automatiquement selon un prédicat
    FilteredList<Produit> produitsFiltres = new FilteredList<>(tousLesProduits, p -> true);

    // Écouter le champ de recherche
    champRecherche.textProperty().addListener((obs, ancienne, nouvelle) -> {
        produitsFiltres.setPredicate(produit -> {
            if (nouvelle == null || nouvelle.isEmpty()) return true; // tout afficher
            String recherche = nouvelle.toLowerCase();
            return produit.getNom().toLowerCase().contains(recherche)
                || produit.getCategorie().toLowerCase().contains(recherche);
        });
    });

    // SortedList : permet le tri par clic sur les colonnes
    SortedList<Produit> produitsTries = new SortedList<>(produitsFiltres);
    produitsTries.comparatorProperty().bind(tableauProduits.comparatorProperty());

    tableauProduits.setItems(produitsTries);
}
```

---

## 9. Navigation entre plusieurs vues FXML

### Pourquoi plusieurs vues ?

Dans une vraie application, on a souvent plusieurs écrans : une page d'accueil, une page de liste, une page de détail, une page de paramètres. Chaque écran est représenté par un fichier `.fxml` distinct avec son propre contrôleur.

### 9.1 Méthode 1 — Remplacer la scène entière

La façon la plus simple : on charge un nouveau FXML et on remplace le contenu de la fenêtre.

**Depuis un contrôleur :**
```java
import javafx.fxml.FXMLLoader;
import javafx.scene.Scene;
import javafx.stage.Stage;

@FXML
private void allerVersListeProduits() throws IOException {
    // Charger la nouvelle vue
    FXMLLoader loader = new FXMLLoader(
        getClass().getResource("liste-produits-view.fxml")
    );
    Scene nouvelleScene = new Scene(loader.load(), 600, 400);

    // Obtenir la fenêtre depuis n'importe quel Node
    Stage stage = (Stage) monBouton.getScene().getWindow();
    stage.setScene(nouvelleScene);
    stage.setTitle("Liste des produits");
}
```

---

### 9.2 Méthode 2 — Remplacer le contenu d'un BorderPane (recommandée)

C'est la méthode la plus utilisée dans les vraies applications. On garde une structure fixe (menu, barre du haut) et on remplace seulement la zone centrale.

**Structure :**
```
MainView.fxml (BorderPane)
├── TOP : barre de navigation fixe
├── LEFT : menu fixe
└── CENTER : contenu qui change selon l'onglet
```

**main-view.fxml :**
```xml
<BorderPane xmlns:fx="http://javafx.com/fxml"
            fx:controller="com.exemple.MainController">

    <top>
        <HBox style="-fx-background-color: #2c3e50; -fx-padding: 15;" spacing="10">
            <Label text="Mon App" style="-fx-text-fill: white; -fx-font-size: 18;"/>
        </HBox>
    </top>

    <left>
        <VBox spacing="5" style="-fx-background-color: #34495e; -fx-padding: 10;" prefWidth="160">
            <Button text="Accueil"   onAction="#allerAccueil"   maxWidth="Infinity" styleClass="btn-nav"/>
            <Button text="Produits"  onAction="#allerProduits"  maxWidth="Infinity" styleClass="btn-nav"/>
            <Button text="Commandes" onAction="#allerCommandes" maxWidth="Infinity" styleClass="btn-nav"/>
        </VBox>
    </left>

    <!-- contentPane reçoit les différentes vues -->
    <center>
        <StackPane fx:id="contentPane"/>
    </center>

</BorderPane>
```

**MainController.java :**
```java
import javafx.fxml.FXML;
import javafx.fxml.FXMLLoader;
import javafx.scene.Node;
import javafx.scene.layout.StackPane;
import java.io.IOException;

public class MainController {

    @FXML private StackPane contentPane;

    @FXML
    public void initialize() {
        // Charger la vue d'accueil au démarrage
        chargerVue("accueil-view.fxml");
    }

    @FXML private void allerAccueil()   { chargerVue("accueil-view.fxml"); }
    @FXML private void allerProduits()  { chargerVue("produits-view.fxml"); }
    @FXML private void allerCommandes() { chargerVue("commandes-view.fxml"); }

    // Méthode utilitaire pour charger une vue dans le contentPane
    private void chargerVue(String nomFxml) {
        try {
            FXMLLoader loader = new FXMLLoader(getClass().getResource(nomFxml));
            Node vue = loader.load();

            contentPane.getChildren().clear(); // supprimer la vue actuelle
            contentPane.getChildren().add(vue); // afficher la nouvelle vue

        } catch (IOException e) {
            System.out.println("Erreur chargement vue : " + e.getMessage());
        }
    }
}
```

---

### 9.3 Méthode 3 — Passer des données entre vues

Quand on navigue vers une nouvelle vue, on veut souvent lui passer des données (ex: le produit sélectionné pour afficher ses détails).

**Étape 1 — Le contrôleur de la vue de détail doit avoir une méthode pour recevoir les données :**

```java
// DetailProduitController.java
public class DetailProduitController {

    @FXML private Label labelNom;
    @FXML private Label labelPrix;
    @FXML private Label labelCategorie;

    // Méthode publique appelée par le contrôleur parent pour passer les données
    public void setProduit(Produit produit) {
        labelNom.setText(produit.getNom());
        labelPrix.setText(String.format("%.2f$", produit.getPrix()));
        labelCategorie.setText(produit.getCategorie());
    }
}
```

**Étape 2 — Le contrôleur parent charge la vue ET passe les données :**

```java
// ProduitsController.java
@FXML
private void voirDetail() {
    Produit selectionne = maListView.getSelectionModel().getSelectedItem();
    if (selectionne == null) return;

    try {
        FXMLLoader loader = new FXMLLoader(getClass().getResource("detail-produit-view.fxml"));
        Node vue = loader.load();

        // Récupérer le contrôleur de la nouvelle vue
        DetailProduitController ctrl = loader.getController();

        // Passer les données au contrôleur
        ctrl.setProduit(selectionne);

        // Afficher la vue
        contentPane.getChildren().clear();
        contentPane.getChildren().add(vue);

    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

---

### 9.4 Ouvrir une nouvelle fenêtre (popup)

```java
@FXML
private void ouvrirFenetreAjout() throws IOException {
    FXMLLoader loader = new FXMLLoader(getClass().getResource("ajout-produit-view.fxml"));

    Stage popup = new Stage();
    popup.setTitle("Ajouter un produit");
    popup.setScene(new Scene(loader.load(), 400, 300));

    // Modality.WINDOW_MODAL : bloque la fenêtre parente tant que le popup est ouvert
    popup.initModality(Modality.WINDOW_MODAL);
    popup.initOwner(monBouton.getScene().getWindow());

    popup.showAndWait(); // attend que le popup soit fermé

    // Après la fermeture du popup, on peut récupérer les données
    AjoutProduitController ctrl = loader.getController();
    Produit nouveauProduit = ctrl.getProduitCree();
    if (nouveauProduit != null) {
        tableauProduits.getItems().add(nouveauProduit);
    }
}
```

---

## 10. Animations

### Pourquoi des animations ?

Les animations rendent l'interface plus vivante et aident l'utilisateur à comprendre ce qui se passe (un élément qui apparaît, un message qui clignote pour attirer l'attention, etc.).

JavaFX offre plusieurs types d'animations via le package `javafx.animation`.

---

### 10.1 FadeTransition — Fondu

Fait apparaître ou disparaître un composant progressivement.

```java
import javafx.animation.FadeTransition;
import javafx.util.Duration;

// Faire apparaître un label (fondu entrant)
private void fadeIn(Node node) {
    FadeTransition fade = new FadeTransition(Duration.millis(500), node);
    fade.setFromValue(0.0); // complètement transparent
    fade.setToValue(1.0);   // complètement opaque
    fade.play();
}

// Faire disparaître un label (fondu sortant)
private void fadeOut(Node node) {
    FadeTransition fade = new FadeTransition(Duration.millis(500), node);
    fade.setFromValue(1.0);
    fade.setToValue(0.0);
    fade.setOnFinished(e -> node.setVisible(false)); // cacher après l'animation
    fade.play();
}

// Utilisation : afficher le résultat avec un fondu
@FXML
private void handleCalculer() {
    labelResultat.setOpacity(0);
    labelResultat.setText("Résultat : 10.79$");
    fadeIn(labelResultat);
}
```

---

### 10.2 TranslateTransition — Déplacement

Déplace un composant d'un point à un autre.

```java
import javafx.animation.TranslateTransition;

// Faire glisser un panneau depuis la gauche
private void glisserDepuisGauche(Node node) {
    TranslateTransition translate = new TranslateTransition(Duration.millis(400), node);
    translate.setFromX(-300); // départ à -300px (hors écran à gauche)
    translate.setToX(0);      // arrivée à sa position normale
    translate.play();
}

// Faire trembler un composant (pour signaler une erreur)
private void trembler(Node node) {
    TranslateTransition tremble = new TranslateTransition(Duration.millis(50), node);
    tremble.setFromX(0);
    tremble.setToX(10);
    tremble.setCycleCount(6);           // répéter 6 fois
    tremble.setAutoReverse(true);       // aller-retour
    tremble.setOnFinished(e -> node.setTranslateX(0)); // revenir à la position initiale
    tremble.play();
}
```

---

### 10.3 ScaleTransition — Zoom

Agrandit ou rétrécit un composant.

```java
import javafx.animation.ScaleTransition;

// Effet "pop" : agrandir puis revenir à la taille normale
private void popEffect(Node node) {
    ScaleTransition scale = new ScaleTransition(Duration.millis(200), node);
    scale.setFromX(1.0);
    scale.setFromY(1.0);
    scale.setToX(1.2);  // agrandir à 120%
    scale.setToY(1.2);
    scale.setAutoReverse(true);
    scale.setCycleCount(2); // aller puis retour
    scale.play();
}
```

---

### 10.4 RotateTransition — Rotation

```java
import javafx.animation.RotateTransition;

// Rotation continue (ex: icône de chargement)
private void tourner(Node node) {
    RotateTransition rotation = new RotateTransition(Duration.millis(1000), node);
    rotation.setFromAngle(0);
    rotation.setToAngle(360);
    rotation.setCycleCount(RotateTransition.INDEFINITE); // tourner indéfiniment
    rotation.setInterpolator(Interpolator.LINEAR);       // vitesse constante
    rotation.play();
}
```

---

### 10.5 SequentialTransition — Animations en séquence

Enchaîne plusieurs animations l'une après l'autre.

```java
import javafx.animation.*;

// Apparaître, trembler, puis disparaître
private void afficherErreurAnimee(Node node, String message) {
    if (node instanceof Label) {
        ((Label) node).setText(message);
    }

    FadeTransition fadeIn = new FadeTransition(Duration.millis(200), node);
    fadeIn.setFromValue(0); fadeIn.setToValue(1);

    TranslateTransition tremble = new TranslateTransition(Duration.millis(50), node);
    tremble.setFromX(0); tremble.setToX(8);
    tremble.setCycleCount(6); tremble.setAutoReverse(true);

    PauseTransition pause = new PauseTransition(Duration.seconds(2));

    FadeTransition fadeOut = new FadeTransition(Duration.millis(500), node);
    fadeOut.setFromValue(1); fadeOut.setToValue(0);

    SequentialTransition sequence = new SequentialTransition(fadeIn, tremble, pause, fadeOut);
    sequence.play();
}
```

---

### 10.6 Timeline — Animation personnalisée

`Timeline` est l'animation la plus flexible. Elle permet de définir des **KeyFrames** (images clés) à des moments précis.

```java
import javafx.animation.KeyFrame;
import javafx.animation.KeyValue;
import javafx.animation.Timeline;

// Animer une ProgressBar de 0 à 100% en 3 secondes
private void animerProgress(ProgressBar pb) {
    Timeline timeline = new Timeline(
        new KeyFrame(Duration.ZERO,        new KeyValue(pb.progressProperty(), 0)),
        new KeyFrame(Duration.seconds(3),  new KeyValue(pb.progressProperty(), 1))
    );
    timeline.play();
}

// Faire clignoter un label (ex: "NOUVEAU !")
private void clignoter(Label label) {
    Timeline clignotement = new Timeline(
        new KeyFrame(Duration.millis(0),   new KeyValue(label.opacityProperty(), 1.0)),
        new KeyFrame(Duration.millis(500), new KeyValue(label.opacityProperty(), 0.0)),
        new KeyFrame(Duration.millis(1000),new KeyValue(label.opacityProperty(), 1.0))
    );
    clignotement.setCycleCount(Timeline.INDEFINITE); // clignoter indéfiniment
    clignotement.play();
}
```

---

### 10.7 Animations au survol d'un bouton (hover)

```java
// Méthode utilitaire pour ajouter des effets de survol sur un bouton
private void ajouterEffetHover(Button bouton) {
    // Couleur originale
    String styleOriginal = bouton.getStyle();

    bouton.setOnMouseEntered(e -> {
        ScaleTransition scale = new ScaleTransition(Duration.millis(150), bouton);
        scale.setToX(1.05);
        scale.setToY(1.05);
        scale.play();
    });

    bouton.setOnMouseExited(e -> {
        ScaleTransition scale = new ScaleTransition(Duration.millis(150), bouton);
        scale.setToX(1.0);
        scale.setToY(1.0);
        scale.play();
    });
}
```

---

### 10.8 Récapitulatif des animations

| Animation | Effet | Propriété animée |
|---|---|---|
| `FadeTransition` | Fondu entrant/sortant | `opacity` (0.0 à 1.0) |
| `TranslateTransition` | Déplacement | `translateX`, `translateY` |
| `ScaleTransition` | Zoom | `scaleX`, `scaleY` |
| `RotateTransition` | Rotation | `rotate` |
| `SequentialTransition` | Séquence d'animations | — |
| `ParallelTransition` | Animations simultanées | — |
| `PauseTransition` | Attente | — |
| `Timeline` | Animation personnalisée | N'importe quelle propriété |

---

## 11. Exercices pratiques

---

### Exercice 1 — Explorateur de layouts

**Objectif :** Créer une application avec un `TabPane` qui présente un exemple de chaque layout.

**Instructions :**
- Créer un `TabPane` avec 4 onglets : "VBox", "HBox", "GridPane", "BorderPane"
- Dans chaque onglet, créer un exemple concret du layout correspondant
- Onglet VBox : un formulaire d'inscription (nom, email, mot de passe, bouton)
- Onglet HBox : une barre de boutons (Précédent, Page 1/5, Suivant)
- Onglet GridPane : un formulaire de produit (nom, prix, catégorie, bouton Ajouter)
- Onglet BorderPane : une mini-application avec menu, contenu et barre de statut

<details>
<summary>💡 Indices</summary>

- Pour le formulaire VBox, utilise `spacing="10"` et `padding="20"`
- Pour la barre HBox, le label "Page 1/5" doit prendre tout l'espace central : `HBox.hgrow="ALWAYS"` avec `maxWidth="Infinity"` et `alignment="CENTER"`
- Pour le GridPane, définit `hgap="10" vgap="8"` et utilise `GridPane.columnSpan="2"` pour le bouton
- Pour le BorderPane, la zone Left peut être un VBox de boutons de navigation avec `prefWidth="120"`

</details>

---

### Exercice 2 — Galerie d'images

**Objectif :** Créer une galerie d'images avec navigation.

**Instructions :**
- Créer une interface avec un `StackPane` central pour afficher l'image
- Ajouter deux boutons "◀ Précédent" et "Suivant ▶" dans un `HBox` en bas
- Afficher le numéro de l'image actuelle (ex: "2 / 5") entre les boutons
- Ajouter un `Label` en bas de l'image pour afficher le nom du fichier
- Quand on passe d'une image à l'autre, animer avec un `FadeTransition`
- Gérer les cas limites : désactiver "Précédent" à la première image, "Suivant" à la dernière

**Comportement attendu :**
```
[◀ Précédent]  [Image affichée]  [Suivant ▶]
               "2 / 5 — pizza.jpg"
```

<details>
<summary>💡 Indices</summary>

- Stocke les noms de fichiers dans une `List<String>` et garde un index `int indexActuel`
- Pour changer l'image avec animation :
  ```java
  FadeTransition fadeOut = new FadeTransition(Duration.millis(200), imageView);
  fadeOut.setToValue(0);
  fadeOut.setOnFinished(e -> {
      imageView.setImage(nouvelleImage);
      FadeTransition fadeIn = new FadeTransition(Duration.millis(200), imageView);
      fadeIn.setToValue(1);
      fadeIn.play();
  });
  fadeOut.play();
  ```
- Pour désactiver un bouton : `btnPrecedent.setDisable(indexActuel == 0)`

</details>

---

### Exercice 3 — Gestionnaire de produits complet

**Objectif :** Créer une application complète avec navigation, TableView, formulaire et animations.

**Structure de l'application :**
```
MainView (BorderPane)
├── TOP : barre avec le titre "Gestionnaire de produits"
├── LEFT : menu avec 2 boutons (Liste, Ajouter)
└── CENTER : zone de contenu qui change
    ├── liste-view.fxml : TableView des produits + bouton Supprimer
    └── ajout-view.fxml : formulaire d'ajout de produit
```

**Instructions — liste-view.fxml :**
- Un `TableView<Produit>` avec 3 colonnes : Nom, Prix, Catégorie
- Un champ de recherche au-dessus du tableau qui filtre en temps réel
- Un bouton "Supprimer" qui retire le produit sélectionné avec confirmation
- Un `Label` en bas qui affiche "X produit(s) — Total : Y$"

**Instructions — ajout-view.fxml :**
- Un `GridPane` avec les champs : Nom, Prix, Catégorie (ComboBox)
- Un bouton "Ajouter" qui valide et ajoute le produit à la liste
- Quand l'ajout réussit : afficher un message de succès avec `FadeTransition`
- Quand un champ est invalide : faire trembler le champ avec `TranslateTransition`

**Instructions — Navigation :**
- Le menu gauche permet de naviguer entre les deux vues
- Les données (la liste de produits) sont partagées entre les deux vues
- Quand on ajoute un produit dans `ajout-view`, il apparaît dans `liste-view`

**Indice pour partager les données :**

```java
// Créer une classe singleton pour les données partagées
public class DonneesApp {

    private static DonneesApp instance;
    private ObservableList<Produit> produits = FXCollections.observableArrayList();

    private DonneesApp() {}

    public static DonneesApp getInstance() {
        if (instance == null) instance = new DonneesApp();
        return instance;
    }

    public ObservableList<Produit> getProduits() { return produits; }
}

// Dans ListeController
tableauProduits.setItems(DonneesApp.getInstance().getProduits());

// Dans AjoutController
DonneesApp.getInstance().getProduits().add(nouveauProduit);
```

<details>
<summary>💡 Solution partielle — MainController.java</summary>

```java
public class MainController {

    @FXML private StackPane contentPane;

    @FXML
    public void initialize() {
        chargerVue("liste-view.fxml");
    }

    @FXML private void allerListe()  { chargerVue("liste-view.fxml"); }
    @FXML private void allerAjout()  { chargerVue("ajout-view.fxml"); }

    private void chargerVue(String nomFxml) {
        try {
            FXMLLoader loader = new FXMLLoader(getClass().getResource(nomFxml));
            Node vue = loader.load();

            // Animation de transition
            vue.setOpacity(0);
            contentPane.getChildren().setAll(vue);

            FadeTransition fade = new FadeTransition(Duration.millis(250), vue);
            fade.setFromValue(0);
            fade.setToValue(1);
            fade.play();

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

</details>