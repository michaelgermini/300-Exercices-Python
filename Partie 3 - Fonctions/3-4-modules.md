# Partie 3.4 : Modules Standard

## 🎯 Objectifs Pédagogiques

Ce chapitre explore les **modules standard** de Python, qui fournissent des fonctionnalités avancées pour les mathématiques, les dates, la génération aléatoire, et bien d'autres applications.

### Concepts Abordés
- **Module math** : fonctions mathématiques avancées
- **Module random** : génération de nombres aléatoires
- **Module datetime** : manipulation de dates et heures
- **Applications pratiques** : calculs, simulations, formatage temporel

---

## 📝 Exercices Pratiques

### Exercice 131 : Utilisation du module datetime pour afficher date/heure
**Objectif** : Afficher la date et l'heure actuelles.

```python
# Solution
from datetime import datetime

maintenant = datetime.now()
print(f"Date et heure actuelles : {maintenant}")
print(f"Année : {maintenant.year}")
print(f"Mois : {maintenant.month}")
print(f"Jour : {maintenant.day}")
print(f"Heure : {maintenant.hour}")
print(f"Minute : {maintenant.minute}")
print(f"Seconde : {maintenant.second}")

# Formatage personnalisé
print(f"Format ISO : {maintenant.isoformat()}")
print(f"Format court : {maintenant.strftime('%d/%m/%Y %H:%M:%S')}")
```

**Explication** :
- **datetime.now()** : date et heure actuelles
- **Attributs** : .year, .month, .day, .hour, etc.
- **Formatage** : .strftime() pour formats personnalisés
- **Précision** : microsecondes disponibles

**Test** : Affiche la date et heure système actuelles.

---

### Exercice 132 : Fonction décorateur simple
**Objectif** : Créer un décorateur simple qui mesure le temps d'exécution.

```python
# Solution
import time
from functools import wraps

def chronometre(fonction):
    """Décorateur qui mesure le temps d'exécution"""
    @wraps(fonction)
    def wrapper(*args, **kwargs):
        debut = time.time()
        resultat = fonction(*args, **kwargs)
        fin = time.time()
        print(f"Temps d'exécution de {fonction.__name__}: {fin - debut:.4f} secondes")
        return resultat
    return wrapper

# Fonction à décorer
@chronometre
def calcul_lourd(n):
    """Calcule la somme des carrés jusqu'à n"""
    return sum(i**2 for i in range(n))

# Tests
print("Tests avec décorateur chronomètre :")
resultat1 = calcul_lourd(10000)
resultat2 = calcul_lourd(50000)
print(f"Résultat 1: {resultat1}")
print(f"Résultat 2: {resultat2}")
```

**Explication** :
- **Décorateur** : fonction qui modifie une autre fonction
- **@wraps** : préserve les métadonnées de la fonction
- **time.time()** : timestamp en secondes
- **Performance** : mesure des temps d'exécution

**Test** : Montre le temps d'exécution de calculs.

---

### Exercice 133 : Fonction décorateur avec argument
**Objectif** : Créer un décorateur qui accepte des arguments.

```python
# Solution
def repeter_executions(n_fois):
    """Décorateur qui exécute une fonction n fois"""
    def decorateur(fonction):
        @wraps(fonction)
        def wrapper(*args, **kwargs):
            resultats = []
            for i in range(n_fois):
                resultat = fonction(*args, **kwargs)
                resultats.append(resultat)
                print(f"Exécution {i+1}/{n_fois}: {resultat}")
            return resultats
        return wrapper
    return decorateur

# Fonction à décorer
@repeter_executions(3)
def lancer_de():
    """Simule un lancer de dé"""
    import random
    return random.randint(1, 6)

# Tests
print("Lancers de dé (3 fois) :")
resultats_des = lancer_de()
print(f"Tous les résultats : {resultats_des}")
```

**Explication** :
- **Décorateur avec paramètres** : fonction qui retourne un décorateur
- **Multiple exécutions** : répétition automatique
- **Collection de résultats** : liste des valeurs retournées
- **Applications** : tests, simulations, moyennes

**Test** : Lance un dé 3 fois et affiche tous les résultats.

---

### Exercice 134 : Fonction pour filtrer les nombres pairs d'une liste
**Objectif** : Créer une fonction qui filtre les nombres pairs.

```python
# Solution
filtrer_pairs = lambda nombres: list(filter(lambda x: x % 2 == 0, nombres))

# Tests
listes_test = [
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    [11, 13, 15, 17, 19],
    [2, 4, 6, 8, 10, 12],
    []
]

print("Filtrage des nombres pairs :")
for i, liste in enumerate(listes_test):
    pairs = filtrer_pairs(liste)
    print(f"Liste {i+1} : {liste} → pairs: {pairs}")
```

**Explication** :
- **filter()** : fonction built-in de filtrage
- **Lambda condition** : test de parité
- **Conversion liste** : list() pour matérialiser le résultat
- **Efficacité** : lazy evaluation de filter

**Test** : [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] → [2, 4, 6, 8, 10].

---

### Exercice 135 : Fonction pour filtrer les nombres impairs d'une liste
**Objectif** : Créer une fonction qui filtre les nombres impairs.

```python
# Solution
filtrer_impairs = lambda nombres: list(filter(lambda x: x % 2 != 0, nombres))

# Tests
listes_test = [
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    [10, 20, 30, 40, 50],
    [1, 3, 5, 7, 9, 11],
    []
]

print("Filtrage des nombres impairs :")
for i, liste in enumerate(listes_test):
    impairs = filtrer_impairs(liste)
    print(f"Liste {i+1} : {liste} → impairs: {impairs}")
```

**Explication** :
- **Logique inverse** : != 0 pour les impairs
- **Complément** : tout ce qui n'est pas pair
- **Pattern** : même structure que le filtrage pair
- **Utilité** : séparation parité

**Test** : [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] → [1, 3, 5, 7, 9].

---

### Exercice 136 : Fonction pour doubler les éléments d'une liste
**Objectif** : Créer une fonction qui double tous les éléments d'une liste.

```python
# Solution
doubler_elements = lambda nombres: list(map(lambda x: x * 2, nombres))

# Tests
listes_test = [
    [1, 2, 3, 4, 5],
    [10, 20, 30],
    [0, -5, 15],
    []
]

print("Doublage des éléments :")
for i, liste in enumerate(listes_test):
    doubles = doubler_elements(liste)
    print(f"Liste {i+1} : {liste} → doubles: {doubles}")
```

**Explication** :
- **map()** : fonction built-in de transformation
- **Lambda de transformation** : multiplication par 2
- **Application** : à tous les éléments
- **Performance** : lazy evaluation

**Test** : [1, 2, 3, 4, 5] → [2, 4, 6, 8, 10].

---

### Exercice 137 : Fonction pour tripler les éléments d'une liste
**Objectif** : Créer une fonction qui triple tous les éléments d'une liste.

```python
# Solution
tripler_elements = lambda nombres: [x * 3 for x in nombres]

# Tests
listes_test = [
    [1, 2, 3],
    [5, 10],
    [-2, 0, 2],
    []
]

print("Triplage des éléments :")
for i, liste in enumerate(listes_test):
    triples = tripler_elements(liste)
    print(f"Liste {i+1} : {liste} → triples: {triples}")
```

**Explication** :
- **Compréhension** : syntaxe concise et lisible
- **Transformation** : multiplication par 3
- **Alternative** : map() avec lambda
- **Équivalence** : même résultat que map

**Test** : [1, 2, 3] → [3, 6, 9].

---

### Exercice 138 : Fonction pour calculer les carrés des éléments
**Objectif** : Créer une fonction qui calcule les carrés des éléments d'une liste.

```python
# Solution
carres_elements = lambda nombres: [x ** 2 for x in nombres]

# Tests
listes_test = [
    [1, 2, 3, 4, 5],
    [0, 10, -5],
    [2.5, 3.7],
    []
]

print("Carrés des éléments :")
for i, liste in enumerate(listes_test):
    carres = carres_elements(liste)
    print(f"Liste {i+1} : {liste} → carrés: {carres}")
```

**Explication** :
- **Puissance 2** : ** 2 ou pow(x, 2)
- **Types** : fonctionne avec int et float
- **Précision** : flottants préservés
- **Mathématiques** : fonction quadratique

**Test** : [1, 2, 3, 4, 5] → [1, 4, 9, 16, 25].

---

### Exercice 139 : Fonction pour calculer les cubes des éléments
**Objectif** : Créer une fonction qui calcule les cubes des éléments d'une liste.

```python
# Solution
cubes_elements = lambda nombres: [x ** 3 for x in nombres]

# Tests
listes_test = [
    [1, 2, 3],
    [-2, 0, 2],
    [1.5, 2.5],
    []
]

print("Cubes des éléments :")
for i, liste in enumerate(listes_test):
    cubes = cubes_elements(liste)
    print(f"Liste {i+1} : {liste} → cubes: {cubes}")
```

**Explication** :
- **Puissance 3** : ** 3
- **Croissance** : plus rapide que les carrés
- **Nombres négatifs** : cubes négatifs
- **Applications** : volumes, physique

**Test** : [1, 2, 3] → [1, 8, 27], [-2, 0, 2] → [-8, 0, 8].

---

### Exercice 140 : Fonction pour générer une table de multiplication
**Objectif** : Créer une fonction qui génère une table de multiplication.

```python
# Solution
def table_multiplication(n):
    """Génère la table de multiplication de n"""
    return [(i, n, i*n) for i in range(1, 11)]

# Tests
tables = [5, 7, 9, 12]
print("Tables de multiplication :")
for n in tables:
    table = table_multiplication(n)
    print(f"\nTable de {n} :")
    for i, base, resultat in table:
        print(f"{i} × {base} = {resultat}")

# Formatage amélioré
print("
Table de 7 (formatée) :")
for i, base, resultat in table_multiplication(7):
    print(f"{base:2d} × {i:2d} = {resultat:3d}")
```

**Explication** :
- **Tuple** : (multiplicateur, base, résultat)
- **Range 1-10** : table complète
- **Compréhension** : génération concise
- **Formatage** : alignement pour lisibilité

**Test** : Table de 5 : 1×5=5, 2×5=10, ..., 10×5=50.

---

## 🔍 Points Clés à Retenir

### 1. **Modules Import**
```python
# Import complet
import math
resultat = math.sqrt(16)

# Import spécifique
from math import sqrt, pi
resultat = sqrt(16)

# Import avec alias
import math as m
resultat = m.sqrt(16)

# Import multiple
from math import sqrt as racine, pi
resultat = racine(16)
```

### 2. **Module Math**
```python
import math

# Constantes
math.pi    # 3.14159...
math.e     # 2.71828...
math.tau   # 6.28318... (2π)

# Fonctions trigonométriques
math.sin(x), math.cos(x), math.tan(x)
math.asin(x), math.acos(x), math.atan(x)

# Fonctions hyperboliques
math.sinh(x), math.cosh(x), math.tanh(x)

# Exponentielles et logarithmes
math.exp(x)    # e^x
math.log(x)    # ln(x)
math.log10(x)  # log10(x)
math.sqrt(x)   # √x
math.pow(x, y) # x^y

# Fonctions spéciales
math.factorial(n)  # n!
math.gcd(a, b)     # PGCD
```

### 3. **Module Random**
```python
import random

# Nombres aléatoires
random.random()        # Float entre 0 et 1
random.randint(a, b)   # Int entre a et b inclus
random.uniform(a, b)   # Float entre a et b

# Séquences
random.choice(seq)     # Élément aléatoire
random.sample(seq, k)  # k éléments sans remise
random.shuffle(seq)    # Mélange en place

# Distributions
random.gauss(mu, sigma)  # Normale
random.expovariate(lambd)  # Exponentielle
```

### 4. **Module Datetime**
```python
from datetime import datetime, date, time, timedelta

# Date et heure actuelles
maintenant = datetime.now()
aujourdhui = date.today()
heure = datetime.now().time()

# Construction
d = date(2024, 12, 25)
dt = datetime(2024, 12, 25, 15, 30, 45)

# Formatage
dt.strftime("%Y-%m-%d %H:%M:%S")
dt.strftime("%d/%m/%Y")

# Parsing
datetime.strptime("25/12/2024", "%d/%m/%Y")

# Opérations
delta = timedelta(days=7, hours=3)
nouvelle_date = aujourdhui + delta
```

## 💡 Optimisations et Astuces

### 1. **Décorateurs Pratiques**
```python
# Décorateur de logging
def logger(fonction):
    @wraps(fonction)
    def wrapper(*args, **kwargs):
        print(f"Appel de {fonction.__name__} avec args={args}, kwargs={kwargs}")
        resultat = fonction(*args, **kwargs)
        print(f"Résultat: {resultat}")
        return resultat
    return wrapper

# Décorateur de cache
cache = {}

def memoize(fonction):
    @wraps(fonction)
    def wrapper(*args):
        if args in cache:
            return cache[args]
        resultat = fonction(*args)
        cache[args] = resultat
        return resultat
    return wrapper
```

### 2. **Fonctions Built-in avec Modules**
```python
# Au lieu de boucles manuelles
import statistics

# Statistiques
moyenne = statistics.mean(nombres)
mediane = statistics.median(nombres)
ecart_type = statistics.stdev(nombres)

# Collections
from collections import Counter
compte = Counter(nombres)  # Comptage des occurrences

# Itérations
from itertools import combinations, permutations
comb = list(combinations([1, 2, 3], 2))  # [(1, 2), (1, 3), (2, 3)]
perm = list(permutations([1, 2, 3]))     # Toutes les permutations
```

### 3. **Gestion d'Erreurs avec Modules**
```python
import logging

# Configuration du logging
logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

def fonction_sensible():
    try:
        # Code risqué
        resultat = 1 / 0
    except ZeroDivisionError as e:
        logger.error(f"Erreur de division par zéro: {e}")
        return None
    except Exception as e:
        logger.error(f"Erreur inattendue: {e}")
        return None
    else:
        logger.info("Opération réussie")
        return resultat
```

## 🚀 Applications Pratiques

### 1. **Simulateur de Jeu**
```python
def simulateur_loto(tirages=1000):
    """Simule des tirages de loto"""
    import random

    resultats = []
    for _ in range(tirages):
        # 6 numéros entre 1 et 49
        tirage = sorted(random.sample(range(1, 50), 6))
        resultats.append(tirage)

    # Analyse des résultats
    tous_numeros = [num for tirage in resultats for num in tirage]
    from collections import Counter
    frequences = Counter(tous_numeros)

    return {
        "tirages": resultats,
        "frequences": dict(frequences.most_common(10)),
        "plus_sorti": frequences.most_common(1)[0][0] if frequences else None,
        "moins_sorti": frequences.most_common()[-1][0] if frequences else None
    }

# Simulation
simulation = simulateur_loto(10000)
print("Fréquences des 10 numéros les plus sortis:")
for numero, freq in list(simulation["frequences"].items())[:10]:
    pourcentage = (freq / 10000) * 100
    print(f"Numéro {numero}: {freq} fois ({pourcentage:.1f}%)")
```

### 2. **Analyseur de Dates**
```python
def analyseur_dates():
    """Analyse et manipule des dates"""
    from datetime import datetime, timedelta

    # Dates importantes
    maintenant = datetime.now()
    debut_annee = datetime(maintenant.year, 1, 1)
    fin_annee = datetime(maintenant.year, 12, 31, 23, 59, 59)

    # Calculs
    jours_passes = (maintenant - debut_annee).days
    jours_restants = (fin_annee - maintenant).days

    # Prochains anniversaires
    anniversaires = [
        datetime(maintenant.year, 3, 15),    # Date fictive
        datetime(maintenant.year, 7, 22),
        datetime(maintenant.year, 12, 5)
    ]

    prochains_anniv = []
    for anniv in anniversaires:
        if anniv < maintenant:
            anniv = datetime(maintenant.year + 1, anniv.month, anniv.day)
        prochains_anniv.append((anniv - maintenant).days)

    return {
        "maintenant": maintenant,
        "debut_annee": debut_annee,
        "fin_annee": fin_annee,
        "jours_passes": jours_passes,
        "jours_restants": jours_restants,
        "prochains_anniversaires": prochains_anniv
    }

# Test
analyse = analyseur_dates()
print(f"Aujourd'hui: {analyse['maintenant'].strftime('%d/%m/%Y %H:%M')}")
print(f"Jours passés cette année: {analyse['jours_passes']}")
print(f"Jours restants: {analyse['jours_restants']}")
print(f"Prochains anniversaires dans: {analyse['prochains_anniversaires']} jours")
```

### 3. **Calculateur Mathématique**
```python
def calculateur_mathematique(expression):
    """Évalue des expressions mathématiques complexes"""
    import math
    import cmath  # Pour les nombres complexes

    # Fonctions disponibles
    fonctions = {
        "sin": math.sin,
        "cos": math.cos,
        "tan": math.tan,
        "exp": math.exp,
        "log": math.log,
        "sqrt": math.sqrt,
        "pi": math.pi,
        "e": math.e,
        "factorial": math.factorial,
        "gcd": math.gcd,
        "lcm": lambda a, b: (a * b) // math.gcd(a, b)
    }

    try:
        # Remplacement des noms de fonctions par les objets fonction
        for nom, func in fonctions.items():
            if callable(func):
                expression = expression.replace(nom + "(", f"fonctions['{nom}'](")

        # Évaluation sécurisée
        resultat = eval(expression, {"__builtins__": {}}, fonctions)
        return resultat

    except Exception as e:
        return f"Erreur: {e}"

# Tests
expressions = [
    "sin(pi/2)",
    "sqrt(16)",
    "log(e)",
    "factorial(5)",
    "gcd(48, 18)",
    "2 * sin(pi/4) + cos(pi/3)",
    "exp(log(5))",
    "lcm(4, 6)"
]

print("Calculateur mathématique:")
for expr in expressions:
    resultat = calculateur_mathematique(expr)
    print(f"{expr} = {resultat}")
```

## 🎯 Défis Supplémentaires

1. **Créez** un simulateur de météo avec des données aléatoires
2. **Développez** un système de logging pour tracer les exécutions de fonctions
3. **Implémentez** un générateur de mots de passe sécurisés
4. **Concevez** un analyseur de performances pour mesurer les temps d'exécution

---

**Exercices complétés : 140/150** 🎯

*Continuez avec le [chapitre suivant](3-5-applications.md) pour les applications pratiques des fonctions !*