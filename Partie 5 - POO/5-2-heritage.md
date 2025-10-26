# Partie 5.2 : Héritage et Polymorphisme

## 🎯 Objectifs Pédagogiques

Ce chapitre explore l'**héritage** et le **polymorphisme** en Python, concepts essentiels de la POO pour la **réutilisation du code** et la **flexibilité des programmes**.

### Concepts Abordés
- **Héritage** : classes filles héritant des classes mères
- **Polymorphisme** : méthodes communes avec implémentations différentes
- **Surcharge** : redéfinition des méthodes dans les classes filles
- **Applications** : modélisation hiérarchique, interfaces communes

---

## 📝 Exercices Pratiques

### Exercice 206 : Créer une classe Rectangle avec largeur et hauteur
**Objectif** : Modéliser une forme géométrique avec calculs.

```python
# Solution
class Rectangle:
    """Classe Rectangle avec calculs d'aire et périmètre"""

    def __init__(self, largeur, hauteur):
        """Constructeur"""
        self.largeur = largeur
        self.hauteur = hauteur

    def calculer_aire(self):
        """Calcule l'aire du rectangle"""
        return self.largeur * self.hauteur

    def calculer_perimetre(self):
        """Calcule le périmètre du rectangle"""
        return 2 * (self.largeur + self.hauteur)

    def est_carre(self):
        """Vérifie si c'est un carré"""
        return self.largeur == self.hauteur

    def info(self):
        """Informations du rectangle"""
        type_forme = "Carré" if self.est_carre() else "Rectangle"
        return f"{type_forme} : {self.largeur} × {self.hauteur}, Aire = {self.calculer_aire()}, Périmètre = {self.calculer_perimetre()}"

# Tests
rectangles = [
    Rectangle(5, 10),
    Rectangle(4, 4),   # Carré
    Rectangle(3, 7),
    Rectangle(12, 8)
]

print("Tests des rectangles :")
for i, rect in enumerate(rectangles):
    print(f"Rectangle {i+1} : {rect.info()}")

# Tests spécifiques
carre = Rectangle(6, 6)
print(f"\nCarré : {carre.info()}")
print(f"Est un carré : {carre.est_carre()}")

rectangle = Rectangle(5, 10)
print(f"Rectangle : {rectangle.info()}")
print(f"Est un carré : {rectangle.est_carre()}")
```

**Explication** :
- **Attributs géométriques** : largeur, hauteur
- **Méthodes de calcul** : aire, périmètre
- **Validation** : test de carrée
- **Applications** : géométrie, design, construction

**Test** : Calculs d'aires et périmètres.

---

### Exercice 207 : Ajouter méthode pour calculer la surface
**Objectif** : Étendre la classe Rectangle avec des méthodes de surface.

```python
# Solution
class Rectangle:
    """Rectangle avec calculs étendus"""

    def __init__(self, largeur, hauteur):
        """Constructeur"""
        self.largeur = largeur
        self.hauteur = hauteur

    def calculer_aire(self):
        """Aire du rectangle"""
        return self.largeur * self.hauteur

    def calculer_perimetre(self):
        """Périmètre du rectangle"""
        return 2 * (self.largeur + self.hauteur)

    def calculer_diagonale(self):
        """Calcule la longueur de la diagonale"""
        import math
        return math.sqrt(self.largeur**2 + self.hauteur**2)

    def redimensionner(self, facteur):
        """Redimensionne le rectangle"""
        self.largeur *= facteur
        self.hauteur *= facteur
        return f"Redimensionnement ×{facteur}. Nouvelles dimensions : {self.largeur} × {self.hauteur}"

    def info(self):
        """Informations complètes"""
        return (f"Rectangle {self.largeur}×{self.hauteur} | "
                f"Aire: {self.calculer_aire()} | "
                f"Périmètre: {self.calculer_perimetre()} | "
                f"Diagonale: {self.calculer_diagonale():.2f}")

# Tests
rect = Rectangle(6, 8)
print(rect.info())

print(rect.redimensionner(2))
print(rect.info())

print(rect.redimensionner(0.5))
print(rect.info())

# Tests avec différentes dimensions
dimensions = [(3, 4), (5, 5), (7, 2), (10, 15)]
print("\nDifférentes dimensions :")
for larg, haut in dimensions:
    rect_test = Rectangle(larg, haut)
    print(f"{larg}×{haut} : {rect_test.info()}")
```

**Explication** :
- **Diagonale** : théorème de Pythagore
- **Redimensionnement** : multiplication par facteur
- **Math** : import pour racine carrée
- **Applications** : transformations, échelles

**Test** : Calculs étendus sur rectangles.

---

### Exercice 208 : Créer une classe Cercle avec rayon
**Objectif** : Modéliser un cercle avec ses propriétés géométriques.

```python
# Solution
class Cercle:
    """Classe Cercle avec calculs géométriques"""

    def __init__(self, rayon):
        """Constructeur"""
        self.rayon = rayon

    def calculer_aire(self):
        """Calcule l'aire du cercle"""
        import math
        return math.pi * self.rayon**2

    def calculer_circonference(self):
        """Calcule la circonférence"""
        import math
        return 2 * math.pi * self.rayon

    def calculer_diametre(self):
        """Calcule le diamètre"""
        return 2 * self.rayon

    def redimensionner(self, facteur):
        """Redimensionne le cercle"""
        self.rayon *= facteur
        return f"Redimensionnement ×{facteur}. Nouveau rayon : {self.rayon}"

    def info(self):
        """Informations du cercle"""
        return (f"Cercle (rayon={self.rayon}) | "
                f"Diamètre: {self.calculer_diametre()} | "
                f"Aire: {self.calculer_aire():.2f} | "
                f"Circonférence: {self.calculer_circonference():.2f}")

# Tests
cercles = [
    Cercle(5),    # Rayon 5
    Cercle(3.5),  # Rayon 3.5
    Cercle(10),   # Rayon 10
    Cercle(1)     # Rayon 1
]

print("Tests des cercles :")
for i, cercle in enumerate(cercles):
    print(f"Cercle {i+1} : {cercle.info()}")

# Test de redimensionnement
cercle_test = Cercle(4)
print(f"\n{cercle_test.info()}")
print(cercle_test.redimensionner(2))
print(cercle_test.info())
print(cercle_test.redimensionner(0.25))
print(cercle_test.info())
```

**Explication** :
- **math.pi** : constante π
- **Formules** : aire = πr², circonférence = 2πr
- **Diamètre** : 2 × rayon
- **Redimensionnement** : proportionnel au rayon

**Test** : Calculs sur différents cercles.

---

### Exercice 209 : Ajouter méthode pour calculer le périmètre du cercle
**Objectif** : Étendre la classe Cercle avec le périmètre.

```python
# Solution
class Cercle:
    """Cercle avec périmètre (circonférence)"""

    def __init__(self, rayon):
        """Constructeur"""
        self.rayon = rayon

    def calculer_aire(self):
        """Aire du cercle"""
        import math
        return math.pi * self.rayon**2

    def calculer_perimetre(self):
        """Périmètre (circonférence) du cercle"""
        import math
        return 2 * math.pi * self.rayon

    def calculer_diametre(self):
        """Diamètre du cercle"""
        return 2 * self.rayon

    def info(self):
        """Informations complètes"""
        return (f"Cercle (r={self.rayon}) | "
                f"Ø: {self.calculer_diametre()} | "
                f"Aire: {self.calculer_aire():.2f} | "
                f"Périmètre: {self.calculer_perimetre():.2f}")

# Tests
cercles_tests = [1, 2, 5, 10, 3.14]
print("Cercles avec périmètre :")
for rayon in cercles_tests:
    cercle = Cercle(rayon)
    print(cercle.info())

# Comparaison aire/périmètre
print("\nComparaison aire/périmètre :")
for rayon in [1, 2, 3, 4, 5]:
    cercle = Cercle(rayon)
    rapport = cercle.calculer_aire() / cercle.calculer_perimetre()
    print(f"r={rayon}: aire/périmètre = {rapport:.2f}")
```

**Explication** :
- **Périmètre = circonférence** : 2πr
- **Rapport aire/périmètre** : πr/2
- **Applications** : physique, ingénierie, design

**Test** : Périmètres et rapports.

---

### Exercice 210 : Créer une classe Etudiant héritant de Personne
**Objectif** : Implémenter l'héritage avec une classe fille.

```python
# Solution
class Personne:
    """Classe de base Personne"""

    def __init__(self, nom, age):
        """Constructeur"""
        self.nom = nom
        self.age = age

    def se_presenter(self):
        """Présentation de base"""
        return f"Je m'appelle {self.nom} et j'ai {self.age} ans"

    def est_majeur(self):
        """Test de majorité"""
        return self.age >= 18

class Etudiant(Personne):
    """Classe Etudiant héritant de Personne"""

    def __init__(self, nom, age, numero_etudiant, niveau="Licence"):
        """Constructeur d'Etudiant"""
        # Appel du constructeur parent
        super().__init__(nom, age)
        self.numero_etudiant = numero_etudiant
        self.niveau = niveau
        self.notes = []

    def ajouter_note(self, note):
        """Ajoute une note"""
        if 0 <= note <= 20:
            self.notes.append(note)
            return f"Note {note}/20 ajoutée"
        return "Note invalide"

    def calculer_moyenne(self):
        """Calcule la moyenne des notes"""
        if not self.notes:
            return 0
        return sum(self.notes) / len(self.notes)

    def se_presenter(self):
        """Surcharge de la méthode parente"""
        presentation_base = super().se_presenter()
        return f"{presentation_base}. Je suis étudiant {self.niveau} (n°{self.numero_etudiant})"

    def info(self):
        """Informations complètes de l'étudiant"""
        return (f"{self.se_presenter()}\n"
                f"Moyenne: {self.calculer_moyenne():.2f}/20\n"
                f"Notes: {self.notes}")

# Tests
etudiants = [
    Etudiant("Alice", 20, "ETU001", "Licence 3"),
    Etudiant("Bob", 22, "ETU002", "Master 1"),
    Etudiant("Charlie", 19, "ETU003", "Licence 2")
]

print("Tests d'héritage :")
for etudiant in etudiants:
    print(f"\n--- {etudiant.nom} ---")
    print(f"Présentation : {etudiant.se_presenter()}")
    print(f"Majeur : {etudiant.est_majeur()}")
    print(f"Niveau : {etudiant.niveau}")
    print(f"Numéro : {etudiant.numero_etudiant}")

# Ajout de notes
print("\nAjout de notes :")
etudiants[0].ajouter_note(15)
etudiants[0].ajouter_note(17)
etudiants[0].ajouter_note(14)

etudiants[1].ajouter_note(12)
etudiants[1].ajouter_note(16)

print(etudiants[0].info())
print(f"\nMoyenne de Bob : {etudiants[1].calculer_moyenne():.2f}/20")
```

**Explication** :
- **super()** : appel du constructeur parent
- **Héritage** : Etudiant hérite de Personne
- **Surcharge** : redéfinition de se_presenter()
- **Attributs spécifiques** : notes, niveau, numéro
- **Polymorphisme** : même méthode, comportement différent

**Test** : Héritage et méthodes spécialisées.

---

### Exercice 211 : Ajouter un attribut note à Etudiant
**Objectif** : Étendre la classe Etudiant avec la gestion des notes.

```python
# Solution
class Etudiant(Personne):
    """Etudiant avec gestion avancée des notes"""

    def __init__(self, nom, age, numero_etudiant, filiere="Informatique"):
        """Constructeur"""
        super().__init__(nom, age)
        self.numero_etudiant = numero_etudiant
        self.filiere = filiere
        self.notes = {}
        self.matieres = []

    def ajouter_matiere(self, matiere):
        """Ajoute une matière"""
        if matiere not in self.matieres:
            self.matieres.append(matiere)
            self.notes[matiere] = []
        return f"Matière {matiere} ajoutée"

    def ajouter_note(self, matiere, note):
        """Ajoute une note pour une matière"""
        if matiere in self.matieres:
            if 0 <= note <= 20:
                self.notes[matiere].append(note)
                return f"Note {note}/20 ajoutée en {matiere}"
            return "Note invalide (0-20)"
        return f"Matière {matiere} non trouvée"

    def moyenne_matiere(self, matiere):
        """Moyenne d'une matière"""
        if matiere in self.notes and self.notes[matiere]:
            return sum(self.notes[matiere]) / len(self.notes[matiere])
        return 0

    def moyenne_generale(self):
        """Moyenne générale"""
        if not self.matieres:
            return 0

        total = 0
        for matiere in self.matieres:
            total += self.moyenne_matiere(matiere)
        return total / len(self.matieres)

    def mention(self):
        """Mention selon la moyenne"""
        moyenne = self.moyenne_generale()
        if moyenne >= 16:
            return "Très bien"
        elif moyenne >= 14:
            return "Bien"
        elif moyenne >= 12:
            return "Assez bien"
        elif moyenne >= 10:
            return "Passable"
        else:
            return "Insuffisant"

    def bulletin(self):
        """Bulletin complet"""
        print(f"\n=== BULLETIN {self.nom.upper()} ===")
        print(f"Numéro: {self.numero_etudiant}")
        print(f"Filière: {self.filiere}")
        print(f"Moyenne générale: {self.moyenne_generale():.2f}/20")
        print(f"Mention: {self.mention()}")

        for matiere in self.matieres:
            notes = self.notes[matiere]
            moyenne_mat = self.moyenne_matiere(matiere)
            print(f"  {matiere}: {notes} (moy: {moyenne_mat:.2f}/20)")

        print("=" * 40)

# Tests
etudiants = [
    Etudiant("Diana", 21, "ETU004", "Mathématiques"),
    Etudiant("Eve", 23, "ETU005", "Physique")
]

# Ajout de matières et notes
etudiants[0].ajouter_matiere("Algèbre")
etudiants[0].ajouter_matiere("Analyse")
etudiants[0].ajouter_note("Algèbre", 18)
etudiants[0].ajouter_note("Algèbre", 16)
etudiants[0].ajouter_note("Analyse", 17)

etudiants[1].ajouter_matiere("Mécanique")
etudiants[1].ajouter_matiere("Thermodynamique")
etudiants[1].ajouter_note("Mécanique", 14)
etudiants[1].ajouter_note("Mécanique", 15)
etudiants[1].ajouter_note("Thermodynamique", 13)
etudiants[1].ajouter_note("Thermodynamique", 16)

# Affichage des bulletins
for etudiant in etudiants:
    etudiant.bulletin()
```

**Explication** :
- **Attributs étendus** : filière, notes par matière
- **Gestion des matières** : ajout et suivi
- **Moyennes** : par matière et générale
- **Bulletin** : affichage structuré

**Test** : Gestion complète des notes d'étudiants.

---

### Exercice 212 : Ajouter une méthode pour afficher la note
**Objectif** : Étendre Etudiant avec l'affichage des notes.

```python
# Solution
class Etudiant(Personne):
    """Etudiant avec affichage des notes"""

    def __init__(self, nom, age, numero_etudiant, annee_etude=1):
        """Constructeur"""
        super().__init__(nom, age)
        self.numero_etudiant = numero_etudiant
        self.annee_etude = annee_etude
        self.notes = []

    def ajouter_note(self, note, matiere="Générale"):
        """Ajoute une note avec matière"""
        if 0 <= note <= 20:
            self.notes.append({"note": note, "matiere": matiere})
            return f"Note {note}/20 en {matiere} ajoutée"
        return "Note invalide"

    def afficher_notes(self):
        """Affiche toutes les notes"""
        if not self.notes:
            return f"{self.nom} n'a pas encore de notes"

        resultat = f"\nNotes de {self.nom} (Année {self.annee_etude}) :"
        for note_info in self.notes:
            resultat += f"\n  {note_info['matiere']}: {note_info['note']}/20"

        # Statistiques
        notes_valeurs = [n["note"] for n in self.notes]
        resultat += f"\n  Moyenne: {sum(notes_valeurs) / len(notes_valeurs):.2f}/20"
        resultat += f"\n  Meilleure note: {max(notes_valeurs)}/20"
        resultat += f"\n  Moins bonne note: {min(notes_valeurs)}/20"

        return resultat

    def moyenne_par_matiere(self):
        """Moyenne par matière"""
        from collections import defaultdict
        moyennes = defaultdict(list)

        for note_info in self.notes:
            moyennes[note_info["matiere"]].append(note_info["note"])

        return {matiere: sum(notes) / len(notes) for matiere, notes in moyennes.items()}

    def se_presenter(self):
        """Présentation personnalisée"""
        base = super().se_presenter()
        return f"{base}. Étudiant année {self.annee_etude} (n°{self.numero_etudiant})"

# Tests
etudiants = [
    Etudiant("Frank", 20, "ETU006", 2),
    Etudiant("Grace", 21, "ETU007", 3)
]

# Ajout de notes variées
etudiants[0].ajouter_note(15, "Mathématiques")
etudiants[0].ajouter_note(13, "Physique")
etudiants[0].ajouter_note(17, "Informatique")
etudiants[0].ajouter_note(16, "Mathématiques")

etudiants[1].ajouter_note(18, "Chimie")
etudiants[1].ajouter_note(16, "Biologie")
etudiants[1].ajouter_note(19, "Chimie")
etudiants[1].ajouter_note(14, "Physique")

print("Tests d'affichage des notes :")
for etudiant in etudiants:
    print(etudiant.se_presenter())
    print(etudiant.afficher_notes())
    print(f"Moyennes par matière : {etudiant.moyenne_par_matiere()}")
    print()
```

**Explication** :
- **Notes structurées** : dictionnaire note/matière
- **Affichage formaté** : présentation claire
- **Statistiques** : moyenne, min, max
- **Moyennes par matière** : regroupement

**Test** : Affichage détaillé des notes.

---

### Exercice 213 : Créer une classe Professeur héritant de Personne
**Objectif** : Implémenter une autre classe fille de Personne.

```python
# Solution
class Professeur(Personne):
    """Classe Professeur héritant de Personne"""

    def __init__(self, nom, age, matiere, grade="Maître de conférences"):
        """Constructeur"""
        super().__init__(nom, age)
        self.matiere = matiere
        self.grade = grade
        self.etudiants = []

    def enseigner(self):
        """Méthode d'enseignement"""
        return f"{self.nom} enseigne {self.matiere} (grade: {self.grade})"

    def noter_etudiant(self, etudiant, note, matiere=None):
        """Note un étudiant"""
        matiere = matiere or self.matiere
        etudiant.ajouter_note(note, matiere)
        return f"Note {note}/20 attribuée à {etudiant.nom} en {matiere}"

    def ajouter_etudiant(self, etudiant):
        """Ajoute un étudiant à la classe"""
        if etudiant not in self.etudiants:
            self.etudiants.append(etudiant)
            return f"Étudiant {etudiant.nom} ajouté à la classe"
        return f"Étudiant {etudiant.nom} déjà dans la classe"

    def liste_etudiants(self):
        """Liste les étudiants"""
        if not self.etudiants:
            return f"{self.nom} n'a pas d'étudiants"

        resultat = f"\nÉtudiants de {self.nom} ({self.matiere}) :"
        for etudiant in self.etudiants:
            resultat += f"\n  - {etudiant.nom} (n°{etudiant.numero_etudiant})"

        return resultat

    def se_presenter(self):
        """Présentation de professeur"""
        base = super().se_presenter()
        return f"{base}. Je suis professeur de {self.matiere} (grade: {self.grade})"

# Tests
professeurs = [
    Professeur("Dr. Smith", 45, "Informatique", "Professeur"),
    Professeur("Dr. Johnson", 38, "Mathématiques", "Maître de conférences")
]

etudiants = [
    Etudiant("Harry", 20, "ETU008", 2),
    Etudiant("Iris", 21, "ETU009", 2),
    Etudiant("Jack", 19, "ETU010", 1)
]

print("Tests d'héritage avec Professeur :")
for prof in professeurs:
    print(f"\n--- {prof.nom} ---")
    print(prof.se_presenter())
    print(prof.enseigner())

# Ajout d'étudiants
professeurs[0].ajouter_etudiant(etudiants[0])
professeurs[0].ajouter_etudiant(etudiants[1])
professeurs[1].ajouter_etudiant(etudiants[2])

print(professeurs[0].liste_etudiants())
print(professeurs[1].liste_etudiants())

# Notation
print(f"\n{professeurs[0].noter_etudiant(etudiants[0], 17, 'Python')}")
print(f"{professeurs[0].noter_etudiant(etudiants[1], 15, 'Algorithmique')}")
print(f"{professeurs[1].noter_etudiant(etudiants[2], 14, 'Algèbre')}")

# Affichage des notes
for etudiant in etudiants:
    print(f"\n{etudiant.afficher_notes()}")
```

**Explication** :
- **Héritage multiple** : Professeur hérite aussi de Personne
- **Méthodes spécialisées** : enseigner, noter, gérer étudiants
- **Relations** : professeur ↔ étudiants
- **Grade** : attribut spécifique aux professeurs

**Test** : Gestion professeur-étudiants.

---

### Exercice 214 : Ajouter méthode pour afficher la matière enseignée
**Objectif** : Étendre Professeur avec l'affichage de la matière.

```python
# Solution
class Professeur(Personne):
    """Professeur avec affichage de matière"""

    def __init__(self, nom, age, matiere, experience=0):
        """Constructeur"""
        super().__init__(nom, age)
        self.matiere = matiere
        self.experience = experience  # années d'expérience
        self.publications = []

    def ajouter_publication(self, titre):
        """Ajoute une publication"""
        self.publications.append(titre)
        return f"Publication '{titre}' ajoutée"

    def afficher_matiere(self):
        """Affiche la matière enseignée"""
        return f"Matière enseignée : {self.matiere} ({self.experience} ans d'expérience)"

    def cv(self):
        """Affiche le CV du professeur"""
        cv = f"\n=== CV de {self.nom.upper()} ==="
        cv += f"\nÂge : {self.age} ans"
        cv += f"\nMatière : {self.matiere}"
        cv += f"\nExpérience : {self.experience} ans"
        cv += f"\nPublications : {len(self.publications)}"

        if self.publications:
            cv += "\nListe des publications :"
            for pub in self.publications:
                cv += f"\n  - {pub}"

        return cv

    def se_presenter(self):
        """Présentation professorale"""
        base = super().se_presenter()
        return f"{base}. Professeur de {self.matiere} depuis {self.experience} ans"

# Tests
professeurs = [
    Professeur("Dr. Wilson", 50, "Intelligence Artificielle", 15),
    Professeur("Dr. Brown", 42, "Bases de Données", 8)
]

# Ajout de publications
professeurs[0].ajouter_publication("L'IA et l'avenir")
professeurs[0].ajouter_publication("Machine Learning avancé")
professeurs[1].ajouter_publication("SQL et optimisation")

print("Tests étendus des professeurs :")
for prof in professeurs:
    print(prof.se_presenter())
    print(prof.afficher_matiere())
    print(prof.cv())
    print()
```

**Explication** :
- **Expérience** : années d'enseignement
- **Publications** : liste des travaux
- **CV** : présentation complète
- **Méthodes spécialisées** : affichage matière

**Test** : CV et présentations de professeurs.

---

## 🔍 Points Clés à Retenir

### 1. **Héritage Simple**
```python
class Parent:
    def __init__(self, nom):
        self.nom = nom

    def se_presenter(self):
        return f"Je suis {self.nom}"

class Enfant(Parent):
    def __init__(self, nom, age):
        super().__init__(nom)  # Appel constructeur parent
        self.age = age

    def se_presenter(self):  # Surcharge
        return f"{super().se_presenter()}, j'ai {self.age} ans"
```

### 2. **Héritage Multiple**
```python
class A:
    def methode_a(self):
        return "Méthode A"

class B:
    def methode_b(self):
        return "Méthode B"

class C(A, B):  # Hérite de A et B
    def methode_c(self):
        return "Méthode C"

# Utilisation
c = C()
print(c.methode_a())  # "Méthode A"
print(c.methode_b())  # "Méthode B"
print(c.methode_c())  # "Méthode C"
```

### 3. **Polymorphisme**
```python
class Animal:
    def faire_du_bruit(self):
        return "Bruit générique"

class Chien(Animal):
    def faire_du_bruit(self):
        return "Woof!"

class Chat(Animal):
    def faire_du_bruit(self):
        return "Miaou!"

# Polymorphisme : même méthode, comportement différent
animaux = [Chien(), Chat(), Animal()]
for animal in animaux:
    print(animal.faire_du_bruit())  # Appels polymorphes
```

### 4. **Surcharge de Méthodes**
```python
class Base:
    def calculer(self, x, y):
        return x + y

class Derivee(Base):
    def calculer(self, x, y):  # Surcharge
        # Peut utiliser super() pour étendre
        resultat_base = super().calculer(x, y)
        return resultat_base * 2

# Test
base = Base()
derivee = Derivee()
print(base.calculer(5, 3))    # 8
print(derivee.calculer(5, 3)) # 16 (8 * 2)
```

## 💡 Optimisations et Astuces

### 1. **Héritage et isinstance**
```python
# Test de type
class Forme:
    pass

class Cercle(Forme):
    pass

class Rectangle(Forme):
    pass

def traiter_forme(forme):
    if isinstance(forme, Cercle):
        return "C'est un cercle"
    elif isinstance(forme, Rectangle):
        return "C'est un rectangle"
    elif isinstance(forme, Forme):
        return "C'est une forme"
    else:
        return "Type inconnu"

# Tests
formes = [Cercle(), Rectangle(), Forme()]
for forme in formes:
    print(traiter_forme(forme))
```

### 2. **Méthodes Abstraites (ABC)**
```python
from abc import ABC, abstractmethod

class FormeGeometrique(ABC):
    @abstractmethod
    def calculer_aire(self):
        pass

    @abstractmethod
    def calculer_perimetre(self):
        pass

class Cercle(FormeGeometrique):
    def __init__(self, rayon):
        self.rayon = rayon

    def calculer_aire(self):
        return 3.14159 * self.rayon**2

    def calculer_perimetre(self):
        return 2 * 3.14159 * self.rayon
```

### 3. **Composition vs Héritage**
```python
# Héritage
class Moteur:
    def demarrer(self):
        return "Moteur démarré"

class Voiture(Moteur):
    pass

# Composition (souvent préférable)
class Moteur:
    def demarrer(self):
        return "Moteur démarré"

class Voiture:
    def __init__(self):
        self.moteur = Moteur()  # Composition

    def demarrer(self):
        return self.moteur.demarrer()
```

## 🚀 Applications Pratiques

### 1. **Système de Formes Géométriques**
```python
class Forme:
    """Classe de base pour les formes géométriques"""
    def __init__(self, nom):
        self.nom = nom

    def aire(self):
        """À implémenter dans les classes filles"""
        raise NotImplementedError("Méthode abstraite")

    def perimetre(self):
        """À implémenter dans les classes filles"""
        raise NotImplementedError("Méthode abstraite")

    def info(self):
        return f"{self.nom}: aire={self.aire():.2f}, périmètre={self.perimetre():.2f}"

class Cercle(Forme):
    def __init__(self, rayon):
        super().__init__("Cercle")
        self.rayon = rayon

    def aire(self):
        import math
        return math.pi * self.rayon**2

    def perimetre(self):
        import math
        return 2 * math.pi * self.rayon

class Rectangle(Forme):
    def __init__(self, largeur, hauteur):
        super().__init__("Rectangle")
        self.largeur = largeur
        self.hauteur = hauteur

    def aire(self):
        return self.largeur * self.hauteur

    def perimetre(self):
        return 2 * (self.largeur + self.hauteur)

    def est_carre(self):
        return self.largeur == self.hauteur

class Triangle(Forme):
    def __init__(self, base, hauteur, a, b, c):
        super().__init__("Triangle")
        self.base = base
        self.hauteur = hauteur
        self.cote_a = a
        self.cote_b = b
        self.cote_c = c

    def aire(self):
        return (self.base * self.hauteur) / 2

    def perimetre(self):
        return self.cote_a + self.cote_b + self.cote_c

# Test polymorphisme
formes = [
    Cercle(5),
    Rectangle(4, 6),
    Rectangle(3, 3),  # Carré
    Triangle(6, 4, 3, 4, 5)
]

print("Système de formes géométriques :")
for forme in formes:
    print(forme.info())
    if hasattr(forme, 'est_carre'):
        print(f"  Est un carré: {forme.est_carre()}")
```

### 2. **Hiérarchie de Véhicules**
```python
class Vehicule:
    """Classe de base pour les véhicules"""
    def __init__(self, marque, modele, annee):
        self.marque = marque
        self.modele = modele
        self.annee = annee
        self.kilometrage = 0

    def rouler(self, distance):
        """Méthode de roulage"""
        self.kilometrage += distance
        return f"{self.marque} {self.modele} a roulé {distance} km"

    def info(self):
        return f"{self.marque} {self.modele} ({self.annee}) - {self.kilometrage} km"

class Voiture(Vehicule):
    """Voiture spécifique"""
    def __init__(self, marque, modele, annee, portes=4):
        super().__init__(marque, modele, annee)
        self.portes = portes

    def info(self):
        base = super().info()
        return f"{base} - {self.portes} portes"

class Moto(Vehicule):
    """Moto spécifique"""
    def __init__(self, marque, modele, annee, type_moto="route"):
        super().__init__(marque, modele, annee)
        self.type_moto = type_moto

    def info(self):
        base = super().info()
        return f"{base} - Moto {self.type_moto}"

class Camion(Vehicule):
    """Camion spécifique"""
    def __init__(self, marque, modele, annee, capacite=10):
        super().__init__(marque, modele, annee)
        self.capacite = capacite  # tonnes

    def info(self):
        base = super().info()
        return f"{base} - Capacité {self.capacite}t"

# Test polymorphisme
vehicules = [
    Voiture("Toyota", "Corolla", 2020, 5),
    Moto("Honda", "CBR", 2022, "sport"),
    Camion("Mercedes", "Actros", 2019, 25)
]

print("Flotte de véhicules :")
for vehicule in vehicules:
    print(f"  {vehicule.info()}")

print("\nTest de roulage :")
for vehicule in vehicules:
    print(f"  {vehicule.rouler(100)}")

print("\nAprès roulage :")
for vehicule in vehicules:
    print(f"  {vehicule.info()}")
```

### 3. **Système de Comptes Bancaires**
```python
class Compte:
    """Compte bancaire de base"""
    def __init__(self, titulaire, solde=0):
        self.titulaire = titulaire
        self.solde = solde

    def deposer(self, montant):
        if montant > 0:
            self.solde += montant
            return f"Dépôt de {montant}€"

    def retirer(self, montant):
        if 0 < montant <= self.solde:
            self.solde -= montant
            return f"Retrait de {montant}€"

    def info(self):
        return f"Compte {self.titulaire}: {self.solde}€"

class CompteCourant(Compte):
    """Compte courant avec découvert"""
    def __init__(self, titulaire, solde=0, decouvert_max=-1000):
        super().__init__(titulaire, solde)
        self.decouvert_max = decouvert_max

    def retirer(self, montant):
        if 0 < montant <= self.solde - self.decouvert_max:
            self.solde -= montant
            return f"Retrait de {montant}€ (découvert autorisé)"
        return "Retrait refusé"

    def info(self):
        base = super().info()
        return f"{base} (découvert max: {self.decouvert_max}€)"

class CompteEpargne(Compte):
    """Compte épargne avec intérêts"""
    def __init__(self, titulaire, solde=0, taux_interet=0.02):
        super().__init__(titulaire, solde)
        self.taux_interet = taux_interet

    def calculer_interets(self):
        """Calcule les intérêts"""
        interets = self.solde * self.taux_interet
        self.solde += interets
        return f"Intérêts calculés: +{interets:.2f}€"

    def info(self):
        base = super().info()
        return f"{base} (taux: {self.taux_interet*100:.1f}%)"

# Test
comptes = [
    CompteCourant("Alice", 1000, -500),
    CompteEpargne("Bob", 2000, 0.03)
]

print("Système de comptes bancaires :")
for compte in comptes:
    print(f"  {compte.info()}")

print("\nOpérations :")
print(f"  {comptes[0].retirer(1200)}")  # Avec découvert
print(f"  {comptes[1].calculer_interets()}")
print(f"  {comptes[1].info()}")

# Test du retrait refusé
print(f"  {comptes[0].retirer(2000)}")  # Refusé
```

## 🎯 Défis Supplémentaires

1. **Créez** une classe Animal avec des sous-classes Chien, Chat, Oiseau
2. **Implémentez** une hiérarchie Employé → Manager → Directeur
3. **Développez** un système de formes avec héritage multiple
4. **Concevez** une classe abstraite pour des figures géométriques

---

**Exercices complétés : 214/230** 🎯

*Continuez avec le [chapitre suivant](5-3-encapsulation.md) pour l'encapsulation !*