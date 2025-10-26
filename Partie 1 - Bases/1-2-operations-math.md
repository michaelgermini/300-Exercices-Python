# Partie 1.2 : Opérations Mathématiques

## 🎯 Objectifs Pédagogiques

Ce chapitre approfondit les **opérations mathématiques** en Python. Nous allons explorer les conversions d'unités, les calculs arithmétiques avancés et les applications pratiques du quotidien.

### Concepts Abordés
- **Conversions d'unités** : km/miles, Celsius/Fahrenheit, minutes/heures
- **Opérateurs arithmétiques** : multiplication, division, modulo, puissance
- **Applications concrètes** : temps, distance, vitesses, tables de multiplication
- **Logique conditionnelle** : tests de positivité, divisibilité

---

## 📝 Exercices Pratiques

### Exercice 13 : Conversion km en miles
**Objectif** : Convertir une distance en kilomètres vers les miles.

```python
# Solution
kilometres = float(input("Distance en km : "))
miles = kilometres * 0.621371
print(kilometres, "km =", round(miles, 2), "miles")
```

**Explication** :
- **Facteur de conversion** : 1 km = 0.621371 miles
- `round(miles, 2)` : arrondi à 2 décimales pour la lisibilité
- Les conversions d'unités sont des applications courantes

**Test** : 10 km = 6.21 miles, 42.195 km (marathon) = 26.22 miles.

---

### Exercice 14 : Conversion minutes en heures
**Objectif** : Convertir un nombre de minutes en heures et minutes.

```python
# Solution
minutes = int(input("Nombre de minutes : "))
heures = minutes // 60
minutes_restantes = minutes % 60
print(minutes, "minutes =", heures, "h", minutes_restantes, "min")
```

**Explication** :
- `//` : division entière (quotient)
- `%` : modulo (reste de la division)
- Application typique : conversion temps

**Test** : 90 min = 1h 30min, 125 min = 2h 5min.

---

### Exercice 15 : Test de positivité
**Objectif** : Vérifier si un nombre est positif, négatif ou nul.

```python
# Solution
nombre = float(input("Entrez un nombre : "))
if nombre > 0:
    print(nombre, "est positif")
elif nombre < 0:
    print(nombre, "est négatif")
else:
    print(nombre, "est nul")
```

**Explication** :
- **Structure complète** : if/elif/else pour tous les cas
- **Comparaison à zéro** : point de référence en mathématiques
- **Égalité** : else gère le cas d'égalité (nombre = 0)

**Test** : Essayez 5 (positif), -3 (négatif), 0 (nul).

---

### Exercice 16 : Affichage des 10 premiers nombres naturels
**Objectif** : Afficher les nombres de 1 à 10.

```python
# Solution avec boucle
for i in range(1, 11):
    print(i, end=" ")
print()  # Saut de ligne final
```

**Explication** :
- `range(1, 11)` : génère les nombres de 1 à 10
- `for i in range()` : boucle pour itérer
- `end=" "` : affiche les nombres sur la même ligne
- `print()` vide : force un saut de ligne

**Test** : Observez la séquence : 1 2 3 4 5 6 7 8 9 10.

---

### Exercice 17 : Nombres pairs de 2 à 20
**Objectif** : Afficher les 10 premiers nombres pairs.

```python
# Solution
print("Nombres pairs de 2 à 20 :")
for i in range(2, 21, 2):  # Départ 2, fin 21, pas 2
    print(i, end=" ")
print()
```

**Explication** :
- `range(2, 21, 2)` : départ à 2, fin avant 21, pas de 2
- **Pas de 2** : génère uniquement les nombres pairs
- **Efficacité** : méthode directe sans test de parité

**Test** : Résultat attendu : 2 4 6 8 10 12 14 16 18 20.

---

### Exercice 18 : Nombres impairs de 1 à 19
**Objectif** : Afficher les 10 premiers nombres impairs.

```python
# Solution
print("Nombres impairs de 1 à 19 :")
for i in range(1, 20, 2):  # Départ 1, fin 20, pas 2
    print(i, end=" ")
print()
```

**Explication** :
- `range(1, 20, 2)` : séquence des nombres impairs
- **Logique** : les impairs sont espacés de 2
- **Pattern** : 2n+1 = 1, 3, 5, 7, 9...

**Test** : Vérifiez : 1 3 5 7 9 11 13 15 17 19.

---

### Exercice 19 : Somme de 1 à 100
**Objectif** : Calculer la somme des nombres de 1 à 100 (formule de Gauss).

```python
# Solution mathématique (formule de Gauss)
n = 100
somme = n * (n + 1) // 2
print("Somme de 1 à", n, "=", somme)

# Alternative avec boucle (pour comparaison)
somme_boucle = 0
for i in range(1, 101):
    somme_boucle += i
print("Somme avec boucle =", somme_boucle)
```

**Explication** :
- **Formule de Gauss** : n(n+1)/2 pour la somme 1+2+...+n
- `//` : division entière (résultat exact)
- **Complexité** : O(1) vs O(n) - démonstration d'optimisation

**Test** : Gauss a résolu ce problème à 8 ans : 5050.

---

### Exercice 20 : Produit de 1 à 10
**Objectif** : Calculer le produit (factoriel de 10) des nombres de 1 à 10.

```python
# Solution
produit = 1
for i in range(1, 11):
    produit *= i  # produit = produit * i
print("Produit de 1 à 10 (10!) =", produit)
```

**Explication** :
- **Initialisation** : produit = 1 (élément neutre)
- `*= ` : multiplication et affectation
- **Résultat** : 10! = 3,628,800

**Test** : 1×2×3×4×5×6×7×8×9×10 = 3,628,800.

---

## 🔍 Points Clés à Retenir

### 1. **Conversions d'Unités**
- **Distance** : 1 km = 0.621371 miles
- **Température** : F = (C × 9/5) + 32
- **Temps** : 60 minutes = 1 heure

### 2. **Opérateurs Mathématiques**
- `//` : division entière (quotient)
- `%` : modulo (reste)
- `**` : puissance
- `*=`, `+=`, `-=`, `/=` : opérateurs composés

### 3. **Fonctions Built-in**
- `range(start, stop, step)` : générateur de séquences
- `round(nombre, decimales)` : arrondi
- `abs(nombre)` : valeur absolue (non utilisée ici)

### 4. **Boucles for**
- `for i in range(n)` : itération de 0 à n-1
- `for i in range(start, stop)` : itération de start à stop-1
- `for i in range(start, stop, step)` : itération avec pas

## 💡 Optimisations et Astuces

### Formule de Gauss (Somme 1 à n)
```python
# Efficace O(1)
somme = n * (n + 1) // 2

# Alternative O(n) - moins efficace
somme = sum(range(1, n+1))
```

### Génération de Nombres Pairs/Impairs
```python
# Nombres pairs : range(0, n+1, 2)
# Nombres impairs : range(1, n+1, 2)
# Carrés : [i**2 for i in range(1, n+1)]
```

## 🚀 Applications Pratiques

### 1. **Calcul de Distance**
```python
vitesse = 60  # km/h
temps = 2.5   # heures
distance = vitesse * temps
print(f"Distance parcourue : {distance} km")
```

### 2. **Calcul d'Intérêts**
```python
capital = 1000  # euros
taux = 0.05     # 5%
interets = capital * taux
print(f"Intérêts : {interets} euros")
```

### 3. **Conversion de Devises**
```python
euros = 100
taux_change = 1.18  # 1€ = 1.18$
dollars = euros * taux_change
print(f"{euros}€ = {dollars}$")
```

## 🎯 Défis Supplémentaires

1. **Calculez** la somme des nombres pairs de 1 à 100
2. **Trouvez** le produit des nombres impairs de 1 à 15
3. **Convertissez** 100°F en Celsius (formule inverse)
4. **Affichez** les multiples de 7 de 7 à 70

---

**Exercices complétés : 20/50** 🎯

*Continuez avec le [chapitre suivant](1-3-entree-sortie.md) pour explorer les interactions utilisateur !*