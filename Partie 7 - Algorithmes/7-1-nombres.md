# Partie 7.1 : Nombres et Séquences

## 🎯 Objectifs Pédagogiques

Ce chapitre explore les **algorithmes sur les nombres** et les **séquences mathématiques** en Python. Nous apprendrons à manipuler les nombres, générer des séquences et résoudre des problèmes algorithmiques classiques.

### Concepts Abordés
- **Nombres premiers** : test, génération, factorisation
- **Séquences** : Fibonacci, factoriels, suites arithmétiques
- **Calculs mathématiques** : PGCD, PPCM, sommes, moyennes
- **Applications** : cryptographie, théorie des nombres, optimisation

---

## 📝 Exercices Pratiques

### Exercice 261 : Vérifier si un nombre est premier
**Objectif** : Implémenter un test de primalité efficace.

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
nombres_test = [1, 2, 3, 4, 5, 7, 11, 13, 17, 19, 23, 29, 31, 97, 100, 997]
print("Tests de primalité :")
for nombre in nombres_test:
    resultat = est_premier(nombre)
    print(f"{nombre"3d"} est premier : {resultat}")
```

**Explication** :
- **Optimisation** : test jusqu'à √n seulement
- **Diviseurs** : test par 2, 3, puis 6k±1
- **Algorithme efficace** : O(√n) au lieu de O(n)
- **Applications** : cryptographie, génération de nombres

**Test** : 2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 97 (premiers).

---

### Exercice 262 : Générer la suite de Fibonacci jusqu'à n
**Objectif** : Générer la suite de Fibonacci jusqu'à une limite.

```python
# Solution
def fibonacci_jusque(n):
    """Génère la suite de Fibonacci jusqu'à n"""
    if n < 0:
        return []

    fib_sequence = []
    a, b = 0, 1

    while a <= n:
        fib_sequence.append(a)
        a, b = b, a + b

    return fib_sequence

# Tests
print("Suite de Fibonacci jusqu'à 100 :")
fib_100 = fibonacci_jusque(100)
print(fib_100)
print(f"Nombre de termes : {len(fib_100)}")

print("\nSuite de Fibonacci jusqu'à 1000 :")
fib_1000 = fibonacci_jusque(1000)
print(f"Nombre de termes : {len(fib_1000)}")

# Vérification : chaque terme = somme des deux précédents
print("\nVérification de la suite :")
for i in range(2, min(10, len(fib_100))):
    verification = fib_100[i] == fib_100[i-1] + fib_100[i-2]
    print(f"F({i}) = F({i-1}) + F({i-2}) : {verification}")
```

**Explication** :
- **Suite de Fibonacci** : chaque terme = somme des deux précédents
- **Génération** : itérative avec deux variables
- **Limite** : s'arrête quand le terme dépasse n
- **Applications** : modélisation, biologie, finance

**Test** : 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89.

---

### Exercice 263 : Calculer le PGCD de deux nombres
**Objectif** : Implémenter l'algorithme d'Euclide pour le PGCD.

```python
# Solution
def pgcd(a, b):
    """Calcule le PGCD de a et b par l'algorithme d'Euclide"""
    while b != 0:
        a, b = b, a % b
    return a

# Tests
paires_test = [
    (48, 18),    # PGCD = 6
    (100, 25),   # PGCD = 25
    (17, 13),    # PGCD = 1
    (60, 48),    # PGCD = 12
    (7, 5),      # PGCD = 1
    (1000, 750), # PGCD = 250
]

print("Calculs de PGCD :")
for a, b in paires_test:
    resultat = pgcd(a, b)
    print(f"PGCD({a}, {b}) = {resultat}")

# Vérification avec math.gcd
import math
print("\nVérification avec math.gcd :")
for a, b in paires_test:
    math_result = math.gcd(a, b)
    notre_result = pgcd(a, b)
    identique = math_result == notre_result
    print(f"math.gcd({a}, {b}) = {math_result}, notre fonction = {notre_result}, identique = {identique}")
```

**Explication** :
- **Algorithme d'Euclide** : PGCD(a,b) = PGCD(b, a mod b)
- **Itération** : continue jusqu'à ce que b = 0
- **Efficacité** : O(log min(a,b))
- **Mathématiques** : propriété fondamentale

**Test** : PGCD(48, 18) = 6, PGCD(100, 25) = 25.

---

### Exercice 264 : Calculer le PPCM de deux nombres
**Objectif** : Calculer le Plus Petit Commun Multiple.

```python
# Solution
def ppcm(a, b):
    """Calcule le PPCM de a et b"""
    if a == 0 or b == 0:
        return 0
    return (a * b) // pgcd(a, b)

# Tests
paires_test = [
    (4, 6),      # PPCM = 12
    (12, 18),    # PPCM = 36
    (7, 11),     # PPCM = 77
    (15, 25),    # PPCM = 75
    (8, 12),     # PPCM = 24
]

print("Calculs de PPCM :")
for a, b in paires_test:
    resultat = ppcm(a, b)
    print(f"PPCM({a}, {b}) = {resultat}")

# Vérification : a * b = PGCD(a,b) * PPCM(a,b)
print("\nVérifications :")
for a, b in paires_test:
    pgcd_val = pgcd(a, b)
    ppcm_val = ppcm(a, b)
    produit = a * b
    verification = pgcd_val * ppcm_val == produit
    print(f"{a} × {b} = {pgcd_val} × {ppcm_val} = {produit} : {verification}")
```

**Explication** :
- **Formule** : PPCM(a,b) = (a × b) / PGCD(a,b)
- **Division entière** : // pour éviter les flottants
- **Relation** : PPCM × PGCD = a × b
- **Applications** : fractions, rythmes, cycles

**Test** : PPCM(4, 6) = 12, PPCM(12, 18) = 36.

---

### Exercice 265 : Vérifier si un nombre est palindrome
**Objectif** : Vérifier si un nombre se lit dans les deux sens.

```python
# Solution
def est_palindrome_nombre(n):
    """Vérifie si un nombre est palindrome"""
    if n < 0:
        return False

    # Conversion en chaîne pour manipulation
    nombre_str = str(n)
    return nombre_str == nombre_str[::-1]

# Tests
nombres_test = [121, 123, 3443, 12321, 12345, 1, 999, 1001, 0, -121]
print("Tests de palindrome numérique :")
for nombre in nombres_test:
    resultat = est_palindrome_nombre(nombre)
    print(f"{nombre"5d"} est palindrome : {resultat}")

# Palindromes célèbres
palindromes_celeb = [121, 343, 3443, 12321, 10201]
print("
Palindromes célèbres :")
for nombre in palindromes_celeb:
    print(f"{nombre} : {est_palindrome_nombre(nombre)}")
```

**Explication** :
- **Conversion string** : str() pour manipuler les chiffres
- **Inversion** : [::-1] technique classique
- **Nombres négatifs** : non considérés comme palindromes
- **Applications** : puzzles, nombres intéressants

**Test** : 121, 3443, 12321 (palindromes).

---

## 🔍 Points Clés à Retenir

### 1. **Test de Primalité**
```python
def est_premier(n):
    if n <= 1:
        return False
    if n <= 3:
        return True
    if n % 2 == 0 or n % 3 == 0:
        return False

    i = 5
    while i * i <= n:
        if n % i == 0 or n % (i + 2) == 0:
            return False
        i += 6
    return True
```

### 2. **Suite de Fibonacci**
```python
def fibonacci_jusque(n):
    fib = [0, 1]
    while fib[-1] <= n:
        fib.append(fib[-1] + fib[-2])
    return fib[:-1]  # Exclure le dernier > n
```

### 3. **PGCD et PPCM**
```python
def pgcd(a, b):
    while b:
        a, b = b, a % b
    return a

def ppcm(a, b):
    return (a * b) // pgcd(a, b) if a and b else 0
```

### 4. **Palindrome Numérique**
```python
def est_palindrome(n):
    s = str(abs(n))
    return s == s[::-1]
```

## 💡 Optimisations et Astuces

### 1. **Test de Primalité Plus Efficace**
```python
def est_premier_rapide(n):
    """Test de primalité plus optimisé"""
    if n < 2:
        return False
    if n < 4:
        return True
    if n % 2 == 0 or n % 3 == 0:
        return False

    # Test tous les nombres de la forme 6k ± 1
    for i in range(5, int(n**0.5) + 1, 6):
        if n % i == 0 or n % (i + 2) == 0:
            return False
    return True
```

### 2. **Génération de Nombres Premiers**
```python
def generer_premiers(limite):
    """Génère tous les nombres premiers jusqu'à limite"""
    premiers = []
    for n in range(2, limite + 1):
        if est_premier(n):
            premiers.append(n)
    return premiers

# Crible d'Ératosthène (plus efficace)
def crible_eratosthene(limite):
    """Crible d'Ératosthène pour générer les nombres premiers"""
    if limite < 2:
        return []

    # Initialisation
    est_premier_liste = [True] * (limite + 1)
    est_premier_liste[0] = est_premier_liste[1] = False

    # Criblage
    for i in range(2, int(limite**0.5) + 1):
        if est_premier_liste[i]:
            for multiple in range(i*i, limite + 1, i):
                est_premier_liste[multiple] = False

    return [i for i in range(2, limite + 1) if est_premier_liste[i]]
```

### 3. **Fibonacci avec Memoization**
```python
memo_fib = {0: 0, 1: 1}

def fibonacci_memo(n):
    """Fibonacci avec memoization"""
    if n in memo_fib:
        return memo_fib[n]

    memo_fib[n] = fibonacci_memo(n-1) + fibonacci_memo(n-2)
    return memo_fib[n]
```

## 🚀 Applications Pratiques

### 1. **Analyseur de Nombres**
```python
def analyser_nombre(n):
    """Analyse complète d'un nombre"""
    analyses = {
        "nombre": n,
        "est_premier": est_premier(n),
        "est_palindrome": est_palindrome_nombre(n),
        "chiffres": len(str(n)),
        "somme_chiffres": sum(int(c) for c in str(abs(n))),
        "produit_chiffres": eval('*'.join(str(abs(n)))) if n != 0 else 0
    }

    # Diviseurs
    diviseurs = [i for i in range(1, n+1) if n % i == 0]
    analyses["diviseurs"] = diviseurs
    analyses["nombre_diviseurs"] = len(diviseurs)
    analyses["est_parfait"] = sum(diviseurs[:-1]) == n

    # Factorisation
    if n > 1:
        facteurs = []
        d = 2
        while d * d <= n:
            while n % d == 0:
                facteurs.append(d)
                n //= d
            d += 1
        if n > 1:
            facteurs.append(n)
        analyses["factorisation"] = facteurs

    return analyses

# Test
analyse = analyser_nombre(28)
print("Analyse de 28 :")
for cle, valeur in analyse.items():
    print(f"  {cle}: {valeur}")
```

### 2. **Générateur de Séries Mathématiques**
```python
def generer_series_math(n):
    """Génère différentes séries mathématiques"""
    series = {}

    # Fibonacci
    series["fibonacci"] = fibonacci_jusque(n)

    # Carrés
    series["carres"] = [i**2 for i in range(1, n+1)]

    # Cubes
    series["cubes"] = [i**3 for i in range(1, n+1)]

    # Triangulaires
    series["triangulaires"] = [i*(i+1)//2 for i in range(1, n+1)]

    # Pentagonaux
    series["pentagonaux"] = [i*(3*i-1)//2 for i in range(1, n+1)]

    # Nombres premiers
    series["premiers"] = crible_eratosthene(min(n, 1000))  # Limite pour performance

    return series

# Test
series = generer_series_math(10)
for nom, valeurs in series.items():
    print(f"{nom}: {valeurs}")
```

### 3. **Calculateur de Propriétés**
```python
def proprietes_nombres(nombres):
    """Calcule diverses propriétés de nombres"""
    resultats = {}

    for nombre in nombres:
        props = {
            "est_premier": est_premier(nombre),
            "est_pair": nombre % 2 == 0,
            "est_palindrome": est_palindrome_nombre(nombre),
            "chiffres": len(str(abs(nombre))),
            "somme_chiffres": sum(int(c) for c in str(abs(nombre))),
            "est_parfait": sum(i for i in range(1, nombre) if nombre % i == 0) == nombre,
            "pgcd_avec_60": pgcd(nombre, 60),
            "ppcm_avec_60": ppcm(nombre, 60)
        }

        # Diviseurs
        diviseurs = [i for i in range(1, nombre+1) if nombre % i == 0]
        props["diviseurs"] = diviseurs
        props["tau"] = len(diviseurs)  # Nombre de diviseurs

        resultats[nombre] = props

    return resultats

# Test
nombres_test = [6, 12, 28, 36, 100]
proprietes = proprietes_nombres(nombres_test)

for nombre, props in proprietes.items():
    print(f"\nPropriétés de {nombre} :")
    for cle, valeur in props.items():
        if cle != "diviseurs":
            print(f"  {cle}: {valeur}")
    print(f"  diviseurs: {props['diviseurs']}")
```

## 🎯 Défis Supplémentaires

1. **Implémentez** le crible d'Ératosthène pour générer les nombres premiers
2. **Créez** une fonction pour factoriser un nombre
3. **Développez** un générateur de nombres parfaits
4. **Concevez** un analyseur de propriétés de nombres avec interface

---

**Exercices complétés : 265/285** 🎯

*Continuez avec le [chapitre suivant](7-2-statistiques.md) pour les statistiques et probabilités !*
