# Partie 6.5 : Applications Avancées de Fichiers

## 🎯 Objectifs Pédagogiques

Ce chapitre final de la Partie 6 présente des **applications avancées** combinant tous les concepts de gestion de fichiers : texte, CSV, JSON, bases de données SQLite et gestion système.

### Concepts Intégrés
- **Applications complexes** : analyse de données, sauvegarde, configuration
- **Intégration** : fichiers, bases de données, interfaces utilisateur
- **Gestion d'erreurs** : robustesse et récupération
- **Applications** : systèmes complets, automatisation

---

## 📝 Exercices Pratiques

### Exercice 251 : Rechercher un élément dans une table
**Objectif** : Implémenter une recherche dans une base de données SQLite.

```python
# Solution
import sqlite3

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

# Tests
print("=== RECHERCHE D'ÉTUDIANTS ===")

# Recherche par nom
rechercher_etudiants("nom", "Dupont")

# Recherche par filière
print("\n--- Recherche par filière ---")
rechercher_etudiants("filiere", "Informatique")

# Recherche par moyenne
print("\n--- Recherche par moyenne ---")
rechercher_etudiants("moyenne", 15)
```

**Explanation** :
- **LIKE** : recherche partielle de chaînes
- **Paramètres** : éviter l'injection SQL
- **Multiple critères** : extension possible
- **Affichage** : formatage des résultats

**Test** : Recherchez des étudiants selon différents critères.

---

### Exercice 252 : Trier les résultats d'une requête
**Objectif** : Trier les résultats de requêtes SQL.

```python
# Solution
import sqlite3

def trier_etudiants(critere="moyenne", ordre="DESC"):
    """Trie les étudiants selon un critère"""
    try:
        connexion = sqlite3.connect("etudiants.db")
        curseur = connexion.cursor()

        # Liste des colonnes valides
        colonnes_valides = ["nom", "prenom", "age", "filiere", "moyenne"]
        if critere not in colonnes_valides:
            print(f"Colonne '{critere}' invalide")
            connexion.close()
            return []

        # Construction de la requête
        requete = f"SELECT * FROM etudiants ORDER BY {critere}"

        if ordre.upper() == "ASC":
            requete += " ASC"
        else:
            requete += " DESC"

        curseur.execute(requete)
        resultats = curseur.fetchall()

        print(f"Étudiants triés par {critere} {ordre} :")
        for etudiant in resultats:
            print(f"  {etudiant[2]} {etudiant[1]}: {etudiant[4]}, Moyenne: {etudiant[5]}")

        connexion.close()
        return resultats

    except sqlite3.Error as e:
        print(f"Erreur de tri : {e}")
        return []

# Tests
print("=== TRI D'ÉTUDIANTS ===")

# Tri par moyenne décroissante
trier_etudiants("moyenne", "DESC")

# Tri par nom croissant
print("\n--- Tri par nom ---")
trier_etudiants("nom", "ASC")

# Tri par filière
print("\n--- Tri par filière ---")
trier_etudiants("filiere", "ASC")
```

**Explication** :
- **ORDER BY** : tri des résultats
- **ASC/DESC** : ordre croissant/décroissant
- **Validation** : colonnes autorisées
- **Applications** : classement, organisation

**Test** : Triez les étudiants selon différents critères.

---

### Exercice 253 : Filtrer les résultats d'une requête
**Objectif** : Appliquer des filtres complexes aux requêtes SQL.

```python
# Solution
import sqlite3

def filtrer_etudiants(filtres):
    """Filtre les étudiants selon plusieurs critères"""
    try:
        connexion = sqlite3.connect("etudiants.db")
        curseur = connexion.cursor()

        # Construction de la requête de base
        requete = "SELECT * FROM etudiants WHERE 1=1"
        parametres = []

        # Ajout des filtres
        for cle, valeur in filtres.items():
            if cle == "age_min":
                requete += " AND age >= ?"
                parametres.append(valeur)
            elif cle == "age_max":
                requete += " AND age <= ?"
                parametres.append(valeur)
            elif cle == "moyenne_min":
                requete += " AND moyenne >= ?"
                parametres.append(valeur)
            elif cle == "filiere":
                requete += " AND filiere = ?"
                parametres.append(valeur)
            elif cle == "nom_commence_par":
                requete += " AND nom LIKE ?"
                parametres.append(f"{valeur}%")

        # Ajout du tri par défaut
        requete += " ORDER BY moyenne DESC"

        curseur.execute(requete, parametres)
        resultats = curseur.fetchall()

        print(f"Filtres appliqués : {filtres}")
        print(f"Résultats : {len(resultats)} étudiants")

        for etudiant in resultats:
            print(f"  {etudiant[2]} {etudiant[1]} ({etudiant[3]} ans, {etudiant[4]}, Moyenne: {etudiant[5]})")

        connexion.close()
        return resultats

    except sqlite3.Error as e:
        print(f"Erreur de filtrage : {e}")
        return []

# Tests
print("=== FILTRAGE D'ÉTUDIANTS ===")

# Filtre simple
filtrer_etudiants({"filiere": "Informatique"})

# Filtres multiples
print("\n--- Filtres multiples ---")
filtrer_etudiants({
    "age_min": 20,
    "moyenne_min": 15
})

# Filtre par nom
print("\n--- Filtre par nom ---")
filtrer_etudiants({
    "nom_commence_par": "D"
})
```

**Explication** :
- **Filtres dynamiques** : construction conditionnelle
- **Paramètres multiples** : liste de valeurs
- **WHERE 1=1** : base pour ajouts conditionnels
- **Complexité** : plusieurs critères simultanés

**Test** : Appliquez différents filtres aux données.

---

### Exercice 254 : Joindre deux tables
**Objectif** : Effectuer des jointures entre tables SQLite.

```python
# Solution
import sqlite3

def joindre_tables():
    """Joint les tables étudiants et filières"""
    try:
        connexion = sqlite3.connect("etudiants.db")
        curseur = connexion.cursor()

        # Création d'une table filières si elle n'existe pas
        curseur.execute("""
            CREATE TABLE IF NOT EXISTS filieres (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                nom TEXT NOT NULL,
                responsable TEXT,
                nombre_etudiants INTEGER DEFAULT 0
            )
        """)

        # Insertion de données de test
        filieres_data = [
            ("Informatique", "Dr. Smith", 0),
            ("Mathématiques", "Dr. Johnson", 0),
            ("Physique", "Dr. Wilson", 0),
            ("Chimie", "Dr. Brown", 0)
        ]

        curseur.executemany("""
            INSERT OR IGNORE INTO filieres (nom, responsable)
            VALUES (?, ?)
        """, filieres_data)

        # Mise à jour du nombre d'étudiants
        curseur.execute("""
            UPDATE filieres
            SET nombre_etudiants = (
                SELECT COUNT(*) FROM etudiants
                WHERE etudiants.filiere = filieres.nom
            )
        """)

        connexion.commit()

        # Jointure LEFT JOIN
        curseur.execute("""
            SELECT e.nom, e.prenom, e.filiere, f.responsable, f.nombre_etudiants
            FROM etudiants e
            LEFT JOIN filieres f ON e.filiere = f.nom
            ORDER BY e.filiere, e.nom
        """)

        resultats = curseur.fetchall()

        print("Jointure étudiants-filières :")
        print("Nom | Prénom | Filière | Responsable | Nb étudiants")
        print("-" * 60)

        for etudiant in resultats:
            nom, prenom, filiere, responsable, nb_etudiants = etudiant
            print(f"{nom:8} | {prenom:8} | {filiere:12} | {responsable or 'N/A':12} | {nb_etudiants or 0:3d}")

        connexion.close()
        return resultats

    except sqlite3.Error as e:
        print(f"Erreur de jointure : {e}")
        return []

# Test
resultats_jointure = joindre_tables()
```

**Explication** :
- **LEFT JOIN** : jointure externe gauche
- **OR IGNORE** : insertion sans erreur si doublon
- **Sous-requête** : mise à jour avec COUNT
- **Affichage** : formatage tabulaire

**Test** : Joint les données d'étudiants et de filières.

---

### Exercice 255 : Créer des index sur une table
**Objectif** : Créer des index pour optimiser les performances.

```python
# Solution
import sqlite3

def creer_indexes():
    """Crée des index pour optimiser les requêtes"""
    try:
        connexion = sqlite3.connect("etudiants.db")
        curseur = connexion.cursor()

        # Création d'index
        index = [
            ("CREATE INDEX IF NOT EXISTS idx_nom ON etudiants (nom)", "Index sur nom"),
            ("CREATE INDEX IF NOT EXISTS idx_filiere ON etudiants (filiere)", "Index sur filière"),
            ("CREATE INDEX IF NOT EXISTS idx_moyenne ON etudiants (moyenne)", "Index sur moyenne"),
            ("CREATE INDEX IF NOT EXISTS idx_nom_filiere ON etudiants (nom, filiere)", "Index composite")
        ]

        for requete, description in index:
            curseur.execute(requete)
            print(f"✓ {description}")

        connexion.commit()

        # Affichage des index existants
        curseur.execute("""
            SELECT name, tbl_name, sql
            FROM sqlite_master
            WHERE type='index' AND tbl_name='etudiants'
        """)

        indexes = curseur.fetchall()
        print(f"\nIndex existants sur la table 'etudiants' : {len(indexes)}")

        for index_info in indexes:
            print(f"  {index_info[0]}: {index_info[2]}")

        # Test de performance avec index
        import time

        debut = time.time()
        curseur.execute("SELECT * FROM etudiants WHERE nom = ?", ("Dupont",))
        resultats = curseur.fetchall()
        fin = time.time()

        print(f"\nRecherche avec index : {fin - debut:.6f} secondes")
        print(f"Résultats : {len(resultats)}")

        connexion.close()

    except sqlite3.Error as e:
        print(f"Erreur de création d'index : {e}")

# Test
creer_indexes()
```

**Explication** :
- **CREATE INDEX** : amélioration des performances
- **Index composite** : sur plusieurs colonnes
- **IF NOT EXISTS** : évite les erreurs de doublon
- **Performance** : mesure de l'impact

**Test** : Créez et testez des index.

---

## 🔍 Points Clés à Retenir

### 1. **Jointures SQL**
```python
# Types de jointures
LEFT JOIN    # Tous les éléments de gauche + correspondances de droite
RIGHT JOIN   # Tous les éléments de droite + correspondances de gauche
INNER JOIN   # Seulement les correspondances
FULL JOIN    # Tous les éléments (non supporté par SQLite)

# Syntaxe
SELECT colonnes
FROM table1
JOIN_TYPE table2 ON condition
```

### 2. **Index et Performance**
```python
# Création d'index
CREATE INDEX nom_index ON table (colonne)

# Index composite
CREATE INDEX idx_composite ON table (col1, col2)

# Index unique
CREATE UNIQUE INDEX idx_unique ON table (colonne)

# Suppression d'index
DROP INDEX nom_index
```

### 3. **Vues SQL**
```python
# Création de vue
CREATE VIEW vue_etudiants_excellents AS
SELECT * FROM etudiants WHERE moyenne >= 16

# Utilisation de vue
SELECT * FROM vue_etudiants_excellents

# Suppression de vue
DROP VIEW vue_etudiants_excellents
```

### 4. **Transactions Avancées**
```python
# Gestion des transactions
BEGIN TRANSACTION
-- Opérations
COMMIT    -- Validation
ROLLBACK  -- Annulation

# Niveaux d'isolation
PRAGMA journal_mode = WAL  # Write-Ahead Logging
PRAGMA synchronous = NORMAL  # Performance
```

## 💡 Optimisations et Astuces

### 1. **Analyse et Optimisation**
```python
# Analyse des requêtes
EXPLAIN QUERY PLAN SELECT * FROM etudiants WHERE nom = 'Dupont'

# Statistiques de la base
ANALYZE etudiants

# Optimisation automatique
VACUUM  # Réorganisation de la base
REINDEX  # Reconstruction des index
```

### 2. **Connexions et Pools**
```python
# Connexion persistante
connexion = sqlite3.connect("base.db")

# Configuration pour les performances
connexion.execute("PRAGMA journal_mode = MEMORY")
connexion.execute("PRAGMA cache_size = 10000")

# Fermeture
connexion.close()
```

### 3. **Types Personnalisés**
```python
import sqlite3
import json

# Enregistrement d'adaptateurs
sqlite3.register_adapter(list, json.dumps)
sqlite3.register_converter("json", json.loads)

# Utilisation
curseur.execute("INSERT INTO config (data) VALUES (?)", ([1, 2, 3],))
curseur.execute("SELECT data FROM config")
resultat = curseur.fetchone()[0]  # Liste reconstruite
```

## 🚀 Applications Pratiques

### 1. **Système de Gestion de Bibliothèque**
```python
def systeme_bibliotheque():
    """Système complet de gestion de bibliothèque"""
    import sqlite3
    import csv
    from datetime import datetime

    # Connexion
    conn = sqlite3.connect("bibliotheque.db")
    curseur = conn.cursor()

    # Création des tables
    curseur.execute("""
        CREATE TABLE IF NOT EXISTS livres (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            titre TEXT NOT NULL,
            auteur TEXT NOT NULL,
            isbn TEXT UNIQUE,
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

    def ajouter_livre(titre, auteur, isbn=None, annee=None):
        """Ajoute un livre"""
        try:
            curseur.execute("""
                INSERT INTO livres (titre, auteur, isbn, annee)
                VALUES (?, ?, ?, ?)
            """, (titre, auteur, isbn, annee))
            conn.commit()
            return curseur.lastrowid
        except sqlite3.IntegrityError:
            print(f"Livre avec ISBN {isbn} existe déjà")
            return None

    def emprunter_livre(isbn, emprunteur):
        """Emprunte un livre"""
        # Trouver le livre
        curseur.execute("SELECT id, disponible FROM livres WHERE isbn = ?", (isbn,))
        resultat = curseur.fetchone()

        if resultat and resultat[1]:  # Disponible
            livre_id = resultat[0]
            curseur.execute("""
                INSERT INTO emprunts (livre_id, emprunteur)
                VALUES (?, ?)
            """, (livre_id, emprunteur))

            curseur.execute("UPDATE livres SET disponible = 0 WHERE id = ?", (livre_id,))
            conn.commit()
            print(f"Livre {isbn} emprunté par {emprunteur}")
        else:
            print(f"Livre {isbn} non disponible")

    def retourner_livre(isbn):
        """Retourne un livre"""
        # Trouver l'emprunt actif
        curseur.execute("""
            SELECT e.id, e.livre_id
            FROM emprunts e
            JOIN livres l ON e.livre_id = l.id
            WHERE l.isbn = ? AND e.date_retour IS NULL
        """, (isbn,))

        resultat = curseur.fetchone()

        if resultat:
            emprunt_id, livre_id = resultat
            curseur.execute("UPDATE emprunts SET date_retour = CURRENT_DATE WHERE id = ?", (emprunt_id,))
            curseur.execute("UPDATE livres SET disponible = 1 WHERE id = ?", (livre_id,))
            conn.commit()
            print(f"Livre {isbn} retourné")
        else:
            print(f"Aucun emprunt actif pour {isbn}")

    def exporter_csv(nom_fichier):
        """Exporte les données en CSV"""
        curseur.execute("""
            SELECT l.titre, l.auteur, l.isbn, l.annee,
                   CASE WHEN l.disponible = 1 THEN 'Disponible' ELSE 'Emprunté' END as statut,
                   e.emprunteur, e.date_emprunt, e.date_retour
            FROM livres l
            LEFT JOIN emprunts e ON l.id = e.livre_id
            ORDER BY l.titre
        """)

        with open(nom_fichier, 'w', newline='', encoding='utf-8') as f:
            writer = csv.writer(f)
            writer.writerow(['Titre', 'Auteur', 'ISBN', 'Année', 'Statut', 'Emprunteur', 'Date emprunt', 'Date retour'])
            writer.writerows(curseur.fetchall())

        print(f"Données exportées vers {nom_fichier}")

    # Test
    print("=== SYSTÈME DE BIBLIOTHÈQUE ===")

    # Ajout de livres
    ajouter_livre("1984", "George Orwell", "978-0451524935", 1949)
    ajouter_livre("Python Crash Course", "Eric Matthes", "978-1593276034", 2015)
    ajouter_livre("Le Petit Prince", "Antoine de Saint-Exupéry", "978-2070612758", 1943)

    # Emprunts
    emprunter_livre("978-0451524935", "Alice")
    emprunter_livre("978-1593276034", "Bob")

    # Export CSV
    exporter_csv("bibliotheque_export.csv")

    conn.close()

# Test
systeme_bibliotheque()
```

### 2. **Analyseur de Performances**
```python
def analyseur_performances():
    """Analyseur de performances de base de données"""
    import sqlite3
    import time

    # Connexion à une base de test
    conn = sqlite3.connect("performances.db")
    curseur = conn.cursor()

    # Création d'une table de test
    curseur.execute("""
        CREATE TABLE IF NOT EXISTS test_data (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            nom TEXT,
            valeur INTEGER,
            categorie TEXT
        )
    """)

    # Insertion de données de test
    import random
    donnees_test = [(f"Element_{i}", random.randint(1, 1000), f"Cat_{i%10}") for i in range(10000)]
    curseur.executemany("INSERT INTO test_data (nom, valeur, categorie) VALUES (?, ?, ?)", donnees_test)
    conn.commit()

    def mesurer_temps(operation, requete, params=None):
        """Mesure le temps d'une opération"""
        debut = time.time()
        curseur.execute(requete, params or [])
        resultat = curseur.fetchall()
        fin = time.time()

        print(f"{operation}: {fin - debut:.4f}s ({len(resultat)} résultats)")
        return fin - debut

    # Tests sans index
    print("=== TESTS SANS INDEX ===")
    t1 = mesurer_temps("Recherche par nom", "SELECT * FROM test_data WHERE nom = ?", ("Element_5000",))
    t2 = mesurer_temps("Recherche par valeur", "SELECT * FROM test_data WHERE valeur > ?", (500,))
    t3 = mesurer_temps("Tri par catégorie", "SELECT * FROM test_data ORDER BY categorie, valeur")

    # Création d'index
    print("\n=== CRÉATION D'INDEX ===")
    curseur.execute("CREATE INDEX IF NOT EXISTS idx_nom ON test_data (nom)")
    curseur.execute("CREATE INDEX IF NOT EXISTS idx_valeur ON test_data (valeur)")
    curseur.execute("CREATE INDEX IF NOT EXISTS idx_categorie ON test_data (categorie)")
    conn.commit()

    # Tests avec index
    print("\n=== TESTS AVEC INDEX ===")
    t4 = mesurer_temps("Recherche par nom (index)", "SELECT * FROM test_data WHERE nom = ?", ("Element_5000",))
    t5 = mesurer_temps("Recherche par valeur (index)", "SELECT * FROM test_data WHERE valeur > ?", (500,))
    t6 = mesurer_temps("Tri par catégorie (index)", "SELECT * FROM test_data ORDER BY categorie, valeur")

    print("
=== COMPARAISON ===")
    print(f"Recherche nom : sans index={t1:.4f}s, avec index={t4:.4f}s (gain: {t1/t4:.1f}x)")
    print(f"Recherche valeur : sans index={t2:.4f}s, avec index={t5:.4f}s (gain: {t2/t5:.1f}x)")
    print(f"Tri catégorie : sans index={t3:.4f}s, avec index={t6:.4f}s (gain: {t3/t6:.1f}x)")

    conn.close()

# Test
analyseur_performances()
```

### 3. **Système de Sauvegarde**
```python
def systeme_sauvegarde():
    """Système de sauvegarde automatique"""
    import sqlite3
    import os
    import shutil
    from datetime import datetime

    # Base source
    source_db = "etudiants.db"
    backup_dir = "backups"

    # Création du répertoire de sauvegarde
    os.makedirs(backup_dir, exist_ok=True)

    def creer_sauvegarde():
        """Crée une sauvegarde de la base"""
        timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
        backup_file = os.path.join(backup_dir, f"etudiants_backup_{timestamp}.db")

        try:
            # Copie de la base
            shutil.copy2(source_db, backup_file)
            print(f"Sauvegarde créée : {backup_file}")

            # Nettoyage des anciennes sauvegardes (garder les 5 dernières)
            backups = sorted([f for f in os.listdir(backup_dir) if f.startswith("etudiants_backup_")])
            if len(backups) > 5:
                for old_backup in backups[:-5]:
                    os.remove(os.path.join(backup_dir, old_backup))
                    print(f"Ancienne sauvegarde supprimée : {old_backup}")

            return backup_file

        except Exception as e:
            print(f"Erreur sauvegarde : {e}")
            return None

    def restaurer_sauvegarde(backup_file):
        """Restaure depuis une sauvegarde"""
        if not os.path.exists(backup_file):
            print(f"Sauvegarde '{backup_file}' non trouvée")
            return False

        try:
            # Vérification de la sauvegarde
            test_conn = sqlite3.connect(backup_file)
            test_conn.execute("SELECT name FROM sqlite_master WHERE type='table'")
            test_conn.close()

            # Restauration
            shutil.copy2(backup_file, source_db)
            print(f"Base restaurée depuis {backup_file}")
            return True

        except Exception as e:
            print(f"Erreur restauration : {e}")
            return False

    def lister_sauvegardes():
        """Liste les sauvegardes disponibles"""
        if not os.path.exists(backup_dir):
            return []

        backups = [f for f in os.listdir(backup_dir) if f.startswith("etudiants_backup_")]
        return sorted(backups)

    # Test
    print("=== SYSTÈME DE SAUVEGARDE ===")

    # Création de sauvegardes
    sauvegarde1 = creer_sauvegarde()
    import time
    time.sleep(1)  # Pause d'1 seconde
    sauvegarde2 = creer_sauvegarde()

    # Liste des sauvegardes
    sauvegardes = lister_sauvegardes()
    print(f"\nSauvegardes disponibles ({len(sauvegardes)}) :")
    for backup in sauvegardes:
        print(f"  {backup}")

    # Restauration (optionnel)
    if sauvegardes:
        print(f"\nRestauration depuis la sauvegarde la plus récente...")
        restaurer_sauvegarde(os.path.join(backup_dir, sauvegardes[-1]))

# Test
systeme_sauvegarde()
```

## 🎯 Bilan de la Partie 6

### Concepts Maîtrisés
✅ **Fichiers texte** : lecture, écriture, manipulation
✅ **Fichiers CSV** : parsing, génération, analyse
✅ **Fichiers JSON** : sérialisation, désérialisation, configuration
✅ **Bases de données SQLite** : création, requêtes, index
✅ **Gestion système** : existence, suppression, organisation
✅ **Applications intégrées** : sauvegarde, analyse, configuration

### Compétences Développées
- **Persistance de données** : fichiers et bases de données
- **Manipulation de formats** : texte, structuré, binaire
- **Gestion de fichiers** : organisation et maintenance
- **Optimisation** : index, requêtes, performances
- **Robustesse** : gestion d'erreurs et validation

---

**🏁 FIN DE LA PARTIE 6 - BRAVO !**

**Exercices complétés : 255/260** 🎯

*Félicitations ! Vous avez terminé la gestion de fichiers et bases de données. Continuez avec la [Partie 7](Partie%207%20-%20Algorithmes/7-1-nombres.md) pour les algorithmes et mathématiques !*
