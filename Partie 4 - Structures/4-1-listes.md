# Partie 4.1 : Listes et Compréhensions

## 🎯 Objectifs Pédagogiques

Ce chapitre approfondit les **listes** en Python, structures de données fondamentales. Nous explorerons les opérations avancées, les compréhensions, et les applications pratiques.

### Concepts Abordés
- **Manipulation avancée** : ajout, suppression, modification
- **Compréhensions de liste** : syntaxe concise et puissante
- **Filtres et transformations** : conditions et expressions
- **Applications pratiques** : tri, recherche, génération

---

## 📝 Exercices Pratiques

### Exercice 151 : Créer une liste et y ajouter des éléments
**Objectif** : Créer une liste vide et y ajouter des éléments un par un.

```python
# Solution
ma_liste = []

# Ajout d'éléments
ma_liste.append("Python")
ma_liste.append("Java")
ma_liste.append("JavaScript")
ma_liste.append("C++")

print(f"Liste créée : {ma_liste}")
print(f"Longueur : {len(ma_liste)}")

# Ajout de différents types
ma_liste.append(42)
ma_liste.append(3.14)
ma_liste.append(True)

print(f"Liste avec types mixtes : {ma_liste}")
print(f"Types des éléments : {[type(x).__name__ for x in ma_liste]}")
```

**Explication** :
- **Création vide** : [] pour liste vide
- **.append()** : ajout en fin de liste
- **Types mixtes** : Python autorise tout
- **Croissance** : taille dynamique

**Test** : ["Python", "Java", "JavaScript", "C++", 42, 3.14, True].

---

### Exercice 152 : Supprimer un élément d'une liste
**Objectif** : Supprimer des éléments spécifiques d'une liste.

```python
# Solution
nombres = [1, 2, 3, 4, 5, 3, 6, 3]

print(f"Liste originale : {nombres}")

# Supprimer la première occurrence de 3
nombres.remove(3)
print(f"Après suppression première 3 : {nombres}")

# Supprimer toutes les occurrences de 3
while 3 in nombres:
    nombres.remove(3)
print(f"Après suppression de toutes les 3 : {nombres}")

# Supprimer par index
nombres.pop(0)  # Supprime le premier élément
print(f"Après pop(0) : {nombres}")

nombres.pop()   # Supprime le dernier élément
print(f"Après pop() : {nombres}")
```

**Explication** :
- **.remove()** : supprime par valeur (première occurrence)
- **Boucle while** : pour supprimer toutes les occurrences
- **.pop()** : supprime par index (retourne la valeur)
- **.pop() sans argument** : supprime le dernier

**Test** : [1, 2, 3, 4, 5, 3, 6, 3] → suppression progressive.

---

### Exercice 153 : Inverser une liste
**Objectif** : Inverser l'ordre des éléments d'une liste.

```python
# Solution
nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

print(f"Original : {nombres}")

# Méthode 1 : slicing
inverse1 = nombres[::-1]
print(f"Inverse (slicing) : {inverse1}")

# Méthode 2 : reverse() en place
nombres.reverse()
print(f"Inverse (reverse) : {nombres}")

# Méthode 3 : reversed() (itérateur)
inverse3 = list(reversed(nombres))
print(f"Inverse (reversed) : {inverse3}")

# Vérification que slicing ne modifie pas l'original
print(f"Original après slicing : {nombres}")
```

**Explication** :
- **[::-1]** : slicing d'inversion
- **.reverse()** : inversion en place (modifie l'original)
- **reversed()** : itérateur d'inversion (nouvelle liste)
- **Performance** : slicing et reversed() plus efficaces

**Test** : [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] → [10, 9, 8, 7, 6, 5, 4, 3, 2, 1].

---

### Exercice 154 : Trier une liste par ordre croissant
**Objectif** : Trier une liste de nombres par ordre croissant.

```python
# Solution
nombres = [64, 34, 25, 12, 22, 11, 90]

print(f"Avant tri : {nombres}")

# Tri en place
nombres.sort()
print(f"Après tri croissant : {nombres}")

# Tri avec sorted() (nouvelle liste)
nombres_desord = [64, 34, 25, 12, 22, 11, 90]
nombres_tries = sorted(nombres_desord)
print(f"Original : {nombres_desord}")
print(f"Trié (sorted) : {nombres_tries}")

# Tri de chaînes
langages = ["Python", "Java", "javascript", "C++", "ruby"]
langages.sort()
print(f"Langages triés : {langages}")
```

**Explication** :
- **.sort()** : tri en place (modifie la liste)
- **sorted()** : tri avec nouvelle liste
- **Ordre naturel** : numérique ou alphabétique
- **Case sensitive** : majuscules avant minuscules

**Test** : [64, 34, 25, 12, 22, 11, 90] → [11, 12, 22, 25, 34, 64, 90].

---

### Exercice 155 : Trier une liste par ordre décroissant
**Objectif** : Trier une liste de nombres par ordre décroissant.

```python
# Solution
nombres = [64, 34, 25, 12, 22, 11, 90]

print(f"Avant tri : {nombres}")

# Tri décroissant en place
nombres.sort(reverse=True)
print(f"Après tri décroissant : {nombres}")

# Tri décroissant avec sorted()
nombres_desord = [64, 34, 25, 12, 22, 11, 90]
nombres_tries_dec = sorted(nombres_desord, reverse=True)
print(f"Original : {nombres_desord}")
print(f"Trié décroissant (sorted) : {nombres_tries_dec}")

# Tri de chaînes décroissant
langages = ["Python", "Java", "javascript", "C++", "ruby"]
langages.sort(reverse=True)
print(f"Langages triés décroissant : {langages}")
```

**Explication** :
- **reverse=True** : paramètre pour ordre inverse
- **Équivalence** : sort(reverse=True) = sorted()[::-1]
- **Performance** : même efficacité que le tri croissant
- **Applications** : classements, priorités

**Test** : [64, 34, 25, 12, 22, 11, 90] → [90, 64, 34, 25, 22, 12, 11].

---

### Exercice 156 : Fusionner deux listes
**Objectif** : Fusionner deux listes en une seule.

```python
# Solution
liste1 = [1, 2, 3, 4, 5]
liste2 = [6, 7, 8, 9, 10]

fusion = liste1 + liste2  # Concaténation
print(f"Liste 1 : {liste1}")
print(f"Liste 2 : {liste2}")
print(f"Fusion : {fusion}")
```

**Explication** :
- **Opérateur +** : concaténation de listes
- **Nouvelles listes** : liste1 et liste2 préservées
- **Ordre** : éléments de liste1 puis liste2

**Test** : [1, 2, 3, 4, 5] + [6, 7, 8, 9, 10] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10].

---

### Exercice 157 : Créer une compréhension de liste
**Objectif** : Créer une compréhension de liste pour générer des carrés.

```python
# Solution
# Compréhension simple
carres = [x**2 for x in range(1, 11)]
print(f"Carrés de 1 à 10 : {carres}")

# Compréhension avec condition
pairs = [x for x in range(1, 21) if x % 2 == 0]
print(f"Nombres pairs 1-20 : {pairs}")

# Compréhension avec transformation conditionnelle
pairs_ou_triples = [x*2 if x % 2 == 0 else x*3 for x in range(1, 11)]
print(f"Doubles des pairs, triples des impairs : {pairs_ou_triples}")

# Compréhension imbriquée
coordonnees = [(x, y) for x in range(3) for y in range(3)]
print(f"Coordonnées 3x3 : {coordonnees}")
```

**Explication** :
- **Syntaxe** : [expression for variable in sequence if condition]
- **Conciseness** : remplace les boucles for
- **Lisibilité** : claire pour les transformations simples
- **Imbriquée** : boucles multiples

**Test** : [1, 4, 9, 16, 25, 36, 49, 64, 81, 100].

---

### Exercice 158 : Créer une compréhension de dictionnaire
**Objectif** : Créer une compréhension de dictionnaire pour associer nombres et carrés.

```python
# Solution
# Dictionnaire nombre -> carré
carres_dict = {x: x**2 for x in range(1, 11)}
print(f"Carrés (dict) : {carres_dict}")

# Dictionnaire avec condition
pairs_dict = {x: x*2 for x in range(1, 11) if x % 2 == 0}
print(f"Doubles des pairs (dict) : {pairs_dict}")

# Inversion d'un dictionnaire existant
original = {"a": 1, "b": 2, "c": 3}
inverse = {v: k for k, v in original.items()}
print(f"Original : {original}")
print(f"Inverse : {inverse}")

# Dictionnaire avec transformation
langages = ["Python", "Java", "JavaScript"]
longueurs = {langage: len(langage) for langage in langages}
print(f"Longueurs : {longueurs}")
```

**Explication** :
- **Syntaxe** : {clé: valeur for variable in sequence if condition}
- **Applications** : mapping, indexation
- **Inversion** : échange clés-valeurs
- **Transformation** : calculs sur les valeurs

**Test** : {1: 1, 2: 4, 3: 9, 4: 16, 5: 25, ...}.

---

### Exercice 159 : Créer une compréhension d'ensemble
**Objectif** : Créer une compréhension d'ensemble pour obtenir des valeurs uniques.

```python
# Solution
# Ensemble de carrés
carres_set = {x**2 for x in range(1, 11)}
print(f"Carrés (set) : {carres_set}")

# Ensemble avec condition
pairs_set = {x for x in range(1, 21) if x % 2 == 0}
print(f"Pairs (set) : {pairs_set}")

# Suppression des doublons d'une liste
nombres_avec_doublons = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
uniques = {x for x in nombres_avec_doublons}
print(f"Avec doublons : {nombres_avec_doublons}")
print(f"Uniques (set) : {uniques}")

# Ensemble de longueurs
mots = ["Python", "Java", "JavaScript", "C++", "Ruby"]
longueurs_set = {len(mot) for mot in mots}
print(f"Longueurs des mots : {longueurs_set}")
```

**Explication** :
- **Syntaxe** : {expression for variable in sequence if condition}
- **Unicité** : suppression automatique des doublons
- **Applications** : déduplication, valeurs distinctes
- **Performance** : ensembles optimisés pour l'unicité

**Test** : {1, 2, 2, 3, 3, 3} → {1, 2, 3}.

---

### Exercice 160 : Filtrer une liste avec compréhension
**Objectif** : Filtrer une liste pour ne garder que les nombres positifs.

```python
# Solution
nombres = [-5, 10, -3, 8, 0, 15, -7, 25, -1, 12]

# Filtrage positif
positifs = [x for x in nombres if x > 0]
print(f"Positifs : {positifs}")

# Filtrage négatif
negatifs = [x for x in nombres if x < 0]
print(f"Négatifs : {negatifs}")

# Filtrage par plage
dans_plage = [x for x in nombres if 5 <= x <= 20]
print(f"Entre 5 et 20 : {dans_plage}")

# Filtrage par type
mixte = [1, "deux", 3.14, True, None, [5, 6]]
entiers = [x for x in mixte if isinstance(x, int)]
print(f"Entiers : {entiers}")
```

**Explication** :
- **Condition if** : filtrage intégré
- **Opérateurs** : >, <, ==, in, isinstance
- **Plages** : <= et >= pour les intervalles
- **Types** : isinstance() pour filtrer par type

**Test** : [-5, 10, -3, 8, 0, 15, -7, 25, -1, 12] → positifs: [10, 8, 15, 25, 12].

---

## 🔍 Points Clés à Retenir

### 1. **Manipulation de Listes**
```python
# Ajout d'éléments
liste.append(element)      # Ajout en fin
liste.insert(index, element)  # Insertion à un index
liste.extend([a, b, c])    # Ajout de plusieurs éléments

# Suppression d'éléments
liste.remove(element)      # Supprime première occurrence
liste.pop(index)          # Supprime par index
liste.clear()             # Vide la liste

# Recherche et test
element in liste          # Test d'appartenance
liste.index(element)      # Premier index
liste.count(element)      # Nombre d'occurrences
```

### 2. **Tri et Inversement**
```python
# Tri
liste.sort()                   # Tri en place croissant
liste.sort(reverse=True)       # Tri en place décroissant
sorted(liste)                  # Nouvelle liste triée

# Inversement
liste.reverse()                # Inversion en place
list(reversed(liste))          # Nouvelle liste inversée
liste[::-1]                    # Inversion par slicing
```

### 3. **Compréhensions**
```python
# Liste
carres = [x**2 for x in range(10)]

# Dictionnaire
mapping = {x: x**2 for x in range(10)}

# Ensemble
uniques = {x**2 for x in range(10)}

# Avec conditions
pairs = [x for x in range(20) if x % 2 == 0]
positifs = [x for x in nombres if x > 0]
```

### 4. **Slicing Avancé**
```python
liste = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

# Syntaxe : [début:fin:pas]
liste[2:7]      # [2, 3, 4, 5, 6] indices 2 à 6
liste[:5]       # [0, 1, 2, 3, 4] du début à 4
liste[5:]       # [5, 6, 7, 8, 9] de 5 à la fin
liste[::2]      # [0, 2, 4, 6, 8] un élément sur deux
liste[::-1]     # [9, 8, 7, 6, 5, 4, 3, 2, 1, 0] inversion

# Modification par slicing
liste[2:5] = [20, 30, 40]  # Remplacement
```

## 💡 Optimisations et Astuces

### 1. **Compréhensions vs Boucles**
```python
# Boucle classique (plus verbeuse)
pairs = []
for nombre in nombres:
    if nombre % 2 == 0:
        pairs.append(nombre)

# Compréhension (plus concise)
pairs = [nombre for nombre in nombres if nombre % 2 == 0]

# Avantages de la compréhension :
# - Plus lisible
# - Plus efficace (implémentation optimisée)
# - Expression directe de l'intention
```

### 2. **Compréhensions Imbriquées**
```python
# Matrices 2D
matrice = [[i + j for j in range(3)] for i in range(3)]
# [[0, 1, 2], [1, 2, 3], [2, 3, 4]]

# Coordonnées
points = [(x, y) for x in range(3) for y in range(3)]
# [(0, 0), (0, 1), (0, 2), (1, 0), (1, 1), (1, 2), (2, 0), (2, 1), (2, 2)]

# Produit cartésien
combinaisons = [(a, b) for a in ["A", "B"] for b in [1, 2]]
# [('A', 1), ('A', 2), ('B', 1), ('B', 2)]
```

### 3. **Fonctions avec Listes**
```python
# Appliquer une fonction à tous les éléments
def appliquer_fonction(liste, fonction):
    return [fonction(x) for x in liste]

# Exemples d'usage
nombres = [1, 2, 3, 4, 5]
doubles = appliquer_fonction(nombres, lambda x: x * 2)
carres = appliquer_fonction(nombres, lambda x: x ** 2)
longueurs = appliquer_fonction(["hello", "world", "python"], len)
```

## 🚀 Applications Pratiques

### 1. **Traitement de Données**
```python
def nettoyer_et_analyser(donnees):
    """Nettoie et analyse une liste de données"""
    # Nettoyage
    nettoyees = [x for x in donnees if x is not None and x != ""]

    # Analyses
    analyses = {
        "original": len(donnees),
        "nettoye": len(nettoyees),
        "uniques": len(set(nettoyees)),
        "numeriques": [x for x in nettoyees if isinstance(x, (int, float))],
        "textes": [x for x in nettoyees if isinstance(x, str)],
        "longueurs": [len(str(x)) for x in nettoyees]
    }

    # Statistiques sur les numériques
    if analyses["numeriques"]:
        analyses["stats_num"] = {
            "somme": sum(analyses["numeriques"]),
            "moyenne": sum(analyses["numeriques"]) / len(analyses["numeriques"]),
            "positifs": [x for x in analyses["numeriques"] if x > 0],
            "pairs": [x for x in analyses["numeriques"] if x % 2 == 0]
        }

    return analyses

# Test
donnees_sales = [1, None, "hello", "", 2, 3.14, "world", 0, -5, "python", None]
resultat = nettoyer_et_analyser(donnees_sales)
for cle, valeur in resultat.items():
    print(f"{cle}: {valeur}")
```

### 2. **Génération de Patterns**
```python
def generer_patterns(taille):
    """Génère différents patterns avec des listes"""
    patterns = {}

    # Pattern 1 : Carrés
    patterns["carres"] = [x**2 for x in range(1, taille + 1)]

    # Pattern 2 : Nombres pairs et impairs alternés
    patterns["alternes"] = [x if x % 2 == 0 else -x for x in range(1, taille + 1)]

    # Pattern 3 : Triangulaire (somme cumulée)
    patterns["triangulaire"] = [sum(range(1, x + 1)) for x in range(1, taille + 1)]

    # Pattern 4 : Fibonacci
    fib = [0, 1]
    [fib.append(fib[-1] + fib[-2]) for _ in range(2, taille)]
    patterns["fibonacci"] = fib[:taille]

    # Pattern 5 : Nombres premiers
    def est_premier(n):
        return n > 1 and all(n % i != 0 for i in range(2, int(n**0.5) + 1))

    patterns["premiers"] = [x for x in range(2, taille + 2) if est_premier(x)]

    return patterns

# Test
patterns = generer_patterns(10)
for nom, valeurs in patterns.items():
    print(f"{nom}: {valeurs}")
```

### 3. **Analyseur de Texte**
```python
def analyser_texte(texte):
    """Analyse complète d'un texte"""
    # Préparation
    mots = texte.lower().replace(".", "").replace(",", "").replace("!", "").replace("?", "").split()

    # Analyses
    analyses = {
        "texte_original": texte,
        "nombre_mots": len(mots),
        "mots_uniques": list(set(mots)),
        "longueur_moyenne": sum(len(mot) for mot in mots) / len(mots) if mots else 0,
        "mots_longs": [mot for mot in mots if len(mot) > 5],
        "mots_courts": [mot for mot in mots if len(mot) <= 3],
        "frequences": {mot: mots.count(mot) for mot in set(mots)},
        "mots_tries_par_longueur": sorted(mots, key=len),
        "mots_tries_par_frequence": sorted(set(mots), key=lambda mot: mots.count(mot), reverse=True)
    }

    return analyses

# Test
texte_test = "Le Python est un langage de programmation très puissant et polyvalent. Python est facile à apprendre et à utiliser."
analyse = analyser_texte(texte_test)
for cle, valeur in analyse.items():
    print(f"{cle}: {valeur}")
    print()
```

## 🎯 Défis Supplémentaires

1. **Créez** une fonction qui génère une liste de nombres premiers
2. **Implémentez** un tri personnalisé (par longueur de chaîne)
3. **Développez** un système de filtrage multiple (pairs ET positifs ET < 100)
4. **Concevez** une fonction pour aplatir une liste de listes

---

**Exercices complétés : 160/200** 🎯

*Continuez avec le [chapitre suivant](4-2-tuples.md) pour explorer les tuples !*