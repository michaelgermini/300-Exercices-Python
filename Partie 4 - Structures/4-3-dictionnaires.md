# Partie 4.3 : Dictionnaires

## 🎯 Objectifs Pédagogiques

Ce chapitre explore les **dictionnaires** en Python, structures de données puissantes pour associer des **clés** à des **valeurs**. Les dictionnaires permettent un accès rapide et une organisation flexible des données.

### Concepts Abordés
- **Création et manipulation** : ajout, modification, suppression
- **Accès et recherche** : par clés, tests d'existence
- **Parcours** : clés, valeurs, éléments
- **Applications** : comptage, indexation, configuration

---

## 📝 Exercices Pratiques

### Exercice 166 : Créer un dictionnaire simple
**Objectif** : Créer un dictionnaire et y ajouter des éléments.

```python
# Solution
# Création d'un dictionnaire vide
mon_dictionnaire = {}
print(f"Dictionnaire vide : {mon_dictionnaire}")

# Ajout d'éléments
mon_dictionnaire["nom"] = "Alice"
mon_dictionnaire["age"] = 25
mon_dictionnaire["ville"] = "Paris"

print(f"Dictionnaire avec éléments : {mon_dictionnaire}")

# Création avec valeurs initiales
personne = {
    "nom": "Bob",
    "age": 30,
    "ville": "Lyon",
    "profession": "Développeur"
}

print(f"Personne : {personne}")

# Dictionnaire avec types mixtes
mixte = {
    "entier": 42,
    "flottant": 3.14,
    "chaine": "Hello",
    "booleen": True,
    "liste": [1, 2, 3],
    "tuple": (4, 5, 6)
}

print(f"Dictionnaire mixte : {mixte}")
```

**Explication** :
- **Syntaxe** : {"clé": "valeur", ...}
- **Ajout** : dictionnaire["clé"] = valeur
- **Types mixtes** : valeurs de tous types autorisées
- **Clés** : doivent être hashables (immuables)

**Test** : {"nom": "Alice", "age": 25, "ville": "Paris"}.

---

### Exercice 167 : Ajouter un élément à un dictionnaire
**Objectif** : Ajouter de nouveaux éléments à un dictionnaire existant.

```python
# Solution
etudiant = {"nom": "Charlie", "age": 20}
print(f"Étudiant initial : {etudiant}")

# Ajout simple
etudiant["note"] = 15.5
print(f"Après ajout note : {etudiant}")

# Ajout multiple
etudiant.update({
    "email": "charlie@univ.fr",
    "telephone": "01-23-45-67-89",
    "specialite": "Informatique"
})

print(f"Après ajout multiple : {etudiant}")

# Ajout conditionnel (si la clé n'existe pas)
if "adresse" not in etudiant:
    etudiant["adresse"] = "123 Rue de l'Université"
print(f"Après ajout conditionnel : {etudiant}")

# Fusion avec un autre dictionnaire
contact = {"linkedin": "charlie-dev", "github": "charlie-code"}
etudiant.update(contact)
print(f"Après fusion : {etudiant}")
```

**Explication** :
- **Ajout** : ["clé"] = valeur
- **Mise à jour** : .update() pour plusieurs éléments
- **Fusion** : .update() avec un autre dictionnaire
- **Conditionnel** : test d'existence avant ajout

**Test** : Étudiant avec nom, âge, note, email, téléphone, etc.

---

### Exercice 168 : Supprimer un élément d'un dictionnaire
**Objectif** : Supprimer des éléments d'un dictionnaire.

```python
# Solution
produit = {
    "nom": "Ordinateur",
    "prix": 800,
    "categorie": "Électronique",
    "marque": "TechCorp",
    "stock": 15
}

print(f"Produit initial : {produit}")

# Suppression par clé
prix = produit.pop("prix")
print(f"Prix supprimé : {prix}")
print(f"Produit après suppression prix : {produit}")

# Suppression avec valeur par défaut
description = produit.pop("description", "Non spécifiée")
print(f"Description (par défaut) : {description}")

# Suppression et affichage
marque = produit.pop("marque", "Inconnue")
print(f"Marque supprimée : {marque}")
print(f"Produit après suppression marque : {produit}")

# Suppression sans récupération
del produit["categorie"]
print(f"Après del categorie : {produit}")

# Vider le dictionnaire
produit.clear()
print(f"Produit vidé : {produit}")
```

**Explanation** :
- **.pop()** : supprime et retourne la valeur
- **del** : supprime sans retourner
- **.clear()** : vide complètement
- **Valeur par défaut** : pop(clé, défaut) si clé absente

**Test** : Suppression progressive des éléments.

---

### Exercice 169 : Accéder à une valeur par clé
**Objectif** : Accéder aux valeurs d'un dictionnaire par leurs clés.

```python
# Solution
etudiant = {
    "nom": "Diana",
    "age": 22,
    "notes": [15, 16, 14, 18],
    "contact": {
        "email": "diana@univ.fr",
        "telephone": "01-11-11-11-11"
    }
}

print(f"Étudiant : {etudiant}")

# Accès simple
print(f"Nom : {etudiant['nom']}")
print(f"Âge : {etudiant['age']}")

# Accès à une liste
print(f"Première note : {etudiant['notes'][0]}")
print(f"Dernière note : {etudiant['notes'][-1]}")

# Accès à un dictionnaire imbriqué
print(f"Email : {etudiant['contact']['email']}")
print(f"Téléphone : {etudiant['contact']['telephone']}")

# Accès avec get() (plus sûr)
email = etudiant.get('email', 'Non spécifié')
print(f"Email (get) : {email}")

adresse = etudiant.get('adresse', 'Non spécifiée')
print(f"Adresse (get) : {adresse}")
```

**Explication** :
- **Accès direct** : dictionnaire['clé']
- **Accès sûr** : .get(clé, défaut)
- **Dictionnaires imbriqués** : dictionnaire['clé1']['clé2']
- **Listes dans dictionnaires** : dictionnaire['clé'][index]

**Test** : Accès à tous les niveaux de structure.

---

### Exercice 170 : Modifier une valeur dans un dictionnaire
**Objectif** : Modifier les valeurs existantes d'un dictionnaire.

```python
# Solution
compte_bancaire = {
    "titulaire": "Eve",
    "solde": 1000.50,
    "devise": "EUR",
    "historique": ["dépôt +500", "retrait -100"]
}

print(f"Compte initial : {compte_bancaire}")

# Modification simple
compte_bancaire["solde"] = 1500.75
print(f"Après modification solde : {compte_bancaire}")

# Modification de devise
compte_bancaire["devise"] = "USD"
print(f"Après changement devise : {compte_bancaire}")

# Ajout à une liste
compte_bancaire["historique"].append("retrait -200")
print(f"Après ajout historique : {compte_bancaire}")

# Modification d'un dictionnaire imbriqué
compte_bancaire["titulaire"] = {
    "prenom": "Eve",
    "nom": "Martin",
    "date_naissance": "1990-05-15"
}
print(f"Après modification titulaire : {compte_bancaire}")

# Calcul et mise à jour
ancien_solde = compte_bancaire["solde"]
compte_bancaire["solde"] = ancien_solde * 1.05  # +5%
compte_bancaire["historique"].append("intérêts +5%")
print(f"Après intérêts : {compte_bancaire}")
```

**Explication** :
- **Modification** : ["clé"] = nouvelle_valeur
- **Listes modifiables** : dans un dictionnaire immuable
- **Calculs** : récupération puis mise à jour
- **Imbrication** : modification de structures internes

**Test** : Modification progressive du compte bancaire.

---

### Exercice 171 : Vérifier si une clé existe dans un dictionnaire
**Objectif** : Vérifier l'existence de clés dans un dictionnaire.

```python
# Solution
personne = {
    "nom": "Frank",
    "age": 28,
    "email": "frank@email.com"
}

# Test avec 'in'
cles_a_tester = ["nom", "age", "email", "telephone", "adresse"]

print("Tests d'existence de clés :")
for cle in cles_a_tester:
    if cle in personne:
        print(f"✓ '{cle}' existe : {personne[cle]}")
    else:
        print(f"✗ '{cle}' n'existe pas")

# Test avec .get()
print("\nTests avec .get() :")
for cle in cles_a_tester:
    valeur = personne.get(cle, "NON TROUVÉ")
    print(f"'{cle}' : {valeur}")

# Test avec valeurs par défaut
configuration = {
    "debug": True,
    "port": 8080,
    "timeout": 30
}

debug = configuration.get("debug", False)
max_connections = configuration.get("max_connections", 10)
theme = configuration.get("theme", "clair")

print(f"\nConfiguration :")
print(f"Debug : {debug}")
print(f"Max connections : {max_connections}")
print(f"Theme : {theme}")
```

**Explication** :
- **Opérateur in** : test d'existence de clé
- **.get()** : accès sûr avec valeur par défaut
- **Applications** : configuration, paramètres optionnels
- **Robustesse** : évite les KeyError

**Test** : Tests de présence de clés.

---

### Exercice 172 : Parcourir un dictionnaire
**Objectif** : Parcourir les clés, valeurs et éléments d'un dictionnaire.

```python
# Solution
inventaire = {
    "pommes": 50,
    "bananes": 30,
    "oranges": 25,
    "poires": 15
}

print("Parcours du dictionnaire :")

# Parcours des clés
print("\n1. Clés uniquement :")
for cle in inventaire:
    print(f"Clé : {cle}")

# Parcours des clés avec .keys()
print("\n2. Clés avec .keys() :")
for cle in inventaire.keys():
    print(f"Clé : {cle}")

# Parcours des valeurs
print("\n3. Valeurs uniquement :")
for valeur in inventaire.values():
    print(f"Valeur : {valeur}")

# Parcours des éléments (clé, valeur)
print("\n4. Éléments (clé, valeur) :")
for cle, valeur in inventaire.items():
    print(f"{cle}: {valeur}")

# Parcours avec index
print("\n5. Avec énumération :")
for index, (cle, valeur) in enumerate(inventaire.items()):
    print(f"{index+1}. {cle}: {valeur}")
```

**Explication** :
- **Clés** : for cle in dictionnaire
- **.keys()** : méthode pour les clés
- **.values()** : méthode pour les valeurs
- **.items()** : méthode pour (clé, valeur) pairs
- **Énumération** : index + élément

**Test** : Différentes façons de parcourir.

---

### Exercice 173 : Compter le nombre d'éléments d'un dictionnaire
**Objectif** : Compter et analyser les éléments d'un dictionnaire.

```python
# Solution
frequences = {
    "a": 15,
    "e": 12,
    "i": 8,
    "o": 7,
    "u": 5,
    "y": 3
}

# Compte des éléments
nombre_elements = len(frequences)
print(f"Nombre d'éléments : {nombre_elements}")

# Compte des clés et valeurs
cles = list(frequences.keys())
valeurs = list(frequences.values())

print(f"Clés : {cles}")
print(f"Valeurs : {valeurs}")
print(f"Nombre de clés : {len(cles)}")
print(f"Nombre de valeurs : {len(valeurs)}")

# Statistiques sur les valeurs
print(f"\nStatistiques des valeurs :")
print(f"Somme des fréquences : {sum(valeurs)}")
print(f"Fréquence moyenne : {sum(valeurs) / len(valeurs):.2f}")
print(f"Voyelle la plus fréquente : {max(frequences, key=frequences.get)} ({frequences[max(frequences, key=frequences.get)]})")
print(f"Voyelle la moins fréquente : {min(frequences, key=frequences.get)} ({frequences[min(frequences, key=frequences.get)]})")
```

**Explication** :
- **len()** : nombre de paires clé-valeur
- **.keys()** : accès aux clés
- **.values()** : accès aux valeurs
- **max/min avec key** : selon les valeurs
- **Applications** : statistiques, analyse

**Test** : 6 éléments, voyelle la plus fréquente : "a".

---

### Exercice 174 : Fusionner deux dictionnaires
**Objectif** : Fusionner deux dictionnaires en un seul.

```python
# Solution
# Dictionnaire 1
personnel = {
    "nom": "Grace",
    "age": 35,
    "departement": "Informatique"
}

# Dictionnaire 2
coordonnees = {
    "email": "grace@entreprise.com",
    "telephone": "01-22-33-44-55"
}

# Fusion avec update()
personnel.update(coordonnees)
print(f"Après update() : {personnel}")

# Fusion avec ** (Python 3.5+)
contact = {**personnel, **coordonnees}
print(f"Avec ** : {contact}")

# Fusion avec | (Python 3.9+)
if hasattr({}, '__or__'):  # Test de disponibilité
    fusion_or = personnel | coordonnees
    print(f"Avec | : {fusion_or}")

# Gestion des conflits
preferences1 = {"theme": "clair", "langue": "fr"}
preferences2 = {"theme": "sombre", "pays": "France"}

# preferences1 prioritaire
fusion1_prioritaire = {**preferences2, **preferences1}
print(f"preferences1 prioritaire : {fusion1_prioritaire}")

# preferences2 prioritaire
fusion2_prioritaire = {**preferences1, **preferences2}
print(f"preferences2 prioritaire : {fusion2_prioritaire}")
```

**Explication** :
- **.update()** : fusion en place
- **{**dict1, **dict2}** : fusion avec création
- **dict1 | dict2** : syntaxe moderne (Python 3.9+)
- **Conflits** : dernière valeur écrase la précédente

**Test** : Fusion de dictionnaires avec gestion des doublons.

---

## 🔍 Points Clés à Retenir

### 1. **Création et Manipulation**
```python
# Création
vide = {}                    # Dictionnaire vide
personne = {"nom": "Alice", "age": 25}
mixte = {1: "un", "deux": 2, 3.14: True}

# Ajout/Modification
dico["nouvelle_cle"] = "valeur"
dico.update({"cle1": "val1", "cle2": "val2"})

# Suppression
del dico["cle"]              # Supprime la clé
valeur = dico.pop("cle")     # Supprime et retourne
dico.clear()                 # Vide le dictionnaire
```

### 2. **Accès et Recherche**
```python
# Accès
valeur = dico["cle"]         # KeyError si clé absente
valeur = dico.get("cle", "defaut")  # Valeur par défaut

# Test d'existence
if "cle" in dico:
    print("Clé existe")

# Recherche dans valeurs
if "valeur" in dico.values():
    print("Valeur trouvée")

# Recherche dans clés
cles_trouvees = [cle for cle in dico if cle.startswith("pre")]
```

### 3. **Parcours**
```python
# Clés seulement
for cle in dico:
    print(cle)

# Clés avec .keys()
for cle in dico.keys():
    print(cle)

# Valeurs avec .values()
for valeur in dico.values():
    print(valeur)

# Clés et valeurs avec .items()
for cle, valeur in dico.items():
    print(f"{cle}: {valeur}")
```

### 4. **Fonctions Utiles**
```python
# Statistiques
len(dico)                    # Nombre d'éléments
max(dico)                    # Clé maximale
min(dico)                    # Clé minimale
max(dico, key=dico.get)      # Clé avec valeur maximale

# Conversion
list(dico)                   # Liste des clés
list(dico.values())          # Liste des valeurs
list(dico.items())           # Liste de (clé, valeur)

# Copie
dico.copy()                  # Copie superficielle
dict(dico)                   # Nouvelle instance
```

## 💡 Optimisations et Astuces

### 1. **Dictionnaires par Défaut**
```python
from collections import defaultdict

# Dictionnaire avec valeurs par défaut
compteur = defaultdict(int)  # 0 par défaut
compteur["a"] += 1
compteur["b"] += 1
print(compteur)  # defaultdict(<class 'int'>, {'a': 1, 'b': 1})

# Avec liste par défaut
groupes = defaultdict(list)
groupes["fruits"].append("pomme")
groupes["fruits"].append("banane")
print(groupes)  # defaultdict(<class 'list'>, {'fruits': ['pomme', 'banane']})
```

### 2. **Compteur avec Dictionnaire**
```python
from collections import Counter

# Comptage simple
texte = "hello world hello python"
compteur = Counter(texte.split())
print(compteur)  # Counter({'hello': 2, 'world': 1, 'python': 1})

# Comptage de caractères
compteur_lettres = Counter(texte.replace(" ", ""))
print(compteur_lettres)  # Counter({'l': 3, 'o': 3, 'h': 2, 'e': 1, ...})

# Éléments les plus fréquents
print(compteur.most_common(2))  # [('hello', 2), ('world', 1)]
```

### 3. **Performance : Dictionnaires vs Listes**
```python
import time

# Recherche dans une liste
grande_liste = list(range(1000000))
debut = time.time()
trouve = 999999 in grande_liste
fin = time.time()
print(f"Recherche dans liste (1M) : {fin - debut:.6f}s")

# Recherche dans un dictionnaire
grand_dico = {i: f"valeur_{i}" for i in range(1000000)}
debut = time.time()
trouve = 999999 in grand_dico
fin = time.time()
print(f"Recherche dans dictionnaire (1M) : {fin - debut:.6f}s")

# Avantage du dictionnaire : O(1) vs O(n)
print(f"Rapport de performance : {((fin - debut) / ((fin - debut) or 1)):.1f}x plus rapide")
```

## 🚀 Applications Pratiques

### 1. **Indexeur de Documents**
```python
def indexer_documents(documents):
    """Crée un index inversé des documents"""
    index = {}

    for doc_id, contenu in documents.items():
        # Nettoyage et tokenisation
        mots = contenu.lower().replace(".", "").replace(",", "").split()

        # Indexation de chaque mot
        for mot in mots:
            if mot not in index:
                index[mot] = []
            if doc_id not in index[mot]:
                index[mot].append(doc_id)

    return index

# Test
docs = {
    1: "Le Python est un langage de programmation",
    2: "Python est facile à apprendre",
    3: "Le langage Python est puissant",
    4: "Java est aussi un langage populaire"
}

index = indexer_documents(docs)
print("Index inversé :")
for mot, documents in index.items():
    print(f"'{mot}': {documents}")

# Recherche
mot_recherche = "python"
print(f"\nDocuments contenant '{mot_recherche}': {index.get(mot_recherche.lower(), [])}")
```

### 2. **Gestionnaire de Configuration**
```python
def charger_configuration(fichier_config=None):
    """Charge et gère la configuration"""
    # Configuration par défaut
    config_defaut = {
        "debug": False,
        "port": 8080,
        "timeout": 30,
        "max_connexions": 100,
        "theme": "clair",
        "langue": "fr"
    }

    # Configuration utilisateur (simulée)
    config_utilisateur = {
        "debug": True,
        "theme": "sombre",
        "langue": "en"
    }

    # Fusion : utilisateur écrase les défauts
    config = {**config_defaut, **config_utilisateur}

    # Validation des types
    if not isinstance(config["port"], int) or config["port"] < 1:
        config["port"] = config_defaut["port"]
        print("Correction du port")

    if config["timeout"] < 0:
        config["timeout"] = config_defaut["timeout"]
        print("Correction du timeout")

    return config

# Test
config = charger_configuration()
print("Configuration chargée :")
for cle, valeur in config.items():
    print(f"  {cle}: {valeur} ({type(valeur).__name__})")

# Utilisation
print(f"\nServeur démarré sur le port {config['port']}")
print(f"Mode debug : {'activé' if config['debug'] else 'désactivé'}")
print(f"Theme : {config['theme']}")
```

### 3. **Analyseur de Logs**
```python
def analyser_logs(logs):
    """Analyse des logs système"""
    # Comptage des types d'événements
    evenements = {}
    erreurs_par_module = {}
    utilisateurs_actifs = set()

    for log in logs:
        # Format log : "timestamp|module|utilisateur|type|message"
        try:
            timestamp, module, utilisateur, log_type, message = log.split("|", 4)

            # Comptage par type
            evenements[log_type] = evenements.get(log_type, 0) + 1

            # Comptage d'erreurs par module
            if log_type == "ERROR":
                erreurs_par_module[module] = erreurs_par_module.get(module, 0) + 1

            # Utilisateurs uniques
            utilisateurs_actifs.add(utilisateur)

        except ValueError:
            # Log mal formaté
            evenements["MALFORMATÉ"] = evenements.get("MALFORMATÉ", 0) + 1

    # Statistiques
    stats = {
        "total_logs": len(logs),
        "types_evenements": evenements,
        "erreurs_par_module": erreurs_par_module,
        "utilisateurs_uniques": len(utilisateurs_actifs),
        "taux_erreur": (erreurs_par_module.get('total', 0) / len(logs) * 100) if logs else 0
    }

    return stats

# Test
logs_test = [
    "2024-01-15 10:30:15|auth|alice|INFO|Connexion réussie",
    "2024-01-15 10:31:22|db|bob|ERROR|Échec de connexion",
    "2024-01-15 10:32:10|api|alice|INFO|Requête traitée",
    "2024-01-15 10:33:45|auth|charlie|WARNING|Mot de passe faible",
    "2024-01-15 10:34:12|db|bob|ERROR|Timeout",
    "2024-01-15 10:35:30|api|diana|INFO|Nouveau utilisateur"
]

analyse = analyser_logs(logs_test)
print("Analyse des logs :")
for cle, valeur in analyse.items():
    print(f"  {cle}: {valeur}")
```

## 🎯 Défis Supplémentaires

1. **Créez** un dictionnaire qui traduit des nombres en mots
2. **Implémentez** un système de cache avec dictionnaire
3. **Développez** un analyseur de fréquences de caractères
4. **Concevez** un dictionnaire avec des dictionnaires imbriqués pour des données hiérarchiques

---

**Exercices complétés : 174/200** 🎯

*Continuez avec le [chapitre suivant](4-4-ensembles.md) pour explorer les ensembles !*