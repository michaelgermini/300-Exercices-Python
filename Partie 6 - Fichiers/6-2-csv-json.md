# Partie 6.2 : Fichiers CSV et JSON

## 🎯 Objectifs Pédagogiques

Ce chapitre explore la **manipulation de fichiers CSV et JSON** en Python, formats couramment utilisés pour l'échange et le stockage de données structurées.

### Concepts Abordés
- **Fichiers CSV** : lecture, écriture, parsing
- **Fichiers JSON** : sérialisation, désérialisation
- **Module csv** : outils spécialisés pour CSV
- **Applications** : données tabulaires, configuration, APIs

---

## 📝 Exercices Pratiques

### Exercice 236 : Lire un fichier CSV
**Objectif** : Lire et analyser le contenu d'un fichier CSV.

```python
# Solution
import csv

def lire_csv(nom_fichier):
    """Lit un fichier CSV et affiche son contenu"""
    try:
        with open(nom_fichier, 'r', newline='', encoding='utf-8') as fichier:
            lecteur = csv.reader(fichier)
            lignes = list(lecteur)

        print(f"Fichier '{nom_fichier}' lu avec succès")
        print(f"Nombre de lignes : {len(lignes)}")

        # Affichage des 5 premières lignes
        print("\nPremières lignes :")
        for i, ligne in enumerate(lignes[:5]):
            print(f"Ligne {i+1}: {ligne}")

        return lignes

    except FileNotFoundError:
        print(f"Erreur : Le fichier '{nom_fichier}' n'existe pas")
        return []
    except Exception as e:
        print(f"Erreur lors de la lecture : {e}")
        return []

# Test
donnees = lire_csv("etudiants.csv")
if donnees:
    print(f"\nColonnes détectées : {len(donnees[0])}")
    print(f"Exemple de données : {donnees[1]}")
```

**Explication** :
- **csv.reader()** : lecteur de fichiers CSV
- **newline=''** : gestion des sauts de ligne
- **list(lecteur)** : conversion en liste de listes
- **Applications** : données tabulaires, exports

**Test** : Créez un fichier "etudiants.csv" avec des données d'étudiants.

---

### Exercice 237 : Écrire un fichier CSV
**Objectif** : Créer et écrire dans un fichier CSV.

```python
# Solution
import csv

def ecrire_csv(nom_fichier, donnees, en_tetes=None):
    """Écrit des données dans un fichier CSV"""
    try:
        with open(nom_fichier, 'w', newline='', encoding='utf-8') as fichier:
            ecrivain = csv.writer(fichier)

            # Écriture des en-têtes si fournis
            if en_tetes:
                ecrivain.writerow(en_tetes)

            # Écriture des données
            ecrivain.writerows(donnees)

        print(f"Fichier '{nom_fichier}' créé avec succès")
        return True

    except Exception as e:
        print(f"Erreur lors de l'écriture : {e}")
        return False

# Test
en_tetes = ["Nom", "Age", "Ville", "Note"]
etudiants = [
    ["Alice", 25, "Paris", 18.5],
    ["Bob", 22, "Lyon", 15.2],
    ["Charlie", 28, "Marseille", 16.8],
    ["Diana", 24, "Toulouse", 19.1]
]

ecrire_csv("etudiants_export.csv", etudiants, en_tetes)

# Vérification
print("\nVérification du fichier créé :")
donnees_lues = lire_csv("etudiants_export.csv")
```

**Explication** :
- **csv.writer()** : écrivain de fichiers CSV
- **writerow()** : écriture d'une ligne
- **writerows()** : écriture de plusieurs lignes
- **En-têtes** : première ligne optionnelle

**Test** : Créez un fichier CSV avec des données d'étudiants.

---

### Exercice 238 : Lire un fichier JSON
**Objectif** : Charger et analyser des données JSON.

```python
# Solution
import json

def lire_json(nom_fichier):
    """Lit un fichier JSON et retourne les données"""
    try:
        with open(nom_fichier, 'r', encoding='utf-8') as fichier:
            donnees = json.load(fichier)

        print(f"Fichier '{nom_fichier}' lu avec succès")
        print(f"Type des données : {type(donnees)}")

        if isinstance(donnees, dict):
            print(f"Clés principales : {list(donnees.keys())}")
        elif isinstance(donnees, list):
            print(f"Nombre d'éléments : {len(donnees)}")

        return donnees

    except FileNotFoundError:
        print(f"Erreur : Le fichier '{nom_fichier}' n'existe pas")
        return None
    except json.JSONDecodeError as e:
        print(f"Erreur de format JSON : {e}")
        return None
    except Exception as e:
        print(f"Erreur lors de la lecture : {e}")
        return None

# Test
config = lire_json("config.json")
if config:
    print(f"\nConfiguration chargée : {config}")
```

**Explication** :
- **json.load()** : désérialisation depuis fichier
- **Gestion d'erreurs** : format JSON invalide
- **Types de données** : dict, list, primitives
- **Applications** : configuration, APIs, données structurées

**Test** : Créez un fichier "config.json" avec des paramètres.

---

### Exercice 239 : Écrire un fichier JSON
**Objectif** : Sérialiser des données Python en JSON.

```python
# Solution
import json

def ecrire_json(nom_fichier, donnees):
    """Écrit des données en format JSON"""
    try:
        with open(nom_fichier, 'w', encoding='utf-8') as fichier:
            json.dump(donnees, fichier, indent=2, ensure_ascii=False)

        print(f"Fichier '{nom_fichier}' créé avec succès")
        return True

    except Exception as e:
        print(f"Erreur lors de l'écriture : {e}")
        return False

# Test
donnees_complexes = {
    "application": "Gestionnaire d'étudiants",
    "version": "1.0.0",
    "configuration": {
        "debug": True,
        "port": 8080,
        "timeout": 30
    },
    "etudiants": [
        {"nom": "Alice", "age": 25, "notes": [15, 16, 14]},
        {"nom": "Bob", "age": 22, "notes": [12, 13, 11]},
        {"nom": "Charlie", "age": 28, "notes": [18, 17, 19]}
    ],
    "statistiques": {
        "total_etudiants": 3,
        "moyenne_age": 25.0,
        "moyenne_notes": 15.11
    }
}

ecrire_json("donnees_complexes.json", donnees_complexes)

# Vérification
print("\nVérification du fichier JSON :")
donnees_lues = lire_json("donnees_complexes.json")
if donnees_lues:
    print(f"Application : {donnees_lues['application']}")
    print(f"Nombre d'étudiants : {donnees_lues['statistiques']['total_etudiants']}")
```

**Explication** :
- **json.dump()** : sérialisation vers fichier
- **indent=2** : formatage lisible
- **ensure_ascii=False** : préservation des caractères spéciaux
- **Structures complexes** : dictionnaires imbriqués, listes

**Test** : Créez un fichier JSON avec des données complexes.

---

### Exercice 240 : Charger un objet avec pickle
**Objectif** : Sérialiser et désérialiser des objets Python avec pickle.

```python
# Solution
import pickle

class Etudiant:
    """Étudiant sérialisable"""

    def __init__(self, nom, age, notes):
        self.nom = nom
        self.age = age
        self.notes = notes

    def moyenne(self):
        return sum(self.notes) / len(self.notes) if self.notes else 0

    def __str__(self):
        return f"{self.nom} ({self.age} ans, moyenne: {self.moyenne():.2f})"

def sauvegarder_objet(objet, nom_fichier):
    """Sauvegarde un objet avec pickle"""
    try:
        with open(nom_fichier, 'wb') as fichier:
            pickle.dump(objet, fichier)
        print(f"Objet sauvegardé dans '{nom_fichier}'")
        return True
    except Exception as e:
        print(f"Erreur sauvegarde : {e}")
        return False

def charger_objet(nom_fichier):
    """Charge un objet depuis pickle"""
    try:
        with open(nom_fichier, 'rb') as fichier:
            objet = pickle.load(fichier)
        print(f"Objet chargé depuis '{nom_fichier}'")
        return objet
    except FileNotFoundError:
        print(f"Fichier '{nom_fichier}' non trouvé")
        return None
    except Exception as e:
        print(f"Erreur chargement : {e}")
        return None

# Test
etudiants = [
    Etudiant("Alice", 25, [15, 16, 14]),
    Etudiant("Bob", 22, [12, 13, 11]),
    Etudiant("Charlie", 28, [18, 17, 19])
]

print("Étudiants originaux :")
for etu in etudiants:
    print(f"  {etu}")

# Sauvegarde
sauvegarder_objet(etudiants, "etudiants.pkl")

# Modification des originaux (simulation)
etudiants[0].notes = [16, 17, 15]  # Modification

print("\nÉtudiants après modification :")
for etu in etudiants:
    print(f"  {etu}")

# Chargement
etudiants_sauvegardes = charger_objet("etudiants.pkl")

print("\nÉtudiants sauvegardés (non modifiés) :")
if etudiants_sauvegardes:
    for etu in etudiants_sauvegardes:
        print(f"  {etu}")
```

**Explication** :
- **pickle.dump()** : sérialisation binaire
- **pickle.load()** : désérialisation
- **Objets complexes** : instances de classes, avec méthodes
- **Persistance** : sauvegarde complète de l'état
- **Attention** : sécurité, ne pas charger de fichiers non fiables

**Test** : Sauvegardez et chargez des objets Python.

---

## 🔍 Points Clés à Retenir

### 1. **Module CSV**
```python
import csv

# Lecture
with open('fichier.csv', 'r', newline='') as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)

# Écriture
with open('fichier.csv', 'w', newline='') as f:
    writer = csv.writer(f)
    writer.writerow(['Col1', 'Col2'])  # En-têtes
    writer.writerows([[1, 2], [3, 4]])  # Données
```

### 2. **Module JSON**
```python
import json

# Sérialisation
data = {"nom": "Alice", "age": 25}
json_str = json.dumps(data, indent=2)  # Chaîne JSON
with open('fichier.json', 'w') as f:
    json.dump(data, f, indent=2)  # Fichier JSON

# Désérialisation
data = json.loads(json_str)  # Depuis chaîne
with open('fichier.json', 'r') as f:
    data = json.load(f)  # Depuis fichier
```

### 3. **Module Pickle**
```python
import pickle

# Sérialisation
with open('objet.pkl', 'wb') as f:
    pickle.dump(mon_objet, f)

# Désérialisation
with open('objet.pkl', 'rb') as f:
    objet_recree = pickle.load(f)

# Attention : pickle peut exécuter du code
# Utiliser seulement pour des données de confiance
```

### 4. **Encodage et Gestion d'Erreurs**
```python
# Encodage UTF-8
with open('fichier.txt', 'r', encoding='utf-8') as f:
    contenu = f.read()

# Gestion d'erreurs
try:
    with open('fichier.csv', 'r') as f:
        reader = csv.reader(f)
        data = list(reader)
except FileNotFoundError:
    print("Fichier non trouvé")
except csv.Error as e:
    print(f"Erreur CSV : {e}")
```

## 💡 Optimisations et Astuces

### 1. **CSV avec Dictionnaires**
```python
# Lecture avec en-têtes
with open('fichier.csv', 'r') as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row['nom'], row['age'])  # Accès par clé

# Écriture avec en-têtes
with open('fichier.csv', 'w') as f:
    fieldnames = ['nom', 'age', 'ville']
    writer = csv.DictWriter(f, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerow({'nom': 'Alice', 'age': 25, 'ville': 'Paris'})
```

### 2. **JSON Avancé**
```python
# Objets personnalisés
class Person:
    def __init__(self, nom, age):
        self.nom = nom
        self.age = age

def person_to_dict(person):
    return {'nom': person.nom, 'age': person.age}

def dict_to_person(data):
    return Person(data['nom'], data['age'])

# Sérialisation personnalisée
person = Person("Alice", 25)
json_str = json.dumps(person, default=person_to_dict)
person_recree = json.loads(json_str, object_hook=dict_to_person)
```

### 3. **Validation JSON**
```python
import json

def valider_json(texte):
    """Valide une chaîne JSON"""
    try:
        json.loads(texte)
        return True, "JSON valide"
    except json.JSONDecodeError as e:
        return False, f"Erreur JSON : {e}"

# Test
tests = [
    '{"nom": "Alice", "age": 25}',
    '{"nom": "Alice", "age": }',  # Invalide
    '{"nom": "Alice", "age": 25',  # Invalide
]

for test in tests:
    valide, message = valider_json(test)
    print(f"{valide}: {message}")
```

## 🚀 Applications Pratiques

### 1. **Analyseur de Données CSV**
```python
def analyser_csv(nom_fichier):
    """Analyse complète d'un fichier CSV"""
    try:
        with open(nom_fichier, 'r', newline='') as f:
            reader = csv.reader(f)
            lignes = list(reader)

        if not lignes:
            return "Fichier vide"

        # Analyse
        nombre_lignes = len(lignes)
        nombre_colonnes = len(lignes[0]) if lignes else 0

        # Types de données par colonne
        types_colonnes = []
        for col in range(nombre_colonnes):
            types = set()
            for ligne in lignes[1:]:  # Ignore les en-têtes
                if col < len(ligne):
                    valeur = ligne[col].strip()
                    try:
                        int(valeur)
                        types.add('int')
                    except ValueError:
                        try:
                            float(valeur)
                            types.add('float')
                        except ValueError:
                            types.add('str')

            types_colonnes.append(types)

        return {
            "nom_fichier": nom_fichier,
            "lignes": nombre_lignes,
            "colonnes": nombre_colonnes,
            "en_tetes": lignes[0] if lignes else [],
            "types_colonnes": types_colonnes,
            "donnees": lignes[1:] if len(lignes) > 1 else []
        }

    except Exception as e:
        return f"Erreur : {e}"

# Test
analyse = analyser_csv("etudiants.csv")
if isinstance(analyse, dict):
    print("Analyse du fichier CSV :")
    for cle, valeur in analyse.items():
        print(f"  {cle}: {valeur}")
else:
    print(analyse)
```

### 2. **Convertisseur CSV vers JSON**
```python
def csv_vers_json(csv_file, json_file):
    """Convertit un fichier CSV en JSON"""
    try:
        # Lecture CSV
        with open(csv_file, 'r', newline='') as f:
            reader = csv.DictReader(f)
            donnees = [row for row in reader]

        # Écriture JSON
        with open(json_file, 'w') as f:
            json.dump(donnees, f, indent=2, ensure_ascii=False)

        print(f"Conversion réussie : {csv_file} → {json_file}")
        return True

    except Exception as e:
        print(f"Erreur conversion : {e}")
        return False

# Test
csv_vers_json("etudiants.csv", "etudiants.json")

# Vérification
if lire_json("etudiants.json"):
    print("Conversion vérifiée avec succès")
```

### 3. **Système de Configuration JSON**
```python
class ConfigManager:
    """Gestionnaire de configuration JSON"""

    def __init__(self, config_file="config.json"):
        self.config_file = config_file
        self.config = self._charger_config()

    def _charger_config(self):
        """Charge la configuration"""
        try:
            return lire_json(self.config_file) or self._config_defaut()
        except:
            return self._config_defaut()

    def _config_defaut(self):
        """Configuration par défaut"""
        return {
            "debug": False,
            "port": 8080,
            "timeout": 30,
            "database": {
                "host": "localhost",
                "port": 5432,
                "name": "app_db"
            }
        }

    def get(self, cle, defaut=None):
        """Récupère une valeur"""
        return self.config.get(cle, defaut)

    def set(self, cle, valeur):
        """Modifie une valeur"""
        self.config[cle] = valeur
        self._sauvegarder_config()

    def _sauvegarder_config(self):
        """Sauvegarde la configuration"""
        ecrire_json(self.config_file, self.config)

    def info(self):
        """Informations de configuration"""
        return {
            "fichier": self.config_file,
            "cles": list(self.config.keys()),
            "config": self.config.copy()
        }

# Test
config = ConfigManager()
print("Configuration actuelle :")
print(f"  Debug : {config.get('debug')}")
print(f"  Port : {config.get('port')}")
print(f"  Database : {config.get('database')}")

# Modification
config.set("debug", True)
config.set("port", 9000)

print("
Après modifications :")
print(f"  Debug : {config.get('debug')}")
print(f"  Port : {config.get('port')}")

# Vérification
info = config.info()
print(f"\nClés de configuration : {info['cles']}")
```

## 🎯 Défis Supplémentaires

1. **Créez** un programme qui importe des données CSV et les exporte en JSON
2. **Implémentez** un système de sauvegarde automatique avec pickle
3. **Développez** un analyseur de logs qui écrit en JSON
4. **Concevez** un convertisseur de formats multiples (CSV, JSON, XML)

---

**Exercices complétés : 240/260** 🎯

*Continuez avec le [chapitre suivant](6-3-gestion.md) pour la gestion de fichiers !*
