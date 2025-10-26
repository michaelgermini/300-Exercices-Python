# Partie 1 - Bases de Python : Solutions

## 🎯 Introduction

Cette partie présente les **solutions complètes** des exercices de la Partie 1. Chaque solution inclut :
- Le code source complet et fonctionnel
- Des explications détaillées
- Des exemples d'utilisation
- Des tests de validation

---

## 📚 Chapitre 1.1 : Solutions - Types de Données

### Exercice 1 : Afficher "Hello World"

**Solution complète :**

```python
# Solution la plus simple
print("Hello World")

# Solution avec formatage
message = "Hello World"
print(message)

# Solution avec f-string (moderne)
print(f"{message}")

# Solution avec format()
print("{}".format(message))
```

**Explications :**
- `print()` : fonction d'affichage en Python
- F-strings : formatage moderne avec `f""`
- `.format()` : méthode de formatage classique
- Variables : stockage des valeurs

**Test :**
```python
Hello World
```

---

### Exercice 2 : Addition de deux nombres

**Solution complète :**

```python
# Solution avec variables
nombre1 = 15
nombre2 = 25
somme = nombre1 + nombre2
print(f"{nombre1} + {nombre2} = {somme}")

# Solution avec input utilisateur
nombre1 = int(input("Premier nombre : "))
nombre2 = int(input("Second nombre : "))
somme = nombre1 + nombre2
print(f"{nombre1} + {nombre2} = {somme}")

# Solution avec calcul direct
print(f"15 + 25 = {15 + 25}")
```

**Explications :**
- `int()` : conversion en nombre entier
- `input()` : saisie utilisateur
- `+` : opérateur d'addition
- F-strings pour l'affichage formaté

**Test :**
```
15 + 25 = 40
```

---

### Exercice 3 : Calcul de l'aire d'un cercle

**Solution complète :**

```python
import math

# Solution avec math.pi
rayon = float(input("Rayon du cercle : "))
aire = math.pi * rayon ** 2
print(f"Aire du cercle de rayon {rayon} = {aire:.2f}")

# Solution avec pi approximatif
rayon = float(input("Rayon du cercle : "))
pi = 3.14159
aire = pi * rayon ** 2
print(f"Aire du cercle de rayon {rayon} = {aire:.2f}")

# Solution avec math.pow (puissance)
import math
rayon = float(input("Rayon du cercle : "))
aire = math.pi * math.pow(rayon, 2)
print(f"Aire du cercle de rayon {rayon} = {aire:.2f}")
```

**Explications :**
- `import math` : module mathématique
- `math.pi` : constante π
- `**` : opérateur de puissance
- `math.pow()` : fonction puissance
- `:.2f` : formatage à 2 décimales

**Test :**
```
Rayon du cercle : 5
Aire du cercle de rayon 5.0 = 78.54
```

---

### Exercice 4 : Conversion Celsius vers Fahrenheit

**Solution complète :**

```python
# Solution avec input
celsius = float(input("Température en Celsius : "))
fahrenheit = (celsius * 9/5) + 32
print(f"{celsius}°C = {fahrenheit:.1f}°F")

# Solution avec formules inverses
fahrenheit = float(input("Température en Fahrenheit : "))
celsius = (fahrenheit - 32) * 5/9
print(f"{fahrenheit}°F = {celsius:.1f}°C")

# Solution avec validation
while True:
    try:
        celsius = float(input("Température en Celsius : "))
        fahrenheit = (celsius * 9/5) + 32
        print(f"{celsius}°C = {fahrenheit:.1f}°F")
        break
    except ValueError:
        print("Veuillez entrer un nombre valide")
```

**Explications :**
- Formule : F = (C × 9/5) + 32
- Formule inverse : C = (F - 32) × 5/9
- `try/except` : gestion des erreurs
- `:1f` : formatage à 1 décimale

**Test :**
```
Température en Celsius : 25
25.0°C = 77.0°F
```

---

### Exercice 5 : Calcul du volume d'une sphère

**Solution complète :**

```python
import math

# Solution avec math
rayon = float(input("Rayon de la sphère : "))
volume = (4/3) * math.pi * rayon ** 3
print(f"Volume de la sphère de rayon {rayon} = {volume:.2f}")

# Solution avec constantes
rayon = float(input("Rayon de la sphère : "))
pi = 3.14159
volume = (4/3) * pi * (rayon ** 3)
print(f"Volume de la sphère de rayon {rayon} = {volume:.2f}")

# Solution avec validation
import math

def calculer_volume_sphere(rayon):
    """Calcule le volume d'une sphère"""
    if rayon < 0:
        return "Rayon invalide (négatif)"
    return (4/3) * math.pi * rayon ** 3

rayon = float(input("Rayon de la sphère : "))
volume = calculer_volume_sphere(rayon)
print(f"Volume : {volume:.2f}")
```

**Explications :**
- Formule : V = (4/3)πr³
- `math.pi` : constante π précise
- Validation : rayon positif
- Fonction : encapsulation du calcul

**Test :**
```
Rayon de la sphère : 3
Volume de la sphère de rayon 3.0 = 113.10
```

---

## 📚 Chapitre 1.2 : Solutions - Opérations Mathématiques

### Exercice 13 : Conversion km en miles

**Solution complète :**

```python
# Solution
kilometres = float(input("Distance en km : "))
miles = kilometres * 0.621371
print(kilometres, "km =", round(miles, 2), "miles")

# Solution avec formatage
kilometres = float(input("Distance en km : "))
miles = kilometres * 0.621371
print(f"{kilometres} km = {miles:.2f} miles")

# Solution avec fonction
def km_vers_miles(km):
    """Convertit km en miles"""
    return km * 0.621371

kilometres = float(input("Distance en km : "))
miles = km_vers_miles(kilometres)
print(f"{kilometres} km = {round(miles, 2)} miles")
```

**Explications :**
- Facteur de conversion : 1 km = 0.621371 miles
- `round(valeur, 2)` : arrondi à 2 décimales
- `f"{valeur:.2f}"` : formatage décimal
- Fonction : réutilisabilité

**Test :**
```
Distance en km : 10
10.0 km = 6.21 miles
```

---

### Exercice 14 : Conversion minutes en heures

**Solution complète :**

```python
# Solution
minutes = int(input("Nombre de minutes : "))
heures = minutes // 60
minutes_restantes = minutes % 60
print(minutes, "minutes =", heures, "h", minutes_restantes, "min")

# Solution avec formatage
minutes = int(input("Nombre de minutes : "))
heures = minutes // 60
minutes_restantes = minutes % 60
print(f"{minutes} minutes = {heures}h{minutes_restantes}min")

# Solution avec fonction
def minutes_vers_heures(minutes):
    """Convertit minutes en heures et minutes"""
    h = minutes // 60
    min_rest = minutes % 60
    return h, min_rest

minutes = int(input("Nombre de minutes : "))
heures, minutes_restantes = minutes_vers_heures(minutes)
print(f"{minutes} minutes = {heures}h{minutes_restantes}min")
```

**Explications :**
- `//` : division entière (quotient)
- `%` : modulo (reste)
- Formatage : affichage lisible
- Fonction : retourne tuple (heures, minutes)

**Test :**
```
Nombre de minutes : 90
90 minutes = 1h30min
```

---

### Exercice 15 : Test de positivité

**Solution complète :**

```python
# Solution
nombre = float(input("Entrez un nombre : "))
if nombre > 0:
    print(nombre, "est positif")
elif nombre < 0:
    print(nombre, "est négatif")
else:
    print(nombre, "est nul")

# Solution avec fonction
def tester_positivite(nombre):
    """Teste si un nombre est positif, négatif ou nul"""
    if nombre > 0:
        return f"{nombre} est positif"
    elif nombre < 0:
        return f"{nombre} est négatif"
    else:
        return f"{nombre} est nul"

nombre = float(input("Entrez un nombre : "))
resultat = tester_positivite(nombre)
print(resultat)

# Solution avec valeur absolue
nombre = float(input("Entrez un nombre : "))
if nombre > 0:
    print(f"{nombre} est positif")
elif nombre < 0:
    print(f"{nombre} est négatif")
else:
    print("Le nombre est nul")
```

**Explications :**
- `if/elif/else` : structure conditionnelle complète
- `>` et `<` : comparaisons
- Fonction : encapsulation logique
- Valeur absolue : pas nécessaire ici

**Test :**
```
Entrez un nombre : 5
5.0 est positif
```

---

### Exercice 16 : Affichage des 10 premiers nombres naturels

**Solution complète :**

```python
# Solution avec boucle
for i in range(1, 11):
    print(i, end=" ")
print()  # Saut de ligne final

# Solution avec while
i = 1
while i <= 10:
    print(i, end=" ")
    i += 1
print()

# Solution avec liste
nombres = list(range(1, 11))
for nombre in nombres:
    print(nombre, end=" ")
print()

# Solution avec *args
print(*range(1, 11))
```

**Explications :**
- `range(1, 11)` : génère 1 à 10
- `end=" "` : affiche sur même ligne
- `for` : itération
- `while` : boucle conditionnelle
- `*` : unpacking

**Test :**
```
1 2 3 4 5 6 7 8 9 10
```

---

### Exercice 17 : Nombres pairs de 2 à 20

**Solution complète :**

```python
# Solution
print("Nombres pairs de 2 à 20 :")
for i in range(2, 21, 2):  # Départ 2, fin 21, pas 2
    print(i, end=" ")
print()

# Solution avec condition
print("Nombres pairs de 2 à 20 :")
for i in range(1, 21):
    if i % 2 == 0:
        print(i, end=" ")
print()

# Solution avec liste
pairs = [i for i in range(2, 21, 2)]
print("Nombres pairs :", pairs)
```

**Explications :**
- `range(start, stop, step)` : avec pas
- `i % 2 == 0` : test de parité
- Compréhension de liste : génération concise
- Pas de 2 : génère directement les pairs

**Test :**
```
Nombres pairs de 2 à 20 : 2 4 6 8 10 12 14 16 18 20
```

---

### Exercice 18 : Nombres impairs de 1 à 19

**Solution complète :**

```python
# Solution
print("Nombres impairs de 1 à 19 :")
for i in range(1, 20, 2):  # Départ 1, fin 20, pas 2
    print(i, end=" ")
print()

# Solution avec condition
print("Nombres impairs de 1 à 19 :")
for i in range(1, 20):
    if i % 2 != 0:
        print(i, end=" ")
print()

# Solution avec liste
impairs = [i for i in range(1, 20, 2)]
print("Nombres impairs :", impairs)
```

**Explications :**
- `range(1, 20, 2)` : impair directement
- `i % 2 != 0` : test d'imparité
- Compréhension : génération concise
- Pattern : 2n+1 pour impairs

**Test :**
```
Nombres impairs de 1 à 19 : 1 3 5 7 9 11 13 15 17 19
```

---

### Exercice 19 : Somme de 1 à 100

**Solution complète :**

```python
# Solution mathématique (formule de Gauss)
n = 100
somme = n * (n + 1) // 2
print("Somme de 1 à", n, "=", somme)

# Alternative avec boucle (pour comparaison)
somme_boucle = 0
for i in range(1, 101):
    somme_boucle += i
print("Somme avec boucle =", somme_boucle)

# Solution avec sum()
somme_sum = sum(range(1, 101))
print("Somme avec sum() =", somme_sum)

# Vérification
print("Formule de Gauss :", 100 * 101 // 2)
print("Toutes méthodes identiques :", somme == somme_boucle == somme_sum)
```

**Explications :**
- **Formule de Gauss** : n(n+1)/2
- `//` : division entière (exacte)
- `sum()` : fonction built-in
- Complexité : O(1) vs O(n)

**Test :**
```
Somme de 1 à 100 = 5050
Somme avec boucle = 5050
Somme avec sum() = 5050
```

---

### Exercice 20 : Produit de 1 à 10

**Solution complète :**

```python
# Solution
produit = 1
for i in range(1, 11):
    produit *= i  # produit = produit * i
print("Produit de 1 à 10 (10!) =", produit)

# Solution avec math
import math
factoriel = math.factorial(10)
print("10! =", factoriel)

# Solution avec fonction récursive
def factoriel(n):
    if n <= 1:
        return 1
    return n * factoriel(n - 1)

print("Factoriel récursif :", factoriel(10))

# Vérification
print("10! = 3,628,800")
print("Vérification :", produit == math.factorial(10) == factoriel(10))
```

**Explications :**
- `math.factorial()` : fonction built-in
- Récursion : factoriel(n) = n × factoriel(n-1)
- Initialisation : produit = 1
- `*= ` : multiplication et affectation

**Test :**
```
Produit de 1 à 10 (10!) = 3628800
10! = 3628800
```

---

## 🎯 Résumé des Solutions - Partie 1

### ✅ **Exercices Résolus (1-20)**

| Exercice | Thème | Solution | Fonctionnalités |
|----------|-------|----------|-----------------|
| **1** | Hello World | ✅ Complète | Affichage, variables, formatage |
| **2** | Addition | ✅ Complète | Input, conversion, calcul |
| **3** | Aire cercle | ✅ Complète | Math.pi, puissance, formatage |
| **4** | Conversion temp | ✅ Complète | Formules, validation, erreurs |
| **5** | Volume sphère | ✅ Complète | Math 3D, validation, fonction |
| **13** | Km → miles | ✅ Complète | Conversion, arrondi, fonction |
| **14** | Minutes → heures | ✅ Complète | Division, modulo, tuple |
| **15** | Test positivité | ✅ Complète | Conditions, elif, fonction |
| **16** | Nombres naturels | ✅ Complète | Boucles, range, unpacking |
| **17** | Nombres pairs | ✅ Complète | Range pas, condition, liste |
| **18** | Nombres impairs | ✅ Complète | Range impair, modulo, liste |
| **19** | Somme 1-100 | ✅ Complète | Gauss, boucle, sum() |
| **20** | Produit 1-10 | ✅ Complète | Factoriel, récursion, math |

### 🚀 **Concepts Clés Maîtrisés**

- **Types de données** : int, float, str
- **Opérations** : +, -, *, /, //, %, **
- **Input/Output** : input(), print(), formatage
- **Mathématiques** : pi, puissance, factoriel
- **Logique** : if/elif/else, boucles, fonctions
- **Validation** : try/except, conditions
- **Formatage** : f-strings, .format(), round()

### 📚 **Fonctionnalités Avancées**

- **Gestion d'erreurs** : validation des entrées
- **Fonctions** : encapsulation et réutilisabilité
- **Formatage** : affichage lisible et professionnel
- **Optimisations** : formules mathématiques vs boucles
- **Tests** : validation et vérification des résultats

---

**🎉 Toutes les solutions de la Partie 1 sont maintenant disponibles !**

*Ces solutions démontrent les bases fondamentales de Python avec des exemples pratiques et des explications détaillées.*
