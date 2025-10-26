# Partie 8.3 : Gestion de Données

## 🎯 Objectifs Pédagogiques

Ce chapitre présente des **projets de gestion de données** complets, combinant bases de données, fichiers, interfaces et algorithmes pour créer des applications fonctionnelles.

### Concepts Intégrés
- **Gestion de contacts** : stockage, recherche, organisation
- **Comptes bancaires** : opérations, historique, sécurité
- **Notes d'étudiants** : moyennes, classements, statistiques
- **Applications** : interfaces, persistance, analyse

---

## 📝 Exercices Pratiques

### Exercice 296 : Gestion d'une liste de contacts
**Objectif** : Créer un système complet de gestion de contacts.

```python
# Solution
class Contact:
    """Représente un contact"""

    def __init__(self, nom, prenom, email, telephone=None, adresse=None):
        """Constructeur"""
        self.nom = nom
        self.prenom = prenom
        self.email = email
        self.telephone = telephone
        self.adresse = adresse

    def __str__(self):
        """Représentation"""
        return f"{self.prenom} {self.nom} ({self.email})"

    def to_dict(self):
        """Conversion en dictionnaire"""
        return {
            "nom": self.nom,
            "prenom": self.prenom,
            "email": self.email,
            "telephone": self.telephone,
            "adresse": self.adresse
        }

    @classmethod
    def from_dict(cls, data):
        """Création depuis dictionnaire"""
        return cls(
            data["nom"],
            data["prenom"],
            data["email"],
            data.get("telephone"),
            data.get("adresse")
        )

class GestionnaireContacts:
    """Système de gestion de contacts"""

    def __init__(self, fichier_sauvegarde="contacts.json"):
        """Constructeur"""
        self.contacts = []
        self.fichier_sauvegarde = fichier_sauvegarde
        self.charger_contacts()

    def ajouter_contact(self, contact):
        """Ajoute un contact"""
        if not any(c.email == contact.email for c in self.contacts):
            self.contacts.append(contact)
            print(f"Contact {contact} ajouté")
            self.sauvegarder_contacts()
            return True
        else:
            print(f"Contact avec email {contact.email} existe déjà")
            return False

    def supprimer_contact(self, email):
        """Supprime un contact par email"""
        for i, contact in enumerate(self.contacts):
            if contact.email == email:
                contact_supprime = self.contacts.pop(i)
                print(f"Contact {contact_supprime} supprimé")
                self.sauvegarder_contacts()
                return True
        print(f"Aucun contact avec l'email {email}")
        return False

    def rechercher_contacts(self, terme):
        """Recherche des contacts par nom, prénom ou email"""
        resultats = []
        terme_lower = terme.lower()

        for contact in self.contacts:
            if (terme_lower in contact.nom.lower() or
                terme_lower in contact.prenom.lower() or
                terme_lower in contact.email.lower()):
                resultats.append(contact)

        return resultats

    def lister_contacts(self):
        """Liste tous les contacts"""
        if not self.contacts:
            print("Aucun contact")
            return []

        print("Liste des contacts :")
        for i, contact in enumerate(self.contacts, 1):
            print(f"{i}. {contact}")
        return self.contacts

    def sauvegarder_contacts(self):
        """Sauvegarde les contacts en JSON"""
        try:
            import json
            with open(self.fichier_sauvegarde, 'w', encoding='utf-8') as f:
                json.dump([c.to_dict() for c in self.contacts], f, indent=2, ensure_ascii=False)
        except Exception as e:
            print(f"Erreur sauvegarde : {e}")

    def charger_contacts(self):
        """Charge les contacts depuis JSON"""
        try:
            import json
            with open(self.fichier_sauvegarde, 'r', encoding='utf-8') as f:
                data = json.load(f)
                self.contacts = [Contact.from_dict(c) for c in data]
        except FileNotFoundError:
            self.contacts = []
        except Exception as e:
            print(f"Erreur chargement : {e}")
            self.contacts = []

# Test du système
print("=== SYSTÈME DE GESTION DE CONTACTS ===")

gestionnaire = GestionnaireContacts()

# Ajout de contacts
contacts_test = [
    Contact("Dupont", "Alice", "alice@email.com", "01-23-45-67-89", "123 Rue A"),
    Contact("Martin", "Bob", "bob@email.com", "01-98-76-54-32", "456 Rue B"),
    Contact("Garcia", "Clara", "clara@email.com", "01-11-22-33-44", "789 Rue C")
]

for contact in contacts_test:
    gestionnaire.ajouter_contact(contact)

# Recherche
print("\n--- Recherche ---")
resultats = gestionnaire.rechercher_contacts("a")
print(f"Contacts trouvés avec 'a' : {len(resultats)}")
for contact in resultats:
    print(f"  {contact}")

# Liste
print("\n--- Liste complète ---")
gestionnaire.lister_contacts()

# Suppression
print("\n--- Suppression ---")
gestionnaire.supprimer_contact("bob@email.com")

# Liste finale
print("\n--- Liste finale ---")
gestionnaire.lister_contacts()
```

**Explication** :
- **Classe Contact** : encapsulation des données
- **GestionnaireContacts** : logique de gestion
- **Persistance JSON** : sauvegarde/chargement
- **Recherche** : par nom, prénom, email
- **Interface** : méthodes d'ajout, suppression, recherche

**Test** : Gérez une liste de contacts avec persistance.

---

### Exercice 297 : Mini gestionnaire de comptes bancaires
**Objectif** : Créer un système de gestion de comptes bancaires.

```python
# Solution
class CompteBancaire:
    """Compte bancaire avec opérations"""

    def __init__(self, numero, titulaire, solde_initial=0):
        """Constructeur"""
        self.numero = numero
        self.titulaire = titulaire
        self.solde = solde_initial
        self.historique = []
        self.date_creation = None

    def deposer(self, montant, description="Dépôt"):
        """Dépose de l'argent"""
        if montant > 0:
            self.solde += montant
            self.historique.append({
                "type": "dépôt",
                "montant": montant,
                "description": description,
                "solde_apres": self.solde
            })
            return f"Dépôt de {montant}€ effectué"
        return "Montant invalide"

    def retirer(self, montant, description="Retrait"):
        """Retire de l'argent"""
        if montant > 0 and self.solde >= montant:
            self.solde -= montant
            self.historique.append({
                "type": "retrait",
                "montant": montant,
                "description": description,
                "solde_apres": self.solde
            })
            return f"Retrait de {montant}€ effectué"
        return "Montant invalide ou fonds insuffisants"

    def transferer(self, autre_compte, montant, description="Transfert"):
        """Transfère vers un autre compte"""
        if montant > 0 and self.solde >= montant:
            self.retirer(montant, f"Transfert vers {autre_compte.numero}")
            autre_compte.deposer(montant, f"Transfert depuis {self.numero}")
            return f"Transfert de {montant}€ vers le compte {autre_compte.numero}"
        return "Transfert impossible"

    def afficher_historique(self):
        """Affiche l'historique des opérations"""
        print(f"Historique du compte {self.numero} :")
        for operation in self.historique[-10:]:  # 10 dernières opérations
            print(f"  {operation['type']}: {operation['montant']}€ - {operation['description']}")

    def __str__(self):
        """Représentation"""
        return f"Compte {self.numero} - {self.titulaire} : {self.solde}€"

class Banque:
    """Système bancaire"""

    def __init__(self):
        """Constructeur"""
        self.comptes = {}
        self.prochain_numero = 1000

    def creer_compte(self, titulaire, solde_initial=0):
        """Crée un nouveau compte"""
        numero = self.prochain_numero
        compte = CompteBancaire(numero, titulaire, solde_initial)
        self.comptes[numero] = compte
        self.prochain_numero += 1
        print(f"Compte {numero} créé pour {titulaire}")
        return numero

    def get_compte(self, numero):
        """Récupère un compte par numéro"""
        return self.comptes.get(numero)

    def lister_comptes(self):
        """Liste tous les comptes"""
        print("Comptes de la banque :")
        for numero, compte in self.comptes.items():
            print(f"  {compte}")

    def bilan_banque(self):
        """Calcule le bilan de la banque"""
        total = sum(compte.solde for compte in self.comptes.values())
        print(f"Bilan de la banque : {total}€ sur {len(self.comptes)} comptes")
        return total

# Test
print("=== SYSTÈME BANCAIRE ===")

banque = Banque()

# Création de comptes
compte1 = banque.creer_compte("Alice Dupont", 1000)
compte2 = banque.creer_compte("Bob Martin", 500)

# Opérations
alice = banque.get_compte(compte1)
bob = banque.get_compte(compte2)

print(f"\n{alice.deposer(200)}")
print(f"{bob.deposer(100)}")

print(f"{alice.retirer(150)}")
print(f"{bob.transferer(alice, 50)}")

# Affichage
print("\n--- États des comptes ---")
alice.afficher_historique()
print()
bob.afficher_historique()

print("\n--- Liste des comptes ---")
banque.lister_comptes()

print("\n--- Bilan ---")
banque.bilan_banque()
```

**Explication** :
- **Classe CompteBancaire** : opérations bancaires
- **Historique** : suivi des opérations
- **Classe Banque** : gestion de plusieurs comptes
- **Transferts** : opérations entre comptes
- **Bilan** : calcul de l'état global

**Test** : Gérez plusieurs comptes bancaires avec opérations.

---

### Exercice 298 : Système de notes pour étudiants
**Objectif** : Créer un système complet de gestion de notes d'étudiants.

```python
# Solution
class Matiere:
    """Représente une matière"""

    def __init__(self, nom, coefficient=1.0):
        """Constructeur"""
        self.nom = nom
        self.coefficient = coefficient
        self.notes = []

    def ajouter_note(self, note):
        """Ajoute une note"""
        if 0 <= note <= 20:
            self.notes.append(note)
            return True
        return False

    def moyenne(self):
        """Calcule la moyenne"""
        if not self.notes:
            return 0
        return sum(self.notes) / len(self.notes)

    def __str__(self):
        """Représentation"""
        return f"{self.nom} (coef: {self.coefficient})"

class Etudiant:
    """Représente un étudiant"""

    def __init__(self, nom, prenom, numero):
        """Constructeur"""
        self.nom = nom
        self.prenom = prenom
        self.numero = numero
        self.matieres = {}

    def ajouter_matiere(self, matiere):
        """Ajoute une matière"""
        self.matieres[matiere.nom] = matiere

    def ajouter_note(self, nom_matiere, note):
        """Ajoute une note à une matière"""
        if nom_matiere in self.matieres:
            return self.matieres[nom_matiere].ajouter_note(note)
        return False

    def moyenne_generale(self):
        """Calcule la moyenne générale"""
        if not self.matieres:
            return 0

        total_pondere = 0
        total_coefficients = 0

        for matiere in self.matieres.values():
            if matiere.notes:  # Seulement les matières avec notes
                total_pondere += matiere.moyenne() * matiere.coefficient
                total_coefficients += matiere.coefficient

        return total_pondere / total_coefficients if total_coefficients > 0 else 0

    def bulletin(self):
        """Affiche le bulletin"""
        print(f"\n=== BULLETIN DE {self.prenom} {self.nom.upper()} ===")
        print(f"Numéro étudiant : {self.numero}")
        print(f"Moyenne générale : {self.moyenne_generale():.2f}/20")

        for nom_matiere, matiere in self.matieres.items():
            print(f"  {matiere}")

    def __str__(self):
        """Représentation"""
        return f"{self.prenom} {self.nom} ({self.numero})"

class Universite:
    """Système de gestion universitaire"""

    def __init__(self):
        """Constructeur"""
        self.etudiants = {}

    def ajouter_etudiant(self, etudiant):
        """Ajoute un étudiant"""
        self.etudiants[etudiant.numero] = etudiant
        print(f"Étudiant {etudiant} ajouté")

    def get_etudiant(self, numero):
        """Récupère un étudiant"""
        return self.etudiants.get(numero)

    def classement(self):
        """Retourne le classement par moyenne"""
        etudiants_avec_notes = [(e.moyenne_generale(), e) for e in self.etudiants.values() if e.matieres]
        etudiants_avec_notes.sort(reverse=True, key=lambda x: x[0])

        print("Classement des étudiants :")
        for i, (moyenne, etudiant) in enumerate(etudiants_avec_notes, 1):
            print(f"{i}. {etudiant} : {moyenne:.2f}/20")

        return etudiants_avec_notes

    def statistiques(self):
        """Calcule les statistiques générales"""
        if not self.etudiants:
            return {}

        moyennes = [e.moyenne_generale() for e in self.etudiants.values() if e.matieres]

        if not moyennes:
            return {"nombre_etudiants": len(self.etudiants), "moyenne_generale": 0}

        return {
            "nombre_etudiants": len(self.etudiants),
            "moyenne_generale": sum(moyennes) / len(moyennes),
            "meilleure_moyenne": max(moyennes),
            "moins_bonne_moyenne": min(moyennes)
        }

# Test
print("=== SYSTÈME DE NOTES UNIVERSITAIRE ===")

universite = Universite()

# Création d'étudiants
etudiants = [
    Etudiant("Dupont", "Alice", "ETU001"),
    Etudiant("Martin", "Bob", "ETU002"),
    Etudiant("Garcia", "Clara", "ETU003")
]

for etudiant in etudiants:
    universite.ajouter_etudiant(etudiant)

# Ajout de matières
matieres = [
    Matiere("Mathématiques", 3.0),
    Matiere("Physique", 2.0),
    Matiere("Informatique", 2.0),
    Matiere("Anglais", 1.0)
]

for etudiant in etudiants:
    for matiere in matieres:
        etudiant.ajouter_matiere(matiere)

# Ajout de notes
notes_test = [
    ("ETU001", "Mathématiques", 18),
    ("ETU001", "Physique", 16),
    ("ETU001", "Informatique", 19),
    ("ETU001", "Anglais", 15),

    ("ETU002", "Mathématiques", 12),
    ("ETU002", "Physique", 14),
    ("ETU002", "Informatique", 13),
    ("ETU002", "Anglais", 11),

    ("ETU003", "Mathématiques", 17),
    ("ETU003", "Physique", 18),
    ("ETU003", "Informatique", 16),
    ("ETU003", "Anglais", 14)
]

for numero, matiere, note in notes_test:
    etudiant = universite.get_etudiant(numero)
    etudiant.ajouter_note(matiere, note)

# Affichage des bulletins
for etudiant in etudiants:
    etudiant.bulletin()

# Classement
print("\n--- Classement ---")
universite.classement()

# Statistiques
print("\n--- Statistiques ---")
stats = universite.statistiques()
for cle, valeur in stats.items():
    print(f"{cle}: {valeur}")
```

**Explication** :
- **Matiere** : gestion des notes par matière
- **Etudiant** : gestion des matières et moyennes
- **Universite** : gestion globale des étudiants
- **Classement** : tri par moyennes
- **Statistiques** : calculs globaux

**Test** : Gérez un système complet de notes universitaires.

---

### Exercice 299 : Mini analyse de texte : fréquences de mots
**Objectif** : Créer un analyseur de fréquences de mots dans un texte.

```python
# Solution
import re
from collections import Counter

class AnalyseurTexte:
    """Analyseur de texte avec statistiques"""

    def __init__(self, texte):
        """Constructeur"""
        self.texte_original = texte
        self.mots = self._extraire_mots()
        self.frequences = Counter(self.mots)

    def _extraire_mots(self):
        """Extrait les mots du texte"""
        # Nettoyage et extraction
        texte_nettoye = re.sub(r'[^\w\s]', '', self.texte_original.lower())
        mots = re.findall(r'\b\w+\b', texte_nettoye)
        return mots

    def mots_plus_frequents(self, n=10):
        """Retourne les n mots les plus fréquents"""
        return self.frequences.most_common(n)

    def mots_rares(self, seuil=1):
        """Retourne les mots qui apparaissent <= seuil fois"""
        return [mot for mot, freq in self.frequences.items() if freq <= seuil]

    def statistiques(self):
        """Calcule les statistiques du texte"""
        if not self.mots:
            return {}

        return {
            "mots_total": len(self.mots),
            "mots_uniques": len(self.frequences),
            "mots_moyens_par_phrase": len(self.mots) / len(re.findall(r'[.!?]+', self.texte_original)) if re.findall(r'[.!?]+', self.texte_original) else 0,
            "longueur_moyenne_mot": sum(len(mot) for mot in self.mots) / len(self.mots),
            "vocabulaire_riche": len(self.frequences) / len(self.mots) * 100
        }

    def generer_resume(self):
        """Génère un résumé des statistiques"""
        stats = self.statistiques()
        plus_frequents = self.mots_plus_frequents(5)

        resume = f"""
=== ANALYSE DU TEXTE ===

📊 Statistiques :
- Mots total : {stats['mots_total']}
- Mots uniques : {stats['mots_uniques']}
- Vocabulaire riche : {stats['vocabulaire_riche']:.1f}%
- Longueur moyenne des mots : {stats['longueur_moyenne_mot']:.1f} caractères

🔥 Mots les plus fréquents :
"""
        for mot, freq in plus_frequents:
            resume += f"  '{mot}': {freq} fois\n"

        rares = self.mots_rares(1)
        if rares:
            resume += f"\n❓ Mots rares (1 occurrence) : {len(rares)} mots\n"

        return resume

# Test
texte_test = """
Le Python est un langage de programmation très populaire.
Python est facile à apprendre et Python est puissant.
Les programmeurs aiment Python pour sa simplicité et sa polyvalence.
Python est utilisé dans de nombreux domaines comme le développement web,
l'intelligence artificielle, l'analyse de données et bien d'autres.
"""

analyseur = AnalyseurTexte(texte_test)
print(analyseur.generer_resume())

# Test avec un autre texte
texte2 = "Le chat dort. Le chien court. Le chat mange. Le chien dort."
analyseur2 = AnalyseurTexte(texte2)
print("\n" + "="*50)
print(analyseur2.generer_resume())
```

**Explication** :
- **AnalyseurTexte** : classe d'analyse de texte
- **Extraction de mots** : nettoyage et tokenisation
- **Frequences** : Counter pour le comptage
- **Statistiques** : calculs sur le vocabulaire
- **Resume** : génération de rapport

**Test** : Analysez les fréquences de mots dans différents textes.

---

### Exercice 300 : Projet final combinant OOP, fichiers et algorithmes
**Objectif** : Créer un projet complet intégrant tous les concepts.

```python
# Solution - Système de Gestion de Bibliothèque Avancé
import json
import sqlite3
from datetime import datetime
from collections import Counter

class Livre:
    """Représente un livre"""

    def __init__(self, titre, auteur, isbn, genre="Général", disponible=True):
        """Constructeur"""
        self.titre = titre
        self.auteur = auteur
        self.isbn = isbn
        self.genre = genre
        self.disponible = disponible
        self.date_ajout = datetime.now()
        self.emprunts = []

    def emprunter(self, utilisateur):
        """Emprunte le livre"""
        if self.disponible:
            self.disponible = False
            self.emprunts.append({
                "utilisateur": utilisateur,
                "date_emprunt": datetime.now(),
                "date_retour": None
            })
            return f"Livre '{self.titre}' emprunté par {utilisateur}"
        return f"Livre '{self.titre}' non disponible"

    def rendre(self, utilisateur):
        """Rend le livre"""
        for emprunt in self.emprunts:
            if emprunt["utilisateur"] == utilisateur and emprunt["date_retour"] is None:
                emprunt["date_retour"] = datetime.now()
                self.disponible = True
                return f"Livre '{self.titre}' rendu par {utilisateur}"

        return f"Aucun emprunt actif pour {utilisateur}"

    def to_dict(self):
        """Conversion en dictionnaire"""
        return {
            "titre": self.titre,
            "auteur": self.auteur,
            "isbn": self.isbn,
            "genre": self.genre,
            "disponible": self.disponible,
            "date_ajout": self.date_ajout.isoformat(),
            "emprunts": self.emprunts
        }

    def __str__(self):
        """Représentation"""
        statut = "Disponible" if self.disponible else "Emprunté"
        return f"{self.titre} ({self.auteur}) - {statut}"

class Bibliotheque:
    """Système de gestion de bibliothèque"""

    def __init__(self, nom="Ma Bibliothèque"):
        """Constructeur"""
        self.nom = nom
        self.livres = {}
        self.utilisateurs = set()
        self.charger_donnees()

    def ajouter_livre(self, livre):
        """Ajoute un livre"""
        if livre.isbn not in self.livres:
            self.livres[livre.isbn] = livre
            self.sauvegarder_donnees()
            print(f"Livre '{livre.titre}' ajouté")
            return True
        print(f"Livre avec ISBN {livre.isbn} existe déjà")
        return False

    def rechercher_livres(self, terme):
        """Recherche des livres"""
        resultats = []
        terme_lower = terme.lower()

        for livre in self.livres.values():
            if (terme_lower in livre.titre.lower() or
                terme_lower in livre.auteur.lower() or
                terme_lower in livre.genre.lower()):
                resultats.append(livre)

        return resultats

    def emprunter_livre(self, isbn, utilisateur):
        """Emprunte un livre"""
        if isbn in self.livres:
            self.utilisateurs.add(utilisateur)
            return self.livres[isbn].emprunter(utilisateur)
        return f"Livre avec ISBN {isbn} non trouvé"

    def rendre_livre(self, isbn, utilisateur):
        """Rend un livre"""
        if isbn in self.livres:
            return self.livres[isbn].rendre(utilisateur)
        return f"Livre avec ISBN {isbn} non trouvé"

    def statistiques(self):
        """Calcule les statistiques"""
        total_livres = len(self.livres)
        livres_disponibles = sum(1 for l in self.livres.values() if l.disponible)
        total_emprunts = sum(len(livre.emprunts) for livre in self.livres.values())

        # Genres les plus populaires
        genres = Counter(livre.genre for livre in self.livres.values())
        genre_plus_populaire = genres.most_common(1)[0] if genres else ("Aucun", 0)

        return {
            "total_livres": total_livres,
            "livres_disponibles": livres_disponibles,
            "livres_empruntes": total_livres - livres_disponibles,
            "total_utilisateurs": len(self.utilisateurs),
            "total_emprunts": total_emprunts,
            "genre_plus_populaire": genre_plus_populaire
        }

    def sauvegarder_donnees(self):
        """Sauvegarde les données en JSON"""
        try:
            with open("bibliotheque.json", 'w', encoding='utf-8') as f:
                json.dump({
                    "nom": self.nom,
                    "livres": {isbn: livre.to_dict() for isbn, livre in self.livres.items()},
                    "utilisateurs": list(self.utilisateurs)
                }, f, indent=2, ensure_ascii=False, default=str)
        except Exception as e:
            print(f"Erreur sauvegarde : {e}")

    def charger_donnees(self):
        """Charge les données depuis JSON"""
        try:
            with open("bibliotheque.json", 'r', encoding='utf-8') as f:
                data = json.load(f)

            self.nom = data.get("nom", self.nom)
            self.utilisateurs = set(data.get("utilisateurs", []))

            for isbn, livre_data in data.get("livres", {}).items():
                livre = Livre(
                    livre_data["titre"],
                    livre_data["auteur"],
                    isbn,
                    livre_data.get("genre", "Général"),
                    livre_data.get("disponible", True)
                )
                livre.emprunts = livre_data.get("emprunts", [])
                self.livres[isbn] = livre

        except FileNotFoundError:
            pass  # Première utilisation
        except Exception as e:
            print(f"Erreur chargement : {e}")

    def menu(self):
        """Affiche le menu principal"""
        print(f"\n=== BIBLIOTHÈQUE : {self.nom} ===")
        print("1. Ajouter un livre")
        print("2. Rechercher des livres")
        print("3. Emprunter un livre")
        print("4. Rendre un livre")
        print("5. Afficher statistiques")
        print("6. Lister tous les livres")
        print("7. Quitter")

    def run(self):
        """Lance l'application"""
        print("📚 SYSTÈME DE GESTION DE BIBLIOTHÈQUE 📚")

        while True:
            self.menu()
            choix = input("Votre choix (1-7) : ").strip()

            if choix == "1":
                # Ajouter un livre
                titre = input("Titre : ")
                auteur = input("Auteur : ")
                isbn = input("ISBN : ")
                genre = input("Genre (optionnel) : ") or "Général"

                livre = Livre(titre, auteur, isbn, genre)
                self.ajouter_livre(livre)

            elif choix == "2":
                # Rechercher
                terme = input("Terme de recherche : ")
                resultats = self.rechercher_livres(terme)
                print(f"{len(resultats)} livre(s) trouvé(s) :")
                for livre in resultats:
                    print(f"  {livre}")

            elif choix == "3":
                # Emprunter
                isbn = input("ISBN du livre : ")
                utilisateur = input("Nom de l'utilisateur : ")
                print(self.emprunter_livre(isbn, utilisateur))

            elif choix == "4":
                # Rendre
                isbn = input("ISBN du livre : ")
                utilisateur = input("Nom de l'utilisateur : ")
                print(self.rendre_livre(isbn, utilisateur))

            elif choix == "5":
                # Statistiques
                stats = self.statistiques()
                print("📊 STATISTIQUES 📊")
                for cle, valeur in stats.items():
                    if cle == "genre_plus_populaire":
                        print(f"Genre le plus populaire : {valeur[0]} ({valeur[1]} livres)")
                    else:
                        print(f"{cle}: {valeur}")

            elif choix == "6":
                # Liste des livres
                print("📖 LISTE DES LIVRES 📖")
                for livre in self.livres.values():
                    print(f"  {livre}")

            elif choix == "7":
                print("Merci d'avoir utilisé le système de bibliothèque !")
                self.sauvegarder_donnees()
                break

            else:
                print("Choix invalide. Essayez 1-7.")

# Test
if __name__ == "__main__":
    bibliotheque = Bibliotheque("Bibliothèque Municipale")
    bibliotheque.run()
```

**Explication** :
- **Système complet** : bibliothèque avec livres et utilisateurs
- **Persistance JSON** : sauvegarde/chargement automatique
- **Recherche** : par titre, auteur, genre
- **Emprunts** : gestion des prêts et retours
- **Statistiques** : analyse des données
- **Interface interactive** : menu et interactions

**Test** : Utilisez le système complet de gestion de bibliothèque.

---

## 🔍 Points Clés à Retenir

### 1. **Architecture d'Application**
```python
# Classes principales
class DomaineMetier:
    def __init__(self, attributs):
        self.attributs = attributs

    def methodes_metier(self):
        pass

class Gestionnaire:
    def __init__(self):
        self.elements = {}

    def ajouter(self, element):
        self.elements[element.id] = element

    def rechercher(self, critere):
        return [e for e in self.elements.values() if critere(e)]
```

### 2. **Persistance de Données**
```python
# Sauvegarde
def sauvegarder(self):
    with open(self.fichier, 'w') as f:
        json.dump(self.to_dict(), f, indent=2)

# Chargement
def charger(self):
    try:
        with open(self.fichier, 'r') as f:
            data = json.load(f)
            self.from_dict(data)
    except FileNotFoundError:
        pass
```

### 3. **Interface Utilisateur**
```python
def menu(self):
    print("1. Option 1")
    print("2. Option 2")
    choix = input("Choix : ")
    return choix

def run(self):
    while True:
        choix = self.menu()
        if choix == "1":
            self.option1()
        elif choix == "2":
            self.option2()
        else:
            break
```

## 💡 Optimisations et Astuces

### 1. **Système de Configuration**
```python
class ConfigManager:
    def __init__(self):
        self.config = self._charger_config()

    def _charger_config(self):
        try:
            with open("config.json", "r") as f:
                return json.load(f)
        except:
            return self._config_defaut()
```

### 2. **Logging et Audit**
```python
def log_operation(self, operation, details):
    with open("audit.log", "a") as f:
        timestamp = datetime.now().isoformat()
        f.write(f"{timestamp} - {operation}: {details}\n")
```

### 3. **Export/Import**
```python
def exporter_csv(self, fichier):
    with open(fichier, 'w', newline='') as f:
        writer = csv.writer(f)
        # Export des données
```

## 🚀 Applications Pratiques

### 1. **Système de Gestion d'Inventaire**
```python
# Classe Produit
class Produit:
    def __init__(self, nom, prix, quantite):
        self.nom = nom
        self.prix = prix
        self.quantite = quantite

# Gestionnaire d'inventaire
class Inventaire:
    def __init__(self):
        self.produits = {}

    def ajouter_produit(self, produit):
        self.produits[produit.nom] = produit

    def valeur_totale(self):
        return sum(p.prix * p.quantite for p in self.produits.values())

# Interface utilisateur
def menu_inventaire():
    print("1. Ajouter produit")
    print("2. Voir inventaire")
    print("3. Valeur totale")
    choix = input("Choix : ")
    return choix
```

### 2. **Analyseur de Performances**
```python
# Classe de mesure
class PerformanceMonitor:
    def __init__(self):
        self.mesures = []

    def mesurer(self, nom_operation, fonction):
        debut = time.time()
        resultat = fonction()
        fin = time.time()
        duree = fin - debut
        self.mesures.append((nom_operation, duree))
        return resultat, duree
```

### 3. **Système de Tâches**
```python
# Classe Tache
class Tache:
    def __init__(self, description, priorite):
        self.description = description
        self.priorite = priorite
        self.terminee = False

# Gestionnaire de tâches
class TodoList:
    def __init__(self):
        self.taches = []

    def ajouter_tache(self, tache):
        self.taches.append(tache)

    def taches_en_cours(self):
        return [t for t in self.taches if not t.terminee]
```

## 🎯 Bilan de la Partie 8

### Concepts Maîtrisés
✅ **Jeux interactifs** : pendu, devinette, score
✅ **Validation** : parenthèses, HTML, parsing
✅ **Gestion de données** : contacts, comptes, notes
✅ **Analyse de texte** : fréquences, statistiques
✅ **Projets intégrés** : bibliothèque, applications complètes
✅ **Interfaces utilisateur** : menus, interactions

### Compétences Développées
- **Conception d'applications** : architecture, interfaces
- **Gestion de données** : stockage, recherche, persistance
- **Logique métier** : règles, validations, calculs
- **Interface utilisateur** : ergonomie, feedback
- **Intégration** : fichiers, bases de données, algorithmes

---

**🏁 FIN DE LA PARTIE 8 - BRAVO !**

**Exercices complétés : 300/300** 🎯

*Félicitations ! Vous avez terminé les 300 exercices Python. Vous êtes maintenant prêt à créer des applications complètes et sophistiquées !* 

## 🎉 RÉCAPITULATIF COMPLET

### ✅ **MISSION ACCOMPLIE !**

**8 Parties - 300 Exercices - Programmation Python Complète**

1. **Partie 1** : Bases de Python (50 exercices)
   - Types de données, opérations, entrées/sorties, chaînes

2. **Partie 2** : Contrôle de flux (50 exercices) 
   - Conditions, boucles, manipulation de listes, transformations

3. **Partie 3** : Fonctions et modules (50 exercices)
   - Fonctions, récursivité, lambda, modules standard

4. **Partie 4** : Structures de données (50 exercices)
   - Listes, tuples, dictionnaires, ensembles, compréhensions

5. **Partie 5** : Programmation orientée objet (30 exercices)
   - Classes, héritage, polymorphisme, encapsulation, surcharge

6. **Partie 6** : Fichiers et bases de données (30 exercices)
   - Fichiers texte, CSV, JSON, SQLite, gestion système

7. **Partie 7** : Algorithmes et mathématiques (25 exercices)
   - Nombres, statistiques, chaînes, cryptographie, binaires

8. **Partie 8** : Projets avancés (15 exercices)
   - Jeux, validation, gestion de données, applications intégrées

### 🚀 **COMPÉTENCES ACQUISES**

- **Programmation de base** : syntaxe, types, opérations
- **Logique algorithmique** : conditions, boucles, fonctions
- **Structures de données** : listes, dictionnaires, ensembles
- **Programmation orientée objet** : classes, héritage, polymorphisme
- **Gestion de fichiers** : lecture, écriture, bases de données
- **Algorithmes** : tri, recherche, optimisation
- **Applications pratiques** : jeux, analyse, gestion

### 📚 **RESSOURCES COMPLÉMENTAIRES**

- **Documentation Python** : docs.python.org
- **Tutoriels** : Real Python, Python.org
- **Exercices** : LeetCode, HackerRank, Codewars
- **Projets** : GitHub, portfolio personnel

### 🎯 **PROCHAINES ÉTAPES**

1. **Pratiquez quotidiennement** : 30 minutes par jour
2. **Créez des projets personnels** : applications utiles
3. **Contribuez à l'open source** : GitHub
4. **Étudiez des frameworks** : Django, Flask, Pandas
5. **Explorez l'IA/ML** : TensorFlow, scikit-learn

**Vous êtes maintenant un développeur Python compétent !** 🌟
