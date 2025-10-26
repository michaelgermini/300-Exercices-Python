# Partie 5.3 : Encapsulation et Surcharge

## 🎯 Objectifs Pédagogiques

Ce chapitre explore l'**encapsulation** et la **surcharge d'opérateurs** en Python, concepts avancés pour **protéger les données** et **personnaliser les opérateurs**.

### Concepts Abordés
- **Encapsulation** : attributs privés, getters, setters
- **Surcharge d'opérateurs** : +, ==, <, etc.
- **Méthodes spéciales** : __str__, __eq__, __lt__
- **Applications** : objets robustes et intuitifs

---

## 📝 Exercices Pratiques

### Exercice 215 : Surcharge d'opérateurs pour additionner deux objets
**Objectif** : Implémenter l'addition de deux objets personnalisés.

```python
# Solution
class Point:
    """Point 2D avec surcharge d'opérateurs"""

    def __init__(self, x, y):
        """Constructeur"""
        self.x = x
        self.y = y

    def __add__(self, other):
        """Addition de deux points"""
        if isinstance(other, Point):
            return Point(self.x + other.x, self.y + other.y)
        elif isinstance(other, (int, float)):
            return Point(self.x + other, self.y + other)
        else:
            raise TypeError("Addition non supportée")

    def __str__(self):
        """Représentation en chaîne"""
        return f"Point({self.x}, {self.y})"

    def __repr__(self):
        """Représentation Python"""
        return f"Point({self.x!r}, {self.y!r})"

# Tests
point1 = Point(3, 4)
point2 = Point(1, 2)
point3 = Point(-2, 5)

print(f"Point 1 : {point1}")
print(f"Point 2 : {point2}")
print(f"Point 3 : {point3}")

# Addition de points
somme_points = point1 + point2
print(f"Point1 + Point2 : {somme_points}")

# Addition avec scalaire
somme_scalaire = point1 + 5
print(f"Point1 + 5 : {somme_scalaire}")

# Addition en chaîne
resultat = point1 + point2 + point3
print(f"Point1 + Point2 + Point3 : {resultat}")

# Vérification
print(f"Représentation repr : {repr(somme_points)}")
```

**Explication** :
- **__add__** : surcharge de l'opérateur +
- **isinstance** : vérification du type
- **Types multiples** : point + point, point + nombre
- **Chaînage** : opérations successives

**Test** : (3, 4) + (1, 2) = (4, 6).

---

### Exercice 216 : Surcharge d'opérateurs pour comparer deux objets
**Objectif** : Implémenter la comparaison d'objets.

```python
# Solution
class Fraction:
    """Fraction avec surcharge de comparaison"""

    def __init__(self, numerateur, denominateur):
        """Constructeur"""
        if denominateur == 0:
            raise ValueError("Dénominateur ne peut être 0")
        self.numerateur = numerateur
        self.denominateur = denominateur
        self._simplifier()

    def _simplifier(self):
        """Simplifie la fraction"""
        import math
        pgcd = math.gcd(self.numerateur, self.denominateur)
        self.numerateur //= pgcd
        self.denominateur //= pgcd

    def __eq__(self, other):
        """Égalité de fractions"""
        if not isinstance(other, Fraction):
            return False
        return (self.numerateur == other.numerateur and
                self.denominateur == other.denominateur)

    def __lt__(self, other):
        """Infériorité"""
        if not isinstance(other, Fraction):
            return NotImplemented
        # Comparaison : a/b < c/d <=> a*d < b*c
        return (self.numerateur * other.denominateur <
                other.numerateur * self.denominateur)

    def __le__(self, other):
        """Inférieur ou égal"""
        return self == other or self < other

    def __str__(self):
        """Représentation"""
        return f"{self.numerateur}/{self.denominateur}"

    def __repr__(self):
        """Représentation Python"""
        return f"Fraction({self.numerateur}, {self.denominateur})"

# Tests
fractions = [
    Fraction(1, 2),   # 0.5
    Fraction(3, 4),   # 0.75
    Fraction(2, 3),   # ~0.666
    Fraction(4, 5),   # 0.8
    Fraction(1, 2),   # 0.5 (doublon)
]

print("Fractions créées :")
for frac in fractions:
    print(f"  {frac} = {frac.numerateur}/{frac.denominateur}")

# Tests d'égalité
print("\nTests d'égalité :")
print(f"Fraction(1,2) == Fraction(2,4) : {Fraction(1, 2) == Fraction(2, 4)}")
print(f"Fraction(1,2) == Fraction(3,4) : {Fraction(1, 2) == Fraction(3, 4)}")

# Tests de comparaison
print("\nTests de comparaison :")
for i in range(len(fractions) - 1):
    for j in range(i + 1, len(fractions)):
        frac1, frac2 = fractions[i], fractions[j]
        print(f"{frac1} < {frac2} : {frac1 < frac2}")
        print(f"{frac1} <= {frac2} : {frac1 <= frac2}")
```

**Explication** :
- **__eq__** : surcharge de ==
- **__lt__** : surcharge de <
- **__le__** : surcharge de <=
- **Simplification** : fractions automatiquement simplifiées
- **Comparaison** : produit croisé pour éviter les divisions

**Test** : 1/2 < 3/4 (vrai), 1/2 == 2/4 (vrai).

---

### Exercice 217 : Encapsulation : attribut privé avec getter et setter
**Objectif** : Implémenter l'encapsulation avec des attributs privés.

```python
# Solution
class CompteBancaire:
    """Compte bancaire avec encapsulation"""

    def __init__(self, titulaire, solde_initial=0):
        """Constructeur"""
        self.titulaire = titulaire
        self._solde = solde_initial  # Attribut privé (convention)
        self.__historique = []       # Attribut très privé

    @property
    def solde(self):
        """Getter pour le solde"""
        return self._solde

    @solde.setter
    def solde(self, nouveau_solde):
        """Setter pour le solde"""
        if nouveau_solde >= 0:
            ancien_solde = self._solde
            self._solde = nouveau_solde
            self.__historique.append(f"Solde modifié : {ancien_solde} → {nouveau_solde}")
        else:
            raise ValueError("Solde ne peut être négatif")

    @property
    def historique(self):
        """Getter pour l'historique"""
        return self.__historique.copy()  # Retourne une copie

    def deposer(self, montant):
        """Dépôt avec encapsulation"""
        if montant > 0:
            self.solde += montant  # Utilise le setter
            self.__historique.append(f"Dépôt : +{montant}")
            return f"Dépôt de {montant}€ effectué"
        return "Montant invalide"

    def retirer(self, montant):
        """Retrait avec encapsulation"""
        if montant > 0:
            if self._solde >= montant:
                self.solde -= montant  # Utilise le setter
                self.__historique.append(f"Retrait : -{montant}")
                return f"Retrait de {montant}€ effectué"
            return "Fonds insuffisants"
        return "Montant invalide"

    def info(self):
        """Informations du compte"""
        return f"Compte de {self.titulaire} : {self.solde}€"

# Tests
compte = CompteBancaire("Alice", 1000)

print(f"Compte initial : {compte.info()}")
print(f"Solde via getter : {compte.solde}")

# Dépôt et retrait
print(compte.deposer(500))
print(compte.retirer(200))
print(f"Solde après opérations : {compte.solde}")

# Historique
print(f"Historique : {compte.historique}")

# Tentative de modification directe
print("\nTentatives de modification directe :")
try:
    compte._solde = -500  # Modifie l'attribut privé
    print(f"Après modification directe : {compte.solde}")
except Exception as e:
    print(f"Erreur : {e}")

# Réinitialisation
compte = CompteBancaire("Alice", 1000)
try:
    compte.solde = 1500  # Utilise le setter
    print(f"Avec setter : {compte.solde}")
except Exception as e:
    print(f"Erreur setter : {e}")

try:
    compte.solde = -100  # Refusé par le setter
except Exception as e:
    print(f"Setter refuse : {e}")

print(f"Historique final : {compte.historique}")
```

**Explication** :
- **@property** : getter pour accès contrôlé
- **@setter** : setter pour modification contrôlée
- **Attributs privés** : _ (convention) et __ (name mangling)
- **Validation** : contrôles dans le setter
- **Historique** : suivi des modifications

**Test** : Encapsulation et validation du solde.

---

### Exercice 218 : Classe abstraite simple
**Objectif** : Implémenter une classe abstraite avec des méthodes abstraites.

```python
# Solution
from abc import ABC, abstractmethod

class FormeGeometrique(ABC):
    """Classe abstraite pour les formes géométriques"""

    def __init__(self, nom):
        """Constructeur"""
        self.nom = nom

    @abstractmethod
    def calculer_aire(self):
        """Méthode abstraite pour l'aire"""
        pass

    @abstractmethod
    def calculer_perimetre(self):
        """Méthode abstraite pour le périmètre"""
        pass

    def description(self):
        """Méthode concrète"""
        return f"Forme géométrique : {self.nom}"

    def info_complete(self):
        """Utilise les méthodes abstraites"""
        return (f"{self.description()}\n"
                f"Aire : {self.calculer_aire():.2f}\n"
                f"Périmètre : {self.calculer_perimetre():.2f}")

class Cercle(FormeGeometrique):
    """Cercle concret"""

    def __init__(self, rayon):
        super().__init__("Cercle")
        self.rayon = rayon

    def calculer_aire(self):
        import math
        return math.pi * self.rayon**2

    def calculer_perimetre(self):
        import math
        return 2 * math.pi * self.rayon

class Rectangle(FormeGeometrique):
    """Rectangle concret"""

    def __init__(self, largeur, hauteur):
        super().__init__("Rectangle")
        self.largeur = largeur
        self.hauteur = hauteur

    def calculer_aire(self):
        return self.largeur * self.hauteur

    def calculer_perimetre(self):
        return 2 * (self.largeur + self.hauteur)

    def est_carre(self):
        return self.largeur == self.hauteur

# Tests
try:
    # Impossible de créer une instance de la classe abstraite
    # forme = FormeGeometrique("Test")  # Erreur
    pass
except Exception as e:
    print(f"Erreur classe abstraite : {e}")

# Création d'instances concrètes
cercle = Cercle(5)
rectangle = Rectangle(4, 6)
carre = Rectangle(3, 3)

print("Tests des classes concrètes :")
print(cercle.info_complete())
print(rectangle.info_complete())
print(carre.info_complete())
print(f"Carré est un carré : {carre.est_carre()}")

# Polymorphisme avec classes abstraites
formes = [cercle, rectangle, carre]
print("\nPolymorphisme avec formes :")
for forme in formes:
    print(forme.info_complete())
```

**Explication** :
- **ABC** : classe abstraite de base
- **@abstractmethod** : méthodes à implémenter obligatoirement
- **Héritage forcé** : classes filles doivent implémenter
- **Polymorphisme** : appel uniforme des méthodes
- **Validation** : impossible d'instancier la classe abstraite

**Test** : Formes concrètes avec méthodes abstraites.

---

### Exercice 219 : Interface et implémentation
**Objectif** : Implémenter une interface avec des méthodes à implémenter.

```python
# Solution
from abc import ABC, abstractmethod

class InterfaceImprimable(ABC):
    """Interface pour les objets imprimables"""

    @abstractmethod
    def imprimer(self):
        """Méthode pour imprimer"""
        pass

    @abstractmethod
    def formater(self, format_type="texte"):
        """Méthode pour formater"""
        pass

class Document(InterfaceImprimable):
    """Document implémentant l'interface"""

    def __init__(self, titre, contenu):
        self.titre = titre
        self.contenu = contenu

    def imprimer(self):
        return f"Impression du document '{self.titre}':\n{self.contenu}"

    def formater(self, format_type="texte"):
        if format_type == "html":
            return f"<h1>{self.titre}</h1><p>{self.contenu}</p>"
        elif format_type == "markdown":
            return f"# {self.titre}\n\n{self.contenu}"
        else:
            return f"{self.titre}\n{'='*len(self.titre)}\n{self.contenu}"

class Image(InterfaceImprimable):
    """Image implémentant l'interface"""

    def __init__(self, nom, largeur, hauteur):
        self.nom = nom
        self.largeur = largeur
        self.hauteur = hauteur

    def imprimer(self):
        return f"Affichage de l'image '{self.nom}' ({self.largeur}×{self.hauteur})"

    def formater(self, format_type="texte"):
        if format_type == "html":
            return f'<img src="{self.nom}" width="{self.largeur}" height="{self.hauteur}" alt="{self.nom}">'
        else:
            return f"Image: {self.nom} ({self.largeur}×{self.hauteur})"

# Tests
documents = [
    Document("Rapport", "Ceci est un rapport important."),
    Image("photo.jpg", 800, 600)
]

print("Tests d'interface :")
for doc in documents:
    print(f"\n--- {type(doc).__name__} ---")
    print(f"Impression : {doc.imprimer()}")
    print(f"Format texte : {doc.formater('texte')}")
    print(f"Format HTML : {doc.formater('html')}")
    print(f"Format Markdown : {doc.formater('markdown')}")

# Test d'interface abstraite
try:
    # interface = InterfaceImprimable()  # Erreur
    pass
except Exception as e:
    print(f"\nErreur interface abstraite : {e}")
```

**Explication** :
- **Interface** : classe abstraite avec méthodes abstraites
- **Implémentation** : classes concrètes implémentent l'interface
- **Polymorphisme** : même interface, comportements différents
- **Formats multiples** : HTML, Markdown, texte

**Test** : Interface polymorphe pour documents et images.

---

### Exercice 220 : Polymorphisme avec méthode commune
**Objectif** : Démontrer le polymorphisme avec des méthodes communes.

```python
# Solution
class Animal:
    """Classe de base Animal"""

    def __init__(self, nom, age):
        self.nom = nom
        self.age = age

    def faire_du_bruit(self):
        """Méthode polymorphe"""
        return f"{self.nom} fait un bruit"

    def se_deplacer(self):
        """Méthode polymorphe"""
        return f"{self.nom} se déplace"

    def info(self):
        return f"{self.nom} ({self.age} ans)"

class Chien(Animal):
    """Chien avec comportement spécifique"""

    def __init__(self, nom, age, race="Inconnue"):
        super().__init__(nom, age)
        self.race = race

    def faire_du_bruit(self):
        return f"{self.nom} aboie : Woof!"

    def se_deplacer(self):
        return f"{self.nom} court sur ses pattes"

    def info(self):
        return f"{super().info()} - Race: {self.race}"

class Chat(Animal):
    """Chat avec comportement spécifique"""

    def __init__(self, nom, age, couleur="Noir"):
        super().__init__(nom, age)
        self.couleur = couleur

    def faire_du_bruit(self):
        return f"{self.nom} miaule : Miaou!"

    def se_deplacer(self):
        return f"{self.nom} se faufile discrètement"

    def info(self):
        return f"{super().info()} - Couleur: {self.couleur}"

class Oiseau(Animal):
    """Oiseau avec comportement spécifique"""

    def __init__(self, nom, age, espece="Moineau"):
        super().__init__(nom, age)
        self.espece = espece

    def faire_du_bruit(self):
        return f"{self.nom} chante : Cui-cui!"

    def se_deplacer(self):
        return f"{self.nom} vole dans les airs"

    def info(self):
        return f"{super().info()} - Espèce: {self.espece}"

# Tests polymorphisme
animaux = [
    Chien("Rex", 3, "Labrador"),
    Chat("Minou", 2, "Blanc"),
    Oiseau("Titi", 1, "Canari"),
    Animal("Animal générique", 5)
]

print("Tests de polymorphisme :")
for animal in animaux:
    print(f"\n--- {type(animal).__name__} : {animal.info()} ---")
    print(f"Bruit : {animal.faire_du_bruit()}")
    print(f"Déplacement : {animal.se_deplacer()}")

# Fonction polymorphe
def faire_parler(animaux):
    """Fonction qui fait parler tous les animaux"""
    print("\nConcert animalier :")
    for animal in animaux:
        print(f"  {animal.faire_du_bruit()}")

faire_parler(animaux)
```

**Explication** :
- **Polymorphisme** : même méthode, implémentations différentes
- **Héritage** : classes filles spécialisées
- **Surcharge** : redéfinition des méthodes
- **Fonction générique** : traitement uniforme

**Test** : Comportements différents pour chaque animal.

---

## 🔍 Points Clés à Retenir

### 1. **Encapsulation**
```python
class ClasseEncapsulee:
    def __init__(self, valeur):
        self._valeur_privee = valeur      # Convention : privé
        self.__valeur_tres_privee = valeur  # Name mangling

    @property
    def valeur(self):                     # Getter
        return self._valeur_privee

    @valeur.setter
    def valeur(self, nouvelle_valeur):   # Setter
        if condition_valide:
            self._valeur_privee = nouvelle_valeur

# Utilisation
obj = ClasseEncapsulee(10)
print(obj.valeur)        # Accès via getter
obj.valeur = 20          # Modification via setter
```

### 2. **Surcharge d'Opérateurs**
```python
class MonObjet:
    def __init__(self, valeur):
        self.valeur = valeur

    def __add__(self, other):      # +
        return MonObjet(self.valeur + other.valeur)

    def __eq__(self, other):       # ==
        return self.valeur == other.valeur

    def __lt__(self, other):       # <
        return self.valeur < other.valeur

    def __str__(self):             # str()
        return f"Objet({self.valeur})"

# Utilisation
obj1 = MonObjet(5)
obj2 = MonObjet(10)
print(obj1 + obj2)      # Objet(15)
print(obj1 == obj2)     # False
print(obj1 < obj2)      # True
```

### 3. **Méthodes Spéciales**
```python
class MonObjet:
    def __str__(self):      # str(objet)
        return "Représentation lisible"

    def __repr__(self):     # repr(objet)
        return "Représentation Python"

    def __eq__(self, other):  # objet == other
        return isinstance(other, MonObjet) and condition

    def __hash__(self):     # Pour ensembles/dictionnaires
        return hash(self.valeur_unique)

    def __len__(self):      # len(objet)
        return self.taille
```

### 4. **Classes Abstraites**
```python
from abc import ABC, abstractmethod

class ClasseAbstraite(ABC):
    @abstractmethod
    def methode_abstraite(self):
        pass

class ClasseConcrete(ClasseAbstraite):
    def methode_abstraite(self):
        return "Implémentation concrète"
```

## 💡 Optimisations et Astuces

### 1. **Propriétés Calculées**
```python
class Rectangle:
    def __init__(self, largeur, hauteur):
        self.largeur = largeur
        self.hauteur = hauteur

    @property
    def aire(self):
        """Aire calculée à la demande"""
        return self.largeur * self.hauteur

    @property
    def perimetre(self):
        """Périmètre calculé à la demande"""
        return 2 * (self.largeur + self.hauteur)

# Utilisation
rect = Rectangle(5, 10)
print(f"Aire : {rect.aire}")      # Accès comme attribut
print(f"Périmètre : {rect.perimetre}")
```

### 2. **Validation Avancée**
```python
class Email:
    def __init__(self, adresse):
        self.adresse = adresse  # Validation dans setter

    @property
    def adresse(self):
        return self._adresse

    @adresse.setter
    def adresse(self, valeur):
        if "@" in valeur and "." in valeur:
            self._adresse = valeur
        else:
            raise ValueError("Adresse email invalide")

# Test
try:
    email = Email("test@example.com")
    print(f"Email valide : {email.adresse}")
    email_invalide = Email("invalid-email")
except ValueError as e:
    print(f"Erreur : {e}")
```

### 3. **Opérateurs en Chaîne**
```python
class Vecteur:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Vecteur(self.x + other.x, self.y + other.y)

    def __mul__(self, scalaire):
        return Vecteur(self.x * scalaire, self.y * scalaire)

# Utilisation en chaîne
v1 = Vecteur(1, 2)
v2 = Vecteur(3, 4)
v3 = Vecteur(2, 1)

resultat = (v1 + v2) * 2 + v3
print(f"({v1} + {v2}) × 2 + {v3} = {resultat}")
```

## 🚀 Applications Pratiques

### 1. **Système de Devises**
```python
class Devise:
    """Représente une devise avec conversion"""

    def __init__(self, montant, code):
        self.montant = montant
        self.code = code

    @property
    def montant(self):
        return self._montant

    @montant.setter
    def montant(self, valeur):
        if valeur >= 0:
            self._montant = valeur
        else:
            raise ValueError("Montant négatif invalide")

    def __add__(self, other):
        if isinstance(other, Devise) and self.code == other.code:
            return Devise(self.montant + other.montant, self.code)
        return NotImplemented

    def __eq__(self, other):
        return (isinstance(other, Devise) and
                self.montant == other.montant and
                self.code == other.code)

    def __str__(self):
        return f"{self.montant:.2f} {self.code}"

    def convertir(self, taux, nouvelle_devise):
        """Conversion vers une autre devise"""
        montant_converti = self.montant * taux
        return Devise(montant_converti, nouvelle_devise)

# Test
euro1 = Devise(100, "EUR")
euro2 = Devise(50, "EUR")
dollar = Devise(120, "USD")

print(f"Euro 1 : {euro1}")
print(f"Euro 2 : {euro2}")
print(f"Dollar : {dollar}")

# Addition
total_euro = euro1 + euro2
print(f"Total EUR : {total_euro}")

# Égalité
euro_test = Devise(100, "EUR")
print(f"euro1 == euro_test : {euro1 == euro_test}")

# Conversion
taux_eur_usd = 1.1
euro_en_dollar = euro1.convertir(taux_eur_usd, "USD")
print(f"100 EUR = {euro_en_dollar}")
```

### 2. **Gestion de Stock avec Encapsulation**
```python
class ProduitStock:
    """Produit en stock avec encapsulation"""

    def __init__(self, nom, prix, quantite):
        self.nom = nom
        self.prix = prix
        self._quantite = quantite  # Privé
        self.__ventes = 0         # Très privé

    @property
    def quantite(self):
        """Quantité avec contrôle d'accès"""
        return self._quantite

    @quantite.setter
    def quantite(self, nouvelle_quantite):
        if nouvelle_quantite >= 0:
            self._quantite = nouvelle_quantite
        else:
            raise ValueError("Quantité ne peut être négative")

    @property
    def ventes(self):
        """Ventes (lecture seule)"""
        return self.__ventes

    def valeur_stock(self):
        """Valeur totale du stock"""
        return self.prix * self._quantite

    def vendre(self, quantite_vendue):
        """Vendre une quantité"""
        if 0 < quantite_vendue <= self._quantite:
            self._quantite -= quantite_vendue
            self.__ventes += quantite_vendue
            return f"Vente de {quantite_vendue} {self.nom}. Stock restant : {self._quantite}"
        return "Vente impossible"

    def restocker(self, quantite_ajoutee):
        """Ajouter du stock"""
        if quantite_ajoutee > 0:
            self.quantite += quantite_ajoutee
            return f"Restockage de {quantite_ajoutee} {self.nom}. Stock : {self._quantite}"
        return "Quantité invalide"

    def info(self):
        """Informations du produit"""
        return (f"{self.nom}: {self.prix}€, "
                f"Stock: {self._quantite}, "
                f"Ventes: {self.__ventes}, "
                f"Valeur: {self.valeur_stock():.2f}€")

# Test
produit = ProduitStock("Ordinateur", 800, 10)
print(produit.info())

print(produit.vendre(3))
print(produit.restocker(5))
print(produit.info())

# Tentatives d'accès direct
print(f"\nTentatives d'accès direct :")
print(f"Quantité via getter : {produit.quantite}")
print(f"Ventes via getter : {produit.ventes}")

try:
    produit._quantite = -5  # Modification directe
    print(f"Après modification directe : {produit.quantite}")
except Exception as e:
    print(f"Erreur setter : {e}")

# Name mangling
print(f"Attribut manglé : {produit._ProduitStock__ventes}")
```

### 3. **Système de Notation**
```python
class Note:
    """Note avec validation et opérateurs"""

    def __init__(self, valeur, matiere):
        self.matiere = matiere
        self.valeur = valeur  # Validation dans setter

    @property
    def valeur(self):
        return self._valeur

    @valeur.setter
    def valeur(self, nouvelle_valeur):
        if 0 <= nouvelle_valeur <= 20:
            self._valeur = nouvelle_valeur
        else:
            raise ValueError("Note doit être entre 0 et 20")

    def __add__(self, other):
        """Addition de notes"""
        if isinstance(other, Note):
            return Note((self.valeur + other.valeur) / 2, f"{self.matiere}+{other.matiere}")
        elif isinstance(other, (int, float)):
            return Note((self.valeur + other) / 2, f"{self.matiere}+moyenne")
        return NotImplemented

    def __eq__(self, other):
        """Égalité de notes"""
        if isinstance(other, Note):
            return self.valeur == other.valeur
        elif isinstance(other, (int, float)):
            return self.valeur == other
        return False

    def __lt__(self, other):
        """Comparaison de notes"""
        if isinstance(other, Note):
            return self.valeur < other.valeur
        elif isinstance(other, (int, float)):
            return self.valeur < other
        return NotImplemented

    def mention(self):
        """Mention selon la note"""
        if self.valeur >= 16:
            return "Très bien"
        elif self.valeur >= 14:
            return "Bien"
        elif self.valeur >= 12:
            return "Assez bien"
        elif self.valeur >= 10:
            return "Passable"
        else:
            return "Insuffisant"

    def __str__(self):
        return f"{self.matiere}: {self.valeur}/20 ({self.mention()})"

# Test
notes = [
    Note(18, "Mathématiques"),
    Note(15, "Physique"),
    Note(12, "Chimie"),
    Note(16, "Informatique")
]

print("Notes des étudiants :")
for note in notes:
    print(f"  {note}")

# Opérations
math = notes[0]
physique = notes[1]

moyenne_sciences = math + physique
print(f"\nMoyenne Math+Physique : {moyenne_sciences}")

# Comparaisons
print(f"Math > Physique : {math > physique}")
print(f"Math == 18 : {math == 18}")
print(f"Informatique > Chimie : {notes[3] > notes[2]}")

# Tri des notes
notes_tries = sorted(notes, key=lambda note: note.valeur, reverse=True)
print(f"\nNotes triées par valeur décroissante :")
for note in notes_tries:
    print(f"  {note}")
```

## 🎯 Défis Supplémentaires

1. **Créez** une classe Complexe avec surcharge des opérateurs arithmétiques
2. **Implémentez** une classe Matrice avec opérations matricielles
3. **Développez** une classe Date avec opérateurs de comparaison
4. **Concevez** une classe Fraction avec opérateurs et simplification

---

**Exercices complétés : 220/230** 🎯

*Continuez avec le [chapitre suivant](5-4-collections.md) pour les collections et sérialisation !*