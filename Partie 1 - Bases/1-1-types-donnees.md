# Partie 1.1 : Types de Données et Opérations

## 🎯 Objectifs Pédagogiques

Dans ce chapitre, nous allons explorer les **types de données fondamentaux** de Python et les **opérations de base**. Ces concepts sont essentiels car ils constituent le socle de toute programmation Python.

### Types de Données Abordés
- **int** : Nombres entiers (1, 42, -17)
- **float** : Nombres décimaux (3.14, -0.5, 2.0)
- **str** : Chaînes de caractères ("Hello", "Python")
- **bool** : Valeurs booléennes (True, False)

---

## 📝 Exercices Pratiques

### Exercice 1 : Hello World
**Objectif** : Afficher un message simple à l'écran.

```python
# Solution
print("Hello World")
```

**Explication** :
- `print()` est une fonction Python qui affiche du texte
- Les guillemets `"Hello World"` définissent une chaîne de caractères
- Le point-virgule final est optionnel en Python

**Test** : Exécutez le code et observez le résultat.

---

### Exercice 2 : Prénom de l'utilisateur
**Objectif** : Demander le prénom de l'utilisateur et l'afficher.

```python
# Solution
prenom = input("Quel est votre prénom ? ")
print("Bonjour,", prenom, "!")
```

**Explication** :
- `input()` demande une saisie à l'utilisateur
- Le texte entre guillemets est le message affiché
- La valeur saisie est stockée dans la variable `prenom`
- `print()` peut afficher plusieurs éléments séparés par des virgules

**Test** : Saisissez votre prénom et validez.

---

### Exercice 3 : Conversion Celsius en Fahrenheit
**Objectif** : Convertir une température de Celsius en Fahrenheit.

```python
# Solution
celsius = float(input("Température en Celsius : "))
fahrenheit = (celsius * 9/5) + 32
print(celsius, "°C =", fahrenheit, "°F")
```

**Explication** :
- `float()` convertit la saisie en nombre décimal
- La formule de conversion : F = (C × 9/5) + 32
- L'ordre des opérations est respecté (multiplication avant addition)

**Test** : Essayez avec 0°C (32°F) et 100°C (212°F).

---

### Exercice 4 : Somme de deux nombres
**Objectif** : Calculer la somme de deux nombres saisis par l'utilisateur.

```python
# Solution
nombre1 = float(input("Premier nombre : "))
nombre2 = float(input("Deuxième nombre : "))
somme = nombre1 + nombre2
print("La somme est :", somme)
```

**Explication** :
- Conversion en `float` pour accepter les nombres décimaux
- L'opérateur `+` additionne les valeurs
- Le résultat est stocké dans la variable `somme`

**Test** : Vérifiez avec 5 + 3 = 8 et 2.5 + 1.7 = 4.2.

---

### Exercice 5 : Nombre pair ou impair
**Objectif** : Vérifier si un nombre est pair ou impair.

```python
# Solution
nombre = int(input("Entrez un nombre entier : "))
if nombre % 2 == 0:
    print(nombre, "est pair")
else:
    print(nombre, "est impair")
```

**Explication** :
- `int()` convertit en nombre entier
- L'opérateur `%` donne le reste de la division
- `if/else` : condition pour tester la parité
- Un nombre est pair si le reste de sa division par 2 est 0

**Test** : Essayez avec 4 (pair), 7 (impair) et 0 (pair).

---

### Exercice 6 : Vérifier si un nombre est impair
**Objectif** : Version alternative avec négation logique.

```python
# Solution alternative
nombre = int(input("Entrez un nombre : "))
if nombre % 2 != 0:
    print(nombre, "est impair")
else:
    print(nombre, "est pair")
```

**Explication** :
- `!=` signifie "différent de"
- Cette version inverse la logique
- Les deux approches sont équivalentes

**Test** : Comparez les résultats avec l'exercice 5.

---

### Exercice 7 : Addition de trois nombres
**Objectif** : Calculer la somme de trois nombres.

```python
# Solution
a = float(input("Premier nombre : "))
b = float(input("Deuxième nombre : "))
c = float(input("Troisième nombre : "))
total = a + b + c
print("La somme est :", total)
```

**Explication** :
- Addition successive de trois valeurs
- Python évalue les expressions de gauche à droite
- Parenthèses inutiles car `+` est associatif à gauche

**Test** : Vérifiez avec 1 + 2 + 3 = 6.

---

### Exercice 8 : Calcul de moyenne
**Objectif** : Calculer la moyenne de plusieurs nombres.

```python
# Solution
note1 = float(input("Note 1 : "))
note2 = float(input("Note 2 : "))
note3 = float(input("Note 3 : "))
moyenne = (note1 + note2 + note3) / 3
print("Moyenne :", moyenne)
```

**Explication** :
- Division par 3 pour calculer la moyenne arithmétique
- L'ordre des opérations : parenthèses d'abord, puis division
- Le résultat est automatiquement un float si l'un des opérandes l'est

**Test** : Vérifiez avec 15, 18, 12 (moyenne = 15.0).

---

### Exercice 9 : Arrondi d'un nombre flottant
**Objectif** : Arrondir un nombre décimal à l'entier le plus proche.

```python
# Solution
nombre = float(input("Nombre décimal : "))
arrondi = round(nombre)
print(nombre, "arrondi =", arrondi)
```

**Explication** :
- `round()` arrondit à l'entier le plus proche
- Arrondi à l'inférieur pour .4 et inférieur
- Arrondi au supérieur pour .5 et supérieur

**Test** : Essayez 3.7 → 4, 3.2 → 3, 4.5 → 4 (en Python 3).

---

### Exercice 10 : Comparaison de deux nombres
**Objectif** : Comparer deux nombres et afficher le plus grand.

```python
# Solution
a = float(input("Premier nombre : "))
b = float(input("Deuxième nombre : "))
if a > b:
    print(a, "est plus grand que", b)
elif a < b:
    print(a, "est plus petit que", b)
else:
    print(a, "est égal à", b)
```

**Explication** :
- `if/elif/else` : structure de décision complète
- `>` : strictement plus grand
- `<` : strictement plus petit
- `elif` : sinon si (exécuté seulement si la condition précédente est fausse)

**Test** : Comparez 5 et 3, 2 et 8, 4 et 4.

---

### Exercice 11 : Carré d'un nombre
**Objectif** : Afficher le carré d'un nombre.

```python
# Solution
nombre = float(input("Nombre : "))
carre = nombre ** 2
print("Le carré de", nombre, "est", carre)
```

**Explication** :
- `**` : opérateur de puissance (exponentiation)
- `nombre ** 2` : nombre au carré
- `nombre ** 0.5` : racine carrée (alternative à `math.sqrt()`)

**Test** : Vérifiez 4² = 16, (-3)² = 9, 2.5² = 6.25.

---

### Exercice 12 : Cube d'un nombre
**Objectif** : Afficher le cube d'un nombre.

```python
# Solution
nombre = float(input("Nombre : "))
cube = nombre ** 3
print("Le cube de", nombre, "est", cube)
```

**Explication** :
- `** 3` : élévation à la puissance 3
- Fonctionne avec tous les types numériques
- Respecte les règles de signe : (-2)³ = -8

**Test** : Vérifiez 2³ = 8, 1.5³ = 3.375, (-1)³ = -1.

---

## 🔍 Points Clés à Retenir

1. **Types de données** : Python est typé dynamiquement mais fortement typé
2. **Conversion** : `int()`, `float()`, `str()`, `bool()` pour les conversions
3. **Opérateurs arithmétiques** : `+`, `-`, `*`, `/`, `%`, `**`, `//`
4. **Comparaison** : `==`, `!=`, `>`, `<`, `>=`, `<=`
5. **Structure conditionnelle** : `if/elif/else` pour les décisions
6. **Saisie utilisateur** : `input()` pour l'interaction
7. **Affichage** : `print()` pour la sortie

## 💡 Erreurs Courantes à Éviter

- **Saisie non convertie** : Toujours convertir `input()` avec `int()` ou `float()`
- **Division par zéro** : Python lève une `ZeroDivisionError`
- **Comparaison d'égalité** : Utiliser `==` (pas `=`)
- **Indentation** : Python utilise l'indentation pour délimiter les blocs
- **Guillemets** : Mélanger guillemets simples et doubles peut causer des erreurs

## 🚀 Prochaines Étapes

Dans le prochain chapitre, nous explorerons les **opérations mathématiques avancées** et les **boucles** pour automatiser les calculs répétitifs.

---

**Exercices complétés : 12/50** 🎯

*Continuez avec le [chapitre suivant](1-2-operations-math.md) pour approfondir les opérations mathématiques !*
