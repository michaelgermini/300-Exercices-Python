# Partie 1.3 : Entrée/Sortie Utilisateur

## 🎯 Objectifs Pédagogiques

Ce chapitre explore l'**interaction avec l'utilisateur** et les **opérations sur les chaînes de caractères**. Ces concepts sont essentiels pour créer des programmes interactifs et manipuler du texte.

### Concepts Abordés
- **Saisie utilisateur** : `input()` avec conversions
- **Formatage de sortie** : `print()` avec divers arguments
- **Chaînes de caractères** : manipulation de base
- **Applications concrètes** : calculs personnels, conversions

---

## 📝 Exercices Pratiques

### Exercice 21 : Année de naissance
**Objectif** : Demander l'âge et calculer l'année de naissance.

```python
# Solution
from datetime import datetime

age = int(input("Quel est votre âge ? "))
annee_actuelle = datetime.now().year
annee_naissance = annee_actuelle - age
print(f"Vous êtes né(e) en {annee_naissance}")
```

**Explication** :
- `datetime.now().year` : obtient l'année actuelle
- **Soustraction** : calcul de l'année de naissance
- **Formatage** : f-string pour une sortie lisible

**Test** : Si vous avez 25 ans en 2024, vous êtes né en 1999.

---

### Exercice 22 : Calcul de l'IMC
**Objectif** : Calculer l'Indice de Masse Corporelle.

```python
# Solution
poids = float(input("Votre poids en kg : "))
taille = float(input("Votre taille en m : "))
imc = poids / (taille ** 2)
print(f"Votre IMC est : {imc:.2f}")

# Interprétation
if imc < 18.5:
    print("Insuffisance pondérale")
elif imc < 25:
    print("Poids normal")
elif imc < 30:
    print("Surpoids")
else:
    print("Obésité")
```

**Explication** :
- **Formule IMC** : poids / taille²
- `:.2f` : formatage à 2 décimales
- **Interprétation** : classification selon l'OMS

**Test** : 70kg, 1.75m → IMC = 22.86 (poids normal).

---

### Exercice 23 : Conversion devise (Dollars/Euros)
**Objectif** : Convertir des dollars en euros.

```python
# Solution
dollars = float(input("Montant en dollars : "))
taux_change = 0.85  # 1$ = 0.85€
euros = dollars * taux_change
print(f"{dollars}$.00 = {euros:.2f}€")
```

**Explication** :
- **Taux de change** : variable pour faciliter les modifications
- **Formatage** : affichage avec 2 décimales
- **Séparateur de milliers** : $.00 pour le style monétaire

**Test** : 100$ = 85.00€ (selon le taux actuel).

---

### Exercice 24 : Distance parcourue
**Objectif** : Calculer la distance = vitesse × temps.

```python
# Solution
vitesse = float(input("Vitesse (km/h) : "))
temps = float(input("Temps (heures) : "))
distance = vitesse * temps
print(f"Distance parcourue : {distance} km")
```

**Explication** :
- **Formule physique** : distance = vitesse × temps
- **Unités cohérentes** : km/h × h = km
- **Application** : calcul de trajets

**Test** : 60 km/h pendant 2.5h = 150 km.

---

### Exercice 25 : Reste de division
**Objectif** : Afficher le reste de la division de deux nombres.

```python
# Solution
dividende = int(input("Dividende : "))
diviseur = int(input("Diviseur : "))
quotient = dividende // diviseur
reste = dividende % diviseur
print(f"{dividende} = {diviseur} × {quotient} + {reste}")
```

**Explication** :
- `//` : division entière (quotient)
- `%` : modulo (reste)
- **Relation** : dividende = diviseur × quotient + reste

**Test** : 17 ÷ 5 = 3 × 5 + 2.

---

### Exercice 26 : Divisibilité par 3 et 5
**Objectif** : Vérifier si un nombre est divisible par 3 et par 5.

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
- `and` : opérateur logique ET
- **Tests multiples** : conditions spécifiques dans l'ordre
- **Priorité** : conditions les plus spécifiques en premier

**Test** : 15 (divisible par 3 et 5), 9 (par 3), 10 (par 5), 7 (ni l'un ni l'autre).

---

### Exercice 27 : Divisibilité par 7
**Objectif** : Version simplifiée pour la divisibilité par 7.

```python
# Solution
nombre = int(input("Entrez un nombre : "))
if nombre % 7 == 0:
    print(f"{nombre} est divisible par 7")
    quotient = nombre // 7
    print(f"Quotient : {quotient}")
else:
    print(f"{nombre} n'est pas divisible par 7")
    reste = nombre % 7
    print(f"Reste : {reste}")
```

**Explication** :
- **Affichage conditionnel** : informations selon le résultat
- **Complément d'information** : quotient ou reste selon le cas
- **UX** : feedback plus riche pour l'utilisateur

**Test** : 21 (divisible, quotient = 3), 22 (non divisible, reste = 1).

---

### Exercice 28 : Table de multiplication
**Objectif** : Afficher la table de multiplication d'un nombre.

```python
# Solution
nombre = int(input("Table de multiplication de : "))
print(f"Table de {nombre} :")
for i in range(1, 11):
    resultat = nombre * i
    print(f"{nombre} × {i} = {resultat}")
```

**Explication** :
- **Boucle 1 à 10** : `range(1, 11)`
- **Formatage** : alignement pour la lisibilité
- **Application** : outil pédagogique classique

**Test** : Table de 7 : 7×1=7, 7×2=14, ..., 7×10=70.

---

### Exercice 29 : Table de multiplication complète
**Objectif** : Afficher les tables de 1 à 10.

```python
# Solution
print("Tables de multiplication :")
for i in range(1, 11):
    print(f"\nTable de {i} :")
    for j in range(1, 11):
        resultat = i * j
        print(f"{i} × {j} = {resultat}")
    print("-" * 20)
```

**Explication** :
- **Double boucle** : table externe (1-10), interne (1-10)
- **Séparation visuelle** : lignes de séparation
- **Formatage** : organisation claire des résultats

**Test** : Affiche toutes les tables de 1×1=1 à 10×10=100.

---

### Exercice 30 : Test de multiplicité
**Objectif** : Vérifier si un nombre est multiple d'un autre.

```python
# Solution
nombre = int(input("Nombre : "))
multiple = int(input("Multiple de : "))
if nombre % multiple == 0:
    quotient = nombre // multiple
    print(f"{nombre} est multiple de {multiple}")
    print(f"Quotient : {quotient}")
else:
    print(f"{nombre} n'est pas multiple de {multiple}")
```

**Explication** :
- **Logique** : multiple si reste de division = 0
- **Généralisation** : remplace les tests spécifiques (×3, ×5, ×7)
- **Information** : affichage du quotient

**Test** : 24 et 6 (multiple, quotient = 4), 25 et 7 (non multiple).

---

## 🔍 Points Clés à Retenir

### 1. **Interaction Utilisateur**
- `input(message)` : saisie avec message
- **Conversions** : `int()`, `float()` pour transformer la saisie
- **Validation** : toujours convertir la saisie utilisateur

### 2. **Formatage de Sortie**
- **f-strings** : `f"{variable:.2f}"` pour le formatage
- **Multiple arguments** : `print(a, b, c)` avec espaces automatiques
- **Formatage numérique** : `:.2f` (2 décimales), `:d` (entier)

### 3. **Opérateurs Logiques**
- `and` : ET logique (toutes les conditions vraies)
- `or` : OU logique (au moins une condition vraie)
- `not` : négation logique

### 4. **Structures Conditionnelles**
- **Tests multiples** : `if/elif/elif/else`
- **Ordre** : conditions spécifiques avant générales
- **Imbrication** : conditions dans d'autres conditions

## 💡 Applications Courantes

### 1. **Calcul d'Intérêts Composés**
```python
capital = float(input("Capital initial : "))
taux = float(input("Taux (%) : ")) / 100
annees = int(input("Nombre d'années : "))
montant_final = capital * (1 + taux) ** annees
print(f"Montant final : {montant_final:.2f}€")
```

### 2. **Conversion de Température**
```python
# Fonction utilitaire
def celsius_to_fahrenheit(c):
    return (c * 9/5) + 32

celsius = float(input("Température (°C) : "))
fahrenheit = celsius_to_fahrenheit(celsius)
print(f"{celsius}°C = {fahrenheit}°F")
```

### 3. **Calcul de Pourcentage**
```python
total = float(input("Total : "))
pourcentage = float(input("Pourcentage : "))
valeur = (total * pourcentage) / 100
print(f"{pourcentage}% de {total} = {valeur}")
```

## 🎯 Défis Supplémentaires

1. **Créez** un programme de calcul de TVA (20%)
2. **Développez** un convertisseur de devises multiples
3. **Implémentez** un calculateur d'âge en jours
4. **Concevez** un programme de calcul de moyenne pondérée

---

**Exercices complétés : 30/50** 🎯

*Continuez avec le [chapitre suivant](1-4-chaines.md) pour explorer les manipulations de chaînes !*