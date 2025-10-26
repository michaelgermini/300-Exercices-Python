# Partie 2.5 : Tests et Validations

## 🎯 Objectifs Pédagogiques

Ce chapitre final de la Partie 2 explore les **tests de validation** et les **opérations avancées sur les listes**. Nous consolidons tous les concepts de contrôle de flux avec des applications pratiques.

### Concepts Abordés
- **Tests d'appartenance** : éléments communs, intersections
- **Filtres conditionnels** : nombres > 10, < 10, dans des plages
- **Génération de séquences** : nombres spécifiques, exclusions
- **Validations complexes** : multiples conditions simultanées

---

## 📝 Exercices Pratiques

### Exercice 91 : Filtres conditionnels (> 10)
**Objectif** : Afficher les nombres d'une liste qui sont supérieurs à 10.

```python
# Solution
nombres = [5, 15, 8, 12, 3, 18, 7, 25, 1, 10]
print("Nombres supérieurs à 10 :")

for nombre in nombres:
    if nombre > 10:
        print(nombre, end=" ")
print()
```

**Explication** :
- **Comparaison** : > 10 pour le seuil
- **Filtrage** : affichage conditionnel
- **Application** : seuils, limites, filtrage

**Test** : 15, 12, 18, 25.

---

### Exercice 92 : Filtres conditionnels (< 10)
**Objectif** : Afficher les nombres d'une liste qui sont inférieurs à 10.

```python
# Solution
nombres = [5, 15, 8, 12, 3, 18, 7, 25, 1, 10]
print("Nombres inférieurs à 10 :")

for nombre in nombres:
    if nombre < 10:
        print(nombre, end=" ")
print()
```

**Explication** :
- **Comparaison inverse** : < 10
- **Complément** : tout ce qui n'est pas > 10
- **Logique** : filtrage par borne inférieure

**Test** : 5, 8, 3, 7, 1.

---

### Exercice 93 : Génération 1 à 50
**Objectif** : Créer une liste avec les nombres de 1 à 50.

```python
# Solution
nombres_1_50 = []
for i in range(1, 51):
    nombres_1_50.append(i)

print(f"Liste de 1 à 50 : {len(nombres_1_50)} éléments")
print(f"Premier : {nombres_1_50[0]}, Dernier : {nombres_1_50[-1]}")

# Alternative avec compréhension
nombres_alt = [i for i in range(1, 51)]
print(f"Même résultat avec compréhension : {len(nombres_alt)} éléments")
```

**Explanation** :
- **Génération séquentielle** : range(1, 51)
- **Accumulation** : append dans une liste vide
- **Vérification** : premier et dernier éléments

**Test** : 50 éléments, de 1 à 50.

---

### Exercice 94 : Nombres pairs 1 à 50
**Objectif** : Créer une liste avec les nombres pairs de 1 à 50.

```python
# Solution
pairs_1_50 = []
for i in range(2, 51, 2):  # Départ 2, pas 2
    pairs_1_50.append(i)

print(f"Nombres pairs de 1 à 50 : {pairs_1_50}")

# Alternative : test de parité
pairs_alt = [i for i in range(1, 51) if i % 2 == 0]
print(f"Même résultat : {len(pairs_alt)} éléments")
```

**Explication** :
- **Range optimisé** : range(2, 51, 2)
- **Efficacité** : génération directe des pairs
- **Alternative** : filtrage après génération

**Test** : 2, 4, 6, ..., 50 (25 éléments).

---

### Exercice 95 : Nombres impairs 1 à 50
**Objectif** : Créer une liste avec les nombres impairs de 1 à 49.

```python
# Solution
impairs_1_50 = []
for i in range(1, 50, 2):  # Départ 1, pas 2
    impairs_1_50.append(i)

print(f"Nombres impairs de 1 à 49 : {impairs_1_50}")

# Alternative : test de parité
impairs_alt = [i for i in range(1, 50) if i % 2 != 0]
print(f"Même résultat : {len(impairs_alt)} éléments")
```

**Explication** :
- **Range impair** : range(1, 50, 2)
- **Pattern** : impairs = 2n+1
- **Complément** : tout ce qui n'est pas pair

**Test** : 1, 3, 5, ..., 49 (25 éléments).

---

### Exercice 96 : Éléments sauf premier et dernier
**Objectif** : Afficher tous les éléments d'une liste sauf le premier et le dernier.

```python
# Solution
nombres = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
print(f"Liste complète : {nombres}")
print("Éléments sauf premier et dernier :")

for i in range(1, len(nombres) - 1):
    print(nombres[i], end=" ")
print()

# Alternative avec slicing
print(f"Même résultat avec slicing : {nombres[1:-1]}")
```

**Explication** :
- **Range ajusté** : range(1, len-1)
- **Exclusion des bornes** : premier (index 0) et dernier (index -1)
- **Slicing** : [1:-1] plus concis

**Test** : [10, 20, 30, 40, 50, 60, 70, 80, 90, 100] → 20, 30, 40, 50, 60, 70, 80, 90.

---

### Exercice 97 : Éléments communs
**Objectif** : Vérifier si deux listes ont des éléments communs.

```python
# Solution
liste1 = [1, 2, 3, 4, 5]
liste2 = [4, 5, 6, 7, 8]

communs = False
for element in liste1:
    if element in liste2:
        communs = True
        print(f"Élément commun trouvé : {element}")
        break

if not communs:
    print("Aucun élément commun")
```

**Explication** :
- **Double itération** : test de chaque élément de liste1 dans liste2
- **Court-circuit** : break dès le premier trouvé
- **Booléen** : suivi de l'état de recherche

**Test** : 4 et 5 sont communs.

---

### Exercice 98 : Doublage avec compréhension
**Objectif** : Créer une liste avec les éléments d'une autre liste multipliés par 2.

```python
# Solution
nombres = [1, 2, 3, 4, 5]

# Avec compréhension (recommandé)
doubles = [nombre * 2 for nombre in nombres]

# Avec boucle classique
doubles_alt = []
for nombre in nombres:
    doubles_alt.append(nombre * 2)

print(f"Originaux : {nombres}")
print(f"Doubles (compréhension) : {doubles}")
print(f"Doubles (boucle) : {doubles_alt}")
print(f"Résultats identiques : {doubles == doubles_alt}")
```

**Explication** :
- **Compréhension** : syntaxe concise et lisible
- **Équivalence** : même résultat que la boucle
- **Performance** : compréhension souvent plus efficace

**Test** : [1, 2, 3, 4, 5] → [2, 4, 6, 8, 10].

---

### Exercice 99 : Multiples de 7
**Objectif** : Afficher tous les multiples de 7 de 7 à 70.

```python
# Solution
print("Multiples de 7 de 7 à 70 :")

# Avec compréhension
multiples_7 = [i for i in range(7, 71) if i % 7 == 0]
print(f"Compréhension : {multiples_7}")

# Avec boucle
print("Boucle :")
for i in range(7, 71):
    if i % 7 == 0:
        print(i, end=" ")
print()
```

**Explication** :
- **Range 7 à 70** : range(7, 71)
- **Test de divisibilité** : i % 7 == 0
- **Multiples** : 7×1, 7×2, ..., 7×10

**Test** : 7, 14, 21, ..., 70 (10 nombres).

---

### Exercice 100 : Synthèse complète
**Objectif** : Application finale combinant tous les concepts de la Partie 2.

```python
# Solution - Analyseur de nombres complet
def analyseur_nombres(nombres):
    """Analyse complète d'une liste de nombres"""
    if not nombres:
        return "Liste vide"

    analyse = {}

    # Statistiques de base
    analyse["total"] = len(nombres)
    analyse["somme"] = sum(nombres)
    analyse["moyenne"] = analyse["somme"] / analyse["total"]
    analyse["maximum"] = max(nombres)
    analyse["minimum"] = min(nombres)

    # Filtres conditionnels
    analyse["pairs"] = [x for x in nombres if x % 2 == 0]
    analyse["impairs"] = [x for x in nombres if x % 2 != 0]
    analyse["positifs"] = [x for x in nombres if x > 0]
    analyse["negatifs"] = [x for x in nombres if x < 0]
    analyse["superieurs_moyenne"] = [x for x in nombres if x > analyse["moyenne"]]

    # Transformations
    analyse["carres"] = [x**2 for x in nombres]
    analyse["doubles"] = [x*2 for x in nombres]

    # Tests de divisibilité
    for diviseur in [3, 5, 7]:
        analyse[f"multiples_{diviseur}"] = [x for x in nombres if x % diviseur == 0]

    return analyse

# Test avec une liste variée
test_nombres = [15, -3, 8, 0, 12, -7, 25, 4, 9, 18]
resultats = analyseur_nombres(test_nombres)

print("=== ANALYSE COMPLÈTE ===")
for section, contenu in resultats.items():
    if isinstance(contenu, list):
        print(f"{section}: {contenu}")
    else:
        print(f"{section}: {contenu}")

print(f"\nVérifications :")
print(f"Pairs + impairs = {len(resultats['pairs']) + len(resultats['impairs'])} (total: {len(test_nombres)})")
print(f"Carrés vérifiés : {all(x**2 in resultats['carres'] for x in test_nombres)}")
```

**Explication** :
- **Fonction complète** : analyse multi-facettes
- **Compréhensions multiples** : filtrage et transformation
- **Statistiques** : calculs automatiques
- **Tests de divisibilité** : multiples conditions
- **Validation** : vérifications croisées

**Test** : Analyse complète d'une liste avec nombres positifs, négatifs, pairs, impairs, multiples.

---

## 🔍 Points Clés à Retenir

### 1. **Compréhensions Avancées**
```python
# Filtrage multiple
grands_pairs = [x for x in nombres if x > 10 and x % 2 == 0]

# Transformation conditionnelle
absolus = [abs(x) for x in nombres]

# Filtres complexes
dans_plage = [x for x in nombres if 10 <= x <= 50]

# Exclusion
sauf_multiples_3 = [x for x in nombres if x % 3 != 0]
```

### 2. **Tests Conditionnels**
```python
# Tests d'appartenance
if element in liste:
    print("Présent")

# Tests de plage
if min_valeur <= nombre <= max_valeur:
    print("Dans la plage")

# Tests multiples
if nombre > 0 and nombre % 2 == 0 and nombre < 100:
    print("Nombre pair positif < 100")
```

### 3. **Génération de Séquences**
```python
# Séquences arithmétiques
pairs = list(range(0, 101, 2))        # 0, 2, 4, ..., 100
impairs = list(range(1, 100, 2))      # 1, 3, 5, ..., 99
multiples_7 = list(range(7, 71, 7))   # 7, 14, 21, ..., 70

# Séquences géométriques (approximation)
puissances_2 = [2**i for i in range(10)]  # 1, 2, 4, 8, 16, ...
```

### 4. **Validations Complexes**
```python
# Validation d'email basique
def email_valide(email):
    return "@" in email and "." in email and len(email) > 5

# Validation de mot de passe
def mot_de_passe_valide(mdp):
    return (len(mdp) >= 8 and
            any(c.isupper() for c in mdp) and
            any(c.islower() for c in mdp) and
            any(c.isdigit() for c in mdp))
```

## 💡 Optimisations et Astuces

### 1. **Fonctions Built-in vs Compréhensions**
```python
# Lent (boucle manuelle)
somme = 0
for x in nombres:
    if x > 10:
        somme += x

# Rapide (built-in + compréhension)
somme = sum(x for x in nombres if x > 10)

# Ultra rapide (built-in seulement si possible)
somme = sum(x for x in nombres if x > 10)
```

### 2. **Génération Efficace**
```python
# Au lieu de :
grands_pairs = []
for x in range(1000):
    if x > 500 and x % 2 == 0:
        grands_pairs.append(x)

# Utiliser :
grands_pairs = [x for x in range(502, 1000, 2)]  # Plus efficace
```

### 3. **Filtres en Cascade**
```python
# Filtre simple
pairs_positifs = [x for x in nombres if x > 0 and x % 2 == 0]

# Filtres multiples avec intersection
divisibles_3_et_5 = [x for x in nombres if x % 3 == 0 and x % 5 == 0]

# Exclusion
non_multiples_3 = [x for x in nombres if x % 3 != 0]
```

## 🚀 Applications Pratiques

### 1. **Filtrage de Données**
```python
def filtrer_etudiants(etudiants, criteres):
    """Filtre les étudiants selon plusieurs critères"""
    filtres = {
        "note_min": [e for e in etudiants if e["note"] >= criteres.get("note_min", 0)],
        "age_max": [e for e in etudiants if e["age"] <= criteres.get("age_max", 150)],
        "sexe": [e for e in etudiants if e["sexe"] == criteres.get("sexe")],
        "mention": [e for e in etudiants if e["mention"] in criteres.get("mentions", ["A", "B", "C", "D", "F"])]
    }

    # Intersection des filtres
    if filtres["note_min"]:
        resultat = filtres["note_min"]
        for filtre in filtres.values():
            if filtre != filtres["note_min"]:
                resultat = [e for e in resultat if e in filtre]
        return resultat

    return etudiants

# Exemple d'usage
etudiants = [
    {"nom": "Alice", "note": 15, "age": 20, "sexe": "F", "mention": "B"},
    {"nom": "Bob", "note": 12, "age": 22, "sexe": "M", "mention": "C"},
    {"nom": "Charlie", "note": 18, "age": 19, "sexe": "M", "mention": "A"}
]

resultat = filtrer_etudiants(etudiants, {"note_min": 14, "age_max": 21})
for etudiant in resultat:
    print(f"{etudiant['nom']}: {etudiant['note']}/20")
```

### 2. **Analyse Statistique**
```python
def analyse_statistique(nombres):
    """Analyse statistique complète"""
    if not nombres:
        return None

    # Statistiques de base
    stats = {
        "n": len(nombres),
        "somme": sum(nombres),
        "moyenne": sum(nombres) / len(nombres),
        "mediane": sorted(nombres)[len(nombres)//2],
        "mode": max(set(nombres), key=nombres.count) if nombres else None
    }

    # Filtres
    stats["pairs"] = [x for x in nombres if x % 2 == 0]
    stats["impairs"] = [x for x in nombres if x % 2 != 0]
    stats["positifs"] = [x for x in nombres if x > 0]
    stats["negatifs"] = [x for x in nombres if x < 0]
    stats["zeros"] = [x for x in nombres if x == 0]

    # Transformations
    stats["carres"] = [x**2 for x in nombres]
    stats["absolus"] = [abs(x) for x in nombres]

    # Tests de divisibilité
    for div in [2, 3, 5, 7, 11]:
        stats[f"div_{div}"] = [x for x in nombres if x % div == 0]

    return stats

# Test
donnees = [1, 2, 3, 2, 4, 2, 5, 2, 3, 1]
stats = analyse_statistique(donnees)
for cle, valeur in stats.items():
    print(f"{cle}: {valeur}")
```

### 3. **Génération de Séquences Spécialisées**
```python
def generer_sequences(n):
    """Génère diverses séquences numériques"""
    sequences = {}

    # Séquences de base
    sequences["naturels"] = list(range(1, n+1))
    sequences["pairs"] = list(range(2, n+1, 2))
    sequences["impairs"] = list(range(1, n+1, 2))

    # Carrés et cubes
    sequences["carres"] = [x**2 for x in range(1, n+1)]
    sequences["cubes"] = [x**3 for x in range(1, n+1)]

    # Nombres premiers (simplifié)
    sequences["premiers"] = [x for x in range(2, n+1) if all(x % i != 0 for i in range(2, int(x**0.5)+1))]

    # Factoriels
    sequences["fact"] = [1]
    for i in range(2, min(n+1, 10)):  # Limite pour éviter débordement
        sequences["fact"].append(sequences["fact"][-1] * i)

    return sequences

# Test
seq = generer_sequences(20)
for nom, valeurs in seq.items():
    print(f"{nom}: {valeurs}")
```

## 🎯 Bilan de la Partie 2

### Concepts Maîtrisés
✅ **Conditions** : if/elif/else, opérateurs logiques
✅ **Boucles** : for, while, range()
✅ **Manipulation de listes** : indexation, slicing, modification
✅ **Transformations** : carrés, cubes, tri, fusion
✅ **Compréhensions** : syntaxe avancée et concise
✅ **Tests et validations** : appartenance, filtres, intersections

### Compétences Développées
- **Logique algorithmique** : conditions et boucles complexes
- **Traitement de données** : filtrage, transformation, analyse
- **Optimisation** : compréhensions vs boucles
- **Validation** : tests multiples et conditions combinées
- **Génération** : création de séquences spécifiques

---

**🏁 FIN DE LA PARTIE 2 - BRAVO !**

**Exercices complétés : 100/100** 🎯

*Félicitations ! Vous avez terminé le contrôle de flux. Continuez avec la [Partie 3](Partie%203%20-%20Fonctions/3-1-fonctions-base.md) pour explorer les fonctions !*