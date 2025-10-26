# Partie 3.1 : Fonctions de Base

## 🎯 Objectifs Pédagogiques

Ce chapitre explore les **fonctions de base** en Python, éléments essentiels pour **structurer et réutiliser le code**. Les fonctions permettent de découper les programmes en modules logiques et réutilisables.

### Concepts Abordés
- **Définition et appel** : création et utilisation de fonctions
- **Paramètres et arguments** : passage de valeurs
- **Valeurs de retour** : return et résultats
- **Applications mathématiques** : calculs, conversions, vérifications

---

## 📝 Exercices Pratiques

### Exercice 101 : Fonction carré
**Objectif** : Créer une fonction qui calcule le carré d'un nombre.

```python
# Solution
def carre(nombre):
    """Calcule le carré d'un nombre"""
    return nombre ** 2

# Test de la fonction
resultat = carre(5)
print(f"Le carré de 5 est {resultat}")

# Tests multiples
for i in range(1, 6):
    print(f"{i}² = {carre(i)}")
```

**Explication** :
- **def** : mot-clé pour définir une fonction
- **Paramètre** : nombre (variable d'entrée)
- **return** : valeur renvoyée par la fonction
- **Docstring** : documentation avec """

**Test** : 5² = 25, 3² = 9, 0² = 0, (-2)² = 4.

---

### Exercice 102 : Test de palindrome
**Objectif** : Créer une fonction qui vérifie si un nombre est palindrome.

```python
# Solution
def est_palindrome(nombre):
    """Vérifie si un nombre est palindrome"""
    nombre_str = str(nombre)
    return nombre_str == nombre_str[::-1]

# Tests
test_nombres = [121, 123, 3443, 12321, 12345]
for nombre in test_nombres:
    resultat = est_palindrome(nombre)
    print(f"{nombre} est palindrome : {resultat}")
```

**Explication** :
- **Conversion string** : str() pour manipuler les chiffres
- **Inversion** : [::-1] technique de slicing
- **Comparaison** : originale vs inversée
- **Application** : nombres qui se lisent dans les deux sens

**Test** : 121 (oui), 123 (non), 3443 (oui), 12321 (oui), 12345 (non).

---

### Exercice 103 : Jeu de devinette
**Objectif** : Créer une fonction pour un jeu de devinette avec nombre aléatoire.

```python
# Solution
import random

def jeu_devinette():
    """Jeu de devinette avec nombre aléatoire"""
    nombre_secret = random.randint(1, 100)
    tentatives = 0

    print("=== JEU DE DEVINETTE ===")
    print("Trouvez le nombre entre 1 et 100")

    while True:
        tentatives += 1
        try:
            guess = int(input(f"Tentative {tentatives} : "))
        except ValueError:
            print("Veuillez entrer un nombre entier")
            continue

        if guess < nombre_secret:
            print("Trop petit !")
        elif guess > nombre_secret:
            print("Trop grand !")
        else:
            print(f"Bravo ! Trouvé en {tentatives} tentatives")
            break

# Lancement du jeu
jeu_devinette()
```

**Explication** :
- **Module random** : génération de nombres aléatoires
- **Boucle while** : continue jusqu'à la solution
- **Gestion d'erreurs** : try/except pour la saisie
- **Feedback** : indications "plus grand" ou "plus petit"

**Test** : Lancez le jeu et essayez de trouver le nombre secret.

---

### Exercice 104 : Fonction factoriel
**Objectif** : Créer une fonction qui calcule le factoriel d'un nombre.

```python
# Solution
def factoriel(n):
    """Calcule le factoriel de n (n!)"""
    if n < 0:
        return "Erreur : nombre négatif"
    elif n == 0 or n == 1:
        return 1
    else:
        resultat = 1
        for i in range(2, n + 1):
            resultat *= i
        return resultat

# Tests
for i in range(6):
    print(f"{i}! = {factoriel(i)}")

print(f"10! = {factoriel(10)}")
print(f"(-5)! = {factoriel(-5)}")
```

**Explication** :
- **Cas de base** : 0! = 1! = 1
- **Boucle** : multiplication de 2 à n
- **Validation** : gestion des nombres négatifs
- **Mathématiques** : n! = n × (n-1) × ... × 1

**Test** : 0! = 1, 1! = 1, 5! = 120, 10! = 3,628,800.

---

### Exercice 105 : Somme d'une liste (fonction)
**Objectif** : Créer une fonction qui calcule la somme d'une liste.

```python
# Solution
def somme_liste(nombres):
    """Calcule la somme des éléments d'une liste"""
    total = 0
    for nombre in nombres:
        total += nombre
    return total

# Tests
liste1 = [1, 2, 3, 4, 5]
liste2 = [10, -5, 3, 8]
liste3 = []

print(f"Somme de {liste1} = {somme_liste(liste1)}")
print(f"Somme de {liste2} = {somme_liste(liste2)}")
print(f"Somme de {liste3} = {somme_liste(liste3)}")

# Comparaison avec built-in
print(f"Built-in sum : {sum(liste1)}")
print(f"Nos résultats sont identiques : {somme_liste(liste1) == sum(liste1)}")
```

**Explication** :
- **Accumulation** : addition successive des éléments
- **Gestion liste vide** : retourne 0
- **Alternative** : built-in sum() plus efficace
- **Pédagogie** : compréhension de l'algorithme

**Test** : [1, 2, 3, 4, 5] = 15, [10, -5, 3, 8] = 16, [] = 0.

---

### Exercice 106 : Produit d'une liste (fonction)
**Objectif** : Créer une fonction qui calcule le produit des éléments d'une liste.

```python
# Solution
def produit_liste(nombres):
    """Calcule le produit des éléments d'une liste"""
    produit = 1
    for nombre in nombres:
        produit *= nombre
    return produit

# Tests
liste1 = [1, 2, 3, 4, 5]
liste2 = [2, 5, 10]
liste3 = [0, 1, 2, 3]

print(f"Produit de {liste1} = {produit_liste(liste1)}")
print(f"Produit de {liste2} = {produit_liste(liste2)}")
print(f"Produit de {liste3} = {produit_liste(liste3)}")

# Comparaison avec reduce
from functools import reduce
import operator
print(f"Avec reduce : {reduce(operator.mul, liste1, 1)}")
```

**Explication** :
- **Initialisation** : produit = 1 (élément neutre)
- **Multiplication successive** : *= pour accumuler
- **Cas zéro** : produit = 0 si un élément est 0
- **Alternative** : reduce avec operator.mul

**Test** : [1, 2, 3, 4, 5] = 120, [2, 5, 10] = 100, [0, 1, 2, 3] = 0.

---

### Exercice 107 : Conversion km en miles (fonction)
**Objectif** : Créer une fonction pour convertir des km en miles.

```python
# Solution
def km_vers_miles(kilometres):
    """Convertit des kilomètres en miles"""
    miles = kilometres * 0.621371
    return round(miles, 2)

# Tests
distances_km = [1, 5, 10, 42.195, 100, 1000]
print("Conversions km → miles :")
for km in distances_km:
    miles = km_vers_miles(km)
    print(f"{km} km = {miles} miles")

# Test avec saisie utilisateur
km_utilisateur = float(input("Entrez une distance en km : "))
miles_utilisateur = km_vers_miles(km_utilisateur)
print(f"{km_utilisateur} km = {miles_utilisateur} miles")
```

**Explication** :
- **Facteur de conversion** : 1 km = 0.621371 miles
- **Arrondi** : round(miles, 2) pour 2 décimales
- **Applications** : géographie, sport, voyages
- **Précision** : arrondi pour la lisibilité

**Test** : 1 km = 0.62 miles, 10 km = 6.21 miles, 42.195 km (marathon) = 26.22 miles.

---

### Exercice 108 : Conversion Celsius en Fahrenheit (fonction)
**Objectif** : Créer une fonction pour convertir Celsius en Fahrenheit.

```python
# Solution
def celsius_vers_fahrenheit(celsius):
    """Convertit Celsius en Fahrenheit"""
    fahrenheit = (celsius * 9/5) + 32
    return fahrenheit

# Tests
temperatures_c = [-40, 0, 20, 37, 100]
print("Conversions °C → °F :")
for c in temperatures_c:
    f = celsius_vers_fahrenheit(c)
    print(f"{c}°C = {f}°F")

# Points de référence
print(f"Eau gèle : {celsius_vers_fahrenheit(0)}°F")
print(f"Eau bout : {celsius_vers_fahrenheit(100)}°F")
print(f"Corps humain : {celsius_vers_fahrenheit(37)}°F")
```

**Explication** :
- **Formule** : F = (C × 9/5) + 32
- **Points remarquables** : 0°C = 32°F, 100°C = 212°F
- **Applications** : météorologie, physique, cuisine
- **Précision** : calcul exact en flottants

**Test** : -40°C = -40°F, 0°C = 32°F, 20°C = 68°F, 37°C = 98.6°F, 100°C = 212°F.

---

### Exercice 109 : Test nombre premier (fonction)
**Objectif** : Créer une fonction qui vérifie si un nombre est premier.

```python
# Solution
def est_premier(n):
    """Vérifie si un nombre est premier"""
    if n <= 1:
        return False
    if n <= 3:
        return True
    if n % 2 == 0 or n % 3 == 0:
        return False

    # Test de divisibilité jusqu'à √n
    i = 5
    while i * i <= n:
        if n % i == 0 or n % (i + 2) == 0:
            return False
        i += 6

    return True

# Tests
nombres_test = [1, 2, 3, 4, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 97, 100]
print("Tests de primalité :")
for nombre in nombres_test:
    resultat = est_premier(nombre)
    print(f"{nombre} est premier : {resultat}")
```

**Explication** :
- **Optimisation** : test jusqu'à √n seulement
- **Diviseurs** : test par 2, 3, puis 6k±1
- **Algorithme efficace** : O(√n) au lieu de O(n)
- **Cas spéciaux** : 1 n'est pas premier, 2 et 3 sont premiers

**Test** : 2 (oui), 4 (non), 7 (oui), 9 (non), 17 (oui), 97 (oui), 100 (non).

---

### Exercice 110 : Affichage Fibonacci (fonction)
**Objectif** : Créer une fonction qui affiche la suite de Fibonacci jusqu'à n.

```python
# Solution
def fibonacci_jusque(n):
    """Affiche la suite de Fibonacci jusqu'à n"""
    if n < 0:
        print("Erreur : n doit être positif")
        return

    fib_sequence = []
    a, b = 0, 1

    while a <= n:
        fib_sequence.append(a)
        a, b = b, a + b

    return fib_sequence

# Tests
print("Fibonacci jusqu'à 20 :")
print(fibonacci_jusque(20))

print("\nFibonacci jusqu'à 100 :")
print(fibonacci_jusque(100))

print("\nFibonacci jusqu'à 1 :")
print(fibonacci_jusque(1))
```

**Explication** :
- **Suite de Fibonacci** : chaque terme = somme des deux précédents
- **Génération** : a, b = b, a+b (double affectation)
- **Limite** : s'arrête quand le terme dépasse n
- **Liste** : retourne la séquence complète

**Test** : 0, 1, 1, 2, 3, 5, 8, 13, 21 (> 20).

---

## 🔍 Points Clés à Retenir

### 1. **Syntaxe de Fonction**
```python
def nom_fonction(parametres):
    """Docstring - description de la fonction"""
    # Code de la fonction
    return valeur  # Optionnel
```

### 2. **Paramètres et Arguments**
```python
# Paramètres : variables dans la définition
def addition(a, b):  # a et b sont des paramètres
    return a + b

# Arguments : valeurs passées lors de l'appel
resultat = addition(5, 3)  # 5 et 3 sont des arguments
```

### 3. **Types de Fonctions**
```python
# Sans paramètre
def hello():
    return "Hello World"

# Avec paramètres
def calculer(a, b, c=0):  # c a une valeur par défaut
    return a + b + c

# Retournant plusieurs valeurs
def stats(nombres):
    return min(nombres), max(nombres), sum(nombres)
```

### 4. **Portée des Variables (Scope)**
```python
variable_globale = 10

def fonction():
    variable_locale = 5  # Variable locale
    print(variable_globale)  # Accès à la globale
    return variable_locale

print(variable_locale)  # ERREUR ! Non définie en dehors
```

## 💡 Optimisations et Astuces

### 1. **Valeurs par Défaut**
```python
def convertir_temperature(celsius, to_fahrenheit=True):
    """Convertit entre Celsius et Fahrenheit"""
    if to_fahrenheit:
        return (celsius * 9/5) + 32
    else:
        return (celsius - 32) * 5/9

# Utilisation
print(convertir_temperature(20))      # 68°F (par défaut)
print(convertir_temperature(68, False))  # 20°C
```

### 2. **Fonctions Lambda (anonymes)**
```python
# Fonction classique
def carre(x):
    return x ** 2

# Équivalent avec lambda
carre_lambda = lambda x: x ** 2

# Utilisation
print(carre(5))        # 25
print(carre_lambda(5)) # 25
```

### 3. **Documentation et Tests**
```python
def factoriel(n):
    """
    Calcule le factoriel de n

    Args:
        n (int): nombre positif ou nul

    Returns:
        int: factoriel de n

    Examples:
        >>> factoriel(5)
        120
        >>> factoriel(0)
        1
    """
    if n < 0:
        raise ValueError("n doit être positif")
    return 1 if n <= 1 else n * factoriel(n-1)
```

## 🚀 Applications Pratiques

### 1. **Calculateur de Statistiques**
```python
def statistiques(nombres):
    """Calcule des statistiques de base"""
    if not nombres:
        return None

    return {
        "minimum": min(nombres),
        "maximum": max(nombres),
        "somme": sum(nombres),
        "moyenne": sum(nombres) / len(nombres),
        "effectif": len(nombres)
    }

donnees = [15, 8, 12, 20, 7, 18, 25]
stats = statistiques(donnees)
for cle, valeur in stats.items():
    print(f"{cle}: {valeur}")
```

### 2. **Validateur de Données**
```python
def valider_donnees(valeur, type_attendu, contraintes=None):
    """Valide une valeur selon des critères"""
    # Test de type
    if type_attendu == "int":
        try:
            valeur = int(valeur)
        except ValueError:
            return False, "Doit être un entier"

    elif type_attendu == "float":
        try:
            valeur = float(valeur)
        except ValueError:
            return False, "Doit être un nombre"

    # Tests de contraintes
    if contraintes:
        if "min" in contraintes and valeur < contraintes["min"]:
            return False, f"Doit être >= {contraintes['min']}"
        if "max" in contraintes and valeur > contraintes["max"]:
            return False, f"Doit être <= {contraintes['max']}"

    return True, valeur

# Tests
resultats = [
    ("25", "int", {"min": 0, "max": 100}),
    ("3.14", "float", {"min": 0}),
    ("abc", "int", None)
]

for val, typ, contr in resultats:
    valide, message_ou_valeur = valider_donnees(val, typ, contr)
    print(f"'{val}' ({typ}): {valide} - {message_ou_valeur}")
```

### 3. **Générateur de Séries**
```python
def generer_serie(type_serie, n, parametres=None):
    """Génère différents types de séries"""
    if type_serie == "arithmetique":
        debut, raison = parametres
        return [debut + i * raison for i in range(n)]

    elif type_serie == "geometrique":
        debut, raison = parametres
        return [debut * (raison ** i) for i in range(n)]

    elif type_serie == "fibonacci":
        if n <= 0:
            return []
        elif n == 1:
            return [0]
        elif n == 2:
            return [0, 1]

        fib = [0, 1]
        for i in range(2, n):
            fib.append(fib[i-1] + fib[i-2])
        return fib

    else:
        return []

# Tests
print("Arithmétique (2, 3) 10 termes:", generer_serie("arithmetique", 10, (2, 3)))
print("Géométrique (2, 3) 8 termes:", generer_serie("geometrique", 8, (2, 3)))
print("Fibonacci 12 termes:", generer_serie("fibonacci", 12))
```

## 🎯 Défis Supplémentaires

1. **Créez** une fonction qui calcule la puissance (base^exposant)
2. **Développez** une fonction de conversion de devises multiples
3. **Implémentez** une fonction de recherche dans une liste
4. **Concevez** une fonction de validation d'adresse email

---

**Exercices complétés : 110/150** 🎯

*Continuez avec le [chapitre suivant](3-2-fonctions-avancees.md) pour les fonctions récursives !*