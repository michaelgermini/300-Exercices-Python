# Partie 6.3 : Gestion de Fichiers

## 🎯 Objectifs Pédagogiques

Ce chapitre explore la **gestion avancée de fichiers** en Python, incluant la vérification d'existence, la suppression, et les opérations sur les systèmes de fichiers.

### Concepts Abordés
- **Vérification d'existence** : os.path.exists()
- **Suppression de fichiers** : os.remove()
- **Chemins et répertoires** : os.path, os.makedirs()
- **Applications** : nettoyage, organisation, gestion de fichiers

---

## 📝 Exercices Pratiques

### Exercice 241 : Supprimer un fichier
**Objectif** : Supprimer un fichier du système de fichiers.

```python
# Solution
import os

def supprimer_fichier(nom_fichier):
    """Supprime un fichier s'il existe"""
    try:
        if os.path.exists(nom_fichier):
            os.remove(nom_fichier)
            print(f"Fichier '{nom_fichier}' supprimé avec succès")
            return True
        else:
            print(f"Le fichier '{nom_fichier}' n'existe pas")
            return False
    except PermissionError:
        print(f"Permission refusée pour supprimer '{nom_fichier}'")
        return False
    except Exception as e:
        print(f"Erreur lors de la suppression : {e}")
        return False

# Tests
print("Tests de suppression de fichiers :")

# Création de fichiers de test
with open("test_delete1.txt", 'w') as f:
    f.write("Fichier à supprimer 1")

with open("test_delete2.txt", 'w') as f:
    f.write("Fichier à supprimer 2")

# Suppression
supprimer_fichier("test_delete1.txt")
supprimer_fichier("test_delete2.txt")

# Tentative de suppression d'un fichier inexistant
supprimer_fichier("fichier_inexistant.txt")

# Vérification
print("\nVérification après suppression :")
for i in range(1, 3):
    fichier = f"test_delete{i}.txt"
    existe = os.path.exists(fichier)
    print(f"{fichier} existe : {existe}")
```

**Explication** :
- **os.path.exists()** : vérification d'existence
- **os.remove()** : suppression de fichier
- **Gestion d'erreurs** : permissions, fichier inexistant
- **Applications** : nettoyage, maintenance

**Test** : Supprimez des fichiers de test.

---

### Exercice 242 : Vérifier si un fichier existe
**Objectif** : Vérifier l'existence de fichiers et répertoires.

```python
# Solution
import os

def verifier_existence(chemin):
    """Vérifie l'existence d'un fichier ou répertoire"""
    if os.path.exists(chemin):
        print(f"✓ '{chemin}' existe")

        if os.path.isfile(chemin):
            print("  C'est un fichier")
            taille = os.path.getsize(chemin)
            print(f"  Taille : {taille} octets")
        elif os.path.isdir(chemin):
            print("  C'est un répertoire")
            contenu = os.listdir(chemin)
            print(f"  Contenu : {len(contenu)} éléments")

        return True
    else:
        print(f"✗ '{chemin}' n'existe pas")
        return False

# Tests
print("Tests de vérification d'existence :")

# Fichiers existants
verifier_existence("README.md")
verifier_existence("Partie 1 - Bases")

# Fichiers inexistants
verifier_existence("fichier_inexistant.txt")
verifier_existence("repertoire_inexistant")

# Tests avec des chemins relatifs
print("\nTests avec chemins relatifs :")
verifier_existence("Partie 1 - Bases/1-1-types-donnees.md")
verifier_existence("Partie 2 - Controle flux/2-1-conditions.md")
```

**Explication** :
- **os.path.exists()** : existence générale
- **os.path.isfile()** : test de fichier
- **os.path.isdir()** : test de répertoire
- **os.path.getsize()** : taille en octets
- **os.listdir()** : contenu d'un répertoire

**Test** : Vérifiez l'existence de différents éléments.

---

### Exercice 243 : Lire un fichier ligne par ligne
**Objectif** : Traiter un fichier en lisant ligne par ligne.

```python
# Solution
def analyser_fichier_lignes(nom_fichier):
    """Analyse un fichier ligne par ligne"""
    try:
        with open(nom_fichier, 'r', encoding='utf-8') as fichier:
            lignes = fichier.readlines()  # Lit toutes les lignes

        print(f"Fichier '{nom_fichier}' contient {len(lignes)} lignes :")

        for i, ligne in enumerate(lignes, 1):
            # Nettoyage de la ligne
            ligne_propre = ligne.strip()
            if ligne_propre:  # Ignore les lignes vides
                print(f"Ligne {i}: '{ligne_propre}' (longueur: {len(ligne_propre)})")

        return lignes

    except FileNotFoundError:
        print(f"Erreur : Le fichier '{nom_fichier}' n'existe pas")
        return []
    except Exception as e:
        print(f"Erreur lors de l'analyse : {e}")
        return []

# Test avec le journal créé précédemment
lignes = analyser_fichier_lignes("journal.txt")

# Traitement ligne par ligne avec readlines()
print("\nAnalyse alternative avec readlines() :")
try:
    with open("journal.txt", 'r') as f:
        for i, ligne in enumerate(f.readlines(), 1):
            print(f"Ligne {i}: {ligne.strip()}")
except Exception as e:
    print(f"Erreur : {e}")
```

**Explanation** :
- **.readlines()** : lit toutes les lignes en liste
- **enumerate()** : numérotation des lignes
- **.strip()** : suppression des espaces et sauts de ligne
- **Filtrage** : ignore les lignes vides

**Test** : Analysez le journal ligne par ligne.

---

### Exercice 244 : Compter les lignes d'un fichier
**Objectif** : Compter le nombre de lignes dans un fichier.

```python
# Solution
def compter_lignes_fichier(nom_fichier):
    """Compte le nombre de lignes dans un fichier"""
    try:
        with open(nom_fichier, 'r', encoding='utf-8') as fichier:
            nombre_lignes = sum(1 for ligne in fichier)

        print(f"Le fichier '{nom_fichier}' contient {nombre_lignes} lignes")
        return nombre_lignes

    except FileNotFoundError:
        print(f"Erreur : Le fichier '{nom_fichier}' n'existe pas")
        return 0
    except Exception as e:
        print(f"Erreur lors du comptage : {e}")
        return 0

# Tests
print("Tests de comptage de lignes :")

# Création de fichiers de test avec différentes tailles
with open("test_lignes1.txt", 'w') as f:
    f.write("Ligne 1\nLigne 2\nLigne 3\n")

with open("test_lignes2.txt", 'w') as f:
    for i in range(10):
        f.write(f"Ligne {i+1}\n")

with open("test_lignes3.txt", 'w') as f:
    f.write("Une seule ligne sans retour à la ligne")

# Comptage
compter_lignes_fichier("test_lignes1.txt")  # 3 lignes
compter_lignes_fichier("test_lignes2.txt")  # 10 lignes
compter_lignes_fichier("test_lignes3.txt")  # 1 ligne

# Fichier vide
with open("test_vide.txt", 'w') as f:
    pass  # Fichier vide

compter_lignes_fichier("test_vide.txt")  # 0 lignes

# Nettoyage
import os
for fichier in ["test_lignes1.txt", "test_lignes2.txt", "test_lignes3.txt", "test_vide.txt"]:
    if os.path.exists(fichier):
        os.remove(fichier)
```

**Explication** :
- **Générateur** : sum(1 for ligne in fichier)
- **Performance** : O(n) mais efficace
- **Cas spéciaux** : fichiers vides, lignes sans \n
- **Applications** : analyse de logs, comptage

**Test** : Comptez les lignes de différents fichiers.

---

### Exercice 245 : Trier les lignes d'un fichier
**Objectif** : Trier le contenu d'un fichier ligne par ligne.

```python
# Solution
def trier_fichier(nom_fichier):
    """Trie les lignes d'un fichier"""
    try:
        with open(nom_fichier, 'r', encoding='utf-8') as fichier:
            lignes = fichier.readlines()

        # Tri des lignes
        lignes_tries = sorted(lignes)

        # Écriture du fichier trié
        with open(nom_fichier, 'w', encoding='utf-8') as fichier:
            fichier.writelines(lignes_tries)

        print(f"Fichier '{nom_fichier}' trié avec succès")
        print(f"Nombre de lignes : {len(lignes_tries)}")

        return lignes_tries

    except FileNotFoundError:
        print(f"Erreur : Le fichier '{nom_fichier}' n'existe pas")
        return []
    except Exception as e:
        print(f"Erreur lors du tri : {e}")
        return []

# Test
print("Test de tri de fichier :")

# Création d'un fichier avec lignes désordonnées
with open("test_tri.txt", 'w') as f:
    lignes = ["Zèbre", "Banane", "Avocat", "Pomme", "Citron", "Mangue"]
    f.write("\n".join(lignes))

print("Contenu avant tri :")
lire_fichier("test_tri.txt")

# Tri
lignes_tries = trier_fichier("test_tri.txt")

print("\nContenu après tri :")
lire_fichier("test_tri.txt")

# Vérification du tri
print(f"\nPremière ligne : '{lignes_tries[0].strip()}'")
print(f"Dernière ligne : '{lignes_tries[-1].strip()}'")

# Nettoyage
import os
os.remove("test_tri.txt")
```

**Explication** :
- **.readlines()** : lecture de toutes les lignes
- **sorted()** : tri alphabétique
- **.writelines()** : écriture des lignes triées
- **Applications** : organisation, classement

**Test** : Triez un fichier de mots.

---

## 🔍 Points Clés à Retenir

### 1. **Module os.path**
```python
import os

# Existence
os.path.exists("fichier.txt")        # Fichier existe ?
os.path.isfile("fichier.txt")        # C'est un fichier ?
os.path.isdir("repertoire")          # C'est un répertoire ?

# Informations
os.path.getsize("fichier.txt")       # Taille en octets
os.path.getmtime("fichier.txt")      # Date de modification
os.path.getctime("fichier.txt")      # Date de création

# Manipulation de chemins
os.path.join("repertoire", "fichier.txt")  # Chemin complet
os.path.splitext("fichier.txt")      # ("fichier", ".txt")
os.path.dirname("chemin/fichier.txt")  # "chemin"
os.path.basename("chemin/fichier.txt") # "fichier.txt"
```

### 2. **Module os**
```python
import os

# Fichiers et répertoires
os.remove("fichier.txt")             # Supprimer fichier
os.makedirs("nouveau/repertoire")   # Créer répertoires
os.rmdir("repertoire_vide")         # Supprimer répertoire vide
os.listdir("repertoire")            # Liste contenu

# Renommage et déplacement
os.rename("ancien.txt", "nouveau.txt")  # Renommer
os.rename("fichier.txt", "sous_dossier/fichier.txt")  # Déplacer

# Chemins absolus
os.getcwd()                         # Répertoire actuel
os.chdir("nouveau/repertoire")      # Changer de répertoire
os.path.abspath("fichier.txt")      # Chemin absolu
```

### 3. **Gestion d'Erreurs**
```python
import os

def operation_securisee(fichier):
    try:
        # Opération risquée
        os.remove(fichier)
    except FileNotFoundError:
        print("Fichier déjà supprimé")
    except PermissionError:
        print("Permission refusée")
    except Exception as e:
        print(f"Erreur inattendue : {e}")

# Test
operation_securisee("fichier_inexistant.txt")
```

### 4. **Chemins et Portabilité**
```python
import os

# Chemins portables
chemin = os.path.join("data", "fichiers", "config.txt")

# Normes de chemins
os.sep      # '/' sur Unix, '\' sur Windows
os.path.sep # Même chose

# Chemins relatifs vs absolus
os.path.isabs("/chemin/absolu")      # True
os.path.isabs("chemin/relatif")      # False

# Extension de fichier
_, extension = os.path.splitext("fichier.txt")
print(extension)  # ".txt"
```

## 💡 Optimisations et Astuces

### 1. **Vérification Avant Opération**
```python
import os

def supprimer_securise(nom_fichier):
    """Suppression sécurisée avec vérification"""
    if os.path.exists(nom_fichier):
        if os.path.isfile(nom_fichier):
            os.remove(nom_fichier)
            print(f"Fichier '{nom_fichier}' supprimé")
        else:
            print(f"'{nom_fichier}' est un répertoire, pas un fichier")
    else:
        print(f"Fichier '{nom_fichier}' n'existe pas")

# Test
supprimer_securise("test.txt")
supprimer_securise("repertoire")  # Erreur
```

### 2. **Opérations Récursives**
```python
import os
import shutil

def supprimer_arborescence(chemin):
    """Supprime un répertoire et son contenu"""
    if os.path.exists(chemin):
        if os.path.isfile(chemin):
            os.remove(chemin)
        else:
            shutil.rmtree(chemin)  # Supprime récursivement
        print(f"Supprimé : {chemin}")
    else:
        print(f"Chemin '{chemin}' n'existe pas")

# Test
supprimer_arborescence("dossier_test")
```

### 3. **Recherche de Fichiers**
```python
import os
import glob

# Recherche par motif
fichiers_txt = glob.glob("*.txt")          # Tous les .txt
fichiers_py = glob.glob("**/*.py")         # Tous les .py récursifs

# Recherche avec os.walk
for racine, dossiers, fichiers in os.walk("."):
    for fichier in fichiers:
        if fichier.endswith(".md"):
            chemin_complet = os.path.join(racine, fichier)
            print(f"Trouvé : {chemin_complet}")
```

## 🚀 Applications Pratiques

### 1. **Analyseur de Répertoire**
```python
def analyser_repertoire(chemin):
    """Analyse le contenu d'un répertoire"""
    if not os.path.exists(chemin):
        return "Répertoire non trouvé"

    stats = {
        "chemin": chemin,
        "fichiers": [],
        "repertoires": [],
        "taille_totale": 0,
        "extensions": {}
    }

    try:
        for element in os.listdir(chemin):
            chemin_element = os.path.join(chemin, element)

            if os.path.isfile(chemin_element):
                stats["fichiers"].append(element)
                taille = os.path.getsize(chemin_element)
                stats["taille_totale"] += taille

                # Extension
                nom, ext = os.path.splitext(element)
                if ext:
                    stats["extensions"][ext] = stats["extensions"].get(ext, 0) + 1

            elif os.path.isdir(chemin_element):
                stats["repertoires"].append(element)

    except PermissionError:
        return "Permission refusée"

    return stats

# Test
stats = analyser_repertoire("Partie 1 - Bases")
if isinstance(stats, dict):
    print("Analyse du répertoire :")
    print(f"  Fichiers : {len(stats['fichiers'])}")
    print(f"  Répertoires : {len(stats['repertoires'])}")
    print(f"  Taille totale : {stats['taille_totale']} octets")
    print(f"  Extensions : {stats['extensions']}")
else:
    print(stats)
```

### 2. **Nettoyeur de Fichiers Temporaires**
```python
def nettoyer_temporaires(extensions=None, age_max=None):
    """Nettoie les fichiers temporaires"""
    if extensions is None:
        extensions = [".tmp", ".temp", ".log", ".bak"]

    nettoyes = 0

    for element in os.listdir("."):
        if os.path.isfile(element):
            nom, ext = os.path.splitext(element)

            # Vérification de l'extension
            if ext.lower() in extensions:
                try:
                    os.remove(element)
                    nettoyes += 1
                    print(f"Supprimé : {element}")
                except Exception as e:
                    print(f"Erreur suppression {element} : {e}")

    print(f"Total nettoyé : {nettoyes} fichiers")
    return nettoyes

# Test
print("Nettoyage des fichiers temporaires :")
nombre_nettoye = nettoyer_temporaires()
print(f"Fichiers nettoyés : {nombre_nettoye}")
```

### 3. **Organisateur de Fichiers**
```python
def organiser_fichiers(source, destination, par_extension=True):
    """Organise les fichiers par extension"""
    if not os.path.exists(source):
        return "Répertoire source non trouvé"

    if not os.path.exists(destination):
        os.makedirs(destination)

    organises = 0

    for element in os.listdir(source):
        chemin_source = os.path.join(source, element)

        if os.path.isfile(chemin_source):
            if par_extension:
                # Organisation par extension
                nom, ext = os.path.splitext(element)
                if ext:
                    dossier_ext = os.path.join(destination, ext[1:])  # Sans le point
                    os.makedirs(dossier_ext, exist_ok=True)
                    chemin_dest = os.path.join(dossier_ext, element)
                else:
                    # Fichiers sans extension
                    dossier_autre = os.path.join(destination, "autres")
                    os.makedirs(dossier_autre, exist_ok=True)
                    chemin_dest = os.path.join(dossier_autre, element)
            else:
                # Tous dans le même dossier
                chemin_dest = os.path.join(destination, element)

            try:
                os.rename(chemin_source, chemin_dest)
                organises += 1
                print(f"Déplacé : {element}")
            except Exception as e:
                print(f"Erreur déplacement {element} : {e}")

    print(f"Total organisé : {organises} fichiers")
    return organises

# Test
organiser_fichiers("temp", "organise")
```

## 🎯 Défis Supplémentaires

1. **Créez** un programme qui trouve tous les fichiers d'une extension donnée
2. **Implémentez** un système de sauvegarde avec copie de fichiers
3. **Développez** un analyseur de taille de répertoires
4. **Concevez** un système de synchronisation de fichiers

---

**Exercices complétés : 245/260** 🎯

*Continuez avec le [chapitre suivant](6-4-sqlite.md) pour les bases de données SQLite !*
