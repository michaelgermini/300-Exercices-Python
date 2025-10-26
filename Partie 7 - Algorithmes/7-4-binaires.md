# Partie 7.4 : Opérations Binaires

## 🎯 Objectifs Pédagogiques

Ce chapitre explore les **opérations binaires** et les **manipulations de bits** en Python. Ces concepts sont essentiels pour la programmation système, les optimisations et la compréhension du niveau le plus bas de l'informatique.

### Concepts Abordés
- **Opérations bit à bit** : ET, OU, XOR, NOT
- **Décalages** : gauche, droite
- **Conversions** : binaire/décimal/hexadécimal
- **Applications** : masques, flags, optimisations

---

## 📝 Exercices Pratiques

### Exercice 276 : Opérations bit à bit : ET
**Objectif** : Implémenter l'opération ET bit à bit.

```python
# Solution
def et_bit_a_bit(a, b):
    """Opération ET bit à bit"""
    return a & b

# Tests
paires_test = [
    (5, 3),     # 101 & 011 = 001 = 1
    (10, 7),    # 1010 & 0111 = 0010 = 2
    (15, 9),    # 1111 & 1001 = 1001 = 9
    (0, 5),     # 0000 & 0101 = 0000 = 0
    (255, 127), # 11111111 & 01111111 = 01111111 = 127
]

print("Opérations ET bit à bit :")
for a, b in paires_test:
    resultat = et_bit_a_bit(a, b)
    binaire_a = bin(a)[2:].zfill(8)
    binaire_b = bin(b)[2:].zfill(8)
    binaire_resultat = bin(resultat)[2:].zfill(8)
    print(f"{a"3d"} ({binaire_a}) & {b"3d"} ({binaire_b}) = {resultat"3d"} ({binaire_resultat})")

# Applications : masques
print("\nApplications avec masques :")
nombre = 170  # 10101010
masque = 15   # 00001111 (4 bits de poids faible)

resultat_masque = nombre & masque
print(f"{nombre} & {masque} = {resultat_masque} (extraction des 4 bits de poids faible)")
```

**Explication** :
- **&** : ET bit à bit
- **Table de vérité** : 1&1=1, 1&0=0, 0&1=0, 0&0=0
- **Applications** : masques, extraction de bits
- **Binaire** : format binaire pour visualisation

**Test** : 5 & 3 = 1.

---

### Exercice 277 : Opérations bit à bit : OU
**Objectif** : Implémenter l'opération OU bit à bit.

```python
# Solution
def ou_bit_a_bit(a, b):
    """Opération OU bit à bit"""
    return a | b

# Tests
paires_test = [
    (5, 3),     # 101 | 011 = 111 = 7
    (10, 7),    # 1010 | 0111 = 1111 = 15
    (15, 9),    # 1111 | 1001 = 1111 = 15
    (0, 5),     # 0000 | 0101 = 0101 = 5
    (240, 15),  # 11110000 | 00001111 = 11111111 = 255
]

print("Opérations OU bit à bit :")
for a, b in paires_test:
    resultat = ou_bit_a_bit(a, b)
    binaire_a = bin(a)[2:].zfill(8)
    binaire_b = bin(b)[2:].zfill(8)
    binaire_resultat = bin(resultat)[2:].zfill(8)
    print(f"{a"3d"} ({binaire_a}) | {b"3d"} ({binaire_b}) = {resultat"3d"} ({binaire_resultat})")

# Applications : activation de bits
print("\nApplications avec activation de bits :")
nombre = 8    # 00001000
masque = 7    # 00000111

resultat_activation = nombre | masque
print(f"{nombre} | {masque} = {resultat_activation} (activation des 3 bits de poids faible)")
```

**Explication** :
- **|** : OU bit à bit
- **Table de vérité** : 1|1=1, 1|0=1, 0|1=1, 0|0=0
- **Applications** : activation de bits, union
- **Binaire** : visualisation des bits

**Test** : 5 | 3 = 7.

---

### Exercice 278 : Opérations bit à bit : XOR
**Objectif** : Implémenter l'opération XOR bit à bit.

```python
# Solution
def xor_bit_a_bit(a, b):
    """Opération XOR bit à bit"""
    return a ^ b

# Tests
paires_test = [
    (5, 3),     # 101 ^ 011 = 110 = 6
    (10, 7),    # 1010 ^ 0111 = 1101 = 13
    (15, 9),    # 1111 ^ 1001 = 0110 = 6
    (0, 5),     # 0000 ^ 0101 = 0101 = 5
    (255, 127), # 11111111 ^ 01111111 = 10000000 = 128
]

print("Opérations XOR bit à bit :")
for a, b in paires_test:
    resultat = xor_bit_a_bit(a, b)
    binaire_a = bin(a)[2:].zfill(8)
    binaire_b = bin(b)[2:].zfill(8)
    binaire_resultat = bin(resultat)[2:].zfill(8)
    print(f"{a"3d"} ({binaire_a}) ^ {b"3d"} ({binaire_b}) = {resultat"3d"} ({binaire_resultat})")

# Applications : échange sans variable temporaire
print("\nApplications avec XOR :")
a, b = 5, 10
print(f"Avant échange : a={a}, b={b}")

a = a ^ b
b = a ^ b
a = a ^ b

print(f"Après échange avec XOR : a={a}, b={b}")
```

**Explication** :
- **^** : XOR bit à bit
- **Table de vérité** : 1^1=0, 1^0=1, 0^1=1, 0^0=0
- **Applications** : échange, cryptographie, parité
- **Échange** : a ^= b; b ^= a; a ^= b

**Test** : 5 ^ 3 = 6.

---

### Exercice 279 : Décalage à gauche (<<)
**Objectif** : Implémenter le décalage à gauche des bits.

```python
# Solution
def decalage_gauche(n, positions):
    """Décalage à gauche de n positions"""
    return n << positions

# Tests
valeurs_test = [
    (5, 1),     # 101 << 1 = 1010 = 10
    (10, 2),    # 1010 << 2 = 101000 = 40
    (15, 1),    # 1111 << 1 = 11110 = 30
    (1, 4),     # 1 << 4 = 10000 = 16
    (255, 1),   # 11111111 << 1 = 11111110 = 510
]

print("Décalages à gauche :")
for n, pos in valeurs_test:
    resultat = decalage_gauche(n, pos)
    binaire_n = bin(n)[2:].zfill(8)
    binaire_resultat = bin(resultat)[2:].zfill(8)
    print(f"{n"3d"} ({binaire_n}) << {pos} = {resultat"3d"} ({binaire_resultat})")

# Applications : multiplication par 2^k
print("\nApplications : multiplication par puissances de 2")
for k in range(5):
    resultat = decalage_gauche(3, k)
    print(f"3 << {k} = {resultat} (3 × 2^{k} = {3 * (2**k)})")
```

**Explication** :
- **<<** : décalage à gauche
- **Multiplication** : × 2^positions
- **Applications** : optimisation, puissances de 2
- **Dépassement** : bits tombent à gauche

**Test** : 5 << 1 = 10.

---

### Exercice 280 : Décalage à droite (>>)
**Objectif** : Implémenter le décalage à droite des bits.

```python
# Solution
def decalage_droite(n, positions):
    """Décalage à droite de n positions"""
    return n >> positions

# Tests
valeurs_test = [
    (10, 1),    # 1010 >> 1 = 101 = 5
    (16, 2),    # 10000 >> 2 = 100 = 4
    (255, 3),   # 11111111 >> 3 = 11111 = 31
    (100, 2),   # 1100100 >> 2 = 11001 = 25
    (7, 1),     # 111 >> 1 = 11 = 3
]

print("Décalages à droite :")
for n, pos in valeurs_test:
    resultat = decalage_droite(n, pos)
    binaire_n = bin(n)[2:].zfill(8)
    binaire_resultat = bin(resultat)[2:].zfill(8)
    print(f"{n"3d"} ({binaire_n}) >> {pos} = {resultat"3d"} ({binaire_resultat})")

# Applications : division par 2^k
print("\nApplications : division par puissances de 2")
for k in range(4):
    resultat = decalage_droite(20, k)
    print(f"20 >> {k} = {resultat} (20 ÷ 2^{k} = {20 // (2**k)})")
```

**Explication** :
- **>>** : décalage à droite
- **Division entière** : ÷ 2^positions
- **Applications** : optimisation, extraction
- **Signe** : préserve le signe pour les négatifs

**Test** : 10 >> 1 = 5.

---

## 🔍 Points Clés à Retenir

### 1. **Opérations Bit à Bit**
```python
# ET bit à bit
a & b        # 1 si les deux bits valent 1

# OU bit à bit
a | b        # 1 si au moins un bit vaut 1

# XOR bit à bit
a ^ b        # 1 si bits différents

# NOT bit à bit
~a           # Inversion de tous les bits

# Décalages
a << n       # Décalage à gauche de n positions
a >> n       # Décalage à droite de n positions
```

### 2. **Conversions**
```python
# Décimal vers binaire
bin(42)      # '0b101010'
bin(42)[2:]  # '101010'

# Binaire vers décimal
int('101010', 2)  # 42

# Hexadécimal
hex(42)      # '0x2a'
int('2a', 16)  # 42
```

### 3. **Masques et Flags**
```python
# Masque pour extraire des bits
masque_4_bits = 0b1111  # 15

# Activation de bits
flag_actif = valeur | masque

# Test de bits
if valeur & masque:
    print("Bits activés")

# Inversion de bits
inverse = valeur ^ masque
```

### 4. **Optimisations**
```python
# Multiplication par 2 rapide
x * 2        # Peut être remplacé par
x << 1       # Plus rapide sur certains processeurs

# Division par 2 rapide
x // 2       # Peut être remplacé par
x >> 1       # Plus rapide

# Test de parité
if x & 1:    # x impair
if not (x & 1):  # x pair
```

## 💡 Optimisations et Astuces

### 1. **Masques pour Permissions**
```python
# Système de permissions avec bits
LIRE = 1 << 0    # 1
ECRIRE = 1 << 1  # 2
EXECUTER = 1 << 2  # 4

# Permissions utilisateur
permissions = LIRE | EXECUTER  # 5

# Test de permission
if permissions & LIRE:
    print("Lecture autorisée")

if permissions & ECRIRE:
    print("Écriture autorisée")
else:
    print("Écriture interdite")
```

### 2. **Compression de Données**
```python
# Compression simple avec bits
def compresser_bits(donnees):
    """Compression basique avec masques"""
    resultat = 0
    for i, bit in enumerate(donnees[:8]):  # 8 bits max
        if bit:
            resultat |= (1 << i)
    return resultat

# Test
donnees = [True, False, True, True, False, True, False, False]
compresse = compresser_bits(donnees)
print(f"Données : {donnees}")
print(f"Compressé : {bin(compresse)} = {compresse}")
```

### 3. **Génération de Nombres Premiers**
```python
def generer_premiers_bitwise(limite):
    """Génère les nombres premiers avec opérations bit à bit"""
    if limite < 2:
        return []

    # Crible d'Ératosthène avec bits
    est_premier = [True] * (limite + 1)
    est_premier[0] = est_premier[1] = False

    for i in range(2, int(limite**0.5) + 1):
        if est_premier[i]:
            # Marquer les multiples avec opérations bit à bit
            for j in range(i*i, limite + 1, i):
                est_premier[j] = False

    return [i for i in range(2, limite + 1) if est_premier[i]]

# Test
premiers = generer_premiers_bitwise(100)
print(f"Nombres premiers jusqu'à 100 : {len(premiers)}")
print(premiers)
```

## 🚀 Applications Pratiques

### 1. **Système de Permissions**
```python
class Permissions:
    """Système de permissions avec bits"""

    # Flags de permissions
    LIRE = 1 << 0      # 1
    ECRIRE = 1 << 1    # 2
    EXECUTER = 1 << 2  # 4
    SUPPRIMER = 1 << 3 # 8
    ADMIN = 1 << 4     # 16

    def __init__(self, valeur=0):
        self.valeur = valeur

    def ajouter_permission(self, permission):
        """Ajoute une permission"""
        self.valeur |= permission

    def supprimer_permission(self, permission):
        """Supprime une permission"""
        self.valeur &= ~permission

    def a_permission(self, permission):
        """Teste une permission"""
        return bool(self.valeur & permission)

    def permissions_actives(self):
        """Liste les permissions actives"""
        permissions = []
        if self.a_permission(self.LIRE):
            permissions.append("LIRE")
        if self.a_permission(self.ECRIRE):
            permissions.append("ECRIRE")
        if self.a_permission(self.EXECUTER):
            permissions.append("EXECUTER")
        if self.a_permission(self.SUPPRIMER):
            permissions.append("SUPPRIMER")
        if self.a_permission(self.ADMIN):
            permissions.append("ADMIN")
        return permissions

    def __str__(self):
        return f"Permissions: {self.permissions_actives()} ({bin(self.valeur)})"

# Test
perms = Permissions()

print("Permissions initiales :")
print(perms)

# Ajout de permissions
perms.ajouter_permission(Permissions.LIRE)
perms.ajouter_permission(Permissions.ECRIRE)
print("\nAprès ajout LIRE et ECRIRE :")
print(perms)

# Test de permissions
print(f"\nA permission LIRE : {perms.a_permission(Permissions.LIRE)}")
print(f"A permission EXECUTER : {perms.a_permission(Permissions.EXECUTER)}")

# Ajout admin
perms.ajouter_permission(Permissions.ADMIN)
print("\nAprès ajout ADMIN :")
print(perms)
```

### 2. **Encodeur/Decodeur de Messages**
```python
def encoder_message(message, cle):
    """Encode un message avec XOR"""
    return ''.join(chr(ord(c) ^ cle) for c in message)

def decoder_message(message_encode, cle):
    """Décode un message avec XOR"""
    return encoder_message(message_encode, cle)  # XOR est symétrique

# Test
message_original = "Hello World!"
cle = 42

message_encode = encoder_message(message_original, cle)
message_decode = decoder_message(message_encode, cle)

print("Message original :", message_original)
print("Message encodé :", message_encode)
print("Message décodé :", message_decode)
print("Décodage réussi :", message_original == message_decode)
```

### 3. **Calculateur de Parité**
```python
def calculer_parite(n):
    """Calcule la parité d'un nombre"""
    parite = 0
    while n:
        parite ^= (n & 1)  # XOR avec le bit de poids faible
        n >>= 1           # Décalage à droite
    return parite

def verifier_parite(n):
    """Vérifie la parité avec l'opérateur %"""
    return n % 2 == calculer_parite(n)

# Tests
nombres_test = [0, 1, 2, 3, 4, 5, 7, 8, 15, 16, 255]

print("Parité des nombres :")
for nombre in nombres_test:
    parite_xor = calculer_parite(nombre)
    parite_mod = nombre % 2
    print(f"{nombre"3d"} : XOR={parite_xor}, Modulo={parite_mod}, Identique={parite_xor == parite_mod}")

# Application : détection d'erreurs
donnees = [0b1010, 0b1100, 0b1111]  # Données avec parité
donnees_avec_parite = [(data << 1) | calculer_parite(data) for data in donnees]
print(f"\nDonnées avec bit de parité : {[bin(d) for d in donnees_avec_parite]}")
```

## 🎯 Défis Supplémentaires

1. **Implémentez** un système de chiffrement par substitution bit à bit
2. **Créez** un générateur de nombres pseudo-aléatoires avec XOR
3. **Développez** un système de hachage simple avec opérations bit à bit
4. **Concevez** un compresseur de données basé sur les patterns binaires

---

**Exercices complétés : 280/285** 🎯

*Continuez avec le [chapitre suivant](7-5-applications.md) pour les applications finales !*
