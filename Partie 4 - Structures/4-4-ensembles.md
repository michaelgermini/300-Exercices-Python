# Partie 4.4 : Ensembles

## 🎯 Objectifs Pédagogiques

Ce chapitre explore les **ensembles (sets)** en Python, structures de données pour gérer des **collections uniques** d'éléments. Les ensembles sont optimisés pour les tests d'appartenance et les opérations ensemblistes.

### Concepts Abordés
- **Création et manipulation** : ajout, suppression, unicité
- **Opérations ensemblistes** : union, intersection, différence
- **Tests d'appartenance** : performance et utilisation
- **Applications** : déduplication, filtrage, analyse

---

## 📝 Exercices Pratiques

### Exercice 175 : Créer un ensemble et y ajouter des éléments
**Objectif** : Créer un ensemble et ajouter des éléments uniques.

```python
# Solution
# Création d'un ensemble vide
mon_ensemble = set()
print(f"Ensemble vide : {mon_ensemble}")

# Ajout d'éléments
mon_ensemble.add("Python")
mon_ensemble.add("Java")
mon_ensemble.add("JavaScript")
mon_ensemble.add("Python")  # Doublon ignoré

print(f"Après ajouts : {mon_ensemble}")
print(f"Taille : {len(mon_ensemble)}")

# Création avec éléments initiaux
langages = {"Python", "Java", "C++", "JavaScript", "Python"}
print(f"Langages (avec doublon) : {langages}")
print(f"Taille : {len(langages)}")

# Ensemble à partir d'une liste
ma_liste = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
ensemble_liste = set(ma_liste)
print(f"Liste avec doublons : {ma_liste}")
print(f"Ensemble unique : {ensemble_liste}")

# Ensemble à partir d'une chaîne
texte = "hello world"
ensemble_lettres = set(texte)
print(f"Texte : '{texte}'")
print(f"Lettres uniques : {ensemble_lettres}")
```

**Explication** :
- **set()** : constructeur d'ensemble vide
- **.add()** : ajout d'un élément (ignoré si déjà présent)
- **Unicité** : doublons automatiquement supprimés
- **Conversion** : set(liste) pour déduplication
- **Itérables** : chaînes, listes, tuples → ensembles

**Test** : {"Python", "Java", "JavaScript"} (3 éléments, pas 4).

---

### Exercice 176 : Supprimer un élément d'un ensemble
**Objectif** : Supprimer des éléments d'un ensemble.

```python
# Solution
nombres = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
print(f"Ensemble initial : {nombres}")

# Suppression d'un élément existant
nombres.remove(5)
print(f"Après remove(5) : {nombres}")

# Suppression avec discard() (plus sûr)
nombres.discard(15)  # N'existe pas, pas d'erreur
print(f"Après discard(15) : {nombres}")

try:
    nombres.remove(15)  # N'existe pas, erreur
    print(f"Après remove(15) : {nombres}")
except KeyError as e:
    print(f"Erreur remove(15) : {e}")

# Suppression et récupération
element_supprime = nombres.pop()  # Supprime un élément au hasard
print(f"Élément supprimé avec pop() : {element_supprime}")
print(f"Ensemble après pop() : {nombres}")

# Vider l'ensemble
nombres.clear()
print(f"Ensemble vidé : {nombres}")
print(f"Est vide : {len(nombres) == 0}")
```

**Explication** :
- **.remove()** : supprime un élément (KeyError si absent)
- **.discard()** : supprime un élément (silencieux si absent)
- **.pop()** : supprime et retourne un élément aléatoire
- **.clear()** : vide l'ensemble
- **Sécurité** : discard() plus sûr que remove()

**Test** : Suppression progressive d'éléments.

---

### Exercice 177 : Vérifier l'existence d'un élément dans un ensemble
**Objectif** : Tester l'appartenance d'éléments à un ensemble.

```python
# Solution
fruits = {"pomme", "banane", "orange", "kiwi", "mangue"}

# Test avec 'in'
elements_a_tester = ["pomme", "banane", "fraise", "ananas", "kiwi"]

print("Tests d'appartenance :")
for element in elements_a_tester:
    if element in fruits:
        print(f"✓ {element} est dans l'ensemble")
    else:
        print(f"✗ {element} n'est pas dans l'ensemble")

# Test avec des nombres
nombres_pairs = {2, 4, 6, 8, 10, 12, 14, 16, 18, 20}

print("\nTests avec des nombres pairs :")
for i in range(1, 11):
    if i in nombres_pairs:
        print(f"✓ {i} est pair")
    else:
        print(f"✗ {i} n'est pas pair")

# Performance : ensembles vs listes
import time

grande_liste = list(range(1000000))
grand_ensemble = set(range(1000000))

# Test dans une liste
debut = time.time()
resultat_liste = 999999 in grande_liste
fin = time.time()
print(f"\nRecherche dans liste (1M éléments) : {fin - debut:.6f}s")

# Test dans un ensemble
debut = time.time()
resultat_ensemble = 999999 in grand_ensemble
fin = time.time()
print(f"Recherche dans ensemble (1M éléments) : {fin - debut:.6f}s")

print(f"Rapport de performance : {((fin - debut) / ((fin - debut) or 1)):.1f}x plus rapide")
```

**Explication** :
- **Opérateur in** : test d'appartenance
- **Performance** : O(1) pour les ensembles vs O(n) pour les listes
- **Applications** : tests rapides, validation
- **Optimisation** : ensembles pour les tests d'appartenance

**Test** : Tests de présence avec performances.

---

### Exercice 178 : Trouver l'union de deux ensembles
**Objectif** : Calculer l'union (tous les éléments distincts) de deux ensembles.

```python
# Solution
ensemble1 = {1, 2, 3, 4, 5}
ensemble2 = {4, 5, 6, 7, 8}
ensemble3 = {7, 8, 9, 10}

print(f"Ensemble 1 : {ensemble1}")
print(f"Ensemble 2 : {ensemble2}")
print(f"Ensemble 3 : {ensemble3}")

# Union de deux ensembles
union_1_2 = ensemble1.union(ensemble2)
print(f"Union 1 ∪ 2 : {union_1_2}")

# Union avec |
union_1_3 = ensemble1 | ensemble3
print(f"Union 1 ∪ 3 : {union_1_3}")

# Union de trois ensembles
union_tous = ensemble1 | ensemble2 | ensemble3
print(f"Union 1 ∪ 2 ∪ 3 : {union_tous}")

# Union avec update
ensemble1_copy = ensemble1.copy()
ensemble1_copy.update(ensemble2)
print(f"Update 1 avec 2 : {ensemble1_copy}")

# Union avec des ensembles de types différents
nombres = {1, 2, 3}
textes = {"a", "b", "c"}
union_mixte = nombres | textes
print(f"Union nombres et textes : {union_mixte}")
```

**Explication** :
- **.union()** : méthode pour l'union
- **| opérateur** : syntaxe plus concise
- **Union multiple** : avec plusieurs ensembles
- **Types mixtes** : ensembles hétérogènes possibles

**Test** : {1, 2, 3, 4, 5} ∪ {4, 5, 6, 7, 8} = {1, 2, 3, 4, 5, 6, 7, 8}.

---

### Exercice 179 : Trouver l'intersection de deux ensembles
**Objectif** : Calculer l'intersection (éléments communs) de deux ensembles.

```python
# Solution
etudiants_info = {"Alice", "Bob", "Charlie", "Diana"}
etudiants_math = {"Bob", "Charlie", "Eve", "Frank"}
etudiants_phy = {"Alice", "Diana", "Eve", "Grace"}

print(f"Étudiants Info : {etudiants_info}")
print(f"Étudiants Math : {etudiants_math}")
print(f"Étudiants Physique : {etudiants_phy}")

# Intersection de deux ensembles
intersection_info_math = etudiants_info.intersection(etudiants_math)
print(f"Info ∩ Math : {intersection_info_math}")

# Intersection avec &
intersection_info_phy = etudiants_info & etudiants_phy
print(f"Info ∩ Physique : {intersection_info_phy}")

# Intersection de trois ensembles
intersection_tous = etudiants_info & etudiants_math & etudiants_phy
print(f"Info ∩ Math ∩ Physique : {intersection_tous}")

# Étudiants qui font au moins deux matières
au_moins_deux = (etudiants_info & etudiants_math) | (etudiants_info & etudiants_phy) | (etudiants_math & etudiants_phy)
print(f"Au moins deux matières : {au_moins_deux}")

# Étudiants dans une seule matière
une_seule_info = etudiants_info - etudiants_math - etudiants_phy
une_seule_math = etudiants_math - etudiants_info - etudiants_phy
une_seule_phy = etudiants_phy - etudiants_info - etudiants_math

print(f"Info seulement : {une_seule_info}")
print(f"Math seulement : {une_seule_math}")
print(f"Physique seulement : {une_seule_phy}")
```

**Explication** :
- **.intersection()** : éléments communs
- **& opérateur** : syntaxe concise
- **Intersection multiple** : éléments dans tous les ensembles
- **Applications** : recoupements, filtres

**Test** : Info ∩ Math = {"Bob", "Charlie"}.

---

### Exercice 180 : Trouver la différence de deux ensembles
**Objectif** : Calculer la différence (éléments dans A mais pas dans B).

```python
# Solution
ensemble_a = {1, 2, 3, 4, 5, 6}
ensemble_b = {4, 5, 6, 7, 8, 9}
ensemble_c = {10, 11, 12}

print(f"Ensemble A : {ensemble_a}")
print(f"Ensemble B : {ensemble_b}")
print(f"Ensemble C : {ensemble_c}")

# Différence A - B
difference_a_b = ensemble_a.difference(ensemble_b)
print(f"A - B : {difference_a_b}")

# Différence avec -
difference_b_a = ensemble_b - ensemble_a
print(f"B - A : {difference_b_a}")

# Différence symétrique (A - B) ∪ (B - A)
difference_sym = ensemble_a.symmetric_difference(ensemble_b)
print(f"A Δ B (différence symétrique) : {difference_sym}")

# Avec ^
difference_sym2 = ensemble_a ^ ensemble_b
print(f"A Δ B (avec ^) : {difference_sym2}")

# Différence avec update
ensemble_a_copy = ensemble_a.copy()
ensemble_a_copy -= ensemble_b  # A = A - B
print(f"A après A -= B : {ensemble_a_copy}")

# Test d'ensembles disjoints
disjoints = ensemble_a.isdisjoint(ensemble_c)
print(f"A et C sont disjoints : {disjoints}")
```

**Explication** :
- **.difference()** : A - B (éléments dans A mais pas B)
- **- opérateur** : syntaxe concise
- **Différence symétrique** : éléments dans A ou B mais pas dans les deux
- **^ opérateur** : XOR ensembliste
- **Disjoints** : aucun élément commun

**Test** : A - B = {1, 2, 3}, B - A = {7, 8, 9}.

---

### Exercice 181 : Supprimer les doublons d'une liste
**Objectif** : Utiliser un ensemble pour supprimer les doublons d'une liste.

```python
# Solution
# Liste avec doublons
nombres_avec_doublons = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4, 5, 5, 5, 5, 5]
print(f"Liste avec doublons : {nombres_avec_doublons}")
print(f"Longueur avec doublons : {len(nombres_avec_doublons)}")

# Méthode 1 : conversion en ensemble puis en liste
nombres_uniques = list(set(nombres_avec_doublons))
print(f"Ensemble unique : {set(nombres_avec_doublons)}")
print(f"Liste unique : {nombres_uniques}")
print(f"Longueur unique : {len(nombres_uniques)}")

# Méthode 2 : compréhension avec ensemble
uniques_comprehension = list({x for x in nombres_avec_doublons})
print(f"Avec compréhension : {uniques_comprehension}")

# Déduplication de texte
texte = "hello world hello python world python"
mots = texte.split()
mots_uniques = list(set(mots))
print(f"\nTexte : '{texte}'")
print(f"Mots : {mots}")
print(f"Mots uniques : {mots_uniques}")
print(f"Nombre de mots : {len(mots)}")
print(f"Mots uniques : {len(mots_uniques)}")

# Déduplication avec préservation de l'ordre (Python 3.7+)
from collections import OrderedDict
mots_ordre_preserve = list(OrderedDict.fromkeys(mots))
print(f"Ordre préservé : {mots_ordre_preserve}")
```

**Explication** :
- **set()** : suppression automatique des doublons
- **list(set())** : conversion en liste
- **Compréhension** : syntaxe concise
- **Ordre** : set() ne préserve pas l'ordre
- **OrderedDict** : préservation de l'ordre (Python 3.7+)

**Test** : [1, 2, 2, 3, 3, 3] → [1, 2, 3].

---

### Exercice 182 : Compresser une liste de chaînes
**Objectif** : Utiliser un ensemble pour analyser des chaînes.

```python
# Solution
# Liste de chaînes
chaines = ["python", "java", "python", "javascript", "java", "c++", "python", "ruby"]

print(f"Chaînes : {chaines}")
print(f"Nombre total : {len(chaines)}")

# Chaînes uniques
chaines_uniques = set(chaines)
print(f"Chaînes uniques : {chaines_uniques}")
print(f"Nombre unique : {len(chaines_uniques)}")

# Analyse des longueurs
longueurs = {len(chaine) for chaine in chaines}
print(f"Longueurs présentes : {longueurs}")

# Caractères uniques dans toutes les chaînes
tous_caracteres = set()
for chaine in chaines:
    tous_caracteres.update(set(chaine))

print(f"Caractères utilisés : {tous_caracteres}")

# Caractères communs à toutes les chaînes
caracteres_communs = set(chaines[0])
for chaine in chaines[1:]:
    caracteres_communs &= set(chaine)

print(f"Caractères communs : {caracteres_communs}")

# Mots les plus fréquents
from collections import Counter
frequences = Counter(chaines)
print(f"Fréquences : {dict(frequences)}")
print(f"Plus fréquent : {frequences.most_common(1)[0]}")
```

**Explication** :
- **Analyse textuelle** : ensembles pour caractères uniques
- **Intersection** : caractères communs
- **Counter** : fréquences des éléments
- **Applications** : traitement de texte, analyse

**Test** : "python", "java", "python" → caractères communs : set().

---

### Exercice 183 : Décompresser une liste de chaînes
**Objectif** : Utiliser un ensemble pour décompresser et analyser des données.

```python
# Solution
# Données compressées (simulation)
donnees_compressees = [
    ("utilisateurs", ["alice", "bob", "alice", "charlie", "bob", "diana"]),
    ("produits", ["laptop", "mouse", "laptop", "keyboard", "mouse"]),
    ("categories", ["electronique", "electronique", "bureau", "bureau", "bureau"])
]

print("Analyse de données compressées :")
for nom_categorie, elements in donnees_compressees:
    print(f"\n{nom_categorie.upper()} :")
    print(f"  Éléments : {elements}")
    print(f"  Total : {len(elements)}")

    # Éléments uniques
    uniques = set(elements)
    print(f"  Uniques : {uniques}")
    print(f"  Nombre unique : {len(uniques)}")

    # Fréquences
    from collections import Counter
    freq = Counter(elements)
    print(f"  Fréquences : {dict(freq)}")

    # Plus et moins fréquents
    plus_freq = freq.most_common(1)[0]
    moins_freq = freq.most_common()[-1]
    print(f"  Plus fréquent : {plus_freq}")
    print(f"  Moins fréquent : {moins_freq}")

# Analyse croisée
tous_utilisateurs = set(donnees_compressees[0][1])
tous_produits = set(donnees_compressees[1][1])

print("
Analyse croisée :")
print(f"Utilisateurs : {tous_utilisateurs}")
print(f"Produits : {tous_produits}")
print(f"Intersection (utilisateurs achetant) : {tous_utilisateurs & tous_produits}")
```

**Explication** :
- **Données compressées** : simulation de données dupliquées
- **Analyse** : déduplication et statistiques
- **Fréquences** : Counter pour le comptage
- **Croisée** : intersection entre catégories
- **Applications** : business intelligence, analyse

**Test** : Analyse d'utilisateurs, produits et catégories.

---

## 🔍 Points Clés à Retenir

### 1. **Création d'Ensembles**
```python
# Ensemble vide
vide = set()

# Ensemble avec éléments
mon_ensemble = {1, 2, 3, 4, 5}
autre_ensemble = {1, 2, 3, 2, 1}  # Doublons supprimés

# À partir d'itérables
set([1, 2, 3])           # Liste
set((1, 2, 3))           # Tuple
set("hello")             # Chaîne -> {'h', 'e', 'l', 'o'}

# Ensemble par compréhension
pairs = {x for x in range(10) if x % 2 == 0}
carres = {x**2 for x in range(5)}
```

### 2. **Modification d'Ensembles**
```python
# Ajout
ensemble.add(element)          # Ajout d'un élément
ensemble.update([a, b, c])     # Ajout de plusieurs éléments

# Suppression
ensemble.remove(element)       # KeyError si absent
ensemble.discard(element)      # Silencieux si absent
ensemble.pop()                # Supprime un élément aléatoire
ensemble.clear()              # Vide l'ensemble

# Opérations en place
ensemble1.update(ensemble2)    # Union en place
ensemble1.intersection_update(ensemble2)  # Intersection en place
ensemble1.difference_update(ensemble2)    # Différence en place
```

### 3. **Opérations Ensemblistes**
```python
ensemble1 = {1, 2, 3, 4}
ensemble2 = {3, 4, 5, 6}

# Union
ensemble1 | ensemble2                    # {1, 2, 3, 4, 5, 6}
ensemble1.union(ensemble2)              # {1, 2, 3, 4, 5, 6}

# Intersection
ensemble1 & ensemble2                    # {3, 4}
ensemble1.intersection(ensemble2)       # {3, 4}

# Différence
ensemble1 - ensemble2                    # {1, 2}
ensemble1.difference(ensemble2)        # {1, 2}

# Différence symétrique
ensemble1 ^ ensemble2                    # {1, 2, 5, 6}
ensemble1.symmetric_difference(ensemble2)  # {1, 2, 5, 6}

# Tests
ensemble1.issubset(ensemble2)            # Est-ce que ensemble1 ⊆ ensemble2 ?
ensemble1.issuperset(ensemble2)          # Est-ce que ensemble1 ⊇ ensemble2 ?
ensemble1.isdisjoint(ensemble2)          # Ensembles disjoints ?
```

### 4. **Performance et Utilisation**
```python
# Tests d'appartenance (O(1))
if element in ensemble:
    print("Présent")

# Recherche dans valeurs (O(n))
if element in ensemble.values():  # Erreur ! Ensembles n'ont pas de .values()

# Conversion pour déduplication
liste_avec_doublons = [1, 2, 2, 3, 3, 3]
liste_unique = list(set(liste_avec_doublons))  # [1, 2, 3]
```

## 💡 Optimisations et Astuces

### 1. **Déduplication Efficace**
```python
# Méthode lente (O(n²))
def dedup_lent(liste):
    resultat = []
    for element in liste:
        if element not in resultat:
            resultat.append(element)
    return resultat

# Méthode rapide (O(n))
def dedup_rapide(liste):
    return list(set(liste))

# Avec préservation de l'ordre (Python 3.7+)
from collections import OrderedDict
def dedup_ordre(liste):
    return list(OrderedDict.fromkeys(liste))
```

### 2. **Tests d'Appartenance Multiples**
```python
# Test multiple avec ensembles
def filtrer_par_criteres(elements, criteres):
    """Filtre les éléments selon plusieurs critères"""
    resultat = set()

    if "positifs" in criteres:
        resultat.update(x for x in elements if x > 0)
    if "pairs" in criteres:
        resultat.update(x for x in elements if x % 2 == 0)
    if "inferieurs_10" in criteres:
        resultat.update(x for x in elements if x < 10)

    return resultat

# Test
nombres = list(range(-5, 16))
criteres = ["positifs", "pairs", "inferieurs_10"]
filtres = filtrer_par_criteres(nombres, criteres)
print(f"Éléments répondant aux critères : {filtres}")
```

### 3. **Analyse de Texte**
```python
def analyser_texte_complet(texte):
    """Analyse complète d'un texte avec ensembles"""
    # Préparation
    mots = texte.lower().replace(".", "").replace(",", "").replace("!", "").replace("?", "").split()

    # Analyses
    analyses = {
        "mots_uniques": set(mots),
        "caracteres_uniques": set(texte.lower()),
        "longueurs_mots": {len(mot) for mot in mots},
        "mots_longs": {mot for mot in mots if len(mot) > 5},
        "mots_courts": {mot for mot in mots if len(mot) <= 3},
        "voyelles_utilisees": {c for c in texte.lower() if c in "aeiou"},
        "consonnes_utilisees": {c for c in texte.lower() if c.isalpha() and c not in "aeiou"}
    }

    # Statistiques
    analyses["stats"] = {
        "total_mots": len(mots),
        "mots_uniques_count": len(analyses["mots_uniques"]),
        "caracteres_uniques_count": len(analyses["caracteres_uniques"]),
        "pourcentage_mots_uniques": (len(analyses["mots_uniques"]) / len(mots)) * 100 if mots else 0
    }

    return analyses

# Test
texte = "Le Python est un langage de programmation très puissant et polyvalent."
analyse = analyser_texte_complet(texte)
for cle, valeur in analyse.items():
    print(f"{cle}: {valeur}")
    print()
```

## 🚀 Applications Pratiques

### 1. **Système de Recommandation**
```python
def systeme_recommandation(utilisateurs, preferences):
    """Système de recommandation simple"""
    # Préparation des données
    utilisateur_cible = "Alice"
    preferences_alice = preferences[utilisateur_cible]

    # Utilisateurs similaires (intersection des préférences)
    similarites = {}
    for utilisateur, prefs in preferences.items():
        if utilisateur != utilisateur_cible:
            intersection = preferences_alice & prefs
            union = preferences_alice | prefs
            similarite = len(intersection) / len(union) if union else 0
            similarites[utilisateur] = similarite

    # Recommandations : items aimés par les similaires mais pas par Alice
    utilisateurs_similaires = [u for u, s in similarites.items() if s > 0.3]
    recommendations = set()

    for utilisateur in utilisateurs_similaires:
        prefs_similaire = preferences[utilisateur]
        recommendations.update(prefs_similaire - preferences_alice)

    return {
        "utilisateur": utilisateur_cible,
        "preferences": preferences_alice,
        "utilisateurs_similaires": utilisateurs_similaires,
        "similarites": similarites,
        "recommendations": recommendations
    }

# Test
preferences = {
    "Alice": {"Python", "Java", "JavaScript"},
    "Bob": {"Python", "C++", "JavaScript"},
    "Charlie": {"Java", "C#", "SQL"},
    "Diana": {"Python", "Java", "SQL"}
}

reco = systeme_recommandation(list(preferences.keys()), preferences)
print("Recommandations pour Alice :")
for cle, valeur in reco.items():
    print(f"  {cle}: {valeur}")
```

### 2. **Analyseur de Données**
```python
def analyser_donnees_ensemblistes(donnees):
    """Analyse de données avec des ensembles"""
    # Conversion en ensembles pour analyse
    tous_elements = set()
    elements_par_categorie = {}

    for categorie, elements in donnees.items():
        elements_set = set(elements)
        tous_elements.update(elements_set)
        elements_par_categorie[categorie] = elements_set

    # Analyses ensemblistes
    analyses = {
        "total_elements_uniques": len(tous_elements),
        "elements_par_categorie": {cat: len(elements) for cat, elements in elements_par_categorie.items()},
        "intersection_tous": set.intersection(*elements_par_categorie.values()) if elements_par_categorie else set(),
        "union_tous": set.union(*elements_par_categorie.values()) if elements_par_categorie else set()
    }

    # Similarités entre catégories
    similarites = {}
    categories = list(elements_par_categorie.keys())

    for i, cat1 in enumerate(categories):
        for cat2 in categories[i+1:]:
            intersection = elements_par_categorie[cat1] & elements_par_categorie[cat2]
            union = elements_par_categorie[cat1] | elements_par_categorie[cat2]
            similarite = len(intersection) / len(union) if union else 0
            similarites[f"{cat1}_{cat2}"] = similarite

    analyses["similarites"] = similarites

    return analyses

# Test
donnees_test = {
    "fruits": ["pomme", "banane", "orange", "pomme", "banane"],
    "legumes": ["carotte", "tomate", "pomme de terre", "carotte"],
    "couleurs": ["rouge", "orange", "vert", "rouge"],
    "nombres": [1, 2, 3, 1, 2]
}

analyse = analyser_donnees_ensemblistes(donnees_test)
print("Analyse ensembliste :")
for cle, valeur in analyse.items():
    print(f"  {cle}: {valeur}")
```

### 3. **Validateur de Données**
```python
def valider_donnees_ensemblistes(donnees, regles):
    """Valide des données selon des règles ensemblistes"""
    resultats = {}

    # Règles disponibles
    regles_disponibles = {
        "unicite": lambda x: len(x) == len(set(x)),
        "plage": lambda x, min_val, max_val: all(min_val <= val <= max_val for val in x),
        "types_homogenes": lambda x: len({type(val).__name__ for val in x}) == 1,
        "pas_de_valeurs_nulles": lambda x: all(val is not None for val in x),
        "longueur_minimale": lambda x, min_len: all(len(str(val)) >= min_len for val in x)
    }

    # Application des règles
    for nom_regle, params in regles.items():
        if nom_regle in regles_disponibles:
            if isinstance(params, dict):
                resultat = regles_disponibles[nom_regle](donnees, **params)
            else:
                resultat = regles_disponibles[nom_regle](donnees, *params)
            resultats[nom_regle] = resultat

    # Validation croisée
    if "unicite" in resultats and "types_homogenes" in resultats:
        resultats["donnees_valides"] = resultats["unicite"] and resultats["types_homogenes"]

    return resultats

# Test
donnees_a_valider = [1, 2, 3, 4, 5, 1]  # Non unique
regles_validation = {
    "unicite": {},
    "plage": {"min_val": 0, "max_val": 10},
    "types_homogenes": {},
    "pas_de_valeurs_nulles": {},
    "longueur_minimale": {"min_len": 1}
}

validation = valider_donnees_ensemblistes(donnees_a_valider, regles_validation)
print("Validation des données :")
for regle, resultat in validation.items():
    print(f"  {regle}: {resultat}")
```

## 🎯 Défis Supplémentaires

1. **Créez** une fonction qui trouve les éléments uniques à chaque ensemble
2. **Implémentez** un système de tags avec des ensembles
3. **Développez** un analyseur de similarité entre textes
4. **Concevez** un système de filtrage collaboratif avec des ensembles

---

**Exercices complétés : 183/200** 🎯

*Continuez avec le [chapitre suivant](4-5-comprehensions.md) pour les compréhensions avancées !*