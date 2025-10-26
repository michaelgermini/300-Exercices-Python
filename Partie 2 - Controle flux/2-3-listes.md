# Partie 2.3 : Manipulation de Listes

## 🎯 Objectifs Pédagogiques

Ce chapitre explore la **manipulation avancée des listes**, structures de données fondamentales en Python. Les listes permettent de stocker et traiter des collections d'éléments.

### Concepts Abordés
- **Accès et modification** : indexation, slicing, modification d'éléments
- **Recherche et test** : appartenance, indices, occurrences
- **Parcours et transformation** : boucles, énumération, doublage
- **Gestion de liste** : ajout, suppression, remplacement

---

## 📝 Exercices Pratiques

### Exercice 71 : Appartenance à une liste
**Objectif** : Vérifier si un élément est présent dans une liste.

```python
# Solution
fruits = ["pomme", "banane", "orange", "kiwi", "mangue"]
element = input("Entrez un fruit : ").lower()

if element in fruits:
    print(f"{element} est dans la liste")
else:
    print(f"{element} n'est pas dans la liste")
```

**Explication** :
- **Opérateur in** : test d'appartenance
- **Case insensitive** : conversion en minuscules
- **Efficacité** : recherche optimisée

**Test** : "pomme" (oui), "fraise" (non).

---

### Exercice 72 : Suppression d'un élément
**Objectif** : Supprimer un élément spécifique d'une liste.

```python
# Solution
nombres = [1, 2, 3, 4, 5, 3, 6, 3]
element = 3

while element in nombres:  # Supprimer toutes les occurrences
    nombres.remove(element)

print(f"Liste après suppression de {element} : {nombres}")
```

**Explication** :
- `.remove()` : supprime la première occurrence
- **Boucle while** : pour supprimer toutes les occurrences
- **Modification en place** : la liste est modifiée

**Test** : [1, 2, 3, 4, 5, 3, 6, 3] → [1, 2, 4, 5, 6].

---

### Exercice 73 : Remplacement d'un élément
**Objectif** : Remplacer un élément par un autre dans une liste.

```python
# Solution
nombres = [1, 2, 3, 4, 5]
print(f"Liste originale : {nombres}")

index = int(input("Index à remplacer (0-4) : "))
nouveau = int(input("Nouveau valeur : "))

if 0 <= index < len(nombres):
    nombres[index] = nouveau
    print(f"Liste modifiée : {nombres}")
else:
    print("Index invalide")
```

**Explication** :
- **Indexation** : nombres[index] pour accéder/modifier
- **Validation** : vérification des bornes
- **Mutation** : modification directe de l'élément

**Test** : Remplacer l'index 2 (3) par 99 → [1, 2, 99, 4, 5].

---

### Exercice 74 : Recherche d'index
**Objectif** : Trouver l'index de la première occurrence d'un élément.

```python
# Solution
couleurs = ["rouge", "bleu", "vert", "rouge", "jaune"]
element = "rouge"

index = couleurs.index(element)
print(f"Premier '{element}' trouvé à l'index : {index}")

# Gestion d'erreur
try:
    index2 = couleurs.index("violet")
    print(f"Violet trouvé à l'index : {index2}")
except ValueError:
    print("Violet n'est pas dans la liste")
```

**Explication** :
- `.index()` : retourne l'index de la première occurrence
- **Exception** : ValueError si élément absent
- **Try/except** : gestion d'erreur élégante

**Test** : "rouge" → 0, "violet" → "Violet n'est pas dans la liste".

---

### Exercice 75 : Affichage avec indices
**Objectif** : Afficher les éléments d'une liste avec leur position.

```python
# Solution
villes = ["Paris", "Lyon", "Marseille", "Toulouse", "Nice"]
print("Villes avec leurs indices :")

for index, ville in enumerate(villes):
    print(f"{index}: {ville}")
```

**Explication** :
- `enumerate()` : génère (index, valeur) pairs
- **Formatage** : alignement index:valeur
- **Lisibilité** : affichage structuré

**Test** : 0: Paris, 1: Lyon, 2: Marseille, 3: Toulouse, 4: Nice.

---

### Exercice 76 : Doublage des éléments
**Objectif** : Parcourir une liste et doubler chaque élément.

```python
# Solution
nombres = [1, 2, 3, 4, 5]
print(f"Original : {nombres}")

for i in range(len(nombres)):
    nombres[i] *= 2

print(f"Doublé : {nombres}")
```

**Explication** :
- **Parcours par index** : range(len(liste))
- **Modification en place** : *= 2
- **Attention** : modification pendant l'itération

**Test** : [1, 2, 3, 4, 5] → [2, 4, 6, 8, 10].

---

### Exercice 77 : Triplage des éléments
**Objectif** : Parcourir une liste et tripler chaque élément.

```python
# Solution
nombres = [1, 2, 3, 4, 5]
print(f"Original : {nombres}")

for i in range(len(nombres)):
    nombres[i] *= 3

print(f"Triplé : {nombres}")
```

**Explication** :
- **Pattern similaire** : même logique que le doublage
- **Multiplication par 3** : *= 3
- **Transformation** : application d'une fonction à chaque élément

**Test** : [1, 2, 3, 4, 5] → [3, 6, 9, 12, 15].

---

### Exercice 78 : Filtrage des nombres pairs
**Objectif** : Afficher seulement les nombres pairs d'une liste.

```python
# Solution
nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print("Nombres pairs :")

for nombre in nombres:
    if nombre % 2 == 0:
        print(nombre, end=" ")
print()
```

**Explication** :
- **Test de parité** : nombre % 2 == 0
- **Filtrage** : affichage conditionnel
- **Séparation** : end=" " pour affichage horizontal

**Test** : 2 4 6 8 10.

---

### Exercice 79 : Filtrage des nombres impairs
**Objectif** : Afficher seulement les nombres impairs d'une liste.

```python
# Solution
nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print("Nombres impairs :")

for nombre in nombres:
    if nombre % 2 != 0:
        print(nombre, end=" ")
print()
```

**Explication** :
- **Négation** : != 0 pour les impairs
- **Complément** : tout ce qui n'est pas pair
- **Logique** : inverse du filtrage pair

**Test** : 1 3 5 7 9.

---

### Exercice 80 : Comptage d'occurrences
**Objectif** : Compter combien de fois un élément apparaît dans une liste.

```python
# Solution
nombres = [1, 2, 3, 2, 4, 2, 5, 2]
element = 2
compteur = 0

for nombre in nombres:
    if nombre == element:
        compteur += 1

print(f"L'élément {element} apparaît {compteur} fois")
```

**Explication** :
- **Compteur** : variable pour accumuler
- **Comparaison** : test d'égalité
- **Accumulation** : += 1 à chaque occurrence

**Test** : 2 apparaît 4 fois dans [1, 2, 3, 2, 4, 2, 5, 2].

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

# Recherche
element in liste          # Test d'appartenance
liste.index(element)      # Premier index
liste.count(element)      # Nombre d'occurrences
```

### 2. **Parcours de Listes**
```python
# Par valeurs
for element in liste:
    print(element)

# Par indices
for i in range(len(liste)):
    print(f"Index {i}: {liste[i]}")

# Par indices et valeurs
for i, element in enumerate(liste):
    print(f"{i}: {element}")
```

### 3. **Slicing (Extraction)**
```python
liste = [0, 1, 2, 3, 4, 5]

# Syntaxe : [début:fin:pas]
liste[1:4]      # [1, 2, 3] éléments 1 à 3
liste[:3]       # [0, 1, 2] du début à 2
liste[3:]       # [3, 4, 5] de 3 à la fin
liste[::2]      # [0, 2, 4] un élément sur deux
liste[::-1]     # [5, 4, 3, 2, 1, 0] inversion
```

### 4. **Listes Mutables**
- **Modification en place** : les listes peuvent être modifiées
- **Référence** : plusieurs variables peuvent pointer vers la même liste
- **Copie** : attention aux copies superficielles vs profondes

## 💡 Optimisations et Astuces

### 1. **Méthodes Efficaces**
```python
# Au lieu de boucles manuelles
compteur = nombres.count(element)  # Plus efficace
index = nombres.index(element)    # Plus simple
maximum = max(nombres)             # Built-in
somme = sum(nombres)              # Built-in
```

### 2. **Compréhensions de Liste**
```python
# Au lieu de :
pairs = []
for nombre in nombres:
    if nombre % 2 == 0:
        pairs.append(nombre)

# Utiliser :
pairs = [nombre for nombre in nombres if nombre % 2 == 0]
```

### 3. **Éviter la Modification Pendant l'Itération**
```python
# DANGER - Modification pendant itération
for nombre in nombres:
    if nombre % 2 == 0:
        nombres.remove(nombre)  # PEUT CAUSER DES ERREURS

# SÛR - Itération sur copie
for nombre in nombres[:]:  # Copie avec slicing
    if nombre % 2 == 0:
        nombres.remove(nombre)
```

## 🚀 Applications Pratiques

### 1. **Tri et Recherche**
```python
def trier_et_chercher(liste, element):
    """Trie et cherche un élément"""
    liste_triee = sorted(liste)
    try:
        index = liste_triee.index(element)
        return index, liste_triee
    except ValueError:
        return -1, liste_triee

nombres = [64, 34, 25, 12, 22, 11, 90]
position, triee = trier_et_chercher(nombres, 25)
print(f"Liste triée : {triee}")
print(f"25 trouvé à la position : {position}")
```

### 2. **Filtrage Multiple**
```python
def filtrer_plage(liste, minimum, maximum):
    """Retourne les éléments dans une plage"""
    return [x for x in liste if minimum <= x <= maximum]

nombres = [1, 5, 8, 12, 15, 18, 22, 25, 30]
resultat = filtrer_plage(nombres, 10, 20)
print(f"Nombres entre 10 et 20 : {resultat}")
```

### 3. **Statistiques sur Liste**
```python
def statistiques_liste(liste):
    """Calcule des statistiques de base"""
    if not liste:
        return None

    stats = {}
    stats["minimum"] = min(liste)
    stats["maximum"] = max(liste)
    stats["somme"] = sum(liste)
    stats["moyenne"] = stats["somme"] / len(liste)
    stats["longueur"] = len(liste)

    # Occurrences du minimum et maximum
    stats["min_occurrences"] = liste.count(stats["minimum"])
    stats["max_occurrences"] = liste.count(stats["maximum"])

    return stats

resultats = statistiques_liste([2, 5, 3, 2, 8, 2, 7])
for cle, valeur in resultats.items():
    print(f"{cle}: {valeur}")
```

## 🎯 Défis Supplémentaires

1. **Supprimez** les doublons d'une liste
2. **Inversez** l'ordre des éléments d'une liste
3. **Trouvez** les éléments communs à deux listes
4. **Implémentez** un tri par sélection

---

**Exercices complétés : 80/100** 🎯

*Continuez avec le [chapitre suivant](2-4-transformations.md) pour les transformations avancées !*