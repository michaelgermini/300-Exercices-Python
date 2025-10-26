# Partie 6.1 : Fichiers Texte

## 🎯 Objectifs Pédagogiques

Ce chapitre explore la **gestion de fichiers texte** en Python, essentielle pour la **persistance de données** et l'**échange d'informations**. Nous apprendrons à lire, écrire et manipuler des fichiers.

### Concepts Abordés
- **Ouverture et fermeture** : with statement, modes d'ouverture
- **Lecture** : ligne par ligne, tout le fichier
- **Écriture** : création, ajout, formatage
- **Applications** : sauvegarde, configuration, logs

---

## 📝 Exercices Pratiques

### Exercice 231 : Lire un fichier texte et afficher son contenu
**Objectif** : Ouvrir et lire le contenu d'un fichier texte.

```python
# Solution
def lire_fichier(nom_fichier):
    """Lit et affiche le contenu d'un fichier"""
    try:
        with open(nom_fichier, 'r', encoding='utf-8') as fichier:
            contenu = fichier.read()
            print(f"Contenu de {nom_fichier} :")
            print(contenu)
            return contenu
    except FileNotFoundError:
        print(f"Erreur : Le fichier '{nom_fichier}' n'existe pas")
        return None
    except Exception as e:
        print(f"Erreur lors de la lecture : {e}")
        return None

# Test
contenu = lire_fichier("mon_fichier.txt")
if contenu:
    print(f"\nLongueur du contenu : {len(contenu)} caractères")
```

**Explication** :
- **with open()** : gestion automatique de la fermeture
- **encoding='utf-8'** : gestion des caractères spéciaux
- **.read()** : lit tout le contenu
- **Gestion d'erreurs** : FileNotFoundError et autres exceptions

**Test** : Créez un fichier "mon_fichier.txt" avec du texte et testez.

---

### Exercice 232 : Compter le nombre de mots dans un fichier texte
**Objectif** : Analyser le contenu d'un fichier et compter les mots.

```python
# Solution
def compter_mots_fichier(nom_fichier):
    """Compte le nombre de mots dans un fichier"""
    try:
        with open(nom_fichier, 'r', encoding='utf-8') as fichier:
            contenu = fichier.read()

        # Nettoyage et comptage
        mots = contenu.split()  # Séparation par espaces
        nombre_mots = len(mots)

        print(f"Fichier '{nom_fichier}' contient {nombre_mots} mots")
        return nombre_mots

    except FileNotFoundError:
        print(f"Erreur : Le fichier '{nom_fichier}' n'existe pas")
        return 0
    except Exception as e:
        print(f"Erreur lors de l'analyse : {e}")
        return 0

# Test
nombre = compter_mots_fichier("mon_fichier.txt")
print(f"Nombre de mots retourné : {nombre}")
```

**Explication** :
- **.split()** : sépare le texte en mots
- **len()** : compte les éléments de la liste
- **Nettoyage implicite** : les espaces multiples sont gérés
- **Robustesse** : gestion des erreurs

**Test** : Comptez les mots dans votre fichier de test.

---

### Exercice 233 : Écrire du texte dans un fichier
**Objectif** : Créer un fichier et y écrire du contenu.

```python
# Solution
def ecrire_fichier(nom_fichier, contenu):
    """Écrit du contenu dans un fichier"""
    try:
        with open(nom_fichier, 'w', encoding='utf-8') as fichier:
            fichier.write(contenu)
            print(f"Contenu écrit dans '{nom_fichier}'")
            return True
    except Exception as e:
        print(f"Erreur lors de l'écriture : {e}")
        return False

# Tests
contenu1 = "Bonjour, ceci est un test d'écriture de fichier."
contenu2 = "Ligne 1\nLigne 2\nLigne 3\n"
contenu3 = "Python est un langage de programmation puissant."

print("Tests d'écriture de fichiers :")
ecrire_fichier("test1.txt", contenu1)
ecrire_fichier("test2.txt", contenu2)
ecrire_fichier("test3.txt", contenu3)

# Vérification
print("\nVérification des fichiers créés :")
for i in range(1, 4):
    try:
        with open(f"test{i}.txt", 'r') as f:
            contenu_lu = f.read()
            print(f"test{i}.txt : {len(contenu_lu)} caractères")
    except Exception as e:
        print(f"Erreur lecture test{i}.txt : {e}")
```

**Explication** :
- **'w'** : mode écriture (écrase le fichier existant)
- **.write()** : écrit une chaîne de caractères
- **Création automatique** : le fichier est créé s'il n'existe pas
- **Encodage** : utf-8 pour les caractères spéciaux

**Test** : Créez trois fichiers de test avec différents contenus.

---

### Exercice 234 : Ajouter du texte à un fichier existant
**Objectif** : Ajouter du contenu à un fichier sans l'écraser.

```python
# Solution
def ajouter_au_fichier(nom_fichier, contenu):
    """Ajoute du contenu à un fichier existant"""
    try:
        with open(nom_fichier, 'a', encoding='utf-8') as fichier:  # Mode append
            fichier.write(contenu + "\n")  # Ajout d'un saut de ligne
            print(f"Contenu ajouté à '{nom_fichier}'")
            return True
    except Exception as e:
        print(f"Erreur lors de l'ajout : {e}")
        return False

# Test
print("Test d'ajout à un fichier :")

# Création initiale
ecrire_fichier("journal.txt", "=== JOURNAL QUOTIDIEN ===\n")

# Ajouts successifs
ajouter_au_fichier("journal.txt", "Lundi : Réunion d'équipe")
ajouter_au_fichier("journal.txt", "Mardi : Développement Python")
ajouter_au_fichier("journal.txt", "Mercredi : Tests unitaires")
ajouter_au_fichier("journal.txt", "Jeudi : Débogage")
ajouter_au_fichier("journal.txt", "Vendredi : Déploiement")

# Lecture du fichier complet
print("\nContenu final du journal :")
lire_fichier("journal.txt")
```

**Explication** :
- **'a'** : mode append (ajout à la fin)
- **.write()** : écrit le contenu
- **Saut de ligne** : ajout de "\n" pour la lisibilité
- **Préservation** : le contenu existant est conservé

**Test** : Ajoutez plusieurs entrées à un journal.

---

### Exercice 235 : Lire un fichier ligne par ligne
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

## 🔍 Points Clés à Retenir

### 1. **Modes d'Ouverture de Fichier**
```python
# Modes principaux
'r'   # Lecture (défaut)
'w'   # Écriture (écrase)
'a'   # Ajout (append)
'x'   # Création exclusive

# Modes binaires
'rb'  # Lecture binaire
'wb'  # Écriture binaire

# Combinaisons
'r+'  # Lecture et écriture
'w+'  # Écriture et lecture
```

### 2. **Gestion des Fichiers**
```python
# Méthode classique (à éviter)
fichier = open('test.txt', 'r')
try:
    contenu = fichier.read()
finally:
    fichier.close()

# Méthode recommandée
with open('test.txt', 'r') as fichier:
    contenu = fichier.read()
# Le fichier est automatiquement fermé
```

### 3. **Méthodes de Lecture**
```python
# Lire tout le contenu
contenu = fichier.read()           # Chaîne complète

# Lire ligne par ligne
for ligne in fichier:              # Itération
    print(ligne.strip())

# Lire n caractères
morceau = fichier.read(100)        # 100 caractères

# Lire une ligne
ligne = fichier.readline()         # Une ligne
lignes = fichier.readlines()       # Toutes les lignes en liste
```

### 4. **Méthodes d'Écriture**
```python
# Écrire une chaîne
fichier.write("texte")             # Sans saut de ligne

# Écrire avec formatage
fichier.write("Ligne {}\n".format(i))

# Écrire plusieurs lignes
fichier.writelines(["Ligne 1\n", "Ligne 2\n"])

# Flush (forcer l'écriture)
fichier.flush()
```

## 💡 Optimisations et Astuces

### 1. **Encodage et Caractères Spéciaux**
```python
# Gestion des encodages
with open('fichier.txt', 'r', encoding='utf-8') as f:
    contenu = f.read()

# Écriture avec encodage
with open('fichier.txt', 'w', encoding='utf-8') as f:
    f.write("Texte avec émojis 😀")

# Détection d'encodage
import chardet
with open('fichier.txt', 'rb') as f:
    raw = f.read()
    result = chardet.detect(raw)
    encoding = result['encoding']
```

### 2. **Chemins de Fichiers**
```python
import os

# Chemin absolu
chemin_absolu = "/Users/nom/fichier.txt"

# Chemin relatif
chemin_relatif = "data/fichier.txt"

# Vérification d'existence
if os.path.exists("fichier.txt"):
    print("Fichier existe")

# Extension de fichier
nom, extension = os.path.splitext("fichier.txt")
print(f"Nom: {nom}, Extension: {extension}")
```

### 3. **Fichiers Temporaires**
```python
import tempfile
import os

# Création d'un fichier temporaire
with tempfile.NamedTemporaryFile(mode='w', delete=False) as f:
    f.write("Contenu temporaire")
    temp_path = f.name

# Utilisation du fichier temporaire
print(f"Fichier temporaire créé : {temp_path}")

# Nettoyage
os.unlink(temp_path)
print("Fichier temporaire supprimé")
```

## 🚀 Applications Pratiques

### 1. **Analyseur de Logs**
```python
def analyser_logs(nom_fichier):
    """Analyse un fichier de logs"""
    try:
        with open(nom_fichier, 'r') as f:
            logs = f.readlines()

        print(f"Nombre total de logs : {len(logs)}")

        # Comptage par type
        types_logs = {}
        for log in logs:
            # Format : "timestamp|type|message"
            try:
                parties = log.strip().split('|')
                if len(parties) >= 2:
                    log_type = parties[1]
                    types_logs[log_type] = types_logs.get(log_type, 0) + 1
            except:
                types_logs["MALFORMATÉ"] = types_logs.get("MALFORMATÉ", 0) + 1

        print("Répartition par type :")
        for log_type, count in types_logs.items():
            pourcentage = (count / len(logs)) * 100
            print(f"  {log_type}: {count} ({pourcentage:.1f}%)")

        return types_logs

    except FileNotFoundError:
        print(f"Fichier de logs '{nom_fichier}' non trouvé")
        return {}

# Test
repartition = analyser_logs("application.log")
print(f"Répartition : {repartition}")
```

### 2. **Générateur de Fichiers de Configuration**
```python
def generer_config(nom_fichier, parametres):
    """Génère un fichier de configuration"""
    lignes_config = [
        "# Configuration générée automatiquement\n",
        f"# Date : {__import__('datetime').datetime.now().isoformat()}\n",
        "\n# Paramètres principaux\n"
    ]

    for cle, valeur in parametres.items():
        lignes_config.append(f"{cle} = {valeur}\n")

    lignes_config.append("\n# Fin de configuration\n")

    try:
        with open(nom_fichier, 'w') as f:
            f.writelines(lignes_config)
        print(f"Configuration générée : {nom_fichier}")
        return True
    except Exception as e:
        print(f"Erreur génération config : {e}")
        return False

# Test
config_params = {
    "debug": "True",
    "port": "8080",
    "timeout": "30",
    "database_url": "sqlite:///app.db",
    "log_level": "INFO"
}

generer_config("config.ini", config_params)
```

### 3. **Sauvegarde et Restauration**
```python
def sauvegarder_donnees(nom_fichier, donnees):
    """Sauvegarde des données dans un fichier"""
    try:
        with open(nom_fichier, 'w') as f:
            for donnee in donnees:
                f.write(f"{donnee}\n")
        print(f"Données sauvegardées dans {nom_fichier}")
        return True
    except Exception as e:
        print(f"Erreur sauvegarde : {e}")
        return False

def restaurer_donnees(nom_fichier):
    """Restaure des données depuis un fichier"""
    try:
        with open(nom_fichier, 'r') as f:
            donnees = [ligne.strip() for ligne in f.readlines()]
        print(f"Données restaurées depuis {nom_fichier}")
        return donnees
    except FileNotFoundError:
        print(f"Fichier de sauvegarde '{nom_fichier}' non trouvé")
        return []
    except Exception as e:
        print(f"Erreur restauration : {e}")
        return []

# Test
donnees_test = ["Alice", "Bob", "Charlie", "Diana", "Eve"]
sauvegarder_donnees("noms_backup.txt", donnees_test)

donnees_restaurees = restaurer_donnees("noms_backup.txt")
print(f"Données restaurées : {donnees_restaurees}")
print(f"Identiques : {donnees_test == donnees_restaurees}")
```

## 🎯 Défis Supplémentaires

1. **Créez** un programme qui copie un fichier vers un autre
2. **Implémentez** un système de logging qui écrit dans un fichier
3. **Développez** un analyseur de CSV simple
4. **Concevez** un générateur de fichiers de test avec du contenu aléatoire

---

**Exercices complétés : 235/260** 🎯

*Continuez avec le [chapitre suivant](6-2-csv-json.md) pour les fichiers CSV et JSON !*
