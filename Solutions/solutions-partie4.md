# Partie 4 - Structures de Données : Solutions

## 🎯 Introduction

Cette partie présente les **solutions complètes** des exercices de la Partie 4. Chaque solution inclut :
- Le code source complet et fonctionnel
- Des explications détaillées
- Des exemples d'utilisation
- Des tests de validation

---

## 📚 Chapitre 4.1 : Solutions - Listes

### Exercice 151 : Créer une liste et y ajouter des éléments

**Solution complète :**

```python
# Solution de base
ma_liste = []

# Ajout d'éléments
ma_liste.append("Python")
ma_liste.append("Java")
ma_liste.append("JavaScript")
ma_liste.append("C++")

print(f"Liste créée : {ma_liste}")

# Solution avec initialisation
langages = ["Python", "Java", "JavaScript", "C++"]
print(f"Liste initialisée : {langages}")

# Solution avec range
nombres = list(range(1, 11))
print(f"Liste avec range : {nombres}")

# Solution avec compréhension
carres = [i**2 for i in range(1, 6)]
print(f"Liste par compréhension : {carres}")

# Solution avec extend
ma_liste = []
ma_liste.extend(["HTML", "CSS", "SQL"])
ma_liste.extend([1, 2, 3])
print(f"Liste avec extend : {ma_liste}")
```

**Explications :**
- `append()` : ajoute un élément à la fin
- `extend()` : ajoute plusieurs éléments
- `list(range())` : conversion range en liste
- Compréhension : génération concise

**Test :**
```
Liste créée : ['Python', 'Java', 'JavaScript', 'C++']
Liste avec range : [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
Liste par compréhension : [1, 4, 9, 16, 25]
```

---

### Exercice 152 : Accéder aux éléments d'une liste

**Solution complète :**

```python
# Solution avec indexation
langages = ["Python", "Java", "JavaScript", "C++", "Ruby"]

print(f"Premier élément : {langages[0]}")
print(f"Deuxième élément : {langages[1]}")
print(f"Dernier élément : {langages[-1]}")
print(f"Avant-dernier : {langages[-2]}")

# Solution avec slicing
print(f"Premiers 3 : {langages[:3]}")
print(f"Derniers 2 : {langages[-2:]}")
print(f"Éléments 1 à 3 : {langages[1:4]}")
print(f"Tous les 2 : {langages[::2]}")

# Solution avec recherche
def trouver_index(liste, element):
    """Trouve l'index d'un élément"""
    try:
        return liste.index(element)
    except ValueError:
        return f"'{element}' non trouvé"

# Tests
print(f"\nIndex de 'Java' : {trouver_index(langages, 'Java')}")
print(f"Index de 'Python' : {trouver_index(langages, 'Python')}")
print(f"Index de 'PHP' : {trouver_index(langages, 'PHP')}")

# Solution avec in
print(f"'Java' dans la liste : {'Java' in langages}")
print(f"'PHP' dans la liste : {'PHP' in langages}")
```

**Explications :**
- `index()` : position d'un élément
- `in` : test d'appartenance
- Slicing : `[start:stop:step]`
- Gestion d'erreurs : ValueError

**Test :**
```
Premier élément : Python
Dernier élément : Ruby
Premiers 3 : ['Python', 'Java', 'JavaScript']
'Java' dans la liste : True
```

---

### Exercice 153 : Modifier les éléments d'une liste

**Solution complète :**

```python
# Solution de base
langages = ["Python", "Java", "JavaScript", "C++", "Ruby"]

print(f"Avant modification : {langages}")
langages[1] = "Java 11"
langages[-1] = "Ruby on Rails"
print(f"Après modification : {langages}")

# Solution avec insertion
langages.insert(2, "TypeScript")
print(f"Après insertion : {langages}")

# Solution avec suppression
langages.pop(1)  # Supprime Java 11
print(f"Après suppression : {langages}")

# Solution avec remplacement multiple
nombres = [1, 2, 3, 4, 5]
print(f"Avant : {nombres}")
nombres[1:4] = [20, 30, 40]  # Remplace 2, 3, 4
print(f"Après remplacement : {nombres}")

# Solution avec remove
fruits = ["pomme", "banane", "orange", "pomme", "kiwi"]
print(f"Avant : {fruits}")
fruits.remove("pomme")  # Supprime première occurrence
print(f"Après remove : {fruits}")

# Solution avec del
del fruits[1]  # Supprime par index
print(f"Après del : {fruits}")
```

**Explications :**
- `insert()` : ajout à position spécifique
- `pop()` : suppression par index
- `remove()` : suppression par valeur
- `del` : suppression par index
- Slicing pour remplacement multiple

**Test :**
```
Avant modification : ['Python', 'Java', 'JavaScript', 'C++', 'Ruby']
Après modification : ['Python', 'Java 11', 'JavaScript', 'C++', 'Ruby on Rails']
Après insertion : ['Python', 'Java 11', 'TypeScript', 'JavaScript', 'C++', 'Ruby on Rails']
```

---

### Exercice 154 : Trier une liste de nombres

**Solution complète :**

```python
# Solution avec sort()
nombres = [64, 34, 25, 12, 22, 11, 90]
print(f"Avant tri : {nombres}")
nombres.sort()
print(f"Après tri croissant : {nombres}")

# Solution avec sorted()
nombres2 = [64, 34, 25, 12, 22, 11, 90]
nombres_tries = sorted(nombres2)
print(f"Tri avec sorted() : {nombres_tries}")
print(f"Original inchangé : {nombres2}")

# Solution avec reverse
nombres.sort(reverse=True)
print(f"Tri décroissant : {nombres}")

# Solution avec clé personnalisée
mots = ["python", "Java", "javascript", "C++", "ruby"]
mots_tries = sorted(mots, key=len)
print(f"Tri par longueur : {mots_tries}")

mots_tries = sorted(mots, key=str.lower)
print(f"Tri alphabétique : {mots_tries}")

# Solution avec tri stable
paires = [(3, 'c'), (1, 'a'), (2, 'b'), (1, 'd')]
paires_tries = sorted(paires)
print(f"Tri de paires : {paires_tries}")
```

**Explications :**
- `sort()` : tri en place (modifie la liste)
- `sorted()` : tri avec copie (conserve original)
- `reverse=True` : tri décroissant
- `key` : fonction de tri personnalisée

**Test :**
```
Avant tri : [64, 34, 25, 12, 22, 11, 90]
Après tri croissant : [11, 12, 22, 25, 34, 64, 90]
Tri avec sorted() : [11, 12, 22, 25, 34, 64, 90]
Tri par longueur : ['C++', 'Java', 'ruby', 'python', 'javascript']
```

---

### Exercice 155 : Compréhension de liste pour les carrés

**Solution complète :**

```python
# Solution de base
carres = [i**2 for i in range(1, 11)]
print(f"Carrés de 1 à 10 : {carres}")

# Solution avec condition
pairs = [i for i in range(1, 11) if i % 2 == 0]
print(f"Nombres pairs : {pairs}")

impairs = [i for i in range(1, 11) if i % 2 != 0]
print(f"Nombres impairs : {impairs}")

# Solution avec transformation
langages = ["python", "java", "javascript", "c++"]
langages_maj = [lang.capitalize() for lang in langages]
print(f"Langages capitalisés : {langages_maj}")

# Solution avec if/else
nombres = range(1, 11)
descriptions = ["pair" if i % 2 == 0 else "impair" for i in nombres]
print(f"Descriptions : {descriptions}")

# Solution avec calculs
temperatures_c = [20, 25, 30, 35, 40]
temperatures_f = [c * 9/5 + 32 for c in temperatures_c]
print(f"Températures F : {temperatures_f}")

# Solution imbriquée
matrice = [[i * j for j in range(1, 4)] for i in range(1, 4)]
print(f"Matrice 3×3 : {matrice}")
```

**Explications :**
- **Compréhension** : `[expression for item in iterable]`
- **Condition** : `[expr for item in iter if condition]`
- **If/else** : `["pair" if condition else "impair" for item]`
- **Imbriquée** : compréhension dans compréhension

**Test :**
```
Carrés de 1 à 10 : [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
Nombres pairs : [2, 4, 6, 8, 10]
Températures F : [68.0, 77.0, 86.0, 95.0, 104.0]
Matrice 3×3 : [[1, 2, 3], [2, 4, 6], [3, 6, 9]]
```

---

## 📚 Chapitre 4.2 : Solutions - Tuples

### Exercice 156 : Créer et manipuler des tuples

**Solution complète :**

```python
# Solution de base
mon_tuple = (1, 2, 3, 4, 5)
print(f"Tuple : {mon_tuple}")
print(f"Type : {type(mon_tuple)}")

# Solution avec un élément
tuple_simple = (42,)
print(f"Tuple un élément : {tuple_simple}")

# Solution sans parenthèses
tuple_implicite = 1, 2, 3
print(f"Tuple implicite : {tuple_implicite}")

# Solution avec différents types
info_personne = ("Alice", 25, "Paris", True)
print(f"Info personne : {info_personne}")

# Solution avec indexation
print(f"Nom : {info_personne[0]}")
print(f"Age : {info_personne[1]}")
print(f"Ville : {info_personne[2]}")

# Solution avec unpacking
nom, age, ville, actif = info_personne
print(f"Unpacked - Nom: {nom}, Age: {age}, Ville: {ville}, Actif: {actif}")

# Solution avec slicing
print(f"Premier et deuxième : {info_personne[:2]}")
print(f"Derniers éléments : {info_personne[1:]}")
```

**Explications :**
- **Tuple** : séquence immuable
- **Virgule** : nécessaire pour tuple un élément
- **Unpacking** : déballage des valeurs
- **Immuabilité** : ne peut pas être modifié

**Test :**
```
Tuple : (1, 2, 3, 4, 5)
Tuple un élément : (42,)
Info personne : ('Alice', 25, 'Paris', True)
Nom : Alice, Age : 25, Ville : Paris, Actif : True
```

---

### Exercice 157 : Conversion liste ↔ tuple

**Solution complète :**

```python
# Solution liste vers tuple
ma_liste = [1, 2, 3, 4, 5]
mon_tuple = tuple(ma_liste)
print(f"Liste : {ma_liste}")
print(f"Tuple : {mon_tuple}")

# Solution tuple vers liste
mon_tuple = (10, 20, 30, 40, 50)
ma_liste = list(mon_tuple)
print(f"Tuple : {mon_tuple}")
print(f"Liste : {ma_liste}")

# Solution avec modification
nombres_tuple = (1, 2, 3, 4, 5)
print(f"Original tuple : {nombres_tuple}")

# Conversion pour modification
nombres_liste = list(nombres_tuple)
nombres_liste.append(6)
nombres_liste[0] = 0
nouveau_tuple = tuple(nombres_liste)

print(f"Après modification : {nouveau_tuple}")

# Solution avec tuples de tuples
coordonnees = [(1, 2), (3, 4), (5, 6)]
print(f"Coordonnées : {coordonnees}")
print(f"Première coord : {coordonnees[0]}")
print(f"X de première : {coordonnees[0][0]}")

# Solution avec named tuples (avancé)
from collections import namedtuple

Point = namedtuple('Point', ['x', 'y'])
point1 = Point(10, 20)
point2 = Point(30, 40)

print(f"Point 1 : {point1}")
print(f"Point 1 X : {point1.x}")
print(f"Point 1 Y : {point1.y}")
```

**Explications :**
- `tuple(liste)` : conversion liste → tuple
- `list(tuple)` : conversion tuple → liste
- **Immuabilité** : conversion nécessaire pour modification
- **Named tuples** : tuples avec noms d'attributs

**Test :**
```
Liste : [1, 2, 3, 4, 5]
Tuple : (1, 2, 3, 4, 5)
Original tuple : (1, 2, 3, 4, 5)
Après modification : (0, 2, 3, 4, 5, 6)
Point 1 : Point(x=10, y=20)
```

---

## 📚 Chapitre 4.3 : Solutions - Dictionnaires

### Exercice 158 : Créer et manipuler un dictionnaire

**Solution complète :**

```python
# Solution de base
etudiant = {
    "nom": "Dupont",
    "prenom": "Alice",
    "age": 20,
    "filiere": "Informatique",
    "notes": [15, 16, 14, 18]
}

print(f"Étudiant : {etudiant}")

# Solution avec dict()
etudiant2 = dict(nom="Martin", prenom="Bob", age=22)
print(f"Étudiant 2 : {etudiant2}")

# Solution avec zip
cles = ["nom", "prenom", "age"]
valeurs = ["Garcia", "Clara", 21]
etudiant3 = dict(zip(cles, valeurs))
print(f"Étudiant 3 : {etudiant3}")

# Solution avec get()
print(f"Nom : {etudiant.get('nom')}")
print(f"Email : {etudiant.get('email', 'Non spécifié')}")

# Solution avec ajout/modification
etudiant["email"] = "alice.dupont@univ.fr"
etudiant["age"] = 21
print(f"Après modification : {etudiant}")
```

**Explications :**
- **Syntaxe** : `{"clé": "valeur"}`
- `dict()` : constructeur
- `zip()` : association clés-valeurs
- `get()` : accès avec valeur par défaut
- **Mutabilité** : ajout/modification possible

**Test :**
```
Étudiant : {'nom': 'Dupont', 'prenom': 'Alice', 'age': 20, 'filiere': 'Informatique', 'notes': [15, 16, 14, 18]}
Email : Non spécifié
Après modification : {'nom': 'Dupont', 'prenom': 'Alice', 'age': 21, 'filiere': 'Informatique', 'notes': [15, 16, 14, 18], 'email': 'alice.dupont@univ.fr'}
```

---

### Exercice 159 : Parcourir un dictionnaire

**Solution complète :**

```python
# Solution avec items()
etudiant = {
    "nom": "Dupont",
    "prenom": "Alice",
    "age": 21,
    "filiere": "Informatique"
}

print("Parcours avec items() :")
for cle, valeur in etudiant.items():
    print(f"{cle}: {valeur}")

# Solution avec keys()
print("\nParcours avec keys() :")
for cle in etudiant.keys():
    print(f"Clé: {cle} -> Valeur: {etudiant[cle]}")

# Solution avec values()
print("\nParcours avec values() :")
for valeur in etudiant.values():
    print(f"Valeur: {valeur}")

# Solution avec enumerate
print("\nParcours avec enumerate :")
for index, (cle, valeur) in enumerate(etudiant.items()):
    print(f"{index + 1}. {cle}: {valeur}")

# Solution avec dictionnaire de listes
notes = {
    "Math": [15, 16, 14],
    "Physique": [18, 17, 19],
    "Info": [16, 15, 17]
}

print("\nNotes par matière :")
for matiere, liste_notes in notes.items():
    moyenne = sum(liste_notes) / len(liste_notes)
    print(f"{matiere}: {liste_notes} (moyenne: {moyenne:.1f})")
```

**Explications :**
- `items()` : clés et valeurs
- `keys()` : seulement les clés
- `values()` : seulement les valeurs
- `enumerate()` : index + items

**Test :**
```
Parcours avec items() :
nom: Dupont
prenom: Alice
age: 21
filiere: Informatique

Notes par matière :
Math: [15, 16, 14] (moyenne: 15.0)
Physique: [18, 17, 19] (moyenne: 18.0)
Info: [16, 15, 17] (moyenne: 16.0)
```

---

## 📚 Chapitre 4.4 : Solutions - Ensembles

### Exercice 160 : Créer et manipuler des ensembles

**Solution complète :**

```python
# Solution de base
mon_ensemble = {1, 2, 3, 4, 5}
print(f"Ensemble : {mon_ensemble}")

# Solution avec set()
nombres = [1, 2, 2, 3, 3, 4, 5, 5]
ensemble_unique = set(nombres)
print(f"Ensemble unique : {ensemble_unique}")

# Solution avec types mixtes
ensemble_mixte = {1, "hello", 3.14, True}
print(f"Ensemble mixte : {ensemble_mixte}")

# Solution avec ajout
fruits = {"pomme", "banane"}
fruits.add("orange")
print(f"Après add : {fruits}")

# Solution avec suppression
fruits.remove("banane")
print(f"Après remove : {fruits}")

# Solution avec discard
fruits.discard("kiwi")  # N'existe pas, pas d'erreur
print(f"Après discard : {fruits}")

# Solution avec clear
ensemble_test = {1, 2, 3}
ensemble_test.clear()
print(f"Après clear : {ensemble_test}")
```

**Explications :**
- **Ensemble** : collection non ordonnée unique
- `set()` : conversion en ensemble
- `add()` : ajout d'un élément
- `remove()` : suppression (erreur si absent)
- `discard()` : suppression (pas d'erreur si absent)
- `clear()` : vidage complet

**Test :**
```
Ensemble : {1, 2, 3, 4, 5}
Ensemble unique : {1, 2, 3, 4, 5}
Après add : {'pomme', 'banane', 'orange'}
Après remove : {'pomme', 'orange'}
```

---

### Exercice 161 : Opérations sur les ensembles

**Solution complète :**

```python
# Solution avec union
ensemble1 = {1, 2, 3, 4, 5}
ensemble2 = {4, 5, 6, 7, 8}

union = ensemble1 | ensemble2
print(f"Union : {union}")

union_method = ensemble1.union(ensemble2)
print(f"Union method : {union_method}")

# Solution avec intersection
intersection = ensemble1 & ensemble2
print(f"Intersection : {intersection}")

intersection_method = ensemble1.intersection(ensemble2)
print(f"Intersection method : {intersection_method}")

# Solution avec différence
difference1 = ensemble1 - ensemble2
print(f"Différence 1-2 : {difference1}")

difference2 = ensemble2 - ensemble1
print(f"Différence 2-1 : {difference2}")

# Solution avec différence symétrique
difference_sym = ensemble1 ^ ensemble2
print(f"Différence symétrique : {difference_sym}")

# Solution avec sous-ensemble
sous_ensemble = {1, 2, 3}
print(f"{sous_ensemble} sous-ensemble de {ensemble1} : {sous_ensemble.issubset(ensemble1)}")

super_ensemble = {1, 2, 3, 4, 5, 6, 7, 8, 9}
print(f"{ensemble1} sous-ensemble de {super_ensemble} : {ensemble1.issubset(super_ensemble)}")

# Solution avec mise à jour
ensemble_a = {1, 2, 3}
ensemble_b = {3, 4, 5}

print(f"Avant : A={ensemble_a}, B={ensemble_b}")
ensemble_a.update(ensemble_b)  # Union en place
print(f"Après update : A={ensemble_a}")

ensemble_a.intersection_update(ensemble_b)  # Intersection en place
print(f"Après intersection_update : A={ensemble_a}")
```

**Explications :**
- `|` : union (opérateur)
- `&` : intersection (opérateur)
- `-` : différence (opérateur)
- `^` : différence symétrique
- `issubset()` : test de sous-ensemble
- `_update()` : modification en place

**Test :**
```
Union : {1, 2, 3, 4, 5, 6, 7, 8}
Intersection : {4, 5}
Différence 1-2 : {1, 2, 3}
Différence symétrique : {1, 2, 3, 6, 7, 8}
{1, 2, 3} sous-ensemble de {1, 2, 3, 4, 5} : True
```

---

## 🎯 Résumé des Solutions - Partie 4

### ✅ **Exercices Résolus (151-161)**

| Exercice | Thème | Solution | Fonctionnalités |
|----------|-------|----------|-----------------|
| **151** | Créer liste | ✅ Complète | Append, extend, compréhension |
| **152** | Accès liste | ✅ Complète | Index, slicing, in, index() |
| **153** | Modifier liste | ✅ Complète | Insert, pop, remove, del |
| **154** | Trier liste | ✅ Complète | Sort, sorted, key, reverse |
| **155** | Compréhension | ✅ Complète | Base, conditions, if/else |
| **156** | Tuples | ✅ Complète | Création, unpacking, immuabilité |
| **157** | Liste ↔ Tuple | ✅ Complète | Conversion, namedtuple |
| **158** | Dictionnaires | ✅ Complète | Création, get, modification |
| **159** | Parcourir dict | ✅ Complète | Items, keys, values, enumerate |
| **160** | Ensembles | ✅ Complète | Add, remove, discard, clear |
| **161** | Opérations sets | ✅ Complète | Union, intersection, subsets |

### 🚀 **Concepts Clés Maîtrisés**

- **Listes** : indexation, slicing, modification, tri
- **Tuples** : immuabilité, unpacking, named tuples
- **Dictionnaires** : clés-valeurs, parcours, méthodes
- **Ensembles** : unicité, opérations mathématiques
- **Compréhensions** : syntaxe concise et puissante
- **Conversions** : entre types de collections

### 📚 **Fonctionnalités Avancées**

- **Manipulations complexes** : slicing, unpacking, conversions
- **Optimisations** : compréhension vs boucles
- **Gestion d'erreurs** : try/except, validation
- **Types nommés** : namedtuple pour structures
- **Opérations ensemblistes** : mathématiques sur collections
- **Performance** : méthodes efficaces de manipulation

---

**🎉 Toutes les solutions de la Partie 4 sont maintenant disponibles !**

*Ces solutions démontrent la maîtrise complète des structures de données en Python, essentielles pour la programmation avancée.*
