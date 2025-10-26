# Partie 7.2 : Statistiques et Probabilités

## 🎯 Objectifs Pédagogiques

Ce chapitre explore les **calculs statistiques** et les **méthodes probabilistes** en Python. Nous apprendrons à analyser des données et à simuler des phénomènes aléatoires.

### Concepts Abordés
- **Statistiques descriptives** : moyenne, médiane, écart-type
- **Probabilités** : simulations, Monte Carlo
- **Analyse de données** : tendances, dispersion
- **Applications** : science des données, simulations

---

## 📝 Exercices Pratiques

### Exercice 266 : Calculer la somme des chiffres d'un nombre
**Objectif** : Décomposer un nombre et calculer la somme de ses chiffres.

```python
# Solution
def somme_chiffres(n):
    """Calcule la somme des chiffres d'un nombre"""
    if n < 0:
        n = -n  # Travaille avec la valeur absolue

    somme = 0
    while n > 0:
        somme += n % 10
        n = n // 10

    return somme

# Tests
nombres_test = [123, 456, 789, 1000, 999, 0, 42, 2024]
print("Somme des chiffres :")
for nombre in nombres_test:
    resultat = somme_chiffres(nombre)
    print(f"{nombre} → {resultat}")

# Test avec de grands nombres
grand_nombre = 123456789
print(f"\nGrand nombre {grand_nombre} :")
print(f"Somme des chiffres : {somme_chiffres(grand_nombre)}")

# Vérification
somme_manuelle = sum(int(c) for c in str(grand_nombre))
print(f"Vérification manuelle : {somme_manuelle}")
```

**Explication** :
- **Décomposition** : extraction chiffre par chiffre
- **Modulo 10** : obtient le dernier chiffre
- **Division entière** : enlève le dernier chiffre
- **Applications** : checksum, vérification de numéros

**Test** : 123 → 6, 456 → 15, 789 → 24.

---

### Exercice 267 : Trouver le maximum de plusieurs nombres
**Objectif** : Trouver le plus grand nombre parmi plusieurs valeurs.

```python
# Solution
def maximum(*nombres):
    """Trouve le maximum de plusieurs nombres"""
    if not nombres:
        return None

    max_val = nombres[0]
    for nombre in nombres[1:]:
        if nombre > max_val:
            max_val = nombre

    return max_val

# Tests
print("Tests de maximum :")
print(f"max(5, 3, 8, 1) = {maximum(5, 3, 8, 1)}")
print(f"max(10, 20, 30) = {maximum(10, 20, 30)}")
print(f"max(-5, -1, -10) = {maximum(-5, -1, -10)}")
print(f"max(42) = {maximum(42)}")
print(f"max() = {maximum()}")

# Comparaison avec built-in
import random
nombres_aleatoires = [random.randint(1, 100) for _ in range(10)]
max_builtin = max(nombres_aleatoires)
max_notre = maximum(*nombres_aleatoires)
print(f"\nComparaison avec max() :")
print(f"Built-in max : {max_builtin}")
print(f"Notre fonction : {max_notre}")
print(f"Identiques : {max_builtin == max_notre}")
```

**Explication** :
- **Paramètres variables** : *nombres pour nombre indéterminé
- **Initialisation** : premier élément comme candidat
- **Comparaison** : test de chaque élément
- **Équivalence** : même résultat que max()

**Test** : max(5, 3, 8, 1) = 8.

---

### Exercice 268 : Trouver le minimum de plusieurs nombres
**Objectif** : Trouver le plus petit nombre parmi plusieurs valeurs.

```python
# Solution
def minimum(*nombres):
    """Trouve le minimum de plusieurs nombres"""
    if not nombres:
        return None

    min_val = nombres[0]
    for nombre in nombres[1:]:
        if nombre < min_val:
            min_val = nombre

    return min_val

# Tests
print("Tests de minimum :")
print(f"min(5, 3, 8, 1) = {minimum(5, 3, 8, 1)}")
print(f"min(10, 20, 30) = {minimum(10, 20, 30)}")
print(f"min(-5, -1, -10) = {minimum(-5, -1, -10)}")
print(f"min(42) = {minimum(42)}")

# Comparaison avec built-in
nombres_aleatoires = [random.randint(1, 100) for _ in range(10)]
min_builtin = min(nombres_aleatoires)
min_notre = minimum(*nombres_aleatoires)
print(f"\nComparaison avec min() :")
print(f"Built-in min : {min_builtin}")
print(f"Notre fonction : {min_notre}")
print(f"Identiques : {min_builtin == min_notre}")
```

**Explication** :
- **Logique symétrique** : < au lieu de >
- **Initialisation identique** : premier élément
- **Pattern** : même structure que maximum
- **Utilité** : recherche de valeurs minimales

**Test** : min(5, 3, 8, 1) = 1.

---

### Exercice 269 : Calculer la moyenne d'une liste de nombres
**Objectif** : Calculer la moyenne arithmétique d'une liste.

```python
# Solution
def moyenne(nombres):
    """Calcule la moyenne d'une liste de nombres"""
    if not nombres:
        return 0

    return sum(nombres) / len(nombres)

# Tests
listes_test = [
    [1, 2, 3, 4, 5],
    [10, 20, 30, 40, 50],
    [15, 25, 35],
    [],
    [42]
]

print("Calculs de moyenne :")
for i, liste in enumerate(listes_test):
    resultat = moyenne(liste)
    print(f"Liste {i+1} {liste} : moyenne = {resultat:.2f}")

# Comparaison avec statistics.mean
import statistics
print("\nComparaison avec statistics.mean :")
for liste in listes_test:
    if liste:  # statistics.mean ne gère pas les listes vides
        stats_mean = statistics.mean(liste)
        notre_mean = moyenne(liste)
        print(f"statistics.mean : {stats_mean:.2f}, notre fonction : {notre_mean:.2f}, identique : {stats_mean == notre_mean}")
```

**Explanation** :
- **Formule** : moyenne = somme / effectif
- **Gestion liste vide** : retourne 0
- **Précision** : division flottante
- **Alternative** : statistics.mean() plus robuste

**Test** : [1, 2, 3, 4, 5] → 3.00.

---

### Exercice 270 : Calculer la variance d'une liste
**Objectif** : Calculer la variance statistique d'une liste.

```python
# Solution
def variance(nombres):
    """Calcule la variance d'une liste de nombres"""
    if len(nombres) < 2:
        return 0

    # Moyenne
    moyenne_val = sum(nombres) / len(nombres)

    # Somme des écarts au carré
    somme_ecarts = sum((x - moyenne_val) ** 2 for x in nombres)

    # Variance = somme_ecarts / (n-1) pour l'échantillon
    return somme_ecarts / (len(nombres) - 1)

# Tests
listes_test = [
    [1, 2, 3, 4, 5],
    [10, 10, 10, 10, 10],
    [2, 4, 6, 8, 10],
    [5, 15, 25, 35, 45]
]

print("Calculs de variance :")
for i, liste in enumerate(listes_test):
    resultat = variance(liste)
    print(f"Liste {i+1} {liste} : variance = {resultat:.2f}")

# Comparaison avec statistics.variance
import statistics
print("\nComparaison avec statistics.variance :")
for liste in listes_test:
    if len(liste) >= 2:  # statistics.variance nécessite au moins 2 valeurs
        stats_var = statistics.variance(liste)
        notre_var = variance(liste)
        print(f"statistics.variance : {stats_var:.2f}, notre fonction : {notre_var:.2f}, identique : {abs(stats_var - notre_var) < 1e-10}")
```

**Explication** :
- **Formule** : variance = Σ(xi - μ)² / (n-1)
- **Écart-type échantillon** : diviseur n-1
- **Moyenne** : μ calculée d'abord
- **Applications** : mesure de dispersion

**Test** : [1, 2, 3, 4, 5] → variance = 2.50.

---

## 🔍 Points Clés à Retenir

### 1. **Statistiques de Base**
```python
def moyenne(nombres):
    return sum(nombres) / len(nombres) if nombres else 0

def variance(nombres):
    if len(nombres) < 2:
        return 0
    moy = moyenne(nombres)
    return sum((x - moy)**2 for x in nombres) / (len(nombres) - 1)

def ecart_type(nombres):
    return variance(nombres)**0.5
```

### 2. **Somme des Chiffres**
```python
def somme_chiffres(n):
    if n < 0:
        n = -n
    somme = 0
    while n > 0:
        somme += n % 10
        n = n // 10
    return somme
```

### 3. **Min/Max avec *args**
```python
def maximum(*nombres):
    if not nombres:
        return None
    max_val = nombres[0]
    for nombre in nombres[1:]:
        if nombre > max_val:
            max_val = nombre
    return max_val

def minimum(*nombres):
    if not nombres:
        return None
    min_val = nombres[0]
    for nombre in nombres[1:]:
        if nombre < min_val:
            min_val = nombre
    return min_val
```

## 💡 Optimisations et Astuces

### 1. **Statistiques avec NumPy (si disponible)**
```python
# Si numpy est installé
import numpy as np

def stats_numpy(nombres):
    array = np.array(nombres)
    return {
        "moyenne": np.mean(array),
        "variance": np.var(array, ddof=1),  # ddof=1 pour échantillon
        "ecart_type": np.std(array, ddof=1),
        "minimum": np.min(array),
        "maximum": np.max(array)
    }
```

### 2. **Médiane**
```python
def mediane(nombres):
    if not nombres:
        return None

    nombres_tries = sorted(nombres)
    n = len(nombres_tries)

    if n % 2 == 0:
        # Médiane = moyenne des deux valeurs centrales
        return (nombres_tries[n//2 - 1] + nombres_tries[n//2]) / 2
    else:
        # Médiane = valeur centrale
        return nombres_tries[n//2]
```

### 3. **Mode (valeur la plus fréquente)**
```python
from collections import Counter

def mode(nombres):
    if not nombres:
        return None

    compteur = Counter(nombres)
    max_freq = max(compteur.values())
    modes = [nombre for nombre, freq in compteur.items() if freq == max_freq]

    return modes[0] if len(modes) == 1 else modes
```

## 🚀 Applications Pratiques

### 1. **Analyseur de Notes**
```python
def analyser_notes(notes):
    """Analyse complète des notes d'étudiants"""
    if not notes:
        return "Aucune note"

    analyses = {
        "nombre_etudiants": len(notes),
        "moyenne": moyenne(notes),
        "mediane": mediane(notes),
        "ecart_type": ecart_type(notes),
        "minimum": min(notes),
        "maximum": max(notes),
        "repartition": {
            "tres_bien": len([n for n in notes if n >= 16]),
            "bien": len([n for n in notes if 14 <= n < 16]),
            "assez_bien": len([n for n in notes if 12 <= n < 14]),
            "passable": len([n for n in notes if 10 <= n < 12]),
            "insuffisant": len([n for n in notes if n < 10])
        }
    }

    return analyses

# Test
notes_etudiants = [12, 15, 8, 18, 14, 9, 16, 11, 19, 13, 17, 10]
analyse = analyser_notes(notes_etudiants)

print("Analyse des notes :")
for cle, valeur in analyse.items():
    if cle == "repartition":
        print("Répartition :")
        for niveau, nombre in valeur.items():
            print(f"  {niveau}: {nombre}")
    else:
        print(f"{cle}: {valeur}")
```

### 2. **Simulateur de Dés**
```python
def simulateur_des(nb_lancers=1000, nb_faces=6):
    """Simule des lancers de dés"""
    import random

    resultats = [random.randint(1, nb_faces) for _ in range(nb_lancers)]

    # Analyse des résultats
    frequences = {}
    for resultat in resultats:
        frequences[resultat] = frequences.get(resultat, 0) + 1

    # Probabilités théoriques
    proba_theorique = 1 / nb_faces

    print(f"Simulation de {nb_lancers} lancers de dé à {nb_faces} faces :")
    print(f"Probabilité théorique par face : {proba_theorique:.3f}")

    print("\nRésultats observés :")
    for face in range(1, nb_faces + 1):
        freq = frequences.get(face, 0)
        proba_observe = freq / nb_lancers
        ecart = abs(proba_observe - proba_theorique) / proba_theorique * 100

        print(f"Face {face}: {freq"4d"} fois ({proba_observe".3f"}) - Écart: {ecart".1f"}%")

    return resultats

# Test
resultats_des = simulateur_des(10000, 6)
```

### 3. **Estimateur de π par Monte Carlo**
```python
def estimer_pi(nb_points=1000000):
    """Estime π par la méthode de Monte Carlo"""
    import random

    points_dans_cercle = 0

    for _ in range(nb_points):
        # Point aléatoire dans le carré [-1, 1] × [-1, 1]
        x = random.uniform(-1, 1)
        y = random.uniform(-1, 1)

        # Test si le point est dans le cercle unitaire
        if x**2 + y**2 <= 1:
            points_dans_cercle += 1

    # Estimation de π : 4 × (points dans cercle / points totaux)
    pi_estime = 4 * points_dans_cercle / nb_points

    print(f"Estimation de π avec {nb_points} points :")
    print(f"Points dans le cercle : {points_dans_cercle}")
    print(f"π ≈ {pi_estime:.6f}")
    print(f"Écart avec π réel : {abs(pi_estime - 3.1415926535):.6f}")

    return pi_estime

# Test
pi_estime = estimer_pi(1000000)
```

## 🎯 Défis Supplémentaires

1. **Calculez** l'écart-type d'une liste de nombres
2. **Implémentez** un estimateur de π plus précis avec plus de points
3. **Créez** un simulateur de distribution normale
4. **Développez** un analyseur de corrélation entre deux listes

---

**Exercices complétés : 270/285** 🎯

*Continuez avec le [chapitre suivant](7-3-chaines.md) pour les chaînes et cryptographie !*
