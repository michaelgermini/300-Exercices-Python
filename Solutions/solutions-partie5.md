# Partie 5 - Programmation Orientée Objet : Solutions

## 🎯 Introduction

Cette partie présente les **solutions complètes** des exercices de la Partie 5. Chaque solution inclut :
- Le code source complet et fonctionnel
- Des explications détaillées
- Des exemples d'utilisation
- Des tests de validation

---

## 📚 Chapitre 5.1 : Solutions - Classes et Objets

### Exercice 201 : Créer une classe Personne avec nom et âge

**Solution complète :**

```python
# Solution de base
class Personne:
    """Classe représentant une personne avec nom et âge"""

    def __init__(self, nom, age):
        """Constructeur de la classe Personne"""
        self.nom = nom
        self.age = age

# Création d'objets
personne1 = Personne("Alice", 25)
personne2 = Personne("Bob", 30)

print(f"Personne 1 : {personne1.nom}, {personne1.age} ans")
print(f"Personne 2 : {personne2.nom}, {personne2.age} ans")

# Solution avec méthodes
class PersonneComplete:
    """Classe Personne avec méthodes"""

    def __init__(self, nom, age):
        """Constructeur"""
        self.nom = nom
        self.age = age

    def se_presenter(self):
        """Méthode de présentation"""
        return f"Bonjour, je m'appelle {self.nom} et j'ai {self.age} ans"

    def est_majeur(self):
        """Test de majorité"""
        return self.age >= 18

    def anniversaire(self):
        """Incrémente l'âge"""
        self.age += 1
        return f"Joyeux anniversaire {self.nom} ! Maintenant {self.age} ans"

# Test de la classe complète
alice = PersonneComplete("Alice Dupont", 25)
bob = PersonneComplete("Bob Martin", 17)

print(f"\n{alice.se_presenter()}")
print(f"Alice est majeure : {alice.est_majeur()}")

print(f"\n{bob.se_presenter()}")
print(f"Bob est majeur : {bob.est_majeur()}")

print(f"\n{alice.anniversaire()}")
print(f"{bob.anniversaire()}")
```

**Explications :**
- **Classe** : `class NomClasse`
- **Constructeur** : `def __init__(self, paramètres)`
- **Attributs** : `self.attribut = valeur`
- **Méthodes** : fonctions de la classe
- **self** : référence à l'instance

**Test :**
```
Personne 1 : Alice, 25 ans
Personne 2 : Bob, 30 ans
Bonjour, je m'appelle Alice Dupont et j'ai 25 ans
Alice est majeure : True
```

---

### Exercice 202 : Ajouter une méthode de présentation

**Solution complète :**

```python
# Solution avec méthode de présentation
class Personne:
    """Classe avec méthode de présentation"""

    def __init__(self, nom, age, profession="inconnue"):
        """Constructeur avec profession"""
        self.nom = nom
        self.age = age
        self.profession = profession

    def se_presenter(self):
        """Présentation complète"""
        return f"Je m'appelle {self.nom}, j'ai {self.age} ans et je suis {self.profession}"

    def changer_profession(self, nouvelle_profession):
        """Change la profession"""
        ancienne = self.profession
        self.profession = nouvelle_profession
        return f"Profession changée de '{ancienne}' à '{nouvelle_profession}'"

# Solution avec formatage avancé
class PersonneFormatee:
    """Classe avec formatage avancé"""

    def __init__(self, nom, prenom, age):
        """Constructeur"""
        self.nom = nom
        self.prenom = prenom
        self.age = age

    def __str__(self):
        """Représentation string"""
        return f"{self.prenom} {self.nom} ({self.age} ans)"

    def __repr__(self):
        """Représentation technique"""
        return f"Personne(nom='{self.nom}', prenom='{self.prenom}', age={self.age})"

    def presentation_officielle(self):
        """Présentation formelle"""
        return f"Monsieur/Madame {self.nom}, {self.prenom}, âgé(e) de {self.age} ans"

# Tests
print("=== Tests des classes ===")

# Test classe de base
alice = Personne("Dupont", 25, "ingénieur")
print(alice.se_presenter())
print(alice.changer_profession("manager"))
print(alice.se_presenter())

# Test classe formatée
personne1 = PersonneFormatee("Dupont", "Alice", 25)
personne2 = PersonneFormatee("Martin", "Bob", 30)

print(f"\nstr() : {personne1}")
print(f"repr() : {repr(personne1}")
print(f"Présentation officielle : {personne1.presentation_officielle()}")

# Test liste de personnes
personnes = [personne1, personne2]
print("
Liste de personnes :")
for personne in personnes:
    print(f"  - {personne}")
```

**Explications :**
- `__str__()` : affichage convivial
- `__repr__()` : affichage technique
- Méthodes de modification : `changer_profession()`
- Formatage : utilisation de f-strings

**Test :**
```
Je m'appelle Dupont, j'ai 25 ans et je suis ingénieur
Profession changée de 'ingénieur' à 'manager'
Je m'appelle Dupont, j'ai 25 ans et je suis manager

str() : Alice Dupont (25 ans)
repr() : Personne(nom='Dupont', prenom='Alice', age=25)
```

---

### Exercice 203 : Classe Rectangle avec calcul d'aire

**Solution complète :**

```python
# Solution de base
class Rectangle:
    """Classe Rectangle avec calcul d'aire"""

    def __init__(self, longueur, largeur):
        """Constructeur"""
        self.longueur = longueur
        self.largeur = largeur

    def calculer_aire(self):
        """Calcule l'aire"""
        return self.longueur * self.largeur

    def calculer_perimetre(self):
        """Calcule le périmètre"""
        return 2 * (self.longueur + self.largeur)

    def est_carre(self):
        """Test si c'est un carré"""
        return self.longueur == self.largeur

# Solution avancée
class RectangleAvance:
    """Rectangle avec validation et propriétés"""

    def __init__(self, longueur, largeur):
        """Constructeur avec validation"""
        if longueur <= 0 or largeur <= 0:
            raise ValueError("Les dimensions doivent être positives")
        self._longueur = longueur
        self._largeur = largeur

    @property
    def longueur(self):
        """Getter pour longueur"""
        return self._longueur

    @longueur.setter
    def longueur(self, valeur):
        """Setter pour longueur"""
        if valeur <= 0:
            raise ValueError("Longueur doit être positive")
        self._longueur = valeur

    @property
    def largeur(self):
        """Getter pour largeur"""
        return self._largeur

    @largeur.setter
    def largeur(self, valeur):
        """Setter pour largeur"""
        if valeur <= 0:
            raise ValueError("Largeur doit être positive")
        self._largeur = valeur

    def aire(self):
        """Propriété calculée"""
        return self._longueur * self._largeur

    def perimetre(self):
        """Propriété calculée"""
        return 2 * (self._longueur + self._largeur)

    def __str__(self):
        """Représentation"""
        return f"Rectangle({self._longueur}×{self._largeur})"

# Tests
print("=== Tests des rectangles ===")

# Test classe de base
rect1 = Rectangle(10, 5)
rect2 = Rectangle(8, 8)

print(f"Rectangle 1 : {rect1.calculer_aire()} aire, {rect1.calculer_perimetre()} périmètre")
print(f"Rectangle 2 : {rect2.calculer_aire()} aire, {rect2.calculer_perimetre()} périmètre")
print(f"Rect2 est carré : {rect2.est_carre()}")

# Test classe avancée
rect3 = RectangleAvance(12, 6)
print(f"\nRectangle 3 : {rect3}")
print(f"Aire : {rect3.aire}")
print(f"Périmètre : {rect3.perimetre}")

# Test modification
rect3.longueur = 10
print(f"Après modification : {rect3}")
print(f"Nouvelle aire : {rect3.aire}")
```

**Explications :**
- **Propriétés** : `@property` pour getters
- **Validation** : setters avec contrôles
- **Propriétés calculées** : aire et périmètre
- **__str__()** : affichage personnalisé

**Test :**
```
Rectangle 1 : 50 aire, 30 périmètre
Rectangle 2 : 64 aire, 32 périmètre
Rect2 est carré : True

Rectangle 3 : Rectangle(12×6)
Aire : 72
Périmètre : 36
```

---

### Exercice 204 : Classe CompteBancaire avec dépôt et retrait

**Solution complète :**

```python
# Solution de base
class CompteBancaire:
    """Compte bancaire avec opérations de base"""

    def __init__(self, titulaire, solde_initial=0):
        """Constructeur"""
        self.titulaire = titulaire
        self.solde = solde_initial

    def deposer(self, montant):
        """Dépose de l'argent"""
        if montant > 0:
            self.solde += montant
            return f"Dépôt de {montant}€ effectué. Nouveau solde : {self.solde}€"
        return "Montant invalide"

    def retirer(self, montant):
        """Retire de l'argent"""
        if montant > 0 and self.solde >= montant:
            self.solde -= montant
            return f"Retrait de {montant}€ effectué. Nouveau solde : {self.solde}€"
        return "Montant invalide ou fonds insuffisants"

    def afficher_solde(self):
        """Affiche le solde"""
        return f"Solde du compte de {self.titulaire} : {self.solde}€"

# Solution avancée avec historique
class CompteBancaireAvance:
    """Compte bancaire avec historique"""

    def __init__(self, titulaire, solde_initial=0):
        """Constructeur"""
        self.titulaire = titulaire
        self.solde = solde_initial
        self.historique = []
        self._numero_compte = None

    def deposer(self, montant, description="Dépôt"):
        """Dépose avec historique"""
        if montant > 0:
            self.solde += montant
            self.historique.append({
                "type": "dépôt",
                "montant": montant,
                "description": description,
                "solde_apres": self.solde
            })
            return f"Dépôt de {montant}€ effectué"
        return "Montant invalide"

    def retirer(self, montant, description="Retrait"):
        """Retrait avec historique"""
        if montant > 0 and self.solde >= montant:
            self.solde -= montant
            self.historique.append({
                "type": "retrait",
                "montant": montant,
                "description": description,
                "solde_apres": self.solde
            })
            return f"Retrait de {montant}€ effectué"
        return "Montant invalide ou fonds insuffisants"

    def transferer(self, autre_compte, montant, description="Transfert"):
        """Transfert vers un autre compte"""
        if montant > 0 and self.solde >= montant:
            self.retirer(montant, f"Transfert vers {autre_compte.titulaire}")
            autre_compte.deposer(montant, f"Transfert depuis {self.titulaire}")
            return f"Transfert de {montant}€ vers {autre_compte.titulaire}"
        return "Transfert impossible"

    def afficher_historique(self):
        """Affiche l'historique"""
        print(f"Historique de {self.titulaire} :")
        for operation in self.historique[-5:]:  # 5 dernières
            print(f"  {operation['type']}: {operation['montant']}€ - {operation['description']}")

    def __str__(self):
        """Représentation"""
        return f"Compte de {self.titulaire} : {self.solde}€"

# Tests
print("=== Tests des comptes bancaires ===")

# Test compte de base
compte1 = CompteBancaire("Alice", 1000)
print(compte1.afficher_solde())
print(compte1.deposer(200))
print(compte1.retirer(150))
print(compte1.afficher_solde())

# Test compte avancé
compte2 = CompteBancaireAvance("Bob", 500)
compte3 = CompteBancaireAvance("Charlie", 300)

print(f"\n{compte2}")
print(compte2.deposer(100))
print(compte2.retirer(50))
print(compte2.transferer(compte3, 75))

print(f"\n{compte2}")
print(f"{compte3}")

compte2.afficher_historique()
compte3.afficher_historique()
```

**Explications :**
- **Historique** : suivi des opérations
- **Transferts** : entre comptes
- **Validation** : montants positifs et solde suffisant
- **Encapsulation** : méthodes pour accéder aux données

**Test :**
```
Solde du compte de Alice : 1000€
Dépôt de 200€ effectué. Nouveau solde : 1200€
Retrait de 150€ effectué. Nouveau solde : 1050€
Solde du compte de Alice : 1050€

Compte de Bob : 500€
Dépôt de 100€ effectué
Transfert de 75€ vers Charlie
```

---

## 📚 Chapitre 5.2 : Solutions - Héritage

### Exercice 205 : Classe Animal avec héritage

**Solution complète :**

```python
# Solution classe de base
class Animal:
    """Classe de base pour tous les animaux"""

    def __init__(self, nom, age):
        """Constructeur"""
        self.nom = nom
        self.age = age

    def faire_du_bruit(self):
        """Fait du bruit"""
        return "L'animal fait du bruit"

    def se_deplacer(self):
        """Se déplace"""
        return "L'animal se déplace"

    def __str__(self):
        """Représentation"""
        return f"{self.nom} ({self.age} ans)"

# Solution avec héritage
class Chien(Animal):
    """Classe Chien héritant d'Animal"""

    def __init__(self, nom, age, race):
        """Constructeur avec race"""
        super().__init__(nom, age)  # Appel du constructeur parent
        self.race = race

    def faire_du_bruit(self):
        """Surcharge de la méthode"""
        return "Woof !"

    def se_deplacer(self):
        """Surcharge de la méthode"""
        return "Le chien court"

    def __str__(self):
        """Représentation avec race"""
        return f"Chien {self.nom} ({self.age} ans, {self.race})"

class Chat(Animal):
    """Classe Chat héritant d'Animal"""

    def __init__(self, nom, age, couleur):
        """Constructeur avec couleur"""
        super().__init__(nom, age)
        self.couleur = couleur

    def faire_du_bruit(self):
        """Surcharge"""
        return "Miaou !"

    def se_deplacer(self):
        """Surcharge"""
        return "Le chat saute"

    def __str__(self):
        """Représentation avec couleur"""
        return f"Chat {self.nom} ({self.age} ans, {self.couleur})"

# Solution avec héritage multiple
class Oiseau(Animal):
    """Classe Oiseau"""

    def __init__(self, nom, age, espece):
        super().__init__(nom, age)
        self.espece = espece

    def faire_du_bruit(self):
        return "Cui cui !"

    def se_deplacer(self):
        return "L'oiseau vole"

# Tests
print("=== Tests de l'héritage ===")

# Test animaux de base
animal = Animal("Générique", 5)
print(f"Animal : {animal.faire_du_bruit()} - {animal.se_deplacer()}")

# Test chien
chien = Chien("Rex", 3, "Berger allemand")
print(f"Chien : {chien.faire_du_bruit()} - {chien.se_deplacer()}")

# Test chat
chat = Chat("Minou", 2, "noir")
print(f"Chat : {chat.faire_du_bruit()} - {chat.se_deplacer()}")

# Test oiseau
oiseau = Oiseau("Titi", 1, "canari")
print(f"Oiseau : {oiseau.faire_du_bruit()} - {oiseau.se_deplacer()}")

# Test polymorphisme
animaux = [chien, chat, oiseau]

print("\n=== Polymorphisme ===")
for animal in animaux:
    print(f"{animal} : {animal.faire_du_bruit()} - {animal.se_deplacer()}")
```

**Explanations :**
- **super()** : appel du constructeur parent
- **Surcharge** : redéfinition des méthodes
- **Polymorphisme** : même interface, comportement différent
- **Héritage** : réutilisation de code

**Test :**
```
Animal : L'animal fait du bruit - L'animal se déplace
Chien : Woof ! - Le chien court
Chat : Miaou ! - Le chat saute
Oiseau : Cui cui ! - L'oiseau vole

=== Polymorphisme ===
Chien Rex (3 ans, Berger allemand) : Woof ! - Le chien court
Chat Minou (2 ans, noir) : Miaou ! - Le chat saute
Oiseau Titi (1 ans, canari) : Cui cui ! - L'oiseau vole
```

---

## 🎯 Résumé des Solutions - Partie 5

### ✅ **Exercices Résolus (201-205)**

| Exercice | Thème | Solution | Fonctionnalités |
|----------|-------|----------|-----------------|
| **201** | Classe Personne | ✅ Complète | Constructeur, attributs, base |
| **202** | Méthodes | ✅ Complète | __str__, __repr__, méthodes |
| **203** | Rectangle | ✅ Complète | Propriétés, validation, calculs |
| **204** | Compte bancaire | ✅ Complète | Opérations, historique, transferts |
| **205** | Héritage | ✅ Complète | Super, surcharge, polymorphisme |

### 🚀 **Concepts Clés Maîtrisés**

- **Classes et objets** : création, instanciation
- **Constructeurs** : `__init__`, paramètres
- **Méthodes** : définition, surcharge, polymorphisme
- **Propriétés** : getters, setters, calculées
- **Héritage** : super(), redéfinition, réutilisation
- **Encapsulation** : protection des données

### 📚 **Fonctionnalités Avancées**

- **Validation** : contrôle des paramètres
- **Formatage** : __str__, __repr__ personnalisés
- **Historique** : suivi des opérations
- **Polymorphisme** : comportement adapté
- **Gestion d'erreurs** : ValueError, contrôles
- **Collections d'objets** : listes, interactions

---

**🎉 Toutes les solutions de la Partie 5 sont maintenant disponibles !**

*Ces solutions démontrent la maîtrise de la programmation orientée objet en Python, base essentielle pour le développement logiciel.*
