# Partie 4.2 : Tuples

## 🎯 Objectifs Pédagogiques

Ce chapitre explore les **tuples** en Python, structures de données **immuables** (non modifiables). Les tuples sont utilisés pour des données qui ne doivent pas changer après création.

### Concepts Abordés
- **Création et accès** : syntaxe, indexation, slicing
- **Immutabilité** : protection contre les modifications
- **Conversion** : liste ↔ tuple, utilisations pratiques
- **Applications** : coordonnées, enregistrements, clés de dictionnaires

---

## 📝 Exercices Pratiques

### Exercice 161 : Créer un tuple et y accéder
**Objectif** : Créer un tuple et accéder à ses éléments.

```python
# Solution
# Création d'un tuple
mon_tuple = (1, 2, 3, 4, 5)
print(f"Tuple créé : {mon_tuple}")
print(f"Type : {type(mon_tuple)}")

# Accès par index
print(f"Premier élément : {mon_tuple[0]}")
print(f"Dernier élément : {mon_tuple[-1]}")
print(f"Éléments 1 à 3 : {mon_tuple[1:4]}")

# Tuple avec différents types
tuple_mixte = ("Python", 3.9, True, [1, 2, 3])
print(f"Tuple mixte : {tuple_mixte}")
print(f"Types : {[type(x).__name__ for x in tuple_mixte]}")

# Tuple vide et singleton
tuple_vide = ()
singleton = (42,)  # Note : virgule obligatoire
print(f"Tuple vide : {tuple_vide}")
print(f"Singleton : {singleton}, type : {type(singleton)}")
```

**Explication** :
- **Syntaxe** : (élément1, élément2, ...)
- **Parenthèses optionnelles** : 1, 2, 3 == (1, 2, 3)
- **Indexation** : même que les listes
- **Singleton** : (42,) pour éviter la confusion avec les expressions
- **Immutabilité** : protection contre les modifications

**Test** : (1, 2, 3, 4, 5), types mixtes autorisés.

---

### Exercice 162 : Convertir une liste en tuple
**Objectif** : Convertir une liste en tuple et inversement.

```python
# Solution
# Liste vers tuple
ma_liste = [1, 2, 3, 4, 5]
mon_tuple = tuple(ma_liste)
print(f"Liste : {ma_liste}")
print(f"Tuple : {mon_tuple}")

# Tuple vers liste
mon_tuple = (10, 20, 30, 40, 50)
ma_liste = list(mon_tuple)
print(f"Tuple : {mon_tuple}")
print(f"Liste : {ma_liste}")

# Modification après conversion
ma_liste.append(60)
print(f"Liste modifiée : {ma_liste}")
print(f"Tuple original inchangé : {mon_tuple}")

# Conversion avec types mixtes
mixte_liste = ["a", 1, True, [1, 2]]
mixte_tuple = tuple(mixte_liste)
print(f"Liste mixte : {mixte_liste}")
print(f"Tuple mixte : {mixte_tuple}")
```

**Explication** :
- **tuple()** : constructeur de tuple
- **list()** : constructeur de liste
- **Conversion** : copie les éléments
- **Indépendance** : modifications n'affectent pas l'original
- **Immutabilité** : tuple protégé, liste modifiable

**Test** : [1, 2, 3, 4, 5] → (1, 2, 3, 4, 5) → [1, 2, 3, 4, 5, 60].

---

### Exercice 163 : Convertir un tuple en liste
**Objectif** : Convertir un tuple en liste pour le modifier.

```python
# Solution
# Tuple immuable
coordonnees = (10, 20, 30)
print(f"Coordonnées originales : {coordonnees}")

# Conversion pour modification
coord_liste = list(coordonnees)
coord_liste[1] = 25  # Modification
coordonnees_modifiees = tuple(coord_liste)

print(f"Coordonnées modifiées : {coordonnees_modifiees}")
print(f"Original inchangé : {coordonnees}")

# Utilisation pratique : ajout d'éléments
personne = ("Alice", 25, "Paris")
print(f"Personne : {personne}")

# Ajout d'information
personne_liste = list(personne)
personne_liste.append("Développeuse")
personne_complete = tuple(personne_liste)
print(f"Personne complète : {personne_complete}")
```

**Explication** :
- **Workflow** : tuple → liste → modification → tuple
- **Préservation** : tuple original intact
- **Applications** : données de référence modifiées temporairement
- **Immutabilité** : protection des données sensibles

**Test** : (10, 20, 30) → modification index 1 → (10, 25, 30).

---

### Exercice 164 : Utilisation des tuples dans les fonctions
**Objectif** : Utiliser des tuples pour retourner plusieurs valeurs.

```python
# Solution
def statistiques(nombres):
    """Retourne plusieurs statistiques dans un tuple"""
    if not nombres:
        return (0, 0, 0, 0)

    minimum = min(nombres)
    maximum = max(nombres)
    somme = sum(nombres)
    moyenne = somme / len(nombres)

    return (minimum, maximum, somme, moyenne)

# Test
donnees = [15, 8, 12, 20, 7, 18, 25, 4, 9]
stats = statistiques(donnees)

print(f"Données : {donnees}")
print(f"Statistiques : {stats}")
print(f"Minimum : {stats[0]}")
print(f"Maximum : {stats[1]}")
print(f"Somme : {stats[2]}")
print(f"Moyenne : {stats[3]:.2f}")

# Déballage du tuple
min_val, max_val, sum_val, avg_val = statistiques(donnees)
print(f"\nDéballage : min={min_val}, max={max_val}, sum={sum_val}, avg={avg_val:.2f}")
```

**Explication** :
- **Retour multiple** : tuple pour plusieurs valeurs
- **Déballage** : affectation simultanée
- **Indexation** : accès par position
- **Applications** : fonctions renvoyant plusieurs résultats

**Test** : retourne (4, 25, 118, 13.11).

---

### Exercice 165 : Tuples nommés et déballage
**Objectif** : Utiliser le déballage de tuples et les tuples nommés.

```python
# Solution
# Déballage simple
point = (10, 20)
x, y = point
print(f"Point : {point}")
print(f"x = {x}, y = {y}")

# Déballage avec *
coordonnees = (1, 2, 3, 4, 5)
premier, *milieu, dernier = coordonnees
print(f"Premier : {premier}")
print(f"Milieu : {milieu}")
print(f"Dernier : {dernier}")

# Échange de valeurs avec tuple
a, b = 5, 10
print(f"Avant échange : a={a}, b={b}")
a, b = b, a  # Échange avec tuple
print(f"Après échange : a={a}, b={b}")

# Tuples nommés (collections.namedtuple)
from collections import namedtuple

# Définition d'un type
Personne = namedtuple('Personne', ['nom', 'age', 'ville'])
alice = Personne('Alice', 25, 'Paris')

print(f"\nTuple nommé : {alice}")
print(f"Nom : {alice.nom}")
print(f"Âge : {alice.age}")
print(f"Ville : {alice.ville}")

# Conversion en dictionnaire
print(f"En dictionnaire : {alice._asdict()}")
```

**Explication** :
- **Déballage** : affectation par position
- **Déballage étendu** : * pour les éléments du milieu
- **Échange** : a, b = b, a technique classique
- **Namedtuple** : tuples avec noms d'attributs
- **Immutabilité** : même que les tuples normaux

**Test** : (10, 20) → x=10, y=20.

---

## 🔍 Points Clés à Retenir

### 1. **Création de Tuples**
```python
# Tuple vide
tuple_vide = ()

# Tuple singleton (virgule obligatoire)
singleton = (42,)

# Tuple normal
mon_tuple = (1, 2, 3)
autre_tuple = 1, 2, 3  # Parenthèses optionnelles

# Tuple mixte
mixte = ("Python", 3.9, True, [1, 2, 3])

# Namedtuple
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y', 'z'])
p = Point(1, 2, 3)
```

### 2. **Accès aux Éléments**
```python
mon_tuple = (10, 20, 30, 40, 50)

# Indexation
mon_tuple[0]    # 10 (premier)
mon_tuple[-1]   # 50 (dernier)
mon_tuple[2]    # 30 (troisième)

# Slicing
mon_tuple[1:4]  # (20, 30, 40)
mon_tuple[:3]   # (10, 20, 30)
mon_tuple[2:]   # (30, 40, 50)
mon_tuple[::-1] # (50, 40, 30, 20, 10)
```

### 3. **Déballage (Unpacking)**
```python
# Déballage simple
x, y, z = (1, 2, 3)

# Déballage étendu
premier, *milieu, dernier = (1, 2, 3, 4, 5)
# premier=1, milieu=[2, 3, 4], dernier=5

# Échange de variables
a, b = b, a

# Ignorer des éléments
x, _, z = (1, 2, 3)  # x=1, z=3 (ignore 2)
```

### 4. **Conversion**
```python
# Liste vers tuple
ma_liste = [1, 2, 3]
mon_tuple = tuple(ma_liste)  # (1, 2, 3)

# Tuple vers liste
mon_tuple = (1, 2, 3)
ma_liste = list(mon_tuple)   # [1, 2, 3]

# Chaîne vers tuple de caractères
texte = "Python"
tuple_lettres = tuple(texte)  # ('P', 'y', 't', 'h', 'o', 'n')
```

## 💡 Optimisations et Astuces

### 1. **Tuples comme Clés de Dictionnaire**
```python
# Les tuples sont hashables (utilisables comme clés)
coordonnees = {(0, 0): "origine", (1, 0): "est", (0, 1): "nord"}
print(coordonnees[(1, 0)])  # "est"

# Les listes ne le sont pas (erreur)
# coordonnees_listes = {[0, 0]: "origine"}  # TypeError
```

### 2. **Tuples pour les Valeurs de Retour**
```python
# Retour de plusieurs valeurs
def division_entiere(a, b):
    quotient = a // b
    reste = a % b
    return (quotient, reste)  # Tuple

resultat = division_entiere(17, 5)
print(f"17 ÷ 5 = {resultat[0]} reste {resultat[1]}")

# Déballage direct
quotient, reste = division_entiere(17, 5)
print(f"Quotient: {quotient}, Reste: {reste}")
```

### 3. **Performance : Tuples vs Listes**
```python
import time

# Test de performance
taille = 1000000

# Création liste
debut = time.time()
liste = [i for i in range(taille)]
fin = time.time()
print(f"Création liste : {fin - debut:.4f}s")

# Création tuple
debut = time.time()
tuple_data = tuple(range(taille))
fin = time.time()
print(f"Création tuple : {fin - debut:.4f}s")

# Accès (tuple plus rapide)
debut = time.time()
for i in range(1000):
    _ = liste[i]
fin = time.time()
print(f"Accès liste : {fin - debut:.4f}s")

debut = time.time()
for i in range(1000):
    _ = tuple_data[i]
fin = time.time()
print(f"Accès tuple : {fin - debut:.4f}s")
```

## 🚀 Applications Pratiques

### 1. **Gestion de Coordonnées**
```python
def calculer_distance(point1, point2):
    """Calcule la distance entre deux points 2D"""
    x1, y1 = point1
    x2, y2 = point2

    distance = ((x2 - x1)**2 + (y2 - y1)**2)**0.5
    return distance

def deplacer_point(point, dx, dy):
    """Déplace un point d'un vecteur (dx, dy)"""
    x, y = point
    return (x + dx, y + dy)

# Tests
point_a = (0, 0)
point_b = (3, 4)

distance = calculer_distance(point_a, point_b)
print(f"Distance entre {point_a} et {point_b} : {distance:.2f}")

point_c = deplacer_point(point_a, 5, 7)
print(f"Point A {point_a} déplacé de (5,7) : {point_c}")

# Triangle
points = [(0, 0), (3, 0), (0, 4)]
distances = [calculer_distance(points[i], points[(i+1) % 3]) for i in range(3)]
print(f"Distances du triangle : {distances}")
```

### 2. **Statistiques avec Tuples**
```python
def statistiques_tuplees(donnees):
    """Retourne les statistiques dans un tuple nommé"""
    from collections import namedtuple

    Stats = namedtuple('Statistiques', ['minimum', 'maximum', 'somme', 'moyenne', 'effectif'])

    if not donnees:
        return Stats(0, 0, 0, 0, 0)

    minimum = min(donnees)
    maximum = max(donnees)
    somme = sum(donnees)
    moyenne = somme / len(donnees)
    effectif = len(donnees)

    return Stats(minimum, maximum, somme, moyenne, effectif)

# Test
notes = [12, 15, 8, 18, 14, 9, 16, 11]
stats = statistiques_tuplees(notes)

print(f"Notes : {notes}")
print(f"Minimum : {stats.minimum}")
print(f"Maximum : {stats.maximum}")
print(f"Somme : {stats.somme}")
print(f"Moyenne : {stats.moyenne:.2f}")
print(f"Effectif : {stats.effectif}")

# Accès par index aussi possible
print(f"Stats[0] (min) : {stats[0]}")
print(f"Stats[3] (moy) : {stats[3]:.2f}")
```

### 3. **Gestion d'Inventaire**
```python
def gerer_inventaire():
    """Simule un système d'inventaire avec tuples"""
    # Articles : (nom, quantite, prix_unitaire)
    inventaire = [
        ("Ordinateur", 10, 800),
        ("Souris", 50, 25),
        ("Clavier", 30, 45),
        ("Écran", 15, 200),
        ("Imprimante", 5, 150)
    ]

    print("=== INVENTAIRE ===")
    total_valeur = 0

    for article in inventaire:
        nom, quantite, prix = article
        valeur_article = quantite * prix
        total_valeur += valeur_article

        print(f"{nom:12} | Qté: {quantite:3d} | Prix: {prix:6.2f}€ | Valeur: {valeur_article:8.2f}€")

    print("-" * 50)
    print(f"Valeur totale inventaire : {total_valeur:.2f}€")

    # Recherche d'article
    article_recherche = "Souris"
    for article in inventaire:
        if article[0] == article_recherche:
            print(f"\nArticle '{article_recherche}' trouvé :")
            print(f"Quantité: {article[1]}")
            print(f"Prix unitaire: {article[2]}€")
            break
    else:
        print(f"\nArticle '{article_recherche}' non trouvé")

gerer_inventaire()
```

## 🎯 Défis Supplémentaires

1. **Créez** une fonction qui trie une liste de tuples par le deuxième élément
2. **Implémentez** un système de coordonnées 3D avec des tuples
3. **Développez** une fonction pour calculer le barycentre de points
4. **Concevez** un dictionnaire avec des tuples comme clés (dates, coordonnées)

---

**Exercices complétés : 165/200** 🎯

*Continuez avec le [chapitre suivant](4-3-dictionnaires.md) pour explorer les dictionnaires !*