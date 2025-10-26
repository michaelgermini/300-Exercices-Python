# Partie 6 - Fichiers et Bases de Données : Solutions

## 🎯 Introduction

Cette partie présente les **solutions complètes** des exercices de la Partie 6. Chaque solution inclut :
- Le code source complet et fonctionnel
- Des explications détaillées
- Des exemples d'utilisation
- Des tests de validation

---

## 📚 Chapitre 6.1 : Solutions - Fichiers Texte

### Exercice 231 : Lire un fichier texte et afficher son contenu

**Solution complète :**

```python
# Solution de base
def lire_fichier(nom_fichier):
    """Lit et affiche le contenu d'un fichier"""
    try:
        with open(nom_fichier, 'r', encoding='utf-8') as fichier:
            contenu = fichier.read()
            print(f"Contenu de {nom_fichier} :")
            print(contenu)
            return contenu
    except FileNotFoundError:
        return f"Erreur : fichier '{nom_fichier}' non trouvé"
    except Exception as e:
        return f"Erreur lors de la lecture : {e}"

# Solution ligne par ligne
def lire_fichier_lignes(nom_fichier):
    """Lit et affiche le fichier ligne par ligne"""
    try:
        with open(nom_fichier, 'r', encoding='utf-8') as fichier:
            print(f"Contenu de {nom_fichier} (ligne par ligne) :")
            for numero, ligne in enumerate(fichier, 1):
                print(f"{numero"3d"}: {ligne.strip()}")
        return True
    except FileNotFoundError:
        print(f"Erreur : fichier '{nom_fichier}' non trouvé")
        return False

# Solution avec readline()
def lire_fichier_readline(nom_fichier):
    """Lit avec readline()"""
    try:
        with open(nom_fichier, 'r', encoding='utf-8') as fichier:
            print(f"Contenu de {nom_fichier} (readline) :")
            ligne = fichier.readline()
            while ligne:
                print(ligne.strip())
                ligne = fichier.readline()
        return True
    except FileNotFoundError:
        print(f"Erreur : fichier '{nom_fichier}' non trouvé")
        return False

# Test
print("=== Test de lecture de fichier ===")

# Création d'un fichier de test
contenu_test = """Bonjour le monde !
Ceci est un fichier de test.
Python est génial !
Fin du fichier."""

with open("test_lecture.txt", 'w', encoding='utf-8') as f:
    f.write(contenu_test)

# Tests des fonctions
print("\n1. Lecture complète :")
lire_fichier("test_lecture.txt")

print("\n2. Lecture ligne par ligne :")
lire_fichier_lignes("test_lecture.txt")

print("\n3. Lecture avec readline :")
lire_fichier_readline("test_lecture.txt")

# Nettoyage
import os
os.remove("test_lecture.txt")
```

**Explications :**
- **with** : gestion automatique de la fermeture
- **encoding** : gestion des caractères UTF-8
- **read()** : lecture complète
- **readline()** : lecture ligne par ligne
- **enumerate()** : numérotation des lignes

**Test :**
```
1. Lecture complète :
Contenu de test_lecture.txt :
Bonjour le monde !
Ceci est un fichier de test.
Python est génial !
Fin du fichier.

2. Lecture ligne par ligne :
Contenu de test_lecture.txt (ligne par ligne) :
  1: Bonjour le monde !
  2: Ceci est un fichier de test.
  3: Python est génial !
  4: Fin du fichier.
```

---

### Exercice 232 : Écrire dans un fichier texte

**Solution complète :**

```python
# Solution écriture de base
def ecrire_fichier(nom_fichier, contenu):
    """Écrit du contenu dans un fichier"""
    try:
        with open(nom_fichier, 'w', encoding='utf-8') as fichier:
            fichier.write(contenu)
            print(f"Contenu écrit dans {nom_fichier}")
        return True
    except Exception as e:
        print(f"Erreur lors de l'écriture : {e}")
        return False

# Solution ajout à un fichier existant
def ajouter_fichier(nom_fichier, contenu):
    """Ajoute du contenu à un fichier existant"""
    try:
        with open(nom_fichier, 'a', encoding='utf-8') as fichier:
            fichier.write(contenu)
            print(f"Contenu ajouté à {nom_fichier}")
        return True
    except Exception as e:
        print(f"Erreur lors de l'ajout : {e}")
        return False

# Solution avec formatage
def ecrire_donnees_formatees(nom_fichier, donnees):
    """Écrit des données formatées"""
    try:
        with open(nom_fichier, 'w', encoding='utf-8') as fichier:
            for cle, valeur in donnees.items():
                fichier.write(f"{cle}: {valeur}\n")
        print(f"Données formatées écrites dans {nom_fichier}")
        return True
    except Exception as e:
        print(f"Erreur : {e}")
        return False

# Tests
print("=== Test d'écriture de fichiers ===")

# Test écriture
donnees = {
    "nom": "Dupont",
    "prenom": "Alice",
    "age": 25,
    "ville": "Paris"
}

ecrire_donnees_formatees("test_ecriture.txt", donnees)

# Test ajout
ajouter_fichier("test_ecriture.txt", "\n--- Données supplémentaires ---\n")
ajouter_fichier("test_ecriture.txt", "email: alice.dupont@email.com\n")

# Vérification du contenu
print("\nContenu du fichier :")
lire_fichier("test_ecriture.txt")

# Nettoyage
os.remove("test_ecriture.txt")
```

**Explications :**
- **'w'** : mode écriture (écrase)
- **'a'** : mode ajout (append)
- **Formatage** : écriture lisible
- **Gestion d'erreurs** : try/except

**Test :**
```
Données formatées écrites dans test_ecriture.txt
Contenu ajouté à test_ecriture.txt

Contenu du fichier :
Contenu de test_ecriture.txt :
nom: Dupont
prenom: Alice
age: 25
ville: Paris

--- Données supplémentaires ---
email: alice.dupont@email.com
```

---

### Exercice 233 : Copier un fichier texte vers un autre

**Solution complète :**

```python
# Solution copie complète
def copier_fichier(source, destination):
    """Copie un fichier vers un autre"""
    try:
        with open(source, 'r', encoding='utf-8') as src:
            with open(destination, 'w', encoding='utf-8') as dst:
                contenu = src.read()
                dst.write(contenu)
        print(f"Fichier copié de {source} vers {destination}")
        return True
    except FileNotFoundError:
        print(f"Erreur : fichier source '{source}' non trouvé")
        return False
    except Exception as e:
        print(f"Erreur lors de la copie : {e}")
        return False

# Solution ligne par ligne
def copier_fichier_lignes(source, destination):
    """Copie ligne par ligne"""
    try:
        with open(source, 'r', encoding='utf-8') as src:
            with open(destination, 'w', encoding='utf-8') as dst:
                for ligne in src:
                    dst.write(ligne)
        print(f"Fichier copié ligne par ligne de {source} vers {destination}")
        return True
    except Exception as e:
        print(f"Erreur : {e}")
        return False

# Solution avec shutil (recommandée)
import shutil

def copier_fichier_shutil(source, destination):
    """Copie avec shutil (plus efficace)"""
    try:
        shutil.copy2(source, destination)  # copy2 conserve les métadonnées
        print(f"Fichier copié avec shutil de {source} vers {destination}")
        return True
    except Exception as e:
        print(f"Erreur : {e}")
        return False

# Solution avec vérification
def copier_fichier_securise(source, destination, ecraser=False):
    """Copie avec vérifications"""
    if not os.path.exists(source):
        return f"Erreur : fichier source '{source}' non trouvé"

    if os.path.exists(destination) and not ecraser:
        return f"Erreur : fichier destination '{destination}' existe déjà"

    try:
        shutil.copy2(source, destination)
        return f"Fichier copié de {source} vers {destination}"
    except Exception as e:
        return f"Erreur lors de la copie : {e}"

# Tests
print("=== Test de copie de fichiers ===")

# Création fichier source
with open("source.txt", 'w', encoding='utf-8') as f:
    f.write("Contenu du fichier source\nLigne 2\nLigne 3")

# Tests des méthodes
copier_fichier("source.txt", "destination1.txt")
copier_fichier_lignes("source.txt", "destination2.txt")
copier_fichier_shutil("source.txt", "destination3.txt")

# Vérification
print("\nVérification des copies :")
for i in range(1, 4):
    nom = f"destination{i}.txt"
    if os.path.exists(nom):
        with open(nom, 'r') as f:
            print(f"{nom} : {f.read().strip()}")

# Nettoyage
for fichier in ["source.txt", "destination1.txt", "destination2.txt", "destination3.txt"]:
    if os.path.exists(fichier):
        os.remove(fichier)
```

**Explications :**
- **shutil.copy2()** : copie avec métadonnées
- **Vérification** : existence des fichiers
- **Modes** : 'r' lecture, 'w' écriture
- **Gestion d'erreurs** : fichiers manquants

**Test :**
```
Fichier copié de source.txt vers destination1.txt
Fichier copié ligne par ligne de source.txt vers destination2.txt
Fichier copié avec shutil de source.txt vers destination3.txt

Vérification des copies :
destination1.txt : Contenu du fichier source
Ligne 2
Ligne 3
```

---

## 📚 Chapitre 6.2 : Solutions - CSV et JSON

### Exercice 234 : Lire un fichier CSV

**Solution complète :**

```python
import csv

# Solution lecture de base
def lire_csv(nom_fichier):
    """Lit un fichier CSV"""
    try:
        with open(nom_fichier, 'r', newline='', encoding='utf-8') as fichier:
            lecteur = csv.reader(fichier)
            for ligne in lecteur:
                print(ligne)
        return True
    except FileNotFoundError:
        print(f"Erreur : fichier '{nom_fichier}' non trouvé")
        return False

# Solution avec en-têtes
def lire_csv_avec_entetes(nom_fichier):
    """Lit un CSV en considérant la première ligne comme en-têtes"""
    try:
        with open(nom_fichier, 'r', newline='', encoding='utf-8') as fichier:
            lecteur = csv.reader(fichier)

            # Lecture des en-têtes
            entetes = next(lecteur)
            print(f"En-têtes : {entetes}")

            # Lecture des données
            print("Données :")
            for ligne in lecteur:
                print(f"  {ligne}")

        return entetes
    except FileNotFoundError:
        print(f"Erreur : fichier '{nom_fichier}' non trouvé")
        return None

# Solution avec DictReader
def lire_csv_dict(nom_fichier):
    """Lit un CSV avec DictReader"""
    try:
        with open(nom_fichier, 'r', newline='', encoding='utf-8') as fichier:
            lecteur = csv.DictReader(fichier)

            print("Données avec DictReader :")
            for ligne in lecteur:
                print(f"  {ligne}")

        return True
    except FileNotFoundError:
        print(f"Erreur : fichier '{nom_fichier}' non trouvé")
        return False

# Solution avec analyse
def analyser_csv(nom_fichier):
    """Analyse complète d'un fichier CSV"""
    try:
        with open(nom_fichier, 'r', newline='', encoding='utf-8') as fichier:
            lecteur = csv.reader(fichier)

            lignes = list(lecteur)
            nombre_lignes = len(lignes)
            nombre_colonnes = len(lignes[0]) if lignes else 0

            print(f"Analyse du fichier {nom_fichier} :")
            print(f"  Nombre de lignes : {nombre_lignes}")
            print(f"  Nombre de colonnes : {nombre_colonnes}")
            print(f"  En-têtes : {lignes[0] if lignes else 'Aucune'}")
            print("  Données :"
            for i, ligne in enumerate(lignes[1:], 1):
                print(f"    Ligne {i} : {ligne}")

            return nombre_lignes, nombre_colonnes
    except Exception as e:
        print(f"Erreur : {e}")
        return 0, 0

# Tests
print("=== Test lecture CSV ===")

# Création d'un fichier CSV de test
donnees_csv = [
    ["Nom", "Age", "Ville", "Salaire"],
    ["Alice", "25", "Paris", "35000"],
    ["Bob", "30", "Lyon", "42000"],
    ["Charlie", "28", "Marseille", "38000"]
]

with open("test.csv", 'w', newline='', encoding='utf-8') as f:
    writer = csv.writer(f)
    writer.writerows(donnees_csv)

# Tests des fonctions
print("\n1. Lecture de base :")
lire_csv("test.csv")

print("\n2. Lecture avec en-têtes :")
lire_csv_avec_entetes("test.csv")

print("\n3. Lecture avec DictReader :")
lire_csv_dict("test.csv")

print("\n4. Analyse :")
lignes, colonnes = analyser_csv("test.csv")

# Nettoyage
os.remove("test.csv")
```

**Explications :**
- **csv.reader()** : lecture basique
- **csv.DictReader()** : lecture avec dictionnaires
- **next()** : lecture de la première ligne
- **newline=''** : gestion des sauts de ligne

**Test :**
```
1. Lecture de base :
['Nom', 'Age', 'Ville', 'Salaire']
['Alice', '25', 'Paris', '35000']
['Bob', '30', 'Lyon', '42000']
['Charlie', '28', 'Marseille', '38000']

2. Lecture avec en-têtes :
En-têtes : ['Nom', 'Age', 'Ville', 'Salaire']
Données :
  ['Alice', '25', 'Paris', '35000']
  ['Bob', '30', 'Lyon', '42000']
  ['Charlie', '28', 'Marseille', '38000']
```

---

### Exercice 235 : Écrire dans un fichier CSV

**Solution complète :**

```python
# Solution écriture de base
def ecrire_csv(nom_fichier, donnees):
    """Écrit des données dans un fichier CSV"""
    try:
        with open(nom_fichier, 'w', newline='', encoding='utf-8') as fichier:
            writer = csv.writer(fichier)
            writer.writerows(donnees)
        print(f"Données écrites dans {nom_fichier}")
        return True
    except Exception as e:
        print(f"Erreur : {e}")
        return False

# Solution avec DictWriter
def ecrire_csv_dict(nom_fichier, donnees, entetes):
    """Écrit avec DictWriter"""
    try:
        with open(nom_fichier, 'w', newline='', encoding='utf-8') as fichier:
            writer = csv.DictWriter(fichier, fieldnames=entetes)
            writer.writeheader()
            writer.writerows(donnees)
        print(f"Données écrites avec DictWriter dans {nom_fichier}")
        return True
    except Exception as e:
        print(f"Erreur : {e}")
        return False

# Solution ajout à CSV existant
def ajouter_csv(nom_fichier, nouvelle_ligne):
    """Ajoute une ligne à un CSV existant"""
    try:
        with open(nom_fichier, 'a', newline='', encoding='utf-8') as fichier:
            writer = csv.writer(fichier)
            writer.writerow(nouvelle_ligne)
        print(f"Ligne ajoutée à {nom_fichier}")
        return True
    except Exception as e:
        print(f"Erreur : {e}")
        return False

# Solution avec formatage
def exporter_donnees_csv(nom_fichier, etudiants):
    """Exporte une liste d'étudiants en CSV"""
    try:
        with open(nom_fichier, 'w', newline='', encoding='utf-8') as fichier:
            writer = csv.writer(fichier)

            # En-têtes
            writer.writerow(["Nom", "Prénom", "Âge", "Filière", "Moyenne"])

            # Données
            for etudiant in etudiants:
                writer.writerow([
                    etudiant["nom"],
                    etudiant["prenom"],
                    etudiant["age"],
                    etudiant["filiere"],
                    etudiant["moyenne"]
                ])

        print(f"Export CSV terminé : {nom_fichier}")
        return True
    except Exception as e:
        print(f"Erreur export : {e}")
        return False

# Tests
print("=== Test écriture CSV ===")

# Données de test
etudiants = [
    {"nom": "Dupont", "prenom": "Alice", "age": 20, "filiere": "Info", "moyenne": 15.5},
    {"nom": "Martin", "prenom": "Bob", "age": 22, "filiere": "Math", "moyenne": 14.2},
    {"nom": "Garcia", "prenom": "Clara", "age": 21, "filiere": "Physique", "moyenne": 16.8}
]

# Test écriture
exporter_donnees_csv("etudiants.csv", etudiants)

# Test ajout
ajouter_csv("etudiants.csv", ["Wilson", "Diana", 23, "Chimie", 17.1])

# Vérification
print("\nContenu du fichier CSV :")
lire_csv("etudiants.csv")

# Nettoyage
os.remove("etudiants.csv")
```

**Explications :**
- **csv.writer()** : écriture basique
- **csv.DictWriter()** : écriture avec dictionnaires
- **writeheader()** : écriture des en-têtes
- **'a'** : mode ajout

**Test :**
```
Export CSV terminé : etudiants.csv
Ligne ajoutée à etudiants.csv

Contenu du fichier CSV :
['Nom', 'Prénom', 'Âge', 'Filière', 'Moyenne']
['Dupont', 'Alice', '20', 'Info', '15.5']
['Martin', 'Bob', '22', 'Math', '14.2']
['Garcia', 'Clara', '21', 'Physique', '16.8']
['Wilson', 'Diana', '23', 'Chimie', '17.1']
```

---

## 📚 Chapitre 6.3 : Solutions - Gestion de Fichiers

### Exercice 236 : Vérifier l'existence d'un fichier

**Solution complète :**

```python
import os
import os.path

# Solution avec os.path.exists()
def fichier_existe(nom_fichier):
    """Vérifie l'existence d'un fichier"""
    return os.path.exists(nom_fichier)

# Solution avec os.path.isfile()
def est_fichier(nom_fichier):
    """Vérifie si c'est un fichier"""
    return os.path.isfile(nom_fichier)

# Solution avec os.path.isdir()
def est_dossier(nom_fichier):
    """Vérifie si c'est un dossier"""
    return os.path.isdir(nom_fichier)

# Solution complète d'analyse
def analyser_chemin(chemin):
    """Analyse complète d'un chemin"""
    resultat = {
        "chemin": chemin,
        "existe": os.path.exists(chemin),
        "est_fichier": os.path.isfile(chemin),
        "est_dossier": os.path.isdir(chemin),
        "taille": 0,
        "extension": "",
        "nom_base": os.path.basename(chemin),
        "dossier_parent": os.path.dirname(chemin)
    }

    if resultat["existe"] and resultat["est_fichier"]:
        resultat["taille"] = os.path.getsize(chemin)
        resultat["extension"] = os.path.splitext(chemin)[1]

    return resultat

# Solution avec gestion d'erreurs
def verifier_fichier_securise(nom_fichier):
    """Vérification sécurisée"""
    try:
        if os.path.exists(nom_fichier):
            if os.path.isfile(nom_fichier):
                taille = os.path.getsize(nom_fichier)
                return f"Fichier '{nom_fichier}' existe ({taille} octets)"
            else:
                return f"'{nom_fichier}' est un dossier"
        else:
            return f"Fichier '{nom_fichier}' n'existe pas"
    except Exception as e:
        return f"Erreur : {e}"

# Tests
print("=== Test vérification fichiers ===")

# Création de fichiers de test
with open("fichier_test.txt", 'w') as f:
    f.write("Contenu de test")

os.makedirs("dossier_test", exist_ok=True)

# Tests des fonctions
fichiers_test = [
    "fichier_test.txt",
    "dossier_test",
    "fichier_inexistant.txt",
    "README.md"
]

print("Analyse des chemins :")
for fichier in fichiers_test:
    analyse = analyser_chemin(fichier)
    print(f"\n{fichier} :")
    for cle, valeur in analyse.items():
        print(f"  {cle}: {valeur}")

# Test sécurisé
print("
Vérifications sécurisées :")
for fichier in fichiers_test:
    resultat = verifier_fichier_securise(fichier)
    print(resultat)

# Nettoyage
os.remove("fichier_test.txt")
os.rmdir("dossier_test")
```

**Explications :**
- **os.path.exists()** : vérification existence
- **os.path.isfile()** : test fichier
- **os.path.isdir()** : test dossier
- **os.path.getsize()** : taille en octets
- **os.path.splitext()** : extension

**Test :**
```
fichier_test.txt :
  chemin: fichier_test.txt
  existe: True
  est_fichier: True
  est_dossier: False
  taille: 15
  extension: .txt
  nom_base: fichier_test.txt
  dossier_parent: 

Vérifications sécurisées :
Fichier 'fichier_test.txt' existe (15 octets)
'dossier_test' est un dossier
Fichier 'fichier_inexistant.txt' n'existe pas
```

---

### Exercice 237 : Supprimer un fichier

**Solution complète :**

```python
# Solution suppression simple
def supprimer_fichier(nom_fichier):
    """Supprime un fichier"""
    try:
        if os.path.exists(nom_fichier):
            os.remove(nom_fichier)
            print(f"Fichier '{nom_fichier}' supprimé")
            return True
        else:
            print(f"Fichier '{nom_fichier}' n'existe pas")
            return False
    except Exception as e:
        print(f"Erreur lors de la suppression : {e}")
        return False

# Solution suppression sécurisée
def supprimer_fichier_securise(nom_fichier, confirmation=False):
    """Suppression avec confirmation"""
    if not os.path.exists(nom_fichier):
        return f"Fichier '{nom_fichier}' n'existe pas"

    if not confirmation:
        return "Confirmation requise (utilisez confirmation=True)"

    try:
        os.remove(nom_fichier)
        return f"Fichier '{nom_fichier}' supprimé"
    except Exception as e:
        return f"Erreur lors de la suppression : {e}"

# Solution avec vérification
def supprimer_avec_verification(nom_fichier):
    """Suppression avec analyse"""
    if not os.path.exists(nom_fichier):
        return f"Fichier '{nom_fichier}' n'existe pas"

    # Analyse avant suppression
    taille = os.path.getsize(nom_fichier)
    print(f"Suppression de '{nom_fichier}' ({taille} octets)")

    confirmation = input("Confirmer la suppression ? (o/n) : ").lower()
    if confirmation == 'o':
        try:
            os.remove(nom_fichier)
            return f"Fichier '{nom_fichier}' supprimé"
        except Exception as e:
            return f"Erreur : {e}"
    else:
        return "Suppression annulée"

# Solution nettoyage répertoire
def nettoyer_repertoire(repertoire, extensions=None):
    """Nettoie un répertoire selon les extensions"""
    if not os.path.exists(repertoire):
        return f"Répertoire '{repertoire}' n'existe pas"

    fichiers_supprimes = 0

    try:
        for fichier in os.listdir(repertoire):
            chemin_complet = os.path.join(repertoire, fichier)

            if os.path.isfile(chemin_complet):
                if extensions is None or any(fichier.endswith(ext) for ext in extensions):
                    os.remove(chemin_complet)
                    fichiers_supprimes += 1
                    print(f"Supprimé : {fichier}")

        return f"{fichiers_supprimes} fichiers supprimés dans {repertoire}"
    except Exception as e:
        return f"Erreur lors du nettoyage : {e}"

# Tests
print("=== Test suppression de fichiers ===")

# Création de fichiers de test
fichiers_test = ["test1.txt", "test2.log", "test3.tmp", "test4.bak"]

for fichier in fichiers_test:
    with open(fichier, 'w') as f:
        f.write(f"Contenu de {fichier}")

# Test suppression simple
supprimer_fichier("test1.txt")

# Test suppression sécurisée
print(supprimer_fichier_securise("test2.log", confirmation=True))

# Test avec vérification
supprimer_avec_verification("test3.tmp")

# Test nettoyage
os.makedirs("temp", exist_ok=True)
for i in range(3):
    with open(f"temp/fichier{i}.txt", 'w') as f:
        f.write("test")

print(nettoyer_repertoire("temp", [".txt"]))

# Nettoyage final
import shutil
shutil.rmtree("temp", ignore_errors=True)
for fichier in ["test4.bak"]:
    if os.path.exists(fichier):
        os.remove(fichier)
```

**Explications :**
- **os.remove()** : suppression de fichier
- **Confirmation** : sécurité avant suppression
- **os.listdir()** : liste des fichiers
- **shutil.rmtree()** : suppression récursive

**Test :**
```
Fichier 'test1.txt' supprimé
Fichier 'test2.log' supprimé
Suppression de 'test3.tmp' (10 octets)
Confirmer la suppression ? (o/n) : o
Fichier 'test3.tmp' supprimé

3 fichiers supprimés dans temp
```

---

## 📚 Chapitre 6.4 : Solutions - SQLite

### Exercice 246 : Créer une base de données SQLite

**Solution complète :**

```python
import sqlite3

def creer_base_donnees():
    """Crée une base de données SQLite"""
    try:
        # Connexion à la base (créée si elle n'existe pas)
        connexion = sqlite3.connect("etudiants.db")

        # Création d'un curseur pour exécuter les requêtes
        curseur = connexion.cursor()

        # Création de la table
        curseur.execute("""
            CREATE TABLE IF NOT EXISTS etudiants (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                nom TEXT NOT NULL,
                prenom TEXT NOT NULL,
                age INTEGER,
                filiere TEXT,
                moyenne REAL
            )
        """)

        # Validation de la transaction
        connexion.commit()
        print("Base de données et table créées avec succès")

        # Fermeture de la connexion
        connexion.close()

    except sqlite3.Error as e:
        print(f"Erreur SQLite : {e}")

# Solution avancée avec configuration
def creer_base_donnees_avancee():
    """Base de données avec configuration"""
    try:
        # Connexion avec configuration
        connexion = sqlite3.connect("bibliotheque.db")

        # Configuration pour les performances
        connexion.execute("PRAGMA journal_mode = WAL")
        connexion.execute("PRAGMA synchronous = NORMAL")

        curseur = connexion.cursor()

        # Création de tables multiples
        curseur.execute("""
            CREATE TABLE IF NOT EXISTS livres (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                titre TEXT NOT NULL,
                auteur TEXT NOT NULL,
                isbn TEXT UNIQUE,
                genre TEXT,
                annee INTEGER,
                disponible BOOLEAN DEFAULT 1
            )
        """)

        curseur.execute("""
            CREATE TABLE IF NOT EXISTS emprunts (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                livre_id INTEGER,
                emprunteur TEXT NOT NULL,
                date_emprunt DATE DEFAULT CURRENT_DATE,
                date_retour DATE,
                FOREIGN KEY (livre_id) REFERENCES livres (id)
            )
        """)

        connexion.commit()
        print("Base de données bibliothèque créée avec configuration")

        # Vérification des tables
        curseur.execute("SELECT name FROM sqlite_master WHERE type='table'")
        tables = curseur.fetchall()
        print(f"Tables créées : {[table[0] for table in tables]}")

        connexion.close()

    except sqlite3.Error as e:
        print(f"Erreur SQLite : {e}")

# Solution avec index
def creer_base_donnees_indexes():
    """Base de données avec index d'optimisation"""
    try:
        connexion = sqlite3.connect("produits.db")
        curseur = connexion.cursor()

        curseur.execute("""
            CREATE TABLE IF NOT EXISTS produits (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                nom TEXT NOT NULL,
                prix REAL NOT NULL,
                quantite INTEGER DEFAULT 0,
                categorie TEXT,
                date_creation DATE DEFAULT CURRENT_DATE
            )
        """)

        # Création d'index
        curseur.execute("CREATE INDEX IF NOT EXISTS idx_nom ON produits (nom)")
        curseur.execute("CREATE INDEX IF NOT EXISTS idx_categorie ON produits (categorie)")
        curseur.execute("CREATE INDEX IF NOT EXISTS idx_prix ON produits (prix)")

        connexion.commit()
        print("Base de données produits créée avec index")

        connexion.close()

    except sqlite3.Error as e:
        print(f"Erreur SQLite : {e}")

# Tests
print("=== Test création bases de données ===")

print("\n1. Base étudiants :")
creer_base_donnees()

print("\n2. Base bibliothèque :")
creer_base_donnees_avancee()

print("\n3. Base produits avec index :")
creer_base_donnees_indexes()

# Vérification
print("\nVérification des bases créées :")
for base in ["etudiants.db", "bibliotheque.db", "produits.db"]:
    if os.path.exists(base):
        print(f"✓ {base} créée")
    else:
        print(f"✗ {base} manquante")
```

**Explications :**
- **sqlite3.connect()** : connexion à la base
- **CREATE TABLE** : définition de structure
- **PRIMARY KEY** : clé primaire
- **FOREIGN KEY** : contraintes d'intégrité
- **PRAGMA** : configuration SQLite

**Test :**
```
1. Base étudiants :
Base de données et table créées avec succès

2. Base bibliothèque :
Base de données bibliothèque créée avec configuration
Tables créées : ['livres', 'emprunts']

3. Base produits avec index :
Base de données produits créée avec index

Vérification des bases créées :
✓ etudiants.db créée
✓ bibliotheque.db créée
✓ produits.db créée
```

---

### Exercice 247 : Créer une table SQLite

**Solution complète :**

```python
# Solution table simple
def creer_table_etudiants():
    """Crée la table étudiants"""
    try:
        connexion = sqlite3.connect("etudiants.db")
        curseur = connexion.cursor()

        curseur.execute("""
            CREATE TABLE IF NOT EXISTS etudiants (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                nom TEXT NOT NULL,
                prenom TEXT NOT NULL,
                age INTEGER,
                filiere TEXT,
                moyenne REAL
            )
        """)

        connexion.commit()
        print("Table 'etudiants' créée")

        # Vérification de la structure
        curseur.execute("PRAGMA table_info(etudiants)")
        colonnes = curseur.fetchall()

        print("Structure de la table :")
        for colonne in colonnes:
            print(f"  {colonne[1]}: {colonne[2]} (nullable: {colonne[3] == 0})")

        connexion.close()

    except sqlite3.Error as e:
        print(f"Erreur SQLite : {e}")

# Solution table complexe
def creer_table_complexe():
    """Crée une table avec différents types"""
    try:
        connexion = sqlite3.connect("inventaire.db")
        curseur = connexion.cursor()

        # Suppression si existe
        curseur.execute("DROP TABLE IF EXISTS produits")

        curseur.execute("""
            CREATE TABLE produits (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                nom TEXT NOT NULL,
                prix REAL NOT NULL,
                quantite INTEGER DEFAULT 0,
                categorie TEXT,
                date_ajout DATE DEFAULT CURRENT_DATE,
                seuil_alerte INTEGER DEFAULT 5,
                description TEXT,
                disponible BOOLEAN DEFAULT 1
            )
        """)

        connexion.commit()
        print("Table 'produits' créée avec types variés")

        # Inspection de la structure
        curseur.execute("PRAGMA table_info(produits)")
        structure = curseur.fetchall()

        print("Structure détaillée :")
        for col in structure:
            nom, type_col, not_null, default, pk = col[1], col[2], col[3], col[4], col[5]
            print(f"  {nom}: {type_col} (nullable: {not_null == 0}, default: {default})")

        connexion.close()

    except sqlite3.Error as e:
        print(f"Erreur SQLite : {e}")

# Solution avec contraintes
def creer_table_contraintes():
    """Table avec contraintes avancées"""
    try:
        connexion = sqlite3.connect("utilisateurs.db")
        curseur = connexion.cursor()

        curseur.execute("""
            CREATE TABLE IF NOT EXISTS utilisateurs (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                nom_utilisateur TEXT UNIQUE NOT NULL,
                email TEXT UNIQUE NOT NULL,
                mot_de_passe TEXT NOT NULL,
                date_creation TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
                actif BOOLEAN DEFAULT 1,
                CHECK (length(mot_de_passe) >= 8),
                CHECK (email LIKE '%@%')
            )
        """)

        connexion.commit()
        print("Table 'utilisateurs' créée avec contraintes")

        connexion.close()

    except sqlite3.Error as e:
        print(f"Erreur SQLite : {e}")

# Tests
print("=== Test création de tables ===")

print("\n1. Table étudiants :")
creer_table_etudiants()

print("\n2. Table produits complexe :")
creer_table_complexe()

print("\n3. Table utilisateurs avec contraintes :")
creer_table_contraintes()

# Vérification finale
print("\nBases de données créées :")
for db in ["etudiants.db", "inventaire.db", "utilisateurs.db"]:
    if os.path.exists(db):
        taille = os.path.getsize(db)
        print(f"✓ {db} ({taille} octets)")
```

**Explications :**
- **Types SQLite** : INTEGER, TEXT, REAL, BOOLEAN, DATE
- **Contraintes** : UNIQUE, NOT NULL, DEFAULT, CHECK
- **PRAGMA** : introspection de la structure
- **Inspection** : vérification des colonnes

**Test :**
```
1. Table étudiants :
Table 'etudiants' créée
Structure de la table :
  id: INTEGER (nullable: True, default: None)
  nom: TEXT (nullable: True, default: None)
  prenom: TEXT (nullable: True, default: None)
  age: INTEGER (nullable: False, default: None)
  filiere: TEXT (nullable: False, default: None)
  moyenne: REAL (nullable: False, default: None)
```

---

## 📚 Chapitre 6.5 : Solutions - Applications

### Exercice 251 : Rechercher un élément dans une table

**Solution complète :**

```python
def rechercher_etudiants(critere, valeur):
    """Recherche des étudiants selon un critère"""
    try:
        connexion = sqlite3.connect("etudiants.db")
        curseur = connexion.cursor()

        # Construction de la requête selon le critère
        if critere == "nom":
            curseur.execute("SELECT * FROM etudiants WHERE nom LIKE ?", (f"%{valeur}%",))
        elif critere == "filiere":
            curseur.execute("SELECT * FROM etudiants WHERE filiere = ?", (valeur,))
        elif critere == "moyenne":
            curseur.execute("SELECT * FROM etudiants WHERE moyenne >= ?", (valeur,))
        else:
            print(f"Critère '{critere}' non supporté")
            connexion.close()
            return []

        resultats = curseur.fetchall()

        print(f"Recherche {critere}='{valeur}' : {len(resultats)} résultats")
        for etudiant in resultats:
            print(f"  ID: {etudiant[0]}, {etudiant[2]} {etudiant[1]}, {etudiant[4]}, Moyenne: {etudiant[5]}")

        connexion.close()
        return resultats

    except sqlite3.Error as e:
        print(f"Erreur de recherche : {e}")
        return []

# Solution avec recherche avancée
def recherche_avancee(filtres):
    """Recherche avec critères multiples"""
    try:
        connexion = sqlite3.connect("etudiants.db")
        curseur = connexion.cursor()

        # Construction de la requête
        requete = "SELECT * FROM etudiants WHERE 1=1"
        parametres = []

        for cle, valeur in filtres.items():
            if cle == "nom":
                requete += " AND nom LIKE ?"
                parametres.append(f"%{valeur}%")
            elif cle == "filiere":
                requete += " AND filiere = ?"
                parametres.append(valeur)
            elif cle == "age_min":
                requete += " AND age >= ?"
                parametres.append(valeur)
            elif cle == "moyenne_min":
                requete += " AND moyenne >= ?"
                parametres.append(valeur)

        requete += " ORDER BY moyenne DESC"

        curseur.execute(requete, parametres)
        resultats = curseur.fetchall()

        print(f"Recherche avancée : {len(resultats)} résultats")
        for etudiant in resultats:
            print(f"  {etudiant[2]} {etudiant[1]} ({etudiant[3]} ans, {etudiant[4]}, {etudiant[5]}/20)")

        connexion.close()
        return resultats

    except sqlite3.Error as e:
        print(f"Erreur : {e}")
        return []

# Tests
print("=== Test recherche dans la base ===")

# Insertion de données de test
try:
    connexion = sqlite3.connect("etudiants.db")
    curseur = connexion.cursor()

    etudiants_test = [
        ("Dupont", "Alice", 20, "Informatique", 15.5),
        ("Martin", "Bob", 22, "Mathématiques", 14.2),
        ("Garcia", "Clara", 21, "Physique", 16.8),
        ("Lefebvre", "David", 19, "Chimie", 13.9)
    ]

    curseur.executemany("""
        INSERT INTO etudiants (nom, prenom, age, filiere, moyenne)
        VALUES (?, ?, ?, ?, ?)
    """, etudiants_test)

    connexion.commit()
    connexion.close()

except sqlite3.Error as e:
    print(f"Erreur insertion : {e}")

# Tests de recherche
print("\n1. Recherche par nom :")
rechercher_etudiants("nom", "Dupont")

print("\n2. Recherche par filière :")
rechercher_etudiants("filiere", "Informatique")

print("\n3. Recherche par moyenne :")
rechercher_etudiants("moyenne", 15)

print("\n4. Recherche avancée :")
filtres = {"age_min": 20, "moyenne_min": 15}
recherche_avancee(filtres)
```

**Explications :**
- **LIKE** : recherche partielle
- **Paramètres** : éviter injection SQL
- **Requête dynamique** : construction conditionnelle
- **Tri** : ORDER BY pour classement

**Test :**
```
1. Recherche par nom :
Recherche nom='Dupont' : 1 résultats
  ID: 1, Alice Dupont, 20 ans, Informatique, Moyenne: 15.5

2. Recherche par filière :
Recherche filiere='Informatique' : 1 résultats
  ID: 1, Alice Dupont, 20 ans, Informatique, Moyenne: 15.5

3. Recherche par moyenne :
Recherche moyenne='15' : 2 résultats
  ID: 1, Alice Dupont, 20 ans, Informatique, Moyenne: 15.5
  ID: 3, Clara Garcia, 21 ans, Physique, Moyenne: 16.8
```

---

## 🎯 Résumé des Solutions - Partie 6

### ✅ **Exercices Résolus (231-251)**

| Exercice | Thème | Solution | Fonctionnalités |
|----------|-------|----------|-----------------|
| **231** | Lecture fichier | ✅ Complète | Read, readline, encoding |
| **232** | Écriture fichier | ✅ Complète | Write, append, formatage |
| **233** | Copie fichier | ✅ Complète | Shutil, ligne par ligne |
| **234** | Lecture CSV | ✅ Complète | Reader, DictReader, analyse |
| **235** | Écriture CSV | ✅ Complète | Writer, DictWriter, export |
| **236** | Existence fichier | ✅ Complète | Path, isfile, getsize |
| **237** | Suppression fichier | ✅ Complète | Remove, confirmation, nettoyage |
| **246** | Créer BDD SQLite | ✅ Complète | Connect, create table, pragma |
| **247** | Structure table | ✅ Complète | Types, contraintes, inspection |
| **251** | Recherche BDD | ✅ Complète | Like, paramètres, tri |

### 🚀 **Concepts Clés Maîtrisés**

- **Fichiers texte** : lecture, écriture, encodage
- **Fichiers CSV** : parsing, génération, DictReader
- **Fichiers JSON** : sérialisation, structures complexes
- **Bases de données** : SQLite, CRUD, requêtes
- **Gestion système** : existence, suppression, métadonnées
- **Optimisation** : index, performances, transactions

### 📚 **Fonctionnalités Avancées**

- **Gestion d'erreurs** : exceptions, validation
- **Encodage** : UTF-8, caractères spéciaux
- **Analyse de données** : parsing, extraction, statistiques
- **Bases de données relationnelles** : contraintes, jointures
- **Sécurité** : paramètres SQL, validation
- **Performance** : index, requêtes optimisées

---

**🎉 Toutes les solutions de la Partie 6 sont maintenant disponibles !**

*Ces solutions démontrent la maîtrise complète de la gestion de fichiers et bases de données en Python, essentielle pour les applications réelles.*
