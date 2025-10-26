# Partie 6.4 : Bases de Données SQLite

## 🎯 Objectifs Pédagogiques

Ce chapitre explore l'utilisation de **bases de données SQLite** en Python, système de base de données léger et intégré pour la persistance de données structurées.

### Concepts Abordés
- **Connexion et création** : sqlite3.connect(), création de tables
- **Opérations CRUD** : Create, Read, Update, Delete
- **Requêtes SQL** : SELECT, INSERT, UPDATE, DELETE
- **Applications** : gestion de données, requêtes complexes

---

## 📝 Exercices Pratiques

### Exercice 246 : Créer une base de données SQLite
**Objectif** : Créer une base de données et une table SQLite.

```python
# Solution
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

# Test
creer_base_donnees()
```

**Explication** :
- **sqlite3.connect()** : connexion à la base
- **cursor.execute()** : exécution de requêtes SQL
- **CREATE TABLE** : définition de la structure
- **commit()** : validation des modifications
- **close()** : fermeture de la connexion

**Test** : Crée une base "etudiants.db" avec une table "etudiants".

---

### Exercice 247 : Créer une table SQLite
**Objectif** : Définir et créer une table avec différents types de colonnes.

```python
# Solution
import sqlite3

def creer_table_complexe():
    """Crée une table avec différents types de données"""
    try:
        connexion = sqlite3.connect("produits.db")
        curseur = connexion.cursor()

        # Suppression de la table si elle existe
        curseur.execute("DROP TABLE IF EXISTS produits")

        # Création de la table avec différents types
        curseur.execute("""
            CREATE TABLE produits (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                nom TEXT NOT NULL,
                prix REAL NOT NULL,
                quantite INTEGER DEFAULT 0,
                categorie TEXT,
                date_creation DATE DEFAULT CURRENT_DATE,
                disponible BOOLEAN DEFAULT 1,
                description TEXT
            )
        """)

        connexion.commit()
        print("Table 'produits' créée avec différents types de colonnes")

        # Affichage de la structure de la table
        curseur.execute("PRAGMA table_info(produits)")
        colonnes = curseur.fetchall()

        print("\nStructure de la table :")
        for colonne in colonnes:
            print(f"  {colonne[1]}: {colonne[2]} (nullable: {colonne[3] == 0})")

        connexion.close()

    except sqlite3.Error as e:
        print(f"Erreur SQLite : {e}")

# Test
creer_table_complexe()
```

**Explication** :
- **Types SQLite** : INTEGER, TEXT, REAL, BOOLEAN, DATE
- **Contraintes** : PRIMARY KEY, NOT NULL, DEFAULT
- **PRAGMA table_info** : introspection de la structure
- **CURRENT_DATE** : valeur par défaut pour les dates

**Test** : Crée une table avec différents types de données.

---

### Exercice 248 : Insérer des données dans une table
**Objectif** : Insérer des enregistrements dans une table SQLite.

```python
# Solution
import sqlite3

def inserer_etudiants():
    """Insère des données d'étudiants"""
    try:
        connexion = sqlite3.connect("etudiants.db")
        curseur = connexion.cursor()

        # Insertion de données
        etudiants = [
            ("Dupont", "Alice", 20, "Informatique", 15.5),
            ("Martin", "Bob", 22, "Mathématiques", 14.2),
            ("Garcia", "Clara", 21, "Physique", 16.8),
            ("Lefebvre", "David", 19, "Chimie", 13.9)
        ]

        # Insertion multiple avec executemany
        curseur.executemany("""
            INSERT INTO etudiants (nom, prenom, age, filiere, moyenne)
            VALUES (?, ?, ?, ?, ?)
        """, etudiants)

        connexion.commit()
        print(f"{len(etudiants)} étudiants insérés avec succès")

        # Insertion individuelle
        curseur.execute("""
            INSERT INTO etudiants (nom, prenom, age, filiere, moyenne)
            VALUES (?, ?, ?, ?, ?)
        """, ("Wilson", "Emma", 23, "Biologie", 17.1))

        connexion.commit()
        print("Étudiante supplémentaire insérée")

        connexion.close()

    except sqlite3.Error as e:
        print(f"Erreur SQLite : {e}")

# Test
inserer_etudiants()
```

**Explication** :
- **executemany()** : insertion multiple efficace
- **?** : paramètres pour éviter l'injection SQL
- **commit()** : validation des insertions
- **Insertion individuelle** : pour les cas uniques

**Test** : Insère des données d'étudiants dans la base.

---

### Exercice 249 : Lire des données depuis une table
**Objectif** : Récupérer et afficher des données depuis une table SQLite.

```python
# Solution
import sqlite3

def lire_etudiants():
    """Lit et affiche les données d'étudiants"""
    try:
        connexion = sqlite3.connect("etudiants.db")
        curseur = connexion.cursor()

        # Sélection de tous les étudiants
        curseur.execute("SELECT * FROM etudiants")
        etudiants = curseur.fetchall()

        print("Liste de tous les étudiants :")
        for etudiant in etudiants:
            print(f"  ID: {etudiant[0]}, {etudiant[2]} {etudiant[1]}, {etudiant[3]} ans, {etudiant[4]}, Moyenne: {etudiant[5]}")

        # Sélection avec conditions
        curseur.execute("SELECT nom, prenom, moyenne FROM etudiants WHERE moyenne > 15")
        etudiants_excellents = curseur.fetchall()

        print(f"\nÉtudiants avec moyenne > 15 ({len(etudiants_excellents)}) :")
        for etudiant in etudiants_excellents:
            print(f"  {etudiant[1]} {etudiant[0]}: {etudiant[2]}/20")

        # Tri par moyenne décroissante
        curseur.execute("SELECT * FROM etudiants ORDER BY moyenne DESC")
        etudiants_tries = curseur.fetchall()

        print("\nClassement par moyenne décroissante :")
        for etudiant in etudiants_tries:
            print(f"  {etudiant[2]} {etudiant[1]}: {etudiant[5]}/20")

        connexion.close()

    except sqlite3.Error as e:
        print(f"Erreur SQLite : {e}")

# Test
lire_etudiants()
```

**Explication** :
- **fetchall()** : récupère tous les résultats
- **WHERE** : conditions de filtrage
- **ORDER BY** : tri des résultats
- **Affichage** : formatage des données

**Test** : Lit et affiche les données d'étudiants.

---

### Exercice 250 : Mettre à jour des données dans une table
**Objectif** : Modifier des enregistrements existants.

```python
# Solution
import sqlite3

def mettre_a_jour_etudiants():
    """Met à jour les données d'étudiants"""
    try:
        connexion = sqlite3.connect("etudiants.db")
        curseur = connexion.cursor()

        # Mise à jour de la moyenne d'un étudiant
        curseur.execute("""
            UPDATE etudiants
            SET moyenne = 16.5
            WHERE nom = 'Dupont' AND prenom = 'Alice'
        """)

        print(f"Lignes modifiées : {curseur.rowcount}")

        # Mise à jour conditionnelle
        curseur.execute("""
            UPDATE etudiants
            SET filiere = 'Informatique Avancée'
            WHERE filiere = 'Informatique' AND moyenne > 15
        """)

        print(f"Lignes modifiées : {curseur.rowcount}")

        # Mise à jour avec calcul
        curseur.execute("""
            UPDATE etudiants
            SET moyenne = moyenne + 0.5
            WHERE age < 21
        """)

        print(f"Lignes modifiées : {curseur.rowcount}")

        connexion.commit()
        print("Modifications validées")

        # Vérification des modifications
        curseur.execute("SELECT nom, prenom, moyenne FROM etudiants")
        etudiants = curseur.fetchall()

        print("\nÉtudiants après modifications :")
        for etudiant in etudiants:
            print(f"  {etudiant[1]} {etudiant[0]}: {etudiant[2]}/20")

        connexion.close()

    except sqlite3.Error as e:
        print(f"Erreur SQLite : {e}")

# Test
mettre_a_jour_etudiants()
```

**Explication** :
- **UPDATE** : modification d'enregistrements
- **SET** : colonnes à modifier
- **WHERE** : conditions de sélection
- **rowcount** : nombre de lignes affectées
- **Calculs** : mise à jour avec expressions

**Test** : Modifie les moyennes et filières des étudiants.

---

## 🔍 Points Clés à Retenir

### 1. **Connexion et Curseur**
```python
import sqlite3

# Connexion
connexion = sqlite3.connect("base.db")

# Curseur pour exécuter les requêtes
curseur = connexion.cursor()

# Exécution de requêtes
curseur.execute("CREATE TABLE ...")
curseur.execute("SELECT * FROM ...")

# Récupération des résultats
resultats = curseur.fetchall()

# Fermeture
connexion.close()
```

### 2. **Types SQLite**
```python
# Types principaux
INTEGER    # Entiers
REAL       # Flottants
TEXT       # Chaînes
BLOB       # Données binaires
BOOLEAN    # Booléens (stockés comme INTEGER 0/1)
DATE       # Dates (stockées comme TEXT)

# Contraintes
PRIMARY KEY     # Clé primaire
NOT NULL        # Valeur obligatoire
DEFAULT valeur  # Valeur par défaut
UNIQUE          # Unicité
```

### 3. **Requêtes SQL Principales**
```python
# CREATE TABLE
curseur.execute("""
    CREATE TABLE table (
        id INTEGER PRIMARY KEY,
        nom TEXT NOT NULL,
        age INTEGER
    )
""")

# INSERT
curseur.execute("INSERT INTO table (nom, age) VALUES (?, ?)", ("Alice", 25))

# SELECT
curseur.execute("SELECT * FROM table WHERE age > 18")
resultats = curseur.fetchall()

# UPDATE
curseur.execute("UPDATE table SET age = ? WHERE nom = ?", (26, "Alice"))

# DELETE
curseur.execute("DELETE FROM table WHERE age < 18")
```

### 4. **Paramètres et Sécurité**
```python
# Paramètres nommés
curseur.execute("SELECT * FROM table WHERE age > :age", {"age": 18})

# Paramètres positionnels (recommandé)
curseur.execute("INSERT INTO table (nom, age) VALUES (?, ?)", ("Alice", 25))

# Évite l'injection SQL
nom_utilisateur = "Alice'; DROP TABLE table; --"
curseur.execute("SELECT * FROM table WHERE nom = ?", (nom_utilisateur,))  # Sécurisé
```

## 💡 Optimisations et Astuces

### 1. **Transactions**
```python
# Transactions explicites
connexion = sqlite3.connect("base.db")
try:
    curseur = connexion.cursor()

    # Début de transaction
    curseur.execute("BEGIN")

    # Opérations
    curseur.execute("INSERT ...")
    curseur.execute("UPDATE ...")

    # Validation
    connexion.commit()

except sqlite3.Error:
    # Annulation en cas d'erreur
    connexion.rollback()

finally:
    connexion.close()
```

### 2. **Index et Performance**
```python
# Création d'index
curseur.execute("CREATE INDEX idx_nom ON etudiants (nom)")
curseur.execute("CREATE INDEX idx_moyenne ON etudiants (moyenne)")

# Index composés
curseur.execute("CREATE INDEX idx_nom_age ON etudiants (nom, age)")

# Vérification des index
curseur.execute("SELECT name FROM sqlite_master WHERE type='index'")
index = curseur.fetchall()
```

### 3. **Types Personnalisés**
```python
import sqlite3
import json

# Adaptateur pour objets complexes
def adaptateur_json(obj):
    return json.dumps(obj)

def convertisseur_json(blob):
    return json.loads(blob.decode('utf-8'))

# Enregistrement des adaptateurs
sqlite3.register_adapter(dict, adaptateur_json)
sqlite3.register_converter("json", convertisseur_json)

# Utilisation
donnees = {"config": "valeur", "options": [1, 2, 3]}
curseur.execute("INSERT INTO config (data) VALUES (?)", (donnees,))
```

## 🚀 Applications Pratiques

### 1. **Gestionnaire d'Inventaire**
```python
def gestionnaire_inventaire():
    """Système de gestion d'inventaire avec SQLite"""
    import sqlite3
    from datetime import datetime

    # Connexion à la base
    conn = sqlite3.connect("inventaire.db")
    curseur = conn.cursor()

    # Création de la table
    curseur.execute("""
        CREATE TABLE IF NOT EXISTS inventaire (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            nom TEXT NOT NULL,
            quantite INTEGER DEFAULT 0,
            prix_unitaire REAL,
            date_ajout DATE DEFAULT CURRENT_DATE,
            seuil_alerte INTEGER DEFAULT 5
        )
    """)

    def ajouter_produit(nom, quantite, prix, seuil=5):
        """Ajoute un produit"""
        curseur.execute("""
            INSERT INTO inventaire (nom, quantite, prix_unitaire, seuil_alerte)
            VALUES (?, ?, ?, ?)
        """, (nom, quantite, prix, seuil))
        conn.commit()
        print(f"Produit '{nom}' ajouté")

    def vendre_produit(nom, quantite_vendue):
        """Vend une quantité d'un produit"""
        curseur.execute("SELECT quantite FROM inventaire WHERE nom = ?", (nom,))
        resultat = curseur.fetchone()

        if resultat:
            quantite_actuelle = resultat[0]
            if quantite_actuelle >= quantite_vendue:
                nouvelle_quantite = quantite_actuelle - quantite_vendue
                curseur.execute("UPDATE inventaire SET quantite = ? WHERE nom = ?", (nouvelle_quantite, nom))
                conn.commit()
                print(f"Vente de {quantite_vendue} {nom}. Stock restant : {nouvelle_quantite}")

                # Alerte si stock faible
                if nouvelle_quantite <= curseur.execute("SELECT seuil_alerte FROM inventaire WHERE nom = ?", (nom,)).fetchone()[0]:
                    print(f"⚠️  Alerte : Stock de {nom} faible ({nouvelle_quantite})")
            else:
                print(f"Stock insuffisant pour {nom}")
        else:
            print(f"Produit '{nom}' non trouvé")

    def inventaire_faible():
        """Liste les produits avec stock faible"""
        curseur.execute("""
            SELECT nom, quantite, seuil_alerte
            FROM inventaire
            WHERE quantite <= seuil_alerte
            ORDER BY quantite
        """)
        produits_faibles = curseur.fetchall()

        if produits_faibles:
            print("Produits avec stock faible :")
            for nom, quantite, seuil in produits_faibles:
                print(f"  {nom}: {quantite}/{seuil}")
        else:
            print("Aucun produit en stock faible")

    def valeur_totale():
        """Calcule la valeur totale de l'inventaire"""
        curseur.execute("SELECT SUM(quantite * prix_unitaire) FROM inventaire")
        total = curseur.fetchone()[0] or 0
        print(f"Valeur totale de l'inventaire : {total:.2f}€")
        return total

    # Test du système
    print("=== SYSTÈME D'INVENTAIRE ===")

    # Ajout de produits
    ajouter_produit("Ordinateur", 10, 800)
    ajouter_produit("Souris", 50, 25, 10)
    ajouter_produit("Clavier", 30, 45, 5)
    ajouter_produit("Écran", 5, 200, 3)

    # Ventes
    vendre_produit("Souris", 15)
    vendre_produit("Écran", 3)

    # Affichage
    inventaire_faible()
    valeur_totale()

    conn.close()

# Test
gestionnaire_inventaire()
```

### 2. **Analyseur de Logs avec Base de Données**
```python
def analyseur_logs_bd():
    """Analyseur de logs avec SQLite"""
    import sqlite3
    from datetime import datetime

    # Connexion et création de la table
    conn = sqlite3.connect("logs.db")
    curseur = conn.cursor()

    curseur.execute("""
        CREATE TABLE IF NOT EXISTS logs (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            timestamp DATETIME DEFAULT CURRENT_TIMESTAMP,
            niveau TEXT,
            module TEXT,
            message TEXT
        )
    """)

    def ajouter_log(niveau, module, message):
        """Ajoute un log"""
        curseur.execute("""
            INSERT INTO logs (niveau, module, message)
            VALUES (?, ?, ?)
        """, (niveau, module, message))
        conn.commit()

    def analyser_logs():
        """Analyse les logs"""
        # Statistiques par niveau
        curseur.execute("""
            SELECT niveau, COUNT(*) as nombre
            FROM logs
            GROUP BY niveau
            ORDER BY nombre DESC
        """)
        stats_niveau = curseur.fetchall()

        # Modules les plus actifs
        curseur.execute("""
            SELECT module, COUNT(*) as nombre
            FROM logs
            GROUP BY module
            ORDER BY nombre DESC
            LIMIT 5
        """)
        modules_actifs = curseur.fetchall()

        # Logs récents
        curseur.execute("""
            SELECT timestamp, niveau, module, message
            FROM logs
            ORDER BY timestamp DESC
            LIMIT 10
        """)
        logs_recents = curseur.fetchall()

        return {
            "stats_niveau": stats_niveau,
            "modules_actifs": modules_actifs,
            "logs_recents": logs_recents
        }

    # Ajout de logs de test
    logs_test = [
        ("INFO", "auth", "Connexion utilisateur"),
        ("ERROR", "db", "Échec de connexion"),
        ("WARNING", "api", "Timeout de requête"),
        ("INFO", "auth", "Déconnexion utilisateur"),
        ("ERROR", "db", "Requête SQL invalide"),
        ("INFO", "api", "Requête traitée"),
        ("WARNING", "auth", "Mot de passe faible"),
        ("ERROR", "api", "Erreur serveur 500")
    ]

    for log in logs_test:
        ajouter_log(*log)

    # Analyse
    analyse = analyser_logs()

    print("=== ANALYSE DES LOGS ===")
    print("Statistiques par niveau :")
    for niveau, nombre in analyse["stats_niveau"]:
        print(f"  {niveau}: {nombre}")

    print("\nModules les plus actifs :")
    for module, nombre in analyse["modules_actifs"]:
        print(f"  {module}: {nombre} logs")

    print("\nLogs récents :")
    for timestamp, niveau, module, message in analyse["logs_recents"]:
        print(f"  [{niveau}] {module}: {message}")

    conn.close()

# Test
analyseur_logs_bd()
```

### 3. **Système de Notes avec Base de Données**
```python
def systeme_notes_bd():
    """Système de gestion de notes avec SQLite"""
    import sqlite3

    # Connexion
    conn = sqlite3.connect("notes.db")
    curseur = conn.cursor()

    # Tables
    curseur.execute("""
        CREATE TABLE IF NOT EXISTS etudiants (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            nom TEXT NOT NULL,
            prenom TEXT NOT NULL,
            email TEXT UNIQUE
        )
    """)

    curseur.execute("""
        CREATE TABLE IF NOT EXISTS matieres (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            nom TEXT NOT NULL UNIQUE,
            coefficient REAL DEFAULT 1.0
        )
    """)

    curseur.execute("""
        CREATE TABLE IF NOT EXISTS notes (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            etudiant_id INTEGER,
            matiere_id INTEGER,
            note REAL,
            date_note DATE DEFAULT CURRENT_DATE,
            FOREIGN KEY (etudiant_id) REFERENCES etudiants (id),
            FOREIGN KEY (matiere_id) REFERENCES matieres (id)
        )
    """)

    def ajouter_etudiant(nom, prenom, email):
        """Ajoute un étudiant"""
        try:
            curseur.execute("""
                INSERT INTO etudiants (nom, prenom, email)
                VALUES (?, ?, ?)
            """, (nom, prenom, email))
            conn.commit()
            return curseur.lastrowid
        except sqlite3.IntegrityError:
            print(f"Étudiant avec email {email} existe déjà")
            return None

    def ajouter_matiere(nom, coefficient=1.0):
        """Ajoute une matière"""
        try:
            curseur.execute("""
                INSERT INTO matieres (nom, coefficient)
                VALUES (?, ?)
            """, (nom, coefficient))
            conn.commit()
            return curseur.lastrowid
        except sqlite3.IntegrityError:
            print(f"Matière {nom} existe déjà")
            return None

    def ajouter_note(etudiant_id, matiere_id, note):
        """Ajoute une note"""
        curseur.execute("""
            INSERT INTO notes (etudiant_id, matiere_id, note)
            VALUES (?, ?, ?)
        """, (etudiant_id, matiere_id, note))
        conn.commit()

    def calculer_moyennes():
        """Calcule les moyennes de tous les étudiants"""
        curseur.execute("""
            SELECT e.prenom, e.nom, AVG(n.note) as moyenne
            FROM etudiants e
            JOIN notes n ON e.id = n.etudiant_id
            GROUP BY e.id, e.prenom, e.nom
            ORDER BY moyenne DESC
        """)
        moyennes = curseur.fetchall()

        print("Moyennes des étudiants :")
        for prenom, nom, moyenne in moyennes:
            print(f"  {prenom} {nom}: {moyenne:.2f}/20")

        return moyennes

    # Test
    print("=== SYSTÈME DE NOTES ===")

    # Ajout d'étudiants
    etudiants = [
        ("Alice", "Dupont", "alice@univ.fr"),
        ("Bob", "Martin", "bob@univ.fr"),
        ("Clara", "Garcia", "clara@univ.fr")
    ]

    ids_etudiants = []
    for nom, prenom, email in etudiants:
        etu_id = ajouter_etudiant(nom, prenom, email)
        if etu_id:
            ids_etudiants.append(etu_id)

    # Ajout de matières
    matieres = [
        ("Mathématiques", 3.0),
        ("Physique", 2.0),
        ("Informatique", 2.0),
        ("Chimie", 1.0)
    ]

    ids_matieres = []
    for nom, coef in matieres:
        mat_id = ajouter_matiere(nom, coef)
        if mat_id:
            ids_matieres.append(mat_id)

    # Ajout de notes
    notes_test = [
        (ids_etudiants[0], ids_matieres[0], 18),  # Alice Math
        (ids_etudiants[0], ids_matieres[1], 16),  # Alice Physique
        (ids_etudiants[0], ids_matieres[2], 19),  # Alice Info
        (ids_etudiants[0], ids_matieres[3], 15),  # Alice Chimie

        (ids_etudiants[1], ids_matieres[0], 12),  # Bob Math
        (ids_etudiants[1], ids_matieres[1], 14),  # Bob Physique
        (ids_etudiants[1], ids_matieres[2], 13),  # Bob Info

        (ids_etudiants[2], ids_matieres[0], 17),  # Clara Math
        (ids_etudiants[2], ids_matieres[1], 18),  # Clara Physique
        (ids_etudiants[2], ids_matieres[2], 16),  # Clara Info
        (ids_etudiants[2], ids_matieres[3], 14),  # Clara Chimie
    ]

    for etu_id, mat_id, note in notes_test:
        ajouter_note(etu_id, mat_id, note)

    # Calcul des moyennes
    moyennes = calculer_moyennes()

    conn.close()

# Test
systeme_notes_bd()
```

## 🎯 Défis Supplémentaires

1. **Créez** un système de gestion de contacts avec SQLite
2. **Implémentez** un système de sauvegarde de configuration
3. **Développez** un analyseur de performances de requêtes
4. **Concevez** un système de migration de base de données

---

**Exercices complétés : 250/260** 🎯

*Continuez avec le [chapitre suivant](6-5-applications.md) pour les applications avancées de fichiers !*
