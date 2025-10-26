# Partie 1.5 : Applications Pratiques

## 🎯 Objectifs Pédagogiques

Ce chapitre final de la Partie 1 met en pratique **tous les concepts** abordés précédemment. Nous allons créer des applications concrètes qui combinent types de données, opérations, entrées/sorties et manipulations de chaînes.

### Concepts Intégrés
- **Applications du quotidien** : IMC, conversions, calculs financiers
- **Logique conditionnelle** : tests multiples et validations
- **Manipulation de données** : traitement et formatage
- **Interaction utilisateur** : programmes complets et conviviaux

---

## 📝 Exercices Pratiques

### Exercice 41 : Double d'un nombre
**Objectif** : Calculer le double d'un nombre saisi.

```python
# Solution simple
nombre = float(input("Entrez un nombre : "))
double = nombre * 2
print(f"Le double de {nombre} est {double}")
```

**Explication** :
- **Multiplication par 2** : opération de base
- **Application** : augmentation, croissance, échelle
- **Généralisation** : base pour les pourcentages

**Test** : 5 → 10, -3 → -6, 2.5 → 5.0.

---

### Exercice 42 : Triple d'un nombre
**Objectif** : Calculer le triple d'un nombre.

```python
# Solution
nombre = float(input("Entrez un nombre : "))
triple = nombre * 3
print(f"Le triple de {nombre} est {triple}")
```

**Explication** :
- **Pattern** : extension du concept de double
- **Mathématiques** : multiplication par 3
- **Applications** : volumes, concentrations, dosages

**Test** : 4 → 12, 1.5 → 4.5, -2 → -6.

---

### Exercice 43 : Affichage lettre par lettre
**Objectif** : Afficher chaque lettre d'un mot sur une ligne séparée.

```python
# Solution
mot = input("Entrez un mot : ")
print("Lettres du mot :")
for lettre in mot:
    print(lettre)
```

**Explication** :
- **Itération sur chaîne** : chaque caractère accessible
- **Boucle implicite** : `for lettre in mot`
- **Affichage vertical** : une lettre par ligne

**Test** : "CHAT" → C H A T (un par ligne).

---

### Exercice 44 : Compteur de voyelles
**Objectif** : Compter le nombre de voyelles dans une chaîne.

```python
# Solution
chaine = input("Entrez une chaîne : ").lower()
voyelles = "aeiou"
compteur = 0

for caractere in chaine:
    if caractere in voyelles:
        compteur += 1

print(f"Nombre de voyelles : {compteur}")
```

**Explication** :
- **Chaîne de référence** : "aeiou" pour les voyelles
- **Test d'appartenance** : `in` pour vérifier
- **Compteur** : accumulation des occurrences
- **Case insensitive** : conversion en minuscules

**Test** : "Python" → 1 (o), "Hello World" → 3 (e,o,o).

---

### Exercice 45 : Compteur de consonnes
**Objectif** : Compter les consonnes (lettres non-voyelles).

```python
# Solution
chaine = input("Entrez une chaîne : ").lower()
voyelles = "aeiou"
consonnes = 0

for caractere in chaine:
    if caractere.isalpha() and caractere not in voyelles:
        consonnes += 1

print(f"Nombre de consonnes : {consonnes}")
```

**Explication** :
- `.isalpha()` : vérifie si c'est une lettre
- **Exclusion** : lettres ET pas des voyelles
- **Précision** : ne compte que les caractères alphabétiques

**Test** : "Python" → 5 (P,y,t,h,n), "Hello" → 3 (H,l,l).

---

### Exercice 46 : Test de plage
**Objectif** : Vérifier si un nombre est dans une plage donnée.

```python
# Solution
nombre = float(input("Entrez un nombre : "))
min_plage = float(input("Minimum de la plage : "))
max_plage = float(input("Maximum de la plage : "))

if min_plage <= nombre <= max_plage:
    print(f"{nombre} est dans la plage [{min_plage}, {max_plage}]")
else:
    print(f"{nombre} n'est pas dans la plage [{min_plage}, {max_plage}]")
```

**Explication** :
- **Opérateur en cascade** : `min <= nombre <= max`
- **Bornes incluses** : <= pour les deux bornes
- **Test d'intervalle** : application courante

**Test** : 5 dans [1, 10] (oui), 15 dans [1, 10] (non).

---

### Exercice 47 : Affichage des éléments d'une liste
**Objectif** : Afficher tous les éléments d'une liste saisie.

```python
# Solution
elements = input("Entrez des éléments (séparés par des virgules) : ")
liste = elements.split(",")
print("Éléments de la liste :")
for element in liste:
    print(f"- {element.strip()}")
```

**Explication** :
- `.split(",")` : division en liste sur les virgules
- `.strip()` : suppression des espaces autour
- **Format d'entrée** : "pomme, banane, orange"
- **Affichage formaté** : puces pour la lisibilité

**Test** : "1, 2, 3" → affiche - 1, - 2, - 3.

---

### Exercice 48 : Longueur d'une liste
**Objectif** : Afficher la longueur d'une liste saisie.

```python
# Solution
elements = input("Entrez des éléments (séparés par des espaces) : ")
liste = elements.split()
longueur = len(liste)
print(f"La liste contient {longueur} éléments")
print(f"Éléments : {liste}")
```

**Explication** :
- `.split()` : division par défaut sur les espaces
- `len()` : longueur de la liste
- **Format flexible** : accepte espaces multiples

**Test** : "un deux trois" → 3 éléments.

---

### Exercice 49 : Ajout à une liste
**Objectif** : Ajouter un élément à une liste existante.

```python
# Solution
# Création de la liste initiale
liste = ["Python", "Java", "C++"]
print(f"Liste initiale : {liste}")

# Ajout d'un élément
nouvel_element = input("Nouvel élément à ajouter : ")
liste.append(nouvel_element)
print(f"Liste après ajout : {liste}")
```

**Explication** :
- **Méthode `.append()`** : ajout en fin de liste
- **Modification en place** : les listes sont mutables
- **Persistance** : la liste garde ses modifications

**Test** : ["Python", "Java", "C++"] + "JavaScript" → ["Python", "Java", "C++", "JavaScript"].

---

### Exercice 50 : Synthèse complète
**Objectif** : Créer une application complète combinant tous les concepts de la Partie 1.

```python
# Solution - Application de calculatrice personnelle
print("=== CALCULATRICE PERSONNELLE ===")

# Informations personnelles
nom = input("Votre nom : ").strip().title()
age = int(input("Votre âge : "))
taille = float(input("Votre taille (m) : "))
poids = float(input("Votre poids (kg) : "))

# Calculs
imc = poids / (taille ** 2)
annee_naissance = 2024 - age  # Année courante
double_age = age * 2
moitie_poids = poids / 2

# Formatage du nom
initiales = nom.split()
sigle = ".".join(mot[0] for mot in initiales) + "."

print(f"\n=== RÉSULTATS POUR {nom.upper()} ===")
print(f"Sigle : {sigle}")
print(f"Âge : {age} ans (né(e) vers {annee_naissance})")
print(f"Taille : {taille} m")
print(f"Poids : {poids} kg")
print(f"IMC : {imc:.1f}")
print(f"Double de votre âge : {double_age} ans")
print(f"Moitié de votre poids : {moitie_poids} kg")

# Interprétation IMC
if imc < 18.5:
    interpretation = "Insuffisance pondérale"
elif imc < 25:
    interpretation = "Poids normal"
elif imc < 30:
    interpretation = "Surpoids"
else:
    interpretation = "Obésité"

print(f"Interprétation IMC : {interpretation}")
print(f"\nMerci {nom} !")
```

**Explication** :
- **Application intégrée** : combine tous les concepts de la Partie 1
- **Interface utilisateur** : titre, sections, formatage
- **Calculs variés** : arithmétique, conditions, chaînes
- **UX** : messages personnalisés et résultats structurés

**Test** : Saisissez vos informations personnelles pour voir tous les calculs.

---

## 🔍 Points Clés à Retenir

### 1. **Intégration des Concepts**
- **Types de données** : mélange int, float, str, bool
- **Opérations** : arithmétiques, logiques, sur chaînes
- **Structures** : conditions, boucles, listes
- **Interaction** : saisie, formatage, affichage

### 2. **Applications Réelles**
- **Santé** : calcul d'IMC et interprétation
- **Données personnelles** : formatage et calculs
- **Interface utilisateur** : programmes conviviaux
- **Validation** : tests et vérifications

### 3. **Bonnes Pratiques**
- **Noms de variables** : explicites et en anglais
- **Commentaires** : pour la compréhension
- **Formatage** : f-strings pour la lisibilité
- **Structure** : organisation logique du code

## 💡 Optimisations et Extensions

### 1. **Fonctions Utilitaires**
```python
def calculer_imc(poids, taille):
    """Calcule l'IMC et retourne interprétation"""
    imc = poids / (taille ** 2)
    if imc < 18.5:
        return imc, "Insuffisance pondérale"
    elif imc < 25:
        return imc, "Poids normal"
    elif imc < 30:
        return imc, "Surpoids"
    else:
        return imc, "Obésité"
```

### 2. **Validation des Saisies**
```python
def saisir_nombre_positif(message):
    """Demande un nombre positif avec validation"""
    while True:
        try:
            nombre = float(input(message))
            if nombre > 0:
                return nombre
            else:
                print("Veuillez entrer un nombre positif.")
        except ValueError:
            print("Veuillez entrer un nombre valide.")
```

### 3. **Formatage Avancé**
```python
def formater_resultats(nom, resultats):
    """Formate les résultats dans un cadre"""
    largeur = 40
    print("=" * largeur)
    print(f"{nom.center(largeur)}")
    print("=" * largeur)
    for cle, valeur in resultats.items():
        print(f"{cle:<20}: {valeur:>15}")
    print("=" * largeur)
```

## 🚀 Projets d'Extension

### 1. **Convertisseur Universel**
- Températures (C/F/K)
- Devises (multiples)
- Unités (longueur, poids, volume)
- Historique des conversions

### 2. **Analyseur de Texte**
- Comptage de caractères, mots, phrases
- Analyse de fréquences
- Recherche de motifs
- Statistiques textuelles

### 3. **Calculateur Financier**
- Intérêts simples/composés
- Amortissement de prêt
- Budget mensuel
- Objectifs d'épargne

## 🎯 Bilan de la Partie 1

### Concepts Maîtrisés
✅ **Types de données** : int, float, str, bool
✅ **Opérations arithmétiques** : +, -, *, /, %, **, //
✅ **Conditions** : if/elif/else, opérateurs logiques
✅ **Boucles** : for, range(), itération
✅ **Chaînes** : manipulation, slicing, méthodes
✅ **Listes** : création, modification, parcours
✅ **Interaction** : input(), print(), formatage

### Compétences Développées
- **Analyse de problèmes** : décomposition en étapes
- **Logique algorithmique** : conditions et boucles
- **Manipulation de données** : traitement et transformation
- **Interface utilisateur** : saisie et affichage
- **Validation** : tests et vérifications

---

**🏁 FIN DE LA PARTIE 1 - BRAVO !**

**Exercices complétés : 50/50** 🎯

*Félicitations ! Vous avez terminé les bases de Python. Continuez avec la [Partie 2](Partie%202%20-%20Controle%20flux/2-1-conditions.md) pour explorer le contrôle de flux !*