# Partie 2.2 : Boucles for et while

## 🎯 Objectifs Pédagogiques

Ce chapitre explore les **boucles** en Python, essentielles pour **automatiser les tâches répétitives**. Les boucles permettent d'exécuter du code plusieurs fois selon des conditions ou des séquences.

### Concepts Abordés
- **Boucle for** : itération sur séquences (listes, chaînes, range)
- **Boucle while** : itération conditionnelle
- **Instructions de contrôle** : break, continue, pass
- **Applications pratiques** : sommes, produits, recherches

---

## 📝 Exercices Pratiques

### Exercice 61 : Multiples de 3 jusqu'à 100
**Objectif** : Afficher tous les multiples de 3 de 3 à 99.

```python
# Solution
print("Multiples de 3 de 3 à 99 :")
for i in range(3, 100, 3):
    print(i, end=" ")
print()
```

**Explication** :
- `range(3, 100, 3)` : séquence 3, 6, 9, ..., 99
- **Pas de 3** : génère uniquement les multiples
- **Efficacité** : méthode directe sans test

**Test** : 3 6 9 ... 96 99 (33 nombres).

---

### Exercice 62 : Multiples de 5 jusqu'à 100
**Objectif** : Afficher tous les multiples de 5 de 5 à 100.

```python
# Solution
print("Multiples de 5 de 5 à 100 :")
for i in range(5, 101, 5):
    print(i, end=" ")
print()
```

**Explication** :
- **Range inclusif** : range(5, 101, 5) pour inclure 100
- **Progression arithmétique** : raison 5
- **Pattern** : 5 × 1, 5 × 2, ..., 5 × 20

**Test** : 5 10 15 ... 95 100 (20 nombres).

---

### Exercice 63 : Année bissextile
**Objectif** : Vérifier si une année est bissextile.

```python
# Solution
annee = int(input("Entrez une année : "))

if (annee % 4 == 0 and annee % 100 != 0) or (annee % 400 == 0):
    print(f"{annee} est une année bissextile")
else:
    print(f"{annee} n'est pas une année bissextile")
```

**Explication** :
- **Règles bissextiles** :
  - Divisible par 4
  - SAUF si divisible par 100 (sauf si divisible par 400)
- **Opérateurs logiques** : combinaison de conditions
- **Précision** : algorithme exact

**Test** : 2024 (oui), 2023 (non), 2000 (oui), 1900 (non).

---

### Exercice 64 : Nombres pairs d'une liste
**Objectif** : Afficher seulement les nombres pairs d'une liste.

```python
# Solution
# Création d'une liste de test
nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print("Nombres pairs de la liste :")

for nombre in nombres:
    if nombre % 2 == 0:
        print(nombre, end=" ")
print()
```

**Explication** :
- **Itération sur liste** : `for nombre in nombres`
- **Test de parité** : condition dans la boucle
- **Filtrage** : affichage sélectif

**Test** : 2 4 6 8 10.

---

### Exercice 65 : Nombres impairs d'une liste
**Objectif** : Afficher seulement les nombres impairs d'une liste.

```python
# Solution
nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print("Nombres impairs de la liste :")

for nombre in nombres:
    if nombre % 2 != 0:
        print(nombre, end=" ")
print()
```

**Explication** :
- **Négation** : `!= 0` au lieu de `== 0`
- **Logique inverse** : impair = pas pair
- **Complément** : couvre tous les autres nombres

**Test** : 1 3 5 7 9.

---

### Exercice 66 : Somme des éléments d'une liste
**Objectif** : Calculer la somme de tous les éléments d'une liste.

```python
# Solution
nombres = [10, 20, 30, 40, 50]
somme = 0

for nombre in nombres:
    somme += nombre

print(f"Somme des éléments : {somme}")
```

**Explication** :
- **Accumulateur** : variable somme initialisée à 0
- `+=` : addition et affectation
- **Itération** : traitement de chaque élément

**Test** : 10+20+30+40+50 = 150.

---

### Exercice 67 : Produit des éléments d'une liste
**Objectif** : Calculer le produit de tous les éléments d'une liste.

```python
# Solution
nombres = [1, 2, 3, 4, 5]
produit = 1  # Élément neutre pour la multiplication

for nombre in nombres:
    produit *= nombre

print(f"Produit des éléments : {produit}")
```

**Explication** :
- **Initialisation** : produit = 1 (neutre)
- `*= ` : multiplication et affectation
- **Croissance** : multiplication successive

**Test** : 1×2×3×4×5 = 120.

---

### Exercice 68 : Compteur positif/négatif
**Objectif** : Compter les nombres positifs et négatifs d'une liste.

```python
# Solution
nombres = [10, -5, 3, -8, 0, 15, -2]
positifs = 0
negatifs = 0

for nombre in nombres:
    if nombre > 0:
        positifs += 1
    elif nombre < 0:
        negatifs += 1

print(f"Nombre de positifs : {positifs}")
print(f"Nombre de négatifs : {negatifs}")
print(f"Nombre de zéros : {len(nombres) - positifs - negatifs}")
```

**Explication** :
- **Compteurs séparés** : suivi distinct positif/négatif
- **elif** : exclusion mutuelle des cas
- **Calcul complémentaire** : zéros par soustraction

**Test** : Positifs: 3, Négatifs: 3, Zéros: 1.

---

### Exercice 69 : Maximum d'une liste
**Objectif** : Trouver le plus grand élément d'une liste.

```python
# Solution
nombres = [15, 3, 9, 27, 18, 5]
maximum = nombres[0]  # Premier élément comme référence

for nombre in nombres[1:]:  # Commencer du deuxième
    if nombre > maximum:
        maximum = nombre

print(f"Le maximum est : {maximum}")
```

**Explication** :
- **Initialisation** : premier élément comme candidat
- **Comparaison successive** : test de chaque élément
- **Mise à jour** : nouveau maximum si trouvé

**Test** : 27 dans [15, 3, 9, 27, 18, 5].

---

### Exercice 70 : Minimum d'une liste
**Objectif** : Trouver le plus petit élément d'une liste.

```python
# Solution
nombres = [15, 3, 9, 27, 18, 5]
minimum = nombres[0]

for nombre in nombres[1:]:
    if nombre < minimum:
        minimum = nombre

print(f"Le minimum est : {minimum}")
```

**Explication** :
- **Logique symétrique** : < au lieu de >
- **Initialisation identique** : premier élément
- **Mise à jour** : nouveau minimum si trouvé

**Test** : 3 dans [15, 3, 9, 27, 18, 5].

---

## 🔍 Points Clés à Retenir

### 1. **Boucle for**
```python
# Syntaxe générale
for element in sequence:
    # Code à exécuter pour chaque élément

# Exemples de séquences
for i in range(10):        # 0 à 9
for i in range(1, 11):     # 1 à 10
for i in range(0, 20, 2):  # 0, 2, 4, ..., 18
for lettre in "Python":    # P, y, t, h, o, n
for nombre in [1, 2, 3]:   # 1, 2, 3
```

### 2. **Boucle while**
```python
# Syntaxe générale
while condition:
    # Code exécuté tant que condition vraie

# Exemple
compteur = 1
while compteur <= 5:
    print(compteur)
    compteur += 1
```

### 3. **Instructions de Contrôle**
- `break` : sort immédiatement de la boucle
- `continue` : passe à l'itération suivante
- `pass` : ne fait rien (placeholder)

### 4. **Range Function**
- `range(stop)` : 0 à stop-1
- `range(start, stop)` : start à stop-1
- `range(start, stop, step)` : avec pas

## 💡 Optimisations et Astuces

### 1. **Fonctions Built-in**
```python
# Au lieu de boucles manuelles
maximum = max(nombres)  # Plus efficace
minimum = min(nombres)
somme = sum(nombres)
longueur = len(nombres)
```

### 2. **Compréhension de Liste**
```python
# Au lieu de :
pairs = []
for nombre in nombres:
    if nombre % 2 == 0:
        pairs.append(nombre)

# Utiliser :
pairs = [nombre for nombre in nombres if nombre % 2 == 0]
```

### 3. **Itération avec Index**
```python
# Accès à l'index et la valeur
for index, valeur in enumerate(nombres):
    print(f"Index {index}: {valeur}")

# Itération sur indices
for i in range(len(nombres)):
    print(f"Position {i}: {nombres[i]}")
```

## 🚀 Applications Pratiques

### 1. **Recherche dans une Liste**
```python
def chercher_element(liste, element):
    """Retourne l'index de l'élément ou -1"""
    for i, valeur in enumerate(liste):
        if valeur == element:
            return i
    return -1

nombres = [10, 20, 30, 40, 50]
position = chercher_element(nombres, 30)
print(f"30 trouvé à l'index : {position}")
```

### 2. **Filtrage de Données**
```python
def filtrer_positifs(nombres):
    """Retourne une liste des nombres positifs"""
    positifs = []
    for nombre in nombres:
        if nombre > 0:
            positifs.append(nombre)
    return positifs

resultat = filtrer_positifs([-5, 10, -3, 8, 0])
print(f"Nombres positifs : {resultat}")
```

### 3. **Statistiques Simples**
```python
def statistiques_basiques(nombres):
    """Calcule min, max, somme, moyenne"""
    if not nombres:  # Liste vide
        return None

    minimum = maximum = nombres[0]
    somme = 0

    for nombre in nombres:
        if nombre < minimum:
            minimum = nombre
        if nombre > maximum:
            maximum = nombre
        somme += nombre

    moyenne = somme / len(nombres)
    return minimum, maximum, somme, moyenne

stats = statistiques_basiques([15, 3, 9, 27, 18, 5])
print(f"Min: {stats[0]}, Max: {stats[1]}, Somme: {stats[2]}, Moyenne: {stats[3]:.2f}")
```

## 🎯 Défis Supplémentaires

1. **Trouvez** le deuxième plus grand élément d'une liste
2. **Comptez** les occurrences de chaque élément
3. **Triez** une liste par ordre croissant (tri bulle)
4. **Implémentez** la recherche dichotomique

---

**Exercices complétés : 70/100** 🎯

*Continuez avec le [chapitre suivant](2-3-listes.md) pour la manipulation de listes !*