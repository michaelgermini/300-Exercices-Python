# Partie 5.1 : Classes et Objets

## 🎯 Objectifs Pédagogiques

Ce chapitre introduit la **programmation orientée objet (POO)** en Python. Nous allons explorer les concepts fondamentaux de **classes** et **objets**, qui permettent de modéliser le monde réel dans le code.

### Concepts Abordés
- **Classes et objets** : création, instanciation, attributs
- **Méthodes** : fonctions appartenant aux objets
- **Constructeur __init__** : initialisation des objets
- **Applications** : modélisation de concepts du monde réel

---

## 📝 Exercices Pratiques

### Exercice 201 : Créer une classe Personne avec nom et âge
**Objectif** : Créer une classe simple avec des attributs de base.

```python
# Solution
class Personne:
    """Classe représentant une personne avec nom et âge"""

    def __init__(self, nom, age):
        """Constructeur de la classe Personne"""
        self.nom = nom
        self.age = age

# Création d'objets
personne1 = Personne("Alice", 25)
personne2 = Personne("Bob", 30)
personne3 = Personne("Charlie", 35)

print(f"Personne 1 : {personne1.nom}, {personne1.age} ans")
print(f"Personne 2 : {personne2.nom}, {personne2.age} ans")
print(f"Personne 3 : {personne3.nom}, {personne3.age} ans")

# Accès aux attributs
print(f"Nom de personne1 : {personne1.nom}")
print(f"Âge de personne2 : {personne2.age}")

# Modification d'attributs
personne1.age = 26
print(f"Après modification : {personne1.nom} a {personne1.age} ans")

# Liste de personnes
personnes = [personne1, personne2, personne3]
for personne in personnes:
    print(f"- {personne.nom} ({personne.age} ans)")
```

**Explication** :
- **class** : définition d'une classe
- **__init__** : constructeur (méthode d'initialisation)
- **self** : référence à l'objet lui-même
- **Attributs** : variables appartenant à l'objet
- **Instances** : objets créés à partir de la classe

**Test** : Création et manipulation de 3 personnes.

---

### Exercice 202 : Ajouter une méthode pour présenter la personne
**Objectif** : Ajouter une méthode pour afficher une présentation.

```python
# Solution
class Personne:
    """Classe Personne avec méthode de présentation"""

    def __init__(self, nom, age, profession="Non spécifiée"):
        """Constructeur avec profession optionnelle"""
        self.nom = nom
        self.age = age
        self.profession = profession

    def se_presenter(self):
        """Méthode pour se présenter"""
        return f"Bonjour, je m'appelle {self.nom}, j'ai {self.age} ans et je suis {self.profession}"

    def est_majeur(self):
        """Méthode pour vérifier la majorité"""
        return self.age >= 18

# Création d'objets
alice = Personne("Alice", 25, "Développeuse")
bob = Personne("Bob", 30, "Designer")
charlie = Personne("Charlie", 16)  # Sans profession

# Tests des méthodes
print("Présentations :")
print(alice.se_presenter())
print(bob.se_presenter())
print(charlie.se_presenter())

print("\nTests de majorité :")
print(f"Alice est majeure : {alice.est_majeur()}")
print(f"Bob est majeur : {bob.est_majeur()}")
print(f"Charlie est majeur : {charlie.est_majeur()}")

# Utilisation avec différents types
personnes = [
    Personne("Diana", 22, "Étudiante"),
    Personne("Eve", 17, "Lycéenne"),
    Personne("Frank", 45, "Manager")
]

print("\nListe de personnes :")
for personne in personnes:
    print(f"{personne.se_presenter()} - Majeur: {personne.est_majeur()}")
```

**Explication** :
- **Méthodes** : fonctions appartenant à la classe
- **self** : accès aux attributs de l'objet
- **Paramètres optionnels** : profession="Non spécifiée"
- **Types de retour** : chaînes, booléens
- **Applications** : interaction, validation

**Test** : Présentations et tests de majorité.

---

### Exercice 203 : Créer une classe CompteBancaire avec dépôt et retrait
**Objectif** : Modéliser un compte bancaire avec opérations.

```python
# Solution
class CompteBancaire:
    """Classe représentant un compte bancaire"""

    def __init__(self, titulaire, solde_initial=0):
        """Constructeur avec titulaire et solde initial"""
        self.titulaire = titulaire
        self.solde = solde_initial

    def deposer(self, montant):
        """Méthode pour déposer de l'argent"""
        if montant > 0:
            self.solde += montant
            return f"Dépôt de {montant}€ effectué. Nouveau solde : {self.solde}€"
        else:
            return "Montant invalide pour le dépôt"

    def retirer(self, montant):
        """Méthode pour retirer de l'argent"""
        if montant > 0:
            if self.solde >= montant:
                self.solde -= montant
                return f"Retrait de {montant}€ effectué. Nouveau solde : {self.solde}€"
            else:
                return f"Fonds insuffisants. Solde actuel : {self.solde}€"
        else:
            return "Montant invalide pour le retrait"

    def afficher_solde(self):
        """Méthode pour afficher le solde"""
        return f"Solde du compte de {self.titulaire} : {self.solde}€"

# Tests
compte_alice = CompteBancaire("Alice", 1000)
print(compte_alice.afficher_solde())

print(compte_alice.deposer(500))
print(compte_alice.retirer(200))
print(compte_alice.retirer(2000))  # Fonds insuffisants

# Compte avec solde initial
compte_bob = CompteBancaire("Bob", 500)
print(f"\n{compte_bob.afficher_solde()}")

# Opérations multiples
operations = [100, -50, 200, -75, 25]
print("Opérations sur le compte de Bob :")
for operation in operations:
    if operation > 0:
        print(compte_bob.deposer(operation))
    else:
        print(compte_bob.retirer(abs(operation)))

print(compte_bob.afficher_solde())
```

**Explication** :
- **Encapsulation** : données et méthodes ensemble
- **Validation** : contrôles des montants
- **État** : solde modifié par les opérations
- **Messages** : retours informatifs
- **Applications** : simulation bancaire

**Test** : Dépôts, retraits, et vérification du solde.

---

### Exercice 204 : Créer une classe Voiture avec marque et vitesse
**Objectif** : Modéliser une voiture avec ses caractéristiques.

```python
# Solution
class Voiture:
    """Classe représentant une voiture"""

    def __init__(self, marque, modele, annee, vitesse_max=0):
        """Constructeur de la classe Voiture"""
        self.marque = marque
        self.modele = modele
        self.annee = annee
        self.vitesse_max = vitesse_max
        self.vitesse_actuelle = 0

    def accelerer(self, acceleration):
        """Méthode pour accélérer"""
        if acceleration > 0:
            if self.vitesse_actuelle + acceleration <= self.vitesse_max:
                self.vitesse_actuelle += acceleration
                return f"Accélération de {acceleration} km/h. Vitesse : {self.vitesse_actuelle} km/h"
            else:
                self.vitesse_actuelle = self.vitesse_max
                return f"Vitesse maximale atteinte : {self.vitesse_max} km/h"
        else:
            return "Accélération doit être positive"

    def freiner(self, deceleration):
        """Méthode pour freiner"""
        if deceleration > 0:
            if self.vitesse_actuelle - deceleration >= 0:
                self.vitesse_actuelle -= deceleration
                return f"Freinage de {deceleration} km/h. Vitesse : {self.vitesse_actuelle} km/h"
            else:
                self.vitesse_actuelle = 0
                return "Arrêt complet"
        else:
            return "Décélération doit être positive"

    def afficher_info(self):
        """Méthode pour afficher les informations"""
        return f"{self.marque} {self.modele} ({self.annee}) - Vitesse max: {self.vitesse_max} km/h, Actuelle: {self.vitesse_actuelle} km/h"

# Tests
voiture1 = Voiture("Toyota", "Corolla", 2020, 180)
voiture2 = Voiture("Ferrari", "488", 2022, 330)

print("Informations des voitures :")
print(voiture1.afficher_info())
print(voiture2.afficher_info())

print("\nTests d'accélération :")
print(voiture1.accelerer(50))
print(voiture1.accelerer(100))
print(voiture1.accelerer(50))  # Vitesse max atteinte

print(f"\n{voiture2.accelerer(100)}")
print(f"{voiture2.accelerer(150)}")
print(f"{voiture2.accelerer(100)}")  # Vitesse max

print("\nTests de freinage :")
print(voiture1.freiner(30))
print(voiture1.freiner(120))  # Arrêt complet
print(voiture2.freiner(200))  # Arrêt complet
```

**Explication** :
- **Attributs multiples** : marque, modèle, année, vitesses
- **Méthodes d'action** : accélérer, freiner
- **Validation** : limites de vitesse
- **État dynamique** : vitesse actuelle changeante
- **Applications** : simulation, jeux

**Test** : Accélérations et freinages de voitures.

---

### Exercice 205 : Ajouter méthode pour accélérer une voiture
**Objectif** : Étendre la classe Voiture avec des méthodes d'accélération.

```python
# Solution
class Voiture:
    """Classe Voiture avec méthodes d'accélération étendues"""

    def __init__(self, marque, modele, annee, vitesse_max=0):
        """Constructeur"""
        self.marque = marque
        self.modele = modele
        self.annee = annee
        self.vitesse_max = vitesse_max
        self.vitesse_actuelle = 0
        self.kilometrage = 0

    def accelerer(self, acceleration):
        """Accélération simple"""
        if acceleration > 0:
            if self.vitesse_actuelle + acceleration <= self.vitesse_max:
                self.vitesse_actuelle += acceleration
                return f"Accélération de {acceleration} km/h. Vitesse : {self.vitesse_actuelle} km/h"
            else:
                self.vitesse_actuelle = self.vitesse_max
                return f"Vitesse maximale atteinte : {self.vitesse_max} km/h"
        return "Accélération invalide"

    def accelerer_progressif(self, acceleration, duree):
        """Accélération progressive sur une durée"""
        if acceleration > 0 and duree > 0:
            # Simulation : accélération linéaire
            acceleration_reelle = min(acceleration, self.vitesse_max - self.vitesse_actuelle)
            self.vitesse_actuelle += acceleration_reelle
            self.kilometrage += (self.vitesse_actuelle * duree) / 60  # km parcourus
            return f"Accélération progressive : +{acceleration_reelle} km/h en {duree} min. Vitesse : {self.vitesse_actuelle} km/h, Km : {self.kilometrage:.1f}"
        return "Paramètres invalides"

    def freiner(self, deceleration):
        """Freinage"""
        if deceleration > 0:
            if self.vitesse_actuelle - deceleration >= 0:
                self.vitesse_actuelle -= deceleration
                return f"Freinage de {deceleration} km/h. Vitesse : {self.vitesse_actuelle} km/h"
            else:
                self.vitesse_actuelle = 0
                return "Arrêt complet"
        return "Décélération invalide"

    def afficher_info(self):
        """Informations complètes"""
        return f"{self.marque} {self.modele} ({self.annee}) - V max: {self.vitesse_max}, V actuelle: {self.vitesse_actuelle}, Km: {self.kilometrage:.1f}"

# Tests
sportive = Voiture("Porsche", "911", 2023, 300)
familiale = Voiture("Renault", "Scenic", 2021, 190)

print("Tests d'accélération étendus :")
print(f"\n{sportive.afficher_info()}")
print(sportive.accelerer(100))
print(sportive.accelerer_progressif(50, 5))  # +50 km/h en 5 min
print(sportive.accelerer_progressif(100, 3))  # Vitesse max
print(sportive.freiner(150))  # Arrêt
print(sportive.accelerer_progressif(100, 10))  # Nouveau départ

print(f"\n{familiale.afficher_info()}")
print(familiale.accelerer(60))
print(familiale.accelerer_progressif(40, 8))
print(familiale.freiner(80))
print(familiale.accelerer_progressif(30, 15))
```

**Explication** :
- **Méthodes étendues** : accélération progressive
- **Calculs** : vitesse et distance
- **Temps** : durée en minutes
- **Kilométrage** : suivi des distances parcourues
- **Applications** : simulation réaliste

**Test** : Accélérations progressives avec calculs de distance.

---

## 🔍 Points Clés à Retenir

### 1. **Syntaxe de Classe**
```python
class NomClasse:
    """Docstring de la classe"""

    def __init__(self, parametres):
        """Constructeur - appelé à la création"""
        self.attribut = valeur  # Attribut d'instance

    def methode(self, parametres):
        """Méthode de la classe"""
        # Code de la méthode
        return resultat
```

### 2. **Instanciation et Attributs**
```python
# Création d'objet
objet = NomClasse(parametres)

# Attributs d'instance
objet.attribut = valeur
objet.nouvel_attribut = valeur

# Attributs de classe (partagés)
class MaClasse:
    attribut_classe = "valeur"

# Accès
MaClasse.attribut_classe  # Accès via la classe
objet.attribut_classe     # Accès via l'instance
```

### 3. **Méthodes Spéciales**
```python
class MaClasse:
    def __init__(self, valeur):     # Constructeur
        self.valeur = valeur

    def __str__(self):              # Représentation chaîne
        return f"MaClasse({self.valeur})"

    def __repr__(self):             # Représentation Python
        return f"MaClasse({self.valeur!r})"

    def __eq__(self, other):        # Égalité
        return isinstance(other, MaClasse) and self.valeur == other.valeur

# Utilisation
obj = MaClasse(42)
print(obj)       # MaClasse(42)
print(repr(obj)) # MaClasse(42)
```

### 4. **Encapsulation**
```python
class Compte:
    def __init__(self, solde):
        self._solde = solde      # Convention : privé (un underscore)

    @property
    def solde(self):             # Getter
        return self._solde

    @solde.setter
    def solde(self, valeur):     # Setter
        if valeur >= 0:
            self._solde = valeur
```

## 💡 Optimisations et Astuces

### 1. **Attributs par Défaut**
```python
class Produit:
    def __init__(self, nom, prix, quantite=0, actif=True):
        self.nom = nom
        self.prix = prix
        self.quantite = quantite
        self.actif = actif

# Utilisation
produit1 = Produit("Ordinateur", 800)           # quantite=0, actif=True
produit2 = Produit("Souris", 25, 100, False)     # Tous les paramètres
```

### 2. **Validation dans le Constructeur**
```python
class Etudiant:
    def __init__(self, nom, age, note):
        self.nom = nom
        if 0 <= age <= 100:
            self.age = age
        else:
            raise ValueError("Age invalide")

        if 0 <= note <= 20:
            self.note = note
        else:
            raise ValueError("Note invalide")

# Test
try:
    etudiant = Etudiant("Alice", 25, 15)
    print(f"Étudiant créé : {etudiant.nom}, {etudiant.age} ans, note: {etudiant.note}")
except ValueError as e:
    print(f"Erreur : {e}")
```

### 3. **Méthodes Statiques et de Classe**
```python
class Mathematiques:
    @staticmethod
    def addition(a, b):          # Pas de self
        return a + b

    @classmethod
    def depuis_chaine(cls, chaine):  # cls = classe
        a, b = map(int, chaine.split(","))
        return cls(a, b)  # Création d'instance

# Utilisation
resultat = Mathematiques.addition(5, 3)  # 8
instance = Mathematiques.depuis_chaine("10,20")
```

## 🚀 Applications Pratiques

### 1. **Gestion de Bibliothèque**
```python
class Livre:
    """Représente un livre dans une bibliothèque"""
    def __init__(self, titre, auteur, annee, disponible=True):
        self.titre = titre
        self.auteur = auteur
        self.annee = annee
        self.disponible = disponible

    def emprunter(self):
        """Emprunte le livre"""
        if self.disponible:
            self.disponible = False
            return f"Livre '{self.titre}' emprunté"
        return f"Livre '{self.titre}' non disponible"

    def rendre(self):
        """Rend le livre"""
        if not self.disponible:
            self.disponible = True
            return f"Livre '{self.titre}' rendu"
        return f"Livre '{self.titre}' déjà disponible"

    def info(self):
        """Informations du livre"""
        statut = "Disponible" if self.disponible else "Emprunté"
        return f"{self.titre} ({self.auteur}, {self.annee}) - {statut}"

# Test
bibliotheque = [
    Livre("1984", "George Orwell", 1949),
    Livre("Python Crash Course", "Eric Matthes", 2019),
    Livre("Le Petit Prince", "Antoine de Saint-Exupéry", 1943)
]

print("Bibliothèque :")
for livre in bibliotheque:
    print(f"  {livre.info()}")

print("\nOpérations :")
print(bibliotheque[0].emprunter())
print(bibliotheque[0].emprunter())  # Déjà emprunté
print(bibliotheque[1].emprunter())
print(bibliotheque[0].rendre())
print(bibliotheque[0].emprunter())  # Maintenant disponible
```

### 2. **Système de Notes Étudiantes**
```python
class Etudiant:
    """Représente un étudiant avec ses notes"""
    def __init__(self, nom, prenom, numero_etudiant):
        self.nom = nom
        self.prenom = prenom
        self.numero = numero_etudiant
        self.notes = []

    def ajouter_note(self, matiere, note):
        """Ajoute une note pour une matière"""
        if 0 <= note <= 20:
            self.notes.append({"matiere": matiere, "note": note})
            return f"Note ajoutée : {matiere} = {note}/20"
        return "Note invalide (0-20)"

    def calculer_moyenne(self):
        """Calcule la moyenne des notes"""
        if not self.notes:
            return 0
        total = sum(note["note"] for note in self.notes)
        return total / len(self.notes)

    def mention(self):
        """Détermine la mention selon la moyenne"""
        moyenne = self.calculer_moyenne()
        if moyenne >= 16:
            return "Très bien"
        elif moyenne >= 14:
            return "Bien"
        elif moyenne >= 12:
            return "Assez bien"
        elif moyenne >= 10:
            return "Passable"
        else:
            return "Insuffisant"

    def bulletin(self):
        """Affiche le bulletin complet"""
        print(f"\n=== BULLETIN DE {self.prenom} {self.nom.upper()} ===")
        print(f"Numéro étudiant : {self.numero}")
        print(f"Nombre de matières : {len(self.notes)}")
        print(f"Moyenne : {self.calculer_moyenne():.2f}/20")
        print(f"Mention : {self.mention()}")
        print("\nDétail des notes :")
        for note in self.notes:
            print(f"  {note['matiere']}: {note['note']}/20")
        print("=" * 50)

# Test
etudiants = [
    Etudiant("Dupont", "Alice", "ETU001"),
    Etudiant("Martin", "Bob", "ETU002"),
    Etudiant("Garcia", "Clara", "ETU003")
]

# Ajout de notes
etudiants[0].ajouter_note("Mathématiques", 18)
etudiants[0].ajouter_note("Physique", 16)
etudiants[0].ajouter_note("Informatique", 19)

etudiants[1].ajouter_note("Mathématiques", 12)
etudiants[1].ajouter_note("Physique", 14)
etudiants[1].ajouter_note("Informatique", 13)

etudiants[2].ajouter_note("Mathématiques", 15)
etudiants[2].ajouter_note("Physique", 17)
etudiants[2].ajouter_note("Informatique", 16)

# Affichage des bulletins
for etudiant in etudiants:
    etudiant.bulletin()
```

### 3. **Gestion de Stock**
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

class Magasin:
    """Représente un magasin avec plusieurs produits"""
    def __init__(self, nom):
        self.nom = nom
        self.produits = []

    def ajouter_produit(self, produit):
        """Ajoute un produit au magasin"""
        self.produits.append(produit)
        return f"Produit {produit.nom} ajouté au magasin {self.nom}"

    def valeur_totale_stock(self):
        """Calcule la valeur totale du stock"""
        return sum(produit.valeur_stock() for produit in self.produits)

    def produits_en_rupture(self):
        """Liste les produits en rupture"""
        return [produit for produit in self.produits if produit.quantite == 0]

    def inventaire(self):
        """Affiche l'inventaire complet"""
        print(f"\n=== INVENTAIRE {self.nom.upper()} ===")
        print(f"Valeur totale stock : {self.valeur_totale_stock():.2f}€")
        print(f"Produits en rupture : {len(self.produits_en_rupture())}")
        print("\nDétail des produits :")
        for produit in self.produits:
            print(f"  {produit.info()}")
        print("=" * 40)

# Test
magasin = Magasin("TechStore")
produits = [
    ProduitStock("Ordinateur", 800, 10),
    ProduitStock("Souris", 25, 50),
    ProduitStock("Clavier", 45, 30),
    ProduitStock("Écran", 200, 0),  # Rupture
    ProduitStock("Imprimante", 150, 5)
]

for produit in produits:
    magasin.ajouter_produit(produit)

# Opérations
print(magasin.produits[0].vendre(2))
print(magasin.produits[1].restocker(20))
print(magasin.produits[3].restocker(10))

magasin.inventaire()
```

## 🎯 Défis Supplémentaires

1. **Créez** une classe Rectangle avec calcul d'aire et périmètre
2. **Implémentez** une classe Cercle avec calcul de surface et circonférence
3. **Développez** une classe Animal avec des méthodes de base
4. **Concevez** une classe Compte avec historique des opérations

---

**Exercices complétés : 205/230** 🎯

*Continuez avec le [chapitre suivant](5-2-heritage.md) pour explorer l'héritage !*