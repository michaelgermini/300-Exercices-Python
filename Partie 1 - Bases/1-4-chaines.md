# Partie 1.4 : Opérations sur Chaînes

## 🎯 Objectifs Pédagogiques

Ce chapitre explore les **manipulations de chaînes de caractères**, un aspect fondamental de Python. Les chaînes sont partout en programmation : saisie utilisateur, fichiers, interfaces web, etc.

### Concepts Abordés
- **Création et manipulation** : création, concaténation, répétition
- **Formatage** : majuscules, minuscules, capitalisation
- **Analyse** : longueur, recherche, extraction
- **Validation** : palindromes, sous-chaînes, caractères spéciaux

---

## 📝 Exercices Pratiques

### Exercice 31 : Chaîne en majuscules
**Objectif** : Convertir une chaîne en majuscules.

```python
# Solution
chaine = input("Entrez une chaîne : ")
majuscules = chaine.upper()
print("En majuscules :", majuscules)
```

**Explication** :
- `.upper()` : méthode de conversion en majuscules
- **Immutable** : la chaîne originale n'est pas modifiée
- **Retour** : nouvelle chaîne en résultat

**Test** : "hello" → "HELLO", "Python 3.9" → "PYTHON 3.9".

---

### Exercice 32 : Chaîne en minuscules
**Objectif** : Convertir une chaîne en minuscules.

```python
# Solution
chaine = input("Entrez une chaîne : ")
minuscules = chaine.lower()
print("En minuscules :", minuscules)
```

**Explication** :
- `.lower()` : conversion en minuscules
- **Utile pour** : comparaisons insensibles à la casse
- **Accents** : conservés (à ≠ à, mais À = à)

**Test** : "HELLO" → "hello", "PyThOn" → "python".

---

### Exercice 33 : Nombre de caractères
**Objectif** : Compter le nombre de caractères d'une chaîne.

```python
# Solution
chaine = input("Entrez une chaîne : ")
longueur = len(chaine)
print(f"La chaîne '{chaine}' contient {longueur} caractères")
```

**Explication** :
- `len()` : fonction built-in pour la longueur
- **Compte** : tous les caractères (lettres, espaces, ponctuation)
- **Indexation** : les indices vont de 0 à longueur-1

**Test** : "Python" → 6, "Hello World" → 11, "" → 0.

---

### Exercice 34 : Inverser une chaîne
**Objectif** : Inverser l'ordre des caractères d'une chaîne.

```python
# Solution
chaine = input("Entrez une chaîne : ")
inverse = chaine[::-1]
print(f"Chaîne originale : {chaine}")
print(f"Chaîne inversée : {inverse}")
```

**Explication** :
- **Slicing** : `[::-1]` technique d'inversion
- **Syntaxe** : `[début:fin:pas]` avec pas négatif
- **Alternative** : boucle for ou fonction `reversed()`

**Test** : "Python" → "nohtyP", "radar" → "radar".

---

### Exercice 35 : Test de palindrome
**Objectif** : Vérifier si une chaîne est un palindrome (se lit dans les deux sens).

```python
# Solution
chaine = input("Entrez une chaîne : ").lower()
# Supprimer les espaces et ponctuations
chaine_nettoyee = "".join(c for c in chaine if c.isalnum())
inverse = chaine_nettoyee[::-1]

if chaine_nettoyee == inverse:
    print(f"'{chaine}' est un palindrome")
else:
    print(f"'{chaine}' n'est pas un palindrome")
```

**Explication** :
- **Nettoyage** : suppression des caractères non alphanumériques
- `.isalnum()` : teste si le caractère est une lettre ou un chiffre
- **Comparaison** : originale vs inversée
- **Case insensitive** : conversion en minuscules

**Test** : "radar" (oui), "Python" (non), "A man a plan a canal Panama" (oui).

---

### Exercice 36 : Remplacement de caractères
**Objectif** : Remplacer des caractères dans une chaîne.

```python
# Solution
chaine = input("Entrez une chaîne : ")
ancien = input("Caractère à remplacer : ")
nouveau = input("Nouveau caractère : ")
chaine_modifiee = chaine.replace(ancien, nouveau)
print(f"Résultat : {chaine_modifiee}")
```

**Explication** :
- `.replace()` : méthode de remplacement
- **Tous les occurrences** : remplace toutes les instances
- **Spécifique** : remplacement exact caractère par caractère

**Test** : "hello" avec "l" → "o" = "heooo".

---

### Exercice 37 : Suppression des espaces
**Objectif** : Supprimer les espaces d'une chaîne.

```python
# Solution
chaine = input("Entrez une chaîne : ")
# Supprimer tous les espaces
chaine_sans_espaces = chaine.replace(" ", "")
print(f"Avec espaces : '{chaine}'")
print(f"Sans espaces : '{chaine_sans_espaces}'")
```

**Explication** :
- `.replace(" ", "")` : remplace les espaces par rien
- **Espaces multiples** : tous supprimés
- **Autres espaces** : \t, \n nécessiteraient `.strip()`

**Test** : "Hello World" → "HelloWorld", "  Python  " → "Python".

---

### Exercice 38 : Concaténation de chaînes
**Objectif** : Concaténer (assembler) deux chaînes.

```python
# Solution
chaine1 = input("Première chaîne : ")
chaine2 = input("Deuxième chaîne : ")
concatenation = chaine1 + chaine2
print(f"Concaténation : {concatenation}")
```

**Explication** :
- `+` : opérateur de concaténation pour les chaînes
- **Efficacité** : les chaînes sont immutables, nouvelle chaîne créée
- **Alternative** : f-strings pour le formatage

**Test** : "Hello" + "World" = "HelloWorld".

---

### Exercice 39 : Répétition de chaîne
**Objectif** : Répéter une chaîne plusieurs fois.

```python
# Solution
chaine = input("Chaîne à répéter : ")
nombre = int(input("Nombre de répétitions : "))
repetition = chaine * nombre
print(f"Répétition : {repetition}")
```

**Explanation** :
- `*` : opérateur de répétition pour les chaînes
- **Nombre entier** : positif uniquement
- **Performance** : efficace pour les petites répétitions

**Test** : "Hi" × 3 = "HiHiHi".

---

### Exercice 40 : Extraction de sous-chaîne
**Objectif** : Extraire une partie d'une chaîne.

```python
# Solution
chaine = input("Entrez une chaîne : ")
debut = int(input("Index de début : "))
fin = int(input("Index de fin : "))
sous_chaine = chaine[debut:fin]
print(f"Chaîne originale : {chaine}")
print(f"Sous-chaîne [{debut}:{fin}] : {sous_chaine}")
```

**Explication** :
- **Slicing** : `[début:fin]` extraction par indices
- **Indices** : début inclus, fin exclus
- **Bornes** : attention aux erreurs d'index

**Test** : "Python"[0:3] = "Pyt", "Hello"[1:4] = "ell".

---

## 🔍 Points Clés à Retenir

### 1. **Immutabilité des Chaînes**
```python
chaine = "Hello"
# chaine[0] = "h"  # ERREUR ! Chaînes immutables
chaine = "hello"   # OK, nouvelle référence
```

### 2. **Indexation et Slicing**
```python
chaine = "Python"
# Indices :    P y t h o n
# Positions :  0 1 2 3 4 5

# Indexation : chaine[0] → "P", chaine[-1] → "n"
# Slicing : chaine[1:4] → "yth", chaine[::-1] → "nohtyP"
```

### 3. **Méthodes de Chaînes**
- `.upper()`, `.lower()` : conversion de casse
- `.replace(vieux, neuf)` : remplacement
- `.strip()`, `.lstrip()`, `.rstrip()` : suppression d'espaces
- `.split(séparateur)` : division en liste
- `.join(liste)` : assemblage avec séparateur

### 4. **Fonctions Built-in**
- `len(chaine)` : longueur
- `str(objet)` : conversion en chaîne
- `reversed(chaine)` : itérateur d'inversion

## 💡 Techniques Avancées

### 1. **Formatage de Chaînes**
```python
nom = "Alice"
age = 25

# f-strings (recommandé)
message = f"{nom} a {age} ans"

# format()
message = "{} a {} ans".format(nom, age)

# % formatting (déprécié)
message = "%s a %d ans" % (nom, age)
```

### 2. **Validation de Chaînes**
```python
# Test de caractères
chaine.isalpha()   # Lettres uniquement
chaine.isdigit()   # Chiffres uniquement
chaine.isalnum()   # Lettres et chiffres
chaine.isspace()   # Espaces uniquement
```

### 3. **Manipulation Avancée**
```python
# Nettoyage de texte
texte = "  Hello World!  "
propre = texte.strip().replace("!", "")

# Recherche
position = texte.find("World")  # Retourne index ou -1
contient = "Python" in texte    # Test d'appartenance
```

## 🚀 Applications Pratiques

### 1. **Validation d'Email**
```python
def valider_email(email):
    return "@" in email and "." in email and len(email) > 5

email = input("Email : ")
print("Email valide :", valider_email(email))
```

### 2. **Formatage de Noms**
```python
def formater_nom(nom):
    return nom.strip().lower().capitalize()

nom = input("Votre nom : ")
print("Formaté :", formater_nom(nom))
```

### 3. **Génération de Codes**
```python
def generer_code(prenom, annee):
    code = f"{prenom[:3].upper()}{annee[-2:]}"
    return code

prenom = input("Prénom : ")
annee = input("Année : ")
print("Code généré :", generer_code(prenom, annee))
```

## 🎯 Défis Supplémentaires

1. **Créez** un programme qui compte les mots d'une phrase
2. **Développez** un générateur d'acronymes
3. **Implémentez** un vérificateur de force de mot de passe
4. **Concevez** un formateur de numéros de téléphone

---

**Exercices complétés : 40/50** 🎯

*Continuez avec le [chapitre suivant](1-5-applications.md) pour les applications pratiques !*