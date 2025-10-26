# Partie 5.4 : Collections et Sérialisation

## 🎯 Objectifs Pédagogiques

Ce chapitre final de la Partie 5 explore les **collections avancées** et la **sérialisation** en Python, concepts pour la **gestion de données complexes** et la **persistance d'objets**.

### Concepts Abordés
- **Collections.namedtuple** : tuples avec noms d'attributs
- **Structures de données** : piles, files, matrices
- **Sérialisation** : JSON, pickle, deepcopy
- **Applications** : stockage, transmission, duplication

---

## 📝 Exercices Pratiques

### Exercice 221 : Classe Stack avec push et pop
**Objectif** : Implémenter une pile (stack) avec les opérations de base.

```python
# Solution
class Stack:
    """Pile (LIFO - Last In, First Out)"""

    def __init__(self, max_size=None):
        """Constructeur avec taille maximale optionnelle"""
        self.items = []
        self.max_size = max_size

    def push(self, item):
        """Ajoute un élément au sommet de la pile"""
        if self.max_size is None or len(self.items) < self.max_size:
            self.items.append(item)
            return f"Élément '{item}' ajouté à la pile"
        return "Pile pleine"

    def pop(self):
        """Retire et retourne l'élément du sommet"""
        if not self.is_empty():
            return self.items.pop()
        return "Pile vide"

    def peek(self):
        """Regarde l'élément du sommet sans le retirer"""
        if not self.is_empty():
            return self.items[-1]
        return "Pile vide"

    def is_empty(self):
        """Vérifie si la pile est vide"""
        return len(self.items) == 0

    def size(self):
        """Retourne la taille de la pile"""
        return len(self.items)

    def __str__(self):
        """Représentation de la pile"""
        return f"Pile: {self.items}"

    def __len__(self):
        """Longueur de la pile"""
        return len(self.items)

# Tests
pile = Stack(max_size=5)

print("Tests de la pile :")
print(pile.push("Livre 1"))
print(pile.push("Livre 2"))
print(pile.push("Livre 3"))

print(f"Pile : {pile}")
print(f"Taille : {pile.size()}")
print(f"Sommet : {pile.peek()}")

print(f"Pop : {pile.pop()}")
print(f"Pile après pop : {pile}")

# Remplissage de la pile
print(pile.push("Livre 4"))
print(pile.push("Livre 5"))

print(f"Pile pleine : {pile}")
print(pile.push("Livre 6"))  # Pile pleine

# Vidage de la pile
print("\nVidage de la pile :")
while not pile.is_empty():
    print(f"Pop : {pile.pop()}")

print(f"Pile finale : {pile}")
print(f"Pop pile vide : {pile.pop()}")
```

**Explication** :
- **LIFO** : Last In, First Out
- **push()** : ajout au sommet (append)
- **pop()** : retrait du sommet
- **peek()** : consultation sans retrait
- **Taille max** : limitation optionnelle

**Test** : Opérations de pile avec gestion des limites.

---

### Exercice 222 : Classe Queue avec enqueue et dequeue
**Objectif** : Implémenter une file (queue) avec les opérations de base.

```python
# Solution
class Queue:
    """File (FIFO - First In, First Out)"""

    def __init__(self, max_size=None):
        """Constructeur"""
        self.items = []
        self.max_size = max_size

    def enqueue(self, item):
        """Ajoute un élément à la fin de la file"""
        if self.max_size is None or len(self.items) < self.max_size:
            self.items.append(item)
            return f"Élément '{item}' ajouté à la file"
        return "File pleine"

    def dequeue(self):
        """Retire et retourne le premier élément"""
        if not self.is_empty():
            return self.items.pop(0)
        return "File vide"

    def front(self):
        """Regarde le premier élément sans le retirer"""
        if not self.is_empty():
            return self.items[0]
        return "File vide"

    def rear(self):
        """Regarde le dernier élément"""
        if not self.is_empty():
            return self.items[-1]
        return "File vide"

    def is_empty(self):
        """Vérifie si la file est vide"""
        return len(self.items) == 0

    def size(self):
        """Retourne la taille de la file"""
        return len(self.items)

    def __str__(self):
        """Représentation de la file"""
        return f"File: {self.items}"

# Tests
file_attente = Queue(max_size=4)

print("Tests de la file d'attente :")
operations = [
    ("Alice", "enqueue"),
    ("Bob", "enqueue"),
    ("Charlie", "enqueue"),
    ("David", "enqueue"),
    ("dequeue", "dequeue"),
    ("Eve", "enqueue"),
    ("dequeue", "dequeue"),
    ("dequeue", "dequeue"),
    ("dequeue", "dequeue"),
    ("dequeue", "dequeue")
]

for operation in operations:
    if operation[1] == "enqueue":
        print(file_attente.enqueue(operation[0]))
    else:
        print(f"Dequeue : {file_attente.dequeue()}")

    print(f"File : {file_attente}")
    print(f"Taille : {file_attente.size()}")
    print(f"Premier : {file_attente.front()}")
    print(f"Dernier : {file_attente.rear()}\n")
```

**Explication** :
- **FIFO** : First In, First Out
- **enqueue()** : ajout à la fin
- **dequeue()** : retrait du début (pop(0))
- **front/rear** : consultation des extrémités
- **Performance** : pop(0) moins efficace que append

**Test** : Opérations de file avec consultation des extrémités.

---

### Exercice 223 : Classe Matrix avec addition et multiplication
**Objectif** : Implémenter une matrice avec opérations arithmétiques.

```python
# Solution
class Matrix:
    """Matrice avec opérations arithmétiques"""

    def __init__(self, data):
        """Constructeur avec liste de listes"""
        if not data or not data[0]:
            raise ValueError("Matrice vide")

        # Validation des dimensions
        n_cols = len(data[0])
        for row in data:
            if len(row) != n_cols:
                raise ValueError("Lignes de longueurs différentes")

        self.data = data
        self.rows = len(data)
        self.cols = n_cols

    def __add__(self, other):
        """Addition de matrices"""
        if not isinstance(other, Matrix):
            return NotImplemented
        if self.rows != other.rows or self.cols != other.cols:
            raise ValueError("Matrices de dimensions différentes")

        result = []
        for i in range(self.rows):
            row = [self.data[i][j] + other.data[i][j] for j in range(self.cols)]
            result.append(row)

        return Matrix(result)

    def __mul__(self, other):
        """Multiplication de matrices"""
        if not isinstance(other, Matrix):
            return NotImplemented
        if self.cols != other.rows:
            raise ValueError("Dimensions incompatibles pour la multiplication")

        result = []
        for i in range(self.rows):
            row = []
            for j in range(other.cols):
                # Calcul du produit scalaire
                element = sum(self.data[i][k] * other.data[k][j] for k in range(self.cols))
                row.append(element)
            result.append(row)

        return Matrix(result)

    def __str__(self):
        """Représentation de la matrice"""
        return "\n".join(str(row) for row in self.data)

    def __repr__(self):
        """Représentation Python"""
        return f"Matrix({self.data})"

    def transpose(self):
        """Transposition de la matrice"""
        transposed = [[self.data[j][i] for j in range(self.rows)] for i in range(self.cols)]
        return Matrix(transposed)

    def get_element(self, i, j):
        """Accès à un élément"""
        if 0 <= i < self.rows and 0 <= j < self.cols:
            return self.data[i][j]
        raise IndexError("Indices hors limites")

# Tests
mat_a = Matrix([[1, 2], [3, 4]])
mat_b = Matrix([[5, 6], [7, 8]])

print("Matrices de test :")
print(f"A =\n{mat_a}")
print(f"B =\n{mat_b}")

# Addition
mat_somme = mat_a + mat_b
print(f"\nA + B =\n{mat_somme}")

# Multiplication
mat_produit = mat_a * mat_b
print(f"\nA × B =\n{mat_produit}")

# Transposition
mat_a_transposee = mat_a.transpose()
print(f"\nA^T =\n{mat_a_transposee}")

# Accès aux éléments
print("
Accès aux éléments :")
print(f"A[0][0] = {mat_a.get_element(0, 0)}")
print(f"A[1][1] = {mat_a.get_element(1, 1)}")

# Test d'erreur
try:
    mat_a.get_element(2, 2)
except IndexError as e:
    print(f"Erreur d'accès : {e}")
```

**Explication** :
- **Validation** : dimensions cohérentes
- **Addition** : élément par élément
- **Multiplication** : produit matriciel
- **Transposition** : échange lignes/colonnes
- **Accès sécurisé** : vérification des indices

**Test** : Opérations matricielles complètes.

---

### Exercice 224 : Créer un objet à partir d'une chaîne JSON
**Objectif** : Démontrer la sérialisation et désérialisation JSON.

```python
# Solution
import json

class Etudiant:
    """Étudiant avec sérialisation JSON"""

    def __init__(self, nom, age, notes, filiere="Informatique"):
        """Constructeur"""
        self.nom = nom
        self.age = age
        self.notes = notes  # Liste de notes
        self.filiere = filiere

    def to_dict(self):
        """Convertit l'objet en dictionnaire pour JSON"""
        return {
            "nom": self.nom,
            "age": self.age,
            "notes": self.notes,
            "filiere": self.filiere
        }

    @classmethod
    def from_dict(cls, data):
        """Crée un objet à partir d'un dictionnaire"""
        return cls(data["nom"], data["age"], data["notes"], data["filiere"])

    def to_json(self):
        """Sérialise en JSON"""
        return json.dumps(self.to_dict(), indent=2)

    @classmethod
    def from_json(cls, json_str):
        """Désérialise depuis JSON"""
        data = json.loads(json_str)
        return cls.from_dict(data)

    def __str__(self):
        """Représentation de l'étudiant"""
        return f"{self.nom} ({self.age} ans, {self.filiere})"

# Tests
etudiants = [
    Etudiant("Alice", 20, [15, 16, 14], "Mathématiques"),
    Etudiant("Bob", 22, [12, 13, 11], "Physique"),
    Etudiant("Charlie", 21, [18, 17, 19], "Informatique")
]

print("Étudiants originaux :")
for etu in etudiants:
    print(f"  {etu}")

# Sérialisation JSON
print("\n=== SÉRIALISATION JSON ===")
for etu in etudiants:
    json_str = etu.to_json()
    print(f"JSON de {etu.nom} :")
    print(json_str)

# Désérialisation
print("\n=== DÉSÉRIALISATION JSON ===")
json_examples = [
    '{"nom": "Diana", "age": 19, "notes": [16, 17, 15], "filiere": "Chimie"}',
    '{"nom": "Eve", "age": 23, "notes": [14, 15, 13], "filiere": "Biologie"}'
]

for json_str in json_examples:
    etu_recree = Etudiant.from_json(json_str)
    print(f"Étudiant recréé : {etu_recree}")
    print(f"Notes : {etu_recree.notes}")
    print(f"Moyenne : {sum(etu_recree.notes) / len(etu_recree.notes):.2f}\n")
```

**Explication** :
- **to_dict()** : conversion en dictionnaire
- **from_dict()** : reconstruction depuis dictionnaire
- **to_json()** : sérialisation JSON
- **from_json()** : désérialisation JSON
- **json.dumps/loads** : fonctions de sérialisation

**Test** : Sérialisation et désérialisation d'objets.

---

### Exercice 225 : Sérialiser un objet en JSON
**Objectif** : Étendre la sérialisation JSON avec des classes complexes.

```python
# Solution
import json

class Produit:
    """Produit avec sérialisation JSON"""

    def __init__(self, nom, prix, quantite, categorie="Général"):
        """Constructeur"""
        self.nom = nom
        self.prix = prix
        self.quantite = quantite
        self.categorie = categorie
        self.date_creation = None  # Sera défini après

    def set_date_creation(self, date):
        """Définit la date de création"""
        self.date_creation = date

    def valeur_totale(self):
        """Calcule la valeur totale"""
        return self.prix * self.quantite

    def to_dict(self):
        """Conversion pour JSON"""
        return {
            "nom": self.nom,
            "prix": self.prix,
            "quantite": self.quantite,
            "categorie": self.categorie,
            "date_creation": self.date_creation,
            "valeur_totale": self.valeur_totale()
        }

    def to_json(self):
        """Sérialisation JSON"""
        return json.dumps(self.to_dict(), indent=2, default=str)

    @classmethod
    def from_dict(cls, data):
        """Reconstruction depuis dictionnaire"""
        produit = cls(
            data["nom"],
            data["prix"],
            data["quantite"],
            data.get("categorie", "Général")
        )
        if "date_creation" in data:
            produit.date_creation = data["date_creation"]
        return produit

    def __str__(self):
        """Représentation"""
        return f"{self.nom} ({self.prix}€, stock: {self.quantite})"

# Tests
produits = [
    Produit("Ordinateur", 800, 10, "Électronique"),
    Produit("Souris", 25, 50, "Accessoires"),
    Produit("Clavier", 45, 30, "Accessoires")
]

# Ajout de dates
from datetime import datetime
for i, produit in enumerate(produits):
    date = datetime(2024, 1, 1 + i)
    produit.set_date_creation(date)

print("Produits avec sérialisation JSON :")
for produit in produits:
    print(f"\nOriginal : {produit}")
    print(f"JSON : {produit.to_json()}")

# Test de reconstruction
json_produit = '''{
  "nom": "Imprimante",
  "prix": 150,
  "quantite": 5,
  "categorie": "Bureau",
  "date_creation": "2024-01-10T00:00:00",
  "valeur_totale": 750
}'''

produit_recree = Produit.from_dict(json.loads(json_produit))
print("
Produit recréé depuis JSON :")
print(f"  {produit_recree}")
print(f"  Valeur totale : {produit_recree.valeur_totale()}€")
print(f"  Date création : {produit_recree.date_creation}")
```

**Explication** :
- **Attributs calculés** : valeur_totale()
- **Dates** : gestion des objets datetime
- **default=str** : conversion des objets non JSON
- **Reconstruction** : from_dict() pour recréer
- **Persistance** : sauvegarde et chargement d'état

**Test** : Sérialisation de produits avec reconstruction.

---

## 🔍 Points Clés à Retenir

### 1. **Collections.namedtuple**
```python
from collections import namedtuple

# Définition
Personne = namedtuple('Personne', ['nom', 'age', 'ville'])

# Création
alice = Personne('Alice', 25, 'Paris')

# Accès
print(alice.nom)      # 'Alice'
print(alice.age)      # 25
print(alice.ville)    # 'Paris'

# Déballage
nom, age, ville = alice
print(f"{nom} a {age} ans et habite {ville}")

# Conversion
print(alice._asdict())  # {'nom': 'Alice', 'age': 25, 'ville': 'Paris'}
```

### 2. **Structures de Données**
```python
# Pile (LIFO)
class Stack:
    def __init__(self):
        self.items = []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        return self.items.pop() if self.items else None

# File (FIFO)
class Queue:
    def __init__(self):
        self.items = []

    def enqueue(self, item):
        self.items.append(item)

    def dequeue(self):
        return self.items.pop(0) if self.items else None

# File avec deque (plus efficace)
from collections import deque
file_efficace = deque()
file_efficace.append("élément")  # enqueue
file_efficace.popleft()          # dequeue
```

### 3. **Sérialisation JSON**
```python
import json

# Objet simple
data = {"nom": "Alice", "age": 25}
json_str = json.dumps(data)      # Sérialisation
data_recree = json.loads(json_str)  # Désérialisation

# Objet complexe
class MonObjet:
    def to_dict(self):
        return {"valeur": self.valeur}

    @classmethod
    def from_dict(cls, data):
        return cls(data["valeur"])

# Sérialisation personnalisée
def objet_to_dict(obj):
    if hasattr(obj, 'to_dict'):
        return obj.to_dict()
    raise TypeError("Objet non sérialisable")

json_str = json.dumps(obj, default=objet_to_dict)
```

### 4. **Pickle pour Objets Complexes**
```python
import pickle

# Sérialisation
with open('objet.pkl', 'wb') as f:
    pickle.dump(mon_objet, f)

# Désérialisation
with open('objet.pkl', 'rb') as f:
    objet_recree = pickle.load(f)

# Attention : pickle peut exécuter du code malveillant
# Utiliser seulement pour des données de confiance
```

## 💡 Optimisations et Astuces

### 1. **Copy vs Deepcopy**
```python
import copy

# Copie superficielle (partage les objets internes)
liste1 = [1, 2, [3, 4]]
liste2 = liste1.copy()  # ou copy.copy(liste1)
liste2[0] = 999
print(liste1)  # [1, 2, [3, 4]] - [3,4] partagé
print(liste2)  # [999, 2, [3, 4]]

# Copie profonde (copie tout)
liste3 = copy.deepcopy(liste1)
liste3[2][0] = 999
print(liste1)  # [1, 2, [3, 4]] - indépendant
print(liste3)  # [1, 2, [999, 4]]
```

### 2. **Counter pour Comptage**
```python
from collections import Counter

# Comptage simple
mots = ["le", "python", "est", "un", "langage", "python", "est", "puissant"]
compteur = Counter(mots)
print(compteur)  # Counter({'python': 2, 'est': 2, 'le': 1, ...})

# Éléments les plus fréquents
print(compteur.most_common(3))  # [('python', 2), ('est', 2), ('le', 1)]

# Mise à jour
compteur.update(["python", "nouveau"])
print(compteur)  # Counter({'python': 3, 'est': 2, ...})
```

### 3. **Defaultdict pour Valeurs par Défaut**
```python
from collections import defaultdict

# Dictionnaire avec valeurs par défaut
compteur = defaultdict(int)
for mot in ["a", "b", "a", "c", "a"]:
    compteur[mot] += 1

print(compteur)  # defaultdict(<class 'int'>, {'a': 3, 'b': 1, 'c': 1})

# Avec liste par défaut
groupes = defaultdict(list)
groupes["fruits"].append("pomme")
groupes["fruits"].append("banane")
groupes["legumes"].append("carotte")

print(groupes)  # defaultdict(<class 'list'>, {'fruits': ['pomme', 'banane'], ...})
```

## 🚀 Applications Pratiques

### 1. **Système de Gestion de Tâches**
```python
from collections import deque
import json
from datetime import datetime

class TaskManager:
    """Gestionnaire de tâches avec file de priorités"""

    def __init__(self):
        self.taches = deque()
        self.taches_terminees = []
        self.historique = []

    def ajouter_tache(self, description, priorite=1):
        """Ajoute une tâche avec priorité"""
        tache = {
            "id": len(self.taches) + 1,
            "description": description,
            "priorite": priorite,
            "date_creation": datetime.now().isoformat(),
            "terminee": False
        }
        self.taches.append(tache)
        self.historique.append(f"Tâche ajoutée: {description}")
        return tache["id"]

    def traiter_tache(self):
        """Traite la tâche la plus prioritaire"""
        if not self.taches:
            return "Aucune tâche"

        # Trier par priorité (plus petit = plus prioritaire)
        taches_tries = sorted(self.taches, key=lambda t: t["priorite"])
        tache = taches_tries[0]

        # Marquer comme terminée
        tache["terminee"] = True
        tache["date_terminaison"] = datetime.now().isoformat()

        # Déplacer vers terminées
        self.taches_terminees.append(tache)
        self.taches = deque(t for t in self.taches if t["id"] != tache["id"])

        self.historique.append(f"Tâche terminée: {tache['description']}")
        return f"Tâche traitée: {tache['description']}"

    def sauvegarder(self, filename):
        """Sauvegarde l'état en JSON"""
        etat = {
            "taches": list(self.taches),
            "taches_terminees": self.taches_terminees,
            "historique": self.historique
        }

        with open(filename, 'w') as f:
            json.dump(etat, f, indent=2)

        return f"Sauvegardé dans {filename}"

    def charger(self, filename):
        """Charge l'état depuis JSON"""
        try:
            with open(filename, 'r') as f:
                etat = json.load(f)

            self.taches = deque(etat["taches"])
            self.taches_terminees = etat["taches_terminees"]
            self.historique = etat["historique"]

            return f"État chargé depuis {filename}"
        except FileNotFoundError:
            return "Fichier non trouvé"

# Test
gestionnaire = TaskManager()

# Ajout de tâches
print("Ajout de tâches :")
taches = [
    ("Répondre aux emails", 2),
    ("Préparer réunion", 1),
    ("Coder nouvelle fonctionnalité", 3),
    ("Tester l'application", 2)
]

for desc, prio in taches:
    id_tache = gestionnaire.ajouter_tache(desc, prio)
    print(f"  Tâche {id_tache}: {desc} (priorité {prio})")

# Traitement
print("
Traitement des tâches :")
while gestionnaire.taches:
    resultat = gestionnaire.traiter_tache()
    print(f"  {resultat}")

print(f"\nHistorique : {gestionnaire.historique}")

# Sauvegarde et chargement
print(f"\n{gestionnaire.sauvegarder('taches_backup.json')}")
print(f"{gestionnaire.charger('taches_backup.json')}")
```

### 2. **Calculateur de Matrices**
```python
class MatrixCalculator:
    """Calculateur de matrices avec opérations"""

    @staticmethod
    def addition(mat1, mat2):
        """Addition de matrices"""
        if len(mat1) != len(mat2) or len(mat1[0]) != len(mat2[0]):
            raise ValueError("Dimensions incompatibles")

        return [[mat1[i][j] + mat2[i][j] for j in range(len(mat1[0]))]
                for i in range(len(mat1))]

    @staticmethod
    def multiplication(mat1, mat2):
        """Multiplication de matrices"""
        if len(mat1[0]) != len(mat2):
            raise ValueError("Dimensions incompatibles")

        result = []
        for i in range(len(mat1)):
            row = []
            for j in range(len(mat2[0])):
                element = sum(mat1[i][k] * mat2[k][j] for k in range(len(mat2)))
                row.append(element)
            result.append(row)

        return result

    @staticmethod
    def transposition(matrice):
        """Transposition"""
        return [[matrice[j][i] for j in range(len(matrice))]
                for i in range(len(matrice[0]))]

    @staticmethod
    def determinant_2x2(matrice):
        """Déterminant d'une matrice 2x2"""
        if len(matrice) != 2 or len(matrice[0]) != 2:
            raise ValueError("Matrice 2x2 requise")

        return matrice[0][0] * matrice[1][1] - matrice[0][1] * matrice[1][0]

    @staticmethod
    def trace(matrice):
        """Trace de la matrice (somme de la diagonale)"""
        return sum(matrice[i][i] for i in range(min(len(matrice), len(matrice[0]))))

# Tests
calc = MatrixCalculator()

# Matrices de test
A = [[1, 2], [3, 4]]
B = [[5, 6], [7, 8]]
C = [[1, 2, 3], [4, 5, 6]]

print("Calculateur de matrices :")
print(f"A = {A}")
print(f"B = {B}")
print(f"C = {C}")

# Addition
print(f"\nA + B = {calc.addition(A, B)}")

# Multiplication
print(f"A × B = {calc.multiplication(A, B)}")

# Transposition
print(f"C^T = {calc.transposition(C)}")

# Déterminant
print(f"dét(A) = {calc.determinant_2x2(A)}")

# Trace
print(f"trace(C) = {calc.trace(C)}")

# Test d'erreur
try:
    calc.addition(A, C)
except ValueError as e:
    print(f"Erreur dimension : {e}")
```

### 3. **Système de Configuration Persistant**
```python
class ConfigManager:
    """Gestionnaire de configuration avec persistance"""

    def __init__(self, filename="config.json"):
        self.filename = filename
        self.config = self._load_config()

    def _load_config(self):
        """Charge la configuration depuis un fichier"""
        try:
            with open(self.filename, 'r') as f:
                return json.load(f)
        except (FileNotFoundError, json.JSONDecodeError):
            return self._default_config()

    def _default_config(self):
        """Configuration par défaut"""
        return {
            "debug": False,
            "theme": "clair",
            "langue": "fr",
            "timeout": 30,
            "max_connexions": 100,
            "notifications": True
        }

    def get(self, key, default=None):
        """Récupère une valeur de configuration"""
        return self.config.get(key, default)

    def set(self, key, value):
        """Modifie une valeur de configuration"""
        self.config[key] = value
        self._save_config()

    def update(self, new_config):
        """Met à jour plusieurs valeurs"""
        self.config.update(new_config)
        self._save_config()

    def _save_config(self):
        """Sauvegarde la configuration"""
        with open(self.filename, 'w') as f:
            json.dump(self.config, f, indent=2)

    def reset(self):
        """Remet la configuration par défaut"""
        self.config = self._default_config()
        self._save_config()

    def info(self):
        """Affiche les informations de configuration"""
        return {
            "fichier": self.filename,
            "elements": len(self.config),
            "config": self.config.copy()
        }

# Test
config = ConfigManager("app_config.json")

print("Configuration initiale :")
print(f"  Debug : {config.get('debug')}")
print(f"  Theme : {config.get('theme')}")
print(f"  Timeout : {config.get('timeout')}")

# Modifications
print("
Modifications :")
config.set("debug", True)
config.set("theme", "sombre")
config.update({"timeout": 60, "max_connexions": 200})

print(f"  Debug après modification : {config.get('debug')}")
print(f"  Theme après modification : {config.get('theme')}")

# Informations
info = config.info()
print(f"\nInformations : {info}")

# Reset
print("
Reset à la configuration par défaut :")
config.reset()
print(f"  Debug après reset : {config.get('debug')}")
print(f"  Theme après reset : {config.get('theme')}")
```

## 🎯 Défis Supplémentaires

1. **Créez** une classe Deque (double-ended queue) personnalisée
2. **Implémentez** un système de cache LRU (Least Recently Used)
3. **Développez** une classe Tree pour des structures arborescentes
4. **Concevez** un système de sauvegarde/chargement automatique d'objets

---

**Exercices complétés : 225/230** 🎯

*Continuez avec le [chapitre suivant](5-5-methodes-speciales.md) pour les méthodes spéciales avancées !*
