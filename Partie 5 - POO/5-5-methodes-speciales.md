# Partie 5.5 : Méthodes Spéciales et Concepts Avancés

## 🎯 Objectifs Pédagogiques

Ce chapitre final de la Partie 5 explore les **méthodes spéciales** et les **concepts avancés** de la POO en Python, permettant de créer des objets plus sophistiqués et intégrés au langage.

### Concepts Abordés
- **Méthodes magiques** : __init__, __str__, __eq__, __lt__
- **Itérateurs** : __iter__, __next__
- **Générateurs** : yield, expressions génératrices
- **Applications** : objets itérables, séquences personnalisées

---

## 📝 Exercices Pratiques

### Exercice 226 : Copier un objet avec deepcopy
**Objectif** : Démontrer la copie profonde d'objets complexes.

```python
# Solution
import copy

class Etudiant:
    """Étudiant avec notes et informations"""

    def __init__(self, nom, notes):
        """Constructeur"""
        self.nom = nom
        self.notes = notes  # Liste de notes

    def ajouter_note(self, note):
        """Ajoute une note"""
        self.notes.append(note)

    def moyenne(self):
        """Calcule la moyenne"""
        return sum(self.notes) / len(self.notes) if self.notes else 0

    def __str__(self):
        """Représentation"""
        return f"{self.nom} : {self.notes} (moyenne: {self.moyenne():.2f})"

# Tests
etudiant_original = Etudiant("Alice", [15, 16, 14])

print("Étudiant original :")
print(f"  {etudiant_original}")

# Copie superficielle
etudiant_copie_superf = copy.copy(etudiant_original)
print("
Copie superficielle :")
print(f"  Original : {etudiant_original}")
print(f"  Copie : {etudiant_copie_superf}")

# Modification de la copie superficielle
etudiant_copie_superf.ajouter_note(18)
print("
Après modification de la copie superficielle :")
print(f"  Original : {etudiant_original}")  # Notes partagées !
print(f"  Copie : {etudiant_copie_superf}")

# Réinitialisation
etudiant_original = Etudiant("Alice", [15, 16, 14])

# Copie profonde
etudiant_copie_profonde = copy.deepcopy(etudiant_original)
print("
Copie profonde :")
print(f"  Original : {etudiant_original}")
print(f"  Copie : {etudiant_copie_profonde}")

# Modification de la copie profonde
etudiant_copie_profonde.ajouter_note(19)
print("
Après modification de la copie profonde :")
print(f"  Original : {etudiant_original}")  # Notes indépendantes
print(f"  Copie : {etudiant_copie_profonde}")

# Test avec objets imbriqués
etudiant_avec_contact = Etudiant("Bob", [12, 13, 11])
etudiant_avec_contact.contact = {"email": "bob@email.com", "tel": "01-23-45"}

etudiant_copie_profonde_2 = copy.deepcopy(etudiant_avec_contact)
etudiant_copie_profonde_2.contact["email"] = "bob.nouveau@email.com"

print("
Test avec objet imbriqué :")
print(f"  Original : {etudiant_avec_contact.contact}")
print(f"  Copie : {etudiant_copie_profonde_2.contact}")
```

**Explication** :
- **copy.copy()** : copie superficielle (partage les références)
- **copy.deepcopy()** : copie profonde (copie tout)
- **Imbrication** : objets contenant d'autres objets
- **Indépendance** : modifications sans effet sur l'original

**Test** : Copie superficielle vs profonde.

---

### Exercice 227 : Méthodes statiques et de classe
**Objectif** : Implémenter des méthodes statiques et de classe.

```python
# Solution
class Mathematiques:
    """Classe avec méthodes statiques et de classe"""

    @staticmethod
    def addition(a, b):
        """Addition statique"""
        return a + b

    @staticmethod
    def multiplication(a, b):
        """Multiplication statique"""
        return a * b

    @classmethod
    def depuis_chaine(cls, expression):
        """Crée une instance depuis une chaîne"""
        try:
            a, op, b = expression.split()
            a, b = float(a), float(b)

            if op == "+":
                resultat = cls.addition(a, b)
            elif op == "*":
                resultat = cls.multiplication(a, b)
            else:
                raise ValueError("Opérateur non supporté")

            return cls(resultat)
        except:
            raise ValueError("Format invalide")

    def __init__(self, valeur):
        """Constructeur"""
        self.valeur = valeur

    def __str__(self):
        """Représentation"""
        return f"Math({self.valeur})"

# Tests
print("Tests des méthodes statiques :")
resultat_add = Mathematiques.addition(5, 3)
resultat_mul = Mathematiques.multiplication(4, 7)
print(f"5 + 3 = {resultat_add}")
print(f"4 × 7 = {resultat_mul}")

# Création depuis chaîne
try:
    expr1 = Mathematiques.depuis_chaine("10 + 5")
    expr2 = Mathematiques.depuis_chaine("6 * 7")
    print(f"\nCréé depuis '10 + 5' : {expr1}")
    print(f"Créé depuis '6 * 7' : {expr2}")
except ValueError as e:
    print(f"Erreur : {e}")

# Test d'erreur
try:
    Mathematiques.depuis_chaine("10 - 5")  # Opérateur non supporté
except ValueError as e:
    print(f"Erreur opérateur : {e}")

# Utilisation normale
math_obj = Mathematiques(42)
print(f"\nObjet normal : {math_obj}")
```

**Explanation** :
- **@staticmethod** : méthode sans self/cls
- **@classmethod** : méthode avec cls comme premier paramètre
- **Factory method** : depuis_chaine() crée des instances
- **Utilité** : méthodes utilitaires, constructeurs alternatifs

**Test** : Méthodes statiques et de classe.

---

### Exercice 228 : Classe abstraite simple
**Objectif** : Implémenter une classe abstraite avec méthodes abstraites.

```python
# Solution
from abc import ABC, abstractmethod

class Vehicule(ABC):
    """Classe abstraite pour les véhicules"""

    def __init__(self, marque, modele):
        """Constructeur"""
        self.marque = marque
        self.modele = modele

    @abstractmethod
    def demarrer(self):
        """Méthode abstraite pour démarrer"""
        pass

    @abstractmethod
    def arreter(self):
        """Méthode abstraite pour arrêter"""
        pass

    def info(self):
        """Méthode concrète"""
        return f"{self.marque} {self.modele}"

class Voiture(Vehicule):
    """Voiture concrète"""

    def __init__(self, marque, modele, portes=4):
        """Constructeur"""
        super().__init__(marque, modele)
        self.portes = portes
        self._en_marche = False

    def demarrer(self):
        """Démarre la voiture"""
        if not self._en_marche:
            self._en_marche = True
            return f"La {self.marque} {self.modele} démarre"
        return f"La {self.marque} {self.modele} est déjà démarrée"

    def arreter(self):
        """Arrête la voiture"""
        if self._en_marche:
            self._en_marche = False
            return f"La {self.marque} {self.modele} s'arrête"
        return f"La {self.marque} {self.modele} est déjà arrêtée"

    def info(self):
        """Informations de la voiture"""
        base = super().info()
        return f"{base} ({self.portes} portes)"

class Moto(Vehicule):
    """Moto concrète"""

    def __init__(self, marque, modele, type_moto="sport"):
        """Constructeur"""
        super().__init__(marque, modele)
        self.type_moto = type_moto
        self._en_marche = False

    def demarrer(self):
        """Démarre la moto"""
        if not self._en_marche:
            self._en_marche = True
            return f"La {self.marque} {self.modele} démarre en vrombissant"
        return f"La {self.marque} {self.modele} est déjà démarrée"

    def arreter(self):
        """Arrête la moto"""
        if self._en_marche:
            self._en_marche = False
            return f"La {self.marque} {self.modele} s'arrête"
        return f"La {self.marque} {self.modele} est déjà arrêtée"

    def info(self):
        """Informations de la moto"""
        base = super().info()
        return f"{base} ({self.type_moto})"

# Tests
try:
    # Impossible de créer une instance abstraite
    vehicule = Vehicule("Generic", "Vehicle")  # Erreur
except Exception as e:
    print(f"Erreur classe abstraite : {e}")

# Création d'instances concrètes
voiture = Voiture("Toyota", "Corolla", 5)
moto = Moto("Honda", "CBR", "sport")

vehicules = [voiture, moto]

print("\nTests des véhicules :")
for veh in vehicules:
    print(f"  {veh.info()}")

print("\nTests de démarrage :")
for veh in vehicules:
    print(f"  {veh.demarrer()}")

print("\nTests d'arrêt :")
for veh in vehicules:
    print(f"  {veh.arreter()}")

# Polymorphisme
print("\nPolymorphisme avec liste de véhicules :")
for veh in vehicules:
    print(f"  {veh.demarrer()}")
    print(f"  {veh.arreter()}")
```

**Explication** :
- **ABC** : Abstract Base Class
- **@abstractmethod** : méthodes à implémenter obligatoirement
- **Héritage forcé** : classes filles doivent implémenter
- **Polymorphisme** : comportement uniforme
- **Validation** : impossible d'instancier la classe abstraite

**Test** : Classes concrètes avec méthodes abstraites.

---

### Exercice 229 : Interface et implémentation
**Objectif** : Implémenter une interface avec méthodes abstraites.

```python
# Solution
from abc import ABC, abstractmethod

class InterfaceVolant(ABC):
    """Interface pour les objets volants"""

    @abstractmethod
    def voler(self):
        """Méthode pour voler"""
        pass

    @abstractmethod
    def atterrir(self):
        """Méthode pour atterrir"""
        pass

    @abstractmethod
    def get_altitude(self):
        """Méthode pour obtenir l'altitude"""
        pass

class Avion(InterfaceVolant):
    """Avion implémentant l'interface"""

    def __init__(self, compagnie, modele):
        """Constructeur"""
        self.compagnie = compagnie
        self.modele = modele
        self.altitude = 0
        self.en_vol = False

    def voler(self):
        """Fait voler l'avion"""
        if not self.en_vol:
            self.en_vol = True
            self.altitude = 10000
            return f"L'{self.compagnie} {self.modele} décolle à {self.altitude}m"
        return f"L'{self.compagnie} {self.modele} est déjà en vol"

    def atterrir(self):
        """Fait atterrir l'avion"""
        if self.en_vol:
            self.en_vol = False
            self.altitude = 0
            return f"L'{self.compagnie} {self.modele} atterrit"
        return f"L'{self.compagnie} {self.modele} est déjà au sol"

    def get_altitude(self):
        """Retourne l'altitude"""
        return self.altitude

    def info(self):
        """Informations de l'avion"""
        statut = "En vol" if self.en_vol else "Au sol"
        return f"{self.compagnie} {self.modele} - {statut} à {self.altitude}m"

class Oiseau(InterfaceVolant):
    """Oiseau implémentant l'interface"""

    def __init__(self, espece, nom):
        """Constructeur"""
        self.espece = espece
        self.nom = nom
        self.altitude = 0
        self.en_vol = False

    def voler(self):
        """Fait voler l'oiseau"""
        if not self.en_vol:
            self.en_vol = True
            self.altitude = 50
            return f"{self.nom} le {self.espece} s'envole à {self.altitude}m"
        return f"{self.nom} vole déjà"

    def atterrir(self):
        """Fait atterrir l'oiseau"""
        if self.en_vol:
            self.en_vol = False
            self.altitude = 0
            return f"{self.nom} se pose"
        return f"{self.nom} est déjà posé"

    def get_altitude(self):
        """Retourne l'altitude"""
        return self.altitude

    def info(self):
        """Informations de l'oiseau"""
        statut = "En vol" if self.en_vol else "Au sol"
        return f"{self.nom} le {self.espece} - {statut} à {self.altitude}m"

# Tests
avion = Avion("Air France", "A320")
oiseau = Oiseau("Moineau", "Titi")

volants = [avion, oiseau]

print("Tests d'interface volante :")
for volant in volants:
    print(f"\n--- {type(volant).__name__} ---")
    print(f"Info : {volant.info()}")
    print(f"Vol : {volant.voler()}")
    print(f"Altitude : {volant.get_altitude()}m")
    print(f"Atterrissage : {volant.atterrir()}")

# Test d'erreur d'interface
try:
    # interface = InterfaceVolant()  # Erreur
    pass
except Exception as e:
    print(f"\nErreur interface : {e}")
```

**Explication** :
- **Interface abstraite** : méthodes à implémenter
- **Implémentations différentes** : avion vs oiseau
- **Polymorphisme** : même interface, comportements variés
- **Validation** : altitude, statut de vol

**Test** : Interface polymorphe pour différents types volants.

---

### Exercice 230 : Polymorphisme avec méthode commune
**Objectif** : Démontrer le polymorphisme avec une méthode commune.

```python
# Solution
class Forme:
    """Classe de base pour les formes"""

    def __init__(self, nom):
        """Constructeur"""
        self.nom = nom

    def calculer_aire(self):
        """Méthode polymorphe"""
        return 0

    def calculer_perimetre(self):
        """Méthode polymorphe"""
        return 0

    def info(self):
        """Informations de base"""
        return f"{self.nom}"

class Cercle(Forme):
    """Cercle avec calculs spécifiques"""

    def __init__(self, rayon):
        """Constructeur"""
        super().__init__("Cercle")
        self.rayon = rayon

    def calculer_aire(self):
        """Aire du cercle"""
        import math
        return math.pi * self.rayon**2

    def calculer_perimetre(self):
        """Circonférence du cercle"""
        import math
        return 2 * math.pi * self.rayon

    def info(self):
        """Informations du cercle"""
        base = super().info()
        return f"{base} (rayon={self.rayon})"

class Rectangle(Forme):
    """Rectangle avec calculs spécifiques"""

    def __init__(self, largeur, hauteur):
        """Constructeur"""
        super().__init__("Rectangle")
        self.largeur = largeur
        self.hauteur = hauteur

    def calculer_aire(self):
        """Aire du rectangle"""
        return self.largeur * self.hauteur

    def calculer_perimetre(self):
        """Périmètre du rectangle"""
        return 2 * (self.largeur + self.hauteur)

    def info(self):
        """Informations du rectangle"""
        base = super().info()
        return f"{base} ({self.largeur}×{self.hauteur})"

class Triangle(Forme):
    """Triangle avec calculs spécifiques"""

    def __init__(self, base, hauteur, a, b, c):
        """Constructeur"""
        super().__init__("Triangle")
        self.base = base
        self.hauteur = hauteur
        self.cote_a = a
        self.cote_b = b
        self.cote_c = c

    def calculer_aire(self):
        """Aire du triangle"""
        return (self.base * self.hauteur) / 2

    def calculer_perimetre(self):
        """Périmètre du triangle"""
        return self.cote_a + self.cote_b + self.cote_c

    def info(self):
        """Informations du triangle"""
        base = super().info()
        return f"{base} (base={self.base}, hauteur={self.hauteur})"

# Tests polymorphisme
formes = [
    Cercle(5),
    Rectangle(4, 6),
    Triangle(6, 4, 3, 4, 5)
]

print("Tests de polymorphisme avec formes :")
for forme in formes:
    print(f"\n--- {type(forme).__name__} ---")
    print(f"Info : {forme.info()}")
    print(f"Aire : {forme.calculer_aire():.2f}")
    print(f"Périmètre : {forme.calculer_perimetre():.2f}")

# Fonction polymorphe
def analyser_formes(formes):
    """Analyse une liste de formes"""
    total_aire = 0
    total_perimetre = 0

    for forme in formes:
        total_aire += forme.calculer_aire()
        total_perimetre += forme.calculer_perimetre()

    return {
        "nombre_formes": len(formes),
        "aire_totale": total_aire,
        "perimetre_total": total_perimetre,
        "aire_moyenne": total_aire / len(formes),
        "perimetre_moyen": total_perimetre / len(formes)
    }

analyse = analyser_formes(formes)
print("
Analyse des formes :")
for cle, valeur in analyse.items():
    if "moyen" in cle:
        print(f"  {cle}: {valeur:.2f}")
    else:
        print(f"  {cle}: {valeur}")
```

**Explication** :
- **Polymorphisme** : même méthode, calculs différents
- **Héritage** : classes filles spécialisées
- **Méthodes surchargées** : calculer_aire(), calculer_perimetre()
- **Fonction générique** : traitement uniforme des formes

**Test** : Calculs polymorphes pour différentes formes.

---

## 🔍 Points Clés à Retenir

### 1. **Méthodes Spéciales**
```python
class MonObjet:
    def __init__(self, valeur):      # Constructeur
        self.valeur = valeur

    def __str__(self):               # str(objet)
        return f"Objet({self.valeur})"

    def __repr__(self):              # repr(objet)
        return f"MonObjet({self.valeur!r})"

    def __eq__(self, other):         # objet == other
        return isinstance(other, MonObjet) and self.valeur == other.valeur

    def __lt__(self, other):         # objet < other
        return self.valeur < other.valeur

    def __add__(self, other):        # objet + other
        return MonObjet(self.valeur + other.valeur)
```

### 2. **Classes Abstraites**
```python
from abc import ABC, abstractmethod

class ClasseAbstraite(ABC):
    @abstractmethod
    def methode_abstraite(self):
        """Méthode à implémenter obligatoirement"""
        pass

    def methode_concrete(self):
        """Méthode avec implémentation par défaut"""
        return "Implémentation par défaut"

class ClasseConcrete(ClasseAbstraite):
    def methode_abstraite(self):
        return "Implémentation concrète"
```

### 3. **Méthodes Statiques et de Classe**
```python
class MaClasse:
    @staticmethod
    def methode_statique(x, y):     # Pas de self/cls
        return x + y

    @classmethod
    def methode_de_classe(cls, x):  # cls = classe
        return cls(x * 2)  # Peut créer des instances

    def __init__(self, valeur):
        self.valeur = valeur

# Utilisation
resultat = MaClasse.methode_statique(5, 3)  # 8
instance = MaClasse.methode_de_classe(5)    # MaClasse(10)
```

### 4. **Itérateurs et Générateurs**
```python
class MonIterateur:
    def __init__(self, max_val):
        self.max_val = max_val
        self.current = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.current >= self.max_val:
            raise StopIteration
        resultat = self.current
        self.current += 1
        return resultat

# Générateur (plus simple)
def mon_generateur(max_val):
    current = 0
    while current < max_val:
        yield current
        current += 1

# Utilisation
for i in MonIterateur(5):
    print(i)  # 0, 1, 2, 3, 4

for i in mon_generateur(5):
    print(i)  # 0, 1, 2, 3, 4
```

## 💡 Optimisations et Astuces

### 1. **Context Managers**
```python
class MonContextManager:
    def __enter__(self):
        print("Entrée dans le contexte")
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Sortie du contexte")
        return False  # Ne pas supprimer les exceptions

# Utilisation
with MonContextManager() as cm:
    print("Dans le contexte")
    # Sort automatiquement à la fin
```

### 2. **Propriétés avec Validation**
```python
class Temperature:
    def __init__(self, celsius):
        self.celsius = celsius

    @property
    def celsius(self):
        return self._celsius

    @celsius.setter
    def celsius(self, valeur):
        if -273.15 <= valeur <= 1000:  # Plage physique réaliste
            self._celsius = valeur
        else:
            raise ValueError("Température invalide")

    @property
    def fahrenheit(self):
        return (self._celsius * 9/5) + 32

    @fahrenheit.setter
    def fahrenheit(self, valeur):
        self.celsius = (valeur - 32) * 5/9

# Test
temp = Temperature(25)
print(f"Celsius: {temp.celsius}°C")
print(f"Fahrenheit: {temp.fahrenheit}°F")

temp.fahrenheit = 77
print(f"Nouvelle température: {temp.celsius}°C")
```

### 3. **Singletons et Patterns**
```python
class Singleton:
    _instance = None

    def __new__(cls, *args, **kwargs):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance

# Test
s1 = Singleton()
s2 = Singleton()
print(s1 is s2)  # True - même instance
```

## 🚀 Applications Pratiques

### 1. **Système de Logging Personnalisé**
```python
import logging
from datetime import datetime

class LoggerPerso:
    """Logger personnalisé avec méthodes spéciales"""

    def __init__(self, nom_fichier="app.log"):
        self.nom_fichier = nom_fichier
        self.niveau = logging.INFO

    def __enter__(self):
        """Context manager pour logging"""
        logging.basicConfig(
            filename=self.nom_fichier,
            level=self.niveau,
            format='%(asctime)s - %(levelname)s - %(message)s'
        )
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        """Fermeture du logger"""
        logging.shutdown()

    def log(self, message, niveau=logging.INFO):
        """Méthode de logging"""
        logger = logging.getLogger()
        if niveau >= self.niveau:
            logger.log(niveau, message)

    def info(self, message):
        """Info logging"""
        self.log(message, logging.INFO)

    def warning(self, message):
        """Warning logging"""
        self.log(message, logging.WARNING)

    def error(self, message):
        """Error logging"""
        self.log(message, logging.ERROR)

# Test
with LoggerPerso("mon_app.log") as logger:
    logger.info("Application démarrée")
    logger.warning("Configuration incomplète")
    logger.error("Erreur de connexion")

    # Code de l'application
    print("Application en cours d'exécution...")

print("Logs sauvegardés dans mon_app.log")
```

### 2. **Générateur de Séquence Personnalisé**
```python
class GenerateurFibonacci:
    """Générateur de nombres de Fibonacci"""

    def __init__(self, max_termes):
        self.max_termes = max_termes
        self.current = 0
        self.a, self.b = 0, 1

    def __iter__(self):
        """Retourne l'itérateur"""
        return self

    def __next__(self):
        """Génère le prochain terme"""
        if self.current >= self.max_termes:
            raise StopIteration

        if self.current == 0:
            self.current += 1
            return 0
        elif self.current == 1:
            self.current += 1
            return 1
        else:
            # Génère le prochain terme de Fibonacci
            prochain = self.a + self.b
            self.a, self.b = self.b, prochain
            self.current += 1
            return prochain

# Test
fib_gen = GenerateurFibonacci(10)
print("Nombres de Fibonacci :")
for nombre in fib_gen:
    print(nombre, end=" ")

# Réinitialisation et nouveau parcours
fib_gen = GenerateurFibonacci(8)
print(f"\nSomme des 8 premiers : {sum(fib_gen)}")
```

### 3. **Système de Cache Intelligent**
```python
from functools import lru_cache
import time

class CacheManager:
    """Gestionnaire de cache avec méthodes spéciales"""

    def __init__(self, max_size=128):
        self.cache = {}
        self.max_size = max_size
        self.access_count = {}

    def __getitem__(self, key):
        """Accès comme un dictionnaire"""
        if key in self.cache:
            self.access_count[key] = self.access_count.get(key, 0) + 1
            return self.cache[key]
        raise KeyError(f"Clé '{key}' non trouvée")

    def __setitem__(self, key, value):
        """Affectation comme un dictionnaire"""
        # Si cache plein, supprimer le moins utilisé
        if len(self.cache) >= self.max_size and key not in self.cache:
            # Trouver le moins accédé
            moins_utilise = min(self.access_count, key=self.access_count.get)
            del self.cache[moins_utilise]
            del self.access_count[moins_utilise]

        self.cache[key] = value
        self.access_count[key] = self.access_count.get(key, 0) + 1

    def __contains__(self, key):
        """Test d'appartenance"""
        return key in self.cache

    def __len__(self):
        """Longueur du cache"""
        return len(self.cache)

    def clear(self):
        """Vide le cache"""
        self.cache.clear()
        self.access_count.clear()

    def stats(self):
        """Statistiques du cache"""
        return {
            "taille": len(self.cache),
            "max_size": self.max_size,
            "utilisation": len(self.cache) / self.max_size * 100,
            "access_count": self.access_count.copy()
        }

# Test
cache = CacheManager(max_size=3)

# Ajout d'éléments
cache["utilisateur_1"] = {"nom": "Alice", "age": 25}
cache["utilisateur_2"] = {"nom": "Bob", "age": 30}
cache["utilisateur_3"] = {"nom": "Charlie", "age": 35}

print("Cache initial :")
print(f"  Taille : {len(cache)}")
print(f"  Contenu : {cache.cache}")

# Accès
alice = cache["utilisateur_1"]
print(f"\nAccès à utilisateur_1 : {alice}")

# Ajout d'un quatrième (devrait évincer un élément)
cache["utilisateur_4"] = {"nom": "Diana", "age": 28}
print("
Après ajout du 4ème :")
print(f"  Taille : {len(cache)}")
print(f"  Contenu : {cache.cache}")

# Stats
stats = cache.stats()
print(f"\nStatistiques : {stats}")
```

## 🎯 Bilan de la Partie 5

### Concepts Maîtrisés
✅ **Classes et objets** : création, attributs, méthodes
✅ **Héritage** : classes filles, surcharge de méthodes
✅ **Polymorphisme** : méthodes communes, comportement différent
✅ **Encapsulation** : attributs privés, getters/setters
✅ **Surcharge d'opérateurs** : +, ==, <, etc.
✅ **Collections** : namedtuple, piles, files, matrices
✅ **Sérialisation** : JSON, pickle, deepcopy
✅ **Méthodes spéciales** : __str__, __eq__, __iter__

### Compétences Développées
- **Modélisation** : conception de classes et hiérarchies
- **Abstraction** : interfaces et classes abstraites
- **Réutilisabilité** : héritage et polymorphisme
- **Robustesse** : encapsulation et validation
- **Intégration** : surcharge d'opérateurs et méthodes spéciales

---

**🏁 FIN DE LA PARTIE 5 - BRAVO !**

**Exercices complétés : 230/230** 🎯

*Félicitations ! Vous avez terminé la programmation orientée objet. Continuez avec la [Partie 6](Partie%206%20-%20Fichiers/6-1-fichiers-texte.md) pour la gestion de fichiers !*
