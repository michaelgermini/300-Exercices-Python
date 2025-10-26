# Partie 3.5 : Applications Pratiques des Fonctions

## 🎯 Objectifs Pédagogiques

Ce chapitre final de la Partie 3 présente des **applications pratiques** combinant tous les concepts de fonctions : fonctions de base, récursives, lambda, modules standard, et décorateurs.

### Concepts Intégrés
- **Applications du quotidien** : calculs, conversions, validations
- **Fonctions utilitaires** : formatage, manipulation, analyse
- **Programmation fonctionnelle** : map, filter, reduce
- **Applications avancées** : générateurs, décorateurs, modules

---

## 📝 Exercices Pratiques

### Exercice 141 : Fonction pour afficher les éléments d'une liste en majuscules
**Objectif** : Créer une fonction qui affiche les éléments d'une liste en majuscules.

```python
# Solution
def afficher_majuscules(liste):
    """Affiche les éléments d'une liste en majuscules"""
    for element in liste:
        print(str(element).upper())

# Tests
listes_test = [
    ["python", "java", "javascript"],
    ["hello", "world"],
    ["Linux", "Windows", "macOS"],
    [1, 2, 3],  # Conversion automatique en string
    []
]

print("Affichage en majuscules :")
for i, liste in enumerate(listes_test):
    print(f"\nListe {i+1} : {liste}")
    afficher_majuscules(liste)
```

**Explication** :
- **Conversion string** : str() pour tous types
- **.upper()** : méthode de chaînes
- **Itération** : affichage de chaque élément
- **Robustesse** : gère types mixtes

**Test** : ["python", "java"] → PYTHON, JAVA.

---

### Exercice 142 : Fonction pour afficher les éléments d'une liste en minuscules
**Objectif** : Créer une fonction qui affiche les éléments d'une liste en minuscules.

```python
# Solution
def afficher_minuscules(liste):
    """Affiche les éléments d'une liste en minuscules"""
    for element in liste:
        print(str(element).lower())

# Tests
listes_test = [
    ["PYTHON", "JAVA", "JAVASCRIPT"],
    ["Hello", "WORLD"],
    ["Linux", "Windows", "macOS"],
    [1, 2, 3],
    []
]

print("Affichage en minuscules :")
for i, liste in enumerate(listes_test):
    print(f"\nListe {i+1} : {liste}")
    afficher_minuscules(liste)
```

**Explication** :
- **.lower()** : conversion en minuscules
- **Pattern similaire** : même structure que majuscules
- **Application** : normalisation de texte
- **Comparaison** : gère majuscules existantes

**Test** : ["PYTHON", "JAVA"] → python, java.

---

### Exercice 143 : Fonction pour vérifier si une liste est vide
**Objectif** : Créer une fonction qui vérifie si une liste est vide.

```python
# Solution
def est_vide(liste):
    """Vérifie si une liste est vide"""
    return len(liste) == 0

# Tests
listes_test = [
    [],
    [1, 2, 3],
    [""],
    ["non vide"],
    [0, 0, 0],
    [],
    [None]
]

print("Tests de liste vide :")
for i, liste in enumerate(listes_test):
    resultat = est_vide(liste)
    print(f"Liste {i+1} {liste} est vide : {resultat}")

# Alternative avec vérité
print("\nAvec opérateur de vérité :")
for i, liste in enumerate(listes_test):
    resultat = not liste  # Liste vide = False
    print(f"Liste {i+1} est vide : {resultat}")
```

**Explication** :
- **Longueur** : len(liste) == 0
- **Opérateur vérité** : not liste
- **Types** : fonctionne avec toutes les séquences
- **Convention** : standard en Python

**Test** : [] (vide), [1, 2, 3] (non vide), [""] (non vide).

---

### Exercice 144 : Fonction pour compter les éléments d'une liste
**Objectif** : Créer une fonction qui compte les éléments d'une liste.

```python
# Solution
def compter_elements(liste):
    """Compte le nombre d'éléments dans une liste"""
    return len(liste)

# Tests
listes_test = [
    [1, 2, 3, 4, 5],
    ["a", "b", "c"],
    [],
    [1],
    list(range(100)),  # 0 à 99
    [x for x in range(50)]  # 0 à 49
]

print("Comptage d'éléments :")
for i, liste in enumerate(listes_test):
    nombre = compter_elements(liste)
    print(f"Liste {i+1} contient {nombre} éléments")

# Comparaison avec built-in
print("\nComparaison avec len() :")
for i, liste in enumerate(listes_test):
    notre_compte = compter_elements(liste)
    builtin_compte = len(liste)
    print(f"Liste {i+1} : notre fonction={notre_compte}, len()={builtin_compte}, identique={notre_compte == builtin_compte}")
```

**Explication** :
- **Fonction simple** : wrapper de len()
- **Pédagogie** : compréhension de len()
- **Équivalence** : même résultat que built-in
- **Applications** : validation, statistiques

**Test** : [1, 2, 3, 4, 5] → 5 éléments.

---

### Exercice 145 : Fonction pour inverser une liste
**Objectif** : Créer une fonction qui inverse l'ordre des éléments d'une liste.

```python
# Solution
def inverser_liste(liste):
    """Inverse l'ordre des éléments d'une liste"""
    return liste[::-1]

# Tests
listes_test = [
    [1, 2, 3, 4, 5],
    ["a", "b", "c"],
    [1],
    [],
    [1, 2, 3, 2, 1],  # Palindrome
    list(range(10))   # 0 à 9
]

print("Inversion de listes :")
for i, liste in enumerate(listes_test):
    inverse = inverser_liste(liste)
    print(f"Original : {liste}")
    print(f"Inverse  : {inverse}")
    print(f"Est palindrome : {liste == inverse}\n")
```

**Explication** :
- **Slicing** : [::-1] technique d'inversion
- **Nouvelle liste** : ne modifie pas l'originale
- **Efficacité** : méthode optimisée Python
- **Test palindrome** : liste == inverse

**Test** : [1, 2, 3, 4, 5] → [5, 4, 3, 2, 1].

---

### Exercice 146 : Fonction pour extraire un sous-ensemble d'une liste
**Objectif** : Créer une fonction qui extrait un sous-ensemble d'une liste.

```python
# Solution
def extraire_sous_ensemble(liste, debut, longueur):
    """Extrait un sous-ensemble d'une liste"""
    fin = debut + longueur
    return liste[debut:fin]

# Tests
grande_liste = list(range(20))  # [0, 1, 2, ..., 19]

extractions = [
    (0, 5),   # 5 premiers
    (5, 5),   # du 6ème au 10ème
    (15, 5),  # 5 derniers
    (10, 10), # du 11ème au 20ème
    (0, 0),   # liste vide
]

print(f"Liste complète : {grande_liste}")
print("\nExtractions de sous-ensembles :")
for i, (debut, longueur) in enumerate(extractions):
    sous_ensemble = extraire_sous_ensemble(grande_liste, debut, longueur)
    print(f"Extraction {i+1} (début={debut}, longueur={longueur}) : {sous_ensemble}")
```

**Explication** :
- **Slicing calculé** : debut:debut+longueur
- **Validation implicite** : slicing gère les dépassements
- **Utilité** : pagination, fenêtrage
- **Paramètres** : position et taille

**Test** : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19] → extraction [5, 5] = [5, 6, 7, 8, 9].

---

### Exercice 147 : Fonction pour fusionner plusieurs listes
**Objectif** : Créer une fonction qui fusionne plusieurs listes.

```python
# Solution
def fusionner_listes(*listes):
    """Fusionne plusieurs listes en une seule"""
    resultat = []
    for liste in listes:
        resultat.extend(liste)
    return resultat

# Tests
liste1 = [1, 2, 3]
liste2 = [4, 5]
liste3 = [6, 7, 8, 9]
liste4 = []

fusion_tests = [
    fusionner_listes(liste1, liste2),
    fusionner_listes(liste1, liste2, liste3),
    fusionner_listes(liste1),
    fusionner_listes(liste1, liste4, liste3),
    fusionner_listes(),  # Aucune liste
]

print("Fusion de plusieurs listes :")
for i, resultat in enumerate(fusion_tests):
    print(f"Fusion {i+1} : {resultat}")

# Comparaison avec opérateur +
print(f"\nComparaison avec + : {liste1 + liste2} vs {fusionner_listes(liste1, liste2)}")
```

**Explication** :
- **Paramètres variables** : *listes
- **.extend()** : ajout de plusieurs éléments
- **Alternative** : opérateur + (pour 2 listes)
- **Robustesse** : gère listes vides

**Test** : [1, 2, 3] + [4, 5] + [6, 7, 8, 9] = [1, 2, 3, 4, 5, 6, 7, 8, 9].

---

### Exercice 148 : Fonction pour vérifier si une liste est vide (lambda)
**Objectif** : Créer une fonction lambda qui vérifie si une liste est vide.

```python
# Solution
est_vide_lambda = lambda liste: len(liste) == 0

# Tests
listes_test = [
    [],
    [1, 2, 3],
    [""],
    ["texte"],
    [0, 0, 0],
    [],
    [None, None]
]

print("Tests avec fonction lambda :")
for i, liste in enumerate(listes_test):
    resultat = est_vide_lambda(liste)
    print(f"Liste {i+1} {liste} est vide : {resultat}")

# Utilisation avec filter
print("\nFiltrage des listes vides :")
toutes_listes = [[], [1, 2], [], [3, 4], []]
listes_pleines = list(filter(lambda x: not est_vide_lambda(x), toutes_listes))
print(f"Listes pleines : {listes_pleines}")
```

**Explication** :
- **Lambda simple** : condition directe
- **Utilisation avancée** : avec filter()
- **Logique** : not est_vide pour les pleines
- **Applications** : filtrage de données

**Test** : [] (True), [1, 2, 3] (False), [""] (False).

---

### Exercice 149 : Fonction pour calculer la moyenne d'une liste (lambda)
**Objectif** : Créer une fonction lambda qui calcule la moyenne d'une liste.

```python
# Solution
moyenne_lambda = lambda nombres: sum(nombres) / len(nombres) if nombres else 0

# Tests
listes_test = [
    [1, 2, 3, 4, 5],
    [10, 20, 30, 40, 50],
    [2, 4, 6, 8],
    [],
    [100]
]

print("Calculs de moyenne avec lambda :")
for i, liste in enumerate(listes_test):
    resultat = moyenne_lambda(liste)
    print(f"Moyenne {i+1} : {resultat:.2f}")

# Comparaison avec fonction classique
def moyenne_classique(nombres):
    return sum(nombres) / len(nombres) if nombres else 0

print("\nComparaison lambda vs classique :")
for liste in listes_test:
    lambda_result = moyenne_lambda(liste)
    classique_result = moyenne_classique(liste)
    print(f"Identique : {lambda_result == classique_result}")
```

**Explication** :
- **Expression conditionnelle** : if nombres else 0
- **Lambda complexe** : plusieurs opérations
- **Équivalence** : même résultat que fonction classique
- **Conciseness** : code compact

**Test** : [1, 2, 3, 4, 5] → 3.00, [] → 0.

---

### Exercice 150 : Synthèse complète des fonctions
**Objectif** : Créer une application complète combinant tous les concepts de fonctions.

```python
# Solution - Analyseur de données complet
def analyseur_complet(donnees, operations=None):
    """Analyse complète de données avec fonctions"""
    if operations is None:
        operations = ["statistiques", "filtres", "transformations", "validations"]

    resultat = {}

    # 1. Analyse avec listes
    resultat["listes"] = {
        "longueur": len(donnees),
        "somme": sum(donnees),
        "moyenne": sum(donnees) / len(donnees) if donnees else 0,
        "minimum": min(donnees) if donnees else None,
        "maximum": max(donnees) if donnees else None,
        "pairs": [x for x in donnees if x % 2 == 0],
        "impairs": [x for x in donnees if x % 2 != 0],
        "carres": [x**2 for x in donnees],
        "doubles": [x*2 for x in donnees]
    }

    # 2. Analyse avec ensembles
    resultat["ensembles"] = {
        "uniques": set(donnees),
        "nombre_uniques": len(set(donnees)),
        "pourcentage_uniques": (len(set(donnees)) / len(donnees) * 100) if donnees else 0,
        "positifs": {x for x in donnees if x > 0},
        "negatifs": {x for x in donnees if x < 0},
        "divisibles_par_3": {x for x in donnees if x % 3 == 0}
    }

    # 3. Analyse avec dictionnaires
    resultat["dictionnaires"] = {
        "frequences": {x: donnees.count(x) for x in set(donnees)},
        "indices": {x: [i for i, val in enumerate(donnees) if val == x] for x in set(donnees)},
        "proprietes": {
            x: {
                "carre": x**2,
                "double": x*2,
                "parite": "pair" if x % 2 == 0 else "impair",
                "signe": "positif" if x > 0 else "négatif" if x < 0 else "nul"
            }
            for x in set(donnees)
        }
    }

    # 4. Analyse avec tuples
    resultat["tuples"] = {
        "statistiques": (len(donnees), sum(donnees), max(donnees), min(donnees)),
        "paires_valeur_index": [(x, i) for i, x in enumerate(donnees)],
        "groupes_parite": (
            [x for x in donnees if x % 2 == 0],
            [x for x in donnees if x % 2 != 0]
        )
    }

    # 5. Matrices et structures complexes
    resultat["matrices"] = {
        "matrice_identite": [[1 if i == j else 0 for j in range(5)] for i in range(5)],
        "matrice_valeurs": [[x for x in donnees[:5]] for _ in range(3)],  # Répétition
        "statistiques_matrice": [
            [len(donnees), sum(donnees)],
            [len(resultat["ensembles"]["uniques"]), len([x for x in donnees if x > 0])]
        ]
    }

    return resultat

# Test avec données variées
donnees_test = [15, 8, 12, 20, 7, 18, 25, 4, 9, 18, 15, 7, 12, 8, 20]
analyse_complete = analyseur_complet(donnees_test)

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

### 1. **Intégration des Concepts**
```python
# Combinaison de tout
def traitement_complet(donnees):
    # Fonction classique
    def nettoyer(d):
        return [x for x in d if x is not None]

    # Lambda pour transformation
    doubler = lambda x: x * 2

    # Map et filter
    nettoyees = nettoyer(donnees)
    positives = list(filter(lambda x: x > 0, nettoyees))
    doublees = list(map(doubler, positives))

    return {
        "original": donnees,
        "nettoye": nettoyees,
        "positives": positives,
        "doublees": doublees
    }
```

### 2. **Fonctions d'Ordre Supérieur**
```python
# Map : transformation
nombres = [1, 2, 3, 4, 5]
carres = list(map(lambda x: x**2, nombres))  # [1, 4, 9, 16, 25]

# Filter : sélection
pairs = list(filter(lambda x: x % 2 == 0, nombres))  # [2, 4]

# Reduce : agrégation
from functools import reduce
produit = reduce(lambda x, y: x * y, nombres)  # 120

# Sorted avec clé
mots = ["banane", "pomme", "kiwi"]
tries = sorted(mots, key=lambda mot: len(mot))  # ["kiwi", "pomme", "banane"]
```

### 3. **Décorateurs Avancés**
```python
# Décorateur avec paramètres
def retry(n_tentatives):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for i in range(n_tentatives):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if i == n_tentatives - 1:
                        raise e
                    print(f"Tentative {i+1} échouée, retry...")
            return None
        return wrapper
    return decorator

# Utilisation
@retry(3)
def operation_risquee():
    import random
    if random.random() < 0.7:  # 70% de chance d'échec
        raise ValueError("Échec aléatoire")
    return "Succès"
```

## 💡 Optimisations et Extensions

### 1. **Fonctions Génériques**
```python
# Fonction qui s'adapte au type
def traiter_elements(elements, operation):
    """Applique une opération à tous les éléments"""
    if not elements:
        return elements

    # Adaptation selon le type
    if isinstance(elements[0], str):
        return [operation(str(element)) for element in elements]
    elif isinstance(elements[0], (int, float)):
        return [operation(float(element)) for element in elements]
    else:
        return [operation(element) for element in elements]

# Tests
nombres = [1, 2, 3, 4, 5]
textes = ["hello", "world", "python"]

# Avec lambda
resultat1 = traiter_elements(nombres, lambda x: x**2)
resultat2 = traiter_elements(textes, lambda x: x.upper())

print(f"Carrés : {resultat1}")
print(f"Majuscules : {resultat2}")
```

### 2. **Composition de Fonctions**
```python
# Composition manuelle
def composer(f, g):
    """Retourne une fonction qui applique g puis f"""
    return lambda x: f(g(x))

# Exemple
double = lambda x: x * 2
carre = lambda x: x ** 2
double_carre = composer(carre, double)  # d'abord double, puis carré

# Test
for x in [1, 2, 3, 4]:
    print(f"{x} → double={double(x)} → double_carre={double_carre(x)}")
```

### 3. **Fonctions Partielle et Curryfication**
```python
from functools import partial

# Fonction avec paramètres multiples
def puissance(base, exposant):
    return base ** exposant

# Création de fonctions spécialisées
carre = partial(puissance, exposant=2)  # base^2
cube = partial(puissance, exposant=3)   # base^3

# Tests
for base in [2, 3, 4, 5]:
    print(f"{base}^2 = {carre(base)}, {base}^3 = {cube(base)}")
```

## 🚀 Applications Pratiques

### 1. **Système de Traitement de Données**
```python
def systeme_traitement(donnees_brutes, pipeline):
    """Traite des données selon un pipeline de fonctions"""
    resultat = donnees_brutes

    for etape in pipeline:
        nom_etape, fonction = etape
        print(f"Étape: {nom_etape}")
        resultat = fonction(resultat)
        print(f"Résultat: {resultat}")

    return resultat

# Pipeline de traitement
pipeline = [
    ("nettoyage", lambda x: [i for i in x if i is not None]),
    ("filtrage", lambda x: list(filter(lambda i: i > 0, x))),
    ("transformation", lambda x: list(map(lambda i: i * 2, x))),
    ("tri", lambda x: sorted(x)),
    ("statistiques", lambda x: {
        "somme": sum(x),
        "moyenne": sum(x)/len(x) if x else 0,
        "effectif": len(x)
    })
]

# Données de test
donnees = [10, -5, None, 15, 0, 25, None, 8, -3]
resultat_final = systeme_traitement(donnees, pipeline)
print(f"\nRésultat final : {resultat_final}")
```

### 2. **Générateur de Rapports**
```python
def generateur_rapport(donnees, format_sortie="complet"):
    """Génère un rapport formaté des données"""
    rapport = {}

    # Analyse de base
    rapport["analyse"] = {
        "type": type(donnees).__name__,
        "effectif": len(donnees),
        "valeurs_uniques": len(set(donnees)) if donnees else 0,
        "valeurs_dupliquees": len(donnees) - len(set(donnees)) if donnees else 0
    }

    # Statistiques conditionnelles
    if all(isinstance(x, (int, float)) for x in donnees):
        nombres = [x for x in donnees if isinstance(x, (int, float))]
        rapport["statistiques"] = {
            "somme": sum(nombres),
            "moyenne": sum(nombres) / len(nombres) if nombres else 0,
            "minimum": min(nombres) if nombres else None,
            "maximum": max(nombres) if nombres else None,
            "pairs": len([x for x in nombres if x % 2 == 0]),
            "impairs": len([x for x in nombres if x % 2 != 0])
        }

    # Transformations
    rapport["transformations"] = {
        "inverses": list(reversed(donnees)),
        "tries_croissant": sorted(donnees),
        "tries_decroissant": sorted(donnees, reverse=True)
    }

    # Formatage selon le type demandé
    if format_sortie == "complet":
        return rapport
    elif format_sortie == "statistiques":
        return rapport.get("statistiques", {})
    elif format_sortie == "analyse":
        return rapport.get("analyse", {})
    else:
        return str(rapport)

# Tests
donnees_test = [15, 8, 12, 20, 7, 18, 25, 4, 9, 18]
rapport = generateur_rapport(donnees_test, "complet")

print("Rapport complet généré :")
for section, contenu in rapport.items():
    print(f"\n{section.upper()}:")
    if isinstance(contenu, dict):
        for cle, valeur in contenu.items():
            print(f"  {cle}: {valeur}")
    else:
        print(f"  {contenu}")
```

### 3. **Calculateur Intelligent**
```python
def calculateur_intelligent(expression, variables=None):
    """Évalue une expression avec variables"""
    if variables is None:
        variables = {}

    try:
        # Ajout des variables dans l'environnement
        environnement = {
            "pi": 3.14159,
            "e": 2.71828,
            **variables
        }

        # Évaluation sécurisée
        resultat = eval(expression, {"__builtins__": {}}, environnement)

        # Formatage selon le type
        if isinstance(resultat, float):
            return round(resultat, 4)
        else:
            return resultat

    except Exception as e:
        return f"Erreur: {e}"

# Tests
expressions = [
    "2 + 3 * 4",
    "pi * 2**2",
    "sqrt(16)",
    "sin(pi/2)",
    "x + y",
    "a * b + c"
]

variables_tests = [
    {},
    {},
    {},
    {},
    {"x": 5, "y": 3},
    {"a": 2, "b": 3, "c": 1}
]

print("Calculateur intelligent:")
for expr, vars in zip(expressions, variables_tests):
    resultat = calculateur_intelligent(expr, vars)
    print(f"{expr} = {resultat}")
```

## 🎯 Bilan de la Partie 3

### Concepts Maîtrisés
✅ **Fonctions de base** : définition, paramètres, return
✅ **Fonctions avancées** : récursivité, *args, **kwargs
✅ **Fonctions lambda** : syntaxe anonyme, utilisation
✅ **Modules standard** : math, random, datetime
✅ **Fonctions d'ordre supérieur** : map, filter, sorted
✅ **Décorateurs** : modification de fonctions
✅ **Applications pratiques** : analyse, traitement, génération

### Compétences Développées
- **Modularité** : découpage du code en fonctions
- **Réutilisabilité** : fonctions génériques et spécialisées
- **Programmation fonctionnelle** : style déclaratif
- **Optimisation** : choix des bonnes structures
- **Robustesse** : gestion d'erreurs et cas limites

---

**🏁 FIN DE LA PARTIE 3 - BRAVO !**

**Exercices complétés : 150/150** 🎯

*Félicitations ! Vous avez terminé les fonctions et modules. Continuez avec la [Partie 4](Partie%204%20-%20Structures/4-1-listes.md) pour explorer les structures de données !*