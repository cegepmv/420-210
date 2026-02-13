+++
title = "BiblioAventure"
weight = 12
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