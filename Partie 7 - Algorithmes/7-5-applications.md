# Partie 7.5 : Applications Finales

## 🎯 Objectifs Pédagogiques

Ce chapitre final de la Partie 7 présente des **applications intégrées** combinant tous les concepts algorithmiques : nombres, statistiques, chaînes, cryptographie et opérations binaires.

### Concepts Intégrés
- **Applications complexes** : puzzles, simulations, analyse
- **Algorithmes combinés** : recherche, tri, optimisation
- **Problèmes classiques** : résolution, implémentation
- **Applications** : jeux, simulations, utilitaires

---

## 📝 Exercices Pratiques

### Exercice 281 : Générer tous les nombres premiers jusqu'à n
**Objectif** : Implémenter le crible d'Ératosthène.

```python
# Solution
def crible_eratosthene(n):
    """Génère tous les nombres premiers jusqu'à n"""
    if n < 2:
        return []

    # Initialisation : tous les nombres sont premiers
    premiers = [True] * (n + 1)
    premiers[0] = premiers[1] = False

    # Criblage
    for i in range(2, int(n**0.5) + 1):
        if premiers[i]:
            # Marquer tous les multiples
            for multiple in range(i*i, n + 1, i):
                premiers[multiple] = False

    # Collecte des nombres premiers
    return [i for i in range(2, n + 1) if premiers[i]]

# Tests
print("Nombres premiers jusqu'à 50 :")
premiers_50 = crible_eratosthene(50)
print(premiers_50)
print(f"Nombre de nombres premiers : {len(premiers_50)}")

print("\nNombres premiers jusqu'à 100 :")
premiers_100 = crible_eratosthene(100)
print(f"Nombre de nombres premiers : {len(premiers_100)}")

# Vérification
print("\nVérification avec quelques nombres :")
for nombre in [17, 23, 29, 31, 37]:
    est_premier = nombre in premiers_50
    print(f"{nombre} est premier : {est_premier}")
```

**Explication** :
- **Crible d'Ératosthène** : algorithme classique
- **Complexité** : O(n log log n)
- **Optimisation** : test jusqu'à √n
- **Applications** : cryptographie, factorisation

**Test** : Nombres premiers jusqu'à 50.

---

### Exercice 282 : Calculer la factorielle d'un nombre
**Objectif** : Implémenter le calcul récursif de factorielle.

```python
# Solution
def factoriel_recursif(n):
    """Calcule n! par récursivité"""
    if n <= 1:
        return 1
    return n * factoriel_recursif(n - 1)

def factoriel_iteratif(n):
    """Calcule n! par itération"""
    resultat = 1
    for i in range(2, n + 1):
        resultat *= i
    return resultat

# Tests
nombres_test = [0, 1, 5, 10, 15]

print("Comparaison récursif vs itératif :")
for n in nombres_test:
    rec = factoriel_recursif(n)
    ite = factoriel_iteratif(n)
    print(f"{n}! : récursif = {rec}, itératif = {ite}, identique = {rec == ite}")

# Performance pour de grandes valeurs
import time

print("\nPerformance pour n=20 :")
debut = time.time()
rec_20 = factoriel_recursif(20)
fin = time.time()
print(f"Récursif : {fin - debut:.6f}s = {rec_20}")

debut = time.time()
ite_20 = factoriel_iteratif(20)
fin = time.time()
print(f"Itératif : {fin - debut:.6f}s = {ite_20}")
```

**Explication** :
- **Récursif** : élégant mais limité par la pile
- **Itératif** : plus efficace pour grandes valeurs
- **Cas de base** : 0! = 1! = 1
- **Applications** : combinatoire, probabilités

**Test** : Comparaison des deux méthodes.

---

### Exercice 283 : Calculer la somme des chiffres d'un nombre
**Objectif** : Décomposer un nombre et calculer la somme de ses chiffres.

```python
# Solution
def somme_chiffres(n):
    """Calcule la somme des chiffres d'un nombre"""
    if n < 0:
        n = -n

    somme = 0
    while n > 0:
        somme += n % 10
        n = n // 10

    return somme

# Tests
nombres_test = [123, 456, 789, 1000, 999, 42, 2024]
print("Somme des chiffres :")
for nombre in nombres_test:
    resultat = somme_chiffres(nombre)
    print(f"{nombre} → {resultat}")

# Propriété intéressante : divisibilité par 9
print("\nTest de divisibilité par 9 :")
for nombre in [18, 27, 36, 45, 99, 108, 117]:
    somme = somme_chiffres(nombre)
    divisible_par_9 = nombre % 9 == 0
    somme_div_9 = somme % 9 == 0
    print(f"{nombre} : divisible par 9 = {divisible_par_9}, somme divisible par 9 = {somme_div_9}")
```

**Explication** :
- **Décomposition** : extraction chiffre par chiffre
- **Modulo 10** : dernier chiffre
- **Division entière** : suppression du dernier chiffre
- **Propriété** : nombre divisible par 9 ⇔ somme de ses chiffres divisible par 9

**Test** : 123 → 6, 999 → 27.

---

### Exercice 284 : Trouver le maximum de plusieurs nombres
**Objectif** : Implémenter une fonction de maximum avec paramètres variables.

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
- **Paramètres variables** : *nombres
- **Initialisation** : premier élément
- **Comparaison successive** : test de chaque élément
- **Équivalence** : même résultat que max()

**Test** : max(5, 3, 8, 1) = 8.

---

### Exercice 285 : Calculer la moyenne d'une liste de nombres
**Objectif** : Calculer la moyenne arithmétique d'une liste.

```python
# Solution
def moyenne(nombres):
    """Calcule la moyenne d'une liste"""
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

# Comparaison avec statistics
import statistics
print("\nComparaison avec statistics.mean :")
for liste in listes_test:
    if liste:
        stats_mean = statistics.mean(liste)
        notre_mean = moyenne(liste)
        print(f"statistics : {stats_mean:.2f}, notre fonction : {notre_mean:.2f}, identique : {stats_mean == notre_mean}")
```

**Explication** :
- **Formule** : moyenne = somme / effectif
- **Gestion liste vide** : retourne 0
- **Précision** : division flottante
- **Alternative** : statistics.mean()

**Test** : [1, 2, 3, 4, 5] → 3.00.

---

## 🔍 Points Clés à Retenir

### 1. **Algorithmes Classiques**
```python
# Crible d'Ératosthène
def crible_eratosthene(n):
    premiers = [True] * (n + 1)
    premiers[0] = premiers[1] = False
    for i in range(2, int(n**0.5) + 1):
        if premiers[i]:
            for j in range(i*i, n + 1, i):
                premiers[j] = False
    return [i for i in range(2, n + 1) if premiers[i]]

# Factorielle récursive
def factoriel(n):
    return 1 if n <= 1 else n * factoriel(n - 1)
```

### 2. **Statistiques**
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

### 3. **Cryptographie**
```python
def chiffrer_cesar(texte, decalage=3):
    resultat = ""
    for c in texte:
        if c.isalpha():
            base = ord('A') if c.isupper() else ord('a')
            c_chiffre = chr((ord(c) - base + decalage) % 26 + base)
            resultat += c_chiffre
        else:
            resultat += c
    return resultat
```

### 4. **Opérations Binaires**
```python
# Masques
LIRE = 1 << 0      # 1
ECRIRE = 1 << 1    # 2
EXECUTER = 1 << 2  # 4

# Test de permission
if permissions & LIRE:
    print("Lecture autorisée")
```

## 💡 Optimisations et Astuces

### 1. **Crible Optimisé**
```python
def crible_eratosthene_opt(n):
    """Version optimisée du crible"""
    if n < 2:
        return []

    # Pas besoin de tableau pour n > 2
    premiers = []
    visited = [False] * (n + 1)

    for i in range(2, n + 1):
        if not visited[i]:
            premiers.append(i)
            # Marquer les multiples
            for j in range(i * i, n + 1, i):
                visited[j] = True

    return premiers
```

### 2. **Fibonacci avec Cache**
```python
fib_cache = {0: 0, 1: 1}

def fibonacci_cache(n):
    if n in fib_cache:
        return fib_cache[n]
    fib_cache[n] = fibonacci_cache(n-1) + fibonacci_cache(n-2)
    return fib_cache[n]
```

### 3. **Monte Carlo Plus Précis**
```python
def estimer_pi_precis(nb_points=10000000):
    """Estimation plus précise de π"""
    import random

    points_dans_cercle = 0
    for _ in range(nb_points):
        x = random.uniform(-1, 1)
        y = random.uniform(-1, 1)
        if x*x + y*y <= 1:
            points_dans_cercle += 1

    return 4 * points_dans_cercle / nb_points
```

## 🚀 Applications Pratiques

### 1. **Résolveur de Sudoku**
```python
def resoudre_sudoku(grille):
    """Résout un Sudoku (simplifié - backtracking)"""
    def est_valide(grille, ligne, col, num):
        # Vérification ligne
        for i in range(9):
            if grille[ligne][i] == num:
                return False

        # Vérification colonne
        for i in range(9):
            if grille[i][col] == num:
                return False

        # Vérification sous-grille 3x3
        debut_ligne = (ligne // 3) * 3
        debut_col = (col // 3) * 3
        for i in range(3):
            for j in range(3):
                if grille[debut_ligne + i][debut_col + j] == num:
                    return False

        return True

    def resoudre(grille):
        for ligne in range(9):
            for col in range(9):
                if grille[ligne][col] == 0:
                    for num in range(1, 10):
                        if est_valide(grille, ligne, col, num):
                            grille[ligne][col] = num
                            if resoudre(grille):
                                return True
                            grille[ligne][col] = 0
                    return False
        return True

    # Copie de la grille
    grille_resolue = [ligne[:] for ligne in grille]

    if resoudre(grille_resolue):
        return grille_resolue
    else:
        return None

# Test avec un Sudoku simple (exemple)
sudoku_simple = [
    [5, 3, 0, 0, 7, 0, 0, 0, 0],
    [6, 0, 0, 1, 9, 5, 0, 0, 0],
    [0, 9, 8, 0, 0, 0, 0, 6, 0],
    [8, 0, 0, 0, 6, 0, 0, 0, 3],
    [4, 0, 0, 8, 0, 3, 0, 0, 1],
    [7, 0, 0, 0, 2, 0, 0, 0, 6],
    [0, 6, 0, 0, 0, 0, 2, 8, 0],
    [0, 0, 0, 4, 1, 9, 0, 0, 5],
    [0, 0, 0, 0, 8, 0, 0, 7, 9]
]

print("Sudoku à résoudre :")
for ligne in sudoku_simple:
    print(ligne)

solution = resoudre_sudoku(sudoku_simple)
if solution:
    print("\nSolution trouvée :")
    for ligne in solution:
        print(ligne)
else:
    print("\nPas de solution trouvée")
```

### 2. **Simulateur de Population**
```python
def simulateur_population(population_initiale, taux_croissance, annees):
    """Simule l'évolution d'une population"""
    population = population_initiale

    print(f"Simulation de population sur {annees} ans :")
    print(f"Population initiale : {population}")

    for annee in range(1, annees + 1):
        population = int(population * (1 + taux_croissance))
        if annee <= 10 or annee % 10 == 0:  # Affichage sélectif
            print(f"Année {annee} : {population} individus")

    return population

# Test
pop_finale = simulateur_population(1000, 0.05, 50)
print(f"Population finale : {pop_finale}")
```

### 3. **Analyseur de Performances**
```python
def analyser_performances():
    """Analyse les performances des algorithmes"""
    import time
    import random

    # Génération de données de test
    tailles = [100, 1000, 10000]
    resultats = {}

    for taille in tailles:
        donnees = list(range(taille))

        # Test de tri
        donnees_copy = donnees[:]
        debut = time.time()
        sorted(donnees_copy)
        tri_time = time.time() - debut

        # Test de recherche
        element = random.choice(donnees)
        debut = time.time()
        element in donnees
        recherche_time = time.time() - debut

        resultats[taille] = {
            "tri": tri_time,
            "recherche": recherche_time
        }

    print("Analyse de performances :")
    print("Taille | Tri (s) | Recherche (s)")
    print("-" * 30)
    for taille, temps in resultats.items():
        print(f"{taille"6d"} | {temps['tri']".6f"} | {temps['recherche']".6f"}")

    return resultats

# Test
performances = analyser_performances()
```

## 🎯 Bilan de la Partie 7

### Concepts Maîtrisés
✅ **Nombres et séquences** : premiers, Fibonacci, factorielle
✅ **Statistiques** : moyenne, variance, Monte Carlo
✅ **Chaînes et cryptographie** : distances, César, anagrammes
✅ **Opérations binaires** : ET, OU, XOR, décalages
✅ **Algorithmes classiques** : crible, tri, recherche
✅ **Applications intégrées** : puzzles, simulations, analyse

### Compétences Développées
- **Algorithmique** : conception et implémentation
- **Optimisation** : choix des bonnes structures
- **Analyse** : performances et complexité
- **Applications** : résolution de problèmes réels
- **Mathématiques** : théorie des nombres et probabilités

---

**🏁 FIN DE LA PARTIE 7 - BRAVO !**

**Exercices complétés : 285/285** 🎯

*Félicitations ! Vous avez terminé les algorithmes et mathématiques. Continuez avec la [Partie 8](Partie%208%20-%20Projets/8-1-jeux.md) pour les projets avancés !*
