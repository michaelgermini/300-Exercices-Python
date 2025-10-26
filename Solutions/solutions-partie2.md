# Partie 2 - Contrôle de Flux : Solutions

## 🎯 Introduction

Cette partie présente les **solutions complètes** des exercices de la Partie 2. Chaque solution inclut :
- Le code source complet et fonctionnel
- Des explications détaillées
- Des exemples d'utilisation
- Des tests de validation

---

## 📚 Chapitre 2.1 : Solutions - Conditions if/elif/else

### Exercice 51 : Test de positivité

**Solution complète :**

```python
# Solution de base
nombre = float(input("Entrez un nombre : "))

if nombre > 0:
    print(f"{nombre} est positif")
elif nombre < 0:
    print(f"{nombre} est négatif")
else:
    print(f"{nombre} est nul")

# Solution avec fonction
def tester_positivite(n):
    """Teste si un nombre est positif, négatif ou nul"""
    if n > 0:
        return "positif"
    elif n < 0:
        return "négatif"
    else:
        return "nul"

# Test de la fonction
nombre = float(input("Entrez un nombre : "))
resultat = tester_positivite(nombre)
print(f"{nombre} est {resultat}")

# Solution avec gestion d'erreurs
while True:
    try:
        nombre = float(input("Entrez un nombre : "))
        break
    except ValueError:
        print("Veuillez entrer un nombre valide")

if nombre > 0:
    print(f"{nombre} est positif")
elif nombre < 0:
    print(f"{nombre} est négatif")
else:
    print("Le nombre est nul")
```

**Explications :**
- `if/elif/else` : structure conditionnelle complète
- `>` et `<` : opérateurs de comparaison
- `float()` : conversion en nombre décimal
- `try/except` : gestion des erreurs de saisie

**Test :**
```
Entrez un nombre : 5
5.0 est positif
```

---

### Exercice 52 : Test de parité

**Solution complète :**

```python
# Solution de base
nombre = int(input("Entrez un nombre entier : "))

if nombre % 2 == 0:
    print(f"{nombre} est pair")
else:
    print(f"{nombre} est impair")

# Solution avec fonction
def tester_parite(n):
    """Teste si un nombre est pair ou impair"""
    if n % 2 == 0:
        return "pair"
    else:
        return "impair"

# Test avec plusieurs nombres
nombres_test = [4, 7, 0, -3, 15]

for nombre in nombres_test:
    parite = tester_parite(nombre)
    print(f"{nombre} est {parite}")

# Solution avec valeur absolue
nombre = int(input("Entrez un nombre : "))
if abs(nombre) % 2 == 0:
    print(f"{nombre} est pair")
else:
    print(f"{nombre} est impair")
```

**Explications :**
- `%` : opérateur modulo (reste division)
- `== 0` : test d'égalité à zéro
- `abs()` : valeur absolue pour nombres négatifs
- Fonction : encapsulation de la logique

**Test :**
```
Entrez un nombre entier : 4
4 est pair

4 est pair
7 est impair
0 est pair
-3 est impair
15 est impair
```

---

### Exercice 53 : Test de divisibilité par 3 et 5

**Solution complète :**

```python
# Solution de base
nombre = int(input("Entrez un nombre : "))

if nombre % 3 == 0 and nombre % 5 == 0:
    print(f"{nombre} est divisible par 3 et par 5")
elif nombre % 3 == 0:
    print(f"{nombre} est divisible par 3")
elif nombre % 5 == 0:
    print(f"{nombre} est divisible par 5")
else:
    print(f"{nombre} n'est divisible ni par 3 ni par 5")

# Solution avec fonction
def analyser_divisibilite(n):
    """Analyse la divisibilité par 3 et 5"""
    divisible_par_3 = n % 3 == 0
    divisible_par_5 = n % 5 == 0

    if divisible_par_3 and divisible_par_5:
        return f"{n} divisible par 3 et 5"
    elif divisible_par_3:
        return f"{n} divisible par 3"
    elif divisible_par_5:
        return f"{n} divisible par 5"
    else:
        return f"{n} non divisible par 3 ni 5"

# Test
nombres = [15, 9, 10, 7, 30, 25]
for nombre in nombres:
    resultat = analyser_divisibilite(nombre)
    print(resultat)
```

**Explications :**
- `and` : opérateur logique ET
- `elif` : sinon si (conditions mutuellement exclusives)
- Tests multiples : vérification par ordre d'importance
- Fonction : analyse complète de divisibilité

**Test :**
```
15 divisible par 3 et 5
9 divisible par 3
10 divisible par 5
7 non divisible par 3 ni 5
```

---

### Exercice 54 : Test de divisibilité par 7

**Solution complète :**

```python
# Solution de base
nombre = int(input("Entrez un nombre : "))

if nombre % 7 == 0:
    print(f"{nombre} est divisible par 7")
    quotient = nombre // 7
    print(f"Quotient : {quotient}")
else:
    print(f"{nombre} n'est pas divisible par 7")
    reste = nombre % 7
    print(f"Reste : {reste}")

# Solution avec fonction complète
def tester_divisibilite_7(n):
    """Teste la divisibilité par 7 avec informations"""
    if n % 7 == 0:
        quotient = n // 7
        return True, f"{n} est divisible par 7", quotient
    else:
        reste = n % 7
        return False, f"{n} n'est pas divisible par 7", reste

# Test de la fonction
nombre = int(input("Entrez un nombre : "))
est_divisible, message, valeur = tester_divisibilite_7(nombre)
print(message)
if est_divisible:
    print(f"Quotient : {valeur}")
else:
    print(f"Reste : {valeur}")
```

**Explications :**
- `//` : division entière (quotient)
- `%` : modulo (reste)
- Retour multiple : booléen + message + valeur
- Information contextuelle : quotient ou reste selon le cas

**Test :**
```
21 est divisible par 7
Quotient : 3

22 n'est pas divisible par 7
Reste : 1
```

---

### Exercice 55 : Test de signe d'un nombre

**Solution complète :**

```python
# Solution avec conditions multiples
nombre = float(input("Entrez un nombre : "))

if nombre > 0:
    print(f"{nombre} est positif")
elif nombre < 0:
    print(f"{nombre} est négatif")
else:
    print("Le nombre est nul")

# Solution avec fonction
def determiner_signe(n):
    """Détermine le signe d'un nombre"""
    if n > 0:
        return "positif", ">"
    elif n < 0:
        return "négatif", "<"
    else:
        return "nul", "="

# Test avec différents nombres
nombres_test = [-5, -0.5, 0, 0.5, 5, 10.5]

for nombre in nombres_test:
    signe, operateur = determiner_signe(nombre)
    print(f"{nombre} est {signe} (0 {operateur} {nombre})")

# Solution avec tests logiques
nombre = float(input("Entrez un nombre : "))

if nombre != 0:  # Non nul
    if nombre > 0:
        print(f"{nombre} est positif")
    else:
        print(f"{nombre} est négatif")
else:
    print("Le nombre est nul")
```

**Explications :**
- `!=` : opérateur "différent de"
- Retour multiple : signe + opérateur de comparaison
- Tests logiques : conditions imbriquées
- Gestion des cas : positif, négatif, nul

**Test :**
```
-5.0 est négatif (0 < -5.0)
0.0 est nul (0 = 0.0)
5.0 est positif (0 > 5.0)
```

---

## 📚 Chapitre 2.2 : Solutions - Boucles for et while

### Exercice 56 : Affichage des 10 premiers nombres naturels

**Solution complète :**

```python
# Solution avec for
print("Avec for :")
for i in range(1, 11):
    print(i, end=" ")
print()

# Solution avec while
print("Avec while :")
i = 1
while i <= 10:
    print(i, end=" ")
    i += 1
print()

# Solution avec liste
print("Avec liste :")
nombres = list(range(1, 11))
print(nombres)

# Solution avec unpacking
print("Avec unpacking :")
print(*range(1, 11))
```

**Explications :**
- `range(1, 11)` : génère de 1 à 10
- `end=" "` : affiche sur la même ligne
- `while` : boucle conditionnelle
- `*` : unpacking des valeurs

**Test :**
```
Avec for : 1 2 3 4 5 6 7 8 9 10
Avec while : 1 2 3 4 5 6 7 8 9 10
```

---

### Exercice 57 : Nombres pairs de 2 à 20

**Solution complète :**

```python
# Solution avec range et pas
print("Nombres pairs de 2 à 20 :")
for i in range(2, 21, 2):
    print(i, end=" ")
print()

# Solution avec condition
print("Nombres pairs de 2 à 20 (condition) :")
for i in range(1, 21):
    if i % 2 == 0:
        print(i, end=" ")
print()

# Solution avec liste
pairs = [i for i in range(2, 21, 2)]
print("Liste des pairs :", pairs)

# Solution avec while
print("Avec while :")
i = 2
while i <= 20:
    print(i, end=" ")
    i += 2
print()
```

**Explications :**
- `range(start, stop, step)` : avec pas de 2
- `i % 2 == 0` : test de parité
- Compréhension de liste : génération concise
- `while` avec incrémentation

**Test :**
```
Nombres pairs de 2 à 20 : 2 4 6 8 10 12 14 16 18 20
```

---

### Exercice 58 : Nombres impairs de 1 à 19

**Solution complète :**

```python
# Solution avec range impair
print("Nombres impairs de 1 à 19 :")
for i in range(1, 20, 2):
    print(i, end=" ")
print()

# Solution avec condition
print("Nombres impairs de 1 à 19 (condition) :")
for i in range(1, 20):
    if i % 2 != 0:
        print(i, end=" ")
print()

# Solution avec liste
impairs = [i for i in range(1, 20, 2)]
print("Liste des impairs :", impairs)

# Solution avec while
print("Avec while :")
i = 1
while i <= 19:
    print(i, end=" ")
    i += 2
print()
```

**Explications :**
- `range(1, 20, 2)` : impair directement
- `i % 2 != 0` : test d'imparité
- Pattern : 2n+1 pour les impairs
- Incrémentation de 2

**Test :**
```
Nombres impairs de 1 à 19 : 1 3 5 7 9 11 13 15 17 19
```

---

### Exercice 59 : Somme de 1 à 100 (formule de Gauss)

**Solution complète :**

```python
# Solution mathématique (formule de Gauss)
n = 100
somme = n * (n + 1) // 2
print(f"Somme de 1 à {n} (Gauss) = {somme}")

# Solution avec boucle for
somme_boucle = 0
for i in range(1, 101):
    somme_boucle += i
print(f"Somme avec boucle for = {somme_boucle}")

# Solution avec while
somme_while = 0
i = 1
while i <= 100:
    somme_while += i
    i += 1
print(f"Somme avec while = {somme_while}")

# Solution avec sum()
somme_sum = sum(range(1, 101))
print(f"Somme avec sum() = {somme_sum}")

# Vérification
print(f"Toutes méthodes identiques : {somme == somme_boucle == somme_while == somme_sum}")
```

**Explications :**
- **Formule de Gauss** : n(n+1)/2
- `//` : division entière (résultat exact)
- `sum()` : fonction built-in efficace
- Complexité : O(1) vs O(n)

**Test :**
```
Somme de 1 à 100 (Gauss) = 5050
Somme avec boucle for = 5050
Somme avec while = 5050
Somme avec sum() = 5050
Toutes méthodes identiques : True
```

---

### Exercice 60 : Produit de 1 à 10

**Solution complète :**

```python
# Solution avec for
produit = 1
for i in range(1, 11):
    produit *= i
print(f"Produit de 1 à 10 = {produit}")

# Solution avec while
produit = 1
i = 1
while i <= 10:
    produit *= i
    i += 1
print(f"Produit avec while = {produit}")

# Solution avec math
import math
factoriel = math.factorial(10)
print(f"10! avec math.factorial = {factoriel}")

# Solution avec fonction récursive
def factoriel_recursif(n):
    if n <= 1:
        return 1
    return n * factoriel_recursif(n - 1)

print(f"Factoriel récursif = {factoriel_recursif(10)}")

# Vérification
print(f"Toutes méthodes identiques : {produit == factoriel == factoriel_recursif(10)}")
```

**Explications :**
- `math.factorial()` : fonction built-in
- Récursion : factoriel(n) = n × factoriel(n-1)
- Initialisation : produit = 1 (élément neutre)
- `*= ` : multiplication et affectation

**Test :**
```
Produit de 1 à 10 = 3628800
10! avec math.factorial = 3628800
Toutes méthodes identiques : True
```

---

## 🎯 Résumé des Solutions - Partie 2

### ✅ **Exercices Résolus (51-60)**

| Exercice | Thème | Solution | Fonctionnalités |
|----------|-------|----------|-----------------|
| **51** | Test positivité | ✅ Complète | Conditions, fonctions, erreurs |
| **52** | Test parité | ✅ Complète | Modulo, fonctions, tests multiples |
| **53** | Divisibilité 3/5 | ✅ Complète | Logique AND/OR, priorités |
| **54** | Divisibilité 7 | ✅ Complète | Quotient, reste, informations |
| **55** | Test signe | ✅ Complète | Comparaisons, retours multiples |
| **56** | Nombres 1-10 | ✅ Complète | Boucles for/while, range |
| **57** | Nombres pairs | ✅ Complète | Range pas, conditions, listes |
| **58** | Nombres impairs | ✅ Complète | Range impair, modulo, patterns |
| **59** | Somme 1-100 | ✅ Complète | Gauss, boucles, sum(), perf |
| **60** | Produit 1-10 | ✅ Complète | Factoriel, récursion, math |

### 🚀 **Concepts Clés Maîtrisés**

- **Structures conditionnelles** : if/elif/else, imbrication
- **Opérateurs** : comparaison (==, !=, <, >), logique (and, or, not)
- **Boucles** : for avec range, while avec conditions
- **Modularité** : fonctions, encapsulation, retours multiples
- **Gestion d'erreurs** : try/except, validation des entrées
- **Optimisation** : formules vs boucles, complexité algorithmique

### 📚 **Fonctionnalités Avancées**

- **Tests automatisés** : validation avec listes de valeurs
- **Interface interactive** : saisie utilisateur continue
- **Formatage** : affichage lisible et professionnel
- **Fonctions utilitaires** : réutilisabilité du code
- **Analyse de performance** : comparaison des méthodes
- **Gestion des cas limites** : nombres négatifs, zéro, bornes

---

**🎉 Toutes les solutions de la Partie 2 sont maintenant disponibles !**

*Ces solutions démontrent la maîtrise des structures de contrôle essentielles en Python, avec des exemples pratiques et des optimisations.*
