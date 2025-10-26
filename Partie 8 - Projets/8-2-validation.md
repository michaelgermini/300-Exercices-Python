# Partie 8.2 : Validation et Parsing

## 🎯 Objectifs Pédagogiques

Ce chapitre présente des **projets de validation et parsing**, combinant tous les concepts pour créer des programmes qui analysent, valident et traitent des données complexes.

### Concepts Intégrés
- **Validation** : parenthèses, HTML, expressions
- **Parsing** : analyse de texte, extraction d'informations
- **Génération** : création de contenu structuré
- **Applications** : vérification, nettoyage, transformation

---

## 📝 Exercices Pratiques

### Exercice 291 : Validateur de parenthèses
**Objectif** : Vérifier si les parenthèses sont correctement équilibrées.

```python
# Solution
def valider_parentheses(expression):
    """Valide l'équilibre des parenthèses"""
    pile = []

    # Mappage des parenthèses
    parentheses = {
        ')': '(',
        ']': '[',
        '}': '{'
    }

    for caractere in expression:
        if caractere in '([{':
            pile.append(caractere)
        elif caractere in ')]}':
            if not pile:
                return False, f"Parenthèse fermante '{caractere}' sans ouverture"

            if pile[-1] == parentheses[caractere]:
                pile.pop()
            else:
                return False, f"Parenthèse '{caractere}' ne correspond pas à '{pile[-1]}'"

    if pile:
        return False, f"Parenthèse(s) ouvrante(s) non fermée(s) : {pile}"

    return True, "Parenthèses équilibrées"

# Tests
expressions_test = [
    "()",                    # ✓ Valide
    "[]",                    # ✓ Valide
    "{}",                    # ✓ Valide
    "(())",                  # ✓ Valide
    "[{()}]",                # ✓ Valide
    "([{}])",                # ✓ Valide
    "((()))",                # ✓ Valide
    "(()",                   # ✗ Invalide
    "())",                   # ✗ Invalide
    "[{]}",                  # ✗ Invalide
    "((()",                  # ✗ Invalide
    "abc(def)ghi",           # ✓ Valide (avec texte)
    "fonction(param1, param2)",  # ✓ Valide
]

print("=== VALIDATEUR DE PARENTHÈSES ===")
for expression in expressions_test:
    valide, message = valider_parentheses(expression)
    statut = "✓" if valide else "✗"
    print(f"{statut} '{expression}': {message}")

# Test interactif
print("\nTest interactif :")
while True:
    expression = input("Entrez une expression (ou 'quit') : ").strip()
    if expression.lower() == 'quit':
        break

    valide, message = valider_parentheses(expression)
    statut = "✓" if valide else "✗"
    print(f"{statut} {message}")
```

**Explication** :
- **Pile (stack)** : suivi des parenthèses ouvrantes
- **Mappage** : correspondance ouverture/fermeture
- **Validation** : équilibre parfait requis
- **Applications** : analyse de code, expressions mathématiques

**Test** : Testez différentes expressions avec parenthèses.

---

### Exercice 292 : Validateur de documents HTML
**Objectif** : Vérifier la validité basique d'un document HTML.

```python
# Solution
def valider_html_basique(html):
    """Valide la structure basique d'un document HTML"""
    erreurs = []
    avertissements = []

    # Vérification des balises de base
    if not html.strip().startswith('<html'):
        erreurs.append("Le document ne commence pas par <html>")

    if not html.strip().endswith('</html>'):
        erreurs.append("Le document ne se termine pas par </html>")

    # Vérification des balises principales
    if '<head>' not in html:
        avertissements.append("Balise <head> manquante")
    if '<body>' not in html:
        avertissements.append("Balise <body> manquante")
    if '<title>' not in html:
        avertissements.append("Balise <title> manquante")

    # Vérification des balises auto-fermantes
    balises_auto_fermantes = ['<br>', '<br/>', '<img', '<input', '<meta']
    for balise in balises_auto_fermantes:
        if balise in html and balise + '>' not in html and balise + '/>' not in html:
            if balise == '<br':
                continue  # <br> peut être sans />
            erreurs.append(f"Balise '{balise}' doit être auto-fermante")

    # Vérification de la structure
    balises_ouvrantes = []
    i = 0

    while i < len(html):
        if html[i] == '<':
            # Début d'une balise
            j = i + 1
            while j < len(html) and html[j] != '>':
                j += 1

            if j < len(html):
                balise = html[i:j+1]

                # Balise ouvrante
                if not balise.startswith('</') and not balise.endswith('/>') and balise != '<br>':
                    if balise.startswith('<br'):
                        pass  # <br> spécial
                    else:
                        balises_ouvrantes.append(balise)

                # Balise fermante
                elif balise.startswith('</'):
                    balise_nom = balise[2:-1]
                    if balises_ouvrantes and balises_ouvrantes[-1][1:-1] == balise_nom:
                        balises_ouvrantes.pop()
                    else:
                        erreurs.append(f"Balise fermante '{balise}' sans balise ouvrante correspondante")

                i = j
        i += 1

    if balises_ouvrantes:
        erreurs.append(f"Balises non fermées : {balises_ouvrantes}")

    return {
        "valide": len(erreurs) == 0,
        "erreurs": erreurs,
        "avertissements": avertissements,
        "score": max(0, 10 - len(erreurs) - len(avertissements) * 0.5)
    }

# Tests
html_tests = [
    "<html><head><title>Test</title></head><body><h1>Hello</h1></body></html>",  # Parfait
    "<html><body><p>Contenu</p></body></html>",  # Sans head/title
    "<html><body><p>Non fermé</body></html>",  # Balise non fermée
    "<html><body></p></body></html>",  # Balise fermante sans ouvrante
    "<div><p>Contenu</p></div>",  # HTML fragment valide
]

print("=== VALIDATEUR HTML BASIQUE ===")
for i, html in enumerate(html_tests):
    resultat = valider_html_basique(html)
    print(f"\nTest {i+1} :")
    print(f"Valide : {resultat['valide']}")
    print(f"Score : {resultat['score']}/10")
    if resultat['erreurs']:
        print(f"Erreurs : {resultat['erreurs']}")
    if resultat['avertissements']:
        print(f"Avertissements : {resultat['avertissements']}")
```

**Explication** :
- **Structure HTML** : vérification des balises principales
- **Balises auto-fermantes** : validation des formats
- **Équilibre** : ouverture/fermeture correspondante
- **Score** : évaluation de la qualité

**Test** : Validez différents documents HTML.

---

### Exercice 293 : Générateur de matrice spirale
**Objectif** : Générer une matrice avec des nombres en spirale.

```python
# Solution
def generer_matrice_spirale(n):
    """Génère une matrice n×n avec des nombres en spirale"""
    if n <= 0:
        return []

    # Initialisation de la matrice
    matrice = [[0] * n for _ in range(n)]

    # Directions : droite, bas, gauche, haut
    directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]

    # Position de départ
    x, y = 0, 0
    direction_index = 0
    nombre = 1

    # Limites pour changer de direction
    top, bottom, left, right = 0, n-1, 0, n-1

    while nombre <= n * n:
        # Remplissage dans la direction actuelle
        matrice[x][y] = nombre
        nombre += 1

        # Calcul de la prochaine position
        dx, dy = directions[direction_index]
        nx, ny = x + dx, y + dy

        # Vérification des limites
        if not (left <= nx <= right and top <= ny <= bottom):
            # Changement de direction
            direction_index = (direction_index + 1) % 4

            # Ajustement des limites
            if direction_index == 0:  # Droite
                top += 1
            elif direction_index == 1:  # Bas
                right -= 1
            elif direction_index == 2:  # Gauche
                bottom -= 1
            elif direction_index == 3:  # Haut
                left += 1

            # Nouvelle position
            dx, dy = directions[direction_index]
            nx, ny = x + dx, y + dy

        x, y = nx, ny

    return matrice

def afficher_matrice(matrice):
    """Affiche une matrice de manière lisible"""
    if not matrice:
        print("Matrice vide")
        return

    n = len(matrice)
    largeur = len(str(n * n)) + 1

    for i in range(n):
        ligne = ""
        for j in range(n):
            ligne += f"{matrice[i][j]:{largeur}d}"
        print(ligne)

# Tests
print("=== GÉNÉRATEUR DE MATRICE SPIRALE ===")

tailles = [3, 4, 5, 6]
for taille in tailles:
    print(f"\nMatrice {taille}×{taille} :")
    matrice = generer_matrice_spirale(taille)
    afficher_matrice(matrice)

# Vérification
print("\nVérification pour 3×3 :")
matrice_3x3 = generer_matrice_spirale(3)
afficher_matrice(matrice_3x3)
print("Attendu : 1 2 3 / 8 9 4 / 7 6 5")
```

**Explication** :
- **Spirale** : remplissage en tournant
- **Directions** : droite, bas, gauche, haut
- **Limites** : ajustement après chaque tour
- **Applications** : puzzles, visualisation de données

**Test** : Générez des matrices spirales de différentes tailles.

---

### Exercice 294 : Analyse et statistiques sur fichiers CSV
**Objectif** : Analyser un fichier CSV et générer des statistiques.

```python
# Solution
import csv
import os

def analyser_csv_avance(nom_fichier):
    """Analyse complète d'un fichier CSV"""
    if not os.path.exists(nom_fichier):
        return f"Fichier '{nom_fichier}' non trouvé"

    try:
        with open(nom_fichier, 'r', newline='', encoding='utf-8') as fichier:
            lecteur = csv.reader(fichier)
            lignes = list(lecteur)

        if not lignes:
            return "Fichier CSV vide"

        # Analyse de structure
        nombre_lignes = len(lignes)
        nombre_colonnes = len(lignes[0]) if lignes else 0

        analyse = {
            "nom_fichier": nom_fichier,
            "lignes_total": nombre_lignes,
            "colonnes": nombre_colonnes,
            "en_tetes": lignes[0] if nombre_lignes > 0 else [],
            "donnees": lignes[1:] if nombre_lignes > 1 else [],
            "taille_fichier": os.path.getsize(nom_fichier)
        }

        # Analyse des types de données par colonne
        types_colonnes = []
        for col in range(nombre_colonnes):
            types = set()
            valeurs_colonne = []

            for ligne in lignes[1:]:  # Ignore les en-têtes
                if col < len(ligne):
                    valeur = ligne[col].strip()
                    valeurs_colonne.append(valeur)

                    # Détection du type
                    try:
                        int(valeur)
                        types.add('int')
                    except ValueError:
                        try:
                            float(valeur)
                            types.add('float')
                        except ValueError:
                            if valeur.lower() in ['true', 'false']:
                                types.add('bool')
                            else:
                                types.add('str')

            types_colonnes.append({
                "type_principal": max(types, key=valeurs_colonne.count) if types else 'str',
                "valeurs_uniques": len(set(valeurs_colonne)),
                "valeurs_vides": valeurs_colonne.count(''),
                "exemples": valeurs_colonne[:3] if valeurs_colonne else []
            })

        analyse["types_colonnes"] = types_colonnes

        # Statistiques numériques
        stats_numeriques = {}
        for col, info_type in enumerate(types_colonnes):
            if info_type["type_principal"] in ['int', 'float']:
                valeurs = []
                for ligne in lignes[1:]:
                    if col < len(ligne):
                        valeur = ligne[col].strip()
                        if valeur:
                            try:
                                if info_type["type_principal"] == 'int':
                                    valeurs.append(int(valeur))
                                else:
                                    valeurs.append(float(valeur))
                            except ValueError:
                                pass

                if valeurs:
                    stats_numeriques[f"colonne_{col}"] = {
                        "minimum": min(valeurs),
                        "maximum": max(valeurs),
                        "moyenne": sum(valeurs) / len(valeurs),
                        "somme": sum(valeurs),
                        "effectif": len(valeurs)
                    }

        analyse["stats_numeriques"] = stats_numeriques

        return analyse

    except Exception as e:
        return f"Erreur lors de l'analyse : {e}"

# Test
print("=== ANALYSEUR CSV AVANCÉ ===")

# Création d'un fichier CSV de test
donnees_test = [
    ["Nom", "Age", "Salaire", "Actif"],
    ["Alice", "25", "35000", "True"],
    ["Bob", "30", "42000", "False"],
    ["Charlie", "28", "38000", "True"],
    ["Diana", "35", "55000", "True"]
]

with open("test_analyse.csv", 'w', newline='') as f:
    writer = csv.writer(f)
    writer.writerows(donnees_test)

# Analyse
analyse = analyser_csv_avance("test_analyse.csv")

if isinstance(analyse, dict):
    print("Analyse du fichier CSV :")
    print(f"Nom : {analyse['nom_fichier']}")
    print(f"Lignes : {analyse['lignes_total']}")
    print(f"Colonnes : {analyse['colonnes']}")
    print(f"Taille : {analyse['taille_fichier']} octets")

    print("\nEn-têtes :")
    print(f"  {analyse['en_tetes']}")

    print("\nTypes de colonnes :")
    for i, type_info in enumerate(analyse['types_colonnes']):
        print(f"  Colonne {i} ({analyse['en_tetes'][i]}) :")
        print(f"    Type principal : {type_info['type_principal']}")
        print(f"    Valeurs uniques : {type_info['valeurs_uniques']}")
        print(f"    Valeurs vides : {type_info['valeurs_vides']}")

    print("\nStatistiques numériques :")
    for col, stats in analyse['stats_numeriques'].items():
        print(f"  {col} :")
        for stat, valeur in stats.items():
            print(f"    {stat}: {valeur}")
else:
    print(analyse)

# Nettoyage
os.remove("test_analyse.csv")
```

**Explication** :
- **Analyse complète** : structure, types, statistiques
- **Détection de types** : automatique par colonne
- **Statistiques** : min, max, moyenne pour les numériques
- **Applications** : exploration de données, qualité des données

**Test** : Analysez un fichier CSV avec des données variées.

---

### Exercice 295 : Calcul des moyennes mobiles
**Objectif** : Calculer les moyennes mobiles d'une série de données.

```python
# Solution
def calculer_moyennes_mobiles(donnees, fenetre=3):
    """Calcule les moyennes mobiles"""
    if len(donnees) < fenetre:
        return []

    moyennes = []
    for i in range(len(donnees) - fenetre + 1):
        fenetre_courante = donnees[i:i + fenetre]
        moyenne = sum(fenetre_courante) / fenetre
        moyennes.append(moyenne)

    return moyennes

def analyser_tendance(moyennes):
    """Analyse la tendance des moyennes mobiles"""
    if len(moyennes) < 2:
        return "Données insuffisantes"

    tendances = []
    for i in range(1, len(moyennes)):
        if moyennes[i] > moyennes[i-1]:
            tendances.append("↗️")
        elif moyennes[i] < moyennes[i-1]:
            tendances.append("↘️")
        else:
            tendances.append("➡️")

    return tendances

# Tests
print("=== CALCUL DE MOYENNES MOBILES ===")

# Données de test
donnees_temperatures = [20, 22, 25, 23, 21, 24, 26, 28, 27, 25, 23, 22]
fenetres = [3, 5, 7]

for fenetre in fenetres:
    print(f"\nFenêtre de {fenetre} valeurs :")
    moyennes = calculer_moyennes_mobiles(donnees_temperatures, fenetre)

    print(f"Données originales : {donnees_temperatures}")
    print(f"Moyennes mobiles : {[round(m, 2) for m in moyennes]}")

    tendances = analyser_tendance(moyennes)
    print(f"Tendances : {tendances}")

# Application : lissage de données
print("
=== APPLICATION : LISSAGE DE DONNÉES ===")
donnees_bruit = [10, 12, 8, 15, 11, 13, 9, 16, 14, 12, 10, 11]
moyennes_lissee = calculer_moyennes_mobiles(donnees_bruit, 3)

print(f"Données bruitées : {donnees_bruit}")
print(f"Données lissées : {[round(m, 2) for m in moyennes_lissee]}")
```

**Explanation** :
- **Fenêtre glissante** : moyenne sur n valeurs successives
- **Lissage** : réduction du bruit dans les données
- **Tendance** : analyse de l'évolution
- **Applications** : analyse de séries temporelles, filtrage

**Test** : Calculez des moyennes mobiles avec différentes fenêtres.

---

## 🔍 Points Clés à Retenir

### 1. **Validation de Parentheses**
```python
def valider_parentheses(expr):
    pile = []
    parentheses = {')': '(', ']': '[', '}': '{'}
    for c in expr:
        if c in '([{':
            pile.append(c)
        elif c in ')]}':
            if not pile or pile.pop() != parentheses[c]:
                return False
    return len(pile) == 0
```

### 2. **Validation HTML**
```python
def valider_html_basique(html):
    # Vérification structure
    # Vérification balises
    # Retour d'un score de validité
    pass
```

### 3. **Matrice Spirale**
```python
def generer_matrice_spirale(n):
    matrice = [[0] * n for _ in range(n)]
    # Logique de spirale
    return matrice
```

### 4. **Analyse CSV**
```python
def analyser_csv(fichier):
    with open(fichier, 'r') as f:
        reader = csv.reader(f)
        donnees = list(reader)
    # Analyse de structure et types
    return analyse
```

## 💡 Optimisations et Astuces

### 1. **Validation Plus Rapide**
```python
def valider_parentheses_rapide(expr):
    """Version optimisée avec Counter"""
    from collections import Counter
    ouverts = Counter()
    fermes = Counter()

    for c in expr:
        if c in '([{':
            ouverts[c] += 1
        elif c in ')]}':
            fermes[c] += 1

    return ouverts['('] == fermes[')'] and ouverts['['] == fermes[']'] and ouverts['{'] == fermes['}']
```

### 2. **Parsing Plus Sophistiqué**
```python
import re

def extraire_donnees_html(html):
    """Extrait des données d'un document HTML"""
    # Extraction de titres
    titres = re.findall(r'<title>(.*?)</title>', html, re.IGNORECASE)

    # Extraction de liens
    liens = re.findall(r'href=["\']([^"\']+)["\']', html, re.IGNORECASE)

    return {"titres": titres, "liens": liens}
```

### 3. **Matrice avec NumPy**
```python
# Si numpy est disponible
import numpy as np

def generer_matrice_numpy(n):
    """Matrice spirale avec NumPy"""
    matrice = np.zeros((n, n), dtype=int)
    # Logique optimisée avec NumPy
    return matrice
```

## 🚀 Applications Pratiques

### 1. **Analyseur de Code**
```python
def analyser_code_python(fichier):
    """Analyse un fichier Python"""
    try:
        with open(fichier, 'r', encoding='utf-8') as f:
            code = f.read()

        # Statistiques
        lignes = code.split('\n')
        lignes_code = [ligne for ligne in lignes if ligne.strip() and not ligne.strip().startswith('#')]

        # Comptage
        fonctions = code.count('def ')
        classes = code.count('class ')
        imports = code.count('import ') + code.count('from ')

        # Longueur moyenne des fonctions
        fonctions_match = re.findall(r'def (\w+)', code)
        moyenne_longueur_nom = sum(len(nom) for nom in fonctions_match) / len(fonctions_match) if fonctions_match else 0

        return {
            "lignes_total": len(lignes),
            "lignes_code": len(lignes_code),
            "fonctions": fonctions,
            "classes": classes,
            "imports": imports,
            "longueur_moyenne_noms_fonctions": round(moyenne_longueur_nom, 2)
        }

    except Exception as e:
        return f"Erreur : {e}"

# Test
stats = analyser_code_python("mon_script.py")
if isinstance(stats, dict):
    print("Analyse du code Python :")
    for cle, valeur in stats.items():
        print(f"  {cle}: {valeur}")
else:
    print(stats)
```

### 2. **Validateur de Configuration**
```python
def valider_config(config_dict, schema):
    """Valide une configuration selon un schéma"""
    erreurs = []

    for cle, regles in schema.items():
        if cle not in config_dict:
            if regles.get("required", False):
                erreurs.append(f"Clé manquante : {cle}")
            continue

        valeur = config_dict[cle]

        # Test de type
        if "type" in regles:
            type_attendu = regles["type"]
            if not isinstance(valeur, type_attendu):
                erreurs.append(f"Type invalide pour {cle} : attendu {type_attendu.__name__}")

        # Test de plage
        if "min" in regles and isinstance(valeur, (int, float)):
            if valeur < regles["min"]:
                erreurs.append(f"Valeur trop petite pour {cle}")

        if "max" in regles and isinstance(valeur, (int, float)):
            if valeur > regles["max"]:
                erreurs.append(f"Valeur trop grande pour {cle}")

        # Test d'énumération
        if "choices" in regles:
            if valeur not in regles["choices"]:
                erreurs.append(f"Valeur invalide pour {cle}")

    return len(erreurs) == 0, erreurs

# Test
schema = {
    "port": {"type": int, "min": 1024, "max": 65535, "required": True},
    "debug": {"type": bool, "required": False},
    "theme": {"type": str, "choices": ["clair", "sombre", "auto"], "required": False},
    "timeout": {"type": int, "min": 1, "max": 300, "required": False}
}

config_test = {
    "port": 8080,
    "debug": True,
    "theme": "sombre",
    "timeout": 30
}

valide, erreurs = valider_config(config_test, schema)
print(f"Configuration valide : {valide}")
if erreurs:
    print(f"Erreurs : {erreurs}")
```

### 3. **Extracteur d'Informations**
```python
def extraire_informations(texte):
    """Extrait diverses informations d'un texte"""
    import re

    # Extraction d'emails
    emails = re.findall(r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b', texte)

    # Extraction de numéros de téléphone
    telephones = re.findall(r'(\+\d{1,3}[- ]?)?\d{1,4}[- ]?\d{1,4}[- ]?\d{4}', texte)

    # Extraction d'URLs
    urls = re.findall(r'http[s]?://(?:[a-zA-Z]|[0-9]|[$-_@.&+]|[!*\\(\\),]|(?:%[0-9a-fA-F][0-9a-fA-F]))+', texte)

    # Extraction de nombres
    nombres = re.findall(r'\b\d+\.?\d*\b', texte)

    # Extraction de mots (plus de 3 lettres)
    mots = re.findall(r'\b[A-Za-z]{4,}\b', texte)

    return {
        "emails": list(set(emails)),  # Uniques
        "telephones": list(set(telephones)),
        "urls": list(set(urls)),
        "nombres": nombres,
        "mots_significatifs": list(set(mots)),
        "statistiques": {
            "emails": len(emails),
            "telephones": len(telephones),
            "urls": len(urls),
            "nombres": len(nombres),
            "mots": len(mots)
        }
    }

# Test
texte_test = """
Bonjour, contactez-moi à alice@example.com ou au +33 1 23 45 67 89.
Visitez notre site https://www.example.com pour plus d'informations.
Nous avons 150 clients et 25.5% de croissance.
Python est un langage programmation très populaire et puissant.
"""

info = extraire_informations(texte_test)
print("Informations extraites :")
for cle, valeur in info.items():
    if cle != "statistiques":
        print(f"  {cle}: {valeur}")
    else:
        print("  statistiques :")
        for stat, val in valeur.items():
            print(f"    {stat}: {val}")
```

## 🎯 Défis Supplémentaires

1. **Créez** un validateur d'adresses email plus sophistiqué
2. **Implémentez** un parseur de fichiers JSON complexe
3. **Développez** un système de validation de formulaires web
4. **Concevez** un extracteur d'informations de documents PDF (simplifié)

---

**Exercices complétés : 295/300** 🎯

*Continuez avec le [chapitre suivant](8-3-gestion.md) pour la gestion de données !*
