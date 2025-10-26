# Partie 3.3 : Fonctions Lambda et Utilitaires

## 🎯 Objectifs Pédagogiques

Ce chapitre explore les **fonctions lambda** et les **fonctions utilitaires** en Python. Les fonctions lambda permettent de créer des fonctions anonymes concises, très utiles avec les fonctions d'ordre supérieur.

### Concepts Abordés
- **Fonctions lambda** : syntaxe et applications
- **Fonctions d'ordre supérieur** : map, filter, sorted avec clés
- **Applications pratiques** : tri, recherche, transformation
- **Fonctions utilitaires** : fusion, extraction, formatage

---

## 📝 Exercices Pratiques

### Exercice 121 : Fonction lambda pour fusionner deux listes
**Objectif** : Créer une fonction qui fusionne deux listes.

```python
# Solution
fusionner_listes = lambda liste1, liste2: liste1 + liste2

# Tests
liste_a = [1, 2, 3]
liste_b = [4, 5, 6]
liste_c = ["a", "b"]
liste_d = ["c", "d", "e"]

resultats = [
    fusionner_listes(liste_a, liste_b),
    fusionner_listes(liste_c, liste_d),
    fusionner_listes([], [1, 2, 3]),
    fusionner_listes([1, 2], [])
]

print("Tests de fusion de listes :")
for i, resultat in enumerate(resultats):
    print(f"Fusion {i+1}: {resultat}")
```

**Explication** :
- **Lambda simple** : lambda paramètres: expression
- **Concaténation** : opérateur + pour les listes
- **Type générique** : fonctionne avec tous types de listes
- **Immutabilité** : nouvelle liste créée

**Test** : [1, 2, 3] + [4, 5, 6] = [1, 2, 3, 4, 5, 6].

---

### Exercice 122 : Fonction pour extraire une sous-liste
**Objectif** : Créer une fonction qui extrait une partie d'une liste.

```python
# Solution
extraire_sous_liste = lambda liste, debut, fin: liste[debut:fin]

# Tests
nombres = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]

extractions = [
    (0, 5),   # 5 premiers
    (5, 5),   # du 6ème au 10ème
    (2, 3),   # du 3ème au 5ème
    (0, 0),   # liste vide
]

print("Extractions de sous-listes :")
for i, (debut, longueur) in enumerate(extractions):
    sous_ensemble = extraire_sous_liste(nombres, debut, longueur)
    print(f"Extraction {i+1} (début={debut}, longueur={longueur}) : {sous_ensemble}")
```

**Explication** :
- **Slicing** : [début:fin] avec indices
- **Bornes** : début inclus, fin exclus
- **Cas limites** : gestion des indices invalides
- **Utilité** : extraction de parties de données

**Test** : [10, 20, 30, 40, 50] du début à 5.

---

### Exercice 123 : Fonction pour répéter une chaîne
**Objectif** : Créer une fonction qui répète une chaîne n fois.

```python
# Solution
repeter_chaine = lambda chaine, n: chaine * n

# Tests
tests_repetition = [
    ("Hello", 3),
    ("Hi", 5),
    ("*", 10),
    ("", 5),
    ("Test", 0)
]

print("Répétitions de chaînes :")
for chaine, n in tests_repetition:
    resultat = repeter_chaine(chaine, n)
    print(f"'{chaine}' × {n} = '{resultat}'")
```

**Explication** :
- **Opérateur * ** : répétition de chaînes
- **Multiplication** : nombre entier positif
- **Cas spéciaux** : n=0 → "", chaîne vide → ""
- **Applications** : bordures, séparateurs

**Test** : "Hello" × 3 = "HelloHelloHello".

---

### Exercice 124 : Fonction pour formater une chaîne
**Objectif** : Créer une fonction qui formate une chaîne avec des variables.

```python
# Solution
formater_chaine = lambda nom, age, ville: f"{nom} a {age} ans et habite {ville}"

# Tests
personnes = [
    ("Alice", 25, "Paris"),
    ("Bob", 30, "Lyon"),
    ("Charlie", 35, "Marseille")
]

print("Formatage de chaînes :")
for nom, age, ville in personnes:
    resultat = formater_chaine(nom, age, ville)
    print(resultat)
```

**Explication** :
- **f-string** : formatage moderne et lisible
- **Variables multiples** : insertion dans le texte
- **Applications** : messages personnalisés
- **Alternative** : .format() ou % formatting

**Test** : "Alice a 25 ans et habite Paris".

---

### Exercice 125 : Fonction pour vérifier un palindrome (lambda)
**Objectif** : Créer une fonction lambda qui vérifie si un mot est palindrome.

```python
# Solution
est_palindrome = lambda mot: mot.lower() == mot.lower()[::-1]

# Tests
mots_test = ["radar", "level", "python", "madam", "hello", "Aa"]
print("Tests de palindrome avec lambda :")
for mot in mots_test:
    resultat = est_palindrome(mot)
    print(f"'{mot}' est palindrome : {resultat}")
```

**Explication** :
- **Lambda conditionnel** : retourne booléen
- **Normalisation** : .lower() pour case insensitive
- **Inversion** : [::-1] technique classique
- **Conciseness** : une seule expression

**Test** : "radar" (oui), "level" (oui), "python" (non).

---

### Exercice 126 : Fonction pour calculer la moyenne d'une liste
**Objectif** : Créer une fonction qui calcule la moyenne d'une liste.

```python
# Solution
moyenne_liste = lambda nombres: sum(nombres) / len(nombres) if nombres else 0

# Tests
listes_test = [
    [1, 2, 3, 4, 5],
    [10, 20, 30, 40, 50],
    [2, 4, 6, 8],
    [],
    [100]
]

print("Calculs de moyenne :")
for i, liste in enumerate(listes_test):
    resultat = moyenne_liste(liste)
    print(f"Moyenne {i+1} : {resultat:.2f}")

# Comparaison avec fonction classique
def moyenne_classique(nombres):
    return sum(nombres) / len(nombres) if nombres else 0

print("\nComparaison lambda vs classique :")
for liste in listes_test:
    lambda_result = moyenne_liste(liste)
    classique_result = moyenne_classique(liste)
    print(f"Identique : {lambda_result == classique_result}")
```

**Explication** :
- **Division** : sum / len
- **Gestion liste vide** : condition if nombres else 0
- **Types** : fonctionne avec int et float
- **Précision** : division flottante automatique

**Test** : [1, 2, 3, 4, 5] → 3.00, [] → 0.

---

### Exercice 127 : Fonction pour calculer l'écart type d'une liste
**Objectif** : Créer une fonction qui calcule l'écart type d'une liste.

```python
# Solution
import math

ecart_type = lambda nombres: math.sqrt(
    sum((x - sum(nombres)/len(nombres))**2 for x in nombres) / len(nombres)
) if nombres else 0

# Tests
listes_test = [
    [1, 2, 3, 4, 5],
    [10, 10, 10, 10, 10],
    [5, 15, 25, 35, 45],
    []
]

print("Calculs d'écart type :")
for i, liste in enumerate(listes_test):
    resultat = ecart_type(liste)
    print(f"Écart type {i+1} : {resultat:.2f}")
```

**Explication** :
- **Formule** : σ = √(Σ(xi - μ)² / n)
- **Math.sqrt** : racine carrée
- **Compréhension** : calcul des écarts au carré
- **Statistiques** : mesure de dispersion

**Test** : [1, 2, 3, 4, 5] → 1.58, [10, 10, 10, 10, 10] → 0.00.

---

### Exercice 128 : Utilisation du module math pour racine carrée
**Objectif** : Utiliser le module math pour calculer des racines carrées.

```python
# Solution
import math

racine_carree = lambda nombre: math.sqrt(nombre) if nombre >= 0 else None

# Tests
nombres_test = [4, 9, 16, 25, 100, 0, -4, 0.25]
print("Racines carrées avec math.sqrt :")
for nombre in nombres_test:
    resultat = racine_carree(nombre)
    if resultat is not None:
        print(f"√{nombre} = {resultat:.2f}")
    else:
        print(f"√{nombre} = Impossible (nombre négatif)")
```

**Explication** :
- **Module math** : fonctions mathématiques avancées
- **Validation** : test de positivité
- **Précision** : math.sqrt plus précis que **0.5
- **Gestion d'erreurs** : nombres négatifs

**Test** : √4 = 2.00, √9 = 3.00, √100 = 10.00, √-4 = Impossible.

---

### Exercice 129 : Utilisation du module math pour puissance
**Objectif** : Utiliser math.pow pour calculer des puissances.

```python
# Solution
import math

puissance = lambda base, exposant: math.pow(base, exposant)

# Tests
calculs = [
    (2, 3),    # 2^3 = 8
    (5, 2),    # 5^2 = 25
    (10, 0),   # 10^0 = 1
    (4, 0.5),  # 4^0.5 = 2
    (2, -1),   # 2^-1 = 0.5
]

print("Calculs de puissance avec math.pow :")
for base, exp in calculs:
    resultat = puissance(base, exp)
    print(f"{base}^{exp} = {resultat:.2f}")
```

**Explication** :
- **math.pow** : puissance avec flottants
- **Exposants** : positifs, négatifs, fractionnaires
- **Précision** : calculs flottants précis
- **Applications** : mathématiques, physique

**Test** : 2^3 = 8.00, 5^2 = 25.00, 10^0 = 1.00, 4^0.5 = 2.00.

---

### Exercice 130 : Utilisation du module random pour tirage
**Objectif** : Utiliser le module random pour des tirages aléatoires.

```python
# Solution
import random

tirage_aleatoire = lambda minimum, maximum: random.randint(minimum, maximum)

# Tests
print("Tirages aléatoires :")
for i in range(10):
    nombre = tirage_aleatoire(1, 100)
    print(f"Tirage {i+1}: {nombre}")

# Jeu de devinette simple
nombre_secret = tirage_aleatoire(1, 20)
print(f"\nJe pense à un nombre entre 1 et 20...")
print(f"Indice : c'est {nombre_secret}")
```

**Explication** :
- **random.randint** : nombre entier aléatoire
- **Bornes incluses** : min et max inclus
- **Applications** : jeux, simulations, tests
- **Reproductibilité** : random.seed() pour des résultats fixes

**Test** : Nombres aléatoires entre 1 et 100.

---

## 🔍 Points Clés à Retenir

### 1. **Fonctions Lambda**
```python
# Syntaxe
lambda parametres: expression

# Exemples
double = lambda x: x * 2
addition = lambda x, y: x + y
est_positif = lambda x: x > 0
longueur = lambda chaine: len(chaine)

# Utilisation
resultat = double(5)  # 10
somme = addition(3, 4)  # 7
```

### 2. **Fonctions d'Ordre Supérieur**
```python
# map : applique une fonction à chaque élément
nombres = [1, 2, 3, 4, 5]
carres = list(map(lambda x: x**2, nombres))  # [1, 4, 9, 16, 25]

# filter : filtre selon une condition
pairs = list(filter(lambda x: x % 2 == 0, nombres))  # [2, 4]

# sorted avec clé
mots = ["banane", "pomme", "kiwi", "orange"]
tries_par_longueur = sorted(mots, key=lambda mot: len(mot))  # ["kiwi", "pomme", "banane"]
```

### 3. **Modules Utiles**
```python
# math : fonctions mathématiques
import math
sqrt(16)  # 4.0
pow(2, 3)  # 8.0
pi  # 3.14159...

# random : génération aléatoire
import random
randint(1, 10)  # Nombre entre 1 et 10
choice([1, 2, 3])  # Élément aléatoire
shuffle(liste)  # Mélange une liste

# datetime : dates et heures
from datetime import datetime
now = datetime.now()
print(now.year, now.month, now.day)
```

### 4. **Fonctions Built-in avec Lambda**
```python
# Tri avec clé personnalisée
etudiants = [
    {"nom": "Alice", "note": 15},
    {"nom": "Bob", "note": 12},
    {"nom": "Charlie", "note": 18}
]

# Tri par note décroissante
tries_par_note = sorted(etudiants, key=lambda e: e["note"], reverse=True)

# Tri par longueur de nom
tries_par_nom = sorted(etudiants, key=lambda e: len(e["nom"]))
```

## 💡 Optimisations et Astuces

### 1. **Lambda vs Fonctions Classiques**
```python
# Lambda : pour fonctions courtes et simples
filtre_pair = lambda x: x % 2 == 0

# Fonction classique : pour fonctions complexes
def filtrer_pairs(nombres):
    """Filtre les nombres pairs d'une liste"""
    return [x for x in nombres if x % 2 == 0]

# Quand utiliser lambda :
# - Avec map, filter, sorted
# - Fonctions courtes (1 ligne)
# - Fonctions anonymes temporaires
```

### 2. **Composition de Fonctions**
```python
# Composition de lambdas
double = lambda x: x * 2
carre = lambda x: x ** 2
double_carre = lambda x: carre(double(x))  # 2x puis x²

# Ou plus simplement :
double_carre_simple = lambda x: (x * 2) ** 2

# Test
for x in [1, 2, 3, 4]:
    print(f"{x} → double={double(x)} → double_carre={double_carre(x)}")
```

### 3. **Lambda Conditionnelles**
```python
# Lambda avec condition
valeur_absolue = lambda x: x if x >= 0 else -x
parite = lambda x: "pair" if x % 2 == 0 else "impair"
classification = lambda x: "positif" if x > 0 else "négatif" if x < 0 else "nul"

# Tests
test_nombres = [-5, -1, 0, 1, 5]
for nombre in test_nombres:
    print(f"{nombre}: abs={valeur_absolue(nombre)}, parité={parite(nombre)}, classification={classification(nombre)}")
```

## 🚀 Applications Pratiques

### 1. **Analyseur de Données**
```python
def analyser_donnees(nombres, operations):
    """Analyse des données avec plusieurs opérations"""
    resultats = {}

    # Opérations disponibles
    operateurs = {
        "somme": lambda x: sum(x),
        "moyenne": lambda x: sum(x) / len(x) if x else 0,
        "maximum": lambda x: max(x) if x else None,
        "minimum": lambda x: min(x) if x else None,
        "pairs": lambda x: list(filter(lambda n: n % 2 == 0, x)),
        "impairs": lambda x: list(filter(lambda n: n % 2 != 0, x)),
        "carres": lambda x: list(map(lambda n: n**2, x)),
        "doubles": lambda x: list(map(lambda n: n*2, x))
    }

    # Application des opérations demandées
    for operation in operations:
        if operation in operateurs:
            resultats[operation] = operateurs[operation](nombres)

    return resultats

# Test
donnees = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
operations = ["somme", "moyenne", "pairs", "carres", "doubles"]

analyse = analyser_donnees(donnees, operations)
for operation, resultat in analyse.items():
    print(f"{operation}: {resultat}")
```

### 2. **Formateur de Données**
```python
def formateur_donnees(elements, format_type="majuscules"):
    """Formate des éléments selon le type demandé"""
    formateurs = {
        "majuscules": lambda x: str(x).upper(),
        "minuscules": lambda x: str(x).lower(),
        "longueur": lambda x: len(str(x)),
        "type": lambda x: type(x).__name__,
        "arrondi": lambda x: round(float(x)) if isinstance(x, (int, float)) else str(x)
    }

    if format_type in formateurs:
        return [formateurs[format_type](element) for element in elements]
    else:
        return elements

# Tests
donnees_mixtes = ["Hello", "WORLD", 123, 45.67, True, None]
formats = ["majuscules", "minuscules", "longueur", "type"]

print("Formatage de données :")
for fmt in formats:
    resultat = formateur_donnees(donnees_mixtes, fmt)
    print(f"{fmt}: {resultat}")
```

### 3. **Générateur de Statistiques**
```python
def statistiques_avancees(donnees, **options):
    """Calcule des statistiques avancées"""
    stats = {}

    # Statistiques de base
    stats["n"] = len(donnees)
    stats["somme"] = sum(donnees)
    stats["moyenne"] = stats["somme"] / stats["n"] if stats["n"] > 0 else 0
    stats["max"] = max(donnees) if donnees else None
    stats["min"] = min(donnees) if donnees else None

    # Filtres conditionnels
    if options.get("pairs"):
        stats["pairs"] = list(filter(lambda x: x % 2 == 0, donnees))
    if options.get("impairs"):
        stats["impairs"] = list(filter(lambda x: x % 2 != 0, donnees))
    if options.get("positifs"):
        stats["positifs"] = list(filter(lambda x: x > 0, donnees))
    if options.get("negatifs"):
        stats["negatifs"] = list(filter(lambda x: x < 0, donnees))

    # Transformations
    if options.get("carres"):
        stats["carres"] = list(map(lambda x: x**2, donnees))
    if options.get("doubles"):
        stats["doubles"] = list(map(lambda x: x*2, donnees))

    # Tests de divisibilité
    for div in options.get("diviseurs", []):
        stats[f"divisibles_par_{div}"] = list(filter(lambda x: x % div == 0, donnees))

    return stats

# Test
donnees = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
options = {
    "pairs": True,
    "impairs": True,
    "carres": True,
    "doubles": True,
    "diviseurs": [2, 3, 5]
}

stats = statistiques_avancees(donnees, **options)
for cle, valeur in stats.items():
    print(f"{cle}: {valeur}")
```

## 🎯 Défis Supplémentaires

1. **Créez** une fonction lambda pour calculer la distance entre deux points
2. **Développez** une fonction pour trier une liste de dictionnaires par une clé
3. **Implémentez** une fonction lambda pour filtrer les nombres premiers
4. **Concevez** une fonction utilitaire pour convertir des unités de température

---

**Exercices complétés : 130/150** 🎯

*Continuez avec le [chapitre suivant](3-4-modules.md) pour l'utilisation des modules standard !*