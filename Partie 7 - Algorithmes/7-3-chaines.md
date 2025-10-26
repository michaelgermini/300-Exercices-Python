# Partie 7.3 : Chaînes et Cryptographie

## 🎯 Objectifs Pédagogiques

Ce chapitre explore les **algorithmes sur les chaînes** et les **méthodes de cryptographie** de base en Python. Nous apprendrons à manipuler les chaînes et à implémenter des chiffrements simples.

### Concepts Abordés
- **Distances sur chaînes** : Hamming, Levenshtein
- **Cryptographie** : César, Morse, anagrammes
- **Analyse de texte** : fréquences, motifs
- **Applications** : sécurité, traitement de texte

---

## 📝 Exercices Pratiques

### Exercice 271 : Calculer la distance de Hamming entre deux chaînes
**Objectif** : Mesurer la différence entre deux chaînes de même longueur.

```python
# Solution
def distance_hamming(chaine1, chaine2):
    """Calcule la distance de Hamming"""
    if len(chaine1) != len(chaine2):
        raise ValueError("Les chaînes doivent avoir la même longueur")

    distance = 0
    for c1, c2 in zip(chaine1, chaine2):
        if c1 != c2:
            distance += 1

    return distance

# Tests
paires_test = [
    ("python", "python"),  # Distance 0
    ("python", "java"),    # Distance 6
    ("hello", "hallo"),    # Distance 1
    ("test", "text"),      # Distance 2
    ("abc", "abc"),        # Distance 0
]

print("Distances de Hamming :")
for ch1, ch2 in paires_test:
    dist = distance_hamming(ch1, ch2)
    print(f"Distance('{ch1}', '{ch2}') = {dist}")

# Distance normalisée (pourcentage)
def distance_hamming_normalisee(chaine1, chaine2):
    """Distance de Hamming normalisée"""
    if len(chaine1) != len(chaine2):
        raise ValueError("Longueurs différentes")

    distance = distance_hamming(chaine1, chaine2)
    return distance / len(chaine1) * 100

print("\nDistances normalisées (%) :")
for ch1, ch2 in paires_test:
    dist_norm = distance_hamming_normalisee(ch1, ch2)
    print(f"Distance normalisée('{ch1}', '{ch2}') = {dist_norm:.1f}%")
```

**Explication** :
- **Distance de Hamming** : nombre de positions différentes
- **Même longueur** : prérequis pour la comparaison
- **Applications** : correction d'erreurs, similarité
- **Normalisation** : pourcentage de différence

**Test** : "python" et "java" → distance 6.

---

### Exercice 272 : Calculer la distance de Levenshtein entre deux chaînes
**Objectif** : Mesurer la différence avec insertions, suppressions, substitutions.

```python
# Solution
def distance_levenshtein(chaine1, chaine2):
    """Calcule la distance de Levenshtein (édition)"""
    m, n = len(chaine1), len(chaine2)

    # Matrice des distances
    matrice = [[0] * (n + 1) for _ in range(m + 1)]

    # Initialisation première ligne et colonne
    for i in range(m + 1):
        matrice[i][0] = i
    for j in range(n + 1):
        matrice[0][j] = j

    # Calcul de la distance
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if chaine1[i-1] == chaine2[j-1]:
                cout = 0
            else:
                cout = 1

            matrice[i][j] = min(
                matrice[i-1][j] + 1,      # Suppression
                matrice[i][j-1] + 1,      # Insertion
                matrice[i-1][j-1] + cout  # Substitution
            )

    return matrice[m][n]

# Tests
paires_test = [
    ("kitten", "sitting"),    # Distance 3
    ("python", "java"),       # Distance 6
    ("hello", "hallo"),       # Distance 1
    ("test", "test"),         # Distance 0
    ("abc", "def"),          # Distance 3
]

print("Distances de Levenshtein :")
for ch1, ch2 in paires_test:
    dist = distance_levenshtein(ch1, ch2)
    print(f"Distance('{ch1}', '{ch2}') = {dist}")

# Explications détaillées
print("\nExplications pour 'kitten' → 'sitting' :")
print("kitten → s i t t e n")
print("sitting → k i t t i n g")
print("Opérations : remplacer 'k' par 's', 'e' par 'i', ajouter 'g'")
```

**Explication** :
- **Distance d'édition** : coût minimal de transformation
- **Opérations** : insertion, suppression, substitution
- **Matrice dynamique** : programmation dynamique
- **Applications** : correction orthographique, diff

**Test** : "kitten" → "sitting" = 3 opérations.

---

### Exercice 273 : Vérifier si une chaîne est anagramme d'une autre
**Objectif** : Vérifier si deux chaînes sont des anagrammes.

```python
# Solution
def sont_anagrammes(chaine1, chaine2):
    """Vérifie si deux chaînes sont des anagrammes"""
    # Suppression des espaces et conversion en minuscules
    chaine1_propre = chaine1.replace(" ", "").lower()
    chaine2_propre = chaine2.replace(" ", "").lower()

    # Tri des caractères
    return sorted(chaine1_propre) == sorted(chaine2_propre)

# Tests
paires_test = [
    ("listen", "silent"),      # Anagrammes
    ("evil", "vile"),          # Anagrammes
    ("python", "java"),        # Pas anagrammes
    ("a gentleman", "elegant man"),  # Anagrammes
    ("rat", "car"),           # Pas anagrammes
]

print("Tests d'anagrammes :")
for ch1, ch2 in paires_test:
    resultat = sont_anagrammes(ch1, ch2)
    print(f"'{ch1}' et '{ch2}' sont anagrammes : {resultat}")

# Anagrammes avec compte de caractères
def sont_anagrammes_compte(chaine1, chaine2):
    """Version avec Counter"""
    from collections import Counter

    chaine1_propre = chaine1.replace(" ", "").lower()
    chaine2_propre = chaine2.replace(" ", "").lower()

    return Counter(chaine1_propre) == Counter(chaine2_propre)

print("\nAvec Counter :")
for ch1, ch2 in paires_test:
    resultat = sont_anagrammes_compte(ch1, ch2)
    print(f"'{ch1}' et '{ch2}' : {resultat}")
```

**Explication** :
- **Tri des caractères** : méthode simple
- **Counter** : comptage des caractères
- **Normalisation** : minuscules, suppression espaces
- **Applications** : puzzles, cryptographie

**Test** : "listen" et "silent" (anagrammes).

---

### Exercice 274 : Chiffrement César
**Objectif** : Implémenter le chiffrement de César.

```python
# Solution
def chiffrer_cesar(texte, decalage=3):
    """Chiffre un texte avec le code de César"""
    resultat = ""

    for caractere in texte:
        if caractere.isalpha():
            # Décalage dans l'alphabet
            base = ord('A') if caractere.isupper() else ord('a')
            caractere_chiffre = chr((ord(caractere) - base + decalage) % 26 + base)
            resultat += caractere_chiffre
        else:
            # Caractères non alphabétiques inchangés
            resultat += caractere

    return resultat

# Tests
textes_test = [
    "Hello World",
    "Python",
    "Bonjour tout le monde",
    "ATTENTION",
    "test 123 !?"
]

print("Chiffrement César (décalage 3) :")
for texte in textes_test:
    chiffre = chiffrer_cesar(texte, 3)
    print(f"'{texte}' → '{chiffre}'")

# Démonstration avec différents décalages
print("\nDifférents décalages pour 'Python' :")
for decalage in range(1, 6):
    chiffre = chiffrer_cesar("Python", decalage)
    print(f"Décalage {decalage}: '{chiffre}'")
```

**Explication** :
- **Décalage circulaire** : (caractère - base + décalage) % 26
- **Majuscules/Minuscules** : traitement séparé
- **Caractères non alpha** : conservés
- **Applications** : chiffrement simple, puzzles

**Test** : "Hello" → "Khoor" (décalage 3).

---

### Exercice 275 : Déchiffrement César
**Objectif** : Déchiffrer un texte chiffré avec César.

```python
# Solution
def dechiffrer_cesar(texte_chiffre, decalage=3):
    """Déchiffre un texte chiffré avec César"""
    # Déchiffrement = chiffrement avec décalage négatif
    return chiffrer_cesar(texte_chiffre, -decalage)

# Tests
textes_chiffres = [
    "Khoor Zruog",
    "Sbwkrq",
    "Erxqmrxu wrxw oh prqgh",
    "DWWHQWLRQ"
]

print("Déchiffrement César (décalage 3) :")
for texte_chiffre in textes_chiffres:
    dechiffre = dechiffrer_cesar(texte_chiffre, 3)
    print(f"'{texte_chiffre}' → '{dechiffre}'")

# Déchiffrement automatique (attaque par force brute)
def dechiffrement_force_brute(texte_chiffre):
    """Essaie tous les décalages possibles"""
    print(f"\nDéchiffrement par force brute de '{texte_chiffre}' :")
    for decalage in range(1, 26):
        dechiffre = dechiffrer_cesar(texte_chiffre, decalage)
        print(f"Décalage {decalage"2d"}: '{dechiffre}'")

# Test de force brute
dechiffrement_force_brute("Sbwkrq")
```

**Explication** :
- **Décalage inverse** : -décalage pour déchiffrer
- **Force brute** : test de tous les décalages
- **Applications** : cryptanalyse, sécurité
- **Limite** : 26 possibilités seulement

**Test** : "Khoor Zruog" → "Hello World".

---

## 🔍 Points Clés à Retenir

### 1. **Distance de Hamming**
```python
def distance_hamming(s1, s2):
    if len(s1) != len(s2):
        raise ValueError("Longueurs différentes")
    return sum(c1 != c2 for c1, c2 in zip(s1, s2))
```

### 2. **Distance de Levenshtein**
```python
def distance_levenshtein(s1, s2):
    m, n = len(s1), len(s2)
    matrice = [[0] * (n + 1) for _ in range(m + 1)]

    for i in range(m + 1):
        matrice[i][0] = i
    for j in range(n + 1):
        matrice[0][j] = j

    for i in range(1, m + 1):
        for j in range(1, n + 1):
            cout = 0 if s1[i-1] == s2[j-1] else 1
            matrice[i][j] = min(
                matrice[i-1][j] + 1,     # Suppression
                matrice[i][j-1] + 1,     # Insertion
                matrice[i-1][j-1] + cout # Substitution
            )

    return matrice[m][n]
```

### 3. **Anagrammes**
```python
def sont_anagrammes(s1, s2):
    s1_clean = s1.replace(" ", "").lower()
    s2_clean = s2.replace(" ", "").lower()
    return sorted(s1_clean) == sorted(s2_clean)
```

### 4. **Chiffrement César**
```python
def chiffrer_cesar(texte, decalage):
    resultat = ""
    for c in texte:
        if c.isalpha():
            base = ord('A') if c.isupper() else ord('a')
            c_chiffre = chr((ord(c) - base + decalage) % 26 + base)
            resultat += c_chiffre
        else:
            resultat += c
    return resultat
```

## 💡 Optimisations et Astuces

### 1. **Distance de Hamming Optimisée**
```python
def distance_hamming_rapide(s1, s2):
    """Version optimisée avec zip"""
    return sum(c1 != c2 for c1, c2 in zip(s1, s2))
```

### 2. **Anagrammes avec Counter**
```python
from collections import Counter

def sont_anagrammes_counter(s1, s2):
    """Version avec Counter"""
    s1_clean = s1.replace(" ", "").lower()
    s2_clean = s2.replace(" ", "").lower()
    return Counter(s1_clean) == Counter(s2_clean)
```

### 3. **Chiffrement César avec Clés Variables**
```python
def chiffrer_cesar_cle(texte, cle="PYTHON"):
    """Chiffrement César avec clé variable"""
    resultat = ""
    cle_index = 0

    for c in texte:
        if c.isalpha():
            # Décalage basé sur la clé
            decalage = ord(cle[cle_index % len(cle)].upper()) - ord('A')
            base = ord('A') if c.isupper() else ord('a')
            c_chiffre = chr((ord(c) - base + decalage) % 26 + base)
            resultat += c_chiffre
            cle_index += 1
        else:
            resultat += c

    return resultat
```

## 🚀 Applications Pratiques

### 1. **Analyseur de Fréquences**
```python
def analyser_frequences(texte):
    """Analyse les fréquences de caractères"""
    from collections import Counter

    # Nettoyage du texte
    texte_propre = texte.lower().replace(" ", "").replace("\n", "")

    # Comptage des caractères
    frequences = Counter(texte_propre)

    # Tri par fréquence décroissante
    caracteres_tries = sorted(frequences.items(), key=lambda x: x[1], reverse=True)

    print("Analyse de fréquences :")
    total_caracteres = len(texte_propre)

    for caractere, freq in caracteres_tries[:10]:  # 10 plus fréquents
        pourcentage = (freq / total_caracteres) * 100
        print(f"'{caractere}': {freq"4d"} fois ({pourcentage"5.2f"}%)")

    return frequences

# Test
texte_test = """
Le Python est un langage de programmation très populaire.
Python est facile à apprendre et puissant.
Les programmeurs aiment Python pour sa simplicité.
"""

frequences = analyser_frequences(texte_test)
```

### 2. **Détecteur de Langue**
```python
def detecter_langue(texte, langues_etalon):
    """Détecte la langue d'un texte par fréquences"""
    from collections import Counter

    # Fréquences du texte
    texte_propre = texte.lower().replace(" ", "").replace("\n", "")
    freq_texte = Counter(texte_propre)

    # Comparaison avec les langues
    similarities = {}
    for langue, freq_etalon in langues_etalon.items():
        # Intersection des caractères présents
        caracteres_communs = set(freq_texte.keys()) & set(freq_etalon.keys())

        if caracteres_communs:
            # Similarité = moyenne des fréquences communes
            similarite = sum(min(freq_texte.get(c, 0), freq_etalon.get(c, 0))
                           for c in caracteres_communs) / len(caracteres_communs)
            similarities[langue] = similarite

    # Langue la plus probable
    if similarities:
        langue_detectee = max(similarities, key=similarities.get)
        return langue_detectee, similarities
    else:
        return "Inconnue", {}

# Test
langues_etalon = {
    "fr": Counter("les mots français ont des fréquences particulières"),
    "en": Counter("english words have different frequency patterns"),
    "es": Counter("las palabras españolas tienen frecuencias distintas")
}

texte_mystere = "Bonjour tout le monde, comment allez-vous ?"
langue, scores = detecter_langue(texte_mystere, langues_etalon)
print(f"Texte détecté comme : {langue}")
print(f"Scores : {scores}")
```

### 3. **Générateur de Mots de Passe**
```python
def generer_mot_de_passe(longueur=12, inclure_symboles=True):
    """Génère un mot de passe sécurisé"""
    import random
    import string

    # Caractères disponibles
    minuscules = string.ascii_lowercase
    majuscules = string.ascii_uppercase
    chiffres = string.digits
    symboles = "!@#$%^&*()_+-=[]{}|;:,.<>?" if inclure_symboles else ""

    tous_caracteres = minuscules + majuscules + chiffres + symboles

    # Génération du mot de passe
    mot_de_passe = ''.join(random.choice(tous_caracteres) for _ in range(longueur))

    # Vérification des critères de sécurité
    a_minuscules = any(c in minuscules for c in mot_de_passe)
    a_majuscules = any(c in majuscules for c in mot_de_passe)
    a_chiffres = any(c in chiffres for c in mot_de_passe)
    a_symboles = any(c in symboles for c in mot_de_passe) if inclure_symboles else True

    if a_minuscules and a_majuscules and a_chiffres and a_symboles:
        return mot_de_passe
    else:
        # Régénération si critères non satisfaits
        return generer_mot_de_passe(longueur, inclure_symboles)

# Tests
print("Génération de mots de passe :")
mots_de_passe = [generer_mot_de_passe(8), generer_mot_de_passe(12), generer_mot_de_passe(16, True)]
for i, mdp in enumerate(mots_de_passe):
    print(f"Mot de passe {i+1} ({len(mdp)} caractères) : {mdp}")
```

## 🎯 Défis Supplémentaires

1. **Implémentez** un chiffrement par substitution plus complexe
2. **Créez** un détecteur de similarité de textes
3. **Développez** un générateur de phrases avec Markov
4. **Concevez** un système de compression de texte simple

---

**Exercices complétés : 275/285** 🎯

*Continuez avec le [chapitre suivant](7-4-binaires.md) pour les opérations binaires !*
