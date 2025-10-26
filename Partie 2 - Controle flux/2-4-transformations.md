# Partie 2.4 : Transformations et Compréhensions

## 🎯 Objectifs Pédagogiques

Ce chapitre explore les **transformations de listes** et les **compréhensions**, techniques puissantes pour créer et modifier des collections de données de manière concise et efficace.

### Concepts Abordés
- **Transformations** : carrés, cubes, doublage, triplage
- **Compréhensions de liste** : syntaxe concise pour créer des listes
- **Filtrage avancé** : conditions dans les transformations
- **Fusions et extensions** : combinaison de listes

---

## 📝 Exercices Pratiques

### Exercice 81 : Somme des nombres pairs
**Objectif** : Calculer la somme des nombres pairs d'une liste.

```python
# Solution
nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
somme_pairs = 0

for nombre in nombres:
    if nombre % 2 == 0:
        somme_pairs += nombre

print(f"Somme des nombres pairs : {somme_pairs}")
```

**Explication** :
- **Filtrage + accumulation** : test ET addition
- **Condition** : parité avant addition
- **Initialisation** : somme à 0

**Test** : 2+4+6+8+10 = 30.

---

### Exercice 82 : Somme des nombres impairs
**Objectif** : Calculer la somme des nombres impairs d'une liste.

```python
# Solution
nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
somme_impairs = 0

for nombre in nombres:
    if nombre % 2 != 0:
        somme_impairs += nombre

print(f"Somme des nombres impairs : {somme_impairs}")
```

**Explication** :
- **Logique inverse** : impairs au lieu de pairs
- **Négation** : != 0 pour les impairs
- **Pattern similaire** : même structure

**Test** : 1+3+5+7+9 = 25.

---

### Exercice 83 : Liste des carrés
**Objectif** : Créer une nouvelle liste avec les carrés des éléments.

```python
# Solution
nombres = [1, 2, 3, 4, 5]
carres = []

for nombre in nombres:
    carres.append(nombre ** 2)

print(f"Originaux : {nombres}")
print(f"Carrés : {carres}")
```

**Explication** :
- **Transformation** : fonction appliquée à chaque élément
- `.append()` : ajout à la nouvelle liste
- **Préservation** : liste originale intacte

**Test** : [1, 2, 3, 4, 5] → [1, 4, 9, 16, 25].

---

### Exercice 84 : Liste des cubes
**Objectif** : Créer une nouvelle liste avec les cubes des éléments.

```python
# Solution
nombres = [1, 2, 3, 4, 5]
cubes = []

for nombre in nombres:
    cubes.append(nombre ** 3)

print(f"Originaux : {nombres}")
print(f"Cubes : {cubes}")
```

**Explication** :
- **Puissance 3** : ** 3 ou pow(nombre, 3)
- **Pattern** : même logique que les carrés
- **Croissance** : cubes croissent plus vite

**Test** : [1, 2, 3, 4, 5] → [1, 8, 27, 64, 125].

---

### Exercice 85 : Tri croissant
**Objectif** : Trier une liste par ordre croissant.

```python
# Solution
nombres = [64, 34, 25, 12, 22, 11, 90]
print(f"Avant tri : {nombres}")

nombres.sort()  # Tri en place
print(f"Après tri croissant : {nombres}")
```

**Explication** :
- `.sort()` : tri en place (modifie la liste)
- **Algorithme** : tri rapide (Timsort en Python)
- **Ordre naturel** : numérique croissant

**Test** : [64, 34, 25, 12, 22, 11, 90] → [11, 12, 22, 25, 34, 64, 90].

---

### Exercice 86 : Tri décroissant
**Objectif** : Trier une liste par ordre décroissant.

```python
# Solution
nombres = [64, 34, 25, 12, 22, 11, 90]
print(f"Avant tri : {nombres}")

nombres.sort(reverse=True)  # Tri décroissant
print(f"Après tri décroissant : {nombres}")
```

**Explication** :
- **Paramètre reverse** : reverse=True
- **Inversion** : ordre inverse du tri naturel
- **Efficacité** : même performance que le tri croissant

**Test** : [64, 34, 25, 12, 22, 11, 90] → [90, 64, 34, 25, 22, 12, 11].

---

### Exercice 87 : Fusion de deux listes
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

### Exercice 88 : Test de liste vide
**Objectif** : Vérifier si une liste est vide.

```python
# Solution
# Liste vide
liste_vide = []
# Liste avec éléments
liste_pleine = [1, 2, 3]

def est_vide(liste):
    return len(liste) == 0

print(f"Liste vide : {est_vide(liste_vide)}")
print(f"Liste pleine : {est_vide(liste_pleine)}")

# Alternative directe
if not liste_vide:
    print("La liste vide est considérée comme False")
else:
    print("La liste vide est considérée comme True")
```

**Explication** :
- **Longueur** : len(liste) == 0
- **Truthy/Falsy** : liste vide = False, liste non vide = True
- **Convention** : `if not liste` pour tester vide

**Test** : [] (vide), [1, 2, 3] (non vide).

---

### Exercice 89 : Premiers éléments
**Objectif** : Afficher les 5 premiers éléments d'une liste.

```python
# Solution
nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
n_premiers = 5

print(f"Liste complète : {nombres}")
print(f"5 premiers éléments : {nombres[:n_premiers]}")

# Avec vérification
if len(nombres) >= n_premiers:
    print(f"5 premiers : {nombres[:n_premiers]}")
else:
    print(f"Pas assez d'éléments, voici tous : {nombres}")
```

**Explication** :
- **Slicing** : [:5] pour les 5 premiers
- **Sécurité** : test de longueur
- **Limite** : évite les erreurs d'index

**Test** : [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12] → [1, 2, 3, 4, 5].

---

### Exercice 90 : Derniers éléments
**Objectif** : Afficher les 5 derniers éléments d'une liste.

```python
# Solution
nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
n_derniers = 5

print(f"Liste complète : {nombres}")
print(f"5 derniers éléments : {nombres[-n_derniers:]}")

# Avec vérification
if len(nombres) >= n_derniers:
    print(f"5 derniers : {nombres[-n_derniers:]}")
else:
    print(f"Pas assez d'éléments, voici tous : {nombres}")
```

**Explication** :
- **Index négatif** : -5: pour les 5 derniers
- **Slicing inversé** : du plus récent au plus ancien
- **Alternative** : nombres[len(nombres)-5:]

**Test** : [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12] → [8, 9, 10, 11, 12].

---

## 🔍 Points Clés à Retenir

### 1. **Compréhensions de Liste**
```python
# Syntaxe générale
nouvelle_liste = [expression for element in sequence if condition]

# Exemples
carres = [x**2 for x in range(10)]              # [0, 1, 4, 9, 16, ...]
pairs = [x for x in range(20) if x % 2 == 0]    # [0, 2, 4, 6, ...]
noms_maj = [nom.upper() for nom in noms]        # Conversion majuscules
```

### 2. **Transformations Courantes**
```python
# Doublage
doubles = [x*2 for x in nombres]

# Triplage
triples = [x*3 for x in nombres]

# Carrés
carres = [x**2 for x in nombres]

# Cubes
cubes = [x**3 for x in nombres]

# Inverses (nombres non nuls)
inverses = [1/x for x in nombres if x != 0]
```

### 3. **Fonctions Built-in pour Listes**
```python
# Tri
sorted(liste)          # Nouvelle liste triée
liste.sort()           # Tri en place

# Recherche
max(liste)             # Plus grand élément
min(liste)             # Plus petit élément
sum(liste)             # Somme des éléments

# Transformation
list(map(fonction, liste))  # Application de fonction
list(filter(condition, liste))  # Filtrage
```

### 4. **Slicing Avancé**
```python
liste = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

# Extraction
liste[2:7]      # [2, 3, 4, 5, 6] indices 2 à 6
liste[:5]       # [0, 1, 2, 3, 4] du début à 4
liste[5:]       # [5, 6, 7, 8, 9] de 5 à la fin
liste[::2]      # [0, 2, 4, 6, 8] un sur deux
liste[::-1]     # [9, 8, 7, 6, 5, 4, 3, 2, 1, 0] inversion

# Modification par slicing
liste[2:5] = [20, 30, 40]  # Remplacement
```

## 💡 Optimisations et Astuces

### 1. **Compréhensions vs Boucles**
```python
# Boucle classique (plus verbeuse)
carres = []
for nombre in nombres:
    carres.append(nombre ** 2)

# Compréhension (plus concise)
carres = [nombre ** 2 for nombre in nombres]

# Avec condition
pairs = [nombre for nombre in nombres if nombre % 2 == 0]
```

### 2. **Fonctions Lambda avec map/filter**
```python
# Au lieu de compréhension
from functools import reduce

# Carrés avec map
carres = list(map(lambda x: x**2, nombres))

# Filtrage avec filter
pairs = list(filter(lambda x: x % 2 == 0, nombres))

# Somme avec reduce
somme = reduce(lambda x, y: x + y, nombres)
```

### 3. **Génération de Séquences**
```python
# Nombres pairs de 0 à 20
pairs = [x for x in range(0, 21, 2)]

# Carrés pairs
carres_pairs = [x**2 for x in range(10) if x**2 % 2 == 0]

# Nombres de 1 à 10 sauf 5
exclus = [x for x in range(1, 11) if x != 5]
```

## 🚀 Applications Pratiques

### 1. **Analyse de Données**
```python
def analyser_notes(notes):
    """Analyse des notes d'étudiants"""
    analyse = {}

    # Statistiques
    analyse["moyenne"] = sum(notes) / len(notes)
    analyse["maximum"] = max(notes)
    analyse["minimum"] = min(notes)

    # Distribution
    analyse["au_dessus_moyenne"] = [note for note in notes if note > analyse["moyenne"]]
    analyse["excellent"] = [note for note in notes if note >= 16]
    analyse["a_revoir"] = [note for note in notes if note < 10]

    return analyse

notes = [12, 15, 8, 18, 14, 9, 16, 11]
resultats = analyser_notes(notes)
for cle, valeur in resultats.items():
    print(f"{cle}: {valeur}")
```

### 2. **Transformation de Texte**
```python
def traiter_texte(texte):
    """Traite un texte : nettoyage et analyse"""
    # Nettoyage
    mots = texte.lower().replace(".", "").replace(",", "").split()

    # Transformations
    longueurs = [len(mot) for mot in mots]
    mots_maj = [mot.upper() for mot in mots if len(mot) > 3]

    return {
        "mots": mots,
        "nombre_mots": len(mots),
        "longueur_moyenne": sum(longueurs) / len(longueurs),
        "mots_longs": mots_maj
    }

texte = "Le Python est un langage de programmation puissant et polyvalent."
resultat = traiter_texte(texte)
for cle, valeur in resultat.items():
    print(f"{cle}: {valeur}")
```

### 3. **Génération de Patterns**
```python
def generer_patterns(n):
    """Génère différents patterns numériques"""
    patterns = {}

    # Carrés
    patterns["carres"] = [x**2 for x in range(1, n+1)]

    # Cubes
    patterns["cubes"] = [x**3 for x in range(1, n+1)]

    # Factoriels (simplifiés)
    patterns["fact"] = [1]  # 1!
    for i in range(2, n+1):
        patterns["fact"].append(patterns["fact"][-1] * i)

    # Nombres pairs et impairs
    patterns["pairs"] = [x for x in range(1, n+1) if x % 2 == 0]
    patterns["impairs"] = [x for x in range(1, n+1) if x % 2 != 0]

    return patterns

patterns = generer_patterns(5)
for cle, valeur in patterns.items():
    print(f"{cle}: {valeur}")
```

## 🎯 Défis Supplémentaires

1. **Générez** une liste des nombres premiers jusqu'à 100
2. **Créez** une matrice identité n×n
3. **Implémentez** un système de filtrage multiple (pairs ET > 10)
4. **Développez** un convertisseur de températures (Celsius vers Fahrenheit)

---

**Exercices complétés : 90/100** 🎯

*Continuez avec le [chapitre suivant](2-5-tests.md) pour les tests et validations !*