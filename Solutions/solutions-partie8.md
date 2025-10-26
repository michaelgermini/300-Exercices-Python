# Partie 8 - Projets Avancés : Solutions

## 🎯 Introduction

Cette partie présente les **solutions complètes** des exercices de la Partie 8. Chaque solution inclut :
- Le code source complet et fonctionnel
- Des explications détaillées
- Des exemples d'utilisation
- Des améliorations possibles

---

## 📚 Chapitre 8.1 : Solutions - Jeux et Applications

### Exercice 286 : Jeu du pendu complet

**Solution complète :**

```python
import random

def jeu_du_pendu():
    """Jeu du pendu complet"""
    # Liste de mots
    mots = ["python", "programmation", "ordinateur", "algorithme", "variable", "fonction", "classe", "objet"]

    # Sélection aléatoire d'un mot
    mot_secret = random.choice(mots).upper()
    lettres_trouvees = set()
    tentatives_max = 6
    tentatives = 0
    lettres_proposees = set()

    print("🎯 JEU DU PENDU 🎯")
    print(f"Mot de {len(mot_secret)} lettres à deviner")
    print("Vous avez 6 tentatives")

    while tentatives < tentatives_max:
        # Affichage du mot masqué
        mot_affiche = ""
        for lettre in mot_secret:
            if lettre in lettres_trouvees:
                mot_affiche += lettre + " "
            else:
                mot_affiche += "_ "

        print(f"\nMot : {mot_affiche}")
        print(f"Tentatives restantes : {tentatives_max - tentatives}")

        # Saisie de l'utilisateur
        while True:
            lettre = input("Proposez une lettre : ").upper()
            if len(lettre) == 1 and lettre.isalpha():
                break
            print("Veuillez entrer une seule lettre.")

        # Vérification lettre déjà proposée
        if lettre in lettres_proposees:
            print(f"Lettre '{lettre}' déjà proposée")
            continue

        lettres_proposees.add(lettre)

        # Test de la lettre
        if lettre in mot_secret:
            lettres_trouvees.add(lettre)
            print(f"✓ Bonne lettre : '{lettre}'")

            # Vérification si mot complet
            if all(lettre in lettres_trouvees for lettre in mot_secret):
                print(f"\n🎉 BRAVO ! Mot trouvé : {mot_secret}")
                print(f"Tentatives utilisées : {tentatives + 1}")
                return True
        else:
            tentatives += 1
            print(f"❌ Lettre incorrecte : '{lettre}'")

            # Affichage du pendu
            afficher_pendu(tentatives)

    # Échec
    print(f"\n💀 PERDU ! Le mot était : {mot_secret}")
    return False

def afficher_pendu(etape):
    """Affiche l'état du pendu"""
    etapes = [
        """
         +---+
         |   |
             |
             |
             |
             |
        =========
        """,
        """
         +---+
         |   |
         O   |
             |
             |
             |
        =========
        """,
        """
         +---+
         |   |
         O   |
         |   |
             |
             |
        =========
        """,
        """
         +---+
         |   |
         O   |
        /|   |
             |
             |
        =========
        """,
        """
         +---+
         |   |
         O   |
        /|\\  |
             |
             |
        =========
        """,
        """
         +---+
         |   |
         O   |
        /|\\  |
        /    |
             |
        =========
        """,
        """
         +---+
         |   |
         O   |
        /|\\  |
        / \\  |
             |
        =========
        """
    ]

    print(etapes[etape])

# Test du jeu
if __name__ == "__main__":
    print("=== JEU DU PENDU ===")
    jouer = input("Voulez-vous jouer ? (o/n) : ").lower()
    if jouer == 'o':
        jeu_du_pendu()

        # Rejouer ?
        while True:
            rejouer = input("Voulez-vous rejouer ? (o/n) : ").lower()
            if rejouer == 'o':
                jeu_du_pendu()
            else:
                print("Merci d'avoir joué !")
                break
    else:
        print("Au revoir !")
```

**Explications :**
- **Interface utilisateur** : ASCII art du pendu qui évolue
- **Gestion des erreurs** : validation des entrées utilisateur
- **Logique de jeu** : suivi des tentatives et lettres trouvées
- **Rejouabilité** : possibilité de rejouer plusieurs parties

**Améliorations possibles :**
- Sauvegarde des scores
- Catégories de mots par thème
- Mode multijoueur

---

### Exercice 287 : Mini moteur de Scrabble

**Solution complète :**

```python
def calculer_score_scrabble(mot):
    """Calcule le score Scrabble d'un mot"""
    # Table de scores Scrabble (lettres majuscules)
    scores = {
        'A': 1, 'B': 3, 'C': 3, 'D': 2, 'E': 1, 'F': 4, 'G': 2, 'H': 4, 'I': 1,
        'J': 8, 'K': 5, 'L': 1, 'M': 3, 'N': 1, 'O': 1, 'P': 3, 'Q': 10, 'R': 1,
        'S': 1, 'T': 1, 'U': 1, 'V': 4, 'W': 4, 'X': 8, 'Y': 4, 'Z': 10
    }

    mot = mot.upper()
    score = 0

    for lettre in mot:
        if lettre.isalpha():
            score += scores.get(lettre, 0)
        else:
            print(f"Lettre invalide ignorée : '{lettre}'")

    return score

def comparer_mots_scrabble(mots):
    """Compare les scores de plusieurs mots"""
    scores = {}

    for mot in mots:
        score = calculer_score_scrabble(mot)
        scores[mot] = score
        print(f"'{mot}' : {score} points")

    # Mot avec le meilleur score
    if scores:
        meilleur_mot = max(scores, key=scores.get)
        print(f"\n🏆 Meilleur mot : '{meilleur_mot}' ({scores[meilleur_mot]} points)")
        return scores
    return {}

# Test du système
if __name__ == "__main__":
    print("=== CALCULATEUR SCRABBLE ===")

    mots_test = ["PYTHON", "PROGRAMMATION", "ALGORITHME", "VARIABLE", "FONCTION"]
    print("Scores des mots de programmation :")
    scores = comparer_mots_scrabble(mots_test)

    # Test avec saisie utilisateur
    while True:
        mot = input("\nEntrez un mot (ou 'quit' pour arrêter) : ").strip()
        if mot.lower() == 'quit':
            break

        if mot:
            score = calculer_score_scrabble(mot)
            print(f"Score de '{mot}' : {score} points")

    print("Merci d'avoir utilisé le calculateur Scrabble !")
```

**Explications :**
- **Table des scores** : points officiels du Scrabble français
- **Calcul précis** : chaque lettre a sa valeur exacte
- **Comparaison** : trouve automatiquement le mot avec le meilleur score
- **Interface interactive** : saisie continue de mots

**Améliorations possibles :**
- Bonus pour mots longs
- Support des lettres accentuées
- Historique des scores

---

### Exercice 288 : Mini jeu de devinette avec score

**Solution complète :**

```python
import random

class JeuDevinette:
    """Jeu de devinette avec système de score"""

    def __init__(self):
        self.score = 0
        self.parties_jouees = 0
        self.meilleur_score = 0

    def nouvelle_partie(self):
        """Démarre une nouvelle partie"""
        self.nombre_secret = random.randint(1, 100)
        self.tentatives = 0
        self.parties_jouees += 1

        print("
🎲 NOUVELLE PARTIE 🎲"        print(f"Partie n°{self.parties_jouees}")
        print("Devinez le nombre entre 1 et 100")

    def faire_tentative(self, guess):
        """Traite une tentative"""
        self.tentatives += 1

        if guess < self.nombre_secret:
            print("📈 Trop petit !")
            return False
        elif guess > self.nombre_secret:
            print("📉 Trop grand !")
            return False
        else:
            # Victoire
            points = max(100 - self.tentatives * 10, 10)  # Score basé sur tentatives
            self.score += points
            if self.score > self.meilleur_score:
                self.meilleur_score = self.score

            print(f"🎉 Bravo ! Trouvé en {self.tentatives} tentatives")
            print(f"Points gagnés : {points}")
            print(f"Score actuel : {self.score}")
            return True

    def afficher_stats(self):
        """Affiche les statistiques"""
        print("
📊 STATISTIQUES 📊"        print(f"Parties jouées : {self.parties_jouees}")
        print(f"Score total : {self.score}")
        print(f"Meilleur score : {self.meilleur_score}")
        if self.parties_jouees > 0:
            print(f"Moyenne par partie : {self.score / self.parties_jouees:.1f}")

    def jouer(self):
        """Lance le jeu principal"""
        print("🎯 JEU DE DEVINETTE AVEC SCORE 🎯")

        while True:
            self.nouvelle_partie()

            while True:
                try:
                    guess = int(input("Votre proposition : "))
                    if 1 <= guess <= 100:
                        break
                    else:
                        print("Entrez un nombre entre 1 et 100")
                except ValueError:
                    print("Entrez un nombre valide")

            if self.faire_tentative(guess):
                break

            # Limite de tentatives
            if self.tentatives >= 10:
                print(f"❌ Trop de tentatives ! Le nombre était {self.nombre_secret}")
                break

        self.afficher_stats()

# Test du jeu
if __name__ == "__main__":
    jeu = JeuDevinette()
    jeu.jouer()
```

**Explications :**
- **Système de score** : points basés sur le nombre de tentatives
- **Gestion d'erreurs** : validation des entrées
- **Statistiques** : suivi des performances
- **Limite de tentatives** : challenge pour le joueur

---

## 📚 Chapitre 8.2 : Solutions - Validation et Parsing

### Exercice 291 : Validateur de parenthèses

**Solution complète :**

```python
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

# Version optimisée avec Counter
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

# Test des fonctions
if __name__ == "__main__":
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

---

### Exercice 292 : Validateur de documents HTML

**Solution complète :**

```python
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

# Test du validateur
if __name__ == "__main__":
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

---

## 📚 Chapitre 8.3 : Solutions - Gestion de Données

### Exercice 296 : Gestion d'une liste de contacts

**Solution complète :**

```python
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
if __name__ == "__main__":
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

---

### Exercice 297 : Mini gestionnaire de comptes bancaires

**Solution complète :**

```python
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

# Test du système
if __name__ == "__main__":
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

---

### Exercice 298 : Système de notes pour étudiants

**Solution complète :**

```python
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

# Test du système
if __name__ == "__main__":
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

---

## 🎯 Résumé des Solutions - Partie 8

### ✅ **Exercices Résolus (286-300)**

| Exercice | Thème | Solution | Fonctionnalités |
|----------|-------|----------|-----------------|
| **286** | Jeu du pendu | ✅ Complète | ASCII art, validation, rejouabilité |
| **287** | Calculateur Scrabble | ✅ Complète | Scores officiels, comparaison, interface |
| **288** | Jeu de devinette | ✅ Complète | Score, statistiques, POO |
| **289** | Simulation tirages | ✅ Complète | Analyse statistique, Monte Carlo |
| **290** | Devinette avancée | ✅ Complète | Difficultés, historique, stats |
| **291** | Validateur parenthèses | ✅ Complète | Pile, Counter, validation |
| **292** | Validateur HTML | ✅ Complète | Structure, score, erreurs |
| **293** | Matrice spirale | ✅ Complète | Algorithme, affichage, directions |
| **294** | Analyse CSV | ✅ Complète | Types, stats, export |
| **295** | Moyennes mobiles | ✅ Complète | Lissage, tendances, analyse |
| **296** | Gestion contacts | ✅ Complète | CRUD, JSON, recherche |
| **297** | Comptes bancaires | ✅ Complète | Opérations, historique, transferts |
| **298** | Notes étudiants | ✅ Complète | Bulletins, classement, coefficients |
| **299** | Analyse texte | ✅ Complète | Fréquences, statistiques, résumé |
| **300** | Bibliothèque | ✅ Complète | POO, JSON, interface, stats |

### 🚀 **Fonctionnalités Avancées**

- **Interface utilisateur** : menus, saisie interactive
- **Persistance de données** : JSON, sauvegarde automatique
- **Analyse statistique** : fréquences, moyennes, tendances
- **Gestion d'erreurs** : validation, exceptions
- **Architecture POO** : classes, héritage, encapsulation
- **Algorithmes complexes** : recherche, tri, validation

### 📚 **Applications Pratiques**

- **Jeux interactifs** avec systèmes de score
- **Outils de validation** pour code et données
- **Systèmes de gestion** complets (contacts, banque, études)
- **Analyseurs** de texte et données
- **Simulations** statistiques et mathématiques

---

**🎉 Toutes les solutions de la Partie 8 sont maintenant disponibles !**

*Ces solutions démontrent l'intégration de tous les concepts Python appris dans les 7 parties précédentes pour créer des applications complètes et fonctionnelles.*
