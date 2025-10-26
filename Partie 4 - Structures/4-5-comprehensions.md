# Partie 4.5 : Compréhensions et Matrices

## 🎯 Objectifs Pédagogiques

Ce chapitre final de la Partie 4 explore les **compréhensions avancées** et les **matrices**, concepts puissants pour la manipulation de données complexes et les calculs multidimensionnels.

### Concepts Abordés
- **Compréhensions avancées** : dictionnaires, ensembles, imbrications
- **Matrices** : création, accès, opérations arithmétiques
- **Transformations** : transposition, addition, multiplication
- **Applications** : traitement d'images, calculs scientifiques

---

## 📝 Exercices Pratiques

### Exercice 184 : Doubler les éléments d'une liste avec compréhension
**Objectif** : Utiliser une compréhension pour doubler tous les éléments d'une liste.

```python
# Solution
nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Compréhension simple
doubles = [x * 2 for x in nombres]
print(f"Originaux : {nombres}")
print(f"Doubles : {doubles}")

# Comparaison avec map()
doubles_map = list(map(lambda x: x * 2, nombres))
print(f"Avec map() : {doubles_map}")
print(f"Identiques : {doubles == doubles_map}")

# Compréhension avec condition
pairs_doubles = [x * 2 for x in nombres if x % 2 == 0]
print(f"Doubles des pairs : {pairs_doubles}")

# Compréhension avec transformation conditionnelle
pairs_ou_triples = [x*2 if x % 2 == 0 else x*3 for x in nombres]
print(f"Doubles des pairs, triples des impairs : {pairs_ou_triples}")
```

**Explication** :
- **Syntaxe** : [expression for variable in sequence if condition]
- **Map vs compréhension** : compréhension plus lisible
- **Condition** : filtrage intégré
- **Transformation conditionnelle** : if/else dans l'expression

**Test** : [1, 2, 3, 4, 5] → doubles pairs: [4, 8].

---

### Exercice 185 : Extraire les nombres pairs d'une liste avec compréhension
**Objectif** : Utiliser une compréhension pour filtrer les nombres pairs.

```python
# Solution
nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]

# Compréhension avec condition
pairs = [x for x in nombres if x % 2 == 0]
print(f"Tous les nombres : {nombres}")
print(f"Nombres pairs : {pairs}")

# Comparaison avec filter()
pairs_filter = list(filter(lambda x: x % 2 == 0, nombres))
print(f"Avec filter() : {pairs_filter}")
print(f"Identiques : {pairs == pairs_filter}")

# Compréhension avec condition multiple
pairs_positifs = [x for x in nombres if x % 2 == 0 and x > 0]
print(f"Pairs positifs : {pairs_positifs}")

# Compréhension avec condition complexe
divisibles_3_ou_5 = [x for x in nombres if x % 3 == 0 or x % 5 == 0]
print(f"Divisibles par 3 ou 5 : {divisibles_3_ou_5}")
```

**Explication** :
- **Filtrage** : condition if pour sélection
- **Filter vs compréhension** : compréhension plus concise
- **Conditions multiples** : and, or dans la condition
- **Logique** : expressions booléennes complexes

**Test** : [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12] → pairs: [2, 4, 6, 8, 10, 12].

---

### Exercice 186 : Compter les occurrences d'un élément dans une liste
**Objectif** : Utiliser une compréhension pour compter les occurrences.

```python
# Solution
elements = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4, 5, 5, 5, 5, 5]

# Comptage avec compréhension
occurrences = {x: elements.count(x) for x in set(elements)}
print(f"Occurrences : {occurrences}")

# Comptage manuel avec compréhension
comptage_manuel = {}
for x in elements:
    comptage_manuel[x] = comptage_manuel.get(x, 0) + 1
print(f"Comptage manuel : {comptage_manuel}")

# Comparaison avec Counter
from collections import Counter
counter = Counter(elements)
print(f"Avec Counter : {dict(counter)}")
print(f"Identiques : {occurrences == dict(counter)}")

# Occurrences avec condition
nombres_pairs = [x for x in elements if x % 2 == 0]
occurrences_pairs = {x: nombres_pairs.count(x) for x in set(nombres_pairs)}
print(f"Occurrences des pairs : {occurrences_pairs}")
```

**Explication** :
- **Compréhension dictionnaire** : {clé: valeur for ...}
- **.count()** : méthode de comptage
- **Counter** : classe spécialisée pour le comptage
- **Équivalence** : même résultat, syntaxes différentes

**Test** : {1: 1, 2: 2, 3: 3, 4: 4, 5: 5}.

---

### Exercice 187 : Trouver les indices d'un élément dans une liste
**Objectif** : Utiliser une compréhension pour trouver tous les indices d'un élément.

```python
# Solution
elements = ["a", "b", "c", "a", "d", "a", "e", "a"]

# Indices avec compréhension
indices_a = [i for i, x in enumerate(elements) if x == "a"]
print(f"Indices de 'a' : {indices_a}")

# Indices de tous les éléments
indices_tous = {x: [i for i, val in enumerate(elements) if val == x] for x in set(elements)}
print(f"Indices de tous : {indices_tous}")

# Comparaison avec méthode classique
def trouver_indices_clasique(liste, element):
    indices = []
    for i, x in enumerate(liste):
        if x == element:
            indices.append(i)
    return indices

print(f"Avec fonction classique : {trouver_indices_clasique(elements, 'a')}")
print(f"Identiques : {indices_a == trouver_indices_clasique(elements, 'a')}")

# Indices avec condition multiple
nombres = [1, 2, 3, 2, 4, 2, 5, 2]
indices_pairs = [i for i, x in enumerate(nombres) if x % 2 == 0]
print(f"Indices des nombres pairs : {indices_pairs}")
```

**Explication** :
- **enumerate()** : génère (index, valeur)
- **Compréhension avec enumerate** : accès simultané
- **Dictionnaire d'indices** : mapping élément → indices
- **Applications** : recherche, positionnement

**Test** : indices de "a" : [0, 3, 5, 7].

---

### Exercice 188 : Parcourir une liste avec énumération
**Objectif** : Utiliser enumerate() avec une compréhension pour le parcours indexé.

```python
# Solution
langages = ["Python", "Java", "JavaScript", "C++", "Ruby"]

# Énumération avec compréhension
langages_indexes = [(i, lang) for i, lang in enumerate(langages)]
print(f"Langages avec indices : {langages_indexes}")

# Énumération avec condition
langages_longs = [(i, lang) for i, lang in enumerate(langages) if len(lang) > 4]
print(f"Langages > 4 caractères : {langages_longs}")

# Énumération avec transformation
langages_info = [(i, lang, len(lang)) for i, lang in enumerate(langages)]
print(f"Langages avec longueur : {langages_info}")

# Comparaison avec zip()
indices = list(range(len(langages)))
langages_zip = list(zip(indices, langages))
print(f"Avec zip() : {langages_zip}")
print(f"Avec enumerate() : {langages_indexes}")
print(f"Identiques : {langages_zip == langages_indexes}")
```

**Explication** :
- **enumerate()** : génère (index, valeur) automatiquement
- **Tuple** : (index, valeur) ou (index, valeur, transformation)
- **Condition** : filtrage sur index ou valeur
- **zip()** : alternative pour indexation manuelle

**Test** : [(0, "Python"), (1, "Java"), (2, "JavaScript"), ...].

---

### Exercice 189 : Créer une matrice 2x2
**Objectif** : Créer une matrice 2x2 et accéder à ses éléments.

```python
# Solution
# Matrice 2x2 simple
matrice_2x2 = [
    [1, 2],
    [3, 4]
]

print(f"Matrice 2x2 : {matrice_2x2}")
print(f"Élément [0][0] : {matrice_2x2[0][0]}")
print(f"Élément [0][1] : {matrice_2x2[0][1]}")
print(f"Élément [1][0] : {matrice_2x2[1][0]}")
print(f"Élément [1][1] : {matrice_2x2[1][1]}")

# Matrice identité 2x2
identite_2x2 = [
    [1, 0],
    [0, 1]
]
print(f"Matrice identité 2x2 : {identite_2x2}")

# Matrice avec compréhension
matrice_carres = [[i * j for j in range(1, 3)] for i in range(1, 3)]
print(f"Matrice de carrés : {matrice_carres}")

# Accès avec compréhension
diagonale = [matrice_2x2[i][i] for i in range(2)]
print(f"Diagonale : {diagonale}")

anti_diagonale = [matrice_2x2[i][1-i] for i in range(2)]
print(f"Anti-diagonale : {anti_diagonale}")
```

**Explication** :
- **Liste de listes** : structure de matrice
- **Indexation 2D** : [ligne][colonne]
- **Compréhension 2D** : boucles imbriquées
- **Diagonale** : éléments où i == j
- **Applications** : mathématiques, images, graphes

**Test** : matrice 2x2 = [[1, 2], [3, 4]].

---

### Exercice 190 : Accéder aux éléments d'une matrice
**Objectif** : Accéder et manipuler les éléments d'une matrice.

```python
# Solution
# Matrice 3x3
matrice_3x3 = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

print(f"Matrice 3x3 : {matrice_3x3}")

# Accès à des éléments spécifiques
print(f"Élément central : {matrice_3x3[1][1]}")
print(f"Première ligne : {matrice_3x3[0]}")
print(f"Dernière colonne : {[ligne[2] for ligne in matrice_3x3]}")

# Extraction de sous-matrices
sous_matrice_2x2 = [ligne[:2] for ligne in matrice_3x3[:2]]
print(f"Sous-matrice 2x2 (haut-gauche) : {sous_matrice_2x2}")

# Somme par ligne
sommes_lignes = [sum(ligne) for ligne in matrice_3x3]
print(f"Sommes par ligne : {sommes_lignes}")

# Somme par colonne
sommes_colonnes = [sum(ligne[i] for ligne in matrice_3x3) for i in range(3)]
print(f"Sommes par colonne : {sommes_colonnes}")

# Somme totale
somme_totale = sum(sum(ligne) for ligne in matrice_3x3)
print(f"Somme totale : {somme_totale}")
```

**Explication** :
- **Indexation** : [ligne][colonne] ou [ligne, colonne]
- **Slicing 2D** : extraction de parties
- **Calculs** : sommes par lignes, colonnes
- **Compréhension** : pour les agrégations

**Test** : somme par lignes : [6, 15, 24].

---

### Exercice 191 : Additionner deux matrices
**Objectif** : Additionner deux matrices de même dimension.

```python
# Solution
# Matrices 2x2
matrice_a = [
    [1, 2],
    [3, 4]
]

matrice_b = [
    [5, 6],
    [7, 8]
]

print(f"Matrice A : {matrice_a}")
print(f"Matrice B : {matrice_b}")

# Addition avec compréhension
matrice_somme = [[matrice_a[i][j] + matrice_b[i][j] for j in range(2)] for i in range(2)]
print(f"A + B : {matrice_somme}")

# Vérification avec des valeurs connues
# 1+5=6, 2+6=8, 3+7=10, 4+8=12

# Addition de matrices 3x3
matrice_c = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

matrice_d = [
    [9, 8, 7],
    [6, 5, 4],
    [3, 2, 1]
]

matrice_somme_3x3 = [[matrice_c[i][j] + matrice_d[i][j] for j in range(3)] for i in range(3)]
print(f"Matrice C + D : {matrice_somme_3x3}")

# Fonction générique d'addition
def addition_matrices(mat1, mat2):
    """Additionne deux matrices de même dimension"""
    if len(mat1) != len(mat2) or len(mat1[0]) != len(mat2[0]):
        raise ValueError("Matrices de dimensions différentes")

    return [[mat1[i][j] + mat2[i][j] for j in range(len(mat1[0]))] for i in range(len(mat1))]

print(f"Addition générique : {addition_matrices(matrice_a, matrice_b)}")
```

**Explication** :
- **Dimension identique** : prérequis pour l'addition
- **Compréhension 2D** : boucles imbriquées
- **Fonction générique** : validation et calcul
- **Applications** : traitement d'images, calculs vectoriels

**Test** : [[1, 2], [3, 4]] + [[5, 6], [7, 8]] = [[6, 8], [10, 12]].

---

### Exercice 192 : Multiplier deux matrices
**Objectif** : Multiplier deux matrices compatibles.

```python
# Solution
# Matrices 2x3 et 3x2
matrice_a = [
    [1, 2, 3],
    [4, 5, 6]
]

matrice_b = [
    [7, 8],
    [9, 10],
    [11, 12]
]

print(f"Matrice A (2x3) : {matrice_a}")
print(f"Matrice B (3x2) : {matrice_b}")

# Multiplication manuelle (A * B)
resultat = [
    [sum(matrice_a[0][k] * matrice_b[k][0] for k in range(3)),
     sum(matrice_a[0][k] * matrice_b[k][1] for k in range(3))],
    [sum(matrice_a[1][k] * matrice_b[k][0] for k in range(3)),
     sum(matrice_a[1][k] * matrice_b[k][1] for k in range(3))]
]

print(f"Résultat A × B (2x2) : {resultat}")

# Multiplication avec compréhension
resultat_comprehension = [
    [sum(matrice_a[i][k] * matrice_b[k][j] for k in range(len(matrice_b)))
     for j in range(len(matrice_b[0]))]
    for i in range(len(matrice_a))
]

print(f"Avec compréhension : {resultat_comprehension}")
print(f"Identiques : {resultat == resultat_comprehension}")

# Vérification : 1×7 + 2×9 + 3×11 = 7 + 18 + 33 = 58
#               1×8 + 2×10 + 3×12 = 8 + 20 + 36 = 64
#               4×7 + 5×9 + 6×11 = 28 + 45 + 66 = 139
#               4×8 + 5×10 + 6×12 = 32 + 50 + 72 = 154
```

**Explication** :
- **Dimensions** : (m×n) × (n×p) = (m×p)
- **Calcul** : somme des produits ligne×colonne
- **Compréhension** : boucles pour i, j, k
- **Complexité** : O(n³) pour matrices n×n

**Test** : [[1, 2, 3], [4, 5, 6]] × [[7, 8], [9, 10], [11, 12]] = [[58, 64], [139, 154]].

---

### Exercice 193 : Transposer une matrice
**Objectif** : Transposer une matrice (échange lignes et colonnes).

```python
# Solution
matrice = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

print(f"Matrice originale (3x3) : {matrice}")

# Transposition manuelle
transposee = [
    [matrice[j][i] for j in range(3)]
    for i in range(3)
]

print(f"Matrice transposée : {transposee}")

# Vérification : élément [i][j] devient [j][i]
print(f"Vérification [0][1] = {matrice[0][1]} devient [1][0] = {transposee[1][0]}")
print(f"Vérification [2][1] = {matrice[2][1]} devient [1][2] = {transposee[1][2]}")

# Transposition avec zip()
transposee_zip = [list(ligne) for ligne in zip(*matrice)]
print(f"Avec zip() : {transposee_zip}")
print(f"Identiques : {transposee == transposee_zip}")

# Transposition de matrice rectangulaire
matrice_rect = [
    [1, 2, 3, 4],
    [5, 6, 7, 8]
]

transposee_rect = [list(ligne) for ligne in zip(*matrice_rect)]
print(f"Matrice rectangulaire (2x4) : {matrice_rect}")
print(f"Transposée (4x2) : {transposee_rect}")
```

**Explication** :
- **Transposition** : matrice[i][j] → matrice[j][i]
- **Compréhension** : échange des indices
- **zip(*)** : transposition élégante
- **Applications** : rotations, algèbre linéaire

**Test** : [[1, 2, 3], [4, 5, 6], [7, 8, 9]] → [[1, 4, 7], [2, 5, 8], [3, 6, 9]].

---

### Exercice 194 : Trouver le maximum dans une matrice
**Objectif** : Trouver l'élément maximum d'une matrice.

```python
# Solution
matrice = [
    [15, 3, 9],
    [27, 18, 5],
    [8, 12, 21]
]

print(f"Matrice : {matrice}")

# Maximum avec compréhension
maximum = max(max(ligne) for ligne in matrice)
print(f"Maximum : {maximum}")

# Position du maximum
position_max = None
for i in range(len(matrice)):
    for j in range(len(matrice[i])):
        if matrice[i][j] == maximum:
            position_max = (i, j)
            break
    if position_max:
        break

print(f"Position du maximum : {position_max}")

# Maximum avec énumération
max_avec_enum = max((matrice[i][j], (i, j)) for i in range(len(matrice)) for j in range(len(matrice[i])))
print(f"Maximum avec énumération : {max_avec_enum[0]} en position {max_avec_enum[1]}")

# Tous les éléments
tous_elements = [matrice[i][j] for i in range(len(matrice)) for j in range(len(matrice[i]))]
print(f"Tous les éléments : {tous_elements}")
print(f"Maximum (tous) : {max(tous_elements)}")
print(f"Minimum (tous) : {min(tous_elements)}")
print(f"Somme (tous) : {sum(tous_elements)}")
```

**Explication** :
- **max() imbriqué** : maximum de chaque ligne, puis maximum global
- **Position** : recherche par double boucle
- **Énumération** : (valeur, position) pairs
- **Aplatissement** : tous les éléments en une liste

**Test** : maximum = 27 en position (1, 0).

---

### Exercice 195 : Trouver le minimum dans une matrice
**Objectif** : Trouver l'élément minimum d'une matrice.

```python
# Solution
matrice = [
    [15, 3, 9],
    [27, 18, 5],
    [8, 12, 21]
]

print(f"Matrice : {matrice}")

# Minimum avec compréhension
minimum = min(min(ligne) for ligne in matrice)
print(f"Minimum : {minimum}")

# Position du minimum
position_min = None
for i in range(len(matrice)):
    for j in range(len(matrice[i])):
        if matrice[i][j] == minimum:
            position_min = (i, j)
            break
    if position_min:
        break

print(f"Position du minimum : {position_min}")

# Minimum avec énumération
min_avec_enum = min((matrice[i][j], (i, j)) for i in range(len(matrice)) for j in range(len(matrice[i])))
print(f"Minimum avec énumération : {min_avec_enum[0]} en position {min_avec_enum[1]}")

# Statistiques complètes
tous_elements = [matrice[i][j] for i in range(len(matrice)) for j in range(len(matrice[i]))]
print(f"Tous les éléments : {tous_elements}")
print(f"Minimum : {min(tous_elements)}")
print(f"Maximum : {max(tous_elements)}")
print(f"Plage (max - min) : {max(tous_elements) - min(tous_elements)}")
```

**Explication** :
- **min() imbriqué** : minimum de chaque ligne, puis minimum global
- **Position** : recherche du premier minimum
- **Énumération** : (valeur, position) pairs
- **Statistiques** : min, max, plage

**Test** : minimum = 3 en position (0, 1).

---

### Exercice 196 : Créer une liste imbriquée
**Objectif** : Créer et manipuler une liste de listes (structure imbriquée).

```python
# Solution
# Liste de listes simple
liste_imbriquee = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

print(f"Liste imbriquée : {liste_imbriquee}")

# Accès aux éléments
print(f"Premier sous-liste : {liste_imbriquee[0]}")
print(f"Élément [0][1] : {liste_imbriquee[0][1]}")
print(f"Élément [2][2] : {liste_imbriquee[2][2]}")

# Modification d'une sous-liste
liste_imbriquee[1].append(10)
print(f"Après ajout à la deuxième sous-liste : {liste_imbriquee}")

# Ajout d'une nouvelle sous-liste
liste_imbriquee.append([11, 12, 13])
print(f"Après ajout d'une sous-liste : {liste_imbriquee}")

# Aplatissement (conversion en liste simple)
aplatie = [element for sous_liste in liste_imbriquee for element in sous_liste]
print(f"Liste aplatie : {aplatie}")

# Compréhension pour créer une liste de listes
carres_imbriques = [[i, i**2] for i in range(1, 6)]
print(f"Paires (nombre, carré) : {carres_imbriques}")
```

**Explication** :
- **Structure** : liste contenant d'autres listes
- **Accès** : [index1][index2]
- **Modification** : des sous-listes modifiables
- **Aplatissement** : compréhension pour tout aplatir

**Test** : [[1, 2, 3], [4, 5, 6], [7, 8, 9]] → aplatie: [1, 2, 3, 4, 5, 6, 7, 8, 9].

---

### Exercice 197 : Accéder aux éléments d'une liste imbriquée
**Objectif** : Accéder et manipuler les éléments d'une structure imbriquée.

```python
# Solution
# Structure de données complexe
etudiants = [
    {"nom": "Alice", "notes": [15, 16, 14]},
    {"nom": "Bob", "notes": [12, 13, 11]},
    {"nom": "Charlie", "notes": [18, 17, 19]}
]

print("Structure étudiants :")
for etudiant in etudiants:
    print(f"  {etudiant}")

# Accès aux noms
noms = [etudiant["nom"] for etudiant in etudiants]
print(f"Noms : {noms}")

# Accès aux notes
toutes_notes = [note for etudiant in etudiants for note in etudiant["notes"]]
print(f"Toutes les notes : {toutes_notes}")

# Moyennes par étudiant
moyennes = [(etudiant["nom"], sum(etudiant["notes"]) / len(etudiant["notes"])) for etudiant in etudiants]
print(f"Moyennes : {moyennes}")

# Étudiants avec moyenne > 15
excellents = [etudiant["nom"] for etudiant in etudiants if sum(etudiant["notes"]) / len(etudiant["notes"]) > 15]
print(f"Étudiants excellents (>15) : {excellents}")

# Structure plus complexe : matrice de dictionnaires
grille = [
    [{"x": i, "y": j, "valeur": i + j} for j in range(3)]
    for i in range(3)
]

print(f"Grille 3x3 : {grille}")
print(f"Valeur en [1][2] : {grille[1][2]}")
```

**Explication** :
- **Imbrication multiple** : dictionnaires dans listes
- **Compréhension** : accès à tous les niveaux
- **Filtres** : conditions sur les valeurs imbriquées
- **Applications** : données structurées, JSON-like

**Test** : noms: ["Alice", "Bob", "Charlie"].

---

### Exercice 198 : Supprimer les doublons d'une liste
**Objectif** : Supprimer les doublons d'une liste en préservant l'ordre.

```python
# Solution
nombres_avec_doublons = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4, 5, 5, 5, 5, 5]

# Méthode 1 : avec set() (ordre non préservé)
uniques_set = list(set(nombres_avec_doublons))
print(f"Avec set() : {uniques_set}")

# Méthode 2 : préservation de l'ordre (Python 3.7+)
from collections import OrderedDict
uniques_ordre = list(OrderedDict.fromkeys(nombres_avec_doublons))
print(f"Ordre préservé : {uniques_ordre}")

# Méthode 3 : compréhension avec énumération
vus = set()
uniques_comprehension = [x for x in nombres_avec_doublons if not (x in vus or vus.add(x))]
print(f"Avec compréhension : {uniques_comprehension}")

# Comparaison des méthodes
print(f"Set non trié : {sorted(uniques_set)}")
print(f"Ordre préservé : {uniques_ordre}")
print(f"Compréhension : {uniques_comprehension}")
print(f"Tous identiques : {set(uniques_set) == set(uniques_ordre) == set(uniques_comprehension)}")

# Déduplication de chaînes
mots_avec_doublons = ["le", "python", "est", "un", "langage", "python", "est", "puissant"]
mots_uniques = list(OrderedDict.fromkeys(mots_avec_doublons))
print(f"Mots avec doublons : {mots_avec_doublons}")
print(f"Mots uniques : {mots_uniques}")
```

**Explication** :
- **set()** : déduplication rapide mais ordre non préservé
- **OrderedDict** : préservation de l'ordre d'insertion
- **Compréhension** : technique élégante avec set
- **Performance** : OrderedDict le plus efficace pour l'ordre

**Test** : [1, 2, 2, 3, 3, 3] → [1, 2, 3].

---

### Exercice 199 : Compresser une liste de chaînes
**Objectif** : Compresser et analyser une liste de chaînes.

```python
# Solution
# Liste de chaînes à analyser
chaines = ["python", "java", "python", "javascript", "java", "c++", "python", "ruby"]

print(f"Chaînes : {chaines}")
print(f"Longueur totale : {len(chaines)}")

# Compression : chaînes uniques avec fréquences
from collections import Counter
frequences = Counter(chaines)
print(f"Fréquences : {dict(frequences)}")

# Format compressé : [(chaîne, fréquence), ...]
compresse = [(chaine, freq) for chaine, freq in frequences.items()]
print(f"Format compressé : {compresse}")

# Décompression
decompresse = [chaine for chaine, freq in compresse for _ in range(freq)]
print(f"Décompressé : {decompresse}")
print(f"Identique à l'original : {chaines == decompresse}")

# Analyse des longueurs
longueurs = [len(chaine) for chaine in chaines]
longueurs_uniques = list(set(longueurs))
print(f"Longueurs : {longueurs}")
print(f"Longueurs uniques : {longueurs_uniques}")

# Chaînes par longueur
chaines_par_longueur = {longueur: [c for c in chaines if len(c) == longueur] for longueur in longueurs_uniques}
print(f"Chaînes par longueur : {chaines_par_longueur}")
```

**Explication** :
- **Counter** : comptage automatique des fréquences
- **Compression** : [(élément, fréquence)]
- **Décompression** : répétition selon la fréquence
- **Analyse** : regroupement par propriétés

**Test** : "python", "java", "python" → compressé: [("python", 3), ("java", 2), ...].

---

### Exercice 200 : Synthèse complète des structures de données
**Objectif** : Application finale combinant toutes les structures de données.

```python
# Solution - Système d'analyse de données complet
def analyseur_donnees_complet(donnees_brutes):
    """Analyse complète avec toutes les structures de données"""
    resultat = {}

    # 1. Analyse avec listes
    resultat["listes"] = {
        "longueur": len(donnees_brutes),
        "somme": sum(donnees_brutes),
        "moyenne": sum(donnees_brutes) / len(donnees_brutes) if donnees_brutes else 0,
        "minimum": min(donnees_brutes) if donnees_brutes else None,
        "maximum": max(donnees_brutes) if donnees_brutes else None,
        "pairs": [x for x in donnees_brutes if x % 2 == 0],
        "impairs": [x for x in donnees_brutes if x % 2 != 0],
        "carres": [x**2 for x in donnees_brutes],
        "doubles": [x*2 for x in donnees_brutes]
    }

    # 2. Analyse avec ensembles
    resultat["ensembles"] = {
        "uniques": set(donnees_brutes),
        "nombre_uniques": len(set(donnees_brutes)),
        "pourcentage_uniques": (len(set(donnees_brutes)) / len(donnees_brutes) * 100) if donnees_brutes else 0,
        "positifs": {x for x in donnees_brutes if x > 0},
        "negatifs": {x for x in donnees_brutes if x < 0},
        "divisibles_par_3": {x for x in donnees_brutes if x % 3 == 0}
    }

    # 3. Analyse avec dictionnaires
    resultat["dictionnaires"] = {
        "frequences": {x: donnees_brutes.count(x) for x in set(donnees_brutes)},
        "indices": {x: [i for i, val in enumerate(donnees_brutes) if val == x] for x in set(donnees_brutes)},
        "proprietes": {
            x: {
                "carre": x**2,
                "double": x*2,
                "parite": "pair" if x % 2 == 0 else "impair",
                "signe": "positif" if x > 0 else "négatif" if x < 0 else "nul"
            }
            for x in set(donnees_brutes)
        }
    }

    # 4. Analyse avec tuples
    resultat["tuples"] = {
        "statistiques": (len(donnees_brutes), sum(donnees_brutes), max(donnees_brutes), min(donnees_brutes)),
        "paires_valeur_index": [(x, i) for i, x in enumerate(donnees_brutes)],
        "groupes_parite": (
            [x for x in donnees_brutes if x % 2 == 0],
            [x for x in donnees_brutes if x % 2 != 0]
        )
    }

    # 5. Matrices et structures complexes
    resultat["matrices"] = {
        "matrice_identite": [[1 if i == j else 0 for j in range(5)] for i in range(5)],
        "matrice_valeurs": [[x for x in donnees_brutes[:5]] for _ in range(3)],  # Répétition
        "statistiques_matrice": [
            [len(donnees_brutes), sum(donnees_brutes)],
            [len(resultat["ensembles"]["uniques"]), len([x for x in donnees_brutes if x > 0])]
        ]
    }

    return resultat

# Test avec données variées
donnees_test = [15, 8, 12, 20, 7, 18, 25, 4, 9, 18, 15, 7, 12, 8, 20]
analyse_complete = analyseur_donnees_complet(donnees_test)

print("=== ANALYSE COMPLÈTE ===")
for structure, contenu in analyse_complete.items():
    print(f"\n--- {structure.upper()} ---")
    if isinstance(contenu, dict):
        for cle, valeur in contenu.items():
            if isinstance(valeur, list) and len(str(valeur)) > 100:
                print(f"{cle}: [{len(valeur)} éléments]")
            else:
                print(f"{cle}: {valeur}")
    else:
        print(contenu)

# Vérifications
print("
=== VÉRIFICATIONS ===")
listes = analyse_complete["listes"]
ensembles = analyse_complete["ensembles"]
dicos = analyse_complete["dictionnaires"]

print(f"Longueur liste : {listes['longueur']}")
print(f"Nombre d'éléments uniques : {ensembles['nombre_uniques']}")
print(f"Pairs + impairs = {len(listes['pairs']) + len(listes['impairs'])}")
print(f"Positifs + négatifs + zéros = {len(ensembles['positifs']) + len(ensembles['negatifs']) + (0 in donnees_test)}")
print(f"Vérification moyenne : {listes['moyenne']:.2f} vs {sum(donnees_test)/len(donnees_test):.2f}")
print(f"Fréquences totalisent : {sum(dicos['frequences'].values())} éléments")
```

**Explication** :
- **Analyse intégrée** : utilisation de toutes les structures
- **Compréhensions multiples** : listes, ensembles, dictionnaires
- **Matrices** : structures 2D pour organisation
- **Validations** : vérifications croisées
- **Performance** : analyse complète et efficace

**Test** : Analyse complète d'une liste avec toutes les structures de données.

---

## 🔍 Points Clés à Retenir

### 1. **Compréhensions Avancées**
```python
# Compréhensions multiples
nombres = [1, 2, 3, 4, 5]

# Liste
pairs = [x for x in nombres if x % 2 == 0]

# Dictionnaire
carres = {x: x**2 for x in nombres}

# Ensemble
uniques = {x**2 for x in nombres}

# Imbriquées
matrice = [[i + j for j in range(3)] for i in range(3)]
coordonnees = [(x, y) for x in range(3) for y in range(3)]
```

### 2. **Matrices**
```python
# Création
matrice = [[i + j for j in range(n)] for i in range(m)]

# Accès
element = matrice[i][j]

# Opérations
somme = [[a[i][j] + b[i][j] for j in range(n)] for i in range(m)]
produit = [[sum(a[i][k] * b[k][j] for k in range(n)) for j in range(p)] for i in range(m)]
transposee = [[matrice[j][i] for j in range(n)] for i in range(m)]
```

### 3. **Fonctions d'Ordre Supérieur avec Compréhensions**
```python
# Map avec compréhension
doubles = [x * 2 for x in nombres]

# Filter avec compréhension
pairs = [x for x in nombres if x % 2 == 0]

# Reduce avec compréhension (simulation)
produit = 1
for x in nombres:
    produit *= x
# Ou avec functools.reduce
from functools import reduce
produit = reduce(lambda x, y: x * y, nombres)
```

## 💡 Optimisations et Astuces

### 1. **Compréhensions vs Fonctions Built-in**
```python
# Compréhension (recommandée)
pairs = [x for x in nombres if x % 2 == 0]

# Filter + map (plus verbeux)
pairs = list(filter(lambda x: x % 2 == 0, map(lambda x: x, nombres)))

# Built-in (plus efficace si possible)
pairs = [x for x in nombres if x % 2 == 0]  # Optimal
```

### 2. **Matrices avec NumPy (si disponible)**
```python
# Si numpy est installé
import numpy as np

# Création
matrice = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

# Opérations
somme = matrice + matrice
produit = matrice * matrice  # Pas la multiplication matricielle
produit_mat = np.dot(matrice, matrice)  # Multiplication matricielle
transposee = matrice.T

# Plus efficace que les listes pour les calculs numériques
```

### 3. **Génération de Patterns Complexes**
```python
# Patterns avec compréhension
def generer_patterns(n):
    patterns = {}

    # Carrés magiques (simplifié)
    patterns["carres"] = [[i**2 for i in range(1, n+1)]]

    # Triangulaire
    patterns["triangulaire"] = [[sum(range(1, i+1))] for i in range(1, n+1)]

    # Fibonacci en 2D
    patterns["fibonacci_2d"] = [[fibonacci_iteratif(i + j) for j in range(n)] for i in range(n)]

    return patterns

# Utilisation
patterns = generer_patterns(5)
for nom, pattern in patterns.items():
    print(f"{nom}: {pattern}")
```

## 🚀 Applications Pratiques

### 1. **Traitement d'Images (Simulation)**
```python
def traiter_image(image, operations):
    """Traite une image représentée par une matrice"""
    resultat = [ligne[:] for ligne in image]  # Copie profonde

    for operation in operations:
        if operation == "negatif":
            resultat = [[255 - pixel for pixel in ligne] for ligne in resultat]
        elif operation == "luminosite":
            resultat = [[min(255, pixel + 50) for pixel in ligne] for ligne in resultat]
        elif operation == "contraste":
            # Simplification : multiplication par 1.2
            resultat = [[min(255, int(pixel * 1.2)) for pixel in ligne] for ligne in resultat]
        elif operation == "flou":
            # Flou simple (moyenne des voisins)
            for i in range(1, len(resultat) - 1):
                for j in range(1, len(resultat[i]) - 1):
                    moyenne = sum(
                        resultat[i-1][j-1:j+2] +
                        resultat[i][j-1:j+2] +
                        resultat[i+1][j-1:j+2]
                    ) // 9
                    resultat[i][j] = moyenne

    return resultat

# Test avec une "image" simple
image_test = [
    [100, 150, 200],
    [50, 120, 180],
    [75, 140, 160]
]

operations = ["negatif", "luminosite"]
image_traitee = traiter_image(image_test, operations)
print("Image originale:")
for ligne in image_test:
    print(ligne)
print("Image traitée:")
for ligne in image_traitee:
    print(ligne)
```

### 2. **Calculateur de Statistiques 2D**
```python
def statistiques_2d(matrice):
    """Calcule des statistiques 2D sur une matrice"""
    if not matrice or not matrice[0]:
        return None

    # Aplatissement
    tous_elements = [element for ligne in matrice for element in ligne]

    # Statistiques globales
    stats_globales = {
        "elements_totaux": len(tous_elements),
        "somme_globale": sum(tous_elements),
        "moyenne_globale": sum(tous_elements) / len(tous_elements),
        "min_global": min(tous_elements),
        "max_global": max(tous_elements)
    }

    # Statistiques par ligne
    stats_lignes = [{
        "somme": sum(ligne),
        "moyenne": sum(ligne) / len(ligne),
        "min": min(ligne),
        "max": max(ligne),
        "elements": ligne
    } for ligne in matrice]

    # Statistiques par colonne
    stats_colonnes = [{
        "somme": sum(ligne[i] for ligne in matrice),
        "moyenne": sum(ligne[i] for ligne in matrice) / len(matrice),
        "min": min(ligne[i] for ligne in matrice),
        "max": max(ligne[i] for ligne in matrice)
    } for i in range(len(matrice[0]))]

    return {
        "globales": stats_globales,
        "par_lignes": stats_lignes,
        "par_colonnes": stats_colonnes
    }

# Test
matrice_test = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12]
]

stats = statistiques_2d(matrice_test)
print("Statistiques 2D:")
for section, contenu in stats.items():
    print(f"\n{section}:")
    if isinstance(contenu, list):
        for i, item in enumerate(contenu):
            print(f"  {i}: {item}")
    else:
        for cle, valeur in contenu.items():
            print(f"  {cle}: {valeur}")
```

### 3. **Générateur de Grilles**
```python
def generateur_grilles(type_grille, taille):
    """Génère différents types de grilles"""
    if type_grille == "identite":
        return [[1 if i == j else 0 for j in range(taille)] for i in range(taille)]

    elif type_grille == "diagonale":
        return [[1 if i == j or i + j == taille - 1 else 0 for j in range(taille)] for i in range(taille)]

    elif type_grille == "damier":
        return [[1 if (i + j) % 2 == 0 else 0 for j in range(taille)] for i in range(taille)]

    elif type_grille == "spiral":
        # Spirale de nombres (simplifiée)
        grille = [[0 for _ in range(taille)] for _ in range(taille)]
        directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]  # droite, bas, gauche, haut
        x, y, dx, dy = 0, 0, 0, 1

        for i in range(1, taille * taille + 1):
            grille[x][y] = i
            nx, ny = x + directions[0][0], y + directions[0][1]

            if not (0 <= nx < taille and 0 <= ny < taille and grille[nx][ny] == 0):
                directions.append(directions.pop(0))  # Rotation
                nx, ny = x + directions[0][0], y + directions[0][1]

            x, y = nx, ny

        return grille

    else:
        return None

# Tests
grilles = {}
for type_grille in ["identite", "diagonale", "damier", "spiral"]:
    grilles[type_grille] = generateur_grilles(type_grille, 5)

print("Grilles générées:")
for type_grille, grille in grilles.items():
    print(f"\n{type_grille.upper()} (5x5):")
    for ligne in grille:
        print(" ".join(f"{x:2d}" for x in ligne))
```

## 🎯 Bilan de la Partie 4

### Concepts Maîtrisés
✅ **Listes avancées** : manipulation, tri, recherche
✅ **Tuples** : immuabilité, déballage, namedtuple
✅ **Dictionnaires** : mapping, méthodes, parcours
✅ **Ensembles** : unicité, opérations ensemblistes
✅ **Compréhensions** : listes, dictionnaires, ensembles
✅ **Matrices** : 2D, opérations arithmétiques, transposition
✅ **Structures complexes** : imbrication, analyse

### Compétences Développées
- **Manipulation de données** : transformation, filtrage, agrégation
- **Algorithmique** : recherche, tri, optimisation
- **Structures complexes** : matrices, imbrications
- **Performance** : choix des bonnes structures
- **Analyse** : statistiques, patterns, validations

---

**🏁 FIN DE LA PARTIE 4 - BRAVO !**

**Exercices complétés : 200/200** 🎯

*Félicitations ! Vous avez terminé les structures de données. Continuez avec la [Partie 5](Partie%205%20-%20POO/5-1-classes-objets.md) pour la programmation orientée objet !*