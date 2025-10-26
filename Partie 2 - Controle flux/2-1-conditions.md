# Partie 2.1 : Conditions if/elif/else

## 🎯 Objectifs Pédagogiques

Ce chapitre explore les **structures conditionnelles** en Python, essentielles pour la **prise de décision** dans les programmes. Les conditions permettent d'exécuter du code selon des critères spécifiques.

### Concepts Abordés
- **Structure if/elif/else** : tests et ramifications
- **Opérateurs de comparaison** : ==, !=, <, >, <=, >=
- **Opérateurs logiques** : and, or, not
- **Applications pratiques** : tests de valeurs, classifications

---

## 📝 Exercices Pratiques

### Exercice 51 : Test de positivité
**Objectif** : Déterminer si un nombre est positif, négatif ou nul.

```python
# Solution
nombre = float(input("Entrez un nombre : "))

if nombre > 0:
    print(f"{nombre} est positif")
elif nombre < 0:
    print(f"{nombre} est négatif")
else:
    print(f"{nombre} est nul")
```

**Explication** :
- **Structure complète** : if/elif/else pour tous les cas
- **Comparaison à zéro** : point de référence mathématique
- **Types numériques** : fonctionne avec int et float

**Test** : 5 (positif), -3 (négatif), 0 (nul), 0.5 (positif).

---

### Exercice 52 : Test de parité
**Objectif** : Vérifier si un nombre est pair ou impair.

```python
# Solution
nombre = int(input("Entrez un nombre entier : "))

if nombre % 2 == 0:
    print(f"{nombre} est pair")
else:
    print(f"{nombre} est impair")
```

**Explication** :
- **Modulo 2** : reste de la division par 2
- **Entier requis** : conversion en int pour éviter les erreurs
- **Logique binaire** : pair si divisible par 2

**Test** : 4 (pair), 7 (impair), 0 (pair), -2 (pair).

---

### Exercice 53 : Divisibilité par 3 ou 5
**Objectif** : Vérifier si un nombre est divisible par 3 ou par 5.

```python
# Solution
nombre = int(input("Entrez un nombre : "))

if nombre % 3 == 0 and nombre % 5 == 0:
    print(f"{nombre} est divisible par 3 et par 5")
elif nombre % 3 == 0:
    print(f"{nombre} est divisible par 3")
elif nombre % 5 == 0:
    print(f"{nombre} est divisible par 5")
else:
    print(f"{nombre} n'est divisible ni par 3 ni par 5")
```

**Explication** :
- **Priorité** : test du ET avant le OU
- **Ordre logique** : conditions spécifiques d'abord
- **Opérateur logique** : `and` pour les deux conditions

**Test** : 15 (par 3 et 5), 9 (par 3), 10 (par 5), 7 (ni l'un ni l'autre).

---

### Exercice 54 : Affichage 1 à 100
**Objectif** : Afficher les nombres de 1 à 100.

```python
# Solution
print("Nombres de 1 à 100 :")
for i in range(1, 101):
    print(i, end=" ")
print()  # Saut de ligne final
```

**Explication** :
- `range(1, 101)` : génère 1 à 100
- **Boucle for** : itération automatique
- `end=" "` : affichage horizontal

**Test** : 1 2 3 ... 99 100.

---

### Exercice 55 : Somme des nombres pairs jusqu'à 50
**Objectif** : Calculer la somme des nombres pairs de 2 à 50.

```python
# Solution
somme = 0
for i in range(2, 51, 2):  # Pairs uniquement
    somme += i
print(f"Somme des nombres pairs de 2 à 50 : {somme}")

# Alternative : test de parité
somme_alt = 0
for i in range(1, 51):
    if i % 2 == 0:
        somme_alt += i
print(f"Même résultat avec test : {somme_alt}")
```

**Explication** :
- **Optimisation** : range avec pas de 2
- **Alternative** : test de parité dans la boucle
- **Efficacité** : première version plus performante

**Test** : Résultat = 650 (vérification : 2+4+...+50).

---

### Exercice 56 : Somme des nombres impairs jusqu'à 50
**Objectif** : Calculer la somme des nombres impairs de 1 à 49.

```python
# Solution
somme = 0
for i in range(1, 50, 2):  # Impairs uniquement
    somme += i
print(f"Somme des nombres impairs de 1 à 49 : {somme}")
```

**Explication** :
- **Range impair** : range(1, 50, 2)
- **Pattern** : impairs = 2n+1
- **Série arithmétique** : somme calculable par formule

**Test** : 1+3+5+...+49 = 625.

---

### Exercice 57 : Plus grand de trois nombres
**Objectif** : Trouver le plus grand de trois nombres.

```python
# Solution
a = float(input("Premier nombre : "))
b = float(input("Deuxième nombre : "))
c = float(input("Troisième nombre : "))

if a >= b and a >= c:
    plus_grand = a
elif b >= a and b >= c:
    plus_grand = b
else:
    plus_grand = c

print(f"Le plus grand est : {plus_grand}")
```

**Explication** :
- **Comparaisons multiples** : test de chaque variable
- **Opérateur >=** : gère l'égalité
- **Logique** : exclusion successive des plus petits

**Test** : 5, 3, 8 → 8; 10, 10, 5 → 10; -1, -5, -3 → -1.

---

### Exercice 58 : Plus petit de trois nombres
**Objectif** : Trouver le plus petit de trois nombres.

```python
# Solution
a = float(input("Premier nombre : "))
b = float(input("Deuxième nombre : "))
c = float(input("Troisième nombre : "))

if a <= b and a <= c:
    plus_petit = a
elif b <= a and b <= c:
    plus_petit = b
else:
    plus_petit = c

print(f"Le plus petit est : {plus_petit}")
```

**Explication** :
- **Logique inverse** : <= au lieu de >=
- **Symétrie** : même structure que l'exercice précédent
- **Cas d'égalité** : géré par <=

**Test** : 5, 3, 8 → 3; 2, 2, 5 → 2; -1, -5, -3 → -5.

---

### Exercice 59 : Comparaison de deux nombres
**Objectif** : Comparer deux nombres et afficher le plus grand.

```python
# Solution
a = float(input("Premier nombre : "))
b = float(input("Deuxième nombre : "))

if a > b:
    print(f"{a} est plus grand que {b}")
elif a < b:
    print(f"{a} est plus petit que {b}")
else:
    print(f"{a} est égal à {b}")
```

**Explication** :
- **Structure if/elif/else** : tous les cas couverts
- **Comparaison complète** : plus grand, plus petit, égal
- **Formatage** : affichage des deux valeurs

**Test** : 5 et 3 (5 plus grand), 2 et 8 (2 plus petit), 4 et 4 (égaux).

---

### Exercice 60 : Plus petit de deux nombres
**Objectif** : Afficher le plus petit de deux nombres.

```python
# Solution
a = float(input("Premier nombre : "))
b = float(input("Deuxième nombre : "))

if a < b:
    print(f"{a} est le plus petit")
else:
    print(f"{b} est le plus petit")
```

**Explication** :
- **Simplification** : else gère les cas "plus petit ou égal"
- **Logique binaire** : seulement deux cas à considérer
- **Efficacité** : une seule comparaison

**Test** : 5 et 3 → 3; 2 et 8 → 2; 4 et 4 → 4.

---

## 🔍 Points Clés à Retenir

### 1. **Structure Conditionnelle**
```python
if condition1:
    # Code si condition1 vraie
elif condition2:
    # Code si condition1 fausse ET condition2 vraie
else:
    # Code si toutes les conditions précédentes fausses
```

### 2. **Opérateurs de Comparaison**
- `==` : égal à
- `!=` : différent de
- `<` : strictement plus petit
- `>` : strictement plus grand
- `<=` : plus petit ou égal
- `>=` : plus grand ou égal

### 3. **Opérateurs Logiques**
- `and` : ET (toutes les conditions vraies)
- `or` : OU (au moins une condition vraie)
- `not` : négation (inverse la condition)

### 4. **Priorité des Opérateurs**
1. **Arithmétiques** : *, /, %, //, +, -
2. **Comparaison** : ==, !=, <, >, <=, >=
3. **Logiques** : not, and, or

## 💡 Optimisations et Astuces

### 1. **Comparaison Multiple**
```python
# Au lieu de :
if a > b and a > c:
    max = a

# Utiliser max() built-in
maximum = max(a, b, c)
```

### 2. **Test d'Intervalle**
```python
# Test si nombre dans [min, max]
if min_valeur <= nombre <= max_valeur:
    print("Dans la plage")
```

### 3. **Conditions Complexes**
```python
# Âge adulte ET pays France
if age >= 18 and pays == "France":
    print("Majeur en France")

# Weekend OU jour férié
if jour == "samedi" or jour == "dimanche" or ferie:
    print("Repos")
```

## 🚀 Applications Pratiques

### 1. **Classification par Notes**
```python
note = float(input("Note (0-20) : "))
if note >= 16:
    mention = "Très bien"
elif note >= 14:
    mention = "Bien"
elif note >= 12:
    mention = "Assez bien"
elif note >= 10:
    mention = "Passable"
else:
    mention = "Insuffisant"
print(f"Mention : {mention}")
```

### 2. **Calcul de Tarifs**
```python
age = int(input("Âge : "))
if age < 12:
    tarif = 5  # Enfant
elif age < 18:
    tarif = 8  # Adolescent
elif age > 65:
    tarif = 7  # Senior
else:
    tarif = 10  # Adulte
print(f"Tarif : {tarif}€")
```

### 3. **Validation de Données**
```python
email = input("Email : ")
if "@" not in email or "." not in email:
    print("Email invalide")
else:
    print("Email valide")
```

## 🎯 Défis Supplémentaires

1. **Classez** un triangle selon ses angles (aigu, droit, obtus)
2. **Déterminez** si une année est bissextile
3. **Calculez** le signe du zodiaque selon la date
4. **Implémentez** un système de notation avec coefficients

---

**Exercices complétés : 60/100** 🎯

*Continuez avec le [chapitre suivant](2-2-boucles.md) pour approfondir les boucles !*