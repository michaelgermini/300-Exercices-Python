# Partie 3.2 : Fonctions Avancées

## 🎯 Objectifs Pédagogiques

Ce chapitre explore les **fonctions avancées** en Python, incluant la **récursivité**, les **paramètres variables** et les **applications algorithmiques complexes**.

### Concepts Abordés
- **Récursivité** : fonctions qui s'appellent elles-mêmes
- **PGCD et PPCM** : algorithmes mathématiques
- **Paramètres variables** : *args et **kwargs
- **Applications** : nombres premiers, suites, calculs mathématiques

---

## 📝 Exercices Pratiques

### Exercice 111 : Factoriel récursif
**Objectif** : Implémenter le factoriel avec une fonction récursive.

```python
# Solution
def factoriel_recursif(n):
    """Calcule le factoriel de n par récursivité"""
    if n <= 1:
        return 1
    else:
        return n * factoriel_recursif(n - 1)

# Tests
for i in range(8):
    print(f"{i}! = {factoriel_recursif(i)}")

print(f"10! = {factoriel_recursif(10)}")
```

**Explication** :
- **Cas de base** : n ≤ 1 → 1
- **Cas récursif** : n × factoriel(n-1)
- **Pile d'appels** : s'empile jusqu'au cas de base
- **Déroulement** : se dépile avec les multiplications

**Test** : 0! = 1, 1! = 1, 5! = 120, 10! = 3,628,800.

---

### Exercice 112 : Fibonacci récursif
**Objectif** : Implémenter la suite de Fibonacci avec une fonction récursive.

```python
# Solution
def fibonacci_recursif(n):
    """Calcule le n-ième terme de Fibonacci par récursivité"""
    if n <= 0:
        return 0
    elif n == 1:
        return 1
    else:
        return fibonacci_recursif(n - 1) + fibonacci_recursif(n - 2)

# Tests
print("Suite de Fibonacci (récursive) :")
for i in range(12):
    print(f"F({i}) = {fibonacci_recursif(i)}")

# Version itérative pour comparaison
def fibonacci_iteratif(n):
    """Version itérative pour comparaison"""
    if n <= 0:
        return 0
    elif n == 1:
        return 1

    a, b = 0, 1
    for i in range(2, n + 1):
        a, b = b, a + b
    return b

print("\nComparaison récursif vs itératif :")
for i in range(10):
    rec = fibonacci_recursif(i)
    ite = fibonacci_iteratif(i)
    print(f"F({i}) : récursif={rec}, itératif={ite}, identique={rec == ite}")
```

**Explication** :
- **Cas de base** : F(0) = 0, F(1) = 1
- **Cas récursif** : F(n) = F(n-1) + F(n-2)
- **Complexité** : exponentielle (beaucoup d'appels redondants)
- **Alternative** : version itérative plus efficace

**Test** : F(0)=0, F(1)=1, F(2)=1, F(3)=2, F(4)=3, F(5)=5, F(6)=8, F(7)=13.

---

### Exercice 113 : PGCD (Plus Grand Commun Diviseur)
**Objectif** : Implémenter l'algorithme d'Euclide pour calculer le PGCD.

```python
# Solution
def pgcd(a, b):
    """Calcule le PGCD de a et b par l'algorithme d'Euclide"""
    while b != 0:
        a, b = b, a % b
    return a

# Tests
paires = [(48, 18), (100, 25), (17, 13), (60, 48), (7, 5)]
print("Calculs de PGCD :")
for a, b in paires:
    resultat = pgcd(a, b)
    print(f"PGCD({a}, {b}) = {resultat}")

# Vérification avec math.gcd
import math
print("\nVérification avec math.gcd :")
for a, b in paires:
    math_result = math.gcd(a, b)
    notre_result = pgcd(a, b)
    print(f"math.gcd({a}, {b}) = {math_result}, notre fonction = {notre_result}, identique = {math_result == notre_result}")
```

**Explication** :
- **Algorithme d'Euclide** : PGCD(a,b) = PGCD(b, a mod b)
- **Itération** : continue jusqu'à ce que b = 0
- **Efficacité** : O(log min(a,b))
- **Mathématiques** : propriété fondamentale

**Test** : PGCD(48, 18) = 6, PGCD(100, 25) = 25, PGCD(17, 13) = 1.

---

### Exercice 114 : PPCM (Plus Petit Commun Multiple)
**Objectif** : Calculer le PPCM de deux nombres.

```python
# Solution
def ppcm(a, b):
    """Calcule le PPCM de a et b"""
    # PPCM(a,b) = (a × b) / PGCD(a,b)
    return (a * b) // pgcd(a, b)

# Tests
paires = [(4, 6), (12, 18), (7, 11), (15, 25), (8, 12)]
print("Calculs de PPCM :")
for a, b in paires:
    resultat = ppcm(a, b)
    print(f"PPCM({a}, {b}) = {resultat}")

# Vérification manuelle
print("\nVérifications manuelles :")
for a, b in [(4, 6), (12, 18)]:
    manuellement = (a * b) // pgcd(a, b)
    notre_fonction = ppcm(a, b)
    print(f"PPCM({a}, {b}) : manuel={manuellement}, fonction={notre_fonction}, identique={manuellement == notre_fonction}")
```

**Explication** :
- **Formule** : PPCM(a,b) = (a × b) / PGCD(a,b)
- **Division entière** : // pour éviter les flottants
- **Relation** : PPCM × PGCD = a × b
- **Applications** : fractions, rythmes, cycles

**Test** : PPCM(4, 6) = 12, PPCM(12, 18) = 36, PPCM(7, 11) = 77.

---

### Exercice 115 : Fonction lambda double
**Objectif** : Créer une fonction lambda qui double un nombre.

```python
# Solution
double = lambda x: x * 2

# Tests
nombres = [1, 2, 3, 4, 5, 10, 100]
print("Doublage avec fonction lambda :")
for nombre in nombres:
    resultat = double(nombre)
    print(f"Double de {nombre} = {resultat}")

# Comparaison avec fonction classique
def double_classique(x):
    return x * 2

print("\nComparaison lambda vs fonction classique :")
for nombre in [5, 10, 15]:
    lambda_result = double(nombre)
    classique_result = double_classique(nombre)
    print(f"double({nombre}) : lambda={lambda_result}, classique={classique_result}, identique={lambda_result == classique_result}")
```

**Explication** :
- **Syntaxe lambda** : lambda paramètres: expression
- **Fonction anonyme** : sans nom, définie en ligne
- **Usage** : pour des fonctions simples, courtes
- **Équivalence** : même résultat qu'une fonction classique

**Test** : 5 → 10, 10 → 20, 100 → 200.

---

### Exercice 116 : Fonction lambda triple
**Objectif** : Créer une fonction lambda qui triple un nombre.

```python
# Solution
triple = lambda x: x * 3

# Tests
nombres = [1, 2, 3, 4, 5]
print("Triplage avec fonction lambda :")
for nombre in nombres:
    resultat = triple(nombre)
    print(f"Triple de {nombre} = {resultat}")

# Utilisation directe
print("\nUtilisation directe :")
print(f"5 × 3 = {(lambda x: x * 3)(5)}")
print(f"10 × 3 = {(lambda x: x * 3)(10)}")
```

**Explication** :
- **Extension** : même pattern que le double
- **Multiplication par 3** : lambda x: x * 3
- **Utilisation directe** : lambda sans affectation
- **Conciseness** : code très compact

**Test** : 1 → 3, 2 → 6, 3 → 9, 4 → 12, 5 → 15.

---

### Exercice 117 : Fonction inverser chaîne
**Objectif** : Créer une fonction qui inverse une chaîne de caractères.

```python
# Solution
def inverser_chaine(chaine):
    """Inverse une chaîne de caractères"""
    return chaine[::-1]

# Tests
chaines_test = ["Python", "Hello", "radar", "12345", ""]
print("Inversion de chaînes :")
for chaine in chaines_test:
    resultat = inverser_chaine(chaine)
    print(f"'{chaine}' → '{resultat}'")

# Test palindrome avec inversion
mots = ["radar", "level", "python", "madam"]
print("\nTests de palindrome avec inversion :")
for mot in mots:
    inverse = inverser_chaine(mot)
    est_palindrome = mot == inverse
    print(f"'{mot}' est palindrome : {est_palindrome}")
```

**Explication** :
- **Slicing** : [::-1] technique d'inversion
- **Immutabilité** : nouvelle chaîne créée
- **Application** : palindromes, cryptographie
- **Efficacité** : méthode Python optimisée

**Test** : "Python" → "nohtyP", "radar" → "radar" (palindrome).

---

### Exercice 118 : Compteur de voyelles (fonction)
**Objectif** : Créer une fonction qui compte les voyelles d'une chaîne.

```python
# Solution
def compter_voyelles(chaine):
    """Compte le nombre de voyelles dans une chaîne"""
    voyelles = "aeiouAEIOU"
    compteur = 0

    for caractere in chaine:
        if caractere in voyelles:
            compteur += 1

    return compteur

# Tests
textes = ["Hello World", "Python", "AEIOU", "bcdfgh", "La vie est belle"]
print("Comptage de voyelles :")
for texte in textes:
    nb_voyelles = compter_voyelles(texte)
    print(f"'{texte}' contient {nb_voyelles} voyelles")
```

**Explication** :
- **Chaîne de référence** : "aeiouAEIOU"
- **Test d'appartenance** : in pour chaque caractère
- **Accumulation** : compteur += 1
- **Case sensitive** : gère majuscules et minuscules

**Test** : "Hello World" → 3, "Python" → 1, "AEIOU" → 5, "bcdfgh" → 0.

---

### Exercice 119 : Compteur de consonnes (fonction)
**Objectif** : Créer une fonction qui compte les consonnes d'une chaîne.

```python
# Solution
def compter_consonnes(chaine):
    """Compte le nombre de consonnes dans une chaîne"""
    voyelles = "aeiouAEIOU"
    consonnes = 0

    for caractere in chaine:
        if caractere.isalpha() and caractere not in voyelles:
            consonnes += 1

    return consonnes

# Tests
textes = ["Hello World", "Python", "AEIOU", "bcdfgh", "123 !?"]
print("Comptage de consonnes :")
for texte in textes:
    nb_consonnes = compter_consonnes(texte)
    print(f"'{texte}' contient {nb_consonnes} consonnes")
```

**Explication** :
- **Filtrage** : .isalpha() pour les lettres uniquement
- **Exclusion** : not in voyelles
- **Précision** : ne compte que les caractères alphabétiques
- **Complément** : tout ce qui n'est pas une voyelle

**Test** : "Hello World" → 7, "Python" → 5, "AEIOU" → 0, "bcdfgh" → 6.

---

### Exercice 120 : Tri d'une liste (fonction)
**Objectif** : Créer une fonction qui trie une liste.

```python
# Solution
def trier_liste(liste):
    """Trie une liste par ordre croissant"""
    return sorted(liste)

# Tests
listes_test = [
    [64, 34, 25, 12, 22, 11, 90],
    [3, 1, 4, 1, 5],
    ["banane", "pomme", "orange", "kiwi"],
    []
]

print("Tests de tri :")
for i, liste in enumerate(listes_test):
    triee = trier_liste(liste)
    print(f"Liste {i+1} : {liste} → {triee}")

# Test avec tri en place
print("\nTri en place (modifie l'original) :")
liste_originale = [3, 1, 4, 1, 5]
print(f"Avant : {liste_originale}")
liste_originale.sort()
print(f"Après : {liste_originale}")
```

**Explication** :
- **sorted()** : retourne nouvelle liste triée
- **.sort()** : trie en place (modifie l'original)
- **Types** : fonctionne avec nombres, chaînes, etc.
- **Ordre naturel** : numérique ou alphabétique

**Test** : [64, 34, 25, 12, 22, 11, 90] → [11, 12, 22, 25, 34, 64, 90].

---

## 🔍 Points Clés à Retenir

### 1. **Récursivité**
```python
# Structure récursive
def fonction_recursive(n):
    if condition_arret:  # Cas de base
        return valeur_base
    else:  # Cas récursif
        return operation + fonction_recursive(n-1)

# Exemple : factoriel
def factoriel(n):
    if n <= 1:
        return 1
    return n * factoriel(n-1)
```

### 2. **Arguments Variables**
```python
# *args : arguments positionnels variables
def somme_tout(*args):
    return sum(args)

# **kwargs : arguments nommés variables
def afficher_infos(**kwargs):
    for cle, valeur in kwargs.items():
        print(f"{cle}: {valeur}")

# Utilisation
print(somme_tout(1, 2, 3, 4, 5))  # 15
afficher_infos(nom="Alice", age=25, ville="Paris")
```

### 3. **Fonctions Lambda**
```python
# Syntaxe
fonction = lambda parametres: expression

# Exemples
carre = lambda x: x**2
addition = lambda x, y: x + y
est_pair = lambda x: x % 2 == 0

# Utilisation avec map, filter
nombres = [1, 2, 3, 4, 5]
carres = list(map(lambda x: x**2, nombres))  # [1, 4, 9, 16, 25]
pairs = list(filter(lambda x: x % 2 == 0, nombres))  # [2, 4]
```

### 4. **Documentation et Tests**
```python
def ma_fonction(param1, param2="defaut"):
    """
    Description de la fonction

    Args:
        param1 (type): description
        param2 (type, optional): description

    Returns:
        type: description du retour

    Raises:
        TypeError: si param1 n'est pas du bon type
    """
    # Code de la fonction
    pass
```

## 💡 Optimisations et Astuces

### 1. **Récursivité vs Itération**
```python
# Récursif (plus élégant mais limité par la pile)
def fibonacci_rec(n):
    if n <= 1:
        return n
    return fibonacci_rec(n-1) + fibonacci_rec(n-2)

# Itératif (plus efficace pour les grandes valeurs)
def fibonacci_ite(n):
    if n <= 1:
        return n
    a, b = 0, 1
    for i in range(2, n+1):
        a, b = b, a + b
    return b
```

### 2. **Memoization (Cache)**
```python
# Cache pour éviter les recalculs
memo = {}

def fibonacci_memo(n):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n

    memo[n] = fibonacci_memo(n-1) + fibonacci_memo(n-2)
    return memo[n]
```

### 3. **Fonctions d'Ordre Supérieur**
```python
# map : applique une fonction à chaque élément
carres = list(map(lambda x: x**2, nombres))

# filter : filtre selon une condition
pairs = list(filter(lambda x: x % 2 == 0, nombres))

# reduce : combine tous les éléments
from functools import reduce
produit = reduce(lambda x, y: x * y, nombres)
```

## 🚀 Applications Pratiques

### 1. **Calculateur Mathématique**
```python
def calculateur_math(operations, *nombres):
    """Effectue plusieurs opérations sur des nombres"""
    resultats = {}

    if "somme" in operations:
        resultats["somme"] = sum(nombres)
    if "produit" in operations:
        resultats["produit"] = reduce(lambda x, y: x * y, nombres, 1)
    if "moyenne" in operations:
        resultats["moyenne"] = sum(nombres) / len(nombres)
    if "maximum" in operations:
        resultats["maximum"] = max(nombres)
    if "minimum" in operations:
        resultats["minimum"] = min(nombres)

    return resultats

# Test
resultats = calculateur_math(["somme", "moyenne", "maximum"], 10, 20, 30, 40, 50)
for operation, resultat in resultats.items():
    print(f"{operation}: {resultat}")
```

### 2. **Analyseur de Texte**
```python
def analyser_texte(texte, **options):
    """Analyse un texte selon les options"""
    resultat = {}

    # Options par défaut
    analyser_voyelles = options.get("voyelles", True)
    analyser_consonnes = options.get("consonnes", True)
    analyser_longueur = options.get("longueur", True)
    analyser_mots = options.get("mots", True)

    if analyser_longueur:
        resultat["longueur"] = len(texte)
        resultat["longueur_sans_espaces"] = len(texte.replace(" ", ""))

    if analyser_voyelles or analyser_consonnes:
        voyelles = "aeiouAEIOU"
        nb_voyelles = sum(1 for c in texte if c in voyelles)
        nb_consonnes = sum(1 for c in texte if c.isalpha() and c not in voyelles)

        if analyser_voyelles:
            resultat["voyelles"] = nb_voyelles
        if analyser_consonnes:
            resultat["consonnes"] = nb_consonnes

    if analyser_mots:
        mots = texte.split()
        resultat["nombre_mots"] = len(mots)
        resultat["mots_longs"] = [mot for mot in mots if len(mot) > 5]

    return resultat

# Test
texte = "Le Python est un excellent langage de programmation"
analyse = analyser_texte(texte, voyelles=True, consonnes=True, longueur=True, mots=True)
for cle, valeur in analyse.items():
    print(f"{cle}: {valeur}")
```

### 3. **Générateur de Séquences**
```python
def generer_sequence(type_seq, n, **params):
    """Génère différents types de séquences"""
    if type_seq == "fibonacci":
        return [fibonacci_iteratif(i) for i in range(n)]

    elif type_seq == "factoriels":
        return [factoriel_recursif(i) for i in range(n)]

    elif type_seq == "carres":
        return [i**2 for i in range(1, n+1)]

    elif type_seq == "cubes":
        return [i**3 for i in range(1, n+1)]

    elif type_seq == "premiers":
        # Nombres premiers jusqu'à n (simplifié)
        premiers = []
        for i in range(2, n+1):
            if all(i % j != 0 for j in range(2, int(i**0.5)+1)):
                premiers.append(i)
        return premiers

    else:
        return []

# Tests
print("Fibonacci 10 premiers:", generer_sequence("fibonacci", 10))
print("Carrés 1 à 10:", generer_sequence("carres", 10))
print("Primes jusqu'à 20:", generer_sequence("premiers", 20))
```

## 🎯 Défis Supplémentaires

1. **Implémentez** une fonction récursive pour la puissance (a^b)
2. **Créez** une fonction pour calculer la somme des chiffres d'un nombre
3. **Développez** une fonction de tri personnalisé (par longueur de chaîne)
4. **Concevez** une fonction pour générer des permutations d'une liste

---

**Exercices complétés : 120/150** 🎯

*Continuez avec le [chapitre suivant](3-3-lambda.md) pour les fonctions lambda avancées !*