+++
title = "Date"
weight = 16
+++

# Les Dates en Java

## Introduction

En Java, il existe plusieurs façons de manipuler les dates et les heures. Depuis Java 8 (2014), le package **`java.time`** est la méthode **moderne et recommandée** pour travailler avec les dates.

Ce package offre des classes :
- **Immutables** (thread-safe)
- **Plus claires** et faciles à utiliser
- **Meilleures** pour les calculs de dates

> **Ce cours se concentre sur `java.time`, la meilleure pratique actuelle.**

---

## 1. Les principales classes de java.time

| Classe | Description | Exemple |
|--------|-------------|---------|
| `LocalDate` | Date sans heure (année, mois, jour) | 2026-04-10 |
| `LocalTime` | Heure sans date (heure, minute, seconde) | 14:30:25 |
| `LocalDateTime` | Date + heure sans fuseau horaire | 2026-04-10T14:30:25 |
| `ZonedDateTime` | Date + heure avec fuseau horaire | 2026-04-10T14:30:25-04:00[America/Toronto] |
| `Instant` | Point dans le temps (timestamp) | 2026-04-10T18:30:25Z |
| `Duration` | Durée en heures/minutes/secondes | 2 heures 30 minutes |
| `Period` | Période en années/mois/jours | 3 mois 15 jours |

---

## 2. LocalDate - Travailler avec les dates

### 2.1 Importer la classe

```java
import java.time.LocalDate;
```

### 2.2 Créer une date

```java
// Date actuelle
LocalDate aujourdhui = LocalDate.now();
System.out.println(aujourdhui); // 2026-04-10

// Date spécifique (année, mois, jour)
LocalDate noel = LocalDate.of(2026, 12, 25);
System.out.println(noel); // 2026-12-25

// Avec le mois en constante (plus lisible)
LocalDate noel2 = LocalDate.of(2026, Month.DECEMBER, 25);
```

### 2.3 Extraire les composantes

```java
LocalDate date = LocalDate.of(2026, 4, 10);

int annee = date.getYear();           // 2026
int mois = date.getMonthValue();      // 4
Month moisEnum = date.getMonth();     // APRIL
int jour = date.getDayOfMonth();      // 10
DayOfWeek jourSemaine = date.getDayOfWeek(); // THURSDAY
int jourAnnee = date.getDayOfYear();  // 100

System.out.println("Année : " + annee);
System.out.println("Mois : " + mois);
System.out.println("Jour de la semaine : " + jourSemaine);
```

### 2.4 Modifier une date

> **Important** : Les objets `LocalDate` sont **immutables**. Les méthodes retournent une **nouvelle** instance.

```java
LocalDate aujourdhui = LocalDate.now(); // 2026-04-10

// Ajouter des jours, mois, années
LocalDate dans7Jours = aujourdhui.plusDays(7);        // 2026-04-17
LocalDate dans2Mois = aujourdhui.plusMonths(2);       // 2026-06-10
LocalDate dans1An = aujourdhui.plusYears(1);          // 2027-04-10

// Soustraire
LocalDate il7Jours = aujourdhui.minusDays(7);         // 2026-04-03
LocalDate il2Mois = aujourdhui.minusMonths(2);        // 2026-02-10

// Modifier une composante spécifique
LocalDate nouvelleDate = aujourdhui.withYear(2025);   // 2025-04-10
LocalDate premiereJour = aujourdhui.withDayOfMonth(1); // 2026-04-01
```

### 2.5 Comparer des dates

```java
LocalDate date1 = LocalDate.of(2026, 4, 10);
LocalDate date2 = LocalDate.of(2026, 12, 25);

// Méthodes de comparaison
boolean estAvant = date1.isBefore(date2);      // true
boolean estApres = date1.isAfter(date2);       // false
boolean estEgal = date1.isEqual(date2);        // false

// Vérifications spéciales
boolean estBissextile = date1.isLeapYear();    // false

if (date1.isBefore(date2)) {
    System.out.println("date1 est avant date2");
}
```

---

## 3. LocalTime - Travailler avec les heures

### 3.1 Créer une heure

```java
import java.time.LocalTime;

// Heure actuelle
LocalTime maintenant = LocalTime.now();
System.out.println(maintenant); // 14:30:25.123456789

// Heure spécifique
LocalTime midi = LocalTime.of(12, 0);              // 12:00
LocalTime heure = LocalTime.of(14, 30, 25);        // 14:30:25
LocalTime precis = LocalTime.of(14, 30, 25, 123);  // 14:30:25.000000123
```

### 3.2 Extraire et modifier

```java
LocalTime heure = LocalTime.of(14, 30, 25);

int heures = heure.getHour();       // 14
int minutes = heure.getMinute();    // 30
int secondes = heure.getSecond();   // 25

// Modifier (retourne une nouvelle instance)
LocalTime plus2h = heure.plusHours(2);      // 16:30:25
LocalTime moins15m = heure.minusMinutes(15); // 14:15:25
```

---

## 4. LocalDateTime - Date + Heure

### 4.1 Créer un LocalDateTime

```java
import java.time.LocalDateTime;

// Maintenant
LocalDateTime maintenant = LocalDateTime.now();
System.out.println(maintenant); // 2026-04-10T14:30:25.123456789

// Date et heure spécifiques
LocalDateTime dateHeure = LocalDateTime.of(2026, 4, 10, 14, 30);
// 2026-04-10T14:30

// Combiner LocalDate et LocalTime
LocalDate date = LocalDate.of(2026, 4, 10);
LocalTime heure = LocalTime.of(14, 30);
LocalDateTime combine = LocalDateTime.of(date, heure);
```

### 4.2 Manipulations

```java
LocalDateTime dt = LocalDateTime.now();

// Extraire les composantes
LocalDate dateSeule = dt.toLocalDate();
LocalTime heureSeule = dt.toLocalTime();

// Modifier
LocalDateTime demain = dt.plusDays(1);
LocalDateTime dans2h = dt.plusHours(2);
LocalDateTime nouveauMois = dt.withMonth(12);
```

---

## 5. Formater et Parser les dates

### 5.1 DateTimeFormatter - Formater une date

```java
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;

LocalDate date = LocalDate.of(2026, 4, 10);

// Formats prédéfinis
String iso = date.format(DateTimeFormatter.ISO_DATE);
System.out.println(iso); // 2026-04-10

// Format personnalisé
DateTimeFormatter formatFR = DateTimeFormatter.ofPattern("dd/MM/yyyy");
String dateFR = date.format(formatFR);
System.out.println(dateFR); // 10/04/2026

DateTimeFormatter formatLong = DateTimeFormatter.ofPattern("EEEE dd MMMM yyyy");
String dateLongue = date.format(formatLong);
System.out.println(dateLongue); // jeudi 10 avril 2026
```

### 5.2 Patterns de formatage

| Pattern | Signification | Exemple |
|---------|---------------|---------|
| `d` ou `dd` | Jour du mois | 5 ou 05 |
| `M` ou `MM` | Mois numérique | 4 ou 04 |
| `MMM` | Mois abrégé | avr. |
| `MMMM` | Mois complet | avril |
| `yy` ou `yyyy` | Année | 26 ou 2026 |
| `E` ou `EEEE` | Jour de la semaine | jeu. ou jeudi |
| `H` ou `HH` | Heure (24h) | 9 ou 09 |
| `h` ou `hh` | Heure (12h) | 9 ou 09 |
| `m` ou `mm` | Minutes | 5 ou 05 |
| `s` ou `ss` | Secondes | 5 ou 05 |
| `a` | AM/PM | AM |

### 5.3 Parser (convertir String → Date)

```java
String texte = "10/04/2026";
DateTimeFormatter format = DateTimeFormatter.ofPattern("dd/MM/yyyy");

LocalDate date = LocalDate.parse(texte, format);
System.out.println(date); // 2026-04-10

// Pour LocalDateTime
String texteHeure = "10/04/2026 14:30";
DateTimeFormatter formatHeure = DateTimeFormatter.ofPattern("dd/MM/yyyy HH:mm");
LocalDateTime dateHeure = LocalDateTime.parse(texteHeure, formatHeure);
```

### 5.4 Formater avec Locale (langue)

```java
import java.util.Locale;

LocalDate date = LocalDate.of(2026, 4, 10);

// En français
DateTimeFormatter formatFR = DateTimeFormatter
    .ofPattern("EEEE dd MMMM yyyy", Locale.FRENCH);
System.out.println(date.format(formatFR)); // jeudi 10 avril 2026

// En anglais
DateTimeFormatter formatEN = DateTimeFormatter
    .ofPattern("EEEE dd MMMM yyyy", Locale.ENGLISH);
System.out.println(date.format(formatEN)); // Thursday 10 April 2026
```

---

## 6. Period - Périodes (jours, mois, années)

`Period` représente une durée en termes de **jours, mois et années**.

```java
import java.time.Period;

// Créer une période
Period unMois = Period.ofMonths(1);
Period deuxSemaines = Period.ofWeeks(2);  // = 14 jours
Period periode = Period.of(1, 6, 15);     // 1 an, 6 mois, 15 jours

// Ajouter une période à une date
LocalDate aujourdhui = LocalDate.now();
LocalDate future = aujourdhui.plus(periode);

// Calculer la période entre deux dates
LocalDate naissance = LocalDate.of(2000, 3, 15);
LocalDate aujourdhuiDate = LocalDate.now();
Period age = Period.between(naissance, aujourdhuiDate);

System.out.println("Âge : " + age.getYears() + " ans, " 
    + age.getMonths() + " mois, " 
    + age.getDays() + " jours");
```

---

## 7. Duration - Durées (heures, minutes, secondes)

`Duration` représente une durée en **heures, minutes, secondes**.

```java
import java.time.Duration;

// Créer une durée
Duration deuxHeures = Duration.ofHours(2);
Duration trenteMins = Duration.ofMinutes(30);
Duration combinee = Duration.ofHours(2).plusMinutes(30);

// Ajouter à un LocalDateTime
LocalDateTime maintenant = LocalDateTime.now();
LocalDateTime plus2h = maintenant.plus(deuxHeures);

// Calculer la durée entre deux moments
LocalDateTime debut = LocalDateTime.of(2026, 4, 10, 9, 0);
LocalDateTime fin = LocalDateTime.of(2026, 4, 10, 17, 30);
Duration duree = Duration.between(debut, fin);

System.out.println("Durée : " + duree.toHours() + " heures");
System.out.println("Ou : " + duree.toMinutes() + " minutes");
```

---

## 8. ZonedDateTime - Dates avec fuseau horaire

```java
import java.time.ZonedDateTime;
import java.time.ZoneId;

// Date/heure dans le fuseau local
ZonedDateTime maintenant = ZonedDateTime.now();
System.out.println(maintenant);
// 2026-04-10T14:30:25.123-04:00[America/Toronto]

// Dans un fuseau spécifique
ZonedDateTime paris = ZonedDateTime.now(ZoneId.of("Europe/Paris"));
ZonedDateTime tokyo = ZonedDateTime.now(ZoneId.of("Asia/Tokyo"));

// Convertir entre fuseaux
ZonedDateTime heureLocale = ZonedDateTime.now();
ZonedDateTime heureNY = heureLocale.withZoneSameInstant(
    ZoneId.of("America/New_York")
);

System.out.println("Ici : " + heureLocale);
System.out.println("À NY : " + heureNY);
```

---

## 9. Instant - Timestamp universel

`Instant` représente un point précis dans le temps (comme un timestamp Unix).

```java
import java.time.Instant;

// Maintenant en UTC
Instant maintenant = Instant.now();
System.out.println(maintenant); // 2026-04-10T18:30:25.123Z

// Obtenir le timestamp en secondes
long secondes = maintenant.getEpochSecond();
System.out.println("Secondes depuis epoch : " + secondes);

// Convertir vers LocalDateTime
LocalDateTime dateHeure = LocalDateTime.ofInstant(
    maintenant, 
    ZoneId.systemDefault()
);
```

---

## 10. Exemples pratiques complets

### Exemple 1 : Calculer l'âge

```java
import java.time.LocalDate;
import java.time.Period;

public class CalculAge {
    public static void main(String[] args) {
        LocalDate dateNaissance = LocalDate.of(2000, 5, 15);
        LocalDate aujourdhui = LocalDate.now();
        
        Period age = Period.between(dateNaissance, aujourdhui);
        
        System.out.println("Vous avez " + age.getYears() + " ans");
    }
}
```

### Exemple 2 : Compte à rebours

```java
import java.time.LocalDate;
import java.time.temporal.ChronoUnit;

public class CompteARebours {
    public static void main(String[] args) {
        LocalDate aujourdhui = LocalDate.now();
        LocalDate vacances = LocalDate.of(2026, 7, 1);
        
        long joursRestants = ChronoUnit.DAYS.between(aujourdhui, vacances);
        
        System.out.println("Plus que " + joursRestants + " jours avant les vacances !");
    }
}
```

### Exemple 3 : Gestion de rendez-vous

```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class Rendezvouz {
    public static void main(String[] args) {
        LocalDateTime rdv = LocalDateTime.of(2026, 4, 15, 14, 30);
        
        DateTimeFormatter format = DateTimeFormatter.ofPattern(
            "EEEE dd MMMM yyyy 'à' HH'h'mm"
        );
        
        System.out.println("Votre rendez-vous : " + rdv.format(format));
        // Votre rendez-vous : mercredi 15 avril 2026 à 14h30
        
        // Rappel 1 jour avant
        LocalDateTime rappel = rdv.minusDays(1);
        System.out.println("Rappel : " + rappel.format(format));
    }
}
```

### Exemple 4 : Vérifier si une date est un week-end

```java
import java.time.LocalDate;
import java.time.DayOfWeek;

public class WeekendChecker {
    public static boolean estWeekend(LocalDate date) {
        DayOfWeek jour = date.getDayOfWeek();
        return jour == DayOfWeek.SATURDAY || jour == DayOfWeek.SUNDAY;
    }
    
    public static void main(String[] args) {
        LocalDate date = LocalDate.of(2026, 4, 11); // Samedi
        
        if (estWeekend(date)) {
            System.out.println("C'est le week-end ! 🎉");
        } else {
            System.out.println("Jour de semaine 😔");
        }
    }
}
```

---

## 11. ChronoUnit - Calculs avancés

```java
import java.time.LocalDate;
import java.time.temporal.ChronoUnit;

LocalDate debut = LocalDate.of(2026, 1, 1);
LocalDate fin = LocalDate.of(2026, 12, 31);

// Différents types de calculs
long jours = ChronoUnit.DAYS.between(debut, fin);
long semaines = ChronoUnit.WEEKS.between(debut, fin);
long mois = ChronoUnit.MONTHS.between(debut, fin);

System.out.println("Jours : " + jours);      // 364
System.out.println("Semaines : " + semaines); // 52
System.out.println("Mois : " + mois);         // 11
```

---

## 12. Bonnes pratiques

### ✅ À FAIRE

1. **Utiliser les types appropriés**
   - `LocalDate` pour les dates seules (anniversaires, dates historiques)
   - `LocalDateTime` pour date + heure sans fuseau horaire
   - `ZonedDateTime` pour les événements internationaux
   - `Instant` pour les timestamps (logs, base de données)

2. **Penser immutabilité**
   ```java
   LocalDate date = LocalDate.now();
   date.plusDays(1); // ❌ Ne modifie PAS date !
   
   LocalDate demain = date.plusDays(1); // ✅ Correct
   ```

3. **Utiliser les constantes**
   ```java
   LocalDate.of(2026, Month.APRIL, 10); // ✅ Lisible
   LocalDate.of(2026, 4, 10);           // ⚠️ Moins clair
   ```

4. **Gérer les fuseaux horaires explicitement**
   ```java
   ZonedDateTime.now(ZoneId.of("America/Toronto"));
   ```

### ❌ À ÉVITER

1. **Ne pas confondre Month et jour**
   ```java
   // Les mois vont de 1 à 12 (pas 0 à 11 comme avec Date !)
   LocalDate.of(2026, 4, 10); // ✅ 10 avril
   ```

2. **Ne pas ignorer les exceptions de parsing**
   ```java
   try {
       LocalDate date = LocalDate.parse("invalid");
   } catch (DateTimeParseException e) {
       System.out.println("Format invalide");
   }
   ```

---

## 13. Résumé des classes principales

| Classe | Utilisation | Exemple de création |
|--------|-------------|---------------------|
| `LocalDate` | Date sans heure | `LocalDate.now()` |
| `LocalTime` | Heure sans date | `LocalTime.of(14, 30)` |
| `LocalDateTime` | Date + heure | `LocalDateTime.now()` |
| `ZonedDateTime` | Date + heure + fuseau | `ZonedDateTime.now()` |
| `Instant` | Timestamp UTC | `Instant.now()` |
| `Period` | Durée en jours/mois/ans | `Period.ofMonths(3)` |
| `Duration` | Durée en h/min/sec | `Duration.ofHours(2)` |
| `DateTimeFormatter` | Formatage/parsing | `DateTimeFormatter.ofPattern("dd/MM/yyyy")` |

---

## 14. Méthodes communes importantes

```java
// Création
.now()              // Moment actuel
.of(...)            // Valeur spécifique
.parse(...)         // Depuis String

// Extraction
.getYear()          // Année
.getMonth()         // Mois
.getDayOfMonth()    // Jour du mois
.getDayOfWeek()     // Jour de la semaine

// Modification (retourne nouvelle instance)
.plusDays(n)        // Ajouter n jours
.minusMonths(n)     // Soustraire n mois
.withYear(y)        // Changer l'année

// Comparaison
.isBefore(...)      // Est avant ?
.isAfter(...)       // Est après ?
.isEqual(...)       // Est égal ?

// Formatage
.format(formatter)  // Vers String
```

---

## 15. Exercices pratiques

### Exercice 1 : Anniversaire
Écrivez un programme qui :
- Demande la date de naissance
- Calcule l'âge exact
- Indique le nombre de jours jusqu'au prochain anniversaire

### Exercice 2 : Heures de travail
Créez un programme qui calcule le nombre d'heures entre deux LocalDateTime (début et fin de journée).

### Exercice 3 : Calendrier
Affichez tous les jours d'un mois donné avec leur jour de la semaine.

### Exercice 4 : Validation de date
Créez une méthode qui vérifie si une String représente une date valide au format "dd/MM/yyyy".

---

## 📌 Note historique : La classe Date (obsolète)

Avant Java 8, on utilisait la classe `java.util.Date` pour manipuler les dates. Cette classe est maintenant **dépréciée** et ne devrait **plus être utilisée** dans le nouveau code.

### Pourquoi Date est obsolète ?

❌ **Problèmes de Date** :
- Non immutable (thread-unsafe)
- API confuse (mois de 0 à 11)
- Mélange date et fuseau horaire
- Calculs de dates difficiles
- Mauvaise gestion des fuseaux horaires

### Exemple avec Date (ancien code)

```java
// ⚠️ ANCIEN CODE - Ne plus utiliser !
import java.util.Date;
import java.text.SimpleDateFormat;

Date maintenant = new Date();
SimpleDateFormat sdf = new SimpleDateFormat("dd/MM/yyyy");
String dateFormatee = sdf.format(maintenant);
```

### Migration Date → java.time

Si vous devez travailler avec du vieux code utilisant `Date` :

```java
// Convertir Date → LocalDateTime
Date ancienneDate = new Date();
LocalDateTime nouveau = ancienneDate.toInstant()
    .atZone(ZoneId.systemDefault())
    .toLocalDateTime();

// Convertir LocalDateTime → Date
LocalDateTime maintenant = LocalDateTime.now();
Date ancienFormat = Date.from(
    maintenant.atZone(ZoneId.systemDefault()).toInstant()
);
```

> **Conseil** : Si vous voyez `java.util.Date` ou `SimpleDateFormat` dans du code existant, envisagez de le migrer vers `java.time`.

---

## 🎓 Ressources supplémentaires

- **Documentation Oracle** : [Package java.time](https://docs.oracle.com/javase/8/docs/api/java/time/package-summary.html)
- **Tutorial officiel** : [Date Time Tutorial](https://docs.oracle.com/javase/tutorial/datetime/)
- **ISO 8601** : Standard international pour les dates

---


# Exercices pratiques - Les Dates en Java (java.time)

## 📚 Comment utiliser ces exercices ?

Chaque exercice est conçu pour vous faire découvrir et pratiquer les concepts de manipulation de dates en Java. Essayez de résoudre les exercices **sans regarder la solution** en premier. Si vous êtes bloqué, consultez les indices progressifs avant de voir la solution complète.

**Niveau de difficulté** :
- ⭐ : Débutant
- ⭐⭐ : Intermédiaire
- ⭐⭐⭐ : Avancé

---

## Niveau 1 : Découverte de LocalDate ⭐

### Exercice 1.1 : Afficher la date du jour

**Objectif** : Créer un programme qui affiche la date actuelle.

**Consigne** :
- Utilisez `LocalDate` pour obtenir la date du jour
- Affichez-la au format : "Nous sommes le [date]"

<details>
<summary>💡 Indice 1</summary>

Regardez la méthode `.now()` de la classe `LocalDate`.
</details>

<details>
<summary>💡 Indice 2</summary>

```java
import java.time.LocalDate;
```
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalDate;

public class DateDuJour {
    public static void main(String[] args) {
        LocalDate aujourdhui = LocalDate.now();
        System.out.println("Nous sommes le " + aujourdhui);
    }
}
```
</details>

---

### Exercice 1.2 : Créer une date spécifique

**Objectif** : Créer et afficher votre date de naissance.

**Consigne** :
- Créez une variable `dateNaissance` avec votre date de naissance
- Affichez : "Je suis né(e) le [date]"

<details>
<summary>💡 Indice</summary>

Utilisez `LocalDate.of(année, mois, jour)`.
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalDate;

public class DateNaissance {
    public static void main(String[] args) {
        LocalDate dateNaissance = LocalDate.of(2000, 5, 15);
        System.out.println("Je suis né(e) le " + dateNaissance);
    }
}
```
</details>

---

### Exercice 1.3 : Extraire les composantes d'une date

**Objectif** : Décomposer une date en année, mois et jour.

**Consigne** :
- Créez une date de votre choix
- Affichez séparément : l'année, le mois et le jour
- Format attendu :
  ```
  Année : 2026
  Mois : 4
  Jour : 10
  ```

<details>
<summary>💡 Indice</summary>

Utilisez `.getYear()`, `.getMonthValue()` et `.getDayOfMonth()`.
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalDate;

public class DecomposerDate {
    public static void main(String[] args) {
        LocalDate date = LocalDate.of(2026, 4, 10);
        
        System.out.println("Année : " + date.getYear());
        System.out.println("Mois : " + date.getMonthValue());
        System.out.println("Jour : " + date.getDayOfMonth());
    }
}
```
</details>

---

### Exercice 1.4 : Quel jour de la semaine ?

**Objectif** : Afficher le jour de la semaine d'une date donnée.

**Consigne** :
- Créez une date (exemple : 1er janvier 2000)
- Affichez le jour de la semaine (MONDAY, TUESDAY, etc.)
- **Bonus** : Affichez aussi le numéro du jour dans l'année

<details>
<summary>💡 Indice</summary>

Regardez `.getDayOfWeek()` et `.getDayOfYear()`.
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalDate;
import java.time.DayOfWeek;

public class JourSemaine {
    public static void main(String[] args) {
        LocalDate date = LocalDate.of(2000, 1, 1);
        DayOfWeek jour = date.getDayOfWeek();
        int jourAnnee = date.getDayOfYear();
        
        System.out.println("Le " + date + " était un " + jour);
        System.out.println("C'était le jour numéro " + jourAnnee + " de l'année");
    }
}
```
</details>

---

## Niveau 2 : Manipulation de dates ⭐

### Exercice 2.1 : Calculer une date future

**Objectif** : Trouver quelle date ce sera dans 100 jours.

**Consigne** :
- Partez de la date du jour
- Ajoutez 100 jours
- Affichez : "Dans 100 jours, nous serons le [date]"

<details>
<summary>💡 Indice</summary>

Utilisez `.plusDays(100)`. N'oubliez pas que les objets LocalDate sont immutables !
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalDate;

public class DateFuture {
    public static void main(String[] args) {
        LocalDate aujourdhui = LocalDate.now();
        LocalDate dans100Jours = aujourdhui.plusDays(100);
        
        System.out.println("Aujourd'hui : " + aujourdhui);
        System.out.println("Dans 100 jours, nous serons le " + dans100Jours);
    }
}
```
</details>

---

### Exercice 2.2 : Combien de jours jusqu'à Noël ?

**Objectif** : Calculer le nombre de jours entre aujourd'hui et le prochain Noël.

**Consigne** :
- Créez une date pour Noël de cette année (25 décembre)
- Calculez la différence en jours
- Affichez : "Il reste [X] jours avant Noël !"
- **Attention** : Si Noël est déjà passé, calculez pour Noël de l'année prochaine

<details>
<summary>💡 Indice 1</summary>

Utilisez `ChronoUnit.DAYS.between(date1, date2)`. N'oubliez pas d'importer `java.time.temporal.ChronoUnit`.
</details>

<details>
<summary>💡 Indice 2</summary>

Utilisez `.isAfter()` pour vérifier si Noël est passé, et `.plusYears(1)` si nécessaire.
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalDate;
import java.time.temporal.ChronoUnit;

public class CompteReboursNoel {
    public static void main(String[] args) {
        LocalDate aujourdhui = LocalDate.now();
        LocalDate noel = LocalDate.of(aujourdhui.getYear(), 12, 25);
        
        // Si Noël est passé, prendre l'année prochaine
        if (aujourdhui.isAfter(noel)) {
            noel = noel.plusYears(1);
        }
        
        long jours = ChronoUnit.DAYS.between(aujourdhui, noel);
        System.out.println("Il reste " + jours + " jours avant Noël !");
    }
}
```
</details>

---

### Exercice 2.3 : Calculateur d'âge

**Objectif** : Créer un programme qui calcule l'âge exact d'une personne.

**Consigne** :
- Demandez une date de naissance (vous pouvez la coder en dur pour l'instant)
- Calculez l'âge en années
- Affichez : "Vous avez [X] ans"
- **Bonus** : Affichez aussi les mois et jours : "Vous avez X ans, Y mois et Z jours"

<details>
<summary>💡 Indice</summary>

Utilisez `Period.between(dateNaissance, aujourdhui)` puis `.getYears()`, `.getMonths()`, `.getDays()`.
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalDate;
import java.time.Period;

public class CalculateurAge {
    public static void main(String[] args) {
        LocalDate dateNaissance = LocalDate.of(2000, 3, 15);
        LocalDate aujourdhui = LocalDate.now();
        
        Period age = Period.between(dateNaissance, aujourdhui);
        
        System.out.println("Vous avez " + age.getYears() + " ans");
        
        // Bonus : affichage complet
        System.out.println("Plus précisément : " + age.getYears() 
            + " ans, " + age.getMonths() + " mois et " 
            + age.getDays() + " jours");
    }
}
```
</details>

---

### Exercice 2.4 : Est-ce un anniversaire ?

**Objectif** : Vérifier si aujourd'hui est l'anniversaire de quelqu'un.

**Consigne** :
- Créez une date de naissance
- Comparez le jour et le mois avec la date actuelle
- Affichez "Joyeux anniversaire !" ou "Ce n'est pas votre anniversaire aujourd'hui"

<details>
<summary>💡 Indice</summary>

Comparez `.getMonthValue()` et `.getDayOfMonth()` des deux dates.
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalDate;

public class VerifierAnniversaire {
    public static void main(String[] args) {
        LocalDate dateNaissance = LocalDate.of(1995, 4, 10);
        LocalDate aujourdhui = LocalDate.now();
        
        if (dateNaissance.getMonthValue() == aujourdhui.getMonthValue() 
            && dateNaissance.getDayOfMonth() == aujourdhui.getDayOfMonth()) {
            System.out.println("🎉 Joyeux anniversaire !");
        } else {
            System.out.println("Ce n'est pas votre anniversaire aujourd'hui");
        }
    }
}
```
</details>

---

## Niveau 3 : Formatage et parsing ⭐⭐

### Exercice 3.1 : Formater une date en français

**Objectif** : Afficher une date au format français : "10/04/2026".

**Consigne** :
- Créez une date
- Utilisez `DateTimeFormatter` pour l'afficher au format "dd/MM/yyyy"

<details>
<summary>💡 Indice</summary>

```java
DateTimeFormatter format = DateTimeFormatter.ofPattern("dd/MM/yyyy");
String dateFormatee = date.format(format);
```
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;

public class FormaterDate {
    public static void main(String[] args) {
        LocalDate date = LocalDate.of(2026, 4, 10);
        DateTimeFormatter formatFR = DateTimeFormatter.ofPattern("dd/MM/yyyy");
        
        String dateFormatee = date.format(formatFR);
        System.out.println("Date formatée : " + dateFormatee);
    }
}
```
</details>

---

### Exercice 3.2 : Date longue en français

**Objectif** : Afficher "jeudi 10 avril 2026".

**Consigne** :
- Créez une date
- Formatez-la pour afficher : jour de la semaine, jour, mois (texte), année
- Utilisez `Locale.FRENCH` pour avoir les noms en français

<details>
<summary>💡 Indice</summary>

Pattern : `"EEEE dd MMMM yyyy"` avec `Locale.FRENCH`.
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.util.Locale;

public class DateLongue {
    public static void main(String[] args) {
        LocalDate date = LocalDate.of(2026, 4, 10);
        DateTimeFormatter format = DateTimeFormatter.ofPattern(
            "EEEE dd MMMM yyyy", 
            Locale.FRENCH
        );
        
        System.out.println(date.format(format));
        // Affiche : jeudi 10 avril 2026
    }
}
```
</details>

---

### Exercice 3.3 : Convertir une chaîne en date

**Objectif** : Parser (convertir) une chaîne de texte en objet LocalDate.

**Consigne** :
- Vous avez la chaîne : "15/08/2025"
- Convertissez-la en LocalDate
- Affichez le jour de la semaine de cette date

<details>
<summary>💡 Indice</summary>

Utilisez `LocalDate.parse(texte, formatter)`.
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;

public class ParserDate {
    public static void main(String[] args) {
        String texte = "15/08/2025";
        DateTimeFormatter format = DateTimeFormatter.ofPattern("dd/MM/yyyy");
        
        LocalDate date = LocalDate.parse(texte, format);
        
        System.out.println("Date parsée : " + date);
        System.out.println("Jour de la semaine : " + date.getDayOfWeek());
    }
}
```
</details>

---

### Exercice 3.4 : Validateur de date

**Objectif** : Créer une méthode qui vérifie si une chaîne est une date valide.

**Consigne** :
- Créez une méthode `estDateValide(String texte)`
- Elle retourne `true` si le texte est une date valide au format "dd/MM/yyyy"
- Elle retourne `false` sinon
- Testez avec : "10/04/2026" (valide) et "32/13/2026" (invalide)

<details>
<summary>💡 Indice</summary>

Utilisez un bloc `try-catch` avec `DateTimeParseException`.
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.time.format.DateTimeParseException;

public class ValidateurDate {
    
    public static boolean estDateValide(String texte) {
        DateTimeFormatter format = DateTimeFormatter.ofPattern("dd/MM/yyyy");
        try {
            LocalDate.parse(texte, format);
            return true;
        } catch (DateTimeParseException e) {
            return false;
        }
    }
    
    public static void main(String[] args) {
        System.out.println("10/04/2026 est valide ? " + estDateValide("10/04/2026"));
        System.out.println("32/13/2026 est valide ? " + estDateValide("32/13/2026"));
        System.out.println("abc est valide ? " + estDateValide("abc"));
    }
}
```
</details>

---

## Niveau 4 : LocalTime et LocalDateTime ⭐⭐

### Exercice 4.1 : Afficher l'heure actuelle

**Objectif** : Créer un programme qui affiche l'heure actuelle.

**Consigne** :
- Utilisez `LocalTime` pour obtenir l'heure
- Affichez au format : "Il est actuellement [heure]"

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalTime;

public class HeureActuelle {
    public static void main(String[] args) {
        LocalTime maintenant = LocalTime.now();
        System.out.println("Il est actuellement " + maintenant);
    }
}
```
</details>

---

### Exercice 4.2 : Créer un rendez-vous

**Objectif** : Créer et afficher un rendez-vous complet (date + heure).

**Consigne** :
- Créez un `LocalDateTime` pour un rendez-vous : le 15 mai 2026 à 14h30
- Affichez-le au format : "Votre rendez-vous est le 15/05/2026 à 14:30"

<details>
<summary>💡 Indice</summary>

Utilisez `DateTimeFormatter.ofPattern("dd/MM/yyyy 'à' HH:mm")`.
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class Rendezvous {
    public static void main(String[] args) {
        LocalDateTime rdv = LocalDateTime.of(2026, 5, 15, 14, 30);
        DateTimeFormatter format = DateTimeFormatter.ofPattern("dd/MM/yyyy 'à' HH:mm");
        
        System.out.println("Votre rendez-vous est le " + rdv.format(format));
    }
}
```
</details>

---

### Exercice 4.3 : Calculer la durée d'un film

**Objectif** : Calculer combien de temps dure un film.

**Consigne** :
- Le film commence à 20h15
- Il se termine à 22h45
- Calculez et affichez la durée en heures et minutes

<details>
<summary>💡 Indice</summary>

Utilisez `Duration.between(debut, fin)` puis `.toHours()` et `.toMinutesPart()`.
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalTime;
import java.time.Duration;

public class DureeFilm {
    public static void main(String[] args) {
        LocalTime debut = LocalTime.of(20, 15);
        LocalTime fin = LocalTime.of(22, 45);
        
        Duration duree = Duration.between(debut, fin);
        
        long heures = duree.toHours();
        long minutes = duree.toMinutesPart();
        
        System.out.println("Le film dure " + heures + "h" + minutes);
    }
}
```
</details>

---

### Exercice 4.4 : Est-ce le matin, l'après-midi ou le soir ?

**Objectif** : Déterminer la période de la journée selon l'heure.

**Consigne** :
- Créez une méthode `getPeriodeJournee(LocalTime heure)`
- Elle retourne :
  - "Matin" si entre 6h et 12h
  - "Après-midi" si entre 12h et 18h
  - "Soir" si entre 18h et 22h
  - "Nuit" sinon
- Testez avec différentes heures

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalTime;

public class PeriodeJournee {
    
    public static String getPeriodeJournee(LocalTime heure) {
        int h = heure.getHour();
        
        if (h >= 6 && h < 12) {
            return "Matin";
        } else if (h >= 12 && h < 18) {
            return "Après-midi";
        } else if (h >= 18 && h < 22) {
            return "Soir";
        } else {
            return "Nuit";
        }
    }
    
    public static void main(String[] args) {
        LocalTime[] heures = {
            LocalTime.of(8, 30),
            LocalTime.of(14, 0),
            LocalTime.of(20, 45),
            LocalTime.of(2, 15)
        };
        
        for (LocalTime h : heures) {
            System.out.println(h + " -> " + getPeriodeJournee(h));
        }
    }
}
```
</details>

---

## Niveau 5 : Projets complets ⭐⭐⭐

### Exercice 5.1 : Calendrier d'un mois

**Objectif** : Afficher tous les jours d'un mois donné.

**Consigne** :
- Demandez un mois et une année (codés en dur)
- Affichez tous les jours du mois avec leur jour de la semaine
- Format : "1 - MONDAY, 2 - TUESDAY, ..."

<details>
<summary>💡 Indice</summary>

Utilisez une boucle de 1 à `date.lengthOfMonth()` et `.withDayOfMonth(i)`.
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalDate;

public class CalendrierMois {
    public static void main(String[] args) {
        int annee = 2026;
        int mois = 4; // Avril
        
        LocalDate premierJour = LocalDate.of(annee, mois, 1);
        int nombreJours = premierJour.lengthOfMonth();
        
        System.out.println("=== Calendrier de " + premierJour.getMonth() 
            + " " + annee + " ===\n");
        
        for (int jour = 1; jour <= nombreJours; jour++) {
            LocalDate date = premierJour.withDayOfMonth(jour);
            System.out.println(jour + " - " + date.getDayOfWeek());
        }
    }
}
```
</details>

---

### Exercice 5.2 : Calculateur de jours ouvrables

**Objectif** : Calculer le nombre de jours ouvrables entre deux dates.

**Consigne** :
- Créez une méthode `compterJoursOuvrables(LocalDate debut, LocalDate fin)`
- Un jour ouvrable = du lundi au vendredi (pas samedi/dimanche)
- Retournez le nombre de jours ouvrables
- Testez avec : du 1er avril 2026 au 30 avril 2026

<details>
<summary>💡 Indice</summary>

Utilisez une boucle avec `.plusDays(1)` et vérifiez `getDayOfWeek()` pour exclure samedi/dimanche.
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalDate;
import java.time.DayOfWeek;

public class JoursOuvrables {
    
    public static int compterJoursOuvrables(LocalDate debut, LocalDate fin) {
        int count = 0;
        LocalDate current = debut;
        
        while (!current.isAfter(fin)) {
            DayOfWeek jour = current.getDayOfWeek();
            
            // Compter seulement lundi à vendredi
            if (jour != DayOfWeek.SATURDAY && jour != DayOfWeek.SUNDAY) {
                count++;
            }
            
            current = current.plusDays(1);
        }
        
        return count;
    }
    
    public static void main(String[] args) {
        LocalDate debut = LocalDate.of(2026, 4, 1);
        LocalDate fin = LocalDate.of(2026, 4, 30);
        
        int joursOuvrables = compterJoursOuvrables(debut, fin);
        
        System.out.println("Du " + debut + " au " + fin);
        System.out.println("Nombre de jours ouvrables : " + joursOuvrables);
    }
}
```
</details>

---

### Exercice 5.3 : Gestionnaire d'événements

**Objectif** : Créer un mini-gestionnaire d'événements avec rappels.

**Consigne** :
Créez une classe `Evenement` avec :
- Un nom (String)
- Une date et heure (LocalDateTime)
- Une méthode `getTempsRestant()` qui retourne le temps jusqu'à l'événement
- Une méthode `estPasse()` qui vérifie si l'événement est passé
- Une méthode `afficherRappel()` qui affiche un message formaté

Créez ensuite 3 événements et affichez leurs informations.

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalDateTime;
import java.time.Duration;
import java.time.format.DateTimeFormatter;

class Evenement {
    private String nom;
    private LocalDateTime dateHeure;
    
    public Evenement(String nom, LocalDateTime dateHeure) {
        this.nom = nom;
        this.dateHeure = dateHeure;
    }
    
    public Duration getTempsRestant() {
        return Duration.between(LocalDateTime.now(), dateHeure);
    }
    
    public boolean estPasse() {
        return LocalDateTime.now().isAfter(dateHeure);
    }
    
    public void afficherRappel() {
        DateTimeFormatter format = DateTimeFormatter.ofPattern(
            "dd/MM/yyyy 'à' HH:mm"
        );
        
        System.out.println("\n=== " + nom + " ===");
        System.out.println("Date : " + dateHeure.format(format));
        
        if (estPasse()) {
            System.out.println("⚠️  Cet événement est passé !");
        } else {
            Duration temps = getTempsRestant();
            long jours = temps.toDays();
            long heures = temps.toHoursPart();
            
            System.out.println("⏰ Dans " + jours + " jours et " 
                + heures + " heures");
        }
    }
}

public class GestionnaireEvenements {
    public static void main(String[] args) {
        Evenement[] evenements = {
            new Evenement("Examen final", 
                LocalDateTime.of(2026, 5, 15, 9, 0)),
            new Evenement("Rendez-vous dentiste", 
                LocalDateTime.of(2026, 4, 20, 14, 30)),
            new Evenement("Concert", 
                LocalDateTime.of(2026, 6, 1, 20, 0))
        };
        
        System.out.println("=== MES ÉVÉNEMENTS ===");
        for (Evenement evt : evenements) {
            evt.afficherRappel();
        }
    }
}
```
</details>

---

### Exercice 5.4 : Simulateur de réservations

**Objectif** : Créer un système de gestion de créneaux horaires.

**Consigne** :
Créez un programme qui :
1. Définit des créneaux disponibles (ex: toutes les heures de 9h à 17h)
2. Permet de "réserver" un créneau
3. Affiche les créneaux disponibles et réservés
4. Vérifie qu'on ne peut pas réserver deux fois le même créneau

<details>
<summary>💡 Indice</summary>

Utilisez une `ArrayList<LocalTime>` pour stocker les créneaux réservés.
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.LocalTime;
import java.util.ArrayList;

class GestionnaireReservations {
    private ArrayList<LocalTime> creneauxReserves;
    private LocalTime heureDebut;
    private LocalTime heureFin;
    
    public GestionnaireReservations(LocalTime debut, LocalTime fin) {
        this.creneauxReserves = new ArrayList<>();
        this.heureDebut = debut;
        this.heureFin = fin;
    }
    
    public boolean reserver(LocalTime creneau) {
        // Vérifier si le créneau est dans les heures d'ouverture
        if (creneau.isBefore(heureDebut) || creneau.isAfter(heureFin)) {
            System.out.println("❌ Créneau en dehors des heures d'ouverture");
            return false;
        }
        
        // Vérifier si déjà réservé
        if (creneauxReserves.contains(creneau)) {
            System.out.println("❌ Ce créneau est déjà réservé");
            return false;
        }
        
        creneauxReserves.add(creneau);
        System.out.println("✅ Créneau " + creneau + " réservé avec succès");
        return true;
    }
    
    public void afficherDisponibilites() {
        System.out.println("\n=== DISPONIBILITÉS ===");
        LocalTime current = heureDebut;
        
        while (!current.isAfter(heureFin)) {
            if (creneauxReserves.contains(current)) {
                System.out.println(current + " - ❌ RÉSERVÉ");
            } else {
                System.out.println(current + " - ✅ DISPONIBLE");
            }
            current = current.plusHours(1);
        }
    }
}

public class SimulateurReservations {
    public static void main(String[] args) {
        GestionnaireReservations systeme = new GestionnaireReservations(
            LocalTime.of(9, 0),
            LocalTime.of(17, 0)
        );
        
        // Tentatives de réservation
        systeme.reserver(LocalTime.of(10, 0));
        systeme.reserver(LocalTime.of(14, 0));
        systeme.reserver(LocalTime.of(10, 0)); // Doublon
        systeme.reserver(LocalTime.of(8, 0));  // Hors horaires
        
        // Afficher toutes les disponibilités
        systeme.afficherDisponibilites();
    }
}
```
</details>

---

### Exercice 5.5 : Comparateur de fuseaux horaires

**Objectif** : Afficher l'heure actuelle dans différents fuseaux horaires.

**Consigne** :
- Créez un programme qui affiche l'heure actuelle à :
  - Montréal (America/Toronto)
  - Paris (Europe/Paris)
  - Tokyo (Asia/Tokyo)
  - Sydney (Australia/Sydney)
- Formatez l'affichage pour qu'il soit clair et lisible

<details>
<summary>💡 Indice</summary>

Utilisez `ZonedDateTime.now(ZoneId.of("..."))`.
</details>

<details>
<summary>✅ Solution</summary>

```java
import java.time.ZonedDateTime;
import java.time.ZoneId;
import java.time.format.DateTimeFormatter;

public class FuseauxHoraires {
    
    public static void afficherHeure(String ville, String zoneId) {
        ZonedDateTime heure = ZonedDateTime.now(ZoneId.of(zoneId));
        DateTimeFormatter format = DateTimeFormatter.ofPattern(
            "HH:mm:ss 'le' dd/MM/yyyy"
        );
        
        System.out.println(ville + " : " + heure.format(format));
    }
    
    public static void main(String[] args) {
        System.out.println("=== HEURE MONDIALE ===\n");
        
        afficherHeure("🇨🇦 Montréal", "America/Toronto");
        afficherHeure("🇫🇷 Paris   ", "Europe/Paris");
        afficherHeure("🇯🇵 Tokyo   ", "Asia/Tokyo");
        afficherHeure("🇦🇺 Sydney  ", "Australia/Sydney");
    }
}
```
</details>

---

## 🎯 Défis bonus

### Défi 1 : Générateur de planning hebdomadaire
Créez un programme qui génère un planning de la semaine avec des événements aléatoires.

### Défi 2 : Calculateur d'échéances
Créez un système qui calcule les dates d'échéance pour des paiements mensuels (ex: prêt sur 12 mois).

### Défi 3 : Détecteur de dates spéciales
Créez un programme qui détecte si une date donnée est :
- Un jour férié (vous choisissez les jours fériés)
- Un vendredi 13
- Un jour bissextile

### Défi 4 : Horloge temps réel
Créez une horloge qui s'actualise chaque seconde et affiche l'heure actuelle (utilisez `Thread.sleep()`).

---

## 📝 Conseils pour progresser

1. **Essayez avant de regarder** : Tentez toujours de résoudre l'exercice par vous-même avant de consulter les indices.

2. **Consultez la documentation** : Habituez-vous à lire la Javadoc de `java.time`.

3. **Expérimentez** : Modifiez les solutions, ajoutez des fonctionnalités, cassez le code pour comprendre.

4. **Écrivez vos propres exercices** : Une fois à l'aise, inventez vos propres défis.

5. **Pratiquez régulièrement** : Faites au moins un exercice par jour pour bien assimiler.

---

**Bonne pratique !**