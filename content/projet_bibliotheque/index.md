+++
title = "BiblioAventure"
weight = 13
url = "/biblioGame/"

+++
# 🎮 PROJET CODEX ARCANUM - L'AVENTURE COMPLÈTE DE LA POO !

<div align="center">

## 🌟 Bienvenue dans l'Aventure des Bibliothèques Légendaires ! 🌟

### 🎵 Musique d'Aventure Épique 🎵

<audio controls autoplay loop volume="0.5">
  <source src="/420-210/sons/son-action-mystery-1.mp3" type="audio/mpeg">
  🎵 Thème d'aventure épique
</audio>

<p style="color: #666; font-style: italic; margin-top: 10px;">
🎧 Active le son pour une expérience immersive !
</p>

</div>

---

## 📊 Ton Tableau de Bord

<div style="background: #2c3e50; color: white; padding: 20px; border-radius: 10px; margin: 20px 0;">
  <h3>🎮 Statistiques du Joueur</h3>
  <p>🏆 Points Totaux : <span id="total-points" style="color: #ffd700; font-size: 1.5em; font-weight: bold;">0</span></p>
  <p>⭐ Niveau Actuel : <span id="player-level">1</span> - Apprenti Codeur</p>
  <p>🎯 Prochain niveau : 30 points</p>
  <div style="background: #34495e; height: 20px; border-radius: 10px; overflow: hidden; margin-top: 10px;">
    <div id="progress-bar" style="background: linear-gradient(90deg, #00ff00, #00cc00); height: 100%; width: 0%; transition: width 0.5s;"></div>
  </div>
</div>

---

## 🗺️ CARTE COMPLÈTE DE L'AVENTURE

```
    🏁 NIVEAU 1          ⚔️ NIVEAU 2         🏰 NIVEAU 3         🔮 NIVEAU 4
   Premier Livre      Bouclier Magique    Royaume Livres     Grimoire Dynamique
      [15 pts]            [15 pts]            [20 pts]            [20 pts]
   
    🐉 NIVEAU 5          🌈 NIVEAU 6         🏛️ NIVEAU 7         👑 NIVEAU 8
  Dragon Héritage     Métamorphose      Temple Abstrait       Boss Final
      [25 pts]            [25 pts]            [30 pts]            [50 pts]

                        TOTAL : 200 POINTS POSSIBLES !
```

### 🎯 Système de progression:
- ⭐ **Bronze** (0-30 pts) : Apprenti Codeur
- ⭐⭐ **Argent** (31-60 pts) : Codeur Compétent  
- ⭐⭐⭐ **Or** (61-100 pts) : Maître POO
- ⭐⭐⭐⭐ **Platine** (101-150 pts) : Grand Architecte
- 👑 **Légende** (151+ pts) : Légende Vivante !

---

## 🏛️ Choisis ta bibliothèque légendaire !

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin: 20px 0;">

<div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 15px; border-radius: 10px; color: white; text-align: center;">
  <h4>🔮 Codex Arcanum</h4>
  <p style="font-size: 0.85em;">Sortilèges de code</p>
</div>

<div style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); padding: 15px; border-radius: 10px; color: white; text-align: center;">
  <h4>⚔️ Grimoire du Guerrier</h4>
  <p style="font-size: 0.85em;">Combat contre bugs</p>
</div>

<div style="background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%); padding: 15px; border-radius: 10px; color: white; text-align: center;">
  <h4>🌊 Océan Connaissance</h4>
  <p style="font-size: 0.85em;">Algorithmes fluides</p>
</div>

<div style="background: linear-gradient(135deg, #fa709a 0%, #fee140 100%); padding: 15px; border-radius: 10px; color: white; text-align: center;">
  <h4>🔥 Forge du Phoenix</h4>
  <p style="font-size: 0.85em;">Créateurs passionnés</p>
</div>

</div>

---

# 🎮 NIVEAU 1 - LE PREMIER LIVRE MAGIQUE

<div style="text-align: center; margin: 20px 0;">
  <audio controls>
    <source src="https://cdn.pixabay.com/download/audio/2022/05/27/audio_1808fbf07a.mp3" type="audio/mpeg">
    🎵 Musique Niveau 1
  </audio>
</div>

<div style="background: linear-gradient(135deg, #667eea, #764ba2); color: white; padding: 20px; border-radius: 15px; margin: 20px 0;">

### 📜 Histoire

*"Bienvenue jeune apprenti ! La bibliothèque est vide... Ta première mission : créer ton premier livre magique qui pourra être emprunté !"*

</div>

## 💎 Points: 15 pts | ⏱️ Temps estimé: 1-2 heures

---

## 🎯 Mission 1.1 : Créer la classe Livre

### Attributs à créer (tous **private**):

| Attribut | Type | Valeur initiale |
|----------|------|-----------------|
| `titre` | `String` | Via constructeur |
| `auteur` | `String` | Via constructeur |
| `annee` | `int` | Via constructeur |
| `estEmprunte` | `boolean` | `false` |

<div style="background: #e3f2fd; padding: 15px; border-left: 4px solid #2196f3; margin: 15px 0;">

### 🎓 Concept POO : L'ENCAPSULATION

**Félicitations !** En déclarant tes attributs `private`, tu viens d'appliquer le principe d'**ENCAPSULATION** !

**C'est quoi l'encapsulation ?**
- Cacher les détails internes d'une classe
- Empêcher l'accès direct aux attributs depuis l'extérieur
- `private` = les attributs sont protégés ✅

**Pourquoi c'est important ?**
- Protège les données contre les modifications non contrôlées
- On peut changer l'implémentation interne sans casser le code externe
- C'est un des **4 piliers de la POO** !

**Note :** Au Niveau 2, tu ajouteras des getters/setters pour permettre un accès **contrôlé** à ces attributs privés.

</div>

### Constructeur:
- **Paramètres:** `String titre, String auteur, int annee`
- **Actions:**
  1. Initialiser `titre`, `auteur`, `annee` avec les paramètres
  2. Mettre `estEmprunte` à `false`
  3. Afficher: `"✨ NOUVEAU LIVRE CRÉÉ : " + titre`

<details>
<summary>💡 Aide syntaxe</summary>

```java
public class Livre {
    private Type attribut;
    
    public Livre(Type param) {
        this.attribut = param;
    }
}
```
</details>

---

## 🎯 Mission 1.2 : Méthode `afficher()`

**Signature:** `public void afficher()`

**Actions à faire:**
1. Afficher une ligne: `╔════════════════════════════════╗`
2. Afficher: `"  📚 " + titre`
3. Afficher: `"  ✍️  " + auteur`
4. Afficher: `"  📅 " + annee`
5. **SI** `estEmprunte` est vrai:
   - Afficher: `"  🔴 EMPRUNTÉ"`
6. **SINON:**
   - Afficher: `"  🟢 DISPONIBLE"`
7. Afficher une ligne: `╚════════════════════════════════╝`

---

## 🎯 Mission 1.3 : Méthode `emprunter()`

**Signature:** `public void emprunter()`

**Logique:**
```
SI le livre EST DÉJÀ emprunté:
    Afficher "❌ Oups ! '[titre]' est déjà emprunté !"
SINON:
    Mettre estEmprunte à true
    Afficher "✅ Super ! Tu as emprunté '[titre]' !"
    Afficher "🎉 +1 emprunt réussi !"
```

---

## 🎯 Mission 1.4 : Méthode `retourner()`

**Signature:** `public void retourner()`

**Logique:**
```
SI le livre EST emprunté:
    Mettre estEmprunte à false
    Afficher "✅ Merci ! '[titre]' est de retour !"
    Afficher "⭐ +1 point de karma !"
SINON:
    Afficher "⚠️ Hmm... '[titre]' n'était pas emprunté !"
```

---

## 🧪 Test Niveau 1

Crée `TestNiveau1.java` et complète:

```java
public class TestNiveau1 {
    public static void main(String[] args) {
        // 🎯 MISSION : Crée 3 livres différents
        Livre livre1 = // TON CODE
        Livre livre2 = // TON CODE  
        Livre livre3 = // TON CODE
        
        // Affiche les 3 livres
        
        // Emprunte livre1
        
        // Essaie d'emprunter livre1 à nouveau
        
        // Retourne livre1
        
        // Essaie de retourner livre3 (pas emprunté)
        
        System.out.println("\n🏆 NIVEAU 1 TERMINÉ !");
    }
}
```

### ✅ Checklist:
- [ ] 3 livres créés
- [ ] 3 livres affichés
- [ ] 1 emprunt réussi
- [ ] 1 tentative sur livre déjà emprunté (erreur attendue)
- [ ] 1 retour réussi
- [ ] 1 tentative de retour sur livre non emprunté (erreur attendue)

---

## 🏆 Défis Bonus (+5 pts chacun)

### Défi 1.A : Attribut `nombrePages`
1. Ajoute attribut `private int nombrePages`
2. Modifie constructeur pour l'accepter
3. Affiche-le dans `afficher()`
4. Crée méthode `public boolean isLong()` qui retourne `true` si > 400 pages

### Défi 1.B : 5 livres de genres variés
Crée 5 livres : Fantasy, SF, Romance, Horreur, Classique

### Défi 1.C : Combo parfait
3 emprunts réussis d'affilée sans erreur

---

# 🔑 NIVEAU 2 - LES PORTES D'ACCÈS (GETTERS/SETTERS)

<div style="text-align: center; margin: 20px 0;">
  <audio controls>
    <source src="https://cdn.pixabay.com/download/audio/2022/05/27/audio_1808fbf07a.mp3" type="audio/mpeg">
    🎵 Musique Niveau 2
  </audio>
</div>

<div style="background: linear-gradient(135deg, #667eea, #764ba2); color: white; padding: 20px; border-radius: 15px; margin: 20px 0;">

### 📜 Histoire

*"Tes attributs sont déjà protégés (private = ENCAPSULATION ✅), mais maintenant on ne peut plus les lire ! Crée des PORTES D'ACCÈS CONTRÔLÉES (getters/setters) avec des GARDIENS (validations) !"*

### 🎓 Rappel Important

**Tu as DÉJÀ l'encapsulation depuis le Niveau 1 !**
- 🆕 Maintenant : Ajouter des **accesseurs** (getters/setters)
- 🆕 Bonus : Ajouter des **validations** dans les setters

</div>

## 💎 Points: 15 pts | ⏱️ Temps: 1-2 heures

---

## 🎯 Mission 2.1 : Ajouter les Getters

### 🎓 Concept : Les Getters (Accesseurs)

**Problème actuel :**
- Tes attributs sont `private` (encapsulation ✅)
- Impossible de les lire depuis l'extérieur !
- `livre.titre` → **ERREUR** ❌

**Solution : Les Getters**
- Méthodes `public` qui **retournent** la valeur des attributs privés
- Permettent un accès **en lecture** contrôlé
- Convention : `get` + nom de l'attribut (ex: `getTitre()`)
- Exception pour `boolean` : on utilise `is` (ex: `isEstEmprunte()`)

---

Crée ces méthodes dans `Livre.java`:

| Méthode | Retour | Action |
|---------|--------|--------|
| `getTitre()` | `String` | Retourne `titre` |
| `getAuteur()` | `String` | Retourne `auteur` |
| `getAnnee()` | `int` | Retourne `annee` |
| `getNombrePages()` | `int` | Retourne `nombrePages` |
| `isEstEmprunte()` | `boolean` | Retourne `estEmprunte` |

<details>
<summary>💡 Template getter</summary>

```java
public Type getNom() {
    return attribut;
}

// Pour boolean:
public boolean isNom() {
    return attributBoolean;
}
```
</details>

---

## 🎯 Mission 2.2 : Setter `setAnnee()` avec validation

### 🎓 Concept : Les Setters (Mutateurs)

**À quoi servent les setters ?**
- Permettent de **modifier** les attributs privés depuis l'extérieur
- **MAIS** avec des **validations** ! C'est ça le pouvoir !

**Sans setter (problème) :**
```java
// Impossible de modifier, attribut private
livre.annee = 2025;  // ERREUR ❌
```

**Avec setter simple (pas terrible) :**
```java
public void setAnnee(int annee) {
    this.annee = annee;  // N'importe quelle valeur acceptée
}
// Problème : on pourrait mettre annee = -500 ou 9999 !
```

**Avec setter + VALIDATION (🏆 MEILLEUR) :**
```java
public void setAnnee(int annee) {
    if (annee >= 1000 && annee <= 2024) {
        this.annee = annee;  // Valeur valide ✅
    } else {
        // Refuser la valeur invalide ❌
    }
}
```

**Avantages :**
- ✅ Protège les données (pas de valeurs absurdes)
- ✅ Attribut reste `private`
- ✅ Contrôle total sur les modifications

---

**Signature:** `public void setAnnee(int annee)`

**Logique:**
```
SI annee est entre 1000 ET 2024 (inclus):
    Modifier this.annee
    Afficher "✅ Année validée : [annee]"
SINON:
    Afficher "⚠️ ALERTE ! Année invalide détectée !"
    Afficher "🛡️ Bouclier activé ! Année réinitialisée à 2000"
    Mettre this.annee à 2000
```

---

## 🎯 Mission 2.3 : Setter `setNombrePages()` avec validation

**Signature:** `public void setNombrePages(int nombrePages)`

**Logique:**
```
SI nombrePages est entre 1 ET 2000 (inclus):
    Modifier this.nombrePages
    Afficher "✅ Pages validées : [nombrePages]"
SINON:
    Afficher "⚠️ ALERTE ! Nombre de pages bizarre !"
    Afficher "🛡️ Bouclier activé ! Pages réinitialisées à 100"
    Mettre this.nombrePages à 100
```

---

## 🎯 Mission 2.4 : Système de Popularité

### Nouvel attribut:
- `private int niveauPopularite` (initialiser à 0 dans constructeur)

### Méthode `ajouterEtoile()`:
**Signature:** `public void ajouterEtoile()`

**Logique:**
```
SI niveauPopularite < 5:
    Augmenter niveauPopularite de 1
    Afficher "⭐ Nouvelle étoile ! [titre] a [niveauPopularite] étoile(s) !"
SINON:
    Afficher "🌟 Maximum atteint ! Ce livre est une LÉGENDE !"
```

### Méthode `isPopulaire()`:
**Signature:** `public boolean isPopulaire()`
**Retourne:** `true` si `niveauPopularite >= 4`, sinon `false`

### Getter:
**Signature:** `public int getNiveauPopularite()`

---

## 🎯 Mission 2.5 : Afficher les étoiles

Dans `afficher()`, après l'année, ajoute:

```java
System.out.print("  ⭐ ");
for (int i = 0; i < niveauPopularite; i++) {
    System.out.print("★");
}
for (int i = niveauPopularite; i < 5; i++) {
    System.out.print("☆");
}
System.out.println();
```

---

## 🎯 Mission 2.6 : Méthode `calculerAge()`

**Signature:** `public int calculerAge()`

**Logique:**
```
age = 2024 - annee
SI age > 50:
    Afficher "📜 Livre ANCIEN ! [age] ans !"
Retourner age
```

---

## 🧪 Test Niveau 2

```java
public class TestNiveau2 {
    public static void main(String[] args) {
        Livre livre = new Livre("1984", "Orwell", 1949, 328);
        
        // Teste setAnnee avec valeur valide
        
        // Teste setAnnee avec 3000 (invalide)
        
        // Teste setNombrePages avec 350
        
        // Teste setNombrePages avec -50 (invalide)
        
        // Ajoute 4 étoiles
        
        // Affiche si populaire
        
        // Calcule et affiche l'âge
        
        // Affiche le livre complet
    }
}
```

---

## 🏆 Défis Bonus

### Défi 2.A : `isClassique()`
Méthode qui retourne `true` si livre a plus de 30 ans

### Défi 2.B : Compteur d'erreurs
Attribut qui compte les validations échouées

### Défi 2.C : Livre 5 étoiles
Monte un livre à 5 étoiles et vois le message spécial

---

# 🏰 NIVEAU 3 - LE ROYAUME DES LIVRES (TABLEAUX)

<div style="text-align: center; margin: 20px 0;">
  <audio controls>
    <source src="https://cdn.pixabay.com/download/audio/2022/05/27/audio_1808fbf07a.mp3" type="audio/mpeg">
    🎵 Musique Niveau 3
  </audio>
</div>

<div style="background: linear-gradient(135deg, #667eea, #764ba2); color: white; padding: 20px; border-radius: 15px; margin: 20px 0;">

### 📜 Histoire

*"Tes livres sont éparpillés ! Construis un ROYAUME (Bibliotheque) pour les organiser dans un tableau !"*

</div>

## 💎 Points: 20 pts | ⏱️ Temps: 2-3 heures

---

## 🎯 Mission 3.1 : Créer la classe Bibliotheque

**Fichier:** `Bibliotheque.java`

### Attributs (tous **private**):

| Attribut | Type | Description |
|----------|------|-------------|
| `nom` | `String` | Nom de la bibliothèque |
| `livres` | `Livre[]` | Tableau de livres |
| `nombreLivres` | `int` | Nombre de livres actuellement ajoutés |
| `pointsGloire` | `int` | Points du joueur |

### Constructeur:
**Paramètres:** `String nom, int capacite`

**Actions:**
1. Initialiser `this.nom = nom`
2. Créer le tableau: `this.livres = new Livre[capacite]`
3. Initialiser `nombreLivres = 0`
4. Initialiser `pointsGloire = 0`
5. Afficher message de bienvenue:
```
🏰════════════════════════════════════🏰
   LE ROYAUME DE [NOM] EST NÉ !
   Capacité : [capacite] livres
🏰════════════════════════════════════🏰
```

---

## 🎯 Mission 3.2 : Méthode `ajouterLivre()`

**Signature:** `public void ajouterLivre(Livre livre)`

**Logique:**
```
SI nombreLivres < livres.length:
    livres[nombreLivres] = livre
    nombreLivres++
    pointsGloire += 10
    
    Afficher "✨ [titre du livre] a rejoint le royaume !"
    Afficher "🏆 +10 points de gloire ! Total : [pointsGloire]"
    
    SI nombreLivres == 5:
        Afficher "🎉 ACHIEVEMENT : 'Collectionneur' !"
    SI nombreLivres == 10:
        Afficher "🎊 ACHIEVEMENT : 'Grande Bibliothèque' !"
SINON:
    Afficher "💥 OH NON ! Le royaume est PLEIN !"
    Afficher "🏗️ Conseil : Agrandis ton royaume !"
```

<details>
<summary>💡 Aide: Accéder au titre du livre</summary>

```java
String titre = livre.getTitre();
```
</details>

---

## 🎯 Mission 3.3 : Méthode `afficherCarte()`

**Signature:** `public void afficherCarte()`

**Actions:**
1. Afficher le titre:
```
╔════════════════════════════════════════╗
║   🗺️  CARTE DU ROYAUME : [NOM]
╚════════════════════════════════════════╝
```

2. Afficher: `"📊 Livres : " + nombreLivres + "/" + livres.length`
3. Afficher: `"🏆 Gloire : " + pointsGloire + " points"`
4. Ligne vide

5. **SI** `nombreLivres == 0`:
   - Afficher: `"🏜️ Le royaume est vide... Ajoute des livres !"`
6. **SINON:**
   - Boucle `for` de `i=0` à `i < nombreLivres`:
     ```
     Créer variable: statut = livres[i].isEstEmprunte() ? "🔴" : "🟢"
     Afficher: "[i+1]. [statut] [titre] - [auteur]"
     ```

7. Ligne vide

<details>
<summary>💡 Template boucle</summary>

```java
for (int i = 0; i < nombreLivres; i++) {
    Livre livre = livres[i];
    String statut = livre.isEstEmprunte() ? "🔴" : "🟢";
    System.out.println((i+1) + ". " + statut + " " + 
                      livre.getTitre() + " - " + livre.getAuteur());
}
```
</details>

---

## 🎯 Mission 3.4 : Méthode `afficherDisponibles()`

**Signature:** `public void afficherDisponibles()`

**Logique:**
```
Afficher "💎 ═══ TRÉSORS DISPONIBLES ═══ 💎"
aucun = true

Pour chaque livre de 0 à nombreLivres:
    SI livre n'est PAS emprunté:
        Afficher "  ✨ [titre]"
        aucun = false

SI aucun est resté true:
    Afficher "  😱 Tous les trésors sont empruntés !"

Ligne vide
```

---

## 🎯 Mission 3.5 : Méthode `chercherLivre()`

**Signature:** `public Livre chercherLivre(String titre)`

**Logique:**
```
Afficher "🔍 Recherche de '[titre]'..."

Pour i de 0 à nombreLivres:
    SI livres[i].getTitre().equalsIgnoreCase(titre):
        Afficher "✅ TROUVÉ ! Position : [i+1]"
        Retourner livres[i]

Afficher "❌ Trésor introuvable..."
Retourner null
```

---

## 🎯 Mission 3.6 : Méthode `emprunterLivre()`

**Signature:** `public void emprunterLivre(String titre)`

**Logique:**
```
Afficher "🎮 ═══ MISSION D'EMPRUNT ═══"
livre = chercherLivre(titre)

SI livre != null:
    Appeler livre.emprunter()
    
    SI livre.isEstEmprunte() est true:
        pointsGloire += 15
        Afficher "🎉 +15 points ! Total : [pointsGloire]"
    SINON:
        pointsGloire -= 5
        Afficher "😢 -5 points..."
```

---

## 🎯 Mission 3.7 : Getter

**Signature:** `public int getPointsGloire()`
**Retourne:** `pointsGloire`

---

## 🧪 Test Niveau 3

```java
public class TestNiveau3 {
    public static void main(String[] args) {
        // Crée une bibliothèque (choisis un nom épique!)
        Bibliotheque biblio = new Bibliotheque("Codex Arcanum", 10);
        
        // Ajoute 5 livres minimum
        
        
        // Affiche la carte
        
        
        // Emprunte 3 livres
        
        
        // Affiche les disponibles
        
        
        // Affiche les points
        System.out.println("Points: " + biblio.getPointsGloire());
    }
}
```

---

## 🏆 Défis Bonus

### Défi 3.A : 100 points de gloire
Optimise pour atteindre 100 points !

### Défi 3.B : Royaume complet
Remplis les 10 emplacements

### Défi 3.C : Combo 5
5 emprunts sans erreur d'affilée

---

# 🔮 NIVEAU 4 - LE GRIMOIRE DYNAMIQUE (ARRAYLIST)

<div style="background: linear-gradient(135deg, #667eea, #764ba2); color: white; padding: 20px; border-radius: 15px; margin: 20px 0;">

### 📜 Histoire

*"Un sorcier t'offre le GRIMOIRE DYNAMIQUE - un tableau INFINI ! Plus de limite de capacité !"*

</div>

## 💎 Points: 20 pts | ⏱️ Temps: 2 heures

---

## 🎯 Mission 4.1 : Convertir en ArrayList

### Modifications dans `Bibliotheque.java`:

**Étape 1:** Ajoute en haut du fichier:
```java
import java.util.ArrayList;
```

**Étape 2:** Change les attributs:
- ❌ Enlève: `private Livre[] livres;`
- ❌ Enlève: `private int nombreLivres;`
- ✅ Ajoute: `private ArrayList<Livre> livres;`

**Étape 3:** Modifie le constructeur:
- **Paramètres:** Seulement `String nom` (plus de capacité!)
- **Initialisation:** `this.livres = new ArrayList<Livre>();`
- **Message:** Change "Capacité: ..." pour "✨ Capacité : ILLIMITÉE ! ✨"

---

## 🎯 Mission 4.2 : Adapter `ajouterLivre()`

**Nouvelle logique:**
```
livres.add(livre)  // Plus besoin de vérifier la capacité!
pointsGloire += 10

Afficher "✨ [titre] invoqué dans le grimoire !"
Afficher "🏆 +10 points ! Total : [pointsGloire]"

SI livres.size() == 5:
    Afficher "🎉 ACHIEVEMENT : 'Collectionneur' !"
SI livres.size() == 15:
    Afficher "🎊 MEGA ACHIEVEMENT : 'Bibliothèque Légendaire' !"
    pointsGloire += 50
```

---

## 🎯 Mission 4.3 : Adapter `afficherCarte()`

**Changements:**
- Remplace `nombreLivres` par `livres.size()`
- Remplace `livres.length` par "∞"
- Boucle: `for (int i = 0; i < livres.size(); i++)`
- Accès: `Livre livre = livres.get(i);`

**Ou utilise for-each:**
```java
int compteur = 1;
for (Livre livre : livres) {
    // Afficher avec compteur++
}
```

---

## 🎯 Mission 4.4 : Adapter `afficherDisponibles()`

**Changements:**
- Utilise `for (Livre livre : livres)` au lieu de boucle avec index

---

## 🎯 Mission 4.5 : Adapter `chercherLivre()`

**Nouvelle version avec for-each:**
```java
for (Livre livre : livres) {
    if (livre.getTitre().equalsIgnoreCase(titre)) {
        System.out.println("✅ TROUVÉ !");
        return livre;
    }
}
System.out.println("❌ Introuvable...");
return null;
```

---

## 🎯 Mission 4.6 : NOUVELLE Méthode `supprimerLivre()`

**Signature:** `public void supprimerLivre(String titre)`

**Logique:**
```
livre = chercherLivre(titre)

SI livre != null:
    livres.remove(livre)
    Afficher "💨 [titre] a été banni du grimoire !"
    Afficher "📊 Livres restants : [livres.size()]"
```

---

## 🎯 Mission 4.7 : NOUVELLE Méthode `rechercherParAuteur()`

**Signature:** `public void rechercherParAuteur(String auteur)`

**Logique:**
```
Afficher "🎯 ═══ QUÊTE : Livres de [auteur] ═══"
trouve = false
compte = 0

Pour chaque livre dans livres:
    SI livre.getAuteur().equalsIgnoreCase(auteur):
        Afficher "  ✨ [titre] ([année])"
        trouve = true
        compte++

SI trouve:
    pointsGloire += (compte * 5)
    Afficher "🎉 Quête réussie ! [compte] livre(s) trouvé(s) !"
    Afficher "🏆 +[compte*5] points !"
SINON:
    Afficher "😢 Quête échouée..."
```

---

## 🧪 Test Niveau 4

```java
public class TestNiveau4 {
    public static void main(String[] args) {
        // Crée bibliothèque SANS limite !
        Bibliotheque grimoire = new Bibliotheque("Le Grimoire Infini");
        
        // Ajoute 7+ livres (teste l'illimité!)
        
        
        // Recherche par auteur
        
        
        // Supprime un livre
        
        
        // Affiche la carte finale
        
    }
}
```

---

# 🐉 NIVEAU 5 - LE DRAGON DE L'HÉRITAGE

<div style="background: linear-gradient(135deg, #667eea, #764ba2); color: white; padding: 20px; border-radius: 15px; margin: 20px 0;">

### 📜 Histoire

*"La bibliothèque a des DVDs, Magazines ! Utilise l'HÉRITAGE pour créer différents types de documents !"*

</div>

## 💎 Points: 25 pts | ⏱️ Temps: 3 heures

---

## 🎯 Mission 5.1 : Créer la classe parent `Document`

**Fichier:** `Document.java`

### Attributs (tous **private**):
- `String titre`
- `int annee`
- `boolean estEmprunte`

### Constructeur:
**Paramètres:** `String titre, int annee`
**Actions:** Initialiser les 3 attributs (estEmprunte à false)

### Méthodes à créer:

#### Getters:
- `public String getTitre()`
- `public int getAnnee()`
- `public boolean isEstEmprunte()`

#### `emprunter()`:
```
SI estEmprunte:
    Afficher "❌ '[titre]' déjà emprunté !"
SINON:
    estEmprunte = true
    Afficher "✅ '[titre]' emprunté !"
```

#### `retourner()`:
```
SI estEmprunte:
    estEmprunte = false
    Afficher "✅ '[titre]' retourné !"
SINON:
    Afficher "⚠️ '[titre]' pas emprunté."
```

#### `afficher()`:
```
Afficher "Titre: [titre]"
Afficher "Année: [annee]"
SI estEmprunte:
    Afficher "Statut: Emprunté"
SINON:
    Afficher "Statut: Disponible"
```

---

## 🎯 Mission 5.2 : Créer `Livre` qui hérite de `Document`

**Fichier:** Modifier `Livre.java`

**Changement de déclaration:**
```java
public class Livre extends Document {
    // ...
}
```

### Nouveaux attributs privés (en plus de ceux hérités):
- `String auteur`
- `int nombrePages`

### Nouveau constructeur:
```java
public Livre(String titre, String auteur, int annee, int nombrePages) {
    super(titre, annee);  // Appelle constructeur parent
    this.auteur = auteur;
    this.nombrePages = nombrePages;
}
```

### Getters spécifiques:
- `public String getAuteur()`
- `public int getNombrePages()`

### Méthode spécifique:
```java
public boolean isLong() {
    return nombrePages > 400;
}
```

### Redéfinir `afficher()`:
```java
@Override
public void afficher() {
    super.afficher();  // Appelle version parent
    System.out.println("Auteur: " + auteur);
    System.out.println("Pages: " + nombrePages);
}
```

---

## 🎯 Mission 5.3 : Créer la classe `Magazine`

**Fichier:** `Magazine.java`

**Déclaration:** `public class Magazine extends Document`

### Attributs privés:
- `int numero`
- `String mois`

### Constructeur:
**Paramètres:** `String titre, int annee, int numero, String mois`
**Action:** 
```java
super(titre, annee);
this.numero = numero;
this.mois = mois;
```

### Getters:
- `public int getNumero()`
- `public String getMois()`

### Redéfinir `afficher()`:
```java
@Override
public void afficher() {
    super.afficher();
    System.out.println("Numéro: " + numero);
    System.out.println("Mois: " + mois);
}
```

### Redéfinir `emprunter()`:
```java
@Override
public void emprunter() {
    super.emprunter();
    if (isEstEmprunte()) {
        System.out.println("📰 À retourner dans 7 jours !");
    }
}
```

---

## 🎯 Mission 5.4 : Créer la classe `DVD`

**Fichier:** `DVD.java`

**Déclaration:** `public class DVD extends Document`

### Attributs privés:
- `String realisateur`
- `int dureeMinutes`

### Constructeur:
**Paramètres:** `String titre, int annee, String realisateur, int dureeMinutes`

### Getters:
- `public String getRealisateur()`
- `public int getDureeMinutes()`

### Méthode spéciale `getDureeFormatee()`:
**Signature:** `public String getDureeFormatee()`
**Logique:**
```
heures = dureeMinutes / 60
minutes = dureeMinutes % 60
Retourner heures + "h" + minutes
```

### Redéfinir `afficher()`:
Appelle parent puis affiche réalisateur et durée formatée

---

## 🧪 Test Niveau 5

```java
public class TestNiveau5 {
    public static void main(String[] args) {
        // Crée 1 livre
        Livre livre = new Livre("Dune", "Herbert", 1965, 688);
        
        // Crée 1 magazine
        Magazine mag = new Magazine("Wired", 2024, 345, "Mars");
        
        // Crée 1 DVD
        DVD dvd = new DVD("Matrix", 1999, "Wachowski", 136);
        
        // Affiche les 3
        
        // Emprunte les 3 (observe les messages différents!)
        
        // Teste isLong() sur le livre
        
        // Teste getDureeFormatee() sur le DVD
    }
}
```

---

## 🏆 Défis Bonus

### Défi 5.A : Classe `BD`
Crée `BD extends Livre` avec attribut `dessinateur`

### Défi 5.B : Classe `CD`
Crée `CD extends Document` avec `artiste` et `nombrePistes`

---

# 🌈 NIVEAU 6 - LA MÉTAMORPHOSE (POLYMORPHISME)

<div style="background: linear-gradient(135deg, #667eea, #764ba2); color: white; padding: 20px; border-radius: 15px; margin: 20px 0;">

### 📜 Histoire

*"Modifie Bibliotheque pour gérer TOUS les types de documents avec polymorphisme !"*

</div>

## 💎 Points: 25 pts | ⏱️ Temps: 2-3 heures

---

## 🎯 Mission 6.1 : Modifier Bibliotheque

**Dans `Bibliotheque.java`:**

**Changement d'attribut:**
- ❌ Enlève: `private ArrayList<Livre> livres;`
- ✅ Ajoute: `private ArrayList<Document> documents;`

**Dans le constructeur:**
```java
this.documents = new ArrayList<Document>();
```

---

## 🎯 Mission 6.2 : Renommer et adapter `ajouterDocument()`

**Anciennement `ajouterLivre()`**

**Nouvelle signature:** `public void ajouterDocument(Document doc)`

**Logique:**
```
documents.add(doc)
pointsGloire += 10

Afficher "➕ '[doc.getTitre()]' ajouté !"
Afficher "🏆 +10 points ! Total : [pointsGloire]"
```

---

## 🎯 Mission 6.3 : Adapter `afficherCatalogue()`

**Anciennement `afficherCarte()`**

**Logique:**
```
Afficher titre catalogue

Pour i de 0 à documents.size():
    doc = documents.get(i)
    
    Créer variable type:
        SI doc instanceof Livre:
            type = "[LIVRE]"
        SINON SI doc instanceof Magazine:
            type = "[MAGAZINE]"
        SINON SI doc instanceof DVD:
            type = "[DVD]"
        SINON:
            type = "[DOCUMENT]"
    
    Afficher "[i+1]. [type] [titre]"
```

<details>
<summary>💡 Aide instanceof</summary>

```java
if (doc instanceof Livre) {
    // C'est un livre
} else if (doc instanceof Magazine) {
    // C'est un magazine
}
```
</details>

---

## 🎯 Mission 6.4 : Méthode `afficherLivres()`

**Signature:** `public void afficherLivres()`

**Logique:**
```
Afficher "📚 ═══ LIVRES ═══"

Pour chaque doc dans documents:
    SI doc instanceof Livre:
        Caster: Livre livre = (Livre) doc
        Afficher "- [titre] par [auteur]"
```

<details>
<summary>💡 Aide casting</summary>

```java
if (doc instanceof Livre) {
    Livre livre = (Livre) doc;
    // Maintenant on peut utiliser livre.getAuteur()
}
```
</details>

---

## 🎯 Mission 6.5 : Méthode `afficherMagazines()`

**Signature:** `public void afficherMagazines()`

**Logique similaire à `afficherLivres()` mais pour Magazine**

---

## 🎯 Mission 6.6 : Méthode `afficherStatistiques()`

**Signature:** `public void afficherStatistiques()`

**Logique:**
```
nbLivres = 0
nbMagazines = 0
nbDVDs = 0

Pour chaque doc dans documents:
    SI doc instanceof Livre: nbLivres++
    SINON SI doc instanceof Magazine: nbMagazines++
    SINON SI doc instanceof DVD: nbDVDs++

Afficher les totaux
```

---

## 🎯 Mission 6.7 : Adapter `emprunterDocument()`

**Changements:**
- Remplace `livres` par `documents`
- Cherche dans `documents` au lieu de `livres`

---

## 🧪 Test Niveau 6

```java
public class TestNiveau6 {
    public static void main(String[] args) {
        Bibliotheque biblio = new Bibliotheque("Le Nexus Polymorphe");
        
        // Ajoute 2 livres, 2 magazines, 2 DVDs
        
        
        // Affiche le catalogue complet
        
        
        // Affiche seulement les livres
        
        
        // Affiche seulement les magazines
        
        
        // Affiche les statistiques
        
    }
}
```

---

# 🏛️ NIVEAU 7 - LE TEMPLE ABSTRAIT

<div style="background: linear-gradient(135deg, #667eea, #764ba2); color: white; padding: 20px; border-radius: 15px; margin: 20px 0;">

### 📜 Histoire

*"Crée des règles STRICTES que tous les documents DOIVENT suivre avec classes abstraites et interfaces !"*

</div>

## 💎 Points: 30 pts | ⏱️ Temps: 3-4 heures

---

## 🎯 Mission 7.1 : Créer `DocumentAbstrait`

**Fichier:** `DocumentAbstrait.java`

**Déclaration:** `public abstract class DocumentAbstrait`

### Attributs privés:
- `String titre`
- `int annee`
- `boolean estEmprunte`

### Constructeur (normal):
Comme `Document` du niveau 5

### Méthodes ABSTRAITES à déclarer:
```java
public abstract void afficher();
public abstract int getDureeEmprunt();
public abstract String getIcone();
```

<details>
<summary>💡 Syntaxe méthode abstraite</summary>

```java
public abstract Type nomMethode(parametres);
// Pas de { }, juste un ;
```
</details>

### Méthodes CONCRÈTES:

#### `emprunter()`:
Comme avant mais utilise `getDureeEmprunt()`:
```java
System.out.println("Emprunté pour " + getDureeEmprunt() + " jours !");
```

#### `retourner()`:
Comme avant

#### Getters:
Comme avant

---

## 🎯 Mission 7.2 : Créer l'interface `Evaluable`

**Fichier:** `Evaluable.java`

**Déclaration:** `public interface Evaluable`

**Méthodes à déclarer:**
```java
void attribuerNote(int note);
int getNote();
void afficherEvaluation();
```

<details>
<summary>💡 Syntaxe interface</summary>

```java
public interface NomInterface {
    void methode1();
    Type methode2();
    // Toutes les méthodes sont automatiquement public abstract
}
```
</details>

---

## 🎯 Mission 7.3 : Créer `LivreComplet`

**Fichier:** `LivreComplet.java`

**Déclaration:** `public class LivreComplet extends DocumentAbstrait implements Evaluable`

### Attributs privés:
- `String auteur`
- `int nombrePages`
- `int note`

### Constructeur:
```java
public LivreComplet(String titre, String auteur, int annee, int nombrePages) {
    super(titre, annee);
    this.auteur = auteur;
    this.nombrePages = nombrePages;
    this.note = 0;
}
```

### Implémenter méthodes abstraites:

#### `getDureeEmprunt()`:
```java
@Override
public int getDureeEmprunt() {
    return 21;  // 3 semaines
}
```

#### `getIcone()`:
```java
@Override
public String getIcone() {
    return "📚";
}
```

#### `afficher()`:
```java
@Override
public void afficher() {
    System.out.println("=== LIVRE ===");
    System.out.println("Titre: " + getTitre());
    System.out.println("Auteur: " + auteur);
    // etc.
}
```

### Implémenter interface Evaluable:

#### `attribuerNote(int note)`:
```
SI note entre 0 et 5:
    this.note = note
    Afficher "Note de [note]/5 attribuée"
SINON:
    Afficher "Note invalide !"
```

#### `getNote()`:
Retourne `note`

#### `afficherEvaluation()`:
```
Afficher "Évaluation: "
Pour i de 0 à note:
    Afficher "★"
Pour i de note à 5:
    Afficher "☆"
Afficher " ([note]/5)"
```

---

## 🎯 Mission 7.4 : Créer `MagazineComplet`

**Fichier:** `MagazineComplet.java`

**Déclaration:** `public class MagazineComplet extends DocumentAbstrait`

### Attributs:
- `int numero`
- `String mois`

### Implémenter:
- `getDureeEmprunt()` → retourne 7
- `getIcone()` → retourne "📰"
- `afficher()` → affiche infos magazine

---

## 🎯 Mission 7.5 : Créer `DVDComplet`

**Fichier:** `DVDComplet.java`

**Déclaration:** `public class DVDComplet extends DocumentAbstrait implements Evaluable`

### Attributs:
- `String realisateur`
- `int dureeMinutes`
- `int note`

### Implémenter:
- Toutes les méthodes abstraites
- Interface Evaluable
- `getDureeEmprunt()` → retourne 14

---

## 🧪 Test Niveau 7

```java
public class TestNiveau7 {
    public static void main(String[] args) {
        // Essaie de créer DocumentAbstrait directement
        // DocumentAbstrait doc = new DocumentAbstrait(...); // ERREUR!
        
        // Crée LivreComplet
        LivreComplet livre = new LivreComplet("Dune", "Herbert", 1965, 688);
        
        // Affiche
        
        // Emprunte (vois le message avec durée!)
        
        // Attribue note
        
        // Affiche évaluation
        
        
        // Crée MagazineComplet (pas Evaluable!)
        
        
        // Crée DVDComplet (Evaluable!)
        
    }
}
```

---

# 👑 NIVEAU 8 - LE BOSS FINAL (PROJET COMPLET)

<div style="background: linear-gradient(135deg, #667eea, #764ba2); color: white; padding: 20px; border-radius: 15px; margin: 20px 0;">

### 📜 Histoire

*"C'est l'heure de l'épreuve ultime ! Crée un système COMPLET de gestion avec TOUTES les fonctionnalités !"*

</div>

## 💎 Points: 50 pts | ⏱️ Temps: 8-12 heures

---

## 🎯 Fonctionnalités à implémenter

### Partie A : Classe `Membre` (10 pts)

**Fichier:** `Membre.java`

**Attributs:**
- `String nom, prenom`
- `String numeroMembre`
- `ArrayList<DocumentAbstrait> documentsEmpruntes`
- `double fraisAccumules`

**Méthodes à créer:**
- `ajouterEmprunt(DocumentAbstrait doc)` - limite 5 emprunts
- `retirerEmprunt(DocumentAbstrait doc)`
- `ajouterFrais(double montant)`
- `payerFrais(double montant)`
- `afficherEmprunts()`

---

### Partie B : Menu Interactif (15 pts)

**Fichier:** `MenuPrincipal.java`

Crée un menu avec `Scanner` qui permet:
```
═══ MENU PRINCIPAL ═══
1. Ajouter un document
2. Afficher catalogue
3. Emprunter document
4. Retourner document
5. Inscrire membre
6. Rechercher
7. Statistiques
0. Quitter
```

**Instructions détaillées:**
- Utilise `Scanner scanner = new Scanner(System.in);`
- Boucle `while` qui continue jusqu'à choix 0
- `switch/case` pour chaque option
- Gestion d'erreurs avec `try/catch`

---

### Partie C : Système de Recherche (10 pts)

**Méthodes à ajouter dans Bibliotheque:**

#### `rechercherParMotCle(String motCle)`:
Cherche dans titre ET auteur (pour les livres)

#### `afficherDocumentsParAnnee(int anneeDebut, int anneeFin)`:
Filtre par plage d'années

---

### Partie D : Statistiques Avancées (10 pts)

**Méthodes:**
- `documentsLesPlusEmpruntes()` - top 5
- `membresLesPlusActifs()` - top 3
- `calculerRevenus()` - total des frais

---

### Partie E : Sauvegarde/Chargement (5 pts - BONUS)

Avec `PrintWriter` et `Scanner`:
- Sauvegarde les documents dans fichier texte
- Recharge au démarrage

---

## 📝 Grille d'Évaluation Finale

### Concepts POO (40 pts):
- [ ] Classes bien conçues (5 pts)
- [ ] Encapsulation (5 pts)
- [ ] Héritage (5 pts)
- [ ] Polymorphisme (5 pts)
- [ ] Classes abstraites (5 pts)
- [ ] Interfaces (5 pts)
- [ ] ArrayList (5 pts)
- [ ] Organisation (5 pts)

### Fonctionnalités (35 pts):
- [ ] Gestion documents (10 pts)
- [ ] Gestion membres (10 pts)
- [ ] Menu interactif (10 pts)
- [ ] Recherche (5 pts)

### Qualité (25 pts):
- [ ] Code commenté (10 pts)
- [ ] Nommage (5 pts)
- [ ] Gestion erreurs (5 pts)
- [ ] Tests (5 pts)

---

## 🎊 FÉLICITATIONS !

Si tu es arrivé ici, tu es maintenant un **MAÎTRE DE LA POO** ! 🎉👑

Tu maîtrises:
✅ Classes et objets
✅ Encapsulation
✅ Tableaux et ArrayList
✅ Héritage
✅ Polymorphisme
✅ Classes abstraites
✅ Interfaces
✅ Composition

**Tu es prêt pour n'importe quel projet Java ! 🚀**

---

# 🛡️ NIVEAU 9 — LES GARDIENS DE L'ACCÈS
 
### 📜 Histoire
 
*"La bibliothèque légendaire grandit ! Des dizaines de classes s'accumulent dans un seul dossier. Le chaos règne… Le Grand Architecte t'ordonne d'organiser le royaume en ZONES (packages) et de poster des GARDIENS (modificateurs d'accès) à chaque porte !"*
 
## 💎 Points : 20 pts | ⏱️ Temps estimé : 2 heures
 
---
 
## 🎯 Mission 9.1 : Créer la structure de packages
 
Réorganise tous tes fichiers Java dans la structure suivante :
 
```
com/bibliotheque/
├── model/       → Document, Livre, Magazine, DVD, LivreComplet…
├── service/     → Bibliotheque, DocumentUtils
├── exception/   → Tes futures exceptions personnalisées (niveau 12)
└── main/        → TestNiveau9, MenuPrincipal
```
 
**Étape 1 :** Crée les dossiers correspondants dans ton projet.
 
**Étape 2 :** Ajoute la déclaration de package en **première ligne** de chaque fichier.
 
Exemples :
```java
package com.bibliotheque.model;   // dans LivreComplet.java
package com.bibliotheque.service; // dans Bibliotheque.java
package com.bibliotheque.main;    // dans TestNiveau9.java
```
 
**Étape 3 :** Ajoute les imports nécessaires dans les classes qui utilisent d'autres packages.
 
```java
package com.bibliotheque.service;
 
import com.bibliotheque.model.DocumentAbstrait;
import com.bibliotheque.model.LivreComplet;
```
 
**À faire :**
1. Déplace chaque fichier dans le bon dossier
2. Ajoute la déclaration `package` en haut
3. Ajoute les `import` manquants
4. Vérifie que tout compile encore
---
 
## 🎯 Mission 9.2 : Différences entre `public`, `private` et *default*
 
### 🎓 Concept : Les modificateurs de visibilité
 
| Modificateur | Même classe | Même package | Autre package |
|---|---|---|---|
| `public` | ✅ | ✅ | ✅ |
| *(default)* | ✅ | ✅ | ❌ |
| `private` | ✅ | ❌ | ❌ |
 
Le modificateur **default** (aucun mot-clé) signifie que la classe ou méthode est visible uniquement dans le **même package**.
 
**À faire :** Crée `FormatHelper.java` dans `com.bibliotheque.service` **sans** le mot-clé `public` :
 
```java
package com.bibliotheque.service;
 
// Pas de 'public' = accès default
class FormatHelper {
 
    static String encadrer(String texte) {
        return "╔══════════════════════╗\n║ " + texte + "\n╚══════════════════════╝";
    }
 
    static String statut(boolean estEmprunte) {
        return estEmprunte ? "🔴 EMPRUNTÉ" : "🟢 DISPONIBLE";
    }
}
```
 
**À tester :**
1. Utilise `FormatHelper.encadrer(...)` dans `Bibliotheque.java` (même package) → doit fonctionner ✅
2. Tente d'utiliser `FormatHelper` depuis `com.bibliotheque.main` → observe l'erreur de compilation ❌
3. Afficher : `"⚠️ FormatHelper est invisible hors du package service !"`
---
 
## 🎯 Mission 9.3 : Classe avec méthodes `public` et `private`
 
Dans `DocumentUtils.java` (package `com.bibliotheque.service`) :
 
**À implémenter :**
 
| Méthode | Modificateur | Description |
|---|---|---|
| `formaterStatut(DocumentAbstrait doc)` | `public static` | Retourne une String lisible avec ID + titre + statut |
| `formaterDuree(int minutes)` | `public static` | Convertit des minutes en format `"2h05"` |
| `validerAnnee(int annee)` | `private static` | Vérifie que l'année est entre 1000 et 2024 |
| `estAncien(int annee)` | `public static` | Retourne `true` si le document a plus de 50 ans |
 
**Instructions pour `formaterStatut` :**
- Retourner une chaîne au format : `"[DOC-0001] Dune — 🟢 DISPONIBLE"`
- Utiliser `doc.getIdentifiant()`, `doc.getTitre()`, `doc.isEstEmprunte()`
**Instructions pour `formaterDuree` :**
- `heures = minutes / 60`
- `mins = minutes % 60`
- Retourner au format `"2h05"` (utilise `String.format("%02d", mins)` pour avoir deux chiffres)
**Instructions pour `validerAnnee` :**
- `private` car c'est un outil interne — on ne veut pas l'exposer à l'extérieur
- Retourne `true` si `annee >= 1000 && annee <= 2024`
**Important :** Le constructeur de `DocumentUtils` doit être `private` pour empêcher de créer des instances d'une classe qui ne contient que des méthodes statiques.
 
---
 
## 🎯 Mission 9.4 : Import statique pour les constantes
 
Crée `BiblioConstantes.java` dans `com.bibliotheque.service` :
 
**À déclarer :**
 
| Constante | Type | Valeur |
|---|---|---|
| `DUREE_EMPRUNT_LIVRE` | `int` | `21` |
| `DUREE_EMPRUNT_MAGAZINE` | `int` | `7` |
| `DUREE_EMPRUNT_DVD` | `int` | `14` |
| `MAX_EMPRUNTS_MEMBRE` | `int` | `5` |
| `SEPARATEUR` | `String` | `"════════════════════════"` |
 
Toutes doivent être `public static final`.
 
Dans `TestNiveau9.java`, utilise l'import statique pour éviter d'écrire `BiblioConstantes.` à chaque fois :
 
```java
import static com.bibliotheque.service.BiblioConstantes.*;
 
// Ensuite, tu peux écrire directement :
System.out.println("Durée emprunt livre : " + DUREE_EMPRUNT_LIVRE + " jours");
```
 
---
 
## 🧪 Test Niveau 9
 
Crée `TestNiveau9.java` dans `com.bibliotheque.main` et complète :
 
```java
package com.bibliotheque.main;
 
import com.bibliotheque.model.*;
import com.bibliotheque.service.*;
import static com.bibliotheque.service.BiblioConstantes.*;
 
public class TestNiveau9 {
    public static void main(String[] args) {
        // Crée une bibliothèque et 3 documents (au moins 1 livre, 1 magazine, 1 DVD)
 
        // Affiche les durées d'emprunt avec les constantes importées statiquement
 
        // Utilise DocumentUtils.formaterStatut() sur chaque document
 
        // Utilise DocumentUtils.formaterDuree(136) et affiche le résultat
 
        // Tente d'utiliser FormatHelper depuis ici — documente l'erreur dans un commentaire
 
        System.out.println("\n🏆 NIVEAU 9 TERMINÉ !");
    }
}
```
 
### ✅ Checklist
 
- [ ] Structure de packages créée et compilable
- [ ] `FormatHelper` en accès default — erreur confirmée depuis `main`
- [ ] `DocumentUtils` avec méthodes `public` et `private`
- [ ] `BiblioConstantes` complète
- [ ] Import statique fonctionnel dans `TestNiveau9`
---
 
## 🏆 Défis Bonus (+5 pts chacun)
 
### Défi 9.A : Organiser les exceptions
Crée le package `com.bibliotheque.exception` et prépare-le pour le niveau 12 (fichier vide avec juste la déclaration de package suffit).
 
### Défi 9.B : Méthodes `private` supplémentaires
Dans `Bibliotheque.java`, identifie au moins 2 méthodes qui devraient être `private` (usage interne seulement) et change leur modificateur. Documente ton choix dans un commentaire.
 
### Défi 9.C : Constante de version
Ajoute `public static final String VERSION = "1.0.0"` à `BiblioConstantes` et affiche-la au démarrage de `Bibliotheque`.
 
---
 
---
 
# ⚡ NIVEAU 10 — LE GRIMOIRE STATIQUE
 
### 📜 Histoire
 
*"Certaines vérités de la bibliothèque sont IMMUABLES et UNIVERSELLES. Le nombre total de documents créés depuis le début des temps, la durée maximale d'un emprunt, l'identifiant unique de chaque livre… Ces données appartiennent à la CLASSE entière, pas à une seule instance. Maîtrise le pouvoir du `static` et du `final` !"*
 
## 💎 Points : 25 pts | ⏱️ Temps estimé : 2 heures
 
---
 
## 🎯 Mission 10.1 : Variable statique — compteur partagé
 
### 🎓 Concept : `static`
 
Une variable `static` appartient à la **classe**, pas à un objet en particulier. Toutes les instances la partagent.
 
```java
public class Exemple {
    private static int compteur = 0;  // Partagé entre tous les objets
 
    public Exemple() {
        compteur++;  // Incrémenté à chaque création d'objet
    }
 
    public static int getCompteur() {  // Appelable sans objet
        return compteur;
    }
}
 
// Utilisation
new Exemple();
new Exemple();
System.out.println(Exemple.getCompteur());  // 2 — appel sur la CLASSE
```
 
**À faire dans `DocumentAbstrait.java` :**
 
1. Ajoute une variable `private static int nombreDocumentsCrees = 0`
2. Ajoute une variable `private static int prochainId = 1`
3. Dans le constructeur :
   - Assigne `this.id = prochainId++` (ID unique et croissant)
   - Incrémente `nombreDocumentsCrees`
   - Afficher : `"📄 Document #[id] créé ! Total : [nombreDocumentsCrees]"`
4. Ajoute la méthode `public static int getNombreDocumentsCrees()`
5. Ajoute la méthode `public int getId()`
---
 
## 🎯 Mission 10.2 : Attribut `final` — immuable après initialisation
 
### 🎓 Concept : `final` sur un attribut
 
Un attribut `final` ne peut être assigné **qu'une seule fois** (dans le constructeur). Il devient immuable ensuite.
 
```java
public class Exemple {
    private final int id;  // Doit être initialisé dans le constructeur
 
    public Exemple(int id) {
        this.id = id;    // ✅ OK — dans le constructeur
        // this.id = 5;  // ❌ ERREUR — déjà assigné
    }
}
```
 
**À faire :**
 
Dans `DocumentAbstrait`, déclare l'attribut `id` avec `private final int id`. Observe que le compilateur t'oblige à l'initialiser dans le constructeur.
 
**Vérifie :** Essaie d'assigner `this.id = 99` une deuxième fois quelque part → le compilateur doit refuser.
 
---
 
## 🎯 Mission 10.3 : Méthode `final` — non-redéfinissable
 
### 🎓 Concept : `final` sur une méthode
 
Une méthode `final` **ne peut pas être redéfinie** (`@Override`) dans une sous-classe.
 
```java
public class Parent {
    public final String getType() {
        return "Je suis un Parent";
    }
}
 
public class Enfant extends Parent {
    // @Override
    // public String getType() { ... }  // ❌ ERREUR DE COMPILATION
}
```
 
**À faire dans `DocumentAbstrait` :**
 
Ajoute la méthode suivante :
 
```java
public final String getIdentifiant() {
    return "DOC-" + String.format("%04d", id);
}
```
 
**Vérifie :** Tente de faire `@Override` de `getIdentifiant()` dans `LivreComplet` → le compilateur doit refuser avec un message clair.
 
---
 
## 🎯 Mission 10.4 : Classe `final` — non-héritable
 
### 🎓 Concept : `final` sur une classe
 
Une classe `final` ne peut **pas être étendue** avec `extends`.
 
```java
public final class MaClasse { }
 
// public class SousClasse extends MaClasse { }  // ❌ ERREUR
```
 
**À faire :**
 
1. Ajoute `final` à la déclaration de `DocumentUtils`
2. Tente d'écrire une classe `MesUtils extends DocumentUtils` → documente l'erreur dans un commentaire
3. Note : `String`, `Integer`, `Math` sont des exemples de classes `final` dans Java lui-même
---
 
## 🎯 Mission 10.5 : Méthode statique utilitaire
 
Dans `DocumentUtils`, ajoute la méthode statique suivante :
 
**Signature :** `public static String resumé(DocumentAbstrait doc)`
 
**Instructions :**
- Retourner une chaîne sur une ligne avec : identifiant, titre, année, statut
- Format : `"[DOC-0001] Dune (1965) — 🟢 DISPONIBLE"`
- Utilise `getIdentifiant()`, `getTitre()`, `getAnnee()`, `isEstEmprunte()`
- Note : cette méthode est **statique** — on l'appelle sans créer d'objet `DocumentUtils`
---
 
## 🧪 Test Niveau 10
 
Crée `TestNiveau10.java` et complète :
 
```java
public class TestNiveau10 {
    public static void main(String[] args) {
        System.out.println("=== GRIMOIRE STATIQUE ===\n");
 
        // Crée 3 documents de types différents
        // Observe les messages de création avec le compteur
 
        // Appel statique sur la CLASSE (pas sur un objet)
        System.out.println("Total créés : " + DocumentAbstrait.getNombreDocumentsCrees());
 
        // Affiche les identifiants uniques (DOC-0001, DOC-0002…)
 
        // Appel statique de DocumentUtils.resumé() sur chaque document
 
        // Démontre que id est immuable (essaie de le changer — comment ?)
 
        System.out.println("\n🏆 NIVEAU 10 TERMINÉ !");
    }
}
```
 
### ✅ Checklist
 
- [ ] `nombreDocumentsCrees` s'incrémente à chaque `new`
- [ ] `id` est `final` — assigné une seule fois dans le constructeur
- [ ] `getIdentifiant()` est `final` — impossible à `@Override`
- [ ] `DocumentUtils` est `final` — impossible d'en hériter
- [ ] `getNombreDocumentsCrees()` s'appelle sur la classe, pas sur un objet
---
 
## 🏆 Défis Bonus (+5 pts chacun)
 
### Défi 10.A : Bloc statique
Ajoute un bloc `static { }` dans `BiblioConstantes` qui affiche un message `"⚡ Constantes chargées !"` au chargement de la classe. Observe quand ce message apparaît.
 
### Défi 10.B : Variable statique dans `Bibliotheque`
Ajoute un compteur `private static int nombreBibliothequesCrees` dans `Bibliotheque` et affiche-le.
 
### Défi 10.C : `final` sur un paramètre
Dans une méthode de ton choix, ajoute `final` devant un paramètre et tente de le modifier dans le corps de la méthode. Documente ce que le compilateur dit.
 
---
 
---
 
# 📜 NIVEAU 11 — LES PARCHEMINS SACRÉS
 
### 📜 Histoire
 
*"Des livres de Fantasy, des DVDs de Science-Fiction, des magazines de Cuisine… Comment distinguer les genres sans risquer des fautes de frappe ? Le Sage Codeur révèle les PARCHEMINS SACRÉS : les énumérations ! Fini les `String` fragiles — place aux types sûrs et infaillibles !"*
 
## 💎 Points : 20 pts | ⏱️ Temps estimé : 2 heures
 
---
 
## 🎯 Mission 11.1 : Enum simple — `JourSemaine`
 
### 🎓 Concept : L'énumération (enum)
 
Un `enum` est un type spécial qui représente un ensemble **fixe et limité** de constantes nommées.
 
```java
// Déclaration
public enum Saison {
    PRINTEMPS, ETE, AUTOMNE, HIVER
}
 
// Utilisation
Saison s = Saison.ETE;
 
if (s == Saison.ETE) {
    System.out.println("Il fait chaud !");
}
 
// Parcourir toutes les valeurs
for (Saison saison : Saison.values()) {
    System.out.println(saison);
}
 
// Obtenir à partir d'une String
Saison s2 = Saison.valueOf("HIVER");
 
// Position (commence à 0)
int pos = Saison.AUTOMNE.ordinal();  // 2
 
// Nom en String
String nom = Saison.ETE.name();  // "ETE"
```
 
**À faire :** Crée `JourSemaine.java` dans `com.bibliotheque.model` avec les 7 jours de la semaine (LUNDI, MARDI, MERCREDI, JEUDI, VENDREDI, SAMEDI, DIMANCHE).
 
**À tester dans `TestNiveau11` :**
1. Crée une variable `JourSemaine jour = JourSemaine.SAMEDI`
2. Affiche si c'est la fin de semaine avec un `if`
3. Parcourt tous les jours avec `values()` et affiche leur position (`ordinal()`)
4. Convertis la String `"LUNDI"` en enum avec `valueOf()`
---
 
## 🎯 Mission 11.2 : Enum simple — `StatutDocument`
 
**À faire :** Crée `StatutDocument.java` avec les valeurs : `DISPONIBLE`, `EMPRUNTE`, `RESERVE`, `PERDU`.
 
**À utiliser :**
- Dans `DocumentAbstrait`, remplace le booléen `estEmprunte` par un attribut `private StatutDocument statut` (initialisé à `DISPONIBLE`)
- Adapte les méthodes `emprunter()` et `retourner()` pour utiliser cet enum au lieu du booléen
- La méthode `isEstEmprunte()` retourne `true` si `statut == StatutDocument.EMPRUNTE`
---
 
## 🎯 Mission 11.3 : Enum avec attributs — `GenreDocument`
 
### 🎓 Concept : Enum avec attributs et méthodes
 
Un enum peut avoir des attributs et des méthodes, comme une classe normale. Le constructeur est toujours `private` (implicitement).
 
```java
public enum PlaneteNaine {
    PLUTON(2377, "Au-delà de Neptune"),
    ERIS(2326, "Très lointaine"),
    CERES(940, "Ceinture d'astéroïdes");
 
    private final int diametrKm;
    private final String description;
 
    PlaneteNaine(int diametrKm, String description) {
        this.diametrKm = diametrKm;
        this.description = description;
    }
 
    public int getDiametre()       { return diametrKm; }
    public String getDescription() { return description; }
}
 
// Utilisation
System.out.println(PlaneteNaine.PLUTON.getDiametre());    // 2377
System.out.println(PlaneteNaine.PLUTON.getDescription()); // Au-delà de Neptune
```
 
**À faire :** Crée `GenreDocument.java` avec au moins 6 genres. Chaque valeur doit avoir :
- Un attribut `String description` (ex : `"Science-Fiction"`)
- Un attribut `String icone` (ex : `"🚀"`)
- Un constructeur qui initialise les deux
- Les getters `getDescription()` et `getIcone()`
- Un `@Override` de `toString()` qui retourne `icone + " " + description`
**Genres suggérés :** ROMAN, SF, FANTASY, BIOGRAPHIE, HISTOIRE, CUISINE, SCIENCE, ACTUALITES, DOCUMENTAIRE, AUTRE
 
---
 
## 🎯 Mission 11.4 : Enum avec attributs — `NiveauLecture`
 
**À faire :** Crée `NiveauLecture.java` avec 4 niveaux : ENFANT, JEUNESSE, ADULTE, EXPERT.
 
Chaque valeur doit avoir :
- Un attribut `int niveau` (valeurs : 1, 2, 3, 4)
- Un attribut `String description` (ex : `"Enfant (0-10 ans)"`)
- Un getter `getNiveau()`
- Une méthode `public boolean estAccessiblePour(NiveauLecture lecteur)` qui retourne `true` si `lecteur.getNiveau() >= this.getNiveau()`
---
 
## 🎯 Mission 11.5 : Intégrer les enums dans `LivreComplet`
 
**Modifications à apporter dans `LivreComplet` :**
 
1. Ajoute deux nouveaux attributs privés :
   - `private GenreDocument genre`
   - `private NiveauLecture niveauLecture`
2. Modifie le constructeur pour accepter ces deux nouveaux paramètres (en plus des existants)
3. Ajoute les getters correspondants
4. Modifie `afficher()` pour afficher le genre et le niveau de lecture en utilisant `toString()` de chaque enum
---
 
## 🎯 Mission 11.6 : Méthode `afficherParGenre()` dans `Bibliotheque`
 
**À faire :** Ajoute dans `Bibliotheque` une méthode `public void afficherParGenre(GenreDocument genre)`.
 
**Instructions :**
1. Affiche un titre avec l'icône et la description du genre
2. Parcours tous les documents avec une boucle `for`
3. Pour chaque document : vérifie avec `instanceof` si c'est un `LivreComplet`, puis caste-le et compare son genre
4. Affiche le titre et l'auteur des documents correspondants
5. Si aucun document trouvé : affiche `"😢 Aucun document de ce genre."`
---
 
## 🧪 Test Niveau 11
 
Crée `TestNiveau11.java` et complète :
 
```java
public class TestNiveau11 {
    public static void main(String[] args) {
        // === Test enum simple JourSemaine ===
        // Crée une variable JourSemaine et teste si c'est la fin de semaine
        // Affiche tous les jours avec leur position (ordinal)
        // Convertis "VENDREDI" en enum avec valueOf()
 
        // === Test StatutDocument ===
        // Crée un livre, affiche son statut initial
        // Emprunte-le, affiche le nouveau statut
        // Retourne-le, affiche le statut final
 
        // === Test GenreDocument et NiveauLecture ===
        // Affiche tous les genres disponibles avec leur icône
 
        // Crée 3 livres de genres différents et ajoute-les à une bibliothèque
 
        // Filtre et affiche les livres de genre SF
 
        // Teste estAccessiblePour() avec différents niveaux
 
        System.out.println("\n🏆 NIVEAU 11 TERMINÉ !");
    }
}
```
 
### ✅ Checklist
 
- [ ] `JourSemaine` simple : `values()`, `ordinal()`, `valueOf()` testés
- [ ] `StatutDocument` remplace le booléen `estEmprunte` dans `DocumentAbstrait`
- [ ] `GenreDocument` avec description et icône
- [ ] `NiveauLecture` avec méthode `estAccessiblePour()`
- [ ] `LivreComplet` utilise les deux enums
- [ ] `afficherParGenre()` fonctionne correctement
---
 
## 🏆 Défis Bonus (+5 pts chacun)
 
### Défi 11.A : Enum `TypeDocument`
Crée `TypeDocument` (LIVRE, MAGAZINE, DVD) et ajoute un getter `getType()` dans `DocumentAbstrait`. Chaque sous-classe retourne son type. Utilise cet enum dans `afficherCatalogue()` au lieu de `instanceof`.
 
### Défi 11.B : Conversion String → Enum avec gestion d'erreur
Ajoute une méthode statique `GenreDocument.fromString(String s)` qui retourne le genre correspondant ou `AUTRE` si non trouvé (utilise un `try-catch` sur `valueOf()`).
 
### Défi 11.C : Enum dans le menu
Dans `MenuPrincipal`, affiche les genres disponibles via `GenreDocument.values()` et laisse l'utilisateur saisir un numéro pour filtrer.
 
---
 
---
 
# 🐉 NIVEAU 12 — LE DRAGON DES EXCEPTIONS
 
### 📜 Histoire
 
*"Un utilisateur tente d'emprunter un livre déjà parti. Un document introuvable est recherché. La bibliothèque est pleine… Ces erreurs surgissent comme des dragons ! Le simple `System.out.println("Erreur")` ne suffit plus. Il faut des exceptions personnalisées, des gardiens try-catch et des ressources qui se ferment proprement !"*
 
## 💎 Points : 35 pts | ⏱️ Temps estimé : 3 heures
 
---
 
## 🎯 Mission 12.1 : Créer `DocumentDejaEmprunteException`
 
### 🎓 Concept : Exception personnalisée
 
Une exception personnalisée hérite de `Exception` (vérifiée) ou de `RuntimeException` (non vérifiée).
 
```java
public class MonException extends Exception {
    private String info;
 
    public MonException(String message, String info) {
        super(message);  // Passe le message à la classe parente
        this.info = info;
    }
 
    public String getInfo() { return info; }
}
 
// Lancer :
throw new MonException("Quelque chose s'est mal passé", "détail");
 
// Attraper :
try {
    // code qui peut lancer l'exception
} catch (MonException e) {
    System.out.println(e.getMessage());
    System.out.println(e.getInfo());
}
```
 
**À faire :** Crée `DocumentDejaEmprunteException.java` dans `com.bibliotheque.exception`.
 
**Instructions :**
- Hérite de `Exception`
- Attributs privés : `String titreDocument`, `String nomEmprunteur`
- Constructeur avec les deux paramètres : appelle `super(...)` avec un message clair du type `"'Dune' est déjà emprunté par : Alice"`
- Getters pour les deux attributs
---
 
## 🎯 Mission 12.2 : Créer `CapaciteDepasseeException`
 
**À faire :** Crée `CapaciteDepasseeException.java` dans `com.bibliotheque.exception`.
 
**Instructions :**
- Hérite de `Exception`
- Attributs : `int capaciteMax`, `int tentative`
- Le message doit indiquer la capacité max et le numéro de tentative
- Getters pour les deux attributs
---
 
## 🎯 Mission 12.3 : Créer `DocumentIntrouvableException`
 
### 🎓 Différence : `Exception` vs `RuntimeException`
 
- **`Exception`** (vérifiée) : le compilateur **oblige** à gérer ou déclarer l'exception avec `throws`
- **`RuntimeException`** (non vérifiée) : facultatif, souvent utilisée pour les erreurs de programmation
```java
// Vérifiée — le compilateur oblige à écrire throws ou try-catch
public class FichierIntrouvableException extends Exception { }
 
// Non vérifiée — facultatif
public class ArgumentInvalideException extends RuntimeException { }
```
 
**À faire :** Crée `DocumentIntrouvableException.java`.
 
**Instructions :**
- Hérite de `RuntimeException` (car c'est une erreur de programmation — on ne devrait pas chercher un document inexistant)
- Attribut : `String titre`
- Message du type : `"Document introuvable : 'Dune'"`
- Getter pour le titre
---
 
## 🎯 Mission 12.4 : Lancer les exceptions dans `Bibliotheque`
 
**Modifications à apporter :**
 
**Dans `emprunterDocument(String titre, String nomEmprunteur)` :**
1. Ajoute `throws DocumentDejaEmprunteException` dans la signature
2. Si le document est déjà emprunté : `throw new DocumentDejaEmprunteException(...)` au lieu d'un `println`
3. Si le document n'existe pas : `throw new DocumentIntrouvableException(...)` (RuntimeException — pas besoin de `throws`)
**Dans `ajouterDocument(DocumentAbstrait doc)` :**
1. Ajoute un paramètre optionnel de capacité maximale à `Bibliotheque` (ex: -1 = illimité)
2. Si la capacité est dépassée : `throw new CapaciteDepasseeException(...)`
3. Ajoute `throws CapaciteDepasseeException` dans la signature
---
 
## 🎯 Mission 12.5 : Gérer les exceptions avec try-catch-finally
 
### 🎓 Concept : try-catch-finally
 
```java
try {
    // Code qui peut lancer une exception
 
} catch (TypeException1 e) {
    // Gérer le type 1
 
} catch (TypeException2 e) {
    // Gérer le type 2
 
} finally {
    // S'exécute TOUJOURS — même si une exception est lancée
    // Utile pour le nettoyage (fermer une ressource, loguer, etc.)
}
```
 
**À faire :** Dans `MenuPrincipal.java`, pour le choix "Emprunter un document" :
 
**Instructions :**
1. Demande le titre et le nom de l'emprunteur avec `Scanner`
2. Dans un bloc `try`, appelle `biblio.emprunterDocument(titre, nom)`
3. Dans un `catch (DocumentDejaEmprunteException e)` : affiche le message + un conseil
4. Dans un `catch (DocumentIntrouvableException e)` : affiche le message
5. Dans un `catch (Exception e)` : attrape toute autre erreur inattendue
6. Dans le `finally` : affiche `"📋 Traitement terminé."` (s'affiche toujours)
---
 
## 🎯 Mission 12.6 : Try-with-resources pour la sauvegarde
 
### 🎓 Concept : try-with-resources
 
```java
// Sans try-with-resources (ancien style) : on doit fermer manuellement
PrintWriter writer = null;
try {
    writer = new PrintWriter("fichier.txt");
    writer.println("contenu");
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (writer != null) writer.close();  // Fermeture manuelle
}
 
// Avec try-with-resources (Java 7+) : fermeture automatique
try (PrintWriter writer = new PrintWriter("fichier.txt")) {
    writer.println("contenu");
} catch (IOException e) {
    e.printStackTrace();
}
// writer est automatiquement fermé — même en cas d'exception !
```
 
**À faire :** Crée `SauvegardeService.java` dans `com.bibliotheque.service`.
 
**Instructions pour `sauvegarder(ArrayList<DocumentAbstrait> docs, String chemin)` :**
1. Utilise `try (PrintWriter writer = new PrintWriter(new FileWriter(chemin)))`
2. Pour chaque document : écris une ligne avec `writer.println(...)` contenant l'identifiant, le titre et l'année séparés par `;`
3. Dans le `catch (IOException e)` : affiche un message d'erreur
4. Affiche un message de succès avec le nombre de documents sauvegardés
**Instructions pour `charger(String chemin)` :**
1. Utilise `try (BufferedReader reader = new BufferedReader(new FileReader(chemin)))`
2. Lis chaque ligne avec `reader.readLine()` dans une boucle `while`
3. Affiche chaque ligne avec un numéro de ligne
4. Dans le `catch (FileNotFoundException e)` : affiche `"Aucune sauvegarde trouvée"`
---
 
## 🧪 Test Niveau 12
 
Crée `TestNiveau12.java` et complète :
 
```java
public class TestNiveau12 {
    public static void main(String[] args) {
        Bibliotheque biblio = new Bibliotheque("Temple des Exceptions");
 
        // Ajoute un livre
 
        // Essaie d'emprunter un livre qui n'existe pas
        // → doit lancer DocumentIntrouvableException
 
        // Emprunte un livre qui existe (succès)
 
        // Essaie d'emprunter le même livre une 2e fois
        // → doit lancer DocumentDejaEmprunteException
        // → affiche e.getMessage() et e.getTitreDocument()
 
        // Teste le bloc finally (doit s'afficher même après l'exception)
 
        // Teste la sauvegarde avec try-with-resources
        // Sauvegarde, puis recharge
 
        System.out.println("\n🏆 NIVEAU 12 TERMINÉ !");
    }
}
```
 
### ✅ Checklist
 
- [ ] `DocumentDejaEmprunteException` avec attributs et message personnalisé
- [ ] `CapaciteDepasseeException` lancée correctement
- [ ] `DocumentIntrouvableException` hérite de `RuntimeException`
- [ ] `emprunterDocument()` déclare `throws DocumentDejaEmprunteException`
- [ ] `try-catch-finally` dans le menu avec tous les cas
- [ ] `try-with-resources` dans `SauvegardeService`
---
 
## 🏆 Défis Bonus (+5 pts chacun)
 
### Défi 12.A : Catch multiple
Dans un même bloc `catch`, attrape deux types d'exceptions avec la syntaxe `catch (TypeA | TypeB e)`. Montre un exemple dans le menu.
 
### Défi 12.B : Validation dans le setter
Dans le setter `setAnnee()` de `LivreComplet`, lance une `IllegalArgumentException` si l'année est invalide au lieu d'un simple `println`.
 
### Défi 12.C : Exception chaînée
Crée une `BiblioException` générique qui encapsule une autre exception avec `super(message, cause)`. Utilise-la pour envelopper une `IOException` dans `SauvegardeService`.
 
---
 
---
 
# 💎 NIVEAU 13 — LE TRÉSOR DES COLLECTIONS
 
### 📜 Histoire
 
*"La bibliothèque légendaire contient des milliers de documents ! Un simple ArrayList ne suffit plus pour tout gérer. Le Grand Bibliothécaire te confie les STRUCTURES DE DONNÉES AVANCÉES : HashMap pour retrouver en un clin d'œil, HashSet pour éliminer les doublons, et les arbres TreeSet et TreeMap pour garder l'ordre !"*
 
## 💎 Points : 35 pts | ⏱️ Temps estimé : 3 heures
 
---
 
## 🎯 Mission 13.1 : `HashMap` — l'index de la bibliothèque
 
### 🎓 Concept : HashMap
 
`HashMap` stocke des paires **clé → valeur**. Chaque clé est unique. L'accès par clé est très rapide.
 
```java
import java.util.HashMap;
 
HashMap<String, Integer> ages = new HashMap<>();
 
// Ajouter
ages.put("Alice", 25);
ages.put("Bob", 30);
 
// Lire
int age = ages.get("Alice");   // 25
ages.get("Inconnu");           // null si absent
 
// Vérifier
boolean existe = ages.containsKey("Bob");   // true
boolean a30 = ages.containsValue(30);       // true
 
// Modifier (même clé = écrase)
ages.put("Alice", 26);
 
// Supprimer
ages.remove("Bob");
 
// Taille
int taille = ages.size();  // 1
 
// Parcourir les clés
for (String nom : ages.keySet()) {
    System.out.println(nom + " → " + ages.get(nom));
}
 
// Parcourir clés et valeurs en même temps
for (java.util.Map.Entry<String, Integer> entree : ages.entrySet()) {
    System.out.println(entree.getKey() + " → " + entree.getValue());
}
```
 
**À faire :** Dans `DocumentRepository` (ou directement dans `Bibliotheque`), ajoute un index `HashMap<String, DocumentAbstrait>` où la clé est l'identifiant du document (ex : `"DOC-0001"`).
 
**Méthodes à implémenter :**
 
1. `ajouterAuIndex(DocumentAbstrait doc)` — ajoute `doc.getIdentifiant()` → `doc` dans le HashMap
   - Appelle cette méthode depuis `ajouterDocument()`
2. `public DocumentAbstrait chercherParId(String id)` — retourne `index.get(id)` (null si absent)
   - Affiche `"🔍 Recherche par ID : [id]"` puis `"✅ Trouvé !"` ou `"❌ Introuvable"`
3. `public void afficherIndex()` — affiche toutes les entrées du HashMap
---
 
## 🎯 Mission 13.2 : `HashSet` — auteurs uniques
 
### 🎓 Concept : HashSet
 
`HashSet` stocke des valeurs **sans doublons** et sans ordre garanti.
 
```java
import java.util.HashSet;
 
HashSet<String> fruits = new HashSet<>();
 
fruits.add("Pomme");
fruits.add("Banane");
fruits.add("Pomme");   // Ignoré — doublon !
 
System.out.println(fruits.size());        // 2
System.out.println(fruits.contains("Banane")); // true
 
fruits.remove("Banane");
 
for (String f : fruits) {
    System.out.println(f);  // Ordre non garanti
}
```
 
**À faire :** Ajoute dans `Bibliotheque` (ou `StatistiquesService`) la méthode `public HashSet<String> getAuteursUniques()`.
 
**Instructions :**
1. Crée un `HashSet<String>` vide
2. Parcours tous les documents avec une boucle `for`
3. Pour ceux qui sont des `LivreComplet` (vérifie avec `instanceof` et caste) : ajoute `getAuteur()` au HashSet
4. Retourne le HashSet (les doublons sont automatiquement éliminés !)
**Également :** Ajoute `public HashSet<String> getTitresUniques()` qui fait la même chose pour les titres (utile pour détecter les doublons de titres).
 
---
 
## 🎯 Mission 13.3 : `TreeSet` — titres triés automatiquement
 
### 🎓 Concept : TreeSet de types simples
 
`TreeSet` est comme `HashSet`, mais les éléments sont **triés automatiquement**. Fonctionne directement avec `String`, `Integer`, `Double`, etc.
 
```java
import java.util.TreeSet;
 
TreeSet<String> noms = new TreeSet<>();
 
noms.add("Charlie");
noms.add("Alice");
noms.add("Bob");
noms.add("Alice");  // Doublon — ignoré
 
System.out.println(noms);  // [Alice, Bob, Charlie] — trié !
 
String premier = noms.first();  // "Alice"
String dernier = noms.last();   // "Charlie"
 
for (String nom : noms) {
    System.out.println(nom);  // Toujours dans l'ordre alphabétique
}
```
 
**À faire :** Ajoute dans `Bibliotheque` la méthode `public TreeSet<String> getTitresTriesAlpha()`.
 
**Instructions :**
1. Crée un `TreeSet<String>` vide
2. Parcours tous les documents
3. Ajoute `doc.getTitre()` pour chaque document
4. Retourne le TreeSet — les titres sont automatiquement triés !
5. Affiche le premier et le dernier titre avec `first()` et `last()`
**Également :** Ajoute `public TreeSet<Integer> getAnneesDistinctes()` qui collecte toutes les années de publication, sans doublons et triées.
 
---
 
## 🎯 Mission 13.4 : `TreeMap` — statistiques triées
 
### 🎓 Concept : TreeMap de types simples
 
`TreeMap` est comme `HashMap`, mais les **clés sont triées**. Avec des clés `String` ou `Integer`, le tri est automatique.
 
```java
import java.util.TreeMap;
 
TreeMap<String, Integer> scores = new TreeMap<>();
 
scores.put("Charlie", 85);
scores.put("Alice", 92);
scores.put("Bob", 78);
 
System.out.println(scores);
// {Alice=92, Bob=78, Charlie=85} — trié par clé alphabétique !
 
String premierNom = scores.firstKey();  // "Alice"
String dernierNom = scores.lastKey();   // "Charlie"
```
 
**À faire :** Ajoute la méthode `public TreeMap<String, Integer> getNombreDocumentsParAnnee()`.
 
**Instructions :**
1. Crée un `TreeMap<String, Integer>` — la clé sera l'année sous forme de String, la valeur le nombre de documents
2. Parcours tous les documents
3. Pour chaque document, crée la clé `String anneeStr = String.valueOf(doc.getAnnee())`
4. Si la clé existe déjà : incrémente la valeur avec `map.get(anneeStr) + 1`
5. Si elle n'existe pas : mets la valeur à 1 avec `map.put(anneeStr, 1)`
6. Retourne la TreeMap — les années sont automatiquement triées !
> **Note :** On utilise `String` comme clé (et non `int`) pour éviter de devoir créer un `Comparator`. Avec `String`, le tri se fait alphabétiquement, ce qui fonctionne bien pour des années à 4 chiffres.
 
---
 
## 🎯 Mission 13.5 : `getOrDefault()` — simplifier le comptage
 
### 🎓 Astuce : `getOrDefault`
 
Au lieu d'écrire :
```java
if (map.containsKey(cle)) {
    map.put(cle, map.get(cle) + 1);
} else {
    map.put(cle, 1);
}
```
 
Tu peux écrire :
```java
map.put(cle, map.getOrDefault(cle, 0) + 1);
```
 
`getOrDefault(cle, 0)` retourne la valeur associée à `cle`, ou `0` si la clé n'existe pas encore.
 
**À faire :** Refactorise la méthode `getNombreDocumentsParAnnee()` en utilisant `getOrDefault`.
 
**Ajoute également** la méthode `public HashMap<String, Integer> getNombreDocumentsParAuteur()` :
- Clé = nom de l'auteur (pour les `LivreComplet` seulement)
- Valeur = nombre de livres de cet auteur
- Utilise `getOrDefault`
---
 
## 🧪 Test Niveau 13
 
Crée `TestNiveau13.java` et complète :
 
```java
public class TestNiveau13 {
    public static void main(String[] args) {
        Bibliotheque biblio = new Bibliotheque("Trésor des Collections");
 
        // Ajoute au moins 6 documents (plusieurs auteurs, plusieurs années, dont des doublons d'auteur)
 
        // === Test HashMap ===
        // Cherche un document par son identifiant (ex: "DOC-0001")
        // Affiche l'index complet
 
        // === Test HashSet ===
        // Affiche tous les auteurs uniques (les doublons doivent disparaître)
        // Compare avec une ArrayList qui, elle, garderait les doublons
 
        // === Test TreeSet ===
        // Affiche les titres triés alphabétiquement
        // Affiche le premier et dernier titre (first() / last())
        // Affiche les années distinctes, triées
 
        // === Test TreeMap ===
        // Affiche le nombre de documents par année (clés triées)
        // Affiche le nombre de livres par auteur
 
        System.out.println("\n🏆 NIVEAU 13 TERMINÉ !");
    }
}
```
 
### ✅ Checklist
 
- [ ] `HashMap` : ajout automatique à l'index lors de `ajouterDocument()`
- [ ] `chercherParId()` retourne le bon document ou null
- [ ] `HashSet` : auteurs uniques sans doublons
- [ ] `TreeSet<String>` : titres triés alphabétiquement, `first()` et `last()` fonctionnent
- [ ] `TreeSet<Integer>` : années sans doublons et triées
- [ ] `TreeMap<String, Integer>` : années triées avec comptage
- [ ] `getOrDefault` utilisé pour simplifier le comptage
---
 
## 🏆 Défis Bonus (+5 pts chacun)
 
### Défi 13.A : Éliminer les doublons
Ajoute une méthode `verifierDoublonsTitres()` qui utilise un `HashSet` pour détecter si deux documents ont le même titre.
 
### Défi 13.B : Conversion entre collections
À partir du `HashSet` des auteurs uniques, crée un `TreeSet` pour les avoir triés. Affiche la différence avec `soutraction` : `HashSet` sans ordre, `TreeSet` avec ordre.
 
### Défi 13.C : Comptage par genre
Ajoute `HashMap<GenreDocument, Integer> getNombreDocumentsParGenre()` qui compte les livres par genre.
 
---
 
---
 
# 📅 NIVEAU 15 — L'HORLOGE DES PARCHEMINS
 
### 📜 Histoire
 
*"La bibliothèque existe depuis des siècles, mais elle n'a jamais su QUAND les livres ont été empruntés, ni COMBIEN DE JOURS il reste avant la date de retour ! Le Maître du Temps t'enseigne l'art de `java.time` : l'API moderne pour dompter les dates et les heures. Chaque emprunt aura désormais une date de début, une date de retour prévue, et des frais de retard calculés à la journée !"*
 
## 💎 Points : 30 pts | ⏱️ Temps estimé : 3 heures
 
---
 
## 🎓 Rappel des classes principales de `java.time`
 
| Classe | Utilisation | Exemple de création |
|---|---|---|
| `LocalDate` | Date sans heure | `LocalDate.now()` |
| `LocalDateTime` | Date + heure | `LocalDateTime.now()` |
| `Period` | Durée en jours/mois/années | `Period.between(date1, date2)` |
| `ChronoUnit` | Calculer des différences | `ChronoUnit.DAYS.between(d1, d2)` |
| `DateTimeFormatter` | Formater / parser | `DateTimeFormatter.ofPattern("dd/MM/yyyy")` |
 
**Import nécessaire :**
```java
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.Period;
import java.time.format.DateTimeFormatter;
import java.time.temporal.ChronoUnit;
```
 
---
 
## 🎯 Mission 15.1 : Créer la classe `Emprunt`
 
Crée `Emprunt.java` dans `com.bibliotheque.model`.
 
**Attributs privés à déclarer :**
 
| Attribut | Type | Description |
|---|---|---|
| `document` | `DocumentAbstrait` | Le document emprunté |
| `nomEmprunteur` | `String` | Nom du membre |
| `dateEmprunt` | `LocalDate` | Date à laquelle l'emprunt a été fait |
| `dateRetourPrevue` | `LocalDate` | Date limite de retour |
| `dateRetourEffective` | `LocalDate` | Date réelle de retour (null si pas encore rendu) |
 
**Constructeur :** `Emprunt(DocumentAbstrait document, String nomEmprunteur)`
- Initialise `document` et `nomEmprunteur`
- Assigne `dateEmprunt = LocalDate.now()`
- Calcule `dateRetourPrevue = dateEmprunt.plusDays(document.getDureeEmprunt())` — utilise la constante de durée selon le type
- `dateRetourEffective` reste `null`
- Affiche : `"📋 Emprunt enregistré : '[titre]' jusqu'au [dateRetourPrevue]"`
**Getters à créer :** pour tous les attributs.
 
---
 
## 🎯 Mission 15.2 : Méthode `retourner()`
 
Dans `Emprunt`, ajoute la méthode `public void retourner()`.
 
**Instructions :**
1. Assigne `dateRetourEffective = LocalDate.now()`
2. Calcule le nombre de jours de retard avec `ChronoUnit.DAYS.between(dateRetourPrevue, dateRetourEffective)`
3. Si `joursRetard > 0` :
   - Affiche : `"⚠️ Retour en retard de [joursRetard] jour(s) !"`
   - Calcule les frais : `joursRetard * BiblioConstantes.FRAIS_RETARD_LIVRE` (ou la constante selon le type de document)
   - Affiche : `"💰 Frais de retard : [frais] $"`
4. Sinon :
   - Affiche : `"✅ Retour dans les délais ! Bravo !"`
---
 
## 🎯 Mission 15.3 : Méthode `estEnRetard()`
 
Dans `Emprunt`, ajoute `public boolean estEnRetard()`.
 
**Instructions :**
- Si `dateRetourEffective != null` (déjà rendu) : retourne `false`
- Sinon : retourne `true` si `LocalDate.now().isAfter(dateRetourPrevue)`
---
 
## 🎯 Mission 15.4 : Méthode `afficher()` avec formatage de date
 
Dans `Emprunt`, ajoute `public void afficher()`.
 
**Instructions :**
1. Crée un `DateTimeFormatter` avec le pattern `"dd/MM/yyyy"`
2. Affiche le nom de l'emprunteur
3. Affiche le titre du document
4. Affiche la date d'emprunt **formatée** : `dateEmprunt.format(formatter)`
5. Affiche la date de retour prévue **formatée**
6. Si `dateRetourEffective != null` : affiche `"Rendu le : [date]"`
7. Sinon : affiche le statut — `"⚠️ EN RETARD"` ou `"🟢 Dans les délais"`
8. Si en retard : calcule et affiche le nombre de jours de retard avec `ChronoUnit.DAYS.between(...)`
---
 
## 🎯 Mission 15.5 : Gérer les emprunts dans `Bibliotheque`
 
**Modifications à apporter dans `Bibliotheque` :**
 
1. Ajoute un attribut `private ArrayList<Emprunt> emprunts = new ArrayList<>()`
2. Modifie `emprunterDocument(String titre, String nomEmprunteur)` :
   - Crée un `new Emprunt(doc, nomEmprunteur)`
   - Change le statut du document : `doc.setStatut(StatutDocument.EMPRUNTE)`
   - Ajoute l'emprunt à la liste `emprunts`
3. Modifie `retournerDocument(String titre)` :
   - Cherche l'emprunt actif pour ce titre dans la liste `emprunts`
   - Appelle `emprunt.retourner()`
   - Change le statut : `doc.setStatut(StatutDocument.DISPONIBLE)`
4. Ajoute `public void afficherTousLesEmprunts()` qui appelle `afficher()` sur chaque emprunt
---
 
## 🎯 Mission 15.6 : Méthode `afficherRetardataires()`
 
Dans `Bibliotheque`, ajoute `public void afficherRetardataires()`.
 
**Instructions :**
1. Affiche un titre `"⚠️ DOCUMENTS EN RETARD"`
2. Parcours la liste `emprunts`
3. Garde seulement ceux pour lesquels `emprunt.estEnRetard()` retourne `true`
4. Pour chaque retardataire : affiche le nom de l'emprunteur, le titre, et le nombre de jours de retard avec `ChronoUnit.DAYS.between(dateRetourPrevue, LocalDate.now())`
5. Si aucun retard : affiche `"✅ Aucun document en retard !"`
---
 
## 🎯 Mission 15.7 : Calculer la date de naissance d'un livre
 
Dans `LivreComplet`, ajoute `public String getAgeLisible()`.
 
**Instructions :**
1. Crée `LocalDate datePublication = LocalDate.of(getAnnee(), 1, 1)`
2. Calcule la période avec `Period.between(datePublication, LocalDate.now())`
3. Retourne une chaîne : `"X ans et Y mois"`
4. Si `age.getYears() > 50` : ajoute `" 📜 (Classique !)"`
---
 
## 🧪 Test Niveau 15
 
Crée `TestNiveau15.java` et complète :
 
```java
public class TestNiveau15 {
    public static void main(String[] args) {
        Bibliotheque biblio = new Bibliotheque("L'Horloge des Parchemins");
 
        // Crée 3 livres de différentes années
 
        // Emprunte 2 livres et affiche les dates de retour prévues
 
        // Affiche tous les emprunts avec les dates formatées (dd/MM/yyyy)
 
        // Retourne un livre dans les délais — affiche le message de succès
 
        // Simule un retard : crée un Emprunt avec une dateRetourPrevue dans le passé
        // (tu peux créer un constructeur de test qui accepte une date d'emprunt)
        // → affiche les frais de retard
 
        // Affiche les retardataires
 
        // Pour chaque livre, affiche son âge lisible avec getAgeLisible()
 
        System.out.println("\n🏆 NIVEAU 15 TERMINÉ !");
        System.out.println("⏱️ Tu maîtrises maintenant java.time !");
    }
}
```
 
### ✅ Checklist
 
- [ ] `Emprunt` avec `LocalDate` pour les 3 dates
- [ ] `dateRetourPrevue` calculée avec `plusDays()` selon la durée du document
- [ ] `retourner()` calcule les jours de retard avec `ChronoUnit.DAYS.between()`
- [ ] `estEnRetard()` utilise `LocalDate.now().isAfter(...)`
- [ ] `afficher()` formate les dates avec `DateTimeFormatter`
- [ ] `afficherRetardataires()` liste les emprunts en retard
- [ ] `getAgeLisible()` utilise `Period.between()`
---
 
## 🏆 Défis Bonus (+5 pts chacun)
 
### Défi 15.A : Formater en français
Dans `Emprunt.afficher()`, affiche la date de retour prévue au format long en français :
`"mercredi 05 mai 2026"` — utilise `DateTimeFormatter.ofPattern("EEEE dd MMMM yyyy", Locale.FRENCH)`.
 
### Défi 15.B : Recherche d'emprunts par période
Ajoute `public ArrayList<Emprunt> getEmpruntsByPeriode(LocalDate debut, LocalDate fin)` qui retourne les emprunts dont la `dateEmprunt` se situe dans la période. Utilise `isBefore()` et `isAfter()`.
 
### Défi 15.C : Statistiques temporelles
Ajoute `public void afficherStatistiquesMensuelles()` qui compte le nombre d'emprunts par mois grâce à `emprunt.getDateEmprunt().getMonthValue()` et un `HashMap<Integer, Integer>`.
 
---
 
---
 
## 🗺️ CARTE DES NOUVEAUX NIVEAUX
 
```
🛡️ NIVEAU 9          ⚡ NIVEAU 10         📜 NIVEAU 11
Gardiens de l'Accès   Grimoire Statique    Parchemins Sacrés
packages + accès      static + final       enum simples + composés
   [20 pts]              [25 pts]             [20 pts]
 
🐉 NIVEAU 12         💎 NIVEAU 13         📅 NIVEAU 15
Dragon des Exceptions Trésor des Collections Horloge des Parchemins
try-catch + customs   HashMap, HashSet,     java.time, LocalDate,
                      TreeSet, TreeMap      Period, DateTimeFormatter
   [35 pts]              [35 pts]             [30 pts]
 
    TOTAL NOUVEAUX NIVEAUX : +165 POINTS !
    TOTAL GÉNÉRAL (niveaux 1-8 + 9-13 + 15) : 365 POINTS POSSIBLES !
 
    🏗️ NIVEAU 14 (SOLID + Composition) → Prévu si le temps le permet
```
 
| Niveau | Thème | Notions principales | Points |
|--------|-------|---------------------|--------|
| 9 | Les Gardiens de l'Accès | Packages, `public`/`private`/default | 20 pts |
| 10 | Le Grimoire Statique | `static`, `final` (attribut, méthode, classe) | 25 pts |
| 11 | Les Parchemins Sacrés | `enum` simple et avec attributs | 20 pts |
| 12 | Le Dragon des Exceptions | Exceptions custom, try-catch-finally, try-with-resources | 35 pts |
| 13 | Le Trésor des Collections | `HashMap`, `HashSet`, `TreeSet`, `TreeMap` | 35 pts |
| 15 | L'Horloge des Parchemins | `LocalDate`, `Period`, `ChronoUnit`, `DateTimeFormatter` | 30 pts |
| **Total** | | | **165 pts** |

## 🎵 Playlist Complète

<div style="background: linear-gradient(135deg, #667eea, #764ba2); padding: 20px; border-radius: 10px; margin: 20px 0; color: white;">

### 🎧 Musiques d'Aventure

- 🎮 **Aventure Principale** - Pour coder
- ⚔️ **Combat Bugs** - Pour débugger
- 🏰 **Exploration** - Pour lire du code
- 🎊 **Victoire** - Pour les tests réussis
- ✨ **Magie POO** - Pour refactorer
- 🚀 **Boss Final** - Pour le projet final

</div>

---